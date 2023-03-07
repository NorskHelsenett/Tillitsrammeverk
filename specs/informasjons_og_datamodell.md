# Informasjons- og datamodell for beskrivelse av tilgangssgrunnlaget ved deling av helseopplysninger

## Sammendrag
Denne spesifikasjonen definerer en informasjons- og datamodell som skal brukes for å uttrykke et helsepersonells grunnlag for tilgang til helseopplysninger ved deling av helseopplysninger på tvers av helsevirksomheter i helse- og omsorgssektoren i Norge.


## Dokumentets status

| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| -0 | Utkast | 17.02.2023 |

Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til tillitsrammeverk for deling av helseopplysninger i helse- og omsorgssektoren.
Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i tillitsrammeverket.

Spesifikasjonen skal versjoneres for å støtte endringer over tid.


## Innholdsfortegnelse
1. Innledning<br/>
2. Bakgrunn
3. Spesifikasjon<br/>
	3.1 Informasjonsmodell<br/>
	3.2 Datamodell<br/>
4. Sikkerhets- og personvernshensyn<br/>
	4.1 Cybersikkerhet<br/>
	4.2 Personvern 
5. Anerkjennelse av bidragsytere til spesifikasjonen
6. Eksempler på bruk av datamodell<br/>
	6.1 JSON eksempel<br/>
	6.2 SAML eksempel<br/>
7. Normative referanser 


## 1. Innledning 
For å gi riktig helsehjelp til riktig tid må helsepersonell ha tilgang til helseopplysninger som ligger lagret hos andre virksomheter enn den virksomheten hvor de yter helsehjelp. Lovverket vårt sier at helsevirksomheter er pliktig til å dele helseopplysninger med alt helsepersonell så fremt de har et tjenstlig behov og at opplysningene er relevante og nødvendige i helsepersonellets behandling av pasienten.

Kravene knyttet til tjenstlig behov og opplysningenes relvans og nødvendighet i behandlingen av pasienten medfører at virksomhetene som har dataansvar for helseopplysningene må styre tilgang på en tilfredsstillende måte.

I tillitsrammeverket legges det opp til en oppgavefordeling knyttet til tilgangsstyring, slik at den konsumerende virksomheten utfører tilgangsstyring til helseopplysninger på vegne av virksomheten som skal dele helseopplysningene. Til tross for at den konsumerende virksomheten er forpliktet til å kontrollere at deres helsepersonell har en gyldig grunn for tilgang til helseopplysninger har virksomheten som deler opplysninger likevel behov for å motta informasjon som beskriver grunnlaget for tilgangen. Informasjonen som beskriver grunnlaget for delingen vil benyttes til flere formål:
* å utføre ytterligere tilgangskontroll
* lovpålagt logging av tilgangen for å avdekke urettmessig tilegnelse av helseopplysninger
* å støtte opp under innbyggers rettigheter

På grunn av at tilgangsstyring er implementert på forskjellig måte i forskjellige systemer og virksomheter er det nødvendig at sektoren samler seg om et felles språk for å uttrykke grunnlaget for tilgang slik at aktørene kan forstå hverandre. Et felles språk vil også bidra til å kommunisere på en konsistent måte til innbygger.

Denne spesifikasjonen definerer et felles språk som skal benyttes til å uttrykke helsepersonells grunnlag for tilgang til helseopplysninger ved deling av helseopplysninger via tekniske grensesnitt.
Spesifikasjonen definerer en informasjonsmodell og en datamodell som skal implementeres i programvare som benyttes av helsepersonell når de yter helsehjelp til sin pasient.


 
## 2. Bakgrunn for spesifikasjonen
Aktørene i helse- og omsorgssektoren har samlet seg rundt en felles tillitsmodell som skisserer tillitsgrunnlaget for å dele helseopplysninger mellom helsepersonell på tvers av virksomhetene i sektoren.

Tillitsmodellen konkretiseres i et tillitsrammeverk som består av vilkår knyttet til bruken av tillitstjenestene. Den første anvendelsen av tillitsrammeverket, og denne spesifikasjonen, er i prosjektet som skal etablere nasjonal dokumentdeling i Kjernejournal.


## 3. Spesifikasjon

Spesifikasjonen inneholder en informasjonsmodell som beskriver hvilken informasjon som skal overføres mellom aktørene, hva denne informasjonen beskriver, og hvorfor den skal overføres.

