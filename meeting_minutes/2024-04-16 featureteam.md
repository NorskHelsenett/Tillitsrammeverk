# Møtereferat fra møte i feature-team for informasjons- og datamodell i tillitsrammeverket - 16.04.2024

## Til stede

- Richard Husevåg (HSØ)
- Morten Stensøy (Helse Nord IKT)
- Nina Nordberg (NHN)
- Eirik Vegler Broen (Oslo Kommune)
- Kenneth Myhra (NHN)
- Steinar Noem (NHN)
- Ragnhild Varmedal (NHN)

### Ikke til stede

- Rune Andreas Grimstad (NHN)
- Øyvind Bech (NHN)
- Michal Cermak (NHN)
- Simone Vandeberg (NHN)

## Agenda

1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Tilbakemeldinger på notater
3. Nye og utestående Issues og diskusjoner (10 stk)
4. Hvordan skal vi håndtere endringer av spesifikasjonene under utprøving?
5. AOB (any other business)?
6. Planlegge neste møte

## Saksgrunnlag og referat

### 1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?

### 2. Tilbakemeldinger på notatet om tillitsrammeverk

Har feature teamet tilbakemeldinger på notatet?
Vi ønsker oss skriftlig tilbakemeldinger, og en eventuell gjennomgang i møte.

Fra feature-teamet:

- Generell kommentar: tillitsrammeverket er også til bruk ved deling av data direkte mellom virksomhetene i sektoren, ikke bare sentralt nasjonalt koblingspunkt eller ved samling/lagring
- Vi kommer en skriftlig tilbakemelding, men må komme etter annet arbeid.

### 3. Utestående Issues og diskusjoner

Vi går igjennom utestående issues i første milepæl og behandler hvert enkelt issue.
Formålet er ikke nødvendigvis å saksbehandle hver issue, det viktigste er å tildele oppgaven med å løse issuet til noen. Dersom vi kan lukke en issue i møtet er det fint.

#### 3.1 Issue #158: Bruk av dash (-) og underscore (_) i attributtnavn

Dette er en kommentar fra Trond Elde - spec er oppdatert - det er mulig at han ikke har sett i riktig branch?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/158

Steinar tar en sveip igjennom spec først og svarer ut Trond og lukker issuet?

#### 3.2 Issue #117: NHN og sektoren har ulik forståelse av risikobilde i kontekst av informasjon i Access Tokens - krever avklaring

Noen framgang på denne?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/150

#### 3.3 Issue #136: Vurdere om alle felter med potensiell fritekst skal valideres opp mot regulæruttrykk og maksimalt antall tegn av tillitsankeret

Tilbakemelding fra HelseID er at de ikke har prioritert arbeid med attestering av helsepersonellets grunnlag for tilgang til helseopplysninger i inneværende sprint. Flyttes til neste milepæl?

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/136

#### 3.4 Issue #157: "care-relation" eller "care-relationship"?

Har vi landet på ett av disse begrepene?
Steinar oppdaterer spesifikasjonen når vi blir enige.

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/157

#### 3.5 Issue #153: ToA: Time of Attestation - Tydeliggjøre beskrivelse av formål og bruk

Steinar skriver et forslag, og oppdaterer spesifikasjonen.
Hva skal den brukes til, og hvordan skal den brukes?
Utdyp hva vi mener mener med attestering i denne konteksten.

https://github.com/NorskHelsenett/Tillitsrammeverk/issues/153

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

#### 3.11 Issue #160: Healthcare-service: Manglende kode for fastlegerelasjon?

Ny issue registrert av Øyvind K:
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/160

KX17 er misvisende for fastlegerelasjon, finnes det andre alternativ?
Noen i teamet som kan ta en titt på denne issuen? Noe HDIR kan hjelpe oss med?

Aksjon: legg til at 7750 også er et kodeverk som kan benyttes. Legg til eksempel..

* https://beta.finnkode.ehelse.no/adm/collections/8254?q=8254
* https://beta.finnkode.ehelse.no/adm/collections/7750?q=fastlege

Ta kontakt med HDIR for å få en avklaring - hvilke koder passer best til vårt formål?

### 4. Hvordan skal vi håndtere endringer av spesifikasjonene under utprøving?

Informasjonsmodellen er versjonert, hvordan versjoneres RAR struktur og Access Tokens/SAML-tokens?
Hvordan informeres relevante aktører?

Tilbakemelding fra teamet: NHN burde ha en kontaktadresse/kontaktpunkt ved endringer som kan brukes. Utviklerportal burde være "sannheten" - varsling av endringer. Bør henge sammen med hva man gjør for andre tjenester.
Det burde også gå mot en veldig forutsigbar endringssyklus - tydelighet hvor lenge eldre versjoner støttes og når nye versjoner rulles ut og tilgjengeliggjøres.

### 5. AoB (Any other Business)?

Dersom noen har et tema de ønsker å diskutere har vi satt av ett eget punkt på agendaen for dette.

Er det mulig å se for seg å binde en request og en attest sammen.

### 6. Planlegge neste møte
