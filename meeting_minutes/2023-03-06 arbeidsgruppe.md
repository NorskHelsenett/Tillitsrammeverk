# Møte i feature-team for informasjons- og datamodell - 06.03.2023

## Til stede
- Richard Husevåg (HSØ)
- Sverre Martin Jensen (Oslo Kommune)
- Erik Vegler Broen (Oslo Kommune - Origo)
- Simone Vandeberg (NHN)
- Steinar Noem (NHN)

### Ikke til stede
- Morten Stensøy (HNIKT)

## Agenda
0. Gjennomgang av agendaen - akseptert av arbeidsgruppa?
1. Behandling av pågående diskusjonstråder
    - Gjennomgang av uavklarte diskusjonstråder
    - Prioritering av tema
2. Gjennomgang av Issues
    - Prioritering av issues
    - Fordeling av oppgaver
3. Gjennomgang av eventuelle pull-requests
    - PR fra Trond Elde
4. Oppgavefordeling
5. Planlegging av fokus-møter
    - Møteplan for denne uken:
        - Tirsdag
        - Fredag
        - Har vi behov for å diskutere andre tema utenfor Github diskusjonene?
            - Hvordan påvirker EHDSI sin informasjonsmodell våre valg?
            - Hvordan påvirker våre valg en eventuell integrasjon med EHDSI?
6. Kommunikasjon med EPJ leverandører
    - Har vi tilstrekkelig informasjon om hva EPJ leverandørene klarer å implementere til september
    - Har de tatt i bruk, eller er i stand til å ta i bruk nasjonale kodeverk (volven), eller må de utvikle støtte for det vi krever i informasjonsmodellen?
    - Er september realistisk?
7. Annet/eventuelt


## Saksbehandling

### 0. Gjennomgang av agendaen
Agenda OK..

### 1. Behandling av pågående diskusjonstråder
https://github.com/NorskHelsenett/Tillitsrammeverk/discussions

Avsluttede diskusjonstråder:
- [#9 - "strukturell rolle"](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/9)

Prioritering av aktive diskusjonstråder:
1. [#6 - HP fødselsnummer og navn](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/6)
    - Loggen bør ha navnet som gjaldt på tidspunktet ved forespørsel. 
    - Kan konkludere med at begge deler skal med.. Flytt over som issue.
2. [#24 - innspill til informasjonsmodell](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/24)
    - Denne kan tas som en issue:
        - Hvilke attributter skal med - hvilke er optional
    - Lukk diskusjonstråden, flytt info over til andre diskusjonstråder
    - Hvor pasienten befinner seg? Bør inn i informasjonsmodellen, konsumenten vet dette.. Kan ikke være obligatorisk.
3. [#22 - Standard struktur for attributter](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/22)
4. [#23 - Organisasjon som objekt](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/23)
    - bør dette reflekteres i informasjonsmodellen
    - kan relateres både til helsepersonellet og pasienten
5. [#12 - Attributter for virksomhet](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/12)
- Hvordan håndterer vi Oslo kommune, med etatene sine?
6. [#11 - "Purpose of Use"](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/11)
    - OK - hvis man abstraherer det til et høyt nivå
    - Vi må skille dette fra helsetjenestetype (med IPLOS)
7. [#3 - HPR-nummer](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/3)
8. [#7 - Er HPR valgfritt eller påkrevd](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/7)
9. [#8 - inkludere autorisasjoner og lisenser i tokens](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/8)
10. [#4 - "funksjonell rolle"](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/4)
    - Avklare hva dette er.. funksjonell rolle vs ansattrolle
    - Oslo klarer ikke å fylle ut denne er det mulig å levere noe på denne i september?
    - Dersom vi kan være enige om at den ikke er obligatorisk kan Oslo leve med at den tas med videre
11. [#10 - "location"](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/10)
12. [#28 - fastlegerelasjon](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/28)

Må vi opprette noen nye diskusjonstråder?
* Mangler - vi mangler diskusjon om pasientens fødselsnummer
* Helsetjenestetype og IPLOS koder

Behandlingssted er avklart


### 2. Gjennomgang av issues
https://github.com/NorskHelsenett/Tillitsrammeverk/issues

#### Åpne issues
1. [#21](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/21)
2. [#20](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/20)
3. [#16](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/16)

#### Nye issues
* [#24 - innspill til informasjonsmodell](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions/24)
    - Denne kan tas som en issue:
        - Hvilke attributter skal med - hvilke er optional
    - Lukk diskusjonstråden, flytt info over til andre diskusjonstråder
        - Hva er "funksjonell rolle?" #4


#### Lukkede issues
1. [#34](https://github.com/NorskHelsenett/Tillitsrammeverk/issues/34)

### 3. Gjennomgang av PR
https://github.com/NorskHelsenett/Tillitsrammeverk/pulls

1. [PR #35](https://github.com/NorskHelsenett/Tillitsrammeverk/pull/35)

Vi gir følgende tilbakemelding på PR:
- opprett diskusjonstråder eller issues i stedet for kommentarer
- fjern kommentarer fra PR og be om review av tekstlige endringer av dokumentet

### 4. Oppgavefordeling
Forsatt fokus på diskusjonene.

Vi må jobbe videre med diskusjoner og med å lukke issues..
- Erik: jobber med issue som han har åpent og jobber med å omstrukturere den ene diskusjonstråden

Hvem gjør hva?

### 5. Planlegging av fokus-møter
Vi har planlagt følgende møter:
- 07.03.2023: HPR og lokal identifikator, IPLOS
- 10.03.2023: Location, Purpose of Use

Må temaene justeres etter gjennomgang av diskusjoner og issues?
- bør klare å ta inn litt mer.. Pasientens identifikator etc.


Bør vi planlegge flere fokuserte møter for denne eller neste uke?

### 6 Kommunikasjon med EPJ leverandører
Har vi tilstrekkelig informasjon om hva EPJ leverandørene klarer å implementere til september?

Har de tatt i bruk, eller er i stand til å ta i bruk nasjonale kodeverk (volven), eller må de utvikle støtte for det vi krever i informasjonsmodellen?

Er målet om september realistisk?

### 7. Annet/eventuelt?
#### Tirsdagsmøter
Gruppa har et ønske om at de tekniske møtene på tirsdager fokuserer på arbeidet mot mål i september:
- NHN fokuserer på risikovurderinger og sikkerhetsvurderinger i tirsdagsmøtene
- Løsningsmønster for Gerica. Sekvensdiagram?
- Hvordan kan man implementere uten proxy (bruk av HelseID og KJ)
- RAR vs assertion framework (authorize endpunkt vs token endepunkt) : Tydelighet ovenfor leverandørene

#### EHDS
EHDSI/FHIR/HL7 - vi bør kommunisere at vi i norge har jobbet mye med temaet. Kanskje er det verdifullt for EHDSI å få input fra vårt arbeid.

Det kan virke som om de har et mer teknisk fokusert tilnærming i motsetning til vår mer funksjonelle tilnærming.

NHN tar forslaget inn i NHN sitt myhealth@eu team.