Spesifikasjonen beskriver også hvilke konkrete attributter som skal brukes for å beskrive informasjonsmodellen i form av en datamodell. Datamodellen beskriver også hvilke verdier som er gyldige for attributtene.

Spesifikasjonen skal benyttes av programvare- og systemleverandører ved implementasjon av programvare som skal brukes ved deling av helseopplysninger på tvers av virksomheter i sektoren. Datamodellen vil implementeres i relevante nasjonale ehelseløsninger og tillitstjenester.

Datamodellen skal benyttes til flere formål:
* for tilgangsstyring og tilgangskontroll i ehelseløsninger, dokumentkilder og i API
* til logging
* for å tilfredsstille pasientens rettigheter

### 3.1 Informasjonsmodell
Informasjonen som skal overføres fra konsument til datakilde kan deles inn i tre hovedkategorier:
1. Informasjon om helsepersonellets identitet
2. Informasjon om helsepersonellets behandlerrelasjon ovenfor pasienten
3. Informasjon om pasienten


#### 3.1.1 Helsepersonellets Identitet
Helsepersonellets grunnleggende identitet består av informasjon som sjelden endres, slik som personens navn og fødselsnummer, i tillegg til helsepersonellets offentlige godkjenninger.

Helsepersonellets identitet er nødvendig å overføre fordi vi må kunne knytte en tilgang til helseopplysninger til en gitt person. Identiteten vil benyttes i forbindelse med tilgangsstyring, tilgangskontroll og logging. 

#### 3.1.2 Helsepersonellets behandlerrelasjon til sin pasient
I delingssammenheng består helsepersonellets digitale identitet også av informasjon som beskriver hvorfor helsepersonellet har behov for tilgang til pasientens helseopplysninger. Disse informasjonselementene forteller noe om helsepersonellets behandlerrelasjon til pasienten.

Norsk lov sier at helsepersonell bare skal gis tilgang til helseopplysninger dersom det foreligger et tjenstlig behov og at opplysningene er relevant og nødvendig i behandlingen av pasienten. Det er helsepersonellet og konsumentens ansvar å sørge for at tilgangen til helseopplysningene er i henhold til loven, men den utleverende part har likevel behov for overført informasjon som beskriver bakgrunnen for forespørselen om helseopplysninger for å tilfredsstille lovkrav knyttet til dokumentasjon og å utføre tilgangskontroll. 

Informasjonen som beskriver helsepersonellets behandlerrelasjon til sin pasient består av følgende informasjon:
* Helsepersonellets rolle i sin behandling av pasienten
* Helsevirksomhet og behandlingssted
* Helsetjenestetype ved behandlingssted
* Formålet med behandlingen av helseopplysninger

#### 3.1.3 Pasientens identitet
Det er en selvfølge at pasienten må identifiseres ved deling av helseopplysninger. Det er ikke nødvendig å overføre annen informasjon om pasienten enn en unik identifikator.


#### 3.1.4 Oppsummert informasjonsmodell

```mermaid
---
title: Informasjonsmodell
---
classDiagram
	Helsepersonell --* Behandlerrelasjon
	Behandlerrelasjon --* Pasient
    class Helsepersonell{
	    +Object Identitet
    }
    class Behandlerrelasjon{
		+Object KontekstuellInformasjon
    }
    class Pasient{
    		+Object PasientIdentifikator
    }

```

### 3.2 Datamodell 
Informasjonsmodellen skal overføres fra konsument til datakilde i form av attributter formattert som nøkkelverdipar. Disse attributtene danner datamodellen, og er en detaljert beskrivelse av hvordan informasjonen skal uttrykkes.

#### 3.2.1 Prinsipper for datamodellen 
Datamodellen skal legge til rette for at helsevirksomhetene lettere kan samhandle med hverandre ved at man benytter samme språk for å uttrykke informasjonen som beskriver helsepersonellet og konteksten som helsepersonellet befinner seg i når han ber om tilgang til helseopplysningene. Den skisserte datamodellen legger til rette for en viss grad av dynamikk ved å angi hvilket kodeverk eller lister over gyldige verdier som er benyttet i datasettet.

