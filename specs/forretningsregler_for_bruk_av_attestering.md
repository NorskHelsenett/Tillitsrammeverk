# Forretningsregler for bruk av attest
Hva attributtet brukes til skal inn i informasjonsmodell, ikke i regler.. Regler=hvordan - infomodell=hva og hvorfor

## Sammendrag
Dette dokumentet beskriver forretningsregler knyttet til attestering av helsepersonellets grunnlag for tilgang til pasientens helseopplysninger i kjøretid.

Bruksscenarier også for etterarbeid (oppfølgingsarbeid)

## Omfang

Attributtene som kan inngå i en attest er spesifisert i [Informasjons- og datamodell for attestering av grunnlag for tilgang ved deling av helseopplysninger](informasjons_og_datamodell.md).
Attesten skal kunne serialiseres ved bruk av forskjellige formater, som f.eks. JSON, SAML og lignende.

| Kategori      | Attributt                | Beskrivelse                                                                                       | Informasjonskilde | 
|---------------|--------------------------|---------------------------------------------------------------------------------------------------| --------- | 
| practitioner  | "subject"                | Helsepersonellets fødselsnummer og navn fra folkeregisteret                                       | Konsument | 
| practitioner  | "hpr_nr"                 | Helsepersonellets HPR-nummer, dersom det finnes                                                   | Konsument | 
| practitioner  | "authorization"     	   | Helsepersonellets autorisasjon, dersom den finnes                                                 | Konsument | 
| practitioner  | "legal_entity"           | Den juridisk ansvarlige virksomheten hvor helsepersonellet jobber sitt org.nr og navn.            | Konsument | 
| practitioner  | "point_of_care"          | Behandlingsstedets org.nr. og navn.<br>Kan være lik verdi som i "legal_entity"                    | Konsument | 
| practitioner  | "department"             | Avdeling/org.enhet hvor helsepersonellet yter helsehjelp                                          | Konsument | 
| care_relation | "healthcare_service"     | Helsetjenestetyper som leveres ved virksomheten                                                   | Konsument | 
| care_relation | "purpose_of_use"         | Helsepersonellets formål med helseopplysningene (til hva de skal brukes)                          | Konsument | 
| care_relation | "purpose_of_use_details" | Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes) | Konsument | 
| care_relation | "decision_ref"           | Referanse til lokal tilgangsbeslutning                                                            | Konsument | 
| patient       | "patient_id"             | Unik identifikator for pasienten                                                                  | Konsument | 
| patient       | "point_of_care"  	       | Virksomheten hvor pasienten mottar behandling <br>Kan være lik verdi som i "legal_entity"         | Konsument | 
| patient       | "department"             | Avdeling/org.enhet hvor pasienten mottar helsehjelp                                        	   | Konsument | 


## Dokumentets status
| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| -0 | Utkast | 24.10.2023 |

Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til tillitsrammeverk for deling av helseopplysninger i helse- og omsorgssektoren.
Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i tillitsrammeverket.

Spesifikasjonen skal versjoneres for å støtte endringer over tid.

## Innholdsfortegnelse

## Innledning
Denne spesifikasjonen definerer felles regler som skal benyttes i forbindelse med attestering av helsepersonells grunnlag for tilgang til helseopplysninger ved deling av helseopplysninger via tekniske grensesnitt, og baserer seg på [datamodell som er angitt i egen spesifikasjon.](informasjons_og_datamodell.md). 

Et felles regelverk vil sikre at alle aktører som er involvert i delingen benytter samme metode for å utføre attestering og håndtere attester i kjøretid.  


Reglene definert i denne spesifikasjonen omfatter:
<ul>
    <li>Hvordan verdier for de enkelte attributter skal fylles ut.</li>
    <li>Hvilke formål en attest skal benyttes for.</li>
    <li>Hvordan attest skal behandles hos den enkelte aktør.</li>
    <li>Hvordan sikkerhets- og personvernshensyn skal ivaretas hos den enkelte aktør.
