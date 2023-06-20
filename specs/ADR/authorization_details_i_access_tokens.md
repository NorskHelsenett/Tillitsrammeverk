---
parent: Architectural Decisions
date: 2023-06-14
id: 202306142
---
# OAuth 2.0 Hvordan skal HelseID reflektere "authorization_details" JSON struktur i Access Token

## Kontekst og problembeskrivelse
Som følge av at HelseID vil implementere spesifikasjonen Rich Authorization Requests må HelseID ta noen valg knyttet til informasjon som skal reflekteres i Access Tokens som blir utstedt av HelseID.

Utfordringene vi har identifisert er gruppert i tre kategorier:
1. HelseID vil tilby overføring av informasjon i parameteret "authorization_details" ved bruk av både _Request Objects_ i _authorize endepunktet_ og _client-assertion_ i refresh_token flyten mot _token endepunktet_. Skal begge tilnærmingene reflekteres på samme måte i Access Tokens utstedt av HelseID?
2. HelseID har spesifisert at de enkelte claims i "authorization_details" fra klienten inneholder færre informasjonselementer enn den reflekterte strukturen i Access Tokens utstedt av HelseID. Bør HelseID både berike strukturen med claims som ikke er definert av klieten, og i tillegg berike de enkelte claims som klienten har overført i http requesten med ytterligere informasjon? Innebærer dette noen risiko?
3. HelseID utsteder i dag Access Tokens med claims som beskriver den samme informasjon som vil bli overført i "authorization_details" strukturen, dette kan medføre problemer for tjenestene som mottar access tokens. Hvordan skal vi håndtere duplisert informasjon når vi tar i bruk "authorization_details" som skissert i dokumentdeling?

## Alternativer som er vurdert

1. Skal den innkommende _"authorization_details"_ strukturen reflekteres på samme måte i Access Tokens utstedt av HelseID når de kommer fra både _token endepunktet_ og _authorize_ endepunktet?
    - Alternativ 1: HelseID bruker forskjellig navngivning på informasjon som kommer via _authorize_ endepunktet og _token_ endepunktet ved å benytte "authorize_details" ved bruk av _authorize endepunktet_, og et annet navn ved bruk av _token endepunktet_, både i http request og i access tokens.
    - Alternativ 2: HelseID bruker "authorization_details" både for informasjon som kommer via _authorize_ endepunktet og _token_ endepunktet, både i http request og i access tokens.
2. Bør HelseID både berike strukturene som blir overført i http requests fra klienten med claims som ikke er definert av klienten, og i tillegg berike de enkelte claims som klienten har overført i http requesten med ytterligere informasjon i Access Tokens?
3. Hvordan skal vi håndtere duplisert informasjon når vi tar i bruk "authorization_details" som skissert i dokumentdeling?


## Beslutning

### Skal den innkommende _"authorization_details"_ strukturen reflekteres på samme måte i Access Tokens utstedt av HelseID når de kommer fra både _token endepunktet_ og _authorize_ endepunktet?
RAR-spesifikasjonen beskriver hvordan en klient kan bruke _token endepunktet_ til å angi hvilke autorisasjonsdetaljer HelseID skal reflektere i et Access Token. I spesifikasjonen er det beskrevet at autorisasjonsserveren skal kontrollere at den underliggende tilgangen (gitt i _authorize endepunktet_) tillater utstedelsen av et access token med de forespurte autorisasjonsdetaljene.

Vår konklusjon er at HelseID kan tillate endring av underliggende grant ved bruk av _refresh_token_ flyt i _token endepunktet_ på grunn av følgende forutsetninger:
- Helsepersonellets behandlingsgrunnlag er hjemmelsbasert, HelseID tilbyr derfor ikke eksplisitt samtykke i _authorize endepunktet_ (selv om vi teknisk tilbyr muligheten).
- Det er systemets oppgave å sannsynliggjøre ovenfor HelseID at det foreligger et behandlingsgrunnlag (hjemmel + tjenstlig behov), ikke sluttbrukeren.
- Helsepersonellet vil vanligvis ha en sesjonsvarighet for sin pålogging i HelseID på en arbeidsdag. Sesjonene blir etter pålogging ivaretatt av refresh_token flyt, og sluttbrukeren skal ikke autentiseres på nytt med mindre Relying Party avslutter sesjonen.
- Å kreve bruk av _authorize endepunktet_ har uheldige praktiske følger for noen programvareleverandører, som må håndtere unødvendig kompleksitet knyttet til å ivareta brukersesjonen i sine system.

