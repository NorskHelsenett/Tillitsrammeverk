# JWT profil for å beskrive grunnlaget for tilgang til helseopplysninger innad i Helsenettet

## Sammendrag
Denne spesifikasjonen definerer et JSON element med en tilhørende struktur som skal brukes for å formidle informasjon om helsepersonell ved bruk av protokollene OpenID Connect og OAuth 2.0. Tiltroen til informasjonen som ligger i JSON elementet i bygger på tillitsrammeverket for deling av helseopplysninger i Helsenettet.


## Dokumentets status

| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| -0 | Utkast | 17.02.2023 |

Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til tillitsrammeverk for deling av helseopplysninger i helse- og omsorgssektoren. Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i tillitsrammeverket.

Spesifikasjonen skal versjoneres for å støtte endringer over tid.

## Innholdsfortegnelse

## 1. Introduksjon
Å lage et tydelig skille mellom informasjon som inngår i tillitsrammeverket og informasjon som ligger utenfor tillitsrammeverket forhindrer at aktørene i samhandlingen benytter informasjon som ikke inngår i tillitsrammeverket til tilgangsstyring og dokumentasjon.

Norsk Helsenett har derfor spesifisert en JWT struktur som er tilpasset behovene i forbindelse med deling av helseopplysninger. Strukturen skal inneholde nødvendig informasjon for å tilfredsstille sikkerhetsmessige og lovpålagte krav knyttet til tilgangskontroll, logging og pasientens behov for informasjon om tilganger som er gitt til hans helseopplysninger.

Denne strukturen skal benyttes i ID Tokens og Access Tokens som utstedes av HelseID, men kan også benyttes for å strukturere informasjon i userinfo endepunktet i HelseID. 
 

## 2. Spesifikasjonens struktur
Spesifikasjonen definerer en JSON struktur som skal benyttes for å beskrive grunnlaget for tilgang til helseopplysninger. Attributter i JSON strukturen som inneholder informasjon kalles "claims" (påstander).

Spesifikasjonen tar først for seg det øverste nivået i JSON strukturen, og tar deretter for seg de underliggende strukturene for hvert overordnede element.

### Claims i spesifikasjonen
Et claim er et navn-verdi par, hvor verdien kan være en datatype eller et objekt. Et objekt kan være en JSON-struktur eller et JSON-array.

````JSON
Datatype:
"tekstverdi": "Tekst"
"tallverdi": 1234

Vi benytter "_" for å skille mellom ord i navngivingen av claims.

Objekt:
"claim_navn": { "claim-navn2": "claim-verdi2"}
"claim_navn": ["element1", "element2"]
````



### Generiske strukturer 
#### Fleksibilitet i JSON strukturen
Spesifikasjonen legger opp til dynamikk i hvordan informasjonen uttrykkes. Dette lar oss uttrykke metainformasjon om påstandene i en mer konsis form.

````JSON
"claim_name": {
	"claim1": "verdi",
	"claim2": "metainformasjon"
	"claim3": "metainformasjon"
}
````


#### Elementer som beskriver virksomheter
Spesifikasjonen definerer flere claims som beskriver virksomheter. Disse attributtene følger samme struktur

````JSON
"juridisk_enhet": {
	"id": "1234",
	"name": "Virksomheten AS",
	"oid": "2.16.578.1.12.4.1.4.101"
}
````

#### Kodeverk
Mange av verdiene i informasjons- og datamodellen skal være basert på gyldige verdier angitt av kodeverk eller hvitelister. Denne spesifikasjonen definerer en struktur for hvordan verdier basert på kodeverk eller hvitelister skal struktureres.

