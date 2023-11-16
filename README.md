# Tillitsrammeverk
PJD med relevante spesifikasjoner er nå i utprøving.
Spesifikasjonene for PJD understøtter krav i tillitsrammeverket for PJD og er klare til å prøves ut.

NHN vil i samarbeid med helsevirksomhetene og EPJ leverandørene som deltar i utprøvingen forbedre og oppdatere spesifikasjonene underveis i utprøvingsperioden basert på erfaringer.

## Samarbeid om spesifikasjoner
Vi har valgt å bruke versjonskontrollverktøyet Github til å skrive dokumentasjon og spesifikasjoner av flere årsaker:
- Det lar oss håndtere versjoner på en god måte
- Det gir oss god kontroll over endringer og historikk
- Det gjør samarbeid på tvers enklere

### Spesifikasjoner
* [Informasjonsmodell og datamodell for attestering av helsepersonells grunnlag for tilgang til helseopplysninger](/specs/informasjons_og_datamodell.md).
* [Forretningsregler for bruk av informasjonsmodell for attestering av helsepersonellets grunnlag for tilgang til helseopplysninger](/specs/forretningsregler_for_bruk_av_attestering.md)

## Prosess
Utviklingen av spesifikasjonene vil foregå over flere iterasjoner, hvor hver iterasjon fører til en ny versjon av spesifikasjonen. NHN skal sørge for framdrift og vil fungere som reviewer av pull-requests, sørger for framdrift i viktige diskusjoner og vil håndtere eventuelle tilbakemeldinger via issues.

Hvis det ikke oppstår nye diskusjoner eller issues som peker på feil, eller dersom endringene kun består av språklige endringer skal det gjennomføres en avstemning om hvorvidt spesifikasjonen skal publiseres som versjon 1.0.

### Diskusjoner
Spesifikasjonene vil bli basert på diskusjoner og innspill gjort i Github. Diskusjoner og innspill i andre kanaler vil ikke bli behandlet. Derfor er det viktig at diskusjoner som foregår utenfor dette repositoriet blir dokumentert skriftlig, enten som diskusjon, eller som issues eller pull-requests.

### Issues
Når du oppdager feil eller mangler i spesifikasjonen må du opprette en issue i Github. Dersom det er behov for å diskutere eller på annen måte behandle en registrert issue skal dette gjøres skriftlig ved å legge inn kommentarer.
Dersom en issue fører til en endring i spesifikasjonen skal denne endringen gjøres via en pull-request, eller som en merge mot den branchen man jobber mot.

### Pull-request
Dersom du ønsker å gjøre endringer direkte i spesifikasjonen skal du benytte [pull-requests i Github](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests). 
Hvis en pull-request er knyttet til en issue ønsker vi at du lenker pull-requesten til issuet.

Norsk Helsenett vil fungere som reviewer av pull-requests, og vil gjøre en kvalitetskontroll og håndtere eventuelle diskusjoner knyttet til innsjekkingen.

### Behov for møter og avklaringer
Vi anser det som sannsynlig at det vil bli behov for å gjennomføre møter, men legger ikke opp til en fast møteserie med mindre det viser seg å bli et  behov. Dersom det viser seg at bidragsyterne til spesifikasjonene har behov for å gjennomføre møter vil disse møtene fasiliteres av NHN og avtales fortløpende.

### Versjonering
Spesifikasjonen vil versjoneres etter hver iterasjon, hvor versjonen indikeres av et suffix, f.eks. "-1", "-2", osv.

Når spesifikasjonen ansees som ferdig skal den publiseres som versjon 1.0.



## Innføring til bruk av Github
### Hvordan bruke Github
Github har god dokumentasjon som beskriver arbeidsflyten.
Les [brukerveiledningen på Github](https://docs.github.com/en/get-started/quickstart/github-flow) for å få en forståelse for de grunnleggende prinsippene.

### Skriv dokumenter i Markdown (.md filer)
Markdown er et språk som kan brukes for å generere html. Det er enkelt i bruk, og krever ingen spesiell programvare.
 
[Innføring til markdown på Github](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

### Verktøy for Markdown (.md filer)
Vi anbefaler to verktøy for å skrive .md filer:
- Github: Github har innebygget teksteditor for Markdown. Dette er den enkleste måten å gjøre endringer, og krever ingen installert programvare på din maskin.
- [Visual Studio Code](https://code.visualstudio.com/): Er et utviklingsverktøy for å skrive programmeringskode. Ved å bruke extensions kan blant annet få forhåndsvisning av dokumentet du skriver.

Det finnes mange andre teksteditorer som man også tilbyr forhåndsvisning av HTML koden som blir generert. [Ta en titt på nettet for å se om du finner noen som passer for deg](https://duckduckgo.com/?q=markdown+editor&t=h_&ia=web).

### Diskuter med andre som bidrar
Vi har valgt å bruke [diskusjoner på Github](https://github.com/NorskHelsenett/Tillitsrammeverk/discussions) for dialog mellom de som bidrar. På den måten er alle diskusjoner synlige for de som deltar, samtidig som vi ivaretar historikken på en god måte.

### Diagram i markdown
Github har støtte for å lage diagram i markdown dokumenter ved bruk av Mermaid.
Se [her for en introduksjon](https://mermaid.js.org/intro/).
