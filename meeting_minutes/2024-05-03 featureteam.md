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

### Ikke til stede

## Agenda
1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Hvordan håndterer vi verdien "description" for attributtet "decision-ref"?
3. Hvordan håndterer vi manglende kodeverk for "purpose_of_use_details"?
4. Utestående Issues og diskusjoner
5. AOB (any other business)?

## Saksgrunnlag og referat

### 1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?

### 2. Hvordan håndterer vi verdien "description" for attributtet "decision-ref"?
NHN godtar ikke at EPJ sender "description" feltet for attributtet "decision-ref" i http-meldinger til HelseID i dag. Dette betyr at feltet ikke blir inkludert i Access Tokens utstedt av HelseID.

Saken er beskrevet i [Issue #134](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/134)

HelseID redegjør kort for denne beslutningen.


### 3. Hvordan håndterer vi manglende kodeverk for "purpose_of_use_details"?
HL7 norge har fjernet kodeverket for "care-relation" fra sitt repository, og det er ikke lenger tilgjengelig.

Det er grunn til anta at HelseID ikke vil akseptere verdier i "purpose_of_use_details" som ikke kan valideres opp mot et kodeverk.

* Hvordan skal dette håndteres? 
* Hvem tar ansvar?

### 4. Utestående Issues og diskusjoner

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


### 5. AOB (any other business)?
Dersom noen har et tema de ønsker å diskutere har vi satt av ett eget punkt på agendaen for dette.
