# Møtereferat fra møte i feature-team for informasjons- og datamodell i tillitsrammeverket - 27.10.2023

## Til stede
- Richard Husevåg (HSØ)
- Eirik Vegler Broen (Oslo Kommune - Origo)
- Frank Furnes (Helse Vest IKT)
- Morten Stensøy (Helse Nord IKT)
- Kristin Rønneberg (NHN)
- Simone Vandeberg (NHN)
- Steinar Noem (NHN)
- Ragnhild Varmedal (NHN)
- Rune Andreas Grimstad (NHN)

### Ikke til stede
- Sverre Martin Jensen (Oslo Kommune)
- Øyvind Kvennås (NHN)
- Kristin Lyng (NHN)
- Øyvind Bech (NHN)
- Nina Nordberg (NHN)
- Michal Cermak (NHN)

## Agenda
1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Gjennomgang av utkast til forretningsregler
3. Hvordan tar vi forretningsregler videre?
4. Utestående Issues
5. Arbeids- og møteplanlegging for neste uke

## Saksbehandling

### 1. Gjennomgang av agendaen
OK

### 2. Gjennomgang av utkast til forretningsregler
- Er det formattert på formålstjenlig måte?
- Gir dokumentet verdi?

Richard: synes det gir mening.. Noe av strukturen må antagelig justeres - ikke alltid at man f.eks. må ha binding til ett attributt. Det tar vi underveis.

Eirik: vi må skrive i forretningsreglene at ID på pasient henger sammen med pasienten. Altså at det ikke blir en blanding mellom pasientid og attest. Dette kan f.eks. løses med en nøkkel. Vi må sikre oss at dette ikke blir blandet sammen. Attesten kan gjenbrukes mange ganger for samme pasient - altså at den følger pasientsesjonen.



### 3. Hvordan tar vi forretningsregler videre?
- Tas inn i løsningsbeskrivelser?

- Hva er Definition of Done? 
Eirik: Forslag - "Kan jeg som epj leverandør, bruke bare denne dokumentasjonen til å lage det som behøves?"

- Spesifikasjonsarbeidet timeboxes til 3 uker.

- Forslag til framdrift: Team tillit oppretter issues for hvert informasjonselement, og tildeler arbeidsoppgaver til enkeltpersoner.

Eirik oppretter en issue hvor formulerer problemstillingen.


### 4. Utestående Issues
#### [Issue 79](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/79)
- Sektoren har gitt tilbakemelding, nhn må ta stilling til innspillene.
- Er ikke en del av informasjonsmodell/attesten
- lar issuet stå åpent inntil vi hører fra Nina

#### [Issue 93](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/93)
- lukkes

#### [Issue 94](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/94) 
- Lukkes

#### [Issue 98](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/98)
- Overføres til N

#### [Issue 100](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/100)
- Lukkes, men beholder diskusjonen.. 

#### [Issue 102](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/102)
- lukkes

#### [Issue 104](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/104)
- NHN viderebehandler dette issuet med det funksjonelle knyttet til PoU - prøv å inkluder diskusjonen videre
- Anbefaling fra Richard er å inkludere ISO kodeverk i tillegg til HL7 (tas opp med NHN-kjernejournal)
Splittes opp i to issues.. ISO ogspsifikasjon på SAML

#### [Issue 105](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/105)
- Holdes åpen til neste uke 
forslag: forretningsregel for angivelse av attributt

### 5. Arbeids- og møteplanlegging for neste uke
- Fordele forretningsregler ut fra informasjonselementer i spesifikasjonen?
- NHN oppretter Issues, teamet "plukker" sine oppgaver selv

De som jobber med reglene tar initiativ til å samles for å diskutere.
NHN innkaller til 2 timers møte fredag 2. november (ikke 11-13)