````JSON
Eksempel på verdi basert på kodeverk:
"claim_name": {
	"code": "1234",
	"text": "",
	"oid_system": "x.x.x.x.x.x.x.x.x.x",


Eksempel på verdi basert på hviteliste:
"claim_name": {
	"code": "1234",
	"text": "",
	"classification_system": "egennavn"
}
````

## 3. Spesifikasjon av strukturen i "trusted_claims" elementet

Elementet "trusted_claims" utgjør toppnivået for innholdet som beskriver grunnlaget for utlevering av helseopplysninger. Elementet er et enkeltstående objekt som består av to claims med underliggende strukturer: 

| Claim type | Beskrivelse |
| --- | ---| 
| "trust_framework" | Informasjon om tillitsrammeverket som beskriver tilliten man kan ha til påstandene i "claims" objektet. |
| "claims" | Påstander hvor tilliten er basert på det angitte tillitsrammeverket |

````JSON
"trust_framework_claims":{
	"trust_framework": { ... },
	"claims": { ... }
}
````

De underliggende elementene som blir spesifisert videre i dette dokumentet deles opp i egne spesifikasjoner som skal benyttes for å beskrive formålet ved utlevering/deling av helseopplysninger.

### 3.1 Spesifikasjon av strukturen i elementet "trust_framework"
Denne strukturen beskriver tillitsrammeverket som ligger til grunn for tilliten som mottakeren kan ha til informasjonen som ligger i "claims" strukturen. Elementet "trust_framework" er et enkeltstående objekt som består av to underliggende strukturer.

| Claim type | Beskrivelse |
| --- | --- | 
| "framework" | Verdi som angir versjon av tillitrammeverk | 
| "agreement" | Struktur som beskriver hvilken avtale/kontrakt som ligger til grunn for tillitsforholdet. <br>Kilde: NHN MIN/Tillitsanker| 

````JSON
"trust_framework":{
    "framework": "eksempel",
	"agreement": {
		8<...>8
	}
}
````


#### 3.1.1 Spesifikasjon av elementet "framework"
"framework" elementet har en tekstlig verdi som angir hvilken versjon av tillitsrammeverket som var i bruk når strukturen ble opprettet av HelseID.

>"nhn_high" indikerer at tillitsrammeverket er tilpasset deling av helseopplysninger i behandlingsrettede helseregistre


````JSON
"trust_framework":{
	"framework": "nhn_high",
	8< … >8
}
````


#### 3.1.2 Spesifikasjon av strukturen "agreement"
Elementet "agreement" er ett enkeltstående objekt som inneholder informasjon om vilkårene for bruk av tjenesten. Objektet er en JSON struktur.
Tilliten som mottakeren har til informasjonen i "claims" elementet hviler på avtalen som "agreement" elementet refererer til.

| Claim | Verdi | 
| --- | --- | -- |
| "version" | Versjonsnummer for avtalen | 
| "legal_entity" | Informasjon om den juridiske enheten som inngikk avtale/aksepterte vilkår |
| "date" | Dato når vilkår ble akseptert/inngått avtale | 
| "id" | Løpenummer for den aktuelle avtalen/identifikator | 
| "granting_body" | Informasjon om den juridiske enheten som det ble inngått avtale med |

````JSON
"trust_framework":{
    8< .... >8
	"agreement": {
		"version": "1.0",
		"legal_entity": {
			"id": "123456789",
			"name": "Helsevirksomheten AS",
			"oid": "2.16.578.1.12.4.1.4.101"
		},
		"date": "14.02.2023",
		"id": "10001",
		"granting_body": {
			"id": "987654321",
			"name": "Norsk Helsenett SF",
			"oid": "2.16.578.1.12.4.1.4.101"
		}
	}
}
````

### 3.2	Spesifikasjon av strukturen i "claims" elementet
Claims elementet er ett enkeltstående objekt som består av fire attributter med underliggende strukturer.

Attributtene som ligger i "claims" elementet er:
* "practicioner"
* "care_relationship"
* "patient"
* "system"



| Claim | Beskrivelse |
| --- | --- |
| "practitioner" | Informasjon om helsepersonellet<br><br> Kilde: HPR, Konsument (klient/IdP) |
| "care_relationship" | Informasjon om helsepersonellets relasjon til pasienten |
| "patient" | Informasjon om pasienten |
| "system" | Informasjon om systemet som ber om tilgang til et API på vegne av helsepersonellet <br><br>Kilde: Konsument eller Databehandler – må være forhåndsregistrert i NHN sin database |

_*Eksempel på JSON strukturen:*_
````JSON
{
	"practicioner":{
		8<...>8
	},
	"care_relationship": {
		8<...>8	
	},
	"system": {
		8<...>8
	}
}
````

#### 4.3.1 Spesifikasjon av "practitioner", "care_relationship" og "patient" elementene

> (*) JSON strukturen som inneholder "practitioner", "care_relationship" og "patient" elementene  hoveddelen av denne strukturen er beskrevet i spesifikasjonen [Informasjons- og datamodell for beskrivelse av tilgangssgrunnlaget ved deling av helseopplysninger](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/informasjons_og_datamodell.md), hvor JSON strukturen for denne informasjonen er definert. 

Elementene "practitioner", "care_relationship" og "patient" er beskrevt i spesifikasjonen av [informasjons- og datamodell](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/informasjons_og_datamodell.md), og vil ikke beskrives i detalj i denne spesifikasjonen.



#### 4.3.4 Spesifikasjon av "system" elementet

| Claim | Beskrivelse |
| --- | --- |
| "system_identifier" | Identifikator som unikt identifiserer det kjørende systemet som helsepersonellet benytter innad i føderasjonen |
| "software_identifier" | Identifikator som unikt identifiserer programvaren som det kjørende systemet benytter innad i føderasjonen |
| "software_name" | Navn på programvare som det kjørende systemet benytter innad i føderasjonen |
| "operated_by" | Struktur som beskriver hvilken virksomhet som har det operative ansvaret for systemet (databehandler). |
| "on_authority_of" | Dersom virksomheten er en databehandler som har fått det operative ansvaret for systemet fra en helsevirksomhet blir dette beskrevet i denne strukturen |


##### Eksempel på "system" object uten verdier
````JSON
{
    "system":{
        "system_identifier": "[value]",
        "software_identifier": "[value]",
        "software_name": "[value]",
        "operated_by": {[object]}
}
````

# API Spesifikke claims

````JSON
{
	"authorization_details":{
		"type": "dokumentdeling_kj",
		"actions": ["read"],
		"locations": "https://kj.nhn.no/",
		"kj_dokumentdeling": { //rar-struktur for dokumentdeling: hva skal barnet hete?
			"version": "1.0",
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
				"decision_ref": { //TODO: vurdere hvorvidt dette attributtet skal inngå i helseindikator?
					"ref_id" : "[id til lokal tilgangsbeslutning som ekstern referanse for kilden]",
					"description": { 8<...>8 }, /* autogenerert i EPJ */
					"user_reason": "Tekst lagt inn av bruker.."
				}
			}
		}
	}
}
````


## 4. Sikkerhets- og personvernshensyn

### 4.1 Sikkerhetshensyn

#### 4.1.1 Tyveri og misbruk av tokens
>TODO: beskrivelse


#### 4.1.2 Manglende validering av Access Token hos tjenesten
>TODO: beskrivelse

#### 4.1.3 Feilkonfigurering av behandling av Access Token
>TODO: beskrivelse

### 4.2 Personvernshensyn
#### 4.2.1 Lekkasje av sensitive personopplysninger
Datamodellen vil bli benyttet til å overføre sensitive personopplysninger om helsepersonellet og helsepersonellets relasjon til sin pasient. Ved å utnytte svakheter og sårbarheter i programvare kan kan en angriper observere sensitiv personinformasjon som overføres mellom de tekniske tjenestene som benyttes ved deling av helseopplysninger. Lekkasje av PII kan oppstå mellom flere parter i verdikjeden:

mellom konsument og autorisasjonsserver/IdP
mellom konsument og informasjonstjeneste
mellom informasjonstjeneste og datagrensesnitt
For å sikre oss mot potensiell lekkasje av PII bør det vurderes å innføre tiltak for å ivareta konfidensialiteten.

#### 4.2.2 Mangelfull informasjon om personvernskonsevenser
Ettersom informasjon i Access Tokens kan bli lagret hos mange aktører og brukt til å informere pasitenten om tilgangen til pasientens helseopplysninger er det en risiko for at både pasienten og helsepersonellet mottar mangelfull informasjon om potensielle personvernskonsekvenser ved overføringen av personopplysningene.

#### 4.2.3 Misbruk av data
Datamodellen beskriver behandlerrelasjonen som helsepersonellet har til sin pasient, og kan være sensitiv. Det er en risiko for at denne informasjonen misbrukes av en eller flere parter som mottar verdiene i datasettet.

#### 4.2.4 Overvåkning av ansatte i andre virksomheter
Datamodellen inneholder en del informasjon som beskriver helsepersonells arbeidsforhold. Denne informasjonen overføres til andre virksomheter enn den virksomheten den ansatte yter helsehjelp hos. Det er en risiko for at denne informasjonen kan benyttes for å overvåke helsepersonell i andre virksomheter.

#### 4.2.5 Urettmessig tilegnelse av helseopplysninger
Det er en risiko for at helsepersonellet som ber om tilgang til helseopplysninger ikke har et tjenstlig behov, og at opplysningene ikke er relevante og nødvendige i behandlingen av pasienten.