# Attributtvalidering

### Validering av attributter i tillitsmodellen

Tillitsmodellen inneholder følgende attributter:

| Attributt | Beskrivelse | Påkrevd |
| --- | --- | --- |
| "hpr_nr" | Helsepersonellets HPR-nummer, dersom det finnes |  **Nei** |
| "authorization" | Helsepersonellets autorisasjon, dersom den finnes |  **Nei** |
| "legal_entity" | Den dataansvarlige virksomhetens org.nr og navn. | **Ja** |
| "point_of_care" | Behandlingsstedets org.nr. og navn.<br>Kan være lik verdi som i "legal_entity" | **Ja** |

JSON-strukturen valideres med tanke på type ```TODO: finn termer for typologi```

Mangel av påkrevde attributter gir `invalid_request`.


###### "hpr_nr" - Attributt JSON format

````JSON
"hpr_nr": {
    "id": "9144900",
    "system": "urn:oid:2.16.578.1.12.4.1.4.4",
    "authority": "https://www.helsedirektoratet.no/"
},
````

Vi validerer at `id` stemmer overens med HPR-nummeret for brukeren (Validerer for match mot HPR-registeret)

###### "authorization" - Attributt JSON format

````JSON
"authorization": {
    "code": "LE",
    "text": "Lege",
    "system": "urn:oid:2.16.578.1.12.4.1.1.9060",
    "assigner": "https://www.helsedirektoratet.no/"
}
````

Attributtet blir kun validert hvis det er til stede i forespørselen.
Vi validerer at `code` stemmer overens med en autorisajon i HPR-nummeret for brukeren 

###### Den dataansvarlige virksomheten - Attributter JSON format

````JSON
"legal_entity": {
    "id": "921592761",
    "name": "Lege Leif Lagesen ENK",
    "system": "2.16.578.1.12.4.1.4.101",
    "authority": "www.brreg.no"
}
```` 

Attributtet blir kun validert hvis det er til stede i forespørselen.
Verdiene `id` og `name` sjekkes mot Enhetsregisteret

###### Behandlingssted - Attributter JSON format

````JSON
"point_of_care": {
    "id": "123456789",
    "name": "Det beste legekontoret i byen AS",
    "system": "2.16.578.1.12.4.1.4.101",
    "authority": "www.brreg.no"
}
````

Verdiene `id` og `name` sjekkes mot Enhetsregisteret


## Validering av attributter i datamodellen for dokumentdeling

| Attributt | Beskrivelse | Påkrevd |
| --- | --- | --- |
| "department" | Avdeling/org.enhet hvor helsepersonellet yter helsehjelp |  **Nei** |
| "healthcare_service" | Helsetjenestetyper som leveres ved virksomheten |  **Ja** |
| "purpose_of_use" | Helsepersonellets formål med helseopplysningene (til hva de skal brukes) |  **Ja** |
| "purpose_of_use_details" | Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes) | **Nei** |
| "decicion_ref" | Referanse til lokal tilgangsbeslutning | **Nei** |

JSON-strukturen valideres med tanke på type ```TODO: finn termer for typologi```

Mangel av påkrevde attributter gir `invalid_request`.


###### "department" - Attributter JSON format

````JSON
"department": {
    "id": "resh:121313", 
    "system": "resh:x.x.x.x.x.x.x",
    "name": "UNN ....",
    "authority": "",
}
````

Validering: ????
Attributtet blir kun validert hvis det er til stede i forespørselen.

###### "healthcare_service" - Attributter JSON format

````JSON
"healthcare_service":{
    "text": "Sykepleietjeneste",
    "code": "KP02",
    "system": "8663",
    "assigner": "www.helsedirektoratet.no"
}
````

Enkel validering på bakgrunn av kodeverk

###### "purpose_of_use" - JSON format

````JSON
"purpose_of_use": {
    "code": "TREAT",
    "text": "Behandling",
    "system": "urn:oid:2.16.840.1.113883.1.11.20448",
    "assigner": "http://terminology.hl7.org/ValueSet/v3-PurposeOfUse"
}
````

Enkel validering på bakgrunn av kodeverk

###### "purpose_of_use_details" - JSON format

````JSON
"purpose_of_use_details": {
    "code": "15",
    "text": "Helsetjenester i hjemmet",
    "system": "urn:oid:x.x.x.x.x.9151",
    "assigner": "https://www.helsedirektoratet.no/"
}
````

Enkel validering på bakgrunn av kodeverk

Attributtet blir kun validert hvis det er til stede i forespørselen.

###### "decicion_ref" - Attributter JSON format

````JSON
"decicion_ref": {
    "ref_id" : "id til lokal tilgangsbeslutning", 
}
````
Tillater kun tall, bokstaver og tegnene _-. Maks lengde 64 tegn.  ???  
Attributtet blir kun validert hvis det er til stede i forespørselen.