</ul>


## Bakgrunn
Aktørene i helse- og omsorgssektoren har samlet seg rundt en felles tillitsmodell som skisserer tillitsgrunnlaget for å dele helseopplysninger mellom helsepersonell på tvers av virksomhetene i sektoren. Les mer om felles tillitsmodell her: [https://www.ehelse.no/standardisering/standarder/anbefaling-av-tillitsmodell-for-data-og-dokumentdeling/](https://www.ehelse.no/standardisering/standarder/anbefaling-av-tillitsmodell-for-data-og-dokumentdeling/_/attachment/inline/4b78b44e-dbfe-4f13-9527-4b47e19a5585:a1003d97d50492bed6eb8064a936354b88a5abf0/Anbefaling%20av%20tillitsmodell%20for%20data-%20og%20dokumentdeling.pdf).

Tillitsmodellen konkretiseres i et tillitsrammeverk som består av vilkår knyttet til bruken av tillitstjenestene (_*Lenke mangler*_). Et grunnleggende vilkår i tillitsrammeverket er kravet til medlemmene av Helsenettet om å etterleve [Norm for informasjonssikkerhet og personvern i helse- og omsorgssektoren](https://www.ehelse.no/normen/normen-for-informasjonssikkerhet-og-personvern-i-helse-og-omsorgssektoren). 

Denne spesifikasjonen er utarbeidet for Pasientens Journaldokumenter (PJD), som er den første anvendelsen av tillitsrammeverket.

## Ordliste

## Spesifikasjon av forretningsregler

Spesifikasjonen definerer felles regler som beskriver  attestering av helsepersonellets grunnlag for tilgang til helseopplysninger samt overføres mellom aktørene. Spesifikasjonen definerer hva denne informasjonen beskriver, og hvorfor den skal overføres.

Spesifikasjonen beskriver en datamodell som angir hvilke konkrete attributter som skal brukes i attesten, og hvilke kodeverk og verdier som er gyldige for hvert attributt.

Spesifikasjonen skal anvendes av programvare- og systemleverandører ved implementasjon av programvare som brukes ved deling av helseopplysninger på tvers av virksomheter i sektoren. 

### Generelle forretningsregler knyttet til attestering av helsepersonellets grunnlag for tilgang
<table>
    <tr><td> ID </td><td> ATT-X </td></tr>
    <tr><td>Navn</td><td>Serialisering av attest</td></tr>
    <tr>
        <td> Regel </td>
        <td>
            En attest skal formatteres til ett av følgende format: 
            <ul>
                <li>JSON</li> 
                <li>XML</li>
            </ul>
            Det er den aktuelle tjenesten som skal konsumeres som avgjør hvilket format som forventes, og blir spesifisert i relevant dokumentasjon av løsning. 
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av:. 
            <ul>
                <li>konsument/innhentende</li> 
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr><td> ID </td><td> ATT-X </td></tr>
    <tr><td>Navn</td><td>Håndtering av sporbarhet</td></tr>
    <tr>
        <td> Regel </td>
        <td>
            Attestens sporbarhet skal ivaretas, slik at attesten:
                <ul>
                    <li>Ivaretar attributtenes integritet under transport og lagring.</li>
                    <li>Entydig, og med høy grad av sannsynlighet, kan knyttes til den konsumerende virksomheten som besluttet tilgangen</li>
                </ul>
            Sporbarhet skal ivaretas ved bruk av digital signatur, og standardiserte signeringsformater:
            <ul>
                <li>For XML: XML-Signature</li>
                <li>For JSON: JOSE - JWS</li>
            </ul>
            Konkrete løsningsvalg kan f.eks. være bruk av SAML eller JWT.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av:. 
            <ul>
                <li>konsument/innhentende</li> 
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr><td> ID </td><td> ATT-X </td></tr>
    <tr><td>Navn</td><td>Sikring av konfidensialitet for informasjon om behandling av pasient.</td></tr>
    <tr>
        <td> Regel </td>
        <td>
            Informasjon som beskriver behandlingsrelasjonen mellom helsepersonellet og pasienten kan være sensitiv og taushetsbelagt, og krever ivaretagelse av konfidensialitet.
            Attesten skal:
                <ul>
                    <li>Overføres ved bruk av kryptert transportlag, f.eks. ved bruk av TLS for transport via http.</li>
                    <li>Krypteres ved lagring over tid</li>                    
                </ul>
            Sporbarhet skal ivaretas ved bruk av digital signatur, og standardiserte signeringsformater:
            <ul>
                <li>For XML: XML-Signature</li>
                <li>For JSON: JOSE - JWS</li>
            </ul>
            Konkrete løsningsvalg kan f.eks. være bruk av SAML eller JWT.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av:. 
            <ul>
                <li>konsument/innhentende</li>
                <li>dokumentkilde/utleverende</li>
            </ul>
        </td>
    </tr>
</table>

### Forretningsregler for beskrivelse av helsepersonellet - attributt: "practitioner"
Informasjon om helsepersonellet er nødvendig for å gjennomføre loggkontroll, sporbarhet og innsyn til innbygger.

#### 1 Forretningsregler for attributtet "subject" 
<table>
    <tr><td> ID </td><td> ATT-X </td></tr>
    <tr><td>Navn</td><td>Bruk av innholdet i attributtet "subject"</td></tr>
    <tr>
        <td> Regel </td>
        <td>Attributtet "subject" skal benyttes til sporbarhetsformål i revisjonslogger, skal benyttes til validering av innkommende parameter i meldinger og KAN eventuelt for informasjon til innbygger (f.eks. http).</td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av alle parter som er involvert i delingen av dokumenter. 
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr><td> ID </td><td> ATT-X </td></tr>
    <tr><td> Navn  </td><td> Visning av innholdet i attributtet "subject" til innbygger </td></tr>
    <tr><td> Regel </td><td> Innbygger skal bare se helsepersonellets navn. Fødselsnummer skal skjules </td></tr>
    <tr>
        <td>Ansvarlig </td><td> 
            Denne regelen håndheves av alle parter som er involvert i delingen av dokumenter. 
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr><td> ID </td><td> ATT-X </td></tr>
    <tr><td> Navn  </td><td> Tillitsnivå (LoA) til data i attributtet "subject" </td></tr>
    <tr>
        <td> Regel </td>
        <td> Identiteten til personen som attributtet "subject" peker på skal være basert på et tillitsnivå "høyt" iht identifikasjonsnivåforskriften, eller tilsvarende. </td>
    </tr>
    <tr>
        <td>Ansvarlig </td>
        <td> 
            Denne regelen håndheves av alle parter som er involvert i delingen av dokumenter. 
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr><td>ID </td><td> ATT-X </td></tr>
    <tr><td> Navn  </td><td> Gyldig identifikator for identifisering av den fysiske personen i attributtet "subject" </td></tr>
    <tr>    
        <td> Regel </td>
        <td> Identifikatoren som skal brukes til å identifisere den fysiske personen skal være registrert i Folkeregisteret. <br/>
            Identifikatoren skal være en av følgende: 
            <ul>
                <li>F-Nummer (2.16.578.1.12.4.1.4.1)</li>
                <li>D-Nummer (2.16.578.1.12.4.1.4.2)</li>                
            </ul>
            Dersom identifikator brukt til å identifisere helsepersonellet ikke er et av de nevnte fødselsnumre skal forespørselen avvises. 
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td> Denne regelen skal håndheves av alle aktører som mottar en attest som følger en http melding.
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>


<table>
    <tr><td> ID </td><td> ATT-X </td></tr>
    <tr><td> Navn  </td><td>Validering av informasjon i attributtet "subject".</td></tr>
    <tr>
        <td> Regel </td>
        <td>Mottaker av attest skal kontrollere og validere at identifikator som identifiserer den fysiske personen i attributtet "subject" i attesten tilsvarer identifikatoren som identifiserer brukeren etter en vellykket autentisering.<br>
        Dersom identifikator i attest ikke tilsvarer identifikator for autentisert bruker skal forespørselen avvises.</td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td> Denne regelen skal håndheves av alle aktører som mottar en attest som følger en http melding.
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende
                <li>tillitsanker/NHN</li>
            </ul>            
        </td>
    </tr>
</table>


#### 2 Forretningsregler for attributtet "legal_entity"

<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Bruk av innholdet i attributtet "legal_entity" </td>
    <tr>    
        <td> Regel </td>
        <td> Identiteten til den juridiske personen skal benyttes til tilgangsstyring hos Tillitsankeret. <br/>
            Tillitsankeret skal kontrollere at den juridiske enheten (virksomheten): 
            <ul>
                <li>har gyldig medlemsskap i Helsenettet</li>
                <li>har akseptert vilkår for medlemssskap i Helsenettet</li>
                <li>har gyldig avtale om tilgang til fellestjenester som HelseID, Kjernejournal osv</li>
                <li>har akseptert bruksvilkår knyttet til fellestjenester</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    <tr>
</table>

<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Sporbarhet knyttet til attributtet "legal_entity" for multi-tenancy systeme og §9 samarbeid</td>
    <tr>    
        <td> Regel </td>
        <td>  
            <ul>
                <li>For multi-tenancy løsninger og §9-samarbeid må den juridisk ansvarlige virksomheten bruke Altinn for å eksplisitt delegere et representasjonsforhold til sin databehandler slik at Tillitsankeret kan utføre kontroll.<br>
                Tillitsanker skal kontrollere at det foreligger en gyldig delegering i Altinn.<li>
                <li>For "on-premise" løsninger vil Tillitsanker benytte informasjon registrert i HelseID selvbetjening til å sikre sporbarhet.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    <tr>
</table>

<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Sporbarhet knyttet til attributtet "legal_entity" for "on-premise" systemer som er brukt av en enkelt virksomhet </td>
    <tr>    
        <td> Regel </td>
        <td>  
            Tilnærming til sporbarhet for dette attributtet er avhengig av systemarkitektur og/eller hvorvidt systemet brukes i §9-samarbeid.
            For on-premise løsninger vil Tillitsanker benytte informasjon registrert i HelseID selvbetjening til å sikre sporbarhet.            
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    <tr>
</table>


Formål med attributtet er også sporbarhet (det juridiske ansvaret - "notoritet"), kan vurderes vist til pasienten i innsynslogg.

#### 3 Forretningsregler for attributtet "point_of_care"

<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Bruk av innholdet i attributtet "point_of_care" </td>
    <tr>    
        <td> Regel </td>
        <td> Identiteten til den juridiske personen skal benyttes til tilgangsstyring hos Tillitsankeret. <br/>
            Tillitsankeret skal kontrollere at den juridiske enheten (virksomheten): 
            <ul>
                <li>har gyldig medlemsskap i Helsenettet</li>
                <li>har akseptert vilkår for medlemssskap i Helsenettet</li>
                <li>har gyldig avtale om tilgang til fellestjenester som HelseID, Kjernejournal osv</li>
                <li>har akseptert bruksvilkår knyttet til fellestjenester</li>
            </ul>
        </td>
    </tr>
    <tr><td> Ansvarlig </td><td>Denne regelen skal håndheves av NHN i rollen som tillitsanker</td>
</table>

#### 4 Forretningsregler for attributtet "department"

#### 5 Forretningsregler for attributtet "hpr_nr"

#### 6 Forretningsregler for attributtet "authorization"


### Forretningsregler for beskrivelse av behandlerrelasjon - attributt: "care_relation"
#### 7 Forretningsregler for attributtet "healthcare_service"

#### 8 Forretningsregler for attributtet "purpose_of_use"
<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Bruk av kode "TREAT" som verdi for attributtet "purpose_of_use" </td>
    <tr>    
        <td> Regel </td>
        <td>TREAT/treatment
            Skal benyttes når forespørsel om tilgang til helsedata skjer i direkte forbindelse med ytelse av helsehjelp som ikke er å regne som akutt. Tilgangsbeslutning hos konsument følger standard regler for tilgangsstyring. 
            Eksempler:
            <ul>
                <li>Planlagt legekonsultasjon hos spesialist</li>
                <li>Behandling hos fastlege som ikke faller under øyeblikkelig hjelp</li>
                <li>Oppfølging av behandlingsplan i virksomhet innen primærhelsetjenesten</li>
            </ul>
        </td>
    </tr>
    <tr><td> Ansvarlig </td><td>Denne regelen skal håndheves av innhentende virksomhet i rollen som konsument</td>
</table>

<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Bruk av kode "ETREAT" som verdi for attributtet "purpose_of_use" </td>
    <tr>    
        <td> Regel </td>
        <td>ETREAT/Emergency Treatment
            Skal benyttes når forespørsel om tilgang til helsedata skjer i direkte forbindelse med ytelse av helsehjelp innen akuttkjeden. Tilgangsbeslutning hos konsument følger standard regler for tilgangsstyring. 
            Eksempler:
            <ul>
                <li>Behandling ved akuttmottak på sykehus eller legevakt</li>
                <li>Behandling i ambulanse, via kontakt med AMK eller legevaktsentral</li>
                <li>Øyeblikkelig hjelp hos fastlege</li>
            </ul>
        </td>
    </tr>
    <tr><td> Ansvarlig </td><td>Denne regelen skal håndheves av innhentende virksomhet i rollen som konsument</td>
</table>

<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Bruk av kode "COC" som verdi for attributtet "purpose_of_use" </td>
    <tr>    
        <td> Regel </td>
        <td>COC/coordination of care
            Skal benyttes når forespørsel om tilgang til helsedata ikke skjer i direkte forbindelse med den kliniske utførelsen av helsehjelp. Tilgangsbeslutning hos konsument følger standard regler for tilgangsstyring. 
            Eksempler:
            <ul>
                <li>Saksbehandling ved tildeling av kommunale helsetjenester</li>
            </ul>
        </td>
    </tr>
    <tr><td> Ansvarlig </td><td>Denne regelen skal håndheves av innhentende virksomhet i rollen som konsument</td>
</table>

<table>
<tr><td>ID </td><td> ATT-X </td></tr>
<tr><td> Navn  </td><td> Bruk av kode "BTG" som verdi for attributtet "purpose_of_use" </td>
    <tr>    
        <td> Regel </td>
        <td>BTG/Break the glass
            Skal benyttes når forespørsel om tilgang til helsedata skjer i direkte forbindelse med ytelse av helsehjelp og en overstyring av normale tilgangsregler er nødvendig for umiddelbar tilgang. Tilgangsbeslutning hos konsument følger ikke standard regler for tilgangsstyring. 
            Eksempler:
            <ul>
                <li>Helsepersonell som yter akutt helsehjelp utenfor egen virksomhet</li>
            </ul>
        </td>
    </tr>
    <tr><td> Ansvarlig </td><td>Denne regelen skal håndheves av innhentende virksomhet i rollen som konsument</td>
</table>


#### 9 Forretningsregler for attributtet "decision_ref"


### Forretningsregler for beskrivelse av pasienten - attributt: "patient"

#### 10 Forretningsregler for attributtet "patient_id"


#### 11 Forretningsregler for attributtet "point_of_care"

#### 11 Forretningsregler for attributtet "department"