Vår konklusjon er også at vi gjenbruker "authorization_details" json struktur både for _authorize endepunktet_ og ved refresh_token flyt i _token endepunktet_ fordi:
- å forvalte to forskjellige strukturer medfører kompleksitet som må forvaltes både for HelseID og programvareleverandørene.
- to forskjellige strukturer kan være forvirrende for mottakere av access tokens.

#### Konsekvenser
På grunn av at det er besluttet å støtte en protokollflyt som ikke er definert i eksisterende åpne standarder, må NHN selv spesifisere vår utvidelse av protkollene. Denne spesifikasjonen må beskrive vår bruk av "authorization_details" for refresh_token flyt i token ved bruk av client-assertions, og hvordan dette skal reflekteres i access tokens.

Spesifikasjonene skal inneholde avsnitt som beskriver konsekvenser for sikkerhet og personvern, basert på en risiko- og personvernsanalyse gjennomført av NHN.


### Bør HelseID både berike strukturene som blir overført i http requests fra klienten med claims som ikke er definert av klienten, og i tillegg berike de enkelte claims som klienten har overført i http requesten med ytterligere informasjon i Access Tokens?
I informasjons- og datamodellen for tillitsrammeverket og dokumentdeling i kjernejournal er det lagt opp til en struktur hvor hvert informasjonselement beskrives med et sett av verdier som er definert i et kodeverk.

Eksempel på en slik struktur:
````JSON
"info-element": {
	"code": "x",
	"text": "tekst som beskriver kodeverdien",
	"system": "urn:oid:x.xx.xxx.x.xx.x.x.x.xxxx",
	"assigner": "https://www.ansvarlig-for-kodeverk.no/"
}
````
Vår konklusjon er at HelseID vil redusere mengden informasjon som overføres fra RP/klient ved å fjerne alle claims som HelseID selv kan berike ved utstedelse av Access Tokens. HelseID tillater altså en smalere datamodell i http request fra klient/RP sammenlignet med Access Tokens.

Som et konkret eksempel vil strukturen vist ovenfor kunne overføres fra klienten uten attributter som "text", "name" og "assigner" claimene:
````JSON
"info-element": {
	"code": "x",
	"system": "urn:oid:x.xx.xxx.x.xx.x.x.x.xxxx",
}
````

I tillegg vil HelseID å berike selve "authorization_details" strukturen med informasjon som klienten ikke har overført. Dette kan være informasjon som HelseID selv er i besittelse av, eller informasjon fra andre kilder i NHN eller nasjonale autoritative kilder.

#### Konsekvenser
Beslutningen innebærer at HelseID må programmeres til å hente nødvendige verdier for å fylle ut felter i Access Tokens som er beskrevet i datamodellen for beskrivelse av helsepersonellets grunnlag for tilgang.

### Hvordan skal vi håndtere duplisert informasjon når vi tar i bruk "authorization_details" som skissert i dokumentdeling?
HelseID utsteder i dag Access Tokens hvor flere  attributter overlapper med attributter som vil bli overført via "authorization_details" fra RP/klient. Dette kan medføre flere utfordringer:
- det kompliserer intern behandling av attributter i HelseID
- det kan være forvirrende for mottakere av Access Tokens fordi
    - verdiene potensielt kan være forskjellige, selv om de tilsynelatende skal beskrive det samme
    - det kan være kompliserende å måtte behandle samme verdier fra forskjellige attributter i samme token

Vår konklusjon er at vi på overordnet nivå ønsker å unngå å duplisere informasjon i Access Tokens, og at vi derfor bør fjerne eksisterende attributter som også er definert i datamodellen for "authorization_details".
- NHN må informere alle systemer som bruker HelseID om fjerning av eksisterende attributter/claims
    - programvareleverandører og systemleverandører må få en overkommelig tidsfrist
    - attributter som skal fjernes må markeres som "utgående" eller lignende i dokumentasjon så raskt som mulig
- HelseID beholder eksisterende attributter/claims som er duplisert i "authorization_details" fram til tidsfristen er utløpt
- Dersom HelseID mottar en "authorization_details" struktur som inneholder andre verdier enn eksisterende attributter skal verdiene i "authorization_details" fra RP/klient overstyre verdiene i eksisterende attributter.
- Verdier i eksisterende attributter skal ikke reflekteres i "authorization_details" eller i tillitsankerstrukturen


## Ytterligere informasjon
