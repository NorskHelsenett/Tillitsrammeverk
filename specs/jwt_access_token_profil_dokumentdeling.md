# JWT profil for å beskrive grunnlaget for tilgang til journaldokumenter i Kjernejournal

## Sammendrag
Denne spesifikasjonen definerer access token.... ved bruk av protokollene OpenID Connect og OAuth 2.0.


## Dokumentets status

| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| -0 | Utkast | xx.xx.2023 |

Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til tillitsrammeverk for deling av helseopplysninger i helse- og omsorgssektoren. Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i tillitsrammeverket.

Spesifikasjonen skal versjoneres for å støtte endringer over tid.

## Innholdsfortegnelse

## 1. Introduksjon
bla bla bla 

## 2. Spesifikasjonens struktur
Bla bla bla


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



# API Spesifikke claims

````JSON
{
    8<.. JSON ..>8
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