Datamodellen skal brukes i sikkerhetsbilletter som skal behandles av mange aktører og i mange systemer. Aktørene som mottar og behandler sikkerhetsbillettene må ha svært høy tillit til at informasjonen er trygg. Det skal være usannsynlig at datamodellen kan inneholde data som kan brukes til sikkerhetsangrep via sikkerhetsbilletter.

> TODO: Informasjonen i datamodellen skal være sporbar slik at vi ivaretar prinsippet om uavviselighet… 

> TODO: mer her om tillitsnivå/sikkerhetsnivå/identiteter osv.. Hvem er den autoritative kilden til informasjonen osv..



#### 3.2.2 Oversikt over attributter i datamodellen 

```mermaid
---
title: Datamodell
---
classDiagram

	Helsepersonell -- Behandlerrelasjon
	Helsepersonell o-- IdentityAttribute
	Behandlerrelasjon o-- IdentityAttribute
	Behandlerrelasjon o-- PurposeOfUse
	Behandlerrelasjon o-- Organization
	Organization o-- LegalEntity
	Organization o-- IdentityAttribute
	PurposeOfUse --|> IdentityAttribute
	Behandlerrelasjon -- Pasient

	class Helsepersonell{
		+IdentityAttribute name
		+IdentityAttribute pid
		+String hpr_nr
	}
		
	class Behandlerrelasjon{
		+IdentityAttribute functionalRole
		+IdentityAttribute clinicalSpeciality
		+Organization healthCareInstitution
		+PurposeOfUse purposeOfUse
	}
	
	class Pasient{
		+String pid
	}
	
	class IdentityAttribute{
		+String value
		+String oid_system
		+bool isOptional		
	}	
	
	class LegalEntity{
		+String id
		+String name		
	}
	class Organization{
		+LegalEntity legalEntity
		+LegalEntity pointOfCare
		+IdentityAttribute facility
		+String locality
	}
	
		
```

#### 3.2.3 Oppsummering av påkrevd eller valgfri informasjon
Ikke all informasjon i datamodellen er relevant, noen informasjonselementer er valgfrie.

Vi har lagt vekt på å ivareta sporbarheten i delingssammenheng, derfor har vi angitt at alle identifikatorer er påkrevd, dette gjelder både fysiske og juridiske personer.

| Informasjon | Beskrivelse | Informasjonskilde | Påkrevd | Status |
| --- | --- | --- | --- | --- |
| "pid" | Fødselsnummer fra folkeregisteret | HelseID | **Ja** | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| "hpr_nr" | Helsepersonellets HPR-nummer, dersom det finnes | HelseID | **Nei** | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| "functional_role" | Helsepersonellets funksjonelle rolle hos virksomheten | Konsumentens EPJ | **Ja** | <span style="color: red; font-weight: bold;">Under behandling</span> |
| "clinical_speciality" | Helsepersonellets kliniske spesialitet | Konsumentens EPJ | **Nei** | <span style="color: red; font-weight: bold;">Under behandling</span> |
| "legal_entity" | Den dataansvarlige virksomhetens org.nr og navn. | - Konsumentens EPJ for §9 samarbeid og multi-tenancy system<br>- HelseID for single-tenancy/on-premise system | **Ja** | <span style="color: green; font-weight: bold;">Inkluderes</style> |
| "point_of_care" | Behandlingsstedets org.nr. og navn.<br>Kan være lik verdi som i "legal_entity" | Konsumentens EPJ | **Ja** | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| "facility_type" | Helsetjenestetyper som leveres ved virksomheten | Konsumentens EPJ | **Ja** | <span style="color: red; font-weight: bold;">Under behandling</span> |
| "locality" | Avdeling/org.enhet hvor helsepersonellet yter helsehjelp | Konsumentens EPJ | **Ja** |<span style="color: red; font-weight: bold;">Under behandling</span> |
| "purpose_of_use" | Helsepersonellets formåle med helseopplysningene (til hva de skal brukes) | Konsumentens EPJ | **Ja** | <span style="color: red; font-weight: bold;">Under behandling</span> |
| "patient_id" | Unik identifikator for pasienten | Konsumentens EPJ | **Ja** | <span style="color: red; font-weight: bold;">Under behandling</span> |

#### 3.2.4 Relasjon til eHSDI datamodell og avvik fra EHDSI sine spesifikasjoner

