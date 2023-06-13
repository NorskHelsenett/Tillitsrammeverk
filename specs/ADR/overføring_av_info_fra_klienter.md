---
parent: Architectural Decisions
---
# Overføre informasjon fra klient til HelseID

## Kontekst og problembeskrivelse
I forbindelse med PDS (program for digital samhandling) - dokumentdeling i kjernejournal - er det et behov for å støtte behov fra sektoren knyttet til formidling av helsepersonellets grunnlag for tilgang til pasientens helseopplysninger i sitt lokale system.

Vi antar at dette er et spesielt case for dokumentdeling i kjernejournal portal.

I dag støtter HelseID støtter HelseID at klienten kan 

RAR spesifikasjonen sier at..

Vår løsning er ikke i tråd med spesifikasjonen.

I forbindelse med Dokdeling må vi være tydelige på hva som skal benyttes.

## Alternativer som er vurdert

1. Bare RAR (lenke til spec)
2. Bare Client Assertions
3. RAR og Client Assertions med oppdatering av grant (lenke til spec)

## Beslutning

Team tillit anbefaler alternativ 3: men mener at HelseID bør peke på RAR som løsningsmønster for dokumentdeling i Kjernejournal for første _implementors draft_ av spesifikasjonene. Samtidig bør A&A jobbe videre med konseptet hvor klienten bruker client_assertions i refresh_token flyt. Ved bruk av Client Assertion Framework bør løsningen risikovurderes, samt at det bør vurderes å endre navnet "authorization_details".

HelseID anbefaler :

Ragnhild har besluttet:

HelseID bør tydeliggjøre underliggende forutsetninger:
- Pålogging 1 gang
- Be om alle scopes ved innlogging (opprette grants)
- Påfølgende kall til HelseID som autorisasjonsserver baserer seg på eksisterende grants

### Konsekvenser

Hvordan skal valget dokumenteres?
Risikovurdering av refresh_token flyten med info om grunnlag for tilgang.
Passe på navngiving (for client assertions: endre fra "authorization_details")
Risikovurder endring av navngiving...
Dersom navnet skal endres, informer leverandørene om:
HUSK Å ENDRE eksisterende "authorization_details" i json struktur til nytt navn..

Det blir viktig å legge inn spesifikke sjekkpunkter knyttet til implementasjonen i code-review

## Fordeler og ulemper ved de ulike alternativene

### 1. Bare RAR

* Uheldig fordi brukeropplevelsen forringes for webbaserte klienter på grunn av at nettleser må hoppe ut til en annen applikasjon (HelseID) og dermed forårsaker blinking i grensessnittet.
* Uheldig for single-page-applikasjoner i nettleser, fordi nettleser må åpne en annen applikasjon (HelseID) som medfører økt kompleksitet i spa-applikasjonen for å ta vare på brukersesjon.
* Kan være uheldig for systemer med kompleks systemarkitektur, fordi systemleverandøren må implementere meldingsflyt mellom nettleseren og bakenforliggende systemkomponenter og synkronisere brukersesjoner i nettleser med brukersesjoner på serversiden.
* Heldig (tillit), fordi det er en åpen internettstandard og har gjennomgått grundig sikkerhetsanalyse.
* Heldig (tillit), fordi det er en åpen internettstandard og dermed vil bli støttet i forskjellig programvare og programvarebibliotek.
* Heldig (tillit), fordi løsningen gir en veldefinert og sikker måte å overføre informasjon om den lokale tilgangen fra klient til API.

### 2. Bare Client Assertions ved bruk av Refresh Token
I dette løsningsmønsteret inkluderer klienten en json struktur som inneholder en datamodell som beskriver helsepersonellets grunnlag for tilgang i en client_assertion (som definert i ....).

* Uheldig, fordi fordi mønsteret ikke er en del av en åpen internettstandard.
* Uheldig, fordi fordi vi selv må spesifisere og forvalte spesifikasjonen.
* Heldig (tillit), fordi det allerede er påkrevd bruk av private_key_jwt som klientautentiseringsmekanisme, derfor må klienten opprette en client_assertion uansett. Mønsteret bygger videre på denne mekanismen.
* Heldig, fordi meldingene foregår via backend kall.
* Heldig, fordi det er enklere for leverandørene å implementere dette mønsteret.
* Heldig, fordi mønsteret allerede er implementert i mesteparten av programvaren i sektoren.

### 3. RAR og Client Assertions ved bruk av Refresh Token 

* Uheldig, fordi det øker kompleksiteten hos NHN - vi må forvalte to løsningsmønstre.
* Uheldig, fordi det kan være forvirrende for leverandørene.
* Heldig, fordi det gir programvareleverandørene flere alternative løsningsmønstre.

## Ytterligere informasjon
Lenke til spesifikasjonene:
* RAR
* Client Assertion Framework
