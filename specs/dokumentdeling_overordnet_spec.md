# Spesifikasjon av tilgangskontroll i dokumentdeling i KJ

## Sammendrag
Dette dokumentet er en spesifikasjon av tilgangsstyring for journalsystemer som skal integreres med Kjernejournal Portal for dokumentdeling i andre scenarier enn for fastlegene som allerede har innført dokumentdeling i Kjernejournal Portal.

Målgruppen for dette dokumentetet er personell hos programvareleverandørene som skal implementere integrasjonen.

## Dokumentets status
| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| 1 | Utkast | xx.06.2023 |
| 2 | Versjon klar til sektor input | 19.06.2023 |

Spesifikasjonen vil bli versjonert for å støtte endringer over tid.

## Innholdsfortegnelse
1. [Innledning](#1-innledning)
2. [Beskrivelse av tilgangsstyring for dokumentdeling i Kjernejournal](#2.-Beskrivelse-av-tilgangsstyring-for-dokumentdeling-i-Kjernejournal)
3. [Sekvensdiagram som beskriver meldingsflyt](#3.-Sekvensdiagram-som-beskriver-meldingsflyt)
4. [Spesifikasjon](#4.-Spesifikasjon)
5. [Sikkerhets- og personvernhensyn](#5-sikkerhets--og-personvernshensyn)


## 1. Innledning 
For å gi riktig helsehjelp til riktig tid må helsepersonell ha tilgang til relevante helseopplysninger som ligger lagret hos andre virksomheter enn den virksomheten hvor de yter helsehjelp. Lovverket i Norge sier at helsevirksomheter er pliktig til å dele helseopplysninger med alt helsepersonell så fremt de har et tjenstlig behov og at opplysningene er relevante og nødvendige i helsepersonellets behandling av pasienten (hpl §45).

Kravene knyttet til tjenstlig behov og opplysningenes relvans og nødvendighet i behandlingen av pasienten medfører at virksomhetene som har dataansvar for helseopplysningene må styre tilgang på en tilfredsstillende måte.

I tjenesten for oppslagg i pasientens journaldokumenter gjennom kjernejournal-portal legges det opp til en oppgavefordeling knyttet til tilgangsstyring, slik at den konsumerende virksomheten utfører tilgangsstyring til helseopplysninger på vegne av dokumentkilden. Til tross for at den konsumerende virksomheten er forpliktet til å kontrollere at deres helsepersonell har en gyldig grunn for tilgang til helseopplysninger har virksomheten som deler opplysninger likevel behov for å motta informasjon som beskriver grunnlaget for tilgangen. Informasjonen som beskriver grunnlaget for delingen vil benyttes til flere formål:

1. å utføre ytterligere tilgangskontroll
2. lovpålagt logging av tilgangen for å avdekke urettmessig tilegnelse av helseopplysninger
3. å støtte opp under innbyggers rettigheter

På grunn av at tilgangsstyring er implementert på forskjellig måte i forskjellige systemer og virksomheter er det nødvendig at konsumentene og dokumentkildene samler seg om et felles språk for å uttrykke grunnlaget for tilgang slik at aktørene kan forstå hverandre. Et felles språk vil også bidra til å kommunisere på en konsistent måte til innbygger.

Denne spesifikasjonen definerer et felles språk som skal benyttes til å uttrykke helsepersonells grunnlag for tilgang til helseopplysninger ved deling av helseopplysninger via tekniske grensesnitt. Spesifikasjonen definerer en informasjonsmodell, datamodell og kodeverk som skal implementeres i programvare som benyttes av helsepersonell når de yter helsehjelp til sin pasient.

## 2. Beskrivelse av tilgangsstyring for dokumentdeling i Kjernejournal
Tilgangsstyring for dokumentdeling i Kjernejournal Portal er basert på en modell tilpasset helsesektoren, hvor partenenes ansvar er tydeliggjort og oppgaver er fordelt i form av et avtalebasert tillitsrammeverk.

Når et helsepersonell gis innsyn til helseopplysninger ved bruk av dokumentdeling i Kjernejournal skal den konsumerende virksomheten på forhånd ha utført påkrevd tilgangsstyring og tilgangskontroll av helsepersonellet slik at dokumentkilden kan være trygg på at helsepersonellet har tjenstlig behov for innsyn i de registrerte opplysningene om pasienten.

Integrasjon med kjernejournal
Basert på lokal tilgang.
Informasjon må overføres via HelseID
NHN fyller på med info

### 2.1 Attributter tilknyttet tillitsrammeverket
[lenke til informasjonsmodell for tillitsrammeverk](http://sdfdsaf)

### 2.2 Attributter spesifikt for dokumentdeling
[lenke til informasjonsmodell for dokumentdeling](http://sdfdsaf)

### 2.3 Sekvensdiagram som beskriver systemintegrasjon
````mermaid
sequenceDiagram 
title Beskrivelse av..

actor HP as Helsepersonell
participant EPJ
participant HelseID
participant KJP
participant Dokumentkilde

HP->>EPJ: Åpner pasientkontekst
EPJ->>EPJ: Utfører tilgangskontroll
EPJ-->>HP: Gir tilgang til pasientens helseopplysninger
HP->>EPJ: Ber om tilgjengelige dokumenter i KJP
EPJ->>HelseID: Ber om autentisering av HP og tilgang til KJP
HelseID-->>EPJ: Leverer Access Token
EPJ->>KJP: Åpne pasient og legger ved Access Token
KJP->>Dokumentkilde: Hent dokumentoversikt, legger ved Access Token
Dokumentkilde-->>KJP: Leverer dokumentoversikt
KJP-->>HP: Viser dokumentoversikt
HP->>KJP: Hent dokument
KJP->>Dokumentkilde: Hent dokument
Dokumentkilde-->>KJP: Leverer dokument
KJP-->>HP: Leverer dokument
````

## 3. Sekvensdiagram som beskriver meldingsflyt
Dette sekvensdiagrammet beskriver meldingsflyt mellom journalsystem, HelseID og KJP for dokumentdeling i Kjernejournal Portal. Sekvensdiagrammet beskriver ikke meldingsflyt mellom tjenester i NHN og dokumentkilden.

I diagrammet under vises bruk av REST-grensesnitt mot HelseID ved autentisering av virksomheten (maskin-maskin). Spesifikasjonen beskriver ikke direkte brukerpålogging til KJ-portal via HelseID.

Denne metoden skiller seg fra den eldre løsningen hvor EPJ må bruke sertifikater og SOAP-basert innhenting av verdier via helseindikator-tjenesten.

````mermaid
sequenceDiagram 
  autonumber
  title Meldingsflyt ved bruk av HelseID og KJP
  actor HP as Helsepersonell
  participant EPJ
  participant HelseID
  participant KJP
  participant Dokumentkilde

  HP->>EPJ: Åpner KJP
  EPJ->>EPJ: generer Request Object (tillitsmodell og dokumentdeling)
  EPJ->>HelseID: POST /authorize (request_object)
  HelseID-->>EPJ: Authorization Code
  EPJ->>HelseID: POST /token (authorization code)
  HelseID-->>EPJ: Access Token, Refresh Token
  EPJ->>KJP: POST KJ-API/session/create (authorization: Access Token, body: pasient-id + samtykkegrunnlag + sha256(nonce))
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
Spesifikasjonen gir en detaljert beskrivelse av meldingsflyten i sekvensdiagrammet over.

Systemene hos NHN som deltar i meldingflyten har ytterligere relevante krav knyttet til integrasjoner mellom journalsystemer og NHN sine systemer. Kravene omfatter blant hvordan pasientidentifikator og samtykkegrunnlag skal overføres fra konsument til NHN.

| --- | --- |
| Bruk av HelseID for Kjernejournal | [Veileder](https://kjernejournal.atlassian.net/wiki/spaces/KJERNEJOURDOK1/pages/786989408/Integration+Guide+Kjernejournal+REST+API+using+HelseID+as+authenticator) |
| Datamodell for dokumentdeling i HelseID | [RAR i HelseID](jwt_rar_profil_tillitsrammeverk.md) |



### 4.1 Autentiser helsepersonellet via HelseID (steg 8, 9 og 10 i sekvensdiagrammet) 
For å logge på brukeren via HelseID, må EPJ starte en nettleser som sender brukeren til HelseIDs påloggingsside (authorize-endepunktet). I dette kallet må det følge en signert [JWT](https://datatracker.ietf.org/doc/html/rfc7519) som inneholder JSON-elementet _authorization_details_.

*Steg 2:* 
EPJ må samle informasjon I dette kallet må det følge en signert [JWT](https://datatracker.ietf.org/doc/html/rfc7519) som inneholder JSON-elementet _authorization_details_.

JSON-elementet _authorization_details_ skal inneholde: 
 * [Claims som beskriver parametre for bruk av Tillitsrammeverket](jwt_rar_profil_tillitsrammeverk.md)
 * [Claims som beskriver parametre for Dokumentdeling](jwt_rar_profil_dokumentdeling.md)

*Steg 4:* 
Resultatet av kallet til /authorize endepunktet i HelseID er en _authorization code_ som EPJ tar vare på.

### 4.2 Hent Access Token fra HelseID (steg 11, 12 og 27 i sekvensdiagrammet)
For å få utlevert et Access token som gir tilgang til pasientopplysninger/dokumentdeling gjennom Kjernejournal portal, må EPJ bruke `atuhorization code` som grant mot token-endepunktet i HelseID.

EPJ må også generere en `client_assertion` som er signert med EPJ sin privatnøkkel. [Dette er beskrevet her](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID).

### 4.2.1 Be om Access Token fra HelseID
##### Steg 11 i sekvensdiagrammet
EPJ sender et POST-kall til token-endepunktet i HelseID som inneholder en `client_assertion` med de relevante parametrene.

#### 4.2.2 Motta Access Token fra HelseID
##### Steg 11 i sekvensdiagrammet
Token-endepunktet i HelseID gir tilbake en response som inneholdler 
 * et Access Token, som kan brukes i kallet til KJP-API
 * et Refresh Token, som kan brukes til å be om et nytt Access Token
 * metadata: utløpstidspunkt, m.m.

#### Håndtering av Access Token livssyklys (steg 26 og 27 i sekvensdiagrammet)
Accesstokenet vil ha en begrenset levetid. 

##### (Beskriv hvordan man sjekker levetid)

Hvis det løper ut, må EPJ kalle token-endepunktet i HelseID med et Refresh Token for å få utvekslet et nytt Access Token.

## 4.3 Opprett brukersesjon i Kjernejournal Portal (steg 12 i sekvensdiagrammet)
[Peke til spesifikasjon av datamodell for pasient-id, samtykkegrunnlag]
Kall til KJP-API/api/Session/create
Opprett session ved å sende inn pasient-id, samtykkegrunnlag og en hashet nonce, med Access token som Authorization Header.

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

## 4.4 Vis pasient i Kjernejournal Portal (steg 14 i sekvensdiagrammet) 


Kjernejournal vil hente pasient-id, samtykkegrunnlag og Access token fra APIet i steg 3. For å gi tilgang til _hentpasient.html_ trenger Kjernejournal koden som EPJ fikk i retur fra api/Session/create og en hash av nonce-verdien som ble sendt i body.
Disse verdiene overføres som query parametre i GET requestens url.

Denne innloggingsflyten innfører to nye parametre i http meldingen, verdien til disse parametrene skal være:
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
### 4.5.2 Avslutt brukersesjon
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