I forbindelse med EU regulativet EHDS er det definert en datamodell for utveksling av helseopplysninger på tvers av landegrenser innad i EU. Vi har tatt utgangspunkt i denne datamodellen når vi har beskrevet informasjons- og datamodellen som skal benyttes ved deling av helseopplysninger innad i Helsenettet, men har tilpasset den til våre behov.


#### 3.2.5 Kategori: Helsepersonellet
Helsepersonellets identitet angis ved bruk av identifikator fra folkeregisteret, navn, og identifkator fra HPR.
Består av identifikatorer fra folkeregisteret og helsepersonellregisteret, samt informasjon som indikerer hvorvidt dette er et helsepersonell (med/uten lisens) eller administrativt personell.


##### 3.2.5.1 Identifikator for helsepersonellet som "fysisk person"
Attributtet "pid" er en forkortelse for "personal identifier", hvor verdien identifiserer en fysisk  person. 

|   |   |
| ---| ---|
| Informasjonselement | Unik identifikator for helsepersonellet |
| Attributt: | "pid" |
| Attributt EHDSI: | "urn:oasis:names:tc:xacml:1.0:subject:subject-id" |
| Obligatorisk: | **Ja** |
| Data type: | String |
| Autoritativ kilde: | Folkeregisteret - Skattedirektoratet |
| Informasjonskilde: | HelseID, basert på innlogging via eID ordning |
| Kodeverk: | 2.16.578.1.12.4.1.4.1 (F-nummer),<br/>2.16.578.1.12.4.1.4.2 (D-nummer),<br/>2.16.578.1.12.4.1.4.3 (H-nummer)|

###### Identifikator for Helsepersonellet - Attributt SAML format

````XML
<saml:Attribute Name="2.16.578.1.12.4.1.4.1">
	<saml:AttributeValue xsi:type="xs:string">xxxxxx34794</saml:AttributeValue>
</saml:Attribute>
````

###### Identifikator for Helsepersonellet - Attributt JSON format

````JSON
"pid":{
	"value": "xxxxxx34794",
	"oid_system": "2.16.578.1.12.4.1.4.1"
}
````

##### 3.2.5.3 Informasjon om helsepersonellet fra Helsepersonellregisteret

###### Helsepersonellnummer
Attributtet "hpr_nr" er en forkortelse for "Helsepersonellnummer" hvor verdien identifiserer et helsepersonell som har fått autorisasjon og/eller lisens til å praktisere som et helsepersonell i Norge.

Noe helsepersonell har ikke autorisasjon, men trenger likevel tilgang på helseopplysninger. Derfor kan ikke attributtet være påkrevd, men skal inkluderes i datamodellen dersom den fysiske personen har et innslag i HPR.
 
|   |   |
| ---| ---|
| Attributt: | "hpr_nr" |
| Status: | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| Informasjonselement | Unik identifikator for helsepersonellet knyttet opp til formelle autorisasjoner eller lisenser |
| Attributt EHDSI: | N/A (?) |
| Obligatorisk: | **Nei** |
| Data type: | String |
| Autoritativ kilde: | Helsepersonellregisteret - Helsedirektoratet |
| Informasjonskilde: | HelseID, basert på oppslag mot HPR etter vellykket pålogging av helsepersonell. |
| Kodeverk: | 2.16.578.1.12.4.1.4.4 |


###### Helsepersonellets funksjonelle rolle - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Helsepersonellregister - Atributter JSON format

````JSON
"professional_license": {
	"hpr_nr": "xxxxxxxxx",
	"oid": "xx.xx.xx.xx"
}
````

#### 3.2.6 Kategori: Behandlerrelasjon
Helsepersonellets behandlerrelasjon til pasientent angis ved hans rolle, spesialitet, virksomhet hvor han yter helsehjelp, behandlingssted, helsetjenestetype og en angivelse av formålet med behandlingen av helseopplysningene.

##### 3.2.6.1 Helsepersonellets funksjonelle rolle
Attributtet "functional_role" representerer helsepersonellets rolle hos virksomheten i hans behandling av pasienten, og angis av kode fra STYRK-08.

|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Yrkesklassifisering av helsepersonellet i organisasjonen.<br/>Basert på den internasjonale standarden ISCO-08 |
| Attributt: | "functional_role" |
| Attributt EHDSI: | "urn:oasis:names:tc:xspa:1.0:subject:functional-role" |
| Obligatorisk: | **Ja** |
| Data type: | String |
| Autoritativ kilde: | Konsumenten - helsepersonellets rolle hos virksomheten |
| Informasjonskilde: | Konsumentens EPJ/HR system |
| Kodeverk: | STYRK-08 (ISCO-08) |
| Gyldige verdier: | Helsefaglige koder (må avklares - subsett av STYRK-08) |

