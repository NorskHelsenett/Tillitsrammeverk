# Møtereferat fra møte i feature-team for informasjons- og datamodell i tillitsrammeverket - 23.04.2024

## Til stede

- Richard Husevåg (HSØ)
- Morten Stensøy (Helse Nord IKT)
- Nina Nordberg (NHN)
- Eirik Vegler Broen (Oslo Kommune)
- Kenneth Myhra (NHN)
- Steinar Noem (NHN)
- Ragnhild Varmedal (NHN)
- Rune Andreas Grimstad (NHN)
- Øyvind Bech (NHN)
- Michal Cermak (NHN)
- Simone Vandeberg (NHN)

### Ikke til stede


## Agenda

1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Diskusjon om versjonering av datamodell
3. Nye og utestående Issues og diskusjoner
4. AOB (any other business)?
5. Planlegge neste møte

## Saksgrunnlag og referat

### 1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?

### 2. Diskusjon om versjonering av datamodell

Informasjonsmodellen er versjonert, hvordan versjoneres RAR struktur og Access Tokens/SAML-tokens? Hvordan informeres relevante aktører?

Recap fra diskusjonen i NHN..

Innspll fra featureteam i forrige møte: NHN burde ha en kontaktadresse/kontaktpunkt ved endringer som kan brukes. Utviklerportal burde være "sannheten" - varsling av endringer. Bør henge sammen med hva man gjør for andre tjenester.
Det burde også gå mot en veldig forutsigbar endringssyklus - tydelighet hvor lenge eldre versjoner støttes og når nye versjoner rulles ut og tilgjengeliggjøres.

### 3. Utestående Issues og diskusjoner

Vi går igjennom utestående issues i første milepæl og behandler hvert enkelt issue.
Formålet er ikke nødvendigvis å saksbehandle hver issue, det viktigste er å tildele oppgaven med å løse issuet til noen. Dersom vi kan lukke en issue i møtet er det fint.

#### 3.1 Issue #158: Bruk av dash (-) og underscore (_) i attributtnavn

Dette er en kommentar fra Trond Elde - spec er oppdatert - det er mulig at han ikke har sett i riktig branch?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/158

Forslag akseptert?

#### 3.4 Issue #157: "care-relation" eller "care-relationship"?

Endret også SAML spesifikasjonen.. Men det kan hende jeg var for ivrig..
Er forslaget akseptert?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/157

#### 3.5 Issue #153: ToA: Time of Attestation - Tydeliggjøre beskrivelse av formål og bruk

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/153

Er forslaget akseptert?

#### 3.11 Issue #160: Healthcare-service: Manglende kode for fastlegerelasjon?

Ny issue registrert av Øyvind K:
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/160

La inn nye koder, og har sendt mail til HDIR.
La issue stå åpen til vi får tilbakemelding fra HDIR?

#### 3.2 Issue #117: NHN og sektoren har ulik forståelse av risikobilde i kontekst av informasjon i Access Tokens - krever avklaring

Noen framgang på denne?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/150

#### 3.3 Issue #136: Vurdere om alle felter med potensiell fritekst skal valideres opp mot regulæruttrykk og maksimalt antall tegn av tillitsankeret

Tilbakemelding fra HelseID er at de ikke har prioritert arbeid med attestering av helsepersonellets grunnlag for tilgang til helseopplysninger i inneværende sprint. Flyttes til neste milepæl?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/136


#### 3.6 Issue #137: Vi manger "decision-ref" i JSON eksempler

Noe framgang på denne?
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/137

#### 3.7 Issue #117: Forretningsregler knyttet til attributtet patient: "patient_id"

Noe framgang på denne?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/117

#### 3.8 Issue #108: Forretningsregler knyttet til attributtet "hpr_nr"

Noe framgang på denne?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/108

#### 3.9 Issue #156: ToA kommer ikke med i SAML tokenet

Tilbakemelding fra HelseID er at de ikke har prioritert arbeid med attestering av helsepersonellets grunnlag for tilgang til helseopplysninger i inneværende sprint. Flyttes til neste milepæl?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/156

#### 3.10 Issue #134: Description på decision-ref

Tilbakemelding fra HelseID er at de ikke har prioritert arbeid med attestering av helsepersonellets grunnlag for tilgang til helseopplysninger i inneværende sprint. Flyttes til neste milepæl?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/134

#### 3.11 Merge branch med main?

Flere leverandører implementerer modellen i dag, antagelig lurt å oppdatere main med endringene. Det er forvirrende at det er forskjeller mellom HelseID sine spesifikasjoner og datamodell i tillitsrammeverket.

Er feature-teamet enig?

### 4. AoB (Any other Business)?

Dersom noen har et tema de ønsker å diskutere har vi satt av ett eget punkt på agendaen for dette.

Er det mulig å se for seg å binde en request og en attest sammen.

### 5. Planlegge neste møte
