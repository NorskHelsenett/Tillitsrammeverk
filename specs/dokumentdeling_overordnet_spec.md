# Overordnet spesifikasjon for tilgangskontroll i dokumentdeling i KJ
Målgruppe: EPJ leverandører og konsumenter

To ulike tilnærminger til å autentisere sluttbruker:
1. HP logger seg inn i EPJ via HelseID (og får SSO til KJ)
2. HP logger seg inn via HelseID når HP åpner KJ-Portal og det ikke er en aktiv sesjon i HelseID

## Sekvensdiagram for leverandør
Diagrammet er forenklet og fokuserer på leverandørens oppgaver og ansvar i forbindelse med integrasjon..

````mermaid
sequenceDiagram 
  autonumber
  title Beskrivelse av ....
  actor HP as Helsepersonell
  participant EPJ
  participant HelseID
  participant KJP
  participant Dokumentkilde

  HP->>EPJ: Velger pasient
  EPJ->>EPJ: generer_assertion(virksomhet, pasientid)
  EPJ->>HelseID: getToken(assertion)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST /helseindikator/ (accesstoken + body)
  KJP-->>EPJ: pasientstatus + ticket(pasientens nin)
  HP->>EPJ: Åpner KJP
  EPJ->>HelseID: Authorize kall (client_assertion)
  HelseID-->>EPJ: code_1
  EPJ->>HelseID: /Token (authorization_details + code_1)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST KJ-API/session/create (authorization: Access Token, body: ticket + sha256(nonce))
  KJP-->>EPJ: code_2
  EPJ->>KJP: GET hentpasient.html?otc=Code_2&nonce=nonce
  KJP-->>KJP: hent access token og ticket(code_2, nonce)
  HP->>KJP: Åpner fanen journaldokumenter
  KJP->>Dokumentkilde: Hent referanseliste (token)
 
  Dokumentkilde-->>Dokumentkilde: Valider token
  Dokumentkilde-->KJP: referanseliste (metadata)
 
  KJP-->>HP: Viser referanseliste
  HP->>KJP: Åpner et journaldokument
  KJP->>Dokumentkilde: Hent dokument (referanse + token)
  Dokumentkilde-->>Dokumentkilde: validerer token
  Dokumentkilde-->>KJP: dokument
  KJP-->>HP: vise dokument

  critical sjekk gyldighet på access token

    option Access token er utløpt
        EPJ->>HelseID: POST token (refresh grant)
        HelseID-->>EPJ: Access Token
        EPJ->>KJP: POST KJ-API/session/refresh (access token) 
        KJP-->>EPJ: HTTP 200 (OK)
    
    option Access token er gyldig
        EPJ->>EPJ: schedule refresh
  end

  critical helsepersonell bytter pasient
  option session er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)
  end
  
  critical brukersesjon i EPJ timer ut
  option session er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)
  end

  critical brukeren lukker EPJ system
  option session er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)

end 
````

# Spesifikasjon
Dette er hva leverandøren må utvikle

## pkt: 2, 3 og 5 i sekvensdiagrammet: Hent token og kall helseindikator

For å få utlevert en ticket til bruk i Kjernejournal portal, må leverandøren be om et Access Token fra HelseID, og bruke dette tokenet i et POST-kall mot /helseindikator-endepunktet i KJ.

Punkt 2: generer en `client_assertion` som er signert med EPJ sin privatnøkkel. [Dette er beskevet her](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID).

Punkt 3: gjør et kall mot token-endepunktet i HelseID ved bruk av et bibliotek. 

Punkt 4: Utfallet av dette kallet er et Access Token som brukes i POST-kallet til /helseindikator-endepunktet i KJ.