###### Helsepersonellets funksjonelle rolle - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Helsepersonellets funksjonelle rolle - Attributter JSON format
````JSON
"functional_role": {
	"Text": "Lege", 
	"value": "2211",
	"oid": "STYRK-08"
}
```` 


##### 3.2.6.2 Helsepersonellets spesialitet
Attributtet "clinical_speciality" representerer helsepersonellets spesialitet i sin behandling av pasienten

|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Helsepersonellets spesialitet |
| Attributt: | "clinical_speciality" |
| Attributt EHDSI: | "urn:ehdsi:names:wp3.4:subject:clinical-speciality" |
| Obligatorisk: | **Nei** |
| Data type: | String |
| Autoritativ kilde: | Konsumenten - helsepersonellets rolle i virksomheten |
| Informasjonskilde: | Konsumentens EPJ/HR system |
| Kodeverk: | SNOMED-CT: Clinical-speciality |
| oid: | 2.16.840.1.113883.3.88.12.80.72 |

###### Helsepersonellets spesialitet - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Helsepersonellets spesialitet - Attributter JSON format
````JSON
"clinical_speciality": {
	"text": "xxxxxx",
	"code": "419772000",
	"oid": "xx.xx.xx.xx.xx.xx"
}
```` 


##### Den dataansvarlige virksomheten 
Attributtet "legal_entity" identifiserer den dataansvarlige hvor helsepersonellet yter helsehjelp.

Informasjonskilden til dette attributtet er avhengig av systemarkitektur eller hvorvidt systemet brukes i §9-samarbeid.

- For multi-tenancy løsninger og §9-samarbeid må journalsystemet hos konsumenten angi "legal_entity". HelseID kontrollerer at databehandler har rett til å opptre på vegne av helsevirksomheten ved å gjøre oppslag i delegeringer som er utført i Altinn.
- For single-tenancy/on-premise løsninger vil HelseID utlede helsevirksomhet.

|   |   |
| ---| ---|
| Status: | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| Informasjonselement | Virksomheten (hovedenhet) som har dataansvaret der hvor helsepersonellet yter helsehjelp |
| Attributt: | "legal_entity" |
| Attributt EHDSI: | "urn:oasis:names:tc:xspa:1.0:subject:organization"<br/>"urn:oasis:names:tc:xspa:1.0:subject:organization-id" |
| Obligatorisk: | **Ja** |
| Data type: | String |
| Autoritativ kilde: | Enhetsregisteret - SSB |
| Informasjonskilde: | §9/multi tenancy: Konsumentens journalsystem<br>single-tenancy: Utledes av HelseID  |
| Kodeverk: | 2.16.578.1.12.4.1.4.101 |


###### Den dataansvarlige virksomheten - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Den dataansvarlige virksomheten - Attributter JSON format

````JSON
"legal_entity": {
	"id": "921592761",
	"name": "Lege Leif Lagesen ENK",
	"oid": "2.16.578.1.12.4.1.4.101"
}
```` 

##### Behandlingssted

Attributtet "point_of_care" identifiserer behandlingsstedet hvor helsepersonellet yter helsehjelp.<br>
Attributtet er obligatorisk. Dersom verdiene for "legal_entity" og "point_of_care" er like skal den gjentas i begge attributter.

|   |   |
| ---| ---|
| Status: | <span style="color: green; font-weight: bold;">Inkluderes</span> |
| Informasjonselement | Virksomheten (underenhet) hvor helsepersonellet yter helsehjelp |
| Attributt: | "point_of_care" |
| Attributt EHDSI: | N/A |
| Obligatorisk: | **JA** |
| Data type: | String |
| Autoritativ kilde: | Enhetsregisteret - SSB |
| Informasjonskilde: | Konsumentens journalsystem |
| Kodeverk: | 2.16.578.1.12.4.1.4.101 |

Attributtet "point_of_care_name" inneholder navnet på behandlingsstedet hvor helsepersonellet yter helsehjelp.

###### Behandlingssted - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Behandlingssted - Attributter JSON format

