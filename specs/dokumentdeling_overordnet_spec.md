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
I tjenesten for oppslagg i pasientens journaldokumenter gjennom kjernejournal-portal legges det opp til en oppgavefordeling knyttet til tilgangsstyring, slik at den konsumerende virksomheten utfører tilgangsstyring til helseopplysninger på vegne av dokumentkilden. Til tross for at den konsumerende virksomheten er forpliktet til å kontrollere at deres helsepersonell har en gyldig grunn for tilgang til helseopplysninger har virksomheten som deler opplysninger likevel behov for å motta informasjon som beskriver grunnlaget for tilgangen. 

På grunn av at tilgangsstyring er implementert på forskjellig måte i forskjellige systemer og virksomheter er det nødvendig at konsumentene og dokumentkildene samler seg om et felles språk for å uttrykke grunnlaget for tilgang slik at aktørene kan forstå hverandre. Et felles språk vil også bidra til å kommunisere på en konsistent måte til innbygger.

## 2. Beskrivelse av tilgangsstyring for dokumentdeling i Kjernejournal
Tilgangsstyring for dokumentdeling i Kjernejournal Portal er basert på en modell tilpasset helsesektoren, hvor partenenes ansvar er tydeliggjort og oppgaver er fordelt i form av et avtalebasert tillitsrammeverk.

Når et helsepersonell gis innsyn til helseopplysninger ved bruk av dokumentdeling i Kjernejournal skal den konsumerende virksomheten på forhånd ha utført påkrevd tilgangsstyring og tilgangskontroll av helsepersonellet slik at dokumentkilden kan være trygg på at helsepersonellet har tjenstlig behov for innsyn i de registrerte opplysningene om pasienten.

Integrasjon med kjernejournal
Basert på lokal tilgang.
Informasjon må overføres via HelseID
NHN fyller på med info

### 2.1 Attributter tilknyttet tillitsrammeverket
[Datamodellmodell for tillitsrammeverket](/specs/datamodell_tillitsmodell.md)

### 2.2 Attributter spesifikt for dokumentdeling
[Datamodellmodell for tillitsrammeverket](/specs/datamodell_dokumentdeling.md)

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
  EPJ->>KJP: POST KJ-API/session/create (authorization: Access Token, body: patient-id:pasient-id + consent:samtykkegrunnlag + code_challenge:sha256(code_verifier))
  KJP-->>EPJ: code
  EPJ->>KJP: GET hentpasient.html?otc=code&ehr_code_verifier=code_verifier
  HP->>KJP: Åpner fanen journaldokumenter
  KJP->>Dokumentkilde: Hent referanseliste
 
  Dokumentkilde-->KJP: referanseliste
 
  KJP-->>HP: Viser referanseliste
  HP->>KJP: Åpner et journaldokument
  KJP->>Dokumentkilde: Hent dokument
  Dokumentkilde-->>KJP: dokument
  KJP-->>HP: vise dokument

  critical sjekk gyldighet på access token

    option Access Token er utløpt
        EPJ->>HelseID: POST /token?response_type=refresh_token..8<>8
        HelseID-->>EPJ: Access Token
        EPJ->>KJP: POST KJ-API/session/refresh (Authorization: bearer AccessToken) 
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

De enkelte systemene hos NHN som deltar i meldingflyten har ytterligere relevante krav som ikke beskrives i denne spesifikasjonen. Kravene omfatter blant hvordan pasientidentifikator og samtykkegrunnlag skal overføres fra konsument til NHN.