Punkt 5: [Integrasjonen til Kjernejournal (helseindikator) er beskrevet her.](https://kjernejournal.atlassian.net/wiki/spaces/KJERNEJOURDOK1/pages/786989408/Integration+Guide+Kjernejournal+REST+API+using+HelseID+as+authenticator)

Punkt 6: Utfall: EPJ har fått utlevert en 'ticket' fra Kjernejournal.

## pkt 8 og 9 - Authorize kall til HelseID

Punkt 8: For å logge på brukeren via HelseID, må EPJ starte en nettleser som sender brukeren til HelseIDs påloggingsside (authorize-endepunktet). Det trengs en [`client_assertion`](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID) for å kunne aksessere denne siden.

Punkt 9: authorize-endepunktet i HelseID gir tilbake `code_1`.

## (Team A&A) pkt 10, 11 og 26 - kalle token endepunktet

For å få utlevert et Access token som gir tilgang til pasientopplysninger/dokumentdeling gjennom Kjernejournal portal, må EPJ bruke `code_1` som grant mot token-endepunktet i HelseID.

I tillegg må EPJ utvide `client_assertion`-strukturen ved å legge ved et JSON-element som inneholder 
 * [Claims som beskriver parametre for bruk av Tillitsrammeverket](lenke_til_jwt_rar_profil_tillitsrammeverket)
 * [Claims som beskriver parametre for Dokumentdeling](lenke_til_jwt_rar_profil_tillitsrammeverket)

[Se dokumentasjonen for bruk av client assertions.](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID)

Punkt 10: EPJ sender et POST-kall til token-endepunktet i HelseID som inneholder en `client_assertion` med de relevante parametrene.

Punkt 11: token-endepunktet i HelseID gir tilbake en response som inneholdler 
 * et Access Token, som kan brukes i kallet til KJP-API
 * et Refresh Token, som kan brukes til å be om et nytt Access token
 * metadata: utløpstidspunkt, m.m.

Punkt 26 og 27: Access-tokenet vil ha en begrenset levetid. Hvis det løper ut, må EPJ kalle token-endepunktet i HelseID med et Refresh Token for å få utvekslet et nytt Access Token.

## (Team Kollektivet) pkt 12 - Kall til KJP-API/api/Session/create
Opprett session ved å sende inn ticket og en hashet nonce, med Access token som Authorization Header.

```http request
POST /api/Session/create/
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkE4...u_UjgeTxzxI2g

{"nonce": <sha256(nonce)>, "ticket": "ca2gveFcW%2BdZ..."}
```

I respons får man opprettet en http session, og får en engangs-kode i svar som bruks ved åpning av Kjernejournal Portal
```http request
200 OK
Content-Type: application/json
Set-Cookie: <session-cookie>

{"code": "edfda05c-dbe7-44..."}
```

## (Team Kollektivet) pkt 14 - hentpasient.html
* kort beskrivelse (enda tryggere)
* eksempel på GET request

## (Team Kollektivet) pkt: xxxx - api/Session/refresh

Før Access Token går ut på dato, må oppdatert token sendes til refresh-endepunktet. 
Authorization header skal inneholde det nye tokenet, og Cookie-header må være satt til samme session man fikk tilbake i createSession-kallet. Dette kallet har ingen body
```http request
POST /api/Sesson/refresh
Cookie: <session-cookie>
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkE4...u_ca2gveFc

```

Eksempel på vellykket respons er 200 OK, og `true` i response body
```http request
200 OK
Content-Type: application/json

true
```

## (Team Kollektivet) pkt: xxxx - api/Session/end (sessionid)

For å avslutte session sendes et Session/end kall med tom body, og uten noe Auth Header, men med Session-cookie-header satt
```http request
POST /api/Session/end
Cookie: <session-cookie>

```

Eksempel på vellykket response er en http 200 respons med `true` som body:
```http request
200 OK

true
```

## Fullt sekvensdiagram
````mermaid
sequenceDiagram 
  autonumber
  title Beskrivelse av ....
  actor HP as Helsepersonell
  participant EPJ
  participant HelseID
  participant KJP
  participant XCA
  participant Dokumentkilde

  HP->>EPJ: Velger pasient
  EPJ->>EPJ: generer_assertion(virksomhet, pasientid)
  EPJ->>HelseID: getToken(assertion)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST /helseindikator/ (accesstoken + body)
  KJP-->>EPJ: pasientstatus + ticket(pasientens nin)
  HP->>EPJ: Åpner KJP
  EPJ->>HelseID: Authorize kall (dpop + authorization details + client_assertion)
  HelseID-->>EPJ: Code
  EPJ->>HelseID: /Token (Code#1)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST KJ-API/session/create (authorization: Access Token, body: ticket + sha256(nonce))
  KJP-->>EPJ: Code#2
  EPJ->>KJP: GET hentpasient.html?otc=Code#2&nonce=nonce
  KJP-->>KJP: hent access token og ticket(code, nonce)
  HP->>KJP: Åpner fanen journaldokumenter
  KJP->>HelseID: hent SAML token (access token + nin)
  HelseID-->>KJP: SAML token
  KJP->>XCA: Hent referanseliste (SAML token)
  loop hente fra alle dokumentkilder
  XCA->>Dokumentkilde: Hent referanseliste (SAML token)
  Dokumentkilde-->>Dokumentkilde: Valider SAML token
  Dokumentkilde-->XCA: referanseliste (m metadata)
  end
  XCA-->>XCA: sammenstiller referanselister til felles oversikt
  XCA-->>KJP: sammenstilt referanseliste
  KJP-->>HP: Viser referanseliste
  HP->>KJP: Åpner et journaldokument
  KJP->>XCA: Hent dokument (referanse + SAML token)
  XCA->>Dokumentkilde: Hent dokument (referanse + SAML token)
  Dokumentkilde-->>Dokumentkilde: validerer SAML token
  Dokumentkilde-->>XCA: dokument
  XCA-->>KJP: dokument
  KJP-->>HP: vise dokument 

  critical sjekk gyldighet på access token

    option Access token er utløpt
        EPJ->>HelseID: POST token (refresh grant)
        HelseID-->>EPJ: Access Token
        EPJ->>KJP: POST KJ-API/session/refresh (access token) 
        KJP-->>EPJ: HTTP 200 (OK)
    
    option Access token er gyldig
        EPJ->>EPJ: schedule refresh
  end

  critical helsepersonell bytter pasient
  option session er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)
  end
  
  critical brukersesjon i EPJ timer ut
  option session er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)
  end

  critical brukeren lukker EPJ system
  option session er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)

end 
````