````JSON
"point_of_care": {
	"id": "123456789",
	"name": "Det beste legekontoret i byen AS",
	"system_oid": "2.16.578.1.12.4.1.4.101"
}
````


##### Helsetjenestetype
Attributtet "facility_type" angir hvilken type helsetjenester som leveres ved virksomheten som helsepersonellet jobber for.

|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Hvilken type helsetjenester som leveres ved virksomheten hvor helsepersonellet yter helsehjelp |
| Attributt: | "facility_type" |
| Attributt EHDSI: | "urn:ehdsi:names:subject:healthcare-facility-type" |
| Obligatorisk: | **Ja** |
| Data type: | string |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Kodeverk: | - eHealth DSI code list<br/>-Volven<br/>  |
| oid code: | 1.3.6.1.4.1.12559.11.10.1.3.2.2.2<br/>volven: 8627<br/>volven: 8662<br/>volven: 8663<br/>volven: 8664<br/>volven: 8665<br/>volven: 8666 |
| Gyldige verdier:| Hospital,<br/>Resident Physician,<br/>Pharmacy,<br/>++? |

###### Helsetjenestetype - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Helsetjenestetype - Attributter JSON format

````JSON
"facility_type":{
	"text": "Sykepleietjeneste",
	"code": "KP02",
	"system_oid": "8663"
}
````

##### Fysisk sted
Attributtet "locality" angir fysisk sted/avdeling hvor helsepersonellet yter eller administrerer helsehjelp.

|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Fysisk sted/avdeling/Organisasjonsenhet hvor helsepersonellet yter helsehjelp |
| Attributt: | "locality" |
| Attributt EHDSI: | "urn:oasis:names:tc:xspa:1.0:environment:locality" |
| Obligatorisk:| **Ja** |
| Data type: | String |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Kodeverk: | ingen |
| Gyldige verdier: | kun alfanumeriske tegn (regex: "^[a-zA-Z0-9_]*$") |

###### Fysisk sted - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Fysisk sted - Attributter JSON format

````JSON
"locality": "Helsehjelpgata 4, 0001 Valderborg"

````

##### Formålet med behandlingen av personopplysninger
Attributtet "purpose_of_use" beskriver det overordnede formålet med behandlingen av personopplysninger.

|   |   |
| ---| ---|
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Kodifisert beskrivelse av hva helsepersonellet skal benytte helseopplysningene til  |
| Attributt: | "purpose_of_use" |
| Attributt EHDSI: | "urn:oasis:names:tc:xspa:1.0:subject:purposeofuse" |
| Obligatorisk: | **Ja** |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Data type: | String |
| Kodeverk: | urn:oid:2.16.840.1.113883.1.11.20448<br/> HL7 - https://terminology.hl7.org/ValueSet-v3-PurposeOfUse.html |
| Gyldige verdier:| TREAT, <br/>ETREAT,<br/>... |

###### Formålet med behandlingen av personopplysninger - Attributter SAML format

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Formålet med behandlingen av personopplysninger - Attributter JSON format

````JSON
"purpose_of_use": {
	"value": "TREAT",
	"system_oid": "urn:oid:2.16.840.1.113883.1.11.20448"
}

````

#### 3.2.7 Kategori: Pasient
##### Unik identifikator for pasienten

| Attributt | |
| --- | --- |
| Status: | <span style="color: red; font-weight: bold;">Under behandling</span> |
| Informasjonselement | Unik identifikator for pasienten som helsepersonellet ber om helseopplysninger for |
| Attributt: | "patient_id" |
| Attributt EHDSI: | |
| Fødselsnummer | Pasientens fødelsenummer fra folkeregisteret |

````XML
<AttributeStatement>
<saml:Attribute>
??
</saml:Attribute>
````

###### Formålet med behandlingen av personopplysninger - Attributter JSON format

````JSON
"patient": {
	"id": "TREAT",
	"oid": "urn:oid:2.16.840.1.113883.1.11.20448"
}

````

## 4. JSON profil for datamodell
Full modell - valgfrie elementer er tatt med

