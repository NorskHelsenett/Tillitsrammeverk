# Spesifikasjon av tilgangskontroll for pasientens journaldokumenter i Kjernejournal Portal

## Sammendrag
Dette dokumentet er en spesifikasjon av tilgangsstyring for journalsystemer som skal integreres med Kjernejournal Portal for dokumentdeling i andre scenarier enn for fastlegene som allerede har innført dokumentdeling i Kjernejournal Portal.

Målgruppen for dette dokumentetet er personell hos programvareleverandørene som skal implementere integrasjonen.

## Dokumentets status
| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| 1 | Første utkast | 01.06.2023 |
| 2 | Versjon klar til sektor input | 19.06.2023 |

Spesifikasjonen vil bli versjonert for å støtte endringer over tid.

## Innholdsfortegnelse
1. [Innledning](#1-innledning)
2. [Beskrivelse av tilgangsstyring for dokumentdeling i Kjernejournal](#2.-Beskrivelse-av-tilgangsstyring-for-dokumentdeling-i-Kjernejournal)
3. [Sekvensdiagram som beskriver meldingsflyt](#3.-Sekvensdiagram-som-beskriver-meldingsflyt)
4. [Spesifikasjon](#4.-Spesifikasjon)
5. [Sikkerhets- og personvernhensyn](#5-sikkerhets--og-personvernshensyn)


## 1. Innledning 
Tilgangsstyring for pasientens journaldokumenter gjennom Kjernejournal Portal er basert på en modell tilpasset helsesektoren, hvor partenenes ansvar er tydeliggjort og oppgaver er fordelt i form av et avtalebasert tillitsrammeverk. Den konsumerende virksomheten skal utføre tilgangsstyring til pasientens helseopplysninger på vegne av dokumentkilden.

Tillitsrammeverket stiller underliggende krav til tilgangsstyring som alle aktører forplikter seg til å etterleve. I tillegg vil NHN, i sin rolle som tillitsanker for sektoren, tilby tillitstjenester som aktørene skal benytte i delingen.

NHN sørger for at:
* helsepersonellet blir autentisert med tilstrekkelig høyt sikkerhetsnivå
* virksomheten hvor helsepersonellet yter helsehjelp er en helsevirksomhet
* eventuelle databehandlere har rett til å opptre på helsevirksomhetens vegne
* journalsystemet som helsepersonellet benytter er kjent
* all utveksling av data mellom NHNs tillitstjenester og konsumentens journalsystem er sikret mot kjente sikkerhetsangrep og misbruk

For å gjøre dokumentkilden i stand til å utføre sine plikter knyttet til ytterligere tilgangsstyring og dokumentasjon av tilgangen må den konsumerende virksomheten overføre informasjon som beskriver grunnlaget for tilgangen. På grunn av at tilgangsstyring er implementert på forskjellig måte i forskjellige systemer og virksomheter er det nødvendig at konsumentene og dokumentkildene samler seg om et felles språk for å uttrykke grunnlaget for tilgang slik at aktørene kan forstå hverandre. Et felles språk vil også bidra til å kommunisere på en konsistent måte til innbygger.

Dette dokumentet spesifiserer de tekniske og semantiske kravene til meldingsflyten mellom konsumentens journalsystem og tjenestene HelseID og Kjernejournal Portal.

## 2. Beskrivelse av tilgangsstyring for pasientens journaldokumenter i Kjernejournal Portal
Tilgangsstyring og tilgangskontroll for pasientens journaldokumenter i Kjernejournal Portal består av oppgaver som utføres hos alle aktører som er involvert i verdikjeden, og utføres både i en forberedende fase og i kjøretid.

*Tilgangsstyring i forberedende fase:*
1. Konsumenten styrer tilgangen som helsepersonellet skal ha i journalsystemet som brukes
2. Konsumenten og NHN styrer tilgangen som journalsystemet og virksomheten skal ha til Kjernejournal Portal ved å bruke HelseID

*Tilgangskontroll i kjøretid:*
1. Journalsystemet utfører tilgangskontroll når helsepersonellet åpner pasientjournalsystemet, og når helsepersonellet ber om tilgang til opplysninger om sin pasient
2. Konsumentens journalsystem ber om tilgang til Kjernejournal Portal i kjøretid, og overfører samtidig data som beskriver beslutning om helsepersonellets tilgang til pasienten
3. HelseID utfører tilgangskontroll når journalsystemet ber om tilgang til Kjernejournal Portal i kjøretid
4. HelseID sørger for at helsepersonellet blir autentisert i henhold til krav
5. HelseID beriker tilgangen med informasjon om helsepersonellet
6. HelseID utsteder en tilgangsbillett (Access Token) til konsumentens journalsystem
7. Konsumentens journalsystem åpner Kjernejournal Portal, og legger ved tilgangsbillett
8. Kjernejournal Portal utfører tilgangskontroll ved å kontrollere tilgangsbillett utstedt av HelseID 


### 2.1 Sekvensdiagram som beskriver hendelser i kjøretid på systemnivå
````mermaid
sequenceDiagram 
title Systemkontekst

actor HP as Helsepersonell
participant EPJ
participant HelseID
participant KJP
participant Dokumentkilde

HP->>EPJ: Åpner pasientkontekst
EPJ->>EPJ: Utfører tilgangskontroll
EPJ-->>HP: Gir tilgang til pasientens helseopplysninger
HP->>EPJ: Ber om tilgjengelige dokumenter i KJP
EPJ->>HelseID: Ber om tilgang til KJP, overfører datamodell for tilgangsbeslutning
HelseID-->>EPJ: Leverer Access Token
EPJ->>KJP: Oppretter brukersesjon
EPJ->>KJP: Åpne pasient og legger ved Access Token
KJP-->>HP: Viser pasient
HP->>KJP: Åpne pasientens journaldokumenter
KJP->>Dokumentkilde: Hent dokumentoversikt, legger ved SAML token
Dokumentkilde-->>KJP: Leverer dokumentoversikt
KJP-->>HP: Viser dokumentoversikt
HP->>KJP: Hent dokument
KJP->>Dokumentkilde: Hent dokument
Dokumentkilde-->>KJP: Leverer dokument
KJP-->>HP: Leverer dokument
````

### 2.2 Datamodell for beskrivelse av grunnlaget for tilgangsbeslutning
Datamodellen for beskrivelse av grunnlaget for tilgangsbeslutningen i konsumentens journalsystem skal overføres fra konsument til dokumentkilde. Modellen er delt i to:

1. Attributter tilknyttet tillitsrammeverk for deling av helseopplysninger i helsesektoren
2. Attributter for beskrivelse av grunnlaget ved pasientens journaldokumenter i Kjernejournal Portal

#### 2.2.1 Attributter tilknyttet tillitsrammeverket
Tillitsrammeverket for deling av helseopplysninger omfatter en informasjonsmodell som beskriver et helsepersonells digitale identitet ved en forespørsel om tilgang til helseopplysninger om sin pasient.
Informasjonen som dekkes av tillitsrammeverket svarer på følgende spørsmål:
* Hvem er helsepersonellet?
* Hvilke formelle autorisasjoner og/eller lisenser har helsepersonellet?
* Hvilken virksomhet har dataansvar for journalsystemet som helsepersonellet benytter?
* Ved hvilket behandlingssted yter helsepersonellet helsehjelp?


Detaljer om informasjons- og datamodell for tillitsrammeverket finnes [i spesifikasjonen](/specs/datamodell_tillitsmodell.md).

Legg merke til at konsumentens journalsystem er informasjonskilde for to informasjonselementer:
* Den dataansvarliges identitet (juridisk enhet)
* Behandlingssted (virksomhet)

#### 2.2.2 Attributter for dokumentdeling
På grunn av den tekniske arkitekturen som er valgt for pasientens journaldokumenter i Kjernejournal Portal er ikke den konsumerende virksomheten i stand til å loggføre tilgangene i henhold til gjeldende regelverk. Derfor må ytterligere informasjon om den lokale tilgangen til dokumentkilden.

For å dekke dette behovet er det definert en datamodell som beskriver ytterligere detaljer ved den lokale tilgangen.
[Datamodellmodell for beskrivelse av helsepersonellets grunnlag for tilgang i pasientens journaldokumenter](/specs/datamodell_dokumentdeling.md).


## 3. Beskrivelse av HTTP meldingsflyt
Denne spesifikasjonen skiller seg fra den eldre løsningen hvor EPJ må bruke virksomhetssertifikat og SOAP-baserte meldinger via helseindikator-tjenesten.

Sekvensdiagrammene i dette kapittelet beskriver meldingsflyt mellom journalsystem, HelseID og KJP for pasientens journaldokumenter i Kjernejournal Portal. 

Sekvensdiagrammet beskriver ikke meldingsflyt mellom tjenester i NHN og dokumentkilden.

*Diagram 1: meldingsflyt for tilgang til pasientens journaldokumenter i Kjernejournal Portal*
````mermaid
sequenceDiagram 
  autonumber
  title Diagram 1: meldingsflyt for tilgang til pasientens journaldokumenter i Kjernejournal Portal
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
  EPJ->>KJP: POST KJ-API/session/create
  KJP-->>EPJ: code
  EPJ->>KJP: GET hentpasient.html?otc=code&ehr_code_verifier=code_verifier&[ytterligere parametre]
  HP->>KJP: Åpner fanen journaldokumenter

  KJP->>Dokumentkilde: Hent referanseliste
  Dokumentkilde-->>KJP: referanseliste
 
  KJP-->>HP: Viser referanseliste
  HP->>KJP: Åpner et journaldokument
  KJP->>Dokumentkilde: Hent dokument
  Dokumentkilde-->>KJP: dokument
  KJP-->>HP: vise dokument

  ````

*Diagram 2: meldingsflyt ved utløpt Access Token:*
````mermaid
sequenceDiagram 
  autonumber
  title Digram 2: meldingsflyt ved utløpt Access Token
  participant EPJ
  participant HelseID
  participant KJP

   critical sjekk gyldighet på access token

    option Access Token er utløpt
        EPJ->>HelseID: POST /token?response_type=refresh_token..8<>8
        HelseID-->>EPJ: Access Token
        EPJ->>KJP: POST KJ-API/session/refresh (Authorization: bearer AccessToken) 
        KJP-->>EPJ: HTTP 200 (OK)
  end

````

*Diagram 3: meldingsflyt når helsepersonellet bytter pasient:*
````mermaid
sequenceDiagram 
  autonumber
  title Diagram 3: meldingsflyt når helsepersonellet bytter pasient
  participant EPJ
  participant KJP

  critical helsepersonell bytter pasient
  option hvis brukersesjon er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid) EPJ-->>EPJ start ny sesjon
    EPJ->>EPJ: start ny sesjon mot KJ (hovedflyt som beskrevet i diagram 1)
  end  

````

*Diagram 4: meldingsflyt når brukersesjon i EPJ utløper på tid:*
````mermaid
sequenceDiagram 
  autonumber
  title Diagram 4: meldingsflyt når brukersesjon i EPJ utløper på tid
  participant EPJ
  participant KJP

  critical brukersesjon i EPJ timer ut
  option hvis brukersesjon er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)
  end

  critical brukeren lukker EPJ system
  option hvis bruersesjon er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)

end 
````

*Diagram 5: meldingsflyt når brukeren lukker EPJ system:*
````mermaid
sequenceDiagram 
  autonumber
  title Diagram 4: meldingsflyt når brukeren lukker EPJ system
  participant EPJ
  participant KJP

  critical brukeren lukker EPJ system
  option hvis brukersesjon er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)

end 
````

## 4. Spesifikasjon
Denne spesifikasjonen gir en detaljert beskrivelse av meldingsflyten i sekvensdiagrammet over.

De enkelte systemene hos NHN som deltar i meldingflyten har ytterligere relevante krav som ikke beskrives i denne spesifikasjonen. Kravene omfatter blant hvordan pasientidentifikator og samtykkegrunnlag skal overføres fra konsument til NHN.

| | |
| --- | --- |
| Bruk av HelseID for Kjernejournal | [Veileder](https://kjernejournal.atlassian.net/wiki/spaces/KJERNEJOURDOK1/pages/786989408/Integration+Guide+Kjernejournal+REST+API+using+HelseID+as+authenticator) |
| Krav til systemleverandører som vil ta i bruk HelseID | [Krav til systemleverandører](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/490930177/HelseID+Client+Requirements) |
| Nettverksoppsett for bruk av HelseID | [Tekniske krav til kjøretidsmiljø](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/5571114/Technical+requirements+for+using+HelseID) |
| Sikkerhtsprofil for HelseID | [Sikkerhetsprofil for HelseID-klienter](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/128352260/Security+profile+for+clients+using+HelseID) |
| Teknisk dokumentasjon | [Claims, scopes og endepunkter](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/58916865/Technical+reference) |
### 4.1 Autentiser helsepersonellet via HelseID (steg 2, 3 og 4 i sekvensdiagrammet)
````mermaid
sequenceDiagram 
  autonumber
  title Diagram 1: meldingsflyt for tilgang til pasientens journaldokumenter i Kjernejournal Portal
  actor HP as Helsepersonell
  participant EPJ
  participant HelseID
  
  HP->>EPJ: Åpner KJP
  rect rgb(100, 100, 100)
  EPJ->>EPJ: generer Request Object (tillitsmodell og dokumentdeling)
  EPJ->>HelseID: POST /authorize (request_object)
  HelseID-->>EPJ: Authorization Code
  end

````


For å logge på brukeren via HelseID må EPJ åpne en nettleser som sender en forespørsel om autentisering av helsepersonellet og tilgang til Kjernejournal Portal. EPJ må legge ved informasjon som beskriver helsepersonellets grunnlag for tilgang til pasientens helseopplysninger i forespørselen.

HelseID sørger for å autentisere helsepersonellet i henhold til gjeldende retningslinjer i tillitsrammeverket.

#### *Steg 2 og 3:* HTTP POST request til /authorize endepunktet

_*Eksempel på http POST request mot /authorize:*_
```
POST /connect/authorize HTTP/1.1
     Host: helseid-sts.test.nhn.no
     Content-Type: application/x-www-form-urlencoded

     client_id=122de46c-a7dd-443f-8892-f6e05cb4aa66
     &scope=openid%20profile 8< ... >8
     &redirect_uri=https://example.com/callback 
     &response_type=code
     &request=eyJhbGciOiJSUzI1NiIsImtpZ 8< ... >8
     &state=3eI1NiIsImt 8< ... >8
     &nonce=6382295010326855 8< ... >8
     &code_challenge=4T7_IIdgSvF1Yfa0Cmkklx 8< ... >8
     &code_challenge_method=S256
```

EPJ må samle nødvendig informasjon om helsepersonellet som angitt i følgende spesifikasjoner:
* [Datamodell for tillitsrammeverk](datamodell_tillitsmodell.md)
* [Datamodell for dokumentdeling](datamodell_dokumentdeling.md)

Attributtene som EPJ har samlet må struktureres i JSON-elementet _authorization_details_, i henhold til følgende spesifikasjoner:
 * [Claims som beskriver parametre for bruk av Tillitsrammeverket](jwt_rar_profil_tillitsrammeverk.md)
 * [Claims som beskriver parametre for Dokumentdeling](jwt_rar_profil_dokumentdeling.md)

HelseID krever at _authorization_details_ strukturen overføres som et såkalt Request Object, som [angitt av HelseID sin dokumentasjon.](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/5636230/Passing+organization+identifier+from+a+client+application+to+HelseID). Et Request Object som overføres til HelseID skal være en [JWT](https://datatracker.ietf.org/doc/html/rfc7519).

#### *Steg 4:* HTTP response fra /authorize endepunktet
Resultatet av kallet til /authorize endepunktet i HelseID er en _authorization code_ som EPJ tar vare på, [som angitt i spesifikasjonen av OpenID Connect](https://openid.net/specs/openid-connect-core-1_0.html#AuthResponse). EPJ må bruke _authorization_code_ når den ber HelseID om å utstede et nytt Access Token som gir tilgang til Kjernejournal Portal. 

### 4.2 Hent Access Token fra HelseID (steg 5 og 6 i sekvensdiagrammet)
````mermaid
sequenceDiagram 
  autonumber
  title Diagram 1: meldingsflyt for tilgang til pasientens journaldokumenter i Kjernejournal Portal
  actor HP as Helsepersonell
  participant EPJ
  participant HelseID
  
  HP->>EPJ: Åpner KJP
  EPJ->>EPJ: generer Request Object (tillitsmodell og dokumentdeling)
  EPJ->>HelseID: POST /authorize (request_object)
  HelseID-->>EPJ: Authorization Code
  rect rgb(100, 100, 100)
  EPJ->>HelseID: POST /token (authorization code)
  HelseID-->>EPJ: Access Token, Refresh Token
  end

  ````

#### *Steg 5:* HTTP POST request til /token endepunktet

For å få utlevert et Access token som gir tilgang til pasientopplysninger/dokumentdeling i Kjernejournal portal, må EPJ bruke samme _authorization code_ som den mottok i [*_steg 4*](#steg-4) for å hente et Access Token i _/token_ endepunktet i HelseID.

##### Krav til klientautentisering i _/token endepunktet_
EPJ må autentiseres ved alle kall til _/token_ endepunktet ved bruk av _client-assertion_ mekanismen. [Dette er beskrevet i HelseID sin dokumentasjon.](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID).

_*Eksempel på http POST request ved bruk av client_assertion:*_
```
POST /connect/token HTTP/1.1
     Host: helseid-sts.test.nhn.no
     Content-Type: application/x-www-form-urlencoded

     grant_type=authorization_code
     &code=SplxlOBeZQQYbYS6WxSbIA&
     &code_verifier=bEaL42izcC-o-xBk0K2vuJ6U-y1p9r_wW2dFWIWgjz-
     &client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
     &client_assertion=PHNhbW 8< ... >8 ZT
```

#### *Steg 6:* HTTP response fra /token endepunktet
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

#### 4.2.1 Håndtering av Access Token livssyklys
Access Tokenet som EPJ systemet mottar fra HelseID vil ha begrenset levetid. EPJ systemet må derfor selv holde orden på om et Access Token er gyldig eller ikke.

Dette gjøres ved å kontrollere attributtet "exp" i Access Tokenet. "exp" er en forkortelse for "expiration time", og angir tidspunktet når tokenets gyldighet utløper

Dersom tokenets levetid er utløpt må EPJ be om et nytt token basert på tilgangen som ble opprettet i [steg 2 og 3](#steg-2-og-3-http-post-request-til-authorize-endepunktet). 
Nytt Access Token hentes ved å bruke _refresh_token_ flyten, som er spesifisert [i OAuth 2.0 spesifikasjonen](https://datatracker.ietf.org/doc/html/rfc6749#section-1.5). 

````mermaid
sequenceDiagram 
  autonumber
  title Digram 2: meldingsflyt ved utløpt Access Token
  participant EPJ
  participant HelseID
  participant KJP

   critical sjekk gyldighet på access token

    option Access Token er utløpt
        EPJ->>HelseID: POST /token?response_type=refresh_token..8<[ og andre påkrevde parametre ]>8
        HelseID-->>EPJ: Access Token
        EPJ->>KJP: POST KJ-API/session/refresh (Authorization: bearer AccessToken) 
        KJP-->>EPJ: HTTP 200 (OK)
  end

````

*Når EPJ har mottatt ett nytt Access Token må også brukersesjonen i KJ oppdateres. Se [4.5.1 Hold sesjonen i KJ i live](#451-hold-sesjonen-i-live)*

##### Klientautentisering ved refresh_token flyt
På samme måte som ved andre kall til /token endepunktet i HelseID må klienten autentiseres ved bruk av _client_assertions_, [som angitt i HelseID sin dokumentasjon](https://helseid.atlassian.net/wiki/spaces/HELSEID/pages/541229057/Using+client+assertions+for+client+authentication+in+HelseID).

## 4.3 Opprett brukersesjon i Kjernejournal Portal
For å unngå å sende sensitive personopplysninger som url-parametre i http GET forespørselen til Kjernejournal Portal må alle EPJ systemer opprette en brukersesjon i Kjernejournal Portal før de åpner nettsidene. Opprettelse av brukersesjon i Kjernejournal beskrives i steg 7 og 8. 

````mermaid
sequenceDiagram   
  title Diagram 1: Opprett brukersesjon i Kjernejournal Portal
  participant EPJ
  participant KJP

  rect rgb(100, 100, 100)
  EPJ->>KJP: POST KJ-API/session/create
  KJP-->>EPJ: code
  end
  ````


### *Steg 7:* HTTP POST til KJP-API-URL/api/Session/create
For å opprette en ny brukersesjon må EPJ sende en HTTP POST request til url KJP-API-URL/api/Session/create.

HTTP POST body må inneholde parametre som angir:
* pasientidentifikator
* samtykkegrunnlag
* beskyttelse mot tyveri av sesjonskode

#### Ivaretagelse av pasientens konfidensialitet
Det forutsettes at all kommunikasjon mellom EPJ og NHN foregår via kryptert transport.

#### Beskyttelse mot misbruk av sesjon
HTTP response fra url KJP-API-URL/api/Session/create inneholder en kode som EPJ må benytte for å angi den aktive sesjonen når den ber om tilgang til en gitt pasient (Steg 9.). 

For å beskytte mot tyveri og misbruk av koden krever Kjernejournal Portal en beskyttelse som er basert på protokollen som er beskrevet i [PKCE spesifikasjonen](https://datatracker.ietf.org/doc/html/rfc7636#section-4.1). 

Beskrivelse:
1. EPJ må generere verdien _ehr_code_verifier_, en kryptografisk tilfeldig verdi basert på tegn som er [definert som gyldige i en URI](https://datatracker.ietf.org/doc/html/rfc3986#section-2.3).
2. EPJ må generere verdien _ehr_code_challenge_ ved følgende metode:
    * Base64UrlEncode(sha256(ascii(_ehr_code_verifier_)))
3. I HTTP POST til _KJP-API-URL/api/Session/create_ skal _ehr_code_challenge_ legges ved som parameter i HTTP body.
4. EPJ må ta vare på _ehr_code_verifier_ for videre bruk i _steg 9_ 

#### Eksempel på HTTP POST request med _ehr_code_challenge_
I tillegg til andre parametre må EPJ legge ved Access token utstedt fra HelseID i Authorization Header.

```http request
POST /api/Session/create/
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkE4...u_UjgeTxzxI2g

{"ehr_code_challenge": _ehr_code_challenge_, "patient-id": "ca2gveFcW%2BdZ..."}
```

### *Steg 8:* HTTP response fra KJP-API-URL/api/Session/create
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
* ehr_code_verifier: klartekst versjon av verdien som ble overført i parameteret _ehr_code_challenge_ i kallet til _KJP-API/api/Session/create_.

### Eksempel på HTTP GET request til /hpp-webapp/hentpasient.html:

```http request

GET /hpp-webapp/hentpasient.html?code=968abbad-7192-4a66-8063-b21b639635a9&ehr_code_verifier=ukyT8vC9KZ1q2qZgt6d2Y_Wr7O9dOUyvTgBEOAAaGrE

```

## 4.5 Sesjonshåndtering i Kjernejournal Portal

### 4.5.1 Hold sesjonen i live
Før Access Token utløper, må EPJ hente et nytt token fra HelseID og sende det til KJP-API-URL/api/Session/refresh.
Authorization header skal inneholde det nye Access Tokenet, og Cookie-header må være satt til samme session man fikk tilbake i createSession-kallet. 

````mermaid
sequenceDiagram 
  autonumber
  title Digram 2: meldingsflyt ved utløpt Access Token
  participant EPJ
  participant HelseID
  participant KJP

   critical sjekk gyldighet på access token

    option Access Token er utløpt
        EPJ->>HelseID: POST /token?response_type=refresh_token..8<>8
        HelseID-->>EPJ: Access Token
        EPJ->>KJP: POST KJ-API/session/refresh (Authorization: bearer AccessToken) 
        KJP-->>EPJ: HTTP 200 (OK)
  end

````

Denne HTTP meldingen har ikke innhold i body.

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
*Diagram 4: meldingsflyt når brukersesjon i EPJ utløper på tid:*
````mermaid
sequenceDiagram 
  autonumber
  title Diagram 4: meldingsflyt når brukersesjon i EPJ utløper på tid
  participant EPJ
  participant KJP

  critical brukersesjon i EPJ timer ut
  option hvis brukersesjon er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)
  end

  critical brukeren lukker EPJ system
  option hvis bruersesjon er aktiv
    EPJ->>KJP: POST KJ-API/session/end (sessionid)

end 
````

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


