Specifications:
1. Wednesday+Thursday: Dokumentdeling - high level specs (mick + helseid + us)
    - HelseID + Tillitsrammeverk (sekvensdiagram)
        - Request (authorization details)
        - Response (access token)
    - Use of the Access Token
    - KJ part (SAML assertion)
2. Thursday: Data/Information model specs (attributes)
    - Tillitsrammeverk (* - us)
    - Dokumentdeling (* - mick)
3. Specs defining how the attributes are wrapped (Friday intro - Steinar)
    - "whatever simone would like to call it" wrapper (us + helseid)
    - "authorization_details" wrapper (helseid + mick)
4. Kravstilling til kontroll av input-parameter fra klient i HelseID (us + helseid)
5. Tracking id's spec (mick + helseid)
    - rules and tools


- Overordnet beskrivelse av flyt (sekvensdiagram)
    - Konsument -> HelseID
    - HelseID -> Konsument
    - Konsument -> KJ
    - KJ -> KJ/HelseID
    - KJ -> Dokumentkilde
    - Dokumentkilde -> KJ
    - KJ -> Konsument


## Tilgangsforespørsel
- Request til HelseID
- Peke til datamodell for dokumentdeling
- Eksempel på authorization_details objekt
- eksempel: HTTP

## Behandling av tilgangsforespørsel i HelseID
- hva skjer i HelseID?
- peke til tillitsrammeverk
- Eksempel på access token

## Konsumenten kaller KJ
- Hva skjer i Konsumenten
- eksempel: HTTP

## Behandling av forespørsel i KJ
- Sekvensdiagram: brukerinteraksjon
- Token-exchange: SAML
- Total datamodell (tillitsrammeverk + api-specific claims)
- Kall til Dokumentkilde
- Resultat fra Dokumenkilde