````JSON
{
	"practicioner": {
		"pid":{
			"value": "xxxxxx34794",
			"name": "Lege Legesen",
			"oid": "2.16.578.1.12.4.1.4.1"
		},
		"professional_license": {
			"hpr_nr": "xxxxxxxxx",
			"oid": "x.x.x.x.x.x."
		}
	},
	"care_relationship": {
		"functional_role": {
			"code": "2211",
			"oid": "STYRK-08"
		},
		"clinical_speciality": {
			"value": "419772000",
			"oid": ""
		},
		"legal_entity": {
			"id": "921592761",
			"name": "Lege Leif Lagesen",
			"oid": "2.16.578.1.12.4.1.4.101"
		},
		"point_of_care": {
			"id": "123456789",
			"name": "Det beste legekontoret i byen AS",
			"oid": "2.16.578.1.12.4.1.4.101"
		},
		"facility_type":{
			"text": "helsetjenestetype",
			"value": "05",
			"oid": ""
		},
		"locality": "Helsehjelpgata 1 0001 Valderborg",
		"purpose_of_use": {
			"Text": "beskrivelse",
			"code": "TREAT",
			"oid": ""
		}
	},
	"patient": {
		"value": "xxxxxx95164",
		"oid": "2.16.578.1.12.4.1.4.1"
	}
}
````

## 5. SAML profil for datamodell

````xml

```` 


## 6. Sikkerhets- og personvernshensyn
### 6.1 Cybersikkerhet
Både egenprodusert og tredjeparts programvarekomponenter som brukes til datalagring samt behandling og presentasjon av informasjonen i datamodellen kan inneholde svakheter som lar en angriper utnytte data som overføres mellom partene til å utføre forskjellige typer angrep på innsiden av en organisasjon.

Informasjonen i datamodellen flyter mellom flere aktører hvor den lagres og behandles av forskjellige typer programvare. Sikkerhetsangrep som utføres i forbindelse med datalagring er svært vanlig, og utgjør en generell sikkerhetsrisiko som kan begrenses ved at verdier som overføres kan valideres og kontrolleres.

Informasjonen i datamodellen vil blant annet benyttes til å utføre analyse av logger, og vil kunne bli vist til sluttbrukere i forskjellige applikasjoner. Dette åpner for angrep mot sårbarheter i programvare, som f.eks. misbruk av makroer eller XSS angrep i nettlesere. Sannsynligheten for denne typen sikkerhetsangrep bør begrenses ved at verdier som overføres kan valideres og kontrolleres.


### 6.2 Personvern

Datamodellen legger til rette for en utlevering av personopplysninger, herunder helseopplysninger, som en behandling av en særlig kategori av personopplysninger, gjennom å sammenstille opplysninger om helsepersonellet, pasientens identifikasjonsnummer, opplysninger om virksomheten der helsehjelpen utføres, formålet med tilgangen til helseopplysninger og relasjonen mellom helsepersonellet og pasienten, for å autentisere tilgang til gitte helseopplysninger.

#### 6.2.1 Tap av personopplysninger
Ved å utnytte svakheter og sårbarheter i programvare kan kan en angriper observere personopplysninger som utleveres mellom tekniske tjenester som benyttes av virksomheter ved deling av helseopplysninger.
Tap av personopplysninger kan oppstå mellom flere parter i verdikjeden:

- mellom konsument og autorisasjonsserver/IdP
- mellom konsument og informasjonstjeneste
- mellom informasjonstjeneste og datagrensesnitt

For å sikre mot potensielt tap av personopplysninger bør det vurderes å etablere tiltak for å ivareta konfidensialiteten.

#### 6.2.2 Overvåkning av ansatte i andre virksomheter
Datamodellen innebærer en utlevering av opplysninger om helsepersonellets arbeidsforhold. Disse opplysningene utleveres til andre virksomheter enn den virksomheten helsepersonellet er ansatt hos eller yter helsehjelp på vegne av. Det legges derfor til rette for at opplysninger kan benyttes til å monitorere helsepersonell i andre virksomheter. Dataansvarlige må følgelig være bevisste begrensningene i formålet med behandlingen av personopplysninger og eventuelt vurdere risiko knyttet til behandling av personopplysninger utover dette formålet.

#### 6.2.3 Vurdering av personvernkonsevenser
For å ivareta rettighetene og frihetene til pasienten og helsepersonellet som registrerte, bør dataansvarlig virksomhet vurdere hvorvidt behandlingen av personopplysninger medfører høy risiko for at de registrertes rettigheter og friheter ikke ivaretas.

