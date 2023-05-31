# Informasjons- og datamodell for dokumentdeling i kjernejournal

## Sammendrag
Denne spesifikasjonen definerer en informasjons- og datamodell som skal benyttes for å uttrykke informasjon om helsepersonellets grunnlag for tilgang til pasientens helseopplysninger ved dokumentdeling i Kjernejournal.
Modellen skal benyttes ved utstedelse av sikkerhetsbilletter i ulikt format som f.eks. SAML Assertions og JWT.
Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i tillitsrammeverk for deling av helseopplysninger i helse og omsorgssektoren.

Spesifikasjonen skal versjoneres for å støtte endringer over tid.

## Dokumentets status

| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| -0 | Utkast | 24.05.2023 |
| -1 | Input fra team dokumentdeling | 25.05.2023 |


Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til dokumentdeling i kjernejournal.

## Innholdsfortegnelse
1. Innledning 
2. Ordliste
3. Bakgrunn for spesifikasjonen
4. Spesifikasjon av datamodell
5. JSON profil for datamodell


## 1. Innledning 
For å gi riktig helsehjelp til riktig tid må helsepersonell ha tilgang til relevante helseopplysninger som ligger lagret hos andre virksomheter enn den virksomheten hvor de yter helsehjelp. Lovverket i Norge sier at helsevirksomheter er pliktig til å dele helseopplysninger med alt helsepersonell så fremt de har et tjenstlig behov og at opplysningene er relevante og nødvendige i helsepersonellets behandling av pasienten (hpl §45).

Kravene knyttet til tjenstlig behov og opplysningenes relvans og nødvendighet i behandlingen av pasienten medfører at virksomhetene som har dataansvar for helseopplysningene må styre tilgang på en tilfredsstillende måte.

I dokumentdeling gjennom kjernejournal-portal legges det opp til en oppgavefordeling knyttet til tilgangsstyring, slik at den konsumerende virksomheten utfører tilgangsstyring til helseopplysninger på vegne av dokumentkilden. Til tross for at den konsumerende virksomheten er forpliktet til å kontrollere at deres helsepersonell har en gyldig grunn for tilgang til helseopplysninger har virksomheten som deler opplysninger likevel behov for å motta informasjon som beskriver grunnlaget for tilgangen. Informasjonen som beskriver grunnlaget for delingen vil benyttes til flere formål:

1. å utføre ytterligere tilgangskontroll
2. lovpålagt logging av tilgangen for å avdekke urettmessig tilegnelse av helseopplysninger
3. å støtte opp under innbyggers rettigheter

På grunn av at tilgangsstyring er implementert på forskjellig måte i forskjellige systemer og virksomheter er det nødvendig at konsumentene og dokumentkildene samler seg om et felles språk for å uttrykke grunnlaget for tilgang slik at aktørene kan forstå hverandre. Et felles språk vil også bidra til å kommunisere på en konsistent måte til innbygger.

Denne spesifikasjonen definerer et felles språk som skal benyttes til å uttrykke helsepersonells grunnlag for tilgang til helseopplysninger ved deling av helseopplysninger via tekniske grensesnitt. Spesifikasjonen definerer en informasjonsmodell, datamodell og kodeverk som skal implementeres i programvare som benyttes av helsepersonell når de yter helsehjelp til sin pasient.

## 2. Ordliste
 
|  Begrep | Definisjon  |
| --- | --- |
|  |  |

## 3. Bakgrunn for spesifikasjonen
Grunnlaget som presenteres i denne spesifikasjonen er samling av identifiserte attributter som anses som nødvendige for å kunne tilby dokumentdelings tjenesten til helsepersonell i Norge. Opprinnelig målet med spesifikasjonen var å tilnærme seg den europeiske spesifikasjonen av datamodellen som benyttes for utveskling av helseopplysninger på tvers av landesgrenser i Europa (ref. EHDS). Representanter fra norsk helsesektor som deltok i spesifiseringsrunde vurderte at norsk behov er litt annerledes enn den europeiske og at det er andre attributter som skal utveskles. Bakgrunnen for datamodellen skal være å tilfredstille nødvendig behov for identifisering av helsepersonell og virksomheten som denne personen representerer, samt med å overføre nødvendig informasjon om grunnlaget for tilgjengliggjøring av pasientens helseopplysnigner. Primær formål med attributtene i datamodellen er å tilfredstille de juridiske krav som stilles til utveksling av helseopplysnigner.

