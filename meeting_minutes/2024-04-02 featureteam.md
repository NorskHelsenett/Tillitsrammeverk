# Møtereferat fra møte i feature-team for informasjons- og datamodell i tillitsrammeverket - 02.04.2024

## Til stede
- Richard Husevåg (HSØ)
- Morten Stensøy (Helse Nord IKT)
- Nina Nordberg (NHN)
- Simone Vandeberg (NHN)
- Steinar Noem (NHN)
- Ragnhild Varmedal (NHN)
- Rune Andreas Grimstad (NHN)
- Øyvind Bech (NHN)
- Michal Cermak (NHN)
- Eirik Vegler Broen (Oslo Kommune)

### Ikke til stede
- Ronny Heitmann Andersen (Helse Vest IKT)
- Sverre Martin Jensen (Oslo Kommune)
- Kenneth Myhra (NHN)

## Agenda
1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Nye og utestående Issues og diskusjoner
3. AOB (any other business)?
4. Planlegge neste møte

## Saksgrunnlag og referat

### 1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
OK - agenda akseptert

Morten: Ok - fint å gå igjennom issues og få litt push

Ragnhild: ønsker å gi status på prodsetting av HelseID.
- i release kvitter HelseID seg med avhengigheter til virksomhetssertifikater (noen hickups i SFM)
- planlagt prodsetting ble utsatt i noen uker
- Ny prodsetting: fant feilkonfigurerte klienter hos sentrale aktører førte til at de måtte rulle tilbake rett før påske

Stor endring i HelseID
Produksjonssetting av ny versjon av HelseID 21.00 i dag
Patch-release i løpet av et par uker.
HelseID ønsker å kjøre hyppige releases etter hovedrelease

Sektoren bes om å melde tilbake ved issues

Eirik: hva innebærer validering av attesten i HelseID (ref info i utviklerportalen)?
Rune: Det kommer noen flere dokumenter som gir ytterligere forklaring på hvordan dette fungerer.

Eirik: validerer dere gyldige koder i 9151 (Iplos) for Purpose_of_use_details?
- Målet må være at utviklere ikke har kommunikasjon med NHN om hvordan mekanismene skal benyttes

Eirik: ang overføring av pasientinformasjon til HelseID er det tvetydig informasjon på dokumentasjonssidene (utviklerportal). Hva er planen for å rydde i dette?


Team A&A har allerede en oppgave på å oppdatere dokumentasjonen - oppgaven er ikke synlig utenfor NHN
Aksjon: opprett et issue på oppdatering av dokumentasjon for HelseID i

Det var en diskusjon rundt pasientid og helsepersonellets attest, som peker på at vi trenger å samle oss.. Dokumentasjon er ett perspektiv, men tillit er et annet..

Morten: Følger pasient-id med i kallet til XDS APIet (altså ikke kjernejournal)? Vi har issues som tar for oss dette..

Richard: dersom de kommersielle leverandører begynner å implementere dette kan vi få en utfordring tidsmessig.. Det må vi ta hensyn til.. Vi må få tydelig dokumentasjon, at attesten ikke er 1:1 med HelseID. Har dokumentdelings-API sin XDS tjenesten tilsvarende tjeneste som helseindikatortjenesten?


Steinar: har vi bommet når vi bruker begrepet helsepersonellets attest? Bør vi finne andre begrep eller ord.
Eirik: Vi må ivareta en viss grad av forutsigbarhet. Endringer tar lang tid i sektoren, og en utprøving sementerer seg raskt. Vi må finne ut om NHN sier et "hard nei" til overføring av pasientinformasjon.

Ragnhild: Vi går i produksjon med noe nå. Vi går i denne retningen. NHN vil ikke ta imot pasient-id i HelseID.

### 2. Utestående Issues og diskusjoner
Vi går igjennom utestående issues og behandler hvert enket issue.
Formålet er ikke nødvendigvis å saksbehandle hver issue, det viktigste er å tildele oppgaven med å løse issuet til noen. Dersom vi kan lukke en issue i møtet er det selvfølgelig fint. 

#### 2.1 Issue #108: Forretningsregler knyttet til attributtet "hpr_nr"
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/108

Morten har startet på noe her, er det behov for bistand eller samarbeid/sparring?

#### 2.2 Issue #117: Forretningsregler knyttet til attributtet patient: "patient_id"
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/117

Richard tok oppgaven, er det behov for bistand eller samarbeid/sparring?

#### 2.3 Issue #133: Forslag til struktur i forretningsregel dokumentet
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/134

Steinar skal kalle inn til eget møte med Morten og Richard.

#### 2.4 Issue #134: Description på decision-ref 
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/134

Er knyttet til [#151](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/151)

#### 2.5 Issue #136: Vurdere om alle felter med potensiell fritekst skal valideres opp mot regulæruttrykk og maksimalt antall tegn av tillitsankeret
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/136

Team A&A (Rune) holder i oppgaven.

Er knyttet til [#151](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/151)

#### 2.6 Issue #137: Vi manger "decision-ref" i JSON eksempler
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/137

Eirik har tatt oppgaven, er det behov for bistand eller samarbeid/sparring?

#### 2.7 Issue #146: Manglende kodeverk for "purpose_of_use_details" for spesialist
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/146

Team A&A (Rune) holder i oppgaven, og avtaler møte med sektor. Er det behov for fasilitering fra Team Tillt?


#### 2.8 Issue #147: Angivelse av assigner og authority i HelseID
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/147

Team A&A (Rune) holder i oppgaven, og avtaler møte med sektor. Er det behov for fasilitering fra Team Tillt?

#### 2.9 Issue #148: Endre datamodell: angivelse av assigner og authority i forespørsel til HelseID
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/148

Team A&A (Rune) holder i oppgaven, og avtaler møte med sektor. Er det behov for fasilitering fra Team Tillt?

#### 2.10 Issue #149: Standardisering av carerelation (fhir audit event)
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/149

Richard holder i oppgaven, og avtaler møte med relevante ressurser. Er det behov for fasilitering fra Team Tillt?

#### 2.11 Issue #150: Oppfølging av innspill om at ulik forståelse av risikobilde
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/150

Generelt spørsmål - sektor har en prosess gående, Er det behov for fasilitering fra Team Tillit?

#### 2.12 Issue #151: Avklaring - hvor langt strekker NHN sitt ansvar seg for å validere innhold i Tokens
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/151

Generelt spørsmål - Ragnhild har tatt oppgaven. Er det behov for fasilitering fra Team Tillit?

#### 2.13 Issue #152: Tjenstlig behov fra helsepersonell som ikke har autorisasjon i Helsepersonellregisteret
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/152

Hvem tar denne oppgaven? Er det behov for fasilitering fra Team Tillit?

#### 2.14 Issue #153: ToA
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/153

Team tillit kan ta ansvar for denne. 

#### 2.15 Issue #156: ToA kommer ikke med i SAML tokenet
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/156

Hvem kan ta denne? Team A&A, PJD?

#### 2.16 Issue #157: "care-relation" eller "care-relationship"
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/157

Navngiving: til diskusjon. Speile HL7?

### 3. AoB (Any other Business)?
Dersom noen har et tema de ønsker å diskutere har vi satt av ett eget punkt på agendaen for dette.

### 4. Planlegge neste møte
