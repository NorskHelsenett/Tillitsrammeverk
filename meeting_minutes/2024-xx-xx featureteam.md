# Møtereferat fra møte i feature-team for informasjons- og datamodell i tillitsrammeverket - 13.03.2024

## Til stede
- Richard Husevåg (HSØ)
- Eirik Vegler Broen (Oslo Kommune)
- Ronny Heitmann Andersen (Helse Vest IKT)
- Morten Stensøy (Helse Nord IKT)
- Nina Nordberg (NHN)
- Simone Vandeberg (NHN)
- Steinar Noem (NHN)
- Kenneth Myhra (NHN)

### Ikke til stede
- Sverre Martin Jensen (Oslo Kommune)
- Ragnhild Varmedal (NHN)
- Rune Andreas Grimstad (NHN)
- Øyvind Bech (NHN)

## Agenda
1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
2. Spørsmål fra leverandør
3. Nye og utestående Issues og diskusjoner
4. AOB (any other business)?
5. Planlegge neste møte

## Saksgrunnlag og referat

### 1. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
OK - agenda akseptert

### 2. Spørsmål fra leverandør
Vi har fått tilbakemelding fra en leverandør:

"Utvikling hos oss har startet å se på dette.

I denne sammenhengen så har vi ett spørsmål angående «"purpose-of-use-details": type tjeneste som pasienten skal motta hos virksomheten». 
Mener denne tidligere ikke var påkrevd.

Er dette fremdeles tilfelle, og vi kan forstå «Ja, hvis forekommer» slik?
I bildet under så er ordlyden slik den foreligger nå.

Om den nå er påkrevd, så lurer vi på hva som forventes å avlevere av kode og kodeverk her for hhv:
Fastlegekontor (unntatt hvor man er fastlege for pas.)
Avtalspesialister
Kommunale tjenester (utenom sykehjemstjenester)
- Helsestasjon
- Fengsel
- Smittevern
- Legevakt
- Overgrepsmottak
- ØHD
- etc" 

Bør vi endre på teksten "Ja, hvis forekommer" slik at den er lettere å forstå?

Eirik: 
- Aksjon: legg til Issue om å endre tekst til "Nei, ikke påkrevd - dersom det ikke er relevant"
- åpner vi for å angi kodeverk? Hvilke følger får dette for validering
- Alle RHF bruker DIPS kodeverk - med det ligger ikke på volven..
- Det kan være fornuftig å la konsumenten definere 

Morten: 
- Forventningen er at man må ha enten healthcare service eller purpose_of_use_details
- Det bør spesifiseres som et krav:
    * Aksjon: legg inn issue i Github - spesifiser en forretningsregel rundt dette

Richard:
- Vi må være mer spesifikk i eksemplene:
* Dersom organisasjonen har flere nivå, og mer enn ett undernivå må denne spesifiseres
* Hvis ikke trenger man ikke... 

Eirik:
* kunne vi innført en overordnet oppsummering/forklaring som blir lenket til i påkrevd/ikke påkrevd i informasjon: aksjon - oppdater informasjonsmodell med peker til krav knyttet til påkrevd/ikke påkrevd

Aksjon: 
* opprett issue: Forbedre forretningsregler slik at det blir mer tydelig


Legge denne inn som issue?

### 3. Utestående Issues og diskusjoner
Vi går igjennom utestående issues og behandler hvert enket issue.
Formålet er ikke nødvendigvis å saksbehandle hver issue, det viktigste er å tildele oppgaven med å løse issuet til noen.
Dersom vi kan lukke en issue i møtet er det selvfølgelig fint. 

#### 3.1 Issue #146: Manglende kodeverk for "purpose_of_use_details" for spesialist
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/146

#### 3.2 Issue #147: Angivelse av assigner og authority i HelseID
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/147

#### 3.3 Issue #148: Endre angivelse av assigner og authority i forespørsel til HelseID i datamodellen
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/148

#### 3.4 Issue #149: Standardisering av carerelation (fhir audit event)
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/149

#### 3.5 Issue #150: Oppfølging av innspill om at ulik forståelse av risikobilde
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/150

#### 3.6 Issue #151: Avklaring - hvor langt strekker NHN sitt ansvar seg for å validere innhold i Tokens
https://github.com/NorskHelsenett/Tillitsrammeverk/issues/151

Eirik: 
* Vi må lage et underlag som beskriver hvordan sektoren mener HelseID bør fungere..
* Bekymringene kan være knyttet til strategien til NHN (f.eks. public cloud)

Richard: 
* Risikoene inngår i en ende til ende samhandling mellom virksomhetene
* Risikoen må sees i sammenheng med den totale risikoen, hvor HelseID er et risikoreduserende tiltak. Vi er mest opptatt av payloaden.

Morten:
* Vi har noe underlag fra før - vi kan få fram at dette er en måte å løse det på
* Vi må beskrive hva den andre siden av risikoen er.. Hva skjer hvis attesten ikke overføres? Hvilken nytte gir dette?

Forslag: Sektoren (foretakene + oslo) beskriver underlaget, kan møtes med NHN hvor vi samler det i et felles underlag - og løfter det til OSG
Eirik: fornuftig å få med flere aktører

Aksjon: opprett to issues for dette

### 4. AoB (Any other Business)?
Dersom noen har et tema de ønsker å diskutere har vi satt av ett eget punkt på agendaen for dette.

Kommentar fra Morten og Richard:
* Ang. Authorization: dersom attributtet ikke fylles ut har vi ingen indikasjon om rollen
HSØ har landet på tre roller

Aksjon: Morten lager issue på dette

Direktoratet har begynt å bruke finnkode i stedet for volven.. 
Vi undersøker med direktoratet om hvorvidt vi bør peke dit i stedet for volven.

"ToA": kommer ikke med i SAML tokenet - steinar oppretter issue og følger opp

### 5. Planlegge neste møte
Ehelsekonferanse neste uke, hva kan være et fast tidspunkt fremover?
Richard: 14-16 er gode tidspunkt

Foreslått tidspunkt: 14-15 på tirsdager (fra 2. april fram til sommerferie)
