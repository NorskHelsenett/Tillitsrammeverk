# Bruk av OpenID Connect for deling av helseopplysninger via API
# IKKE FERDIG
# VELDIG UNDER ARBEID
# IKKE LES OM DU IKKE SKAL BIDRA

## 1. Introduksjon
Dette dokumentet er en teknisk spesifikasjon som beskriver hvordan OpenID Connect og OAuth 2.0 skal benyttes ved deling av helseopplysninger innad i Helsenettet. Dokumentet er ment for utviklere og tekniske arkitekter som skal konsumere API hvor det er et krav at helsepersonellet er autentisert.

OpenID Connect er en protokoll som lar utvikleren selv velge en del sikkerhetsmessige egenskaper ved protokollen. Når man deler helseopplysninger er det forventet at sikkerheten blir ivaretatt på god nok måte. Denne spesifikasjonen er ikke en generell beskrivelse av hvordan OpenID Connect skal benyttes, men en spesifikk beskrivelse av hvordan HelseID skal brukes ved deling av helseopplysninger. 

HelseID gjør det mulig å gjenbruke en autentisering mellom to eller flere applikasjoner, såkalt Single Sign-On (SSO).  HelseID gjør det også mulig for applikasjonen som ber om autentisering, også kalt Relying Party (RP), å gjenbruke en pålogget brukersesjon når RP også er en OAuth klient som skal be om tilgang til et API. 

> **_TODO:_** [Legg inn en tegning her]

## 2. Forutsetninger og underliggende krav


