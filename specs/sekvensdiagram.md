# Sekvensdiagram
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
  EPJ->>HelseID: Authorize kall (authorization details + client_assertion)
  HelseID-->>EPJ: Code
  EPJ->>HelseID: /Token (Code#1)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST KJ-API/session/create (authorization: Access Token, body: ticket + sha256(nonce))
  KJP-->>EPJ: Code#2
  EPJ->>KJP: GET hentpasient.html?otc=Code#2&nonce=nonce
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

## pkt: 2, 3 og 5 Hent token og kall helseindikator
1. Innledende tekst
2. Lenke til spesifikasjon: 
[Integrasjonen er beskrevet her](https://kjernejournal.atlassian.net/wiki/spaces/KJERNEJOURDOK1/pages/786989408/Integration+Guide+Kjernejournal+REST+API+using+HelseID+as+authenticator)


## (Team A&A) pkt 8 - Authorize kall til HelseID
1. Innledende tekst
2. Lenker til relevante spesifikasjoner
    * Datamodellene: dokumentdeling og tillitsrammeverk
    * auth_details spec
    * bruk av helseid (med brukerpålogging)
3. Eksempel på HTTP

## (Team A&A) pkt 10 - kalle token endepunktet
1. Innledende tekst
2. Lenker til relevante spesifikasjoner
    * bruk av helseid (med brukerpålogging)
3. Eksempel på HTTP

## (Team Kollektivet) pkt 12 - Kall til KJP-API/api/Session/create
* kort beskrivelse
* eksempel på POST request
* eksempel på Response

## (Team Kollektivet) pkt 14 - hentpasient.html
* kort beskrivelse (enda tryggere)
* eksempel på GET request

## (Team Kollektivet) pkt: xxxx - api/Session/refresh
* kort beskrivelse
* eksempel på POST request
* eksempel på response (200 OK, ved feil 401/403/500??)

## (Team Kollektivet) pkt: xxxx - api/Session/end (sessionid)
* kort beskrivelse
* eksempel på POST request
* eksempel på response (200 OK, ved feil 401/403/500??)


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
