# Attributtvalidering

Dette dokumentet beskriver hvordan HelseID vil validere attributtene som sendes inn som en del av kallet til HelseID for å få utlevert et Access Token som gir tilgang til helseopplysninger.

### Validering av attributter i tillitsmodellen

Tillitsmodellen inneholder følgende attributter:

| Attributt | Beskrivelse | Påkrevd |
| --- | --- | --- |
| "professional_license" | Helsepersonellets lisens, dersom det finnes |  **Nei** |
| "legal_entity" | Den dataansvarlige virksomhetens org.nr og navn. | **Ja** |
| "point_of_care" | Behandlingsstedets org.nr. og navn.<br>Kan være lik verdi som i "legal_entity" | **Ja** |

JSON-strukturen valideres ut fra `type`-claimet, og/eller versjonsnummeret.

Mangel av påkrevde attributter og/eller ugyldige parametre (se under) i kallet til HelseID gir feilkoden `invalid_authorization_details `, som beskrevet i [RFC 9396](https://www.rfc-editor.org/rfc/rfc9396#name-authorization-error-respons).


###### `professional_license`-attributtets JSON-format

````JSON
"professional_license": {
    "hpr_nr": "9144900",
    "authorization": "LE",
},
````

HelseID validerer at `hpr_nr` stemmer overens med HPR-nummeret for brukeren (Validerer for match mot HPR-registeret). 

HelseID validerer at `authorization` matcher en autorisasjon som stemmer overens med en autorisasjon som finnes for brukerens innslag i HPR-registeret.

###### `legal_entity`-attributtets JSON-format

````JSON
"legal_entity": {
    "id": "921592761",
    "name": "Lege Leif Lagesen ENK",
}
```` 

Verdiene `id` og `name` sjekkes mot Enhetsregisteret.

###### `point_of_care`-attributtets JSON-format

````JSON
"point_of_care": {
    "id": "123456789",
    "name": "Det beste legekontoret i byen AS",
}
````

Verdiene `id` og `name` sjekkes mot Enhetsregisteret


## Validering av attributter i datamodellen for dokumentdeling

| Attributt | Beskrivelse | Påkrevd |
| --- | --- | --- |
| "healthcare_service" | Helsetjenestetyper som leveres ved virksomheten |  **Ja** |
| "purpose_of_use" | Helsepersonellets formål med helseopplysningene (til hva de skal brukes) |  **Ja** |
| "purpose_of_use_details" | Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes) | **Nei** |
| "decicion_ref" | Referanse til lokal tilgangsbeslutning | **Nei** |

JSON-strukturen valideres ut fra `type`-claimet, og/eller versjonsnummeret.

Mangel av påkrevde attributter og/eller ugyldige parametre (se under) i kallet til HelseID gir feilkoden `invalid_authorization_details `, som beskrevet i [RFC 9396](https://www.rfc-editor.org/rfc/rfc9396#name-authorization-error-respons).


###### `healthcare_service`-attributtets JSON-format

````JSON
"healthcare_service":{
    "text": "Sykepleietjeneste",
    "code": "KP02",}
````
* Enkel validering på bakgrunn av kodeverk

###### `purpose_of_use`-attributtets JSON-format

````JSON
"purpose_of_use": {
    "code": "TREAT",
    "text": "Behandling",
}
````
* Enkel validering på bakgrunn av kodeverk

###### `purpose_of_use_details`-attributtets JSON-format

````JSON
"purpose_of_use_details": {
    "code": "15",
    "text": "Helsetjenester i hjemmet",
}
````
* Enkel validering på bakgrunn av kodeverk
* Attributtet blir kun validert hvis det er til stede i forespørselen.

###### `decicion_ref`-attributtets JSON-format

````JSON
"decicion_ref": {
    "ref_id" : "id til lokal tilgangsbeslutning", 
}
````
* Tillater kun tall, bokstaver og tegnene _-. 
* Maks lengde 64 tegn.
* Attributtet blir kun validert hvis det er til stede i forespørselen.
