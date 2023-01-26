# Informasjons- og datamodell

## Innledning 

 

### Relasjon til eHSDI datamodell 

EHDSI har definert en datamodell for utveksling av helseopplysninger på tvers av land i EU. Vi har basert oss på denne modellen når vi har beskrevet informasjons- og datamodellen som skal benyttes ved deling av helseopplysninger innad i Helsenettet. 

### Påkrevd eller valgfri informasjon 

 

## Informasjonsmodell 

| Helsepersonellets identitet | |
| --- | --- | --- |
| Helsepersonellets rolle hos helsevirksomheten | Strukturell rolle og Funksjonell rolle |
| Helsepersonellets spesialitet | |
| Helsepersonellets autorisasjoner | |
| Delegerte rettigheter | |
| Helsevirksomheten hvor helsepersonellet jobber | Helsetjenestetype og Behandlingssted |
| Overordnet formål med behandlingen av helseopplysningene | |
| Pasient | |
 

## Datamodell 

### Prinsipper for datamodellen 

Datamodellen skal legge til rette for at helsevirksomhetene lettere kan samhandle med hverandre ved at man benytter samme språk for å uttrykke informasjonen som beskriver helsepersonellet og konteksten som helsepersonellet befinner seg i når han ber om tilgang til helseopplysningene. 

Datamodellen skal brukes i sikkerhetsbilletter som skal behandles av mange aktører og i mange systemer. Aktørene som mottar og behandler sikkerhetsbillettene må ha svært høy tillit til at informasjonen er trygg. Det skal være usannsynlig at datamodellen kan inneholde data som kan brukes til sikkerhetsangrep via sikkerhetsbilletter. 

Informasjonen i datamodellen skal være sporbar, og må ivareta prinsippet om uavviselighet… mer her om tillitsnivå/sikkerhetsnivå/identiteter osv.. Hvem er den autoritative kilden til informasjonen osv.. 

  
### Attributter i datamodellen 

#### Oversikt over attributter i datamodellen 

| Informasjonskategori | Attributter | Obligatorisk | Informasjonskilde |
| --- | --- | --- | --- |
| Helsepersonell | Fødselsnummer | | eID-ordning |
| | Navn | | Folkeregisteret |
| | HPR-nummer | | HPR-registeret |
| | Autorisasjoner og lisenser | | HPR-registeret |
| Behandlerelasjon | Strukturell rolle | | Konsument |
| | Funksjonell rolle | | Konsument |
| | Spesialitet | | Konsument |
| | Helsevirksomhet | | Konsument |
| | Helsetjenestetype | | Konsument |
| | Behandlingssted | | Konsument |
| | Formålet med behandlingen | | Konsument |
| Pasient | Fødselsnummer/identifikator | | Konsument |

#### Detaljert beskrivelse av attributter i datamodellen 

##### Helsepersonell 

| Attributt | Beskrivelse | Detaljer |
| --- | --- |
| Fødselsnummer | Skatt (Folkeregisteret) |
| Navn | Skatt (Folkeregisteret) |
| HPR-nummer | Helsedirektoratet (HPR) |
|Autorisasjoner og lisenser | Helsedirektoratet (HPR) |
 

##### Behandlerrelasjon 

| Attributt | Beskrivelse | Detaljer |
| --- | --- | --- |
| Strukturell rolle | [ASTM strukturelle roller](https://www.standard.no/no/Nettbutikk/produktkatalogen/Produktpresentasjon/?ProductID=629944) | Med autorisasjon,  uten autorisasjon,  og sekretær/adm personell.. |
| Funksjonell rolle | Styrk-08 | Gyldige verdier(?) |
| Spesialitet | SNOMED: [clinical-speciality 2.16.840.1.113883.3.88.12.80.72](https://fhir-ru.github.io/valueset-c80-practice-codes.html) | |
| Helsevirksomhet | Juridisk person - Org.nr fra virksomhetsregisteret | |
| Helsetjenestetype | [Volven koder](https://volven.no/categoryres.asp?open_f=true&catID=3&subID=8&srcTable=KVELEMENT&open=true&subCat=163) | |
| Behandlingssted | Virksomhet - Org.nr fra virksomhetsregisteret | |
| Formålet (PurposeOfUse) | HL7 koder (link) | |


##### Pasient 

| Attributt | |
| Fødselsnummer | Pasientens fødelsenummer fra folkeregisteret |

 

 

## Normative referanser 

Normative referanser spesifiserer dokumenter som må leses for å forstå eller implementere datamodellen, eller teknologi som må være på plass for å kunne implementere teknologien. 