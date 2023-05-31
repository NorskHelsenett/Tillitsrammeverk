# Sikkerhets- og personvernshensyn

Dette dokumentet beskriver sikkerhets- og personvernshensyn i kontekst av bruk av HelseID for å skaffe grunnlag for tilgang til helseopplysninger.

### Sikkerhetshensyn
Peke til https://www.ietf.org/archive/id/draft-ietf-oauth-rar-23.html#name-security-considerations
Beskriv valgte tiltak som forhindrer deler av problemet..
Beskriv ytterligere tiltak som må vurderes av klient/server/HelseID

### Personvernshensyn
Peke til https://www.ietf.org/archive/id/draft-ietf-oauth-rar-23.html#name-privacy-considerations
Beskriv valgte tiltak som forhindrer deler av problemet
Beskriv ytterligere tiltak som må vurderes av klient/server/HelseID

#### Lekkasje av personopplysninger

Datamodellen vil bli benyttet til å overføre personopplysninger om helsepersonellet. Ved å utnytte svakheter og sårbarheter i programvare kan kan en angriper observere personinformasjon som overføres mellom de tekniske tjenestene som benyttes ved deling av helseopplysninger. Lekkasje av PII kan oppstå mellom flere parter i verdikjeden:

mellom konsument og autorisasjonsserver/IdP
mellom konsument og informasjonstjeneste
mellom informasjonstjeneste og datagrensesnitt
For å sikre oss mot potensiell lekkasje av PII bør det vurderes å innføre tiltak for å ivareta konfidensialiteten.

#### Mangelfull informasjon om personvernskonsevenser
Ettersom informasjon i Access Tokens kan bli lagret hos mange aktører og brukt til å informere pasienten om tilgangen til pasientens helseopplysninger er det en risiko for at både pasienten og helsepersonellet mottar mangelfull informasjon om potensielle personvernskonsekvenser ved overføringen av personopplysningene.

#### Misbruk av data
Datamodellen beskriver behandlerrelasjonen som helsepersonellet har til sin pasient, og kan være sensitiv. Det er en risiko for at denne informasjonen misbrukes av en eller flere parter som mottar verdiene i datasettet.

#### Overvåkning av ansatte i andre virksomheter
Datamodellen inneholder en del informasjon som beskriver helsepersonells arbeidsforhold. Denne informasjonen overføres til andre virksomheter enn den virksomheten den ansatte yter helsehjelp hos. Det er en risiko for at denne informasjonen kan benyttes for å overvåke helsepersonell i andre virksomheter.

#### Urettmessig tilegnelse av helseopplysninger
Det er en risiko for at helsepersonellet som ber om tilgang til helseopplysninger ikke har et tjenstlig behov, og at opplysningene ikke er relevante og nødvendige i behandlingen av pasienten.