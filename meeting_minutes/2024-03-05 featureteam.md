# Møtereferat fra møte i feature-team for informasjons- og datamodell i tillitsrammeverket - 05.03.2024

## Til stede
- Richard Husevåg (HSØ)
- Eirik Vegler Broen (Oslo Kommune)
- Sverre Martin Jensen (Oslo Kommune)
- Ronny Heitmann Andersen (Helse Vest IKT)
- Morten Stensøy (Helse Nord IKT)
- Nina Nordberg (NHN)
- Simone Vandeberg (NHN)
- Steinar Noem (NHN)
- Ragnhild Varmedal (NHN)
- Rune Andreas Grimstad (NHN)
- Kenneth Myhra (NHN)
- Øyvind Bech (NHN)

## Agenda
1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Hvordan håndterer vi verdien "description" for attributtet "decision-ref"?
3. Hvordan håndterer vi manglende kodeverk for "purpose_of_use_details"?
4. Angivelse av assigner og authority i datamodell
4. Utestående Issues og diskusjoner
5. AOB (any other business)?
6. Planlegge neste møte

## Saksgrunnlag og referat

### 1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?

Tilbakemelding fra Teamet: 
*Vi ønsker å diskutere at HelseID kan ikke ta imot angivelse av assigner (eller authority)..
Må vi rulle tilbake og snakke om grunnlaget for datamodellen?*

_Vi la til et nytt punkt i agendaen: 4. Angivelse av assigner og authority i datamodell_

### 1.5 Hilserunde for nye fjes i teamet

### 2. Hvordan håndterer vi verdien "description" for attributtet "decision-ref"?
NHN godtar ikke at EPJ sender "description" feltet for attributtet "decision-ref" i http-meldinger til HelseID i dag. Dette betyr at feltet ikke blir inkludert i Access Tokens utstedt av HelseID.

Saken er beskrevet i [Issue #134](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/134)

HelseID redegjør kort for denne beslutningen.

Richard: 
dette er ikke en tekst smo sluttbruker legger inn, men en maskingenerert tekst som beskriver beslutningsmal. Får ikke til å bygge opp noe tilsvarende med strukturerte data. Informasjonen kommer fra beslutningsmalen i DIPS, tidspunktet for innleggelse, tilhørighet til organisasjon. Det er også noen innskutte ord i verdien.

HelseID: 
dette er ikke innhold som vi kan validere, men vi ser behovet.

Eirik: 
Vi forstår behovet for å validere, men vi må forsøke å være pragmatiske. Kan attributtet settes med assigner=virksomheten, og en forhåndsdefinert oid? Det krever mye arbeid å definere et kodeverk.

Morten:
Det kan være mulig for DIPS å hente tilstrekkelig informasjon ved å kombinere verdier fra andre attributter?

Eirik:
For et legevaktsystem vil det være naturlig å sende en unik identifikator, eller eventuelt et tidspunkt. En kunne se for seg at vi starter med et statisk kodeverk, men beveger oss mot noe mer oppslagsbasert.

Sverre: 
Oslo kommune ser ikke for seg å ta dette feltet i bruk umiddelbart..

Steinar:
Burde det ikke være opp til den behandlingsansvarlige å vurdere personvernskonsekvenser og å gjennomføre eventuelle risikovurderinger? Hjemmelsgrunnlaget ligger i pasientjournalforskriften §14 - altså er det konsument/kilde som har behandlingsansvar for opplysningene. At dokumentasjonen overføres til kilden og lagres der er en del av oppgavefordelingen mellom partene, hvor NHN har rollen som databehandler.

Aksjon:
NHN/HelseID og Richard samles for å diskutere videre..
Oppdaterer Issue #134 på Github

### 3. Hvordan håndterer vi manglende kodeverk for "purpose_of_use_details"?
HL7 norge har fjernet kodeverket for "care-relation" fra sitt repository, og det er ikke lenger tilgjengelig.

Det er grunn til anta at HelseID ikke vil akseptere verdier i "purpose_of_use_details" som ikke kan valideres opp mot et kodeverk.

* Hvordan skal dette håndteres? 
* Hvem tar ansvar?

Richard: 
Dette er foreløpig et DIPS proprietært kodeverk, som gjør at vi kan kjenne igjen kodene i DIPS kodeverket.
Må kunne angi assigner og system. HelseID krever system: auditevent/hl7norway/... og godtar kodeverket slik det foreligger..


Mich:
Hva skjer når Helseplattformen skal ta dette i bruk? Må de bruke DIPS kodeverk?

Nina:
Produksjonssetting går live med dagens kodeverk.. 

Aksjon:
HelseID tar et møte med HSØ/Sykehuspartner for å gå igjennom kodene som er i bruk i dag - hva valideres?

Opprett Issues: 
* Standardisering av kodeverk (Richard) - fint om helse-midt er rundt bordet...

### 4. Angivelse av assigner og authority i datamodell

Rune:
Man oppgir en kode og system som verdien tilhører: tanken er at HelseID utleder assigner eller authority.
Dette er valgt for å minimere størrelsen/mengden data som blir sendt til HelseID.
Et system vil alltid ha en assigner eller authority, derfor har HelseID antatt at det er unødvendig at det sendes.

Morten:
Problemet er at feltene ikke er med i SAML tokenet. Det er greit at assigner og authority ikke er med i attesten fra konsumenten.

Richard:
For enkelte koder fra samme system kan det finnes forskjellige assigner.. Det kan være lokale koder fra en gitt assigner.
Det er ganske annerledes enn hva vi så for oss når vi spesifiserte. HelseID validerer mer enn det vi så for oss. NHN har en annen forståelse av risikobildet enn det vi har. Skulle gjerne ha sett at vi fikk informasjon om dette tidligere.
Jeg tror vi klarer å komme oss i gang uten at vi trenger å gjøre noen endringer, men vi må ta en dypere diskusjon om dette.

Aksjon:
Vi må opprette to issues:
* Vi må se nærmere på tilnærmingene
* Vi må rette den ene eller den andre dokumentasjonen

### 5. Utestående Issues og diskusjoner

Vi går igjennom utestående issues og behandler hvert enket issue.
Formålet er ikke nødvendigvis å saksbehandle hver issue, det viktigste er å tildele oppgaven med å løse issuet til noen.
Dersom vi kan lukke en issue i møtet er det selvfølgelig fint. 

* [Issue #31](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/31) - Beskrive featureteamets funksjon og tilhørende prosesser
* [Issue #108](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/108) - Forretningsregler for "hpr_nr"
* [Issue #117](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/117) - Forretningsregler for "patient_id"
* [Issue #133](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/133) - Struktur i forretningsreglerdokumentet
* [Issue #136](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/136) - Validering av fritekst
* [Issue #137](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/137) - Manglende JSON eksempler på "decision-ref"
* [Issue #144](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/144) - Snake-case vs kebab-case
* [Issue #145](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/145) - "hpr-nr" kodeverk vs identitet

### 6. AOB (any other business)?
Dersom noen har et tema de ønsker å diskutere har vi satt av ett eget punkt på agendaen for dette.
* Er det mulig å ta en ny diskusjon om pasientinformasjon i tokens
* Vi bør kanskje forenkle dokumentasjonen, pasientens journaldokumenter, helseid og featureteam.

### 7. Planlegge neste møte
Vi rakk ikke å gå igjennom utestående issues og diskusjoner.. Vi går igjennom dette neste fredag.
