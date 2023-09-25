# JWT profil for å beskrive grunnlaget for tilgang til journaldokumenter i Kjernejournal

TODO: beskriv hvordan dette dokumentet er knyttet til JWT-profilen for tillitsrammeverket

## Sammendrag
Denne spesifikasjonen definerer en struktur i et utlevert Access token som kan brukes til dokumentdeling via Kjernejournal, ved bruk av protokollene OpenID Connect og OAuth 2.0.


## Dokumentets status

| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| 0.1 | Utkast |26.05.2023 |

Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til dokumentdeling via Kjernejournal for deling av helseopplysninger i helse- og omsorgssektoren. Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i tillitsrammeverket.

Spesifikasjonen skal versjoneres for å støtte endringer over tid.

## Innholdsfortegnelse

## 1. Introduksjon
Norsk Helsenett har spesifisert en JWT-struktur som er tilpasset behovene knyttet til dokumentdeling via Kjernejournal. Strukturen skal inneholde nødvendig informasjon for å tilfredsstille sikkerhetsmessige og lovpålagte krav knyttet til tilgangskontroll, logging og pasientens behov for informasjon om tilganger som er gitt til deres helseopplysninger.

TODO: hva med userinfo-endepunktet?
Denne strukturen skal benyttes i ID Tokens og Access Tokens som utstedes av HelseID, men kan også benyttes for å strukturere informasjon i userinfo-endepunktet i HelseID.

## 2. Spesifikasjonens struktur
Spesifikasjonen definerer en JSON struktur som skal benyttes for å beskrive grunnlaget for tilgang til journaldokumenter via Kjernejournal. Attributter i JSON strukturen som inneholder informasjon kalles "claims" (påstander).

Spesifikasjonen tar først for seg det øverste nivået i JSON-strukturen, og tar deretter for seg de underliggende strukturene for hvert overordnede element.

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

#### Kodeverk
Mange av verdiene i informasjons- og datamodellen skal være basert på gyldige verdier angitt av kodeverk. Denne spesifikasjonen definerer en struktur for hvordan verdier basert på kodeverk skal struktureres.

````JSON
Eksempel på verdi basert på kodeverk:
"claim_name": {
	"code": "1234",
	"text": "",
	"oid_system": "x.x.x.x.x.x.x.x.x.x",
````

## 3. Spesifikasjon av strukturen i "trusted_claims" elementet

Elementet "trusted_claims" utgjør toppnivået for innholdet som beskriver grunnlaget for utlevering av helseopplysninger. Elementet er et enkeltstående objekt som består av to claims med underliggende strukturer: 

| Claim type | Beskrivelse |
| --- | ---| 
| "claims" | Påstander hvor tilliten er basert på det angitte tillitsrammeverket |

TODO: finn et godt navn!
````JSON
"authorization_details":{
	"type": "kj_dokumendeling",
	"actions": ["read_document", "read_documentlist"],
	"locations": ["kj.nhn.no"],
	"claim1": { ... },
	"claim2": { ... },
	"claim3: "",
}
````

De underliggende elementene som blir spesifisert videre i dette dokumentet deles opp i egne spesifikasjoner som skal benyttes for å beskrive formålet ved utlevering/deling av helseopplysninger.


TODO: PBR!!!
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

TODO: vurder nytten av dette!!

#### 4.2.1 Lekkasje av personopplysninger
Datamodellen vil bli benyttet til å overføre  personopplysninger om helsepersonellet. Ved å utnytte svakheter og sårbarheter i programvare kan kan en angriper observere personinformasjon som overføres mellom de tekniske tjenestene som benyttes ved deling av helseopplysninger. Lekkasje av PII (personlig identifserbar informasjon) kan oppstå mellom flere parter i verdikjeden:

mellom konsument og autorisasjonsserver/IdP
mellom konsument og informasjonstjeneste
mellom informasjonstjeneste og datagrensesnitt
For å sikre oss mot potensiell lekkasje av PII bør det vurderes å innføre tiltak for å ivareta konfidensialiteten.

#### 4.2.2 Urettmessig tilegnelse av helseopplysninger
Det er en risiko for at helsepersonellet som ber om tilgang til helseopplysninger ikke har et tjenstlig behov, og at opplysningene ikke er relevante og nødvendige i behandlingen av pasienten.