## 4. Spesifikasjon
Spesifikasjonen inneholder en informasjonsmodell som beskriver hvilken informasjon som skal overføres mellom aktørene, hva denne informasjonen beskriver, og hvorfor den skal overføres.

Spesifikasjonen beskriver også hvilke konkrete attributter som skal brukes for å beskrive informasjonsmodellen i form av en datamodell. Datamodellen angir hvilke kodeverk og verdier som er gyldige for de ulike attributtene.

Spesifikasjonen skal benyttes av programvare- og systemleverandører ved implementasjon av programvare som skal brukes ved deling av helseopplysninger på tvers av virksomheter i sektoren. Datamodellen vil også implementeres i relevante nasjonale ehelseløsninger og tillitstjenester.

### 4.1 Informasjonsmodell
I dokumentdeling består helsepersonellets digitale identitet av informasjon som beskriver hvorfor helsepersonellet har behov for tilgang til pasientens helseopplysninger. Disse informasjonselementene forteller noe om helsepersonellets behandlerrelasjon til pasienten.
Modellen skal, i utgangspunktet, være felles for JWT og XUA.

Informasjonen som skal overføres fra konsument til datakilde beskriver behandlerrelasjonen som helsepersonellet har til sin pasient.

_**TODO: peke til informasjonsmodell i tillitsrammeverket - og beskriv kort hva den inneholder**_

1. Avdeling eller organisasjonsenhet hvor helsepersonellet yter helsehjelp til sin pasient
2. Typen helsetjeneste som leveres ved virksomheten hvor helsepersonellet behandler sin pasient
3. Helsepersonellets formål med helseopplysningene


Norsk lov og ytterligere konkretisering i Norm for informasjonssikkerhet sier at helsepersonell bare skal gis tilgang til helseopplysninger dersom det foreligger et tjenstlig behov og at opplysningene er relevant og nødvendig i behandlingen av pasienten. Det er helsepersonellet og konsumentens ansvar å sørge for at tilgangen til helseopplysningene er i henhold til loven, men den utleverende part har likevel behov for overført informasjon som beskriver bakgrunnen for forespørselen om helseopplysninger for å tilfredsstille lovkrav knyttet til dokumentasjon og å utføre tilgangskontroll. 

- Databehandler (juridisk enhet)
- Behandlingssted


# Datamodell for detaljert autorisasjonsinformasjon

Modellen som er presentert her må ses på som en "alfa-versjon"/"0.1-versjon" av datamodellen. Den er ikke nødvendigvis testet i praksis og læring må til for å se verdien av informasjonen i verdikjeden. Norsk helsenett, spesielt teamet ved dokumentdelingsproduktet kan IKKE stille seg bak behovet for alle disse informasjons elementer (ref. kommentar under tabellen).

| Attributt | Beskrivelse | Informasjonskilde | Påkrevd | Status | Formål |
| --- | --- | --- | --- | --- | --- |
| "department" | Avdeling/org.enhet hvor helsepersonellet yter helsehjelp | Konsumentens EPJ | **Nei** |<span style="color: green; font-weight: bold;">Inkluderes</span> | Informasjon til pasienten |
| "healthcare_service" | Helsetjenestetyper som leveres ved virksomheten | Konsumentens EPJ | **Ja** | <span style="color: green; font-weight: bold;">Inkluderes</span> | Tilgangsstyring og informasjon til pasienten? |
| "purpose_of_use" | Helsepersonellets formål med helseopplysningene (til hva de skal brukes) | Kjernejournal, eller<br>Konsumentens EPJ | **Ja** | <span style="color: green; font-weight: bold;">Inkluderes</span> | Tilgangsstyring |
| "purpose_of_use_details" | Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes) | Konsumentens EPJ | **Nei** | <span style="color: green; font-weight: bold;">Inkluderes</span> | Loggkontroll |
| "tracing_ref" | Referanse til opprinnelsen av forespørsel | Konsumentens EPJ | **Nei** | <span style="color: green; font-weight: bold;">Inkluderes</span> | Loggkontroll |



#### 4.2.6 Kategori: Behandlerrelasjon
Helsepersonellets behandlerrelasjon til pasienten angis av hvilken virksomheten han yter helsehjelp for, ved hvilket behandlingssted helsehjelpen ytes, helsetjenestetype og en beskrivelse av formålet med behandlingen av helseopplysningene.


