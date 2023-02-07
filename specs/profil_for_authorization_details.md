# Profil for authorization_details json struktur

## Sammendrag

## Dokumentets status

## Innholdsfortegnelse

## 1. Innledning
- Behovet:
	+ Deling av helseopplysninger
	+ Datakilden må tilfredsstille krav til tilgangsstyring og tilgangskontroll
	+ Tillitsmodell og tillitsrammeverk: fordeling av oppgaver
	+ Overføre informasjon om lokal tilgang til datakilde
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