| | |
| --- | --- |
| Bruk av HelseID for Kjernejournal | [Veileder](https://kjernejournal.atlassian.net/wiki/spaces/KJERNEJOURDOK1/pages/786989408/Integration+Guide+Kjernejournal+REST+API+using+HelseID+as+authenticator) |
| Datamodell for dokumentdeling i HelseID | [JSON profil for RAR](jwt_rar_profil_tillitsrammeverk.md) |
| Datamodell for dokumentdeling i HelseID | [JSON profil for RAR](jwt_rar_profil_dokumentdeling.md) |

### 4.1 Autentiser helsepersonellet via HelseID (steg 2, 3 og 4 i sekvensdiagrammet)
For å logge på brukeren via HelseID må EPJ åpne en nettleser som sender en forespørsel om autentisering av helsepersonellet og tilgang til Kjernejournal Portal. EPJ må legge ved informasjon som beskriver helsepersonellets grunnlag for tilgang til pasientens helseopplysninger i forespørselen.

HelseID sørger for å autentisere helsepersonellet i henhold til gjeldende retningslinjer i tillitsrammeverket.

*Steg 2 og 3:*
EPJ må samle nødvendig informasjon om helsepersonellet som angitt i følgende spesifikasjoner:
* [Datamodell for tillitsrammeverk](datamodell_tillitsmodell.md)
* [Datamodell for dokumentdeling](datamodell_dokumentdeling.md)

Attributtene som EPJ har samlet må struktureres i JSON-elementet _authorization_details_, i henhold til følgende spesifikasjoner:
 * [Claims som beskriver parametre for bruk av Tillitsrammeverket](jwt_rar_profil_tillitsrammeverk.md)
 * [Claims som beskriver parametre for Dokumentdeling](jwt_rar_profil_dokumentdeling.md)

HelseID krever at _authorization_details_ strukturen overføres som et såkalt Request Object, som [angitt av HelseID sin dokumentasjon.](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/5636230/Passing+organization+identifier+from+a+client+application+to+HelseID). Et Request Object som overføres til HelseID skal være en [JWT](https://datatracker.ietf.org/doc/html/rfc7519).

*Steg 4:* 
Resultatet av kallet til /authorize endepunktet i HelseID er en _authorization code_ som EPJ tar vare på, [som angitt i spesifikasjonen av OpenID Connect](https://openid.net/specs/openid-connect-core-1_0.html#AuthResponse). EPJ må bruke _authorization_code_ når den ber HelseID om å utstede et nytt Access Token som gir tilgang til Kjernejournal Portal. 

### 4.2 Hent Access Token fra HelseID (steg 5 og 6 i sekvensdiagrammet)
*Steg 5:*
For å få utlevert et Access token som gir tilgang til pasientopplysninger/dokumentdeling i Kjernejournal portal, må EPJ bruke samme _authorization code_ som den mottok i *_steg 4* for å hente et Access Token i _/token_ endepunktet i HelseID.

#### Krav til klientautentisering i _/token endepunktet_
EPJ må autentiseres ved alle kall til _/token_ endepunktet ved bruk av _client-assertion_ mekanismen. [Dette er beskrevet i HelseID sin dokumentasjon.](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID).

_*Eksempel på http POST request ved bruk av client_assertion:*_
```
POST /token HTTP/1.1
     Host: server.example.no
     Content-Type: application/x-www-form-urlencoded

     grant_type=authorization_code
     &code=SplxlOBeZQQYbYS6WxSbIA&
     &code_verifier=bEaL42izcC-o-xBk0K2vuJ6U-y1p9r_wW2dFWIWgjz-
     &client_assertion_type=urn%3Aietf%3Aparams%3Aoauth
     %3Aclient-assertion-type%3Asaml2-bearer
     &client_assertion=PHNhbW 8< ... >8 ZT
```

*Steg 6:*
En vellykket POST request mot /token endepunktet i HelseID gir en http Response som inneholdler følgende: 
 * et Access Token, som skal brukes i kallet til KJP-API
 * et Refresh Token, som kan brukes til å be om et nytt Access Token
 * metadata: utløpstidspunkt, m.m.

_*Eksempel på HTTP response etter HTTP request mot /token endepunktet:*_
```JSON
     HTTP/1.1 200 OK
     Content-Type: application/json;charset=UTF-8
     Cache-Control: no-store
     Pragma: no-cache

     {
       "access_token":"2YotnFZFEjr1zCsicMWpAA",
       "token_type":"bearer",
       "expires_in":3600,
       "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
     }
```

#### 4.2.1 Håndtering av Access Token livssyklys (steg 18 og 19 i sekvensdiagrammet)
Access Tokenet som EPJ systemet mottar fra HelseID vil ha begrenset levetid. EPJ systemet må derfor selv holde orden på om et Access Token er gyldig eller ikke.

Dette gjøres ved å kontrollere attributtet "exp" i Access Tokenet. "exp" er en forkortelse for "expiration time", og angir tidspunktet når tokenets gyldighet utløper

Dersom tokenets levetid er utløpt må EPJ be om et nytt token basert på tilgangen som ble opprettet i steg 2 og 3. Dette gjøres ved å bruke _refresh_token_ flyten, som er spesifisert [i OAuth 2.0 spesifikasjonen](https://datatracker.ietf.org/doc/html/rfc6749#section-1.5). 

*Når EPJ har mottatt ett nytt Access Token må også brukersesjonen i KJ oppdateres. Se [4.5.1 Hold sesjonen i KJ i live](#451-hold-sesjonen-i-live)*

##### Klientautentisering ved refresh_token flyt
På samme måte som ved andre kall til /token endepunktet i HelseID må klienten autentiseres ved bruk av _client_assertions_, [som angitt i HelseID sin dokumentasjon](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID).

## 4.3 Opprett brukersesjon i Kjernejournal Portal (steg 7 og 8 i sekvensdiagrammet)
For å unngå å sende sensitive personopplysninger som url-parametre i http GET forespørselen til Kjernejournal Portal må alle EPJ systemer opprette en brukersesjon i Kjernejournal Portal før de åpner nettsidene. Opprettelse av brukersesjon i Kjernejournal beskrives i steg 7 og 8. 

*Steg 7:*
For å opprette en ny brukersesjon må EPJ sende en HTTP POST request til url KJP-API-URL/api/Session/create.

HTTP POST body må inneholde parametre som angir:
* pasient-id
* samtykkegrunnlag

#### Steg 7: Beskyttelse mot misbruk av sesjon
HTTP response fra url KJP-API-URL/api/Session/create inneholder en kode som EPJ må benytte for å angi den aktive sesjonen når den ber om tilgang til en gitt pasient (Steg 9.). 

For å beskytte mot tyveri og misbruk av koden krever Kjernejournal Portal en beskyttelse som er basert på protokollen som er beskrevet i [PKCE spesifikasjonen](https://datatracker.ietf.org/doc/html/rfc7636#section-4.1). 

Oppsummert:
1. EPJ må generere verdien _ehr_code_verifier_, en kryptografisk tilfeldig verdi basert på tegn som er [definert som gyldige i en URI](https://datatracker.ietf.org/doc/html/rfc3986#section-2.3).
2. EPJ må generere verdien _ehr_code_verifier_ ved følgende metode:
  * Base64UrlEncode(SHA256(ASCII(_ehr_code_verifier_)))

I kallet til skal _ehr_code_challenge_ legges ved som parameter i HTTP body.

#### Steg 7: Eksempel på HTTP POST request med _ehr_code_challenge_
I tillegg til andre parametre må EPJ legge ved Access token utstedt fra HelseID i Authorization Header.

```http request
POST /api/Session/create/
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkE4...u_UjgeTxzxI2g

{"ehr_code_challenge": <sha256(nonce)>, "patient-id": "ca2gveFcW%2BdZ..."}
```

*Steg 8:*
Når brukersesjonen i Kjernejournal er opprettet vil KJP-API utstede en kode til engangsbruk som EPJ må bruke i steg 9.

I respons får man opprettet en http session, og får en engangs-kode i svar som bruks ved åpning av Kjernejournal Portal.

```http request
200 OK
Content-Type: application/json
Set-Cookie: <session-cookie>

{"code": "edfda05c-dbe7-44..."}
```

## 4.4 Vis pasient i Kjernejournal Portal (steg 9 i sekvensdiagrammet) 
Kjernejournal vil hente pasient-id, samtykkegrunnlag og Access token fra APIet i steg 3. For å gi tilgang til _hentpasient.html_ trenger Kjernejournal koden som EPJ fikk i retur fra api/Session/create og en hash av nonce-verdien som ble sendt i body.
Disse verdiene overføres som query parametre i GET requestens url.

Denne innloggingsflyten innfører to nye parametre i http meldingen, verdien til disse parametrene skal være:
* code: koden som EPJ mottok i http response fra kall til _KJP-API-URL/api/Session/create_.
* nonce: nonce verdien som ble overført i kallet til _KJP-API/api/Session/create_ i klartekst.

### Eksempel på http request til KJP-API/api/Session/create:

```http request

GET /hpp-webapp/hentpasient.html?code=968abbad-7192-4a66-8063-b21b639635a9&ehr_code_verifier=ukyT8vC9KZ1q2qZgt6d2Y_Wr7O9dOUyvTgBEOAAaGrE

```

## 4.5 Sesjonshåndtering i Kjernejournal Portal

### 4.5.1 Hold sesjonen i live
*Steg 20:* 
api/Session/refresh

Før Access Token utløper, må EPJ hente et nytt token fra HelseID og sende det til KJP-API-URL/api/Session/refresh.
Authorization header skal inneholde det nye Access Tokenet, og Cookie-header må være satt til samme session man fikk tilbake i createSession-kallet. 

Dette kallet har ingen body.

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