#### 6.2.4 Forutsetninger for behandling av personopplysninger med utgangspunkt i datamodellen
Med utgangspunkt i at datamodellen legger til rette for en utlevering av personopplysninger, herunder helseopplysninger, som en behandling av en særlig kategori av personopplysninger, vil det forutsettes at behandlingen skjer i tråd med prinsipper for behandling av personopplysninger. Personvernkonsekvensene ved tap av personopplysninger eller utilsiktet tilgang vil være store, og behandlingen vil følgelig måtte innebære et særlig fokus på misbruk gjennom behandling av opplysningene til andre formål og helsepersonellets dokumenterte tjenstlige behov for tilgang til gitte helseopplysninger
 
## 7. Anerkjennelse av bidragsytere til spesifikasjonen
Teamet som har hatt ansvaret for denne spesifikasjonen har bestått av Morten Stensøy (HNIKT), Richard Husevåg (HSØ), Sverre Martin Jensen (Oslo Kommune), Erik Vegler Broen (Oslo Kommune - Origo), Simone Vandeberg (NHN), Steinar Noem (NHN).

Vi ønsker å takke Michal Cermak, Trond Elde, Eva Tone Fosse, Helge Bjertnæs, Øyvind Kvennås for verdifulle bidrag i utviklingen av spesifikasjonen.

## 8. Eksempler på bruk av datamodell


#### Eksempel #1 - Fastlege ber om tilgang til dokument
I dette eksempelet har en fastlege ...


##### JSON

```JSON
{
	"practicioner": {
		"pid":{
			"value": "xxxxxx34794",
			"oid_system": "2.16.578.1.12.4.1.4.1"
		},
		"professional_license": {
			"hpr_nr": "xxxxxxxxx",
			"oid": "xxxxxxxxxx"
		}
	},
	"care_relationship": {
		"functional_role": {
			"value": "2211",
			"system_oid": ""
		},
		"legal_entity": {
			"id": "921592761",
			"name": "Lege Leif Lagesen",
			"system_oid": "2.16.578.1.12.4.1.4.101"
		},
		"facility_type":{
			"value": "05",
			"system_oid": ""
		},
		"locality": "Helsehjelpgata 1 0001 Valderborg",
		"purpose_of_use": {
			"value": "TREAT",
			"system_oid": ""
		}
	},
	"patient": {
		"value": "xxxxxx95164",
		"oid_system": "2.16.578.1.12.4.1.4.1"
	}
}
```

##### SAML

#### Eksempel #2 - Ansatt i kommune ber om tilgang til dokument

I dette eksempelet har...

##### JSON
Har ikke klinisk spesialitet, har ikke HPR autorisasjon eller lisens

```JSON
{
	"practicioner": {
		"pid":{
			"value": "xxxxxx34794",
			"oid": "2.16.578.1.12.4.1.4.1"
		},
	},
	"care_relationship": {
		"functional_role": {
			"code": "2226",
			"oid": ""
		},
		"legal_entity": {
			"id": "921592761",
			"name": "Helsearbeider Helge Helsefyr",
			"oid": "2.16.578.1.12.4.1.4.101"
		},
		"point_of_care": {
			"id": "123456789",
			"point_of_care_name": "Det beste sykehjemmet i landet",
			"oid": "2.16.578.1.12.4.1.4.101"
		},
		"facility_type":{
			"code": "KP02",
			"oid": "8663"
		},
		"locality": "Helsehjelpgata 4 0001 Valderborg",
		"purpose_of_use": {
			"code": "COC",
			"oid": "urn:oid:2.16.840.1.113883.1.11.20448"
		}
	},
	"patient": {
		"value": "xxxxxx95164",
		"oid": "2.16.578.1.12.4.1.4.1"
	}
}
```

##### SAML

#### Eksempel #3 - HP i foretak ber om tilgang til dokument
##### JSON
##### SAML

#### Eksempel #4 - Legesekretær ber om tilgang til dokument på vegne av lege
##### JSON
##### SAML

## 9. Normative referanser 

Normative referanser spesifiserer dokumenter som må leses for å forstå eller implementere datamodellen, eller teknologi som må være på plass for å kunne implementere teknologien. 

* Styrk-08
* SNOMED-CT
* ASTM
* Volven
* Enhetsregisteret
* Folkeregisteret
* Helsepersonellregisteret