# RAR vs Assertion Framework
## Planen
Ragnhild beslutter veien videre:
- Aidn og Pridok skal ikke benytte KJP, og er ikke relevant
- Alternativer:
    1. Å tilby RAR og Assertion Framework 
    2. Å ikke tilby RAR
    3. Å ikke tilby Assertion Framework

## RAR
````mermaid
sequenceDiagram 
  autonumber
  title Beskrivelse av ....
  actor HP as Helsepersonell
  participant EPJ
  participant HelseID
  participant KJP

  HP->>EPJ: Velger pasient
  EPJ->>EPJ: generer_assertion(virksomhet, pasientid)
  EPJ->>HelseID: POST hid/token(assertion)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST /helseindikator/ (accesstoken + body)
  KJP-->>EPJ: pasientstatus + ticket(pasient-id)
  HP->>EPJ: Åpner KJP
  EPJ->>EPJ: createRO(authorization_details)
  EPJ->>HelseID: POST hid/authorize?response_type=code&ro=request_object
  HelseID-->>EPJ: code
  EPJ->>HelseID: hid/token (code)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: GET hentpasient.html
  KJP-->>HP: vis_referanseliste
  HP->>KJP: hent_journaldokument
  KJP-->>HP: vise dokument

  critical HP velger ny pasient
  HP->>EPJ: velg pasient
  EPJ->>EPJ: generer_assertion(virksomhet, pasientid)
  EPJ->>HelseID: POST hid/token(assertion)
  HelseID-->>EPJ: AccessToken
  EPJ->>KJP: POST /helseindikator/ (AccessToken + body)
  KJP-->>EPJ: pasientstatus + ticket(pasient-id)
  HP->>EPJ: Åpner KJP
  EPJ->>EPJ: createRO(authorization_details)
  EPJ->>HelseID: POST hid/authorize?response_type=code&ro=request_object
  HelseID-->>EPJ: code
  EPJ->>HelseID: hid/token (code)
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: GET hentpasient.html
  KJP-->>HP: vis_referanseliste
  HP->>KJP: hent_journaldokument
  KJP-->>HP: vise dokument
  

  
end 
````

## Assertion Framework


````mermaid
sequenceDiagram 
  autonumber
  title Beskrivelse av ....
  actor HP as Helsepersonell
  participant EPJ
  participant HelseID
  participant KJP

  EPJ->>HelseID: Logg inn bruker med normal flyt (med KJ scope)
  HP->>EPJ: Velger pasient
  EPJ->>EPJ: createAssertion(virksomhet, pasientid)
  EPJ->>HelseID: POST hid/token?grant_type=client_credentials&assertion=assertion
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: POST /helseindikator/ (accesstoken + body)
  KJP-->>EPJ: pasientstatus + ticket(pasient-id)
  HP->>EPJ: Åpner KJP
  EPJ->>EPJ: createAssertion(authorization_details)
  EPJ->>HelseID: POST hid/token?response_type=refresh_token&assertion=assertion
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: GET hentpasient.html
  KJP-->>HP: vis_referanseliste
  HP->>KJP: hent_journaldokument
  KJP-->>HP: vise dokument

  critical HP velger ny pasient
  HP->>EPJ: velg pasient
  EPJ->>EPJ: createAssertion(virksomhet, pasientid)
  EPJ->>HelseID: POST hid/token?grant_type=client_credentials&assertion=assertion
  HelseID-->>EPJ: AccessToken
  EPJ->>KJP: POST /helseindikator/ (AccessToken + body)
  KJP-->>EPJ: pasientstatus + ticket(pasient-id)
  HP->>EPJ: Åpner KJP
  EPJ->>EPJ: createAssertion(authorization_details)
  EPJ->>HelseID: POST hid/token?grant_type=refresh_token&assertion=assertion
  HelseID-->>EPJ: Access Token
  EPJ->>KJP: GET hentpasient.html
  KJP-->>HP: vis_referanseliste
  HP->>KJP: hent_journaldokument
  KJP-->>HP: vise dokument
  

  
end 
````
