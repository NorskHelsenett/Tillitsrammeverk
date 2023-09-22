Solution patterns

#########
PAR, DPoP, RAR have impact on what we do
HTTP message signatures will also have an impact
########

# Introducing the concept of "Attestations"



# Pattern A:
Using HelseID to transport the information model

## Variation 1:
* Use the Authorize endpoint (Grant)
* The information is part of the Grant
* The Grant is reflected in the access token and in the userinfo endpoint

Pros: 
Cons: 
- Problematic with the 3rd party cookies for browser based apps
- Problematic for Ragnhilds view on Patient-id
- Requires frequent user log-in with every change in the grant

## Variation 2:
* Use the Authorize endpoint for the tillitsanker information
* Use the Token endpoint for the "Attestation" (client assertion)
* The "Attestation" is included in the access token but not in the userinfo endpoint, it is not part of the grant

pros: could "ride" on the refresh_token (no log in required - based on a first login.. only changes if the legal entity)
cons:

# Pattern B: (OMSs preferred option)
* Using HelseID to transport parts of the information model (OMSs cut-off)
* Passing the "Attestation" directly from the client to the API

pros: simplifies things for HelseID
cons: makes it more difficult for the API-tilbydere and the EHR systems

Thoughts:
- 