# JWT profil for å beskrive grunnlaget for tilgang til helseopplysninger innad i Helsenettet

## 1. Introduksjon
Norsk Helsenett har spesifisert en JWT struktur for å gi aktører som benytter HelseID nødvendig informasjon for å tilfredsstille sikkerhetsmessige og lovpålagte krav til tilgangskontroll ved deling av helseopplysninger via API.  

Denne strukturen skal benyttes i ID Tokens og Access Tokens som utstedes av HelseID, men skal også benyttes for å strukturere userinfo endepunktet i HelseID. 

Informasjonen som kreves for tilgangskontroll og dokumentasjon av tilgang til helseopplysninger er i dag ikke standardisert, og krever en annen representasjon enn den som finnes i de standardiserte spesifikasjonene og profilene som er tilgjengelige i dag. 

## 2. Spesifikasjonens struktur
* Claims
  * Claim navn
  * Objekt eller Array (verdien for et claim kan være enkeltstående eller array) 
  * Obligatorisk (valgfri eller påkrevd) 
  * Beskrivelse
  * Informasjonskilder 
  

Generiske strukturer 
* Virksomhet
* Legger opp til fleksibilitet (identifikator, system, navn) 
* Eksempel: "legal_entity" 


## 3. Spesifikasjon av strukturen i "Trusted Claims" elementet
Denne spesifikasjonen definerer et JSON element som brukes for å formidle informasjon om helsepersonell. Tiltroen til denne informasjonen bygger på tillitsrammeverket for deling av helseopplysninger i Helsenettet. 

Å lage et tydelig skille mellom informasjon som inngår i tillitsrammeverket og informasjon som ligger utenfor tillitsrammeverket forhindrer at aktørene i samhandlingen benytter informasjon som ikke inngår i tillitsrammeverket til tilgangsstyring og dokumentasjon. 

Elementet "trusted_claims" utgjør toppnivået for innholdet som beskriver grunnlaget for utlevering av helseopplysninger. Elementet er et enkeltstående objekt som består av to claims med underliggende strukturer: 

| | |
| --- | ---| 
| trust_framework | Informasjon om tillitsrammeverket som beskriver tilliten man kan ha til påstandene i "claims" objektet. |
| "claims" | Påstander hvor tilliten er basert på det angitte tillitsrammeverket |

De underliggende elementene som blir spesifisert videre i dette dokumentet deles opp i egne spesifikasjoner som skal benyttes for å beskrive formålet ved utlevering/deling av helseopplysninger.

## 4. Spesifikasjon av strukturen i elementet "trust_framework"
Denne strukturen beskriver tillitsrammeverket som ligger til grunn for tilliten som mottakeren kan ha til informasjonen som ligger i "claims" strukturen. Elementet "trust_framework" er et enkeltstående objekt som består av to underliggende strukturer.

| Claim type | Verdi | Påkrevd |
| --- | --- | --- |
| Version | Verdi som angir versjon av tillitrammeverk | Ja |
| Agreement | Struktur som beskriver hvilken avtale/kontrakt som ligger til grunn for tillitsforholdet. <br>Kilde: NHN MIN/Tillitsanker| Ja |

### 4.1	Spesifikasjon av "version" elementet
"Version" elementet har en tekstlig verdi som angir hvilken versjon av tillitsrammeverket som var i bruk når strukturen ble opprettet. Strukturen er ment å kunne støtte flere samtidige tillitsrammeverk. 
NHN vedlikeholder en liste over gyldige verdier for elementet "version" og hvilket tillitsrammeverk verdien peker på.

> "trust_framework":{<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"version": "nhn_high",<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8< … >8<br>
}

### 4.2	Spesifikasjon av "Agreement" strukturen
"Agreement" elementet er ett enkeltstående objekt som inneholder en JSON struktur som inneholder informasjon om vilkårene for bruk av tjenesten. Tilliten som mottakeren har til informasjonen i "claims" elementet hviler på denne avtalen.

| Claim | Verdi | Påkrevd |
| --- | --- | -- |
| Version | Versjonsnummer for avtalen | Ja |
| Legal_entity | Informasjon om den juridiske enheten som inngikk avtale/aksepterte vilkår |Ja | 
| Date | Dato når vilkår ble akseptert/inngått avtale | Ja |
| Agreement_id | Løpenummer for den aktuelle avtalen/identifikator | Ja |
| Granting_body | Informasjon om den juridiske enheten som det ble inngått avtale med | Ja |


### 4.3	Spesifikasjon av strukturen i Claims elementet
Claims elementet inneholder informasjonen om helsepersonellet som beskriver grunnlaget for tilgangen til helseopplysninger.

Claims elementet er ett enkeltstående objekt som består av to claims med underliggende strukturer.

| Claim | Beskrivelse |
| --- | --- |
| "practitioner" | Informasjon om helsepersonellet<br><br> Kilde: HPR, Konsument (klient/IdP) |
| "care_relationship" | Informasjon om helsepersonellets relasjon til pasienten |
| "system" | Informasjon om systemet som ber om tilgang til et API på vegne av helsepersonellet <br><br>Kilde: Konsument eller Databehandler – må være forhåndsregistrert i NHN sin database | 


#### 4.3.1 Spesifikasjon av practitioner strukturen

Denne strukturen benyttes til å beskrive grunnlaget for tilgangen til helseopplysningene.

##### Eksempel på practitioner object uten verdier
{
    "practitioner": {
        "professional_licence":{ [object] }, 
        "role": { [object] },
        "site_of_care":{ [object] },
        "purpose": { [object] }
    }
}

##### Spesifikasjon av claims i practitioners strukturen
| Claim | Beskrivelse |
| --- | --- |
| "pid" | Fødselsenummer fra folkeregisteret |
| "name" | Fullt navnt |
| "professional_license" | Informasjon om helsepersonellets autorisasjon eller lisens.<br>Kilde: HPR |

### 4.2.1 Spesifikasjon av "care_relationship" strukturen


### 4.3.1 Spesifikasjon av System


{
    "system":{
        "system_identifier": "[value]",
        "software_identifier": "[value]",
        "software_name": "[value]",
        "operated_by": {[object]}
}


| Claim | Beskrivelse |
| --- | --- |
| "system_identifier" | Identifikator som unikt identifiserer det kjørende systemet som helsepersonellet benytter innad i føderasjonen |
| "software_identifier" | Identifikator som unikt identifiserer programvaren som det kjørende systemet benytter innad i føderasjonen |
| "software_name" | Navn på programvare som det kjørende systemet benytter innad i føderasjonen |
| "operated_by" | Struktur som beskriver hvilken virksomhet som har det operative ansvaret for systemet (databehandler). |
| "on_authority_of" | Dersom virksomheten er en databehandler som har fått det operative ansvaret for systemet fra en helsevirksomhet blir dette beskrevet i denne strukturen |