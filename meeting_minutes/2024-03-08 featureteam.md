# Møtereferat fra møte i feature-team for informasjons- og datamodell i tillitsrammeverket - 08.03.2024

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

### Ikke til stede

## Agenda
1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Utestående Issues og diskusjoner
3. Pasientinformasjon i tokens
4. Bør/kan vi forenkle forvaltning og utvikling av spesifikasjonen?
5. AOB (any other business)?
6. Planlegge neste møte

## Saksgrunnlag og referat

### 1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?

### 2. Utestående Issues og diskusjoner
Vi går igjennom utestående issues og behandler hvert enket issue.
Formålet er ikke nødvendigvis å saksbehandle hver issue, det viktigste er å tildele oppgaven med å løse issuet til noen.
Dersom vi kan lukke en issue i møtet er det selvfølgelig fint. 

#### 2.1 Issue #31: Beskrive featureteamets funksjon og tilhørende prosesser
[Issue #31](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/31) 

#### 2.2 Issue #108: Forretningsregler for "hpr_nr"
[Issue #108](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/108)

#### 2.3 Issue #117: Forretningsregler for "patient_id"
[Issue #117](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/117) 

#### 2.4 Issue #133: Struktur i forretningsreglerdokumentet
[Issue #133](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/133)

#### 2.5 Issue #136: Validering av fritekst
[Issue #136](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/136) 

#### 2.6 Issue #137: Manglende JSON eksempler på "decision-ref"
[Issue #137](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/137)

#### 2.7 Issue #144: Snake-case vs kebab-case
[Issue #144](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/144) 

#### 2.8 Issue #145: "hpr-nr" kodeverk vs identitet
[Issue #145](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/145) 

### 3. Pasientinformasjon i tokens
Er det mulig å ta en ny diskusjon om pasientinformasjon i tokens?

Ragnhild: Synes i utgangspunktet at det ikke er en god løsning å transportere pasientid via HelseID, men skjønner at det er et behov og et ønske fra sektoren. Team A&A (HelseID) gjennomfører en DPIA, og en eventuell risikovurdering og tids/kostnadsestimering.

Eirik: Er prinsippielt helt enig med Ragnhild om det å overføre pasientid er en suboptimal løsning, men vi må være pragmatisk på kort sikt. På lengre sikt kan vi kanskje se for oss en annen løsning.

Richard: På noen områder må vi akseptere noen risikoer for å ta ned andre risikoer.

### 4. Bør/kan vi forenkle forvaltning og utvikling av spesifikasjonen?
Vi bør kanskje forenkle dokumentasjonen, pasientens journaldokumenter, helseid og featureteam.

Vi rakk ikke å behandle saken i møtet.

### 6. AoB (Any other Business)?
Dersom noen har et tema de ønsker å diskutere har vi satt av ett eget punkt på agendaen for dette.

### 7. Planlegge neste møte
Vi rakk ikke å gå igjennom utestående issues og diskusjoner.. Vi går igjennom dette neste fredag.

* Mange av oss har en del arbeid og saker som må løses fremover, når passer det å
* det er avtalt møte den 18. mars for å diskutere målbilde med tillitsrammeverk

Forslag: vi kan treffes onsdag neste uke (13. mars 14.30-15.30)
