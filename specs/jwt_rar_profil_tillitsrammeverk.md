# Spesifikasjon for å beskrive grunnlaget for tilgang til helseopplysninger via HelseID

## Sammendrag
Denne spesifikasjonen definerer et JSON-element med en tilhørende struktur som skal brukes for å formidle informasjon om helsepersonell ved bruk av protokollene OpenID Connect og OAuth 2.0. Tiltroen til informasjonen som ligger i JSON elementet i bygger på Tillitsrammeverket for deling av helseopplysninger i Helsenettet.

Dokumentet er ment å brukes sammen med andre spesifikasjoner, som for eksempel «Spesifikasjon for bruk av HelseID for tilgang til journaldokumenter i Kjernejournal» [lenke]

## Dokumentets status

| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| 0.1 | Utkast | 31.02.2023 |

Spesifikasjonen vil bli versjonert for å støtte endringer over tid.

## Innholdsfortegnelse
1. [Innledning](#1-innledning)
2. [JSON-strukturer](#2-json-strukturer)
3. [Spesifikasjon av strukturen i «nhn:trust_framework:parameters»-elementet](#3-spesifikasjon-av-strukturen-i-«nhntrust_frameworkparameters»-elementet)
4. [Claims som beskriver parametre for bruk av tillitsrammeverket](#4-claims-som-beskriver-parametre-for-bruk-av-tillitsrammeverket)
5. [Sikkerhets- og personvernhensyn](#5-sikkerhets--og-personvernshensyn)

## 1. Innledning
Å lage et tydelig skille mellom informasjon som inngår i tillitsrammeverket og informasjon som ligger utenfor tillitsrammeverket forhindrer at aktørene i samhandlingen benytter informasjon som ikke inngår i tillitsrammeverket til tilgangsstyring og dokumentasjon.

Norsk Helsenett har derfor spesifisert en JWT-struktur som er tilpasset behovene i forbindelse med deling av helseopplysninger. Strukturen skal inneholde nødvendig informasjon for å tilfredsstille sikkerhetsmessige og lovpålagte krav knyttet til tilgangskontroll, logging og pasientens behov for informasjon om tilganger som er gitt til deres helseopplysninger.

Denne strukturen skal benyttes ved forespørsel til HelseID. Informasjonen fra strukturen brukes som grunnlag for innhold i Access Tokens, som igjen kan brukes til å få tilgang til helseopplysninger. 
 

## 2. JSON-strukturer
Spesifikasjonen definerer en JSON-struktur som skal benyttes for å beskrive grunnlaget for tilgang til helseopplysninger. Attributter i JSON-strukturen som inneholder informasjon kalles "claims" (påstander).

### Claims i spesifikasjonen
Et claim er et navn/verdi-par, hvor verdien kan være en datatype eller et objekt. Et objekt kan enten være en JSON-struktur eller et JSON-array.

````JSON
Datatype:
"tekstverdi": "Tekst"
"tallverdi": 1234

Vi benytter "_" for å skille mellom ord i navngivingen av claims.

Objekt:
"claim_navn": { 
	"claim_navn2": "claim-verdi2"
},
"claim_navn": [ "element1", "element2" ]
````

#### Fleksibilitet i JSON-strukturen
Spesifikasjonen legger opp til dynamikk med tanke på hvordan informasjonen uttrykkes. Dette lar oss uttrykke metainformasjon om påstandene i en mer konsis form:

````JSON
"claim_name": {
	"claim1": "verdi",
	"claim2": "metainformasjon"
	"claim3": "metainformasjon"
}
````

#### Kodeverk
Mange av verdiene i informasjons- og datamodellen vil være basert på gyldige verdier angitt av kodeverk. Eksempelet under viser en struktur for hvordan verdier basert på kodeverk skal struktureres:

````JSON
"claim_name": {
	"code": "1234",
	"system": "oid:x.x.x.x.x.x.x.x.x.x",

````

## 3. Spesifikasjon av strukturen i «nhn:trust_framework:parameters»-elementet

Ved forespørsel til HelseID for å få tilgang til helseopplysninger, er det nødvendig å sende inn en struktur som inneholder informasjon som beskrevet i [datamodellen](https://lenke_her)


### 3.1 JSON-strukturen som beskriver parametrene for Tillitsrammeverket

Dette elemenetet inneholder 3 claims som beskrevet under:

| Claim type | Beskrivelse |
| --- | --- | 
| `type` | Verdi som angir at elementet beskriver tillitsrammeverket. Verdien må være satt som  `nhn:trust_framework:parameters` | 
| `version` | Verdi som angir versjon av tillitrammeverk. Kan utelates; i så fall vil versjonen settes til `1.0`. | 
| `value` | En struktur som inneholder informasjon om helsepersonellet og helsepersonellets relasjon til pasienten | 

````JSON
{
	"type": "nhn:trust_framework:parameters",
	"version": "0.1",
	"value": {…}
}
````


### 3.2	Spesifikasjon av strukturen i «value»-elementet
`value`-elementet er et enkeltstående objekt som består av to attributter med underliggende strukturer.


| Claim type | Beskrivelse |
| --- | --- | 
| `practitioner` | Informasjon om helsepersonellet<br><br> Kilde: HPR, Konsument (klient/IdP) |
| `care_relationship` | Informasjon om helsepersonellets relasjon til pasienten |

_*Eksempel på JSON strukturen:*_
````JSON
{
	"practicioner":{
		…
	},
	"care_relationship": {
		…	
	}
}
````

#### Spesifikasjon av «practitioner»- og «care_relationship»-elementene

> (*) JSON-strukturen som inneholder "practitioner" og "care_relationship" elementene  hoveddelen av denne strukturen er beskrevet i spesifikasjonen [Informasjons- og datamodell for beskrivelse av tilgangssgrunnlaget ved deling av helseopplysninger](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/informasjons_og_datamodell.md), hvor JSON strukturen for denne informasjonen er definert. 

Semantikken for elementene `practitioner` og `care_relationship` er beskrevt i spesifikasjonen av [informasjons- og datamodell](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/informasjons_og_datamodell.md), og vil ikke beskrives i detalj i denne spesifikasjonen.


## 4. Claims som beskriver parametre for bruk av Tillitsrammeverket

JSON-dokumentet under beskriver hvordan en struktur som gjør bruk av Tillitsrammeverket kan se ut. Vær oppmerksom på at en slik struktur som regel vil være kombinert med en annen struktur som beskriver API-spesifikke claims; ett eksempel på dette kan være parametre for dokumentdeling.

````JSON
"authorization_details":[
	{
		"type": "nhn:trust_framework:parameters",
		"version": "0.1",
		"value": {
			"practicioner": {
				"professional_license": {
					"hpr_nr": "9144900",
					"authorization": "LE",
				},
			}
			"care_relationship": {
				"legal_entity": {
					"id": "993467049",
					"name": "OSLO UNIVERSITETSSYKEHUS HF",
				},
				"point_of_care": {
					"id": "974589095",
					"name": "OSLO UNIVERSITETSSYKEHUS HF ULLEVÅL - SOMATIKK",
				}
			}
		}
	},
	{
		…
		// API-spesifikke claims kan opprettes her, for eksempel parametre for Dokumentdeling
	}
]
````
### 4.1 Overføring av «authorization_details»-strukturen

*Dette er en oppsummering, detaljene beskrives i dokumentet [Profil for bruk av OpenID Connect og OAuth 2.0 i HelseID ved deling av dokumenter i Kjernejournal](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/bruk_av_oidc.md).*

Strukturen `authorization_details` som er beskrevet ovenfor, overføres til HelseID i en forespørsel om tilgang til tjenester eller API-er som deler helseopplysninger. Den danner grunnlaget for tilgangen som blir gitt i HelseID.
 
Strukturen kan inngå som parameter i forespørsler til både authorize-endepunktet og token-endepunktet. Se [Profil for bruk av OpenID Connect og OAuth 2.0 i HelseID ved deling av dokumenter i Kjernejournal](https://github.com/NorskHelsenett/Tillitsrammeverk/blob/main/specs/bruk_av_oidc.md) for en detaljert beskrivelse av hvordan HelseID skal brukes.

#### Via authorization-endepunktet - authorization_details i Request Objects
Når `authorization_details`-strukturen overføres som parameter i authorization-endepunktet MÅ den inngå som parameter i et Request Object, som beskrevet i [OpenID Connect spesifikasjonen](https://openid.net/specs/openid-connect-core-1_0.html#JWTRequests) og iht [gjeldende krav til bruk av Request Object i HelseID](https://lenke.no).

#### I token-endepunktet - authorization_details i client_assertion
Når `authorization_details`-strukturen overføres som parameter i token-endepunktet MÅ den inngå som parameter i Client Assertion, som beskrevet i [OAuth Assertion Framework](https://www.rfc-editor.org/rfc/rfc7521) iht [gjeldende krav til klientautentisering i HelseID](https://lenke.no).


## 5. Sikkerhets- og personvernshensyn

Se eget dokument. <!--- lenke -->