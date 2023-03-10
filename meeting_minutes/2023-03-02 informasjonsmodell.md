# Møte i feature-team for informasjons- og datamodell - 02.03.2023

## Til stede
- Richard Husevåg (HSØ)
- Morten Stensøy (HNIKT)
- Sverre Martin Jensen (Oslo Kommune)
- Erik Vegler Broen (Oslo Kommune - Origo)
- Simone Vandeberg (NHN)
- Steinar Noem (NHN)

### Observatører
- Ragnhild Varmedal (Observatør - NHN)

## Agenda
1. Introduksjon, forslag til prosess
2. Gjennomgang av diskusjonstråder - kan noen overføres til issues?
3. Behandling av utestående issues
4. Oppgavefordeling
5. Trenger vi flere deltagere i feature-teamet (redaksjonsteamet for spesifikasjonene)
6. Andre Tema/utestående saker?
7. Møteplanlegging

## Referat
### Målet med dagens møte
Gruppa er enige om at vi raskt må komme til enighet om informasjonsmodellen. Målet er å ferdigstille spesifikasjonen innen mars 2023.

Målet med dagens møte er:
- å identifisere hvilke informasjonselementer vi kan "spikre"
- å identifisere hvilke informasjonselementer vi må diskutere videre
- å identifisere hvilke informasjonselementer vi må utsette til etter leveransen i september 2023

### Prosess
- NHN prioriterer issues og kommuniserer dette på Github
- Teamet jobber videre med diskusjonstråder og bidrar ved å plukke issues

### Beslutningslogg

Tentativ dato for siste innspill fra arbeidsgruppa (de som deltar på github) er 17.03.​

HN & HSØ som kilde kan motta  lokale kodesverk for sept leveransen.​

For koder som ikke er basert på nasjonale kodesverk må NHN må som minimum gjennomgå sanitization

#### Det ble besluttet at følgende informasjonselementer skal være med i informasjonsmodellen:​
Vi konverterer følgende diskusjonstrådene til issue:​
- Helsepersonellets identitet​
- Juridisk enhet​
- Behandlingssted​

#### Det ble besluttet av vi trenger flere diskusjoner for å lande følgende informasjonselementer:​
- Informasjon fra HPR​
- Helsetjenestetype​
- IPLOS​ tjenestetype
- Formattering av attributter​
- "location"/detaljert org.info​
- Purpose of use​

#### Det ble besluttet at vi fjerner følgende informasjonselement fra informasjonsmodellen:​
- Strukturell rolle (fra EHDSI)​

#### Det ble besluttet å opprette en ny diskusjonstråd for tema vedrørende følgende informasjonselementer:​
- Lokal identitet for helsepersonell​
- Strukturell rolle fra EHDSI​

#### NHN må diskutere og vurdere konsekvensen av pasientens identitet i Access Tokens (DPIA/risikovurdering/alternative løsninger) ​
- Informasjonsmodellen må reflektere at dette er et risikoelement

### Møteplan
Teamet har planlagt tre arbeidsmøter uke 10 (6-10 mars)
- 06.03.2023 - Issues og diskusjoner
- 07.03.2023 - Diskusjon om HPR registeret og lokal identifikator for helsepersonell
- 10.03.2023 - Purpose Of Use og helsetjenestetyper i IPLOS