##### "department": Avdeling/organisasjonsenhet
Attributtet "department" angir avdelingen hvor helsepersonellet yter eller administrerer helsehjelp.
Konsumenten må vurdere hvilket nivå som vil være tilstrekkelig for å beskrive tilhørigheten på et godt nok nivå.

| :warning:                | Intern kommentar fra team dok.deling | Modenhet |
|--------------------------|:------------------------|-----|
| "department"             | Dette elementet har ingen verdi for tilgangsstyring til tjenesten dok.deling hos Norsk helsenett. Dette elementet ønskes av representanter fra sektoren og derfor kan ikke Norsk helsenett stå ansvarlig for evt. mangler ute i sektoren. Må ses som en informasjonselement som evt. blir tatt ut i fremtiden | Lav |
|                          | Det kan være problematisk med å referere til RESH-registeret siden den ikke er alltid oppdatert i tråd med siste organisasjonsendringer. I praksis vil dette medføre at det kan være avvikk mellom det som er sannhet og det som står registert i systemer. Det kan antas at dette vil medføre behov for å overføre fritekst, noe som ikke er ønskelig av sikkerhets hensyn ||

Attributtet er ikke relevant for alle typer virksomheter. Det er derfor ikke obligatorisk å legge det ved. 

I kommunal sektor vil det være relevant å bruke attributtet "department" for å angi aktuell skole i skolehelsetjenestenm mens det i sykehjemskontekst ikke er relevant å angi avdeling.

Dersom konsumenten har lokale identifikatorer som brukes for å beskrive avdeling/organisasjonsenhet må de fremdeles angi system og assigner. I slike tilfeller vil den juridiske enheten være "assigner".

Attributtet blir benyttet ved loggkontroll, samt for å gi informasjon om tilgangen til helseopplysninger til innbygger.


|   |   |
| ---| ---|
| Status: | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| Informasjonselement | Fysisk sted/avdeling/Organisasjonsenhet hvor helsepersonellet yter helsehjelp |
| Attributt: | "department" |
| Attributt EHDSI: | N/A |
| Avtalemessig påkrevd | **Ja, hvis forekommer** |
| Obligatorisk:| **Nei** |
| Data type: | Object |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Kodeverk: | RESH/Enhetsregisteret [????] |
| Gyldige verdier: | N/A |





###### "department" - Attributter JSON format

````JSON
"department": {
        "id": "resh:121313", 
        "system": "resh:x.x.x.x.x.x.x",
        "name": "UNN ....",
        "authority": "",
    },
````

##### "healthcare_service": Helsetjenestetype
Attributtet "healthcare_service" angir hvilken type helsetjenester som leveres/ytes ved virksomheten som helsepersonellet jobber for.

| :warning:               | Intern kommentar fra team dok.deling | Modenhet |
|--------------------------|:------------------------|-----|
| "healthcare_service"     | Utydelig kardinalitet for dette informasjonselementet. En helsevirksomhet yter gjerne flere typer av helsehjelp. Gitt at det blir kun maks 1 tjeneste som kan knyttes til aktøren, kan formålet endre seg etter Aut&Aut? Denne kan brukes aktivt i NHNs tjenesten for dok.deling. | Lav |
|                          | I XUA (SAML) blir denne verdien overskrivet dersom helsepersonell viser seg til å være "fastlege" for pasienten denne forespørsel gjelder | |

Attributtet _kan_ benyttes til tilgangsstyring hos datakilden (som erstatning for eller i kombinasjon med rolle), men også i forbindelse med loggkontroll/analyse og ved innsyn til innbygger.

