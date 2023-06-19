# Spesifikasjon for bruk av HelseID for tilgang til journaldokumenter i Kjernejournal

| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| 0.1 | Utkast | 2.06.2023 |
| 0.2| Utkast til sektoren | 19.06.2023 |

Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til dokumentdeling via Kjernejournal for deling av helseopplysninger i helse- og omsorgssektoren. Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i Tillitsrammeverket.

Dokumentet er ment for bruk sammen med dokumentet «Spesifikasjon for å beskrive grunnlaget for tilgang til helseopplysninger via HelseID». [lenke]

Spesifikasjonen vil bli versjonert for å støtte endringer over tid.


## Definisjon av begrep og forkortelser
TODO: lenker
Spesifikasjonen benytter begreper og terminologi som er definert i følgende spesifikasjoner: [@!RFC6749], [@!RFC6750], [@!RFC7636], [@!OIDC] og ISO29100.

## Innholdsfortegnelse
1. [Innledning](#1-innledning)
2. [Spesifikasjon](#2-spesifikasjon-av-strukturen-i-«nhndokumentdelingparameters»-elementet)
3. [JSON-struktur](#3-json-struktur)


## 1. Innledning
Denne spesifikasjonen definerer et JSON-format som skal benyttes til å overføre informasjon om grunnlaget for tilgangen som er gitt i helsepersonellets lokale EPJ-system til den som deler helseopplysningene. 

Denne spesifikasjonen er en del av et spesifikasjonssett som baserer seg på tillitsrammeverket for deling av helseopplysninger på tvers av helsevirksomheter i helse- og omsorgssektoren, og må sees i sammenheng med de andre spesifikasjonene.

## 2. Spesifikasjon av strukturen i «nhn:dokumentdeling:parameters»-elementet

Ved forespørsel til HelseID for å få tilgang til helseopplysninger, er det nødvendig å sende inn en struktur som inneholder informasjon som beskrevet i [datamodellen for oppslag i pasientens journaldokumenter](datamodell_dokumentdeling.md).


### 2.1 JSON-strukturen som beskriver parametrene for Dokumentdeling

Dette elemenetet inneholder claims som beskrevet under:

| Claim type | Beskrivelse | Obligatorisk |
| --- | --- | --- |
| `type` | Verdi som angir at elementet beskriver tillitsrammeverket. Verdien må være satt som  `nhn:dokumentdeling:parameters` | **Ja** |
| `version` | Verdi som angir versjon av tillitrammeverk. Kan utelates; i så fall vil versjonen settes til `1.0`. |  **Nei** |
| `healthcare_service` | Helsetjenestetyper som leveres ved virksomheten. </br> Parametre: `code` og `system`</br>Kodeverk: <br/>urn:oid:2.16.578.1.12.4.1.1.8627 – [Tjenestetyper innen spesialisthelsetjenesten](https://volven.no/produkt.asp?open_f=true&id=495806&catID=3&subID=8&subCat=163&oid=8627)<br/>urn:oid:2.16.578.1.12.4.1.1.8662 – [Fylkeskommunale tjenestetyper](https://volven.no/produkt.asp?open_f=true&id=496298&catID=3&subID=8&subCat=163&oid=8662)<br/>urn:oid:2.16.578.1.12.4.1.1.8663 – [Tjenestetyper for kommunal helse- og omsorgstjeneste mv](https://volven.no/produkt.asp?open_f=true&id=496326&catID=3&subID=8&subCat=163&oid=8663)<br/>urn:oid:2.16.578.1.12.4.1.1.8664 – [Tjenestetyper for apotek og bandasjister](https://volven.no/produkt.asp?open_f=true&id=496327&catID=3&subID=8&subCat=163&oid=8664)<br/>urn:oid:2.16.578.1.12.4.1.1.8666 – [Felles tjenestetyper](https://volven.no/produkt.asp?open_f=true&id=496328&catID=3&subID=8&subCat=163&oid=8666)<br/>urn:oid:2.16.578.1.12.4.1.1.8668 – [Tjenestetyper for spesialisthelsetjenesten](https://volven.no/produkt.asp?open_f=true&id=496329&catID=3&subID=8&subCat=163&oid=8668)| **Ja** |
| `purpose_of_use` | Helsepersonellets formål med helseopplysningene (til hva de skal brukes) </br>Parametre: `code` og `system`</br>Kodeverk: urn:oid:2.16.840.1.113883.1.11.20448 - [HL7](https://terminology.hl7.org/ValueSet-v3-PurposeOfUse.html) | **Ja** |
| `purpose_of_use_details` | Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes) </br>Parametre: `code` og `system`</br>Kodeverk:</br>Kommune: urn:oid:2.16.578.1.12.4.1.1.9151 - [volven](https://volven.no/produkt.asp?open_f=true&id=494341&catID=3&subID=8&subCat=140&oid=9151)<br/>Spesialisthelsetjenesten: urn:AuditEventHL7Norway/CodeSystem/carerelation – [HL7 Norway](https://hl7norway.github.io/AuditEvent/currentbuild/CodeSystem-carerelation.html) | **Ja** |
| `tracing_ref` | Parameter: `ref_id`</br> Referanse til opprinnelsen av forespørsel  | **Ja** |

````JSON
{
    "type": "nhn:dokumentdeling:parameters",
    "version": "0.1",
    "healthcare_service": {
        {…}
    },
    "purpose_of_use": {
        {…}
    },
    "purpose_of_use_details": {
        {…}
    },
    "tracing_ref": {
        {…}
    }	
}
````

### 3 JSON-Struktur

Under vises en JSON-struktur som inneholder både dokumentdeling-strukturen, strukturen for attributter for Tillitsrammeverket og andre elementer som er relevant for HelseID.

```JSON
"authorization_details":[
    {
        "type": "nhn:trust_framework:parameters",
        "version": "0.1",
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
                "system": "oid:2.16.578.1.12.4.1.4.101"                
            },
            "point_of_care": {
                "id": "974589095",
                "name": "OSLO UNIVERSITETSSYKEHUS HF ULLEVÅL - SOMATIKK",
                "system": "oid:2.16.578.1.12.4.1.4.101"            }
        }
    },
    {
        "type": "nhn:dokumentdeling:parameters",
        "version": "0.1",				
        "healthcare_service": {
            "code": "S03",
            "system": "urn:oid:2.16.578.1.12.4.1.1.8627"
        },
        "purpose_of_use": {
            "code": "TREAT",
            "system": "urn:oid:2.16.840.1.113883.1.11.20448"
        },
        "purpose_of_use_details": {
            "code": "15",
            "system": "urn:oid:2.16.578.1.12.4.1.1.9151"
        },
        "tracing_ref": {
            "ref_id" : "[id til lokal tilgangsbeslutning som ekstern referanse for kilden]",
        }			
    },
    // Ev. andre elementer:
    {
        "type" : "helseid_authorization" ,
        "practitioner_role" : { 
            "organization" : { 
                "identify" : {
                    "system" : "urn: oid: 2.16.578.1.12.4.1.2.101" ,
                    "type" : "ENH" ,
                    "value" : "[orgnummer]"
        }
            }
        }
    },
    {
        "type": "helseid://claims/external/amk-context",
        "value": 
        { 
            "foo":
            [
                {
                    "bar": "role1"
                }, 
                {
                    "bar": "role2"
                }
            ]
        }
    }
]

```