- [OpenID Connect](https://openid.net/specs/openid-connect-core-1_0.html)
- [OAuth 2.0](https://www.rfc-editor.org/rfc/rfc6749)
- [HelseID sikkerhetsprofil for klienter](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/128352260/Security+profile+for+clients+using+HelseID) (basert på FAPI 2.0)
- JWT profil for tillitsrammeverk - "trusted_claims"  **_TODO:_** [Legg til lenke]


### 2.1 Tillitsrammeverk for deling av helseopplysninger
Tillitsrammeverk for deling av helseopplysninger i norsk helsesektor er beskrevet i egne dokumenter.

> **_TODO:_** [Legg inn lenker til rammeverket, samt en kort oppsummering.}

- Helsenettet 
- Norm for informasjonssikkerhet 
- eID i tillitsrammeverket 
- Avtaleverk 

## 3. Krav knyttet til bruk av HelseID
### Krav til RP/Klient
- Skal
- Bør
- Kan
- Kommende krav

### Krav til API/Tjeneste
- Skal
- Bør
- Kan
- Kommende krav

### Krav til HelseID
- Skal
- Bør
- Kan
- Kommende krav

## 3. Bruk av HelseID ved deling av helseopplysninger

### 3.1 Overordnet beskrivelse av bruksmønster

### 3.1 Autentiseringsforespørsel

RP ber om autentisering av den fysiske personen ved bruk av normal flyt iht. protokoll, men med følgende presiseringer: 
* RP skal benytte en av følgende mekanismer ved forespørsler mot HelseID: 
  * Request Object, som beskrevet i …., eller   
    **Spørsmål:_** Skal vi kreve at parametre inkluderes i RO, eller forsette dagens policy hvor det er valgfritt   
  * Pushed Authorization Requests, som beskrevet i.. 
  
* Dersom Request Object benyttes skal denne overføres til HelseID som et form parameter.

* Det er et krav at et token ikke skal kunne stjeles eller misbrukes. Mekanismene som skal forhindre dette er ikke tilgjengelig i HelseID enda, men når de er på plass skal klienten bruke DPoP eller mTLS for å binde seg krypografisk til Access Tokens.

* RP/API klient skal overføre informasjon som beskriver bakgrunnen for tilgangsforespørselen ved bruk av mekanismen Rich Authorization Requests, som beskrevet i **_TODO:_** [Lenke til eget dokument]

* Informasjon som beskriver bakgrunn for tilgangsforespørselen skal følge standarden som er angitt i… (autentiseringsforespørsler) 

* RP skal autentisere brukeren iht. regler i tillitsrammeverket **_TODO:_** [Lenke her]
   * Dette inkluderer å verifisere at lokal brukeridentitet (om noen) i RP er lik brukeridentiteten returnert fra HelseID.

```mermaid
sequenceDiagram 
  autonumber
  title Overordnet autentiseringsflyt
  actor HP as Helsepersonell
  participant RP as Client
  participant HelseID as STS
  participant IDP
  participant API as API Resource

  HP-->RP: Hent helseinformasjon  
  rect rgba(150, 150, 150, 0.1)
  RP->>HelseID: Authenticate User (authorize-endpoint)
  activate HelseID
  HelseID->>IDP: Authenticate User
  IDP->>HelseID: OK
  HelseID->>RP: Ok
  deactivate HelseID
  end
  RP->>HelseID: Get Tokens (token-endpoint)
  HelseID->>RP: Identity Token, Access Token and Refresh Token
  loop Until Access Token expires or Context changes
  RP->>API: Invoke with Access Token as Bearer Token
  end

Note over RP: Access Token Expires
RP->>HelseID: Get new Access Token with Refresh token   
HelseID->>RP: New Access Token 
 
```
Hvert enkelt steg i flyten over er beskrevet i detalj under

**_TODO:_** [Legg inn sekvensdiagram som viser målbilde med PAR og DPoP]


#### 3.1.1 Kall fra RP for brukerautentisering
Når et helsepersonell ønsker å få tilgang til helseopplysninger i andre virksomheter SKAL helsepersonellet autentiseres i HelseID, ref steg 1 og 2 i figuren over.

Brukeren SKAL sendes i nettleser til endepunktet [/authorize](https://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint) i HelseID. Endepunktet er dokumentert [her](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/5571605/Authorize+Endpoint).

Utover normal protokollflyt er det følgende nødvendig

##### 3.1.1.x Krav knyttet til forespørsler om brukerautentisering
Basert på FAPI 2.0, med egne tilpassinger [lenke til vår profil]
* Request Object (signert med klienthemmeligheten)
* Hvordan velge IdP


#### 3.1.1.1 Overføre informasjon om grunnlaget for tilgang fra RP
Ved deling av helseopplysninger på tvers av virksomheter i helsesektoren krever tillitsrammeverket at konsumentens EPJ-system overfører informasjon som beskriver hvorfor helsepersonellet har fått tilgang til pasientens helseopplysninger.
Datamodellen er [beskrevet i en egen spesifikasjon](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/informasjons_og_datamodell.md).

HelseID krever at denne informasjonen struktureres og formatteres i henhold til spesifikasjonen [profil for authorization_details" struktur](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/profil_for_authorization_details.md).

Strukturen som inneholder informasjon om grunnlaget for at helsepersonellet har fått tilgang til pasientens helseopplysninger skal enten:
* sendes til HelseID i autentiseringsforespørselen ved å benytte parameteret "request" i henhold til [OpenID Connect - Request Object](https://openid.net/specs/openid-connect-core-1_0.html#RequestObject), eller
* sendes til [token endepunktet](https://www.rfc-editor.org/rfc/rfc6749#section-3.2) som del av klientautentiseringen i henhold til [client_assertion](https://www.rfc-editor.org/rfc/rfc7521#page-13), og [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication). 

Det er opp til leverandør å velge mekanismen som passer best.

**_TODO:_** [Lenke til konkret eksempel + eksempelkode].

Et request object SKAL overføres som et FORM verdier i en POST request.

#### 3.1.1.2 Forspørsel om tilgang til flere API-er
Tjenester som inngår i tillitsmodellen krever at Access Tokens ment for dem, ikke skal kunne brukes for å få tilgang andre API-er. I praksis innebærer dette at claimet "aud" (audience) ikke kan ha mer enn en verdi. *Audience* er navnet som identifiserer API-et i HelseID

HelseID gjør det enkelt for klienter å hente ett Access Token per tjeneste ved å tilby mekanismen [Resource Indicators](https://www.rfc-editor.org/rfc/rfc8707). Bruk av Resource indikators er beskrevet [her](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/481755152/Requesting+multiple+access+tokens+with+single+audiences).


### 3.1.2 Kontroller i HelseID av forespørsler om brukerautentisering
Figuren under viser hvilke kontroller HelseID gjør når en klient forespør brukerautentisering.

```mermaid
flowchart LR
  Error[Vis feilmelding]
  Param{Kontroll av standard protokollparamtere}
  S[Autentiseringsforspørsel fra Klient] --> Param
  Param-- Ugyldig --> Error 
  Param-- Ok --->RO{Er Request Object brukt}
  RO-- Ja -->V_RO{Kontroller RO\nSe 'Kontroll av påstander fra klient'} 
  RO-- Nei -->IDP
  V_RO-- OK --> IDP[Send bruker til IDP\n Ved SSO, send bruker tilbake til fagsystem]
  V_RO-- Ugyldig --> Error

```
#### 3.1.2.1 Kontroll av standard protokollparamtere
Det første som skjer en en kontroll av protokollparametre i forespørselen i henhold til OpenID Connect og sikkerhetsprofilen til HelseID. Dette inkluderer, men er ikke begrenset til:

  * Sjekk av at klienten er registrert og aktivert i HelseID
  * Sjekk av at klienten forspør API-er og annen informasjon den har tilgang til
  * Sjekk av at klienten sender med en gyldig redirect_uri
  * Sjekk av at klienten bruker PKCE
  * (Fremtidig) Sjekk av at klienten bruker DPoP dersom et forespurt API krever det
  * (Fremtidig) Sjekk av systemidentitet

Dersom noen av disse kontrollene feiler, vil sluttbrukeren se en feilmelding i sin nettleser.

Merk at protokollparametre både kan sendes som GET eller POST parametre, eller som en del av et Request Object. 

#### 3.1.2.2 Kontroll av Request Object
Dersom klienten har inkludert et Request Object for å overføre kontekstuell informasjon til HelseID (f.eks virksomhet eller brukerkontekst), vil kontroll av dette skje på samme måte som for client assertions i Token-endepunktet. Se **_TODO:_** [LEGG INN LENKE TIL AVSNITT].

Dersom noen av disse kontrollene feiler, vil sluttbrukeren se en feilmelding i sin nettleser.


#### 3.1.2.3 Kall til IDP

Dersom alle kontroller er ok, sjekker HelseID om brukeren allerede har en sesjon i HelseID. Dersom dette er tilfelle, og klienten ikke eksplisitt har spurt om å ikke benytte Single sign-on, sendes brukeren tilbake til klienten (fagsystemet).

Om ikke, sendes brukeren til ekstern IDP for autentisering.


### 3.1.3 Kontroller av svar fra ekstern IDP
Etter at en bruker har autentisert seg hos en ekstern IDP, vil HelseID kontrollere resultatet.

```mermaid
flowchart LR
  Error[Vis feilmelding]
  IDP{Kontroll av identitetstoken fra ekstern IDP}  
  S[Svar fra IDP] --> IDP
  IDP-- Ugyldig --> Error
  IDP-- OK --> IDP_I{Kontroll av informasjon fra IDP}
  IDP_I-- Ugyldig --> Error
  IDP_I-- OK --> IDP_P[Persister nødvendig informasjon i brukersesjon]
  IDP_P-->Client[Send bruker tilbake til fagsystem]  
```

### 3.1.3.1 Kontroll av svar fra ekstern IDP
Etter at brukeren har autentisert seg i ekstern IDP, sendes informasjon om dette tilbake til HelseID. Dette vil alltid være et Identity Token. HelseID validerer først gyldigheten på dette tokenet i henhold til protokollspesifikasjon og egen sikkerhetsprofil. 

Dersom noen av disse kontrollene feiler, vil sluttbrukeren se en feilmelding i sin nettleser.

### 3.1.3.1 Kontroll av informasjon fra ekstern IDP
HelseID forventer å få informasjon fra IDP om identitet til bruker, sikkerhetsnivå, påloggingsmekanisme mm. HelseID kontroller at denne informasjon er tilstede og gyldig.

Dersom dette feiler, vil sluttbrukeren se en feilmelding i sin nettleser.


#### 3.1.3 Håndtering av resultat av brukerautentisering i klient
Når klienten mottar resultatet fra brukerautentiseringen fra HelseID, skal dette benyttes for å hente Identity-, Refresh- og Access Tokens. Dette gjøres i henhold i protokkspesifikasjon og HelseID sin sikkerhetsprofil.


#### 3.1.4 Kall fra klient for å hente tokens
* Authorization Details (context, virksomhet, annet)
* Client Assertion


* Vise kontroller i HelseID 
  * Vise autentisering av klient 
    (Krav til signeringsalg, levetid på token, JTI)
  * Vise kontroll av klient 
    (Godkjent for PDS)
  * Vise sjekk av systemidentitet
    (Ikke implementert ennå) 
  * Vise sjekk av virksomhetsidentitet 
  * Vise berikelse av personinformasjon 
  * Vise berikelse av HPR informasjon 

###  Validering av Client Assertion

#### Validering av ekstra informasjon i Client Assertion (eller Request Object)


### 3.1.4 Generering av Access Token og Identity Token
- Peke på "trusted_claims" profilen 


* Vise utstedelse av access token og id token 
* Vise kall til token endepunktet med Auth Code 
* Vise utstedelse av Access Token 

#### 3.1.4 Kontroller i RP av Identity Token
* Pek til profil
* Kontroll av lokal identitet vs Identity Token



### 3.3 Forespørsel til API
- Validering av token i API
- DPoP 
- eID 
- Validering og bruk av informasjon i token 
- Revisjonslogging 

### 3.4 Bruk av refreshtoken
 


## 4. Sikkerhetsvurderinger
HelseID krever sikkerhetsprofilen FAPI 2.0 (lenke til vår versjon av profilen)
Pek til Security BCP og Trusselmodell

Beskriv konkrete sikkerhetstiltak på klienten:
- XSS (for nettlesere)
- Sjekk av parametre som sendes til HelseID 
- Kontroll av tokens 
- Riktig URL til HelseID

Sikkerhet i API:
- Kreve DPoP eller mTLS

Sikkerhet i OP:
- Nøkkelmateriale 
- Sikkerhet i registre brukt til berikelse av informasjon 

 