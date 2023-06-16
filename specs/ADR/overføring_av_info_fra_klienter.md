---
parent: Architectural Decisions
date: 2023-06-14
id: 202306141
---
# Overføring av informasjon fra API-klient til HelseID ved bruk av RAR og OAuth 2.0 Assertion Framework

## Kontekst og problembeskrivelse
I forbindelse med PDS (program for digital samhandling) og utvikling av funksjonalitet knyttet til dokumentdeling i kjernejournal er det et behov for å støtte sektoren med formidling av helsepersonellets grunnlag for tilgang til pasientens helseopplysninger i sitt lokale system.

HelseID har i dag blant annet støtte for at klienten kan angi og overføre den juridiske personen og behandlingsstedet hvor et helsepersonell yter helsehjelp ved to forskjellige løsningsmønstre. Det foreslåtte designet for dokumentdeling i Kjernejournal er å bygge videre på disse mønstrene i forbindelse med dokumentdeling i kjernejournal.

Informasjon om helsepersonellets grunnlag for tilgang kan i dag overføres på en av disse måtene:
1. Ved å legge ved en "authorization_details" json-struktur i Request Object som overføres i kall til _authorize_ endepunktet.
2. Ved å legge ved en "authorization_details" json-struktur i en client-assertion som overføres til _token_ endepunktet i HelseID ved bruk av flyten angitt av _response_type=refresh_token_ (refresh token flyt).

Begge løsningene er inspirert av den åpne standarden [OAuth 2.0 Rich Authorization Requests](https://datatracker.ietf.org/doc/html/rfc9396), men avviker fra standarden på ulike måter. 

Et avvik fra [RAR standarden](https://datatracker.ietf.org/doc/html/rfc9396) er bruken av client assertions ved refresh token flyt for å endre tilgangen som blir gitt via authorize-endepunktet HelseID. Dette avviket diskuteres i avsnittet om ["authorization_details" i Client Assertions ved bruk av Refresh Token](#3-rar-og-client-assertions-ved-bruk-av-refresh-token).
Et annet avvik er at "authorization_details" strukturen i dag ikke er reflektert i Access Tokens utstedt av HelseID, og at HelseID ikke aksepterer "authorization_details" som request parameter (må være en del av Request Object i OIDC flyten).

Vår hypotese er at den overordnede problemstillingen ikke er et særtilfelle for dokumentdeling i kjernejournal portal, men at mange av de underliggende problemstillingene som fører til behovet for å gå utenfor standarder også vil gjelde for alle andre systemer.

Det er viktig å ta en rask beslutning om valgt design på grunn av at programvareleverandørene må implementere flyten i journalsystemene som skal bruke dokumentdeling i Kjernejournal.

### Diskusjon om mønster for dokumentdeling i Kjernejournal
Vi tror ikke at det totale løsningsmønsteret som er skissert for Kjernejournal Portal vil bli brukt av andre system, og må anse mønsteret som en spesialtilpassing for Kjernejournals spesifikke behov og eksisterende proprietære token mekanisme.

En grunnleggende forskjell mellom vanlige løsningsmønstre og løsningen _dokumentdeling i Kjernejournal Portal_ er at konsumenten ikke er i stand til å loggføre informasjon om helsepersonellets grunnlag for tilgang i forbindelse med innsyn i journaldokument i andre virksomheter for hvert innsyn. Vi antar at det derfor er behov for å overføre større mengder informasjon om helsepersonellets grunnlag enn normalt til dokumentkilden via Kjernejournal.

Dokumentdeling i Kjernejournal skiller seg fra _normal_ bruk av HelseID på flere måter. Blant annet overlapper Kjernejournals eksisterende flyt for deres proprietære token løsning og proof of possession mekanismer med lignende mekanismer i HelseID. I tillegg har konsumenten et behov for å overføre mer informasjon til dokumentkilden enn de ville ha gjort i en situasjon hvor konsumenten var i stand til å logge tilgangene som blir gitt til dokumentene selv, fordi dokumentkilden må dokumentere tilgangen på vegne av konsumenten.

## Alternativer som er vurdert
Det finnes to åpne standarder som kan benyttes for å overføre informasjon fra API-klient til API via HelseID.

Vi har vurdert hvorvidt HelseID skal tilby følgende alternativer i forbindelse med spesifikasjon for programvareleverandørene som skal implementere integrasjon mot dokumentdeling i Kjernejournal:

1. Bare overføre informasjon ved bruk av [OAuth 2.0 Rich Authorization Requests](https://datatracker.ietf.org/doc/html/rfc9396)
2. Bare overføre informasjon ved bruk av [Assertion Framework for OAuth 2.0 Client Authentication and Authorization Grants](https://datatracker.ietf.org/doc/html/rfc7521)
3. Å tillate både [OAuth 2.0 Rich Authorization Requests](https://datatracker.ietf.org/doc/html/rfc9396) og [Assertion Framework for OAuth 2.0 Client Authentication and Authorization Grants](https://datatracker.ietf.org/doc/html/rfc7521) for å overføre "authorization_details".

## Beslutning
Team tillit og Team A&A anbefaler at HelseID støtter alternativ 3, men mener at HelseID bør peke på bruk av RAR som primært løsningsmønster for dokumentdeling i Kjernejournal for _første versjon av spesifikasjonene_ (høst 2023).
På grunn av at støtte for alternativ 3 krever ytterligere arbeid vil Team A&A og Team Tillit jobbe videre med konseptet hvor klienten bruker client_assertions i refresh_token flyt ved behov.
Ved bruk av "authorization_details" som del av client-assertion bør løsningen spesifiseres, dokumenteres og risikovurderes.

Som følge av denne beslutningen har Team tillit og Team A&A også gjennomført en vurdering av hvordan "authorization_details" skal reflekteres i Access Tokens som er dokumentert i [et eget ADR dokument](/specs/ADR/authorization_details_i_access_tokens.md).

### Konsekvenser
For dokumentdeling i Kjernejournal Portal vil HelseID peke på eksisterende spesifikasjon av OAuth 2.0 Rich Authorization Requests.

For videre arbeid knyttet til bruk av Assertion Framework må HelseID tydeliggjøre følgende underliggende forutsetninger i sin generelle dokumentasjon og kravstilling:
- Helsepersonellet må alltid være logget på i HelseID før bruk av Assertion Framework
- Klienten må be om alle scopes ved innlogging slik at den underliggende _granten_ allerede er opprettet
- Påfølgende kall til HelseID som autorisasjonsserver baserer seg på eksisterende grants

I tillegg må team A&A risikovurdere følgende:
- refresh_token flyten i kombinasjon med client-assertion som inneholder informasjon om grunnlag for tilgang
- gjenbruk av det reservert ordet "authorization_details" for client-assertion

Det blir også nødvendig å legge inn spesifikke sjekkpunkter knyttet til implementasjonen i code-review.

## Fordeler og ulemper ved de ulike alternativene
Tilnærming til vurdering av fordeler og ulemper:
1. Vi går ikke inn i problematikk knyttet til fremtidige scenarier
2. Vi antar at vi vil gjenbruke det reserverte ordet "authorization_details" i client-assertions
3. Vi ser bort fra potensielle problemer knyttet til user consent, ettersom vi baserer oss på lovhjemmel som behandlingsgrunnlag

### 1. Bare RAR
RAR definerer et nytt http request parameter for authorize endepunktet som kalles "authorization_details", hvor klientapplikasjonen kan legge ved mer detaljert informasjon om den lokale autorisasjonen som sluttbrukeren har fått i sitt system.

* Uheldig fordi brukeropplevelsen forringes for webbaserte klienter på grunn av at nettleser må hoppe ut til en annen applikasjon (HelseID) og dermed forårsaker blinking i grensessnittet.
* Uheldig for single-page-applikasjoner i nettleser (uvisst hvorvidt dette er problematisk for andre typer applikasjoner), fordi nettleser må åpne en annen applikasjon (HelseID) som medfører økt kompleksitet i spa-applikasjonen for å ta vare på brukersesjon.
* Kan være uheldig for systemer med kompleks systemarkitektur, fordi systemleverandøren må implementere meldingsflyt mellom nettleseren og bakenforliggende systemkomponenter og synkronisere brukersesjoner i nettleser med brukersesjoner på serversiden.
* Heldig (tillit), fordi det er en åpen internettstandard og har gjennomgått grundig sikkerhetsanalyse.
* Heldig (tillit), fordi det er en åpen internettstandard og dermed vil bli støttet i forskjellig programvare og programvarebibliotek.
* Heldig (tillit), fordi løsningen gir en veldefinert og sikker måte å overføre informasjon om den lokale tilgangen fra klient til API.

### 2. Overføre informasjon ved bruk av _client-assertions_ i refresh_token flyt til token endepunktet
I dette løsningsmønsteret inkluderer klienten en json struktur som inneholder en datamodell som beskriver helsepersonellets grunnlag for tilgang i en client_assertion. 

HelseID implementerer i dag Client Assertion spesifikasjonen for å tilby sterk klientautentisering, men benytter seg ikke av muligheten til å legge ved autorisasjonsinformasjon som spesifikasjonen også beskriver.

* Uheldig, fordi fordi mønsteret ikke er spesifisert i en åpen internettstandard
* Uheldig, fordi fordi vi selv må spesifisere og forvalte spesifikasjonen.
* Heldig (tillit), fordi det allerede er påkrevd bruk av private_key_jwt som klientautentiseringsmekanisme, derfor må klienten opprette en client_assertion uansett. Mønsteret bygger videre på denne mekanismen.
* Heldig, fordi meldingene foregår via backend kall.
* Heldig, fordi det er enklere for leverandørene å implementere dette mønsteret.
* Heldig, fordi mønsteret allerede er implementert i mesteparten av programvaren i sektoren.

### 3. Både bruk av RAR og _client-assertions_ i refresh_token flyt til token endepunktet

* Uheldig, fordi det øker kompleksiteten hos NHN - vi må forvalte to løsningsmønstre.
* Uheldig, fordi det kan være forvirrende for leverandørene.
* Heldig, fordi det gir programvareleverandørene flere alternative løsningsmønstre.

## Ytterligere informasjon