|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Hvilken type helsetjenester som leveres ved virksomheten hvor helsepersonellet yter helsehjelp |
| Attributt: | "healthcare_service" |
| Attributt EHDSI: | N/A |
| Obligatorisk: | **Ja** |
| Data type: | string |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Kodeverk: | [Tjenestetyper innen spesialisthelsetjenesten](https://volven.no/produkt.asp?open_f=true&id=495806&catID=3&subID=8&subCat=163&oid=8627)<br/>[Tjenestetyper for spesialisthelsetjenesten](https://volven.no/produkt.asp?open_f=true&id=496329&catID=3&subID=8&subCat=163&oid=8668)<br/>[Tjenestetyper for kommunal helse- og omsorgstjeneste mv](https://volven.no/produkt.asp?open_f=true&id=496326&catID=3&subID=8&subCat=163&oid=8663)<br/>[Fylkeskommunale tjenestetyper](https://volven.no/produkt.asp?open_f=true&id=496298&catID=3&subID=8&subCat=163&oid=8662)<br/>[Tjenestetyper for apotek og bandasjister](https://volven.no/produkt.asp?open_f=true&id=496327&catID=3&subID=8&subCat=163&oid=8664)<br/>[Felles tjenestetyper](https://volven.no/produkt.asp?open_f=true&id=496328&catID=3&subID=8&subCat=163&oid=8666) |
| Gyldige verdier:| N/A |



###### "healthcare_service" - Attributter JSON format

````JSON
"healthcare_service":{
	"text": "Sykepleietjeneste",
	"code": "KP02",
	"system": "8663",
	"assigner": "www.helsedirektoratet.no"
}
````

##### "purpose_of_use": formålet med behandlingen av personopplysninger
Attributtet "purpose_of_use" beskriver det overordnede formålet som helsepersonellet har med behandlingen av personopplysninger.

|   |   |
| ---| ---|
| Status: | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| Informasjonselement | Kodifisert beskrivelse av hva helsepersonellet skal benytte helseopplysningene til  |
| Attributt: | "purpose_of_use" |
| Attributt EHDSI: | "urn:oasis:names:tc:xspa:1.0:subject:purposeofuse" |
| Obligatorisk: | **Ja** |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Data type: | Object |
| Kodeverk: | urn:oid:2.16.840.1.113883.1.11.20448 - [HL7](https://terminology.hl7.org/ValueSet-v3-PurposeOfUse.html) |
| Gyldige verdier:| TREAT //Behandling,  <br/>ETREAT  //Nødtilgang,<br/>COC  //Administrativ tilgang<br/> |


###### "purpose_of_use" - JSON format

````JSON
"purpose_of_use": {
	"code": "TREAT",
	"text": "Behandling",
	"system": "urn:oid:2.16.840.1.113883.1.11.20448",
	"assigner": "http://terminology.hl7.org/ValueSet/v3-PurposeOfUse"
}
````

##### "purpose_of_use_details": type tjeneste som pasienten skal motta hos virksomheten
Attributtet "purpose_of_use_details" beskriver konklusjonen av tilgangangsreglene som ligger til grunn for at helsepersonellet er blitt gitt tilgang til pasientens helseopplysninger i hens journalsystem. Attributtet representerer en oppsummering av tilgangsbeslutningen i lokalt system hos konsument.

| :warning:                | Intern kommentar fra team dok.deling | Modenhet |
|-------------------- -----|:------------------------|-----|
| "purpose_of_use_details" | Dette elementet har ingen verdi for tilgangsstyring til tjenesten dok.deling hos Norsk helsenett. Dette elementet ønskes av representanter fra sektoren og derfor kan ikke Norsk helsenett stå ansvarlig for evt. mangler ute i sektoren. Må ses som en informasjonselement som evt. blir tatt ut i fremtidige versjoner | Lav |


Attributtet knytter helsepersonellet til pasienten ved å gi en forklaring på hvorfor helsepersonellet trenger helseopplysningene.

Informasjonen i attributtet kan beskrives ved bruk av forskjellige kodeverk avhengig av hvilke helsetjenester pasienten mottar.

Formålet med dette attributtet er å gi kilden dokumentasjon av grunnlaget for tilgjengeliggjøringen for bruk i loggkontroll samt som informasjon til innbygger.

For kommune vil denne være gitt av: .....
I spesialist vil denne være gitt av beslutningsmal.


|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Kodifisert beskrivelse av tjenesten som virksomheten yter til pasienten  |
| Attributt: | "purpose_of_use_details" |
| Attributt EHDSI: | N/A |
| Obligatorisk: | **Ja** |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Data type: | Object |
| Kodeverk: | Kommune: urn:oid:x.x.x.x.x.9151 - [volven](https://volven.no/produkt.asp?open_f=true&id=494341&catID=3&subID=8&subCat=140&oid=9151)<br/>Spesialisthelsetjenesten:[HL7 Norway](https://hl7norway.github.io/AuditEvent/currentbuild/CodeSystem-carerelation.html) |
| Gyldige verdier:| N/A |

###### "purpose_of_use_details" - JSON format

````JSON
"purpose_of_use_details": {
	"code": "15",
	"text": "Helsetjenester i hjemmet",
	"system": "urn:oid:x.x.x.x.x.9151",
	"assigner": "https://www.helsedirektoratet.no/"
},
````


##### "tracing_ref": referanse til systemet som initierte forespørselen
Attributtet er en referanse til det systemet som har initiert traffikken. Denne referanse kan gjerne referere til en lokal beslutning som ble benyttet ved å identifere forespørselen på et senere tidspunkt. Referansen skal sikre sporbarhet på tvers mellom systemene, slik at konsumenter og kilder av opplysninger har tilgang til felles identifikator. Hver forespørsel som initieres av konsumentens system skal ha en unik identifikator som følger sesjonen og relatert pasient kontekst.

Målet med å bruke elementet er også å kunne begrense gyldighet av selve tokenet som utveksles slik at den ikke skal kunne gjenbrukes på et senere tidspunkt.

Systemet må sørge for å angi denne informasjon til kilden av helseopplysninger ved å øverføring og samtidig ta vare på denne identifikator for senere anledning.

~~Attributtet er en referanse til den lokale tilgangsbeslutningen hos konsumenten. Formålet med dette attributtet er at kilden skal være i stand til å referere til en lokal beslutning hos konsumenten ved behov for oppfølging etter en logganalyse.~~

| :warning:                | Intern kommentar fra team dok.deling | Modenhet |
|--------------------------|:------------------------|-----|
| "tracing_ref"            |   | Lav |


|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Ekstern referanse til opprinnelse av forespørselen  |
| Attributt: | "tracing_ref" |
| Attributt EHDSI: | N/A |
| Obligatorisk: | **Ja** |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Data type: | GUID |
| Kodeverk: | N/A |
| Gyldige verdier:| regex = “^[{]?[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}[}]?$”  |


###### "tracing_ref" - Attributter JSON format

````JSON
    "tracing_ref": {
        "ref_id" : "id til lokal tilgangsbeslutning", 
    }
````

#### 4.2.7 Kategori: Pasient - "patient_id"
##### "patient_id": Unik identifikator for pasienten

Attributtet er til behandling av NHN - ROS/DIPA

**Kommentar fra dok.deling: Vi må huske på at modellen som diskuteres skal være felles for XUA og JWT. Dersom STS velger å ikke ha dette informasjonselementet i JWT så kan den fortsatt være aktuell for XUA (SAML) som vil inkludere det.**

| Attributt | |
| --- | --- |
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Unik identifikator for pasienten som helsepersonellet ber om helseopplysninger for |
| Attributt: | "patient" |
| Attributt EHDSI: | |
| Fødselsnummer | Pasientens fødelsenummer fra folkeregisteret |

###### "patient_id" - Attributter JSON format

````JSON
"patient": {
	"id": "05076600324",
	"name": "Kognar Maman",
	"system": "urn:oid:2.16.578.1.12.4.1.4.1",
	"authority": "https://www.skatteetaten.no"
}
````



## 5. JSON profil for datamodell
Full modell - valgfrie elementer er tatt med

````JSON
{
	"care_relationship": {
		"healthcare_service": {
			"code": "S03",
			"text": "Indremedisin",
			"system": "urn:oid:2.16.578.1.12.4.1.1.8655",
			"assigner": "https://www.helsedirektoratet.no/"
		},
		"department": {
			"id": "resh:121313", 
			"system": "resh:x.x.x.x.x.x.x",
			"name": "Avdeling ved Sykehus",
			"authority": "RESH",
    	},
		"purpose_of_use": {
			"code": "TREAT",
			"text": "Behandling",
			"system": "urn:oid:2.16.840.1.113883.1.11.20448",
			"assigner": "http://terminology.hl7.org/ValueSet/v3-PurposeOfUse"
		},
		"purpose_of_use_details": {
			"code": "15",
			"text": "Helsetjenester i hjemmet",
			"system": "urn:oid:x.x.x.x.x.9151",
			"assigner": "https://www.helsedirektoratet.no/"
		},
		"tracing_ref": {
			"ref_id" : "[id til lokal kjente identifikator som blir en ekstern referanse for kilden]",
		}
	},
}
````
