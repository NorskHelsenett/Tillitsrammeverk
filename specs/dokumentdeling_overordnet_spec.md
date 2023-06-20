# Overordnet spesifikasjon av tilgangskontroll i dokumentdeling i KJ

## Sammendrag

Målgruppe: EPJ leverandører

**Dette dokumentet beskriver hvordan EPJ integerer med Kjernejournal i andre scenarier enn fastlegenoe.**

HP logger seg inn via HelseID når HP åpner KJ-Portal og det ikke er en aktiv sesjon i HelseID

_beskrive dette bedre_

## Dokumentets status
| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| 1 | Utkast | 20.06.2023 |

Spesifikasjonen vil bli versjonert for å støtte endringer over tid.

## Innholdsfortegnelse
1. [Innledning](#1-innledning)
2. [Beskrivelse av tilgangsstyring for dokumentdeling i Kjernejournal](#2.-Beskrivelse-av-tilgangsstyring-for-dokumentdeling-i-Kjernejournal)
3. [Sekvensdiagram som beskriver meldingsflyt](#3.-Sekvensdiagram-som-beskriver-meldingsflyt)
4. [Spesifikasjon](#4.-Spesifikasjon)
5. [Sikkerhets- og personvernhensyn](#5-sikkerhets--og-personvernshensyn)

## 1. Innledning

Beskrive spesifikasjonen, og formålet med spesifikasjonen 

## 2. Beskrivelse av tilgangsstyring for dokumentdeling i Kjernejournal
Når et helsepersonell skal få innsyn i helseopplysninger ved bruk av dokumentdeling i Kjernejournal skal den konsumerende virksomheten ha utført påkrevd tilgangsstyring og tilgangskontroll av helsepersonellet slik at dokumentkilden kan være trygg på at helsepersonellet har tjenstlig behov for innsyn i de registrerte opplysningene om pasienten.

Integrasjon med kjernejournal
Basert på lokal tilgang.
Informasjon må overføres via HelseID
NHN fyller på med info

- Opprette sesjon i Kjernejournal: helseindikator
- logge inn bruker
- håndtere sesjon

Kjernejournal håndterer kommunikasjon med dokumentkildene.

## 3. Sekvensdiagram som beskriver meldingsflyt
Dette sekvensdiagrammet beskriver leverandørens oppgaver og ansvar i forbindelse med integrasjon, og inneholder ikke en beskrivelse av meldingsflyt videre i verdikjeden.

I diagrammet under vises bruk av REST-grensesnitt mot HelseID ved autentisering av virksomheten (maskin-maskin). Det er også mulig å benytte brukerpålogging i HelseID ved innlogging til KJ-portal, men denne flyten er ikke vist i denne spesifikasjonen.

Denne metoden skiller seg fra den eldre løsningen hvor EPJ må bruke sertifikater og SOAP-basert innhenting av verdier via helseindikator-tjenesten.

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
  EPJ->>EPJ: generer Client Assertion(virksomhet)
  EPJ->>HelseID: POST /token (client_assertion)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST /helseindikator/ (Access Token + body)
  KJP-->>EPJ: pasientstatus + ticket(pasientens fødselsnummer)
  HP->>EPJ: Åpner KJP
  EPJ->>EPJ: generer Request Object (tillitsmodell og dokumentdeling)
  EPJ->>HelseID: POST /authorize (request_object)
  HelseID-->>EPJ: Authorization Code
  EPJ->>HelseID: /token (authorization code)
  HelseID-->>EPJ: Access Token, Refresh Token
  EPJ->>KJP: POST KJ-API/session/create (authorization: Access Token, body: ticket + sha256(nonce))
  KJP-->>EPJ: code
  EPJ->>KJP: GET hentpasient.html?otc=code&nonce=nonce
  KJP-->>KJP: hent access token og ticket(code, nonce)
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

    option Access Token er utløpt
        EPJ->>HelseID: POST /token (refresh token grant)
        HelseID-->>EPJ: Access Token
        EPJ->>KJP: POST KJ-API/session/refresh (Access Token) 
        KJP-->>EPJ: HTTP 200 (OK)
  end

  critical helsepersonell bytter pasient
  option session er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid) EPJ-->>EPJ start ny sesjon
    EPJ->>EPJ: start ny sesjon mot KJ
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

## 4. Spesifikasjon
Denne spesifikasjonen beskriver den overordnede flyten som vises i sekvensdiagrammet over i større detalj.

# KAN HELE DETTE KAPITTELET FLYTTES UT AV DOKUMENTET?

### 4.1 Hent token og kall helseindikator (steg 2, 3 og 5 i sekvensdiagrammet)

For å få utlevert en ticket til bruk i Kjernejournal portal, må leverandøren be om et Access Token fra HelseID, og bruke dette tokenet i et POST-kall mot /helseindikator-endepunktet i KJ.

Punkt 2: generer en `client_assertion` som er signert med EPJ sin privatnøkkel. [Dette er beskevet her](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID). Denne kan enten inkludere en authorization_details-struktur [som beskrevet her](jwt_rar_profil_tillitsrammeverk.md) 
eller [som beskrevet her (dersom ditt system allerede har integrert med HelseID).](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/5636230/Passing+organization+identifier+from+a+client+application+to+HelseID)

Punkt 3: gjør et kall mot token-endepunktet i HelseID ved bruk av et bibliotek. 

Punkt 4: Utfallet av dette kallet er et Access Token som brukes i POST-kallet til /helseindikator-endepunktet i KJ.

Punkt 5: [Integrasjonen til Kjernejournal (helseindikator) er beskrevet her.](https://kjernejournal.atlassian.net/wiki/spaces/KJERNEJOURDOK1/pages/786989408/Integration+Guide+Kjernejournal+REST+API+using+HelseID+as+authenticator)

Punkt 6: Utfall: EPJ har fått utlevert en 'ticket' fra Kjernejournal.

### 4.2 Autentiser helsepersonellet via HelseID (steg 8, 9 og 10 i sekvensdiagrammet) 

Punkt 8 og 9: For å logge på brukeren via HelseID, må EPJ starte en nettleser som sender brukeren til HelseIDs påloggingsside (authorize-endepunktet). I dette kallet må det følge en signert [JWT](https://datatracker.ietf.org/doc/html/rfc7519) (i Request Object) som inneholder et JSON-element (`authorization_details`) som inneholder 
 * [Claims som beskriver parametre for bruk av Tillitsrammeverket](jwt_rar_profil_tillitsrammeverk.md)
 * [Claims som beskriver parametre for Dokumentdeling](jwt_rar_profil_dokumentdeling.md)

Punkt 10: authorize-endepunktet i HelseID gir tilbake `authorization code`.

### 4.3 Hent Access Token fra HelseID (steg 11, 12 og 27 i sekvensdiagrammet)
For å få utlevert et Access token som gir tilgang til pasientopplysninger/dokumentdeling gjennom Kjernejournal portal, må EPJ bruke `atuhorization code` som grant mot token-endepunktet i HelseID.

EPJ må også generere en `client_assertion` som er signert med EPJ sin privatnøkkel. [Dette er beskrevet her](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID).

### 4.3.1 Be om Access Token fra HelseID
##### Steg 11 i sekvensdiagrammet
EPJ sender et POST-kall til token-endepunktet i HelseID som inneholder en `client_assertion` med de relevante parametrene.

#### 4.3.2 Motta Access Token fra HelseID
##### Steg 11 i sekvensdiagrammet
Token-endepunktet i HelseID gir tilbake en response som inneholdler 
 * et Access Token, som kan brukes i kallet til KJP-API
 * et Refresh Token, som kan brukes til å be om et nytt Access Token
 * metadata: utløpstidspunkt, m.m.

#### Håndtering av Access Token livssyklys (steg 26 og 27 i sekvensdiagrammet)
Accesstokenet vil ha en begrenset levetid. 

##### (Beskriv hvordan man sjekker levetid)

Hvis det løper ut, må EPJ kalle token-endepunktet i HelseID med et Refresh Token for å få utvekslet et nytt Access Token.

## 4.4 Opprett brukersesjon i Kjernejournal Portal (steg 12 i sekvensdiagrammet) 
Kall til KJP-API/api/Session/create
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

## 4.5 Vis pasient i Kjernejournal Portal (steg 14 i sekvensdiagrammet) 

Denne spesifikasjonen beskriver en ny innloggingsflyt som fører til at parameteret _**ticket**_ fjernes som request parameter fra _hentpasient.html_, og i stedet overføres til Kjernejournal via et API. Denne medlingsflyten vises i steg 15 (api/Session/create) i sekvensdiagrammet over,  og er beskrevet i 4.4 i denne spesifikasjonen.

Kjernejournal vil motta ticket og Access token fra det nye APIet. For å gi tilgang til _hentpasient.html_ trenger Kjernejournal koden som EPJ fikk i retur fra api/Session/create sammen med en hash av nonce-verdien som ble sendt i body.
Disse verdiene overføres som query parametre i GET requestens url.

Den nye innloggingsflyten innfører to nye parametre i http meldingen, verdien til disse parametrene skal være:
* otc: koden som EPJ mottok i http response fra kall til _api/Session/create_.
* nonce: nonce verdien som ble overført i kallet til _KJP-API/api/Session/create_ i klartekst.

### Eksempel på http request til KJP-API/api/Session/create:

```http request

GET /hpp-webapp/hentpasient.html?otc=968abbad-7192-4a66-8063-b21b639635a9&nonce=ukyT8vC9KZ1q2qZgt6d2Y_Wr7O9dOUyvTgBEOAAaGrE

```

## 4.5 Sesjonshåndtering i Kjernejournal Portal

### 4.5.1 Hold sesjonen i live
pkt: xxxx - api/Session/refresh

Før Access Token går ut på dato, må oppdatert token sendes til refresh-endepunktet. 
Authorization header skal inneholde det nye tokenet, og Cookie-header må være satt til samme session man fikk tilbake i createSession-kallet. Dette kallet har ingen body.

Eksempel på gyldig HTTP request:
```http request
POST /api/Sesson/refresh
Cookie: <session-cookie>
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkE4...u_ca2gveFc

```
Dersom forespørelsen om oppfriskning av sesjonen er vellykket vil serveren gi HTTP Status Code 200 OK, og `true` i response body
```http request
200 OK
Content-Type: application/json

true
```
### 4.5.1 Avslutt brukersesjon
pkt: xxxx - api/Session/end (sessionid)

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


