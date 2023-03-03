# Informasjons- og datamodell for beskrivelse av tilgangssgrunnlaget ved deling av helseopplysninger
Versjon: 0.1

Dato: 31.01.2023

## Sammendrag
Denne spesifikasjonen definerer en informasjons- og datamodell som skal brukes for å uttrykke et helsepersonells grunnlag for tilgang til helseopplysninger ved deling av helseopplysninger på tvers av helsevirksomheter i helse- og omsorgssektoren i Norge.


## Dokumentets status
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
    Helsepersonell o-- Autorisasjoner
	Helsepersonell --* Behandlerrelasjon
	Behandlerrelasjon --* Pasient
    class Autorisasjoner{
	    +Object Autorisasjoner
    }
    class Helsepersonell{
	    +Object Identitet
	    +Autorisasjoner Autorisasjoner
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
	Behandlerrelasjon -- Pasient
	Helsepersonell o-- FormalAuthorization
	Helsepersonell o-- IdentityAttribute
	Behandlerrelasjon o-- IdentityAttribute
	Behandlerrelasjon o-- Organization
	Behandlerrelasjon o-- PurposeOfUse
	FormalAuthorization o-- Authorization
	FormalAuthorization o-- Licence
	Organization o-- LegalEntity
	Organization o-- IdentityAttribute
	PurposeOfUse --|> IdentityAttribute


	
	class Helsepersonell{
		+IdentityAttribute name
		+IdentityAttribute pid
		+FormalAuthorization professional_licence
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
	class Authorization{
	}
	
	class Licence{
	}
	
	class FormalAuthorization{
		+String hpr_nr
		+List<Authorization> authorizations
		+List<Licence> licences
	}
		
```

#### 3.2.3 Oppsummering av påkrevd eller valgfri informasjon
Ikke all informasjon i datamodellen er relevant, noen informasjonselementer er valgfrie.

Vi har lagt vekt på å ivareta sporbarheten i delingssammenheng, derfor har vi angitt at alle identifikatorer er påkrevd, dette gjelder både fysiske og juridiske personer.

| Informasjon | Beskrivelse | Informasjonskilde | Påkrevd |
| --- | --- | --- | --- |
| "pid" | Fødselsnummer fra folkeregisteret | HelseID | **Ja** |
| "hpr_nr" | Helsepersonellets HPR-nummer, dersom det finnes | HelseID | **Nei** |
| "authorization" | Helsepersonellets autorissjoner, dersom de finnes | HelseID | **Nei** |
| "licence" | Helsepersonellets lisenser, dersom de finnes | HelseID | **Nei** |
| "functional_role" | Helsepersonellets funksjonelle rolle hos virksomheten | Konsumentens EPJ | **Ja** |
| "clinical_speciality" | Helsepersonellets kliniske spesialitet | Konsumentens EPJ | **Nei** |
| "legal_entity_id" | Den dataansvarlige virksomhetens org.nr | Konsumentens EPJ | **Ja** |
| "legal_entity_name" | Den dataansvarlige virksomhetens navn | Konsumentens EPJ | **Ja** |
| "point_of_care_id" | Behandlingsstedets org.nr., dersom det er relevant | Konsumentens EPJ | **Nei** |
| "point_of_care_name" | Behandlingsstedets navn, dersom det er relevant | Konsumentens EPJ | **Nei** |
| "facility_type" | Helsetjenestetyper som leveres ved virksomheten | Konsumentens EPJ | **Ja** |
| "locality" | Avdeling/org.enhet hvor helsepersonellet yter helsehjelp | Konsumentens EPJ | **Ja** |
| "purpose_of_use" | Helsepersonellets formåle med helseopplysningene (til hva de skal brukes) | Konsumentens EPJ | **Ja** |
| "patient_id" | Unik identifikator for pasienten | Konsumentens EPJ | **Ja** |

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
 
|   |   |
| ---| ---|
| Attributt: | "hpr_nr" |
| Informasjonselement | Unik identifikator for helsepersonellet knyttet opp til formelle autorisasjoner eller lisenser |
| Attributt EHDSI: | N/A (?) |
| Obligatorisk: | **Nei** |
| Data type: | String |
| Autoritativ kilde: | Helsepersonellregisteret - Helsedirektoratet |
| Informasjonskilde: | HelseID, basert på oppslag mot HPR etter vellykket pålogging av helsepersonell. |
| Kodeverk: | 2.16.578.1.12.4.1.4.4 |

###### Helsepersonellets autorisasjoner og lisenser
Attributtene "authorization" og "licence" brukes for å beskrive autorisasjoner og lisenser som Helsepersonellet har fått tildelt av statens autorisasjonskontor for helsepersonell.

|   |   |
| ---| ---|
| Informasjonselement | Beskriver helsepersonellets autorisasjoner og/eller lisenser |
| Attributter: | "authorization"<br/>"licence" |
| Attributt EHDSI: | N/A |
| Obligatorisk: | **Nei** |
| Data type: | Object | 
| Autoritativ kilde: | Helsepersonellregisteret - Helsedirektoratet |
| Informasjonskilde: | HelseID, basert på oppslag mot HPR etter vellykket pålogging av helsepersonell |

###### Helsepersonellregister - Attributter SAML format

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
	"authorization": {[...]},
	"licence": {[...]},
	"oid": "xx.xx.xx.xx"
}
````  


#### 3.2.6 Kategori: Behandlerrelasjon
Helsepersonellets behandlerrelasjon til pasientent angis ved hans rolle, spesialitet, virksomhet hvor han yter helsehjelp, behandlingssted, helsetjenestetype og en angivelse av formålet med behandlingen av helseopplysningene.

##### 3.2.6.1 Helsepersonellets funksjonelle rolle
Attributtet "functional_role" representerer helsepersonellets rolle hos virksomheten i hans behandling av pasienten, og angis av kode fra STYRK-08.

|   |   |
| ---| ---|
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
Attributtet "legal_entity_id" og "legal_entity_name" identifiserer virksomheten hvor helsepersonellet yter helsehjelp.

|   |   |
| ---| ---|
| Informasjonselement | Virksomheten (hovedenhet) hvor helsepersonellet yter helsehjelp |
| Attributt: | "legal_entity_id"<br/>"legal_entity_name" |
| Attributt EHDSI: | "urn:oasis:names:tc:xspa:1.0:subject:organization"<br/>"urn:oasis:names:tc:xspa:1.0:subject:organization-id" |
| Obligatorisk: | Ja |
| Data type: | String |
| Autoritativ kilde: | Enhetsregisteret - SSB |
| Informasjonskilde: | Konsument (HelseID + Altinn) |
| Kodeverk: | (kode for enhetsregisteret)|


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
	"oid": "x.x.x.x.x.x"
}
```` 

##### Behandlingssted

Attributtet "point_of_care_id" og "point_of_care_name" identifiserer behandlingsstedet hvor helsepersonellet yter helsehjelp.

|   |   |
| ---| ---|
| Informasjonselement | Virksomheten (underenhet) hvor helsepersonellet yter helsehjelp |
| Attributt: | "point_of_care_id"<br/>"point_of_care_name" |
| Attributt EHDSI: | N/A |
| Obligatorisk: | **Nei** |
| Data type: | String |
| Autoritativ kilde: | Enhetsregisteret - SSB |
| Informasjonskilde: | Konsument (HelseID + Altinn) |
| Kodeverk: | (kode for enhetsregisteret) |

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
	"system_oid": ""
}
````


##### Helsetjenestetype
Attributtet "facility_type" angir hvilken type helsetjenester som leveres ved virksomheten som helsepersonellet jobber for.

|   |   |
| ---| ---|
| Informasjonselement | Hvilken type helsetjenester som leveres ved virksomheten hvor helsepersonellet yter helsehjelp |
| Attributt: | "facility_type" |
| Attributt EHDSI: | "urn:ehdsi:names:subject:healthcare-facility-type" |
| Obligatorisk: | **Ja** |
| Data type: | string |
| Autoritativ kilde: | Konsument |
| Informasjonskilde: | Konsumentens EPJ |
| Kodeverk: | eHealth DSI code list<br/> Volven<br/>  |
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
			"oid": "2.16.578.1.12.4.1.4.1"
		},
		"professional_license": {
			"hpr_nr": "xxxxxxxxx",
			"authorization": {[...]},
			"licence": {[...]}
		}
	},
	"care_relationship": {
		"functional_role": {
			"code": "2211",
			"oid": ""
		},
		"clinical_speciality": {
			"value": "419772000",
			"oid": ""
		},
		"legal_entity": {
			"id": "921592761",
			"name": "Lege Leif Lagesen",
			"oid": ""
		},
		"point_of_care": {
			"id": "123456789",
			"name": "Det beste legekontoret i byen AS",
			"oid": ""
		},
		"facility_type":{
			"text": "helsetjenestetype",
			"value": "05",
			"oid": ""
		}
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
#### 6.2.1 Lekkasje av sensitive personopplysninger
Datamodellen vil bli benyttet til å overføre sensitive personopplysninger om helsepersonellet og helsepersonellets relasjon til sin pasient. Ved å utnytte svakheter og sårbarheter i programvare kan kan en angriper observere sensitiv personinformasjon som overføres mellom de tekniske tjenestene som benyttes ved deling av helseopplysninger. 
Lekkasje av PII kan oppstå mellom flere parter i verdikjeden:
* mellom konsument og autorisasjonsserver/IdP
* mellom konsument og informasjonstjeneste
* mellom informasjonstjeneste og datagrensesnitt

For å sikre oss mot potensiell lekkasje av PII bør det vurderes å innføre tiltak for å ivareta konfidensialiteten.

#### 6.2.2 Mangelfull informasjon om personvernskonsevenser
Det er en risiko for at både pasienten og helsepersonellet mottar mangelfull informasjon om potensielle personvernskonsekvenser ved overføringen av personopplysningene.

#### 6.2.3 Misbruk av data
Datamodellen beskriver behandlerrelasjonen som helsepersonellet har til sin pasient, og kan være sensitiv. Det er en risiko for at denne informasjonen misbrukes av en eller flere parter som mottar verdiene i datasettet.

#### 6.2.4 Overvåkning av ansatte i andre virksomheter
Datamodellen inneholder en del informasjon som beskriver helsepersonells arbeidsforhold. Denne informasjonen overføres til andre virksomheter enn den virksomheten den ansatte yter helsehjelp hos. Det er en risiko for at denne informasjonen kan benyttes for å overvåke helsepersonell i andre virksomheter.
	
#### 6.2.5 Urettmessig tilegnelse av helseopplysninger
Det er en risiko for at helsepersonellet som ber om tilgang til helseopplysninger ikke har et tjenstlig behov, og at opplysningene ikke er relevante og nødvendige i behandlingen av pasienten.
 
## 7. Anerkjennelse av bidragsytere til spesifikasjonen
Vi ønsker å takke kongen, fedrelandet og Ringnes, samt alle andre som har hatt innvirkning på spesifikasjonen..

Norsk Helsenett SF har hatt det overordnede ansvaret for å utvikle denne spesifikasjonen basert på viktige bidrag fra sektoren...

Vi ønsker å takk Erik Vegler Broen ved Oslo Kommune, Trond Elde ved DIPS, +++ for verdifulle bidrag i utviklingen av spesifikasjonen.

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
			"authorization": {[...]},
			"licence": {[...]}
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
			"system_oid": ""
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
			"oid": ""
		},
		"point_of_care": {
			"id": "123456789",
			"point_of_care_name": "Det beste sykehjemmet i landet",
			"oid": ""
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