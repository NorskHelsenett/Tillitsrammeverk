# Profil for authorization_details json struktur

## Sammendrag

## Dokumentets status

## Innholdsfortegnelse

## 1. Innledning
Ved deling av helseopplysninger på tvers av helsevirksomhetene i norsk helse- og omsorgssektor har virksomheten som deler informasjon en plikt til å etterleve krav i både norm for informasjonssikkerhet og i lovverket. For å tilfredsstille disse kravene har aktører i sektoren samlet seg rundt en modell som beskriver hvordan aktørene kan bygge tilstrekkelig tillit til at delingen skjer innenfor rammene til loven. 

Tillitsmodellen realiseres i et tillitsrammeverk som beskriver konkrete krav til aktørene som skal dele helseopplysninger, og som peker på konkrete tillitsbyggende tjenester som skal benyttes i forbindelse med delingen.

I tillitsrammeverket fordeles oppgaver knyttet til tilgangsstyring ved at konsumenten forplikter seg til å utføre tilstrekkelig god tilgangsstyring og tilgangskontroll på vegne av den som deler helseopplysningene. Virksomheten som deler helseopplysningene skal være trygg på at helsepersonellet har et tjenstlig behov, og at helseopplysningene er relevant og nødvendig i behandlingen av pasienten.

Selv om konsumenten skal utføre tilgangsstyring på vegne av den som deler helseopplysningene trenger datakilden informasjon som beskriver grunnlaget for tilgangen for å gjøre ytterligere tilgangsstyring, logging og for å gi informasjon om tilgangen til pasienten. Informasjonen om den lokale tilgangen må overføres fra konsumenten til datakilden.

### 1.1 Transport av informasjon om lokal tilgang via HelseID

- HelseID som løsning på behovet
	+ Etablerer tillitsforhold til klientene
	+ API har 100% tillit til HelseID
	+ Informasjon er relatert til identitet - passer godt inn i HelseID sammenheng

## 2. Konsept
- Hva er Rich Authorization Requests?
	+ Kort intro til spesifikasjonen
	+ Kort om knytning til samtykke
	+ Hva er RAR ment å bli brukt til?

- klienten autentiserer og autoriserer
- Klienten uttrykker autorisasjon ved bruk av datamodellen
- Klienten pakker inn datamodellen i authorization_details objektet
- Klienten overfører til HelseID
- HelseID reflekterer authorization_details i Access Token

## 3. Spesifikasjon
### 3.1 Avvik fra standard
### 3.2 JSON Struktur
### 3.3 Overføring av authorization_details strukturen
#### 3.3.1 authorization_details i RO
#### 3.3.2 authorization_details i client_assertion


## 4. Sikkerhets- og personvernshensyn