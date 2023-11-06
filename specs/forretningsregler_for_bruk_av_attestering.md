# Forretningsregler for bruk av attest
## Sammendrag
Dette dokumentet beskriver forretningsregler knyttet til attestering av helsepersonellets grunnlag for tilgang til pasientens helseopplysninger i kjøretid.

Forretningsreglene omfatter forberedende faser, kjøretid og for bruksscenarier knyttet til oppfølgingsarbeid etter delingen har funnet sted.

## Omfang

Attributtene som kan inngå i en attest er spesifisert i [Informasjons- og datamodell for attestering av grunnlag for tilgang ved deling av helseopplysninger](informasjons_og_datamodell.md).

Tabellen under gir en oversikt over attributtene som inngår i en attest. 

| Kategori      | Attributt                | Beskrivelse                                                                                       | 
|---------------|--------------------------|---------------------------------------------------------------------------------------------------| 
| practitioner  | "identifier"             | Helsepersonellets fødselsnummer og navn fra folkeregisteret                                       | 
| practitioner  | "hpr-nr"                 | Helsepersonellets HPR-nummer, dersom det finnes                                                   | 
| practitioner  | "authorization"     	    | Helsepersonellets autorisasjon, dersom den finnes                                                 | 
| practitioner  | "legal-entity"           | Den juridisk ansvarlige virksomheten hvor helsepersonellet jobber sitt org.nr og navn.            | 
| practitioner  | "point-of-care"          | Behandlingsstedets org.nr. og navn.<br>Kan være lik verdi som i "legal-entity"                    | 
| practitioner  | "department"             | Avdeling/org.enhet hvor helsepersonellet yter helsehjelp                                          | 
| care-relation | "healthcare-service"     | Helsetjenestetyper som leveres ved virksomheten                                                   | 
| care-relation | "purpose-of-use"         | Helsepersonellets formål med helseopplysningene (til hva de skal brukes)                          | 
| care-relation | "purpose-of-use-details" | Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes) | 
| care-relation | "decision-ref"           | Referanse til lokal tilgangsbeslutning                                                            | 
| patient       | "patient_id"             | Unik identifikator for pasienten                                                                  | 
| patient       | "point-of-care"  	       | Virksomheten hvor pasienten mottar behandling <br>Kan være lik verdi som i "legal-entity"         | 
| patient       | "department"             | Avdeling/org.enhet hvor pasienten mottar helsehjelp                                        	   | 

En attest er ikke knyttet til en spesifikk internettprotokoll, eller et spesifikt format, men skal kunne serialiseres ved bruk av forskjellige formater, som f.eks. JSON, XML og CBOR, og benyttes i forskjellige protokoller (som http, amqp, smtp osv). Noen forretningsregler vil være spesifikke for enkelte protokoller eller serialiseringsformater.

## Dokumentets status
| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| -0 | Utkast | 27.10.2023 |

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

Spesifikasjonen definerer felles regler som beskriver hvordan helsepersonellets grunnlag for tilgang til helseopplysninger skal attesteres og krav knyttet hvordan attesten skal benyttes. Spesifikasjonen definerer hvilke kodeverk og verdier som er gyldige for hvert attributt.

### Formålet med forretningsregler
Forretningsreglene skal anvendes av programvare- og systemleverandører ved implementasjon av programvare som brukes ved deling av helseopplysninger på tvers av virksomheter i sektoren.

Forretningsreglene gir også et utgangspunkt for kvalitetssikring/testing av systemene som skal implementere attesteringsfunksjonalitet eller behandle attester.

### 1. Generelle forretningsregler knyttet til attestering av helsepersonellets grunnlag for tilgang
##### (Mulig at dette går inn i et generelt tillitsrammeverk og tas ut av forretningskrav for PJD..)
<table>
    <tr>
        <td> ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Serialisering av attest</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>
            En attest skal formatteres til ett av følgende format: 
            <ul>
                <li>JSON</li> 
                <li>XML</li>
            </ul>
            Det er den aktuelle tjenesten som skal konsumeres som avgjør hvilket format som forventes. Serialiseringsdetaljer blir spesifisert i relevant dokumentasjon av løsning. 
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
    <tr>
        <td> ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Håndtering av sporbarhet</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>
            Attestens sporbarhet skal ivaretas, slik at attesten:
            <ul>
                <li>Ivaretar attributtenes integritet under transport og lagring.</li>
                <li>Entydig, og med høy grad av sannsynlighet, kan knyttes til den konsumerende virksomheten som besluttet tilgangen</li>
            </ul>            
            Sporbarhet kan for eksempel ivaretas ved bruk av digital signatur, og standardiserte signeringsformater:
            <ul>
                <li>XML-Signature og SAML formatet</li>
                <li>Json Web Signatures og JWT formatet</li>
            </ul>
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
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Sikring av konfidensialitet for informasjon om behandling av pasient.</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>
            Informasjon som beskriver behandlingsrelasjonen mellom helsepersonellet og pasienten kan være sensitiv og taushetsbelagt, og krever ivaretagelse av konfidensialitet.
            Attesten skal:
            <ul>
                <li>Overføres ved bruk av kryptert transportlag, f.eks. ved bruk av TLS for transport via http.</li>
                <li>Krypteres ved lagring over tid</li>                    
            </ul>
            Sporbarhet kan f.eks. ivaretas ved bruk av digital signatur, og standardiserte signeringsformater som:
            <ul>
                <li>XML-Encryption og SAML formatet</li>
                <li>Json Web Encryption og JWT formatet</li>
            </ul>
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

### 2. Forretningsregler for beskrivelse av helsepersonellet - attributt: "practitioner"
Informasjon om helsepersonellet er nødvendig for å gjennomføre loggkontroll, sporbarhet og innsyn til innbygger.

#### 2.1 Forretningsregler for attributtet "identifier" 

<table>
    <tr>
        <td> ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Bruk av innholdet i attributtet "identifier"</td>
    </tr>
    <tr>
        <td>Regel</td>
        <td>
            Attributtet "identifier":
            <ul>
                <li>SKAL benyttes til sporbarhetsformål i revisjonslogger</li>
                <li>SKAL benyttes til validering av innkommende parameter i meldinger</li>
                <li>KAN benyttes for informasjon til innbygger</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av alle parter som er involvert i delingen av dokumenter. 
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Visning av innholdet i attributtet "identifier" til innbygger.</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td> Ved anvendelse av attest som informasjonskilde for visning av innsynslogg til innbygger, gjelder følgende regler:
            <ul>
                <li>Innbygger SKAL se helsepersonellets navn.</li>
                <li>Fødselsnummer SKAL IKKE vises</li> 
            </ul>
        </td>
    </tr>
    <tr>
        <td>Ansvarlig </td>
        <td> 
            Denne regelen håndheves av alle parter som er involvert i delingen av dokumenter. 
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Tillitsnivå (LoA) knyttet til data i attributtet "identifier" </td>
    </tr>
    <tr>
        <td> Regel </td>
        <td> Identiteten til personen som attributtet "identifier" peker på SKAL være basert på et tillitsnivå "høyt" iht identifikasjonsnivåforskriften, eller tilsvarende. </td>
    </tr>
    <tr>
        <td>Ansvarlig </td>
        <td> 
            Denne regelen håndheves av alle parter som er involvert i delingen av dokumenter. 
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Gyldig identifikator for identifisering av den fysiske personen i attributtet "identifier" </td>
    </tr>
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
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>


<table>
    <tr>
        <td> ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Validering av informasjon i attributtet "identifier".</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>Mottaker av attest skal kontrollere og validere at identifikator som identifiserer den fysiske personen i attributtet "identifier" i attesten tilsvarer identifikatoren som identifiserer brukeren etter en vellykket autentisering.<br>
        Dersom identifikator i attest ikke tilsvarer identifikator for autentisert bruker skal forespørselen avvises.</td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td> Denne regelen skal håndheves av alle aktører som mottar en attest som følger en http melding.
            <ul>
                <li>konsument/innhentende</li> 
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>            
        </td>
    </tr>
</table>


#### 2.2 Forretningsregler for attributtet "legal-entity"

<table>
    <tr>
        <td>ID </td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Bruk av innholdet i attributtet "legal-entity"</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td> Identiteten til den juridiske personen skal benyttes til tilgangsstyring hos Tillitsankeret. Tillitsankeret skal kontrollere at den juridiske enheten (virksomheten):
            <ul>
                <li>har gyldig medlemsskap i Helsenettet</li>
                <li>har akseptert vilkår for medlemssskap i Helsenettet</li>
                <li>har gyldig avtale om tilgang til fellestjenester som HelseID, Kjernejournal osv</li>
                <li>har akseptert bruksvilkår knyttet til fellestjenester</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    </tr>
</table>


<table>
    <tr>
        <td>ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td> Navn </td>
        <td> Sporbarhet knyttet til attributtet "legal-entity" for multi-tenancy systeme og <a href="https://lovdata.no/lov/2014-06-20-42/§9">§9 samarbeid</a></td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
                For multi-tenancy løsninger og <a href="https://lovdata.no/lov/2014-06-20-42/§9">§9-samarbeid</a> må den juridisk ansvarlige virksomheten bruke Altinn for å eksplisitt delegere et representasjonsforhold til sin databehandler slik at Tillitsankeret kan utføre kontroll.<br>
                Tillitsanker skal kontrollere at det foreligger en gyldig delegering i Altinn.            
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
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td> Sporbarhet knyttet til attributtet "legal-entity" for "on-premise" systemer som er brukt av en enkelt virksomhet </td>
    </tr>
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
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Korrekt angivelse av "legal-entity".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Attributtet "legal-entity" skal inneholde helsepersonellets virksomhetstilhørighet. Det er den registrerte hovedenheten i Brønnøysundregisteret hvor helsepersonellet yter helsehjelp for som skal oppgis.<br> Dersom personellet er innleid og formelt ansatt hos et vikarbyrå eller tilsvarende virksomhet er det ikke denne virksomheten som skal angis.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Korrekt bruk av attributtet "legal-entity".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen dokumenterer hvilken virksomhet som er ansvarlig for personellets tilgang, og vil, sammen med annen informasjon i attesten, dokumentere grunnlaget for at tilgang blir gitt av kilder.<br> 
            Attributtet vil også inngå i pasientjournalens innsynslogg hos kildene. 
            Denne opplysningen SKAL benyttes ved:
            <ul>
                <li>Lovpålagt etterfølgende kontroll av tilgangene hos kilder.</li>
                <li>Visning i løsningen for digitalt innbyggerinnsyn i tilgangslogg fra kilder dersom dette elementet på generelt grunnlag vurderes å gjøre tilgangene mer forståelige for innbyggere.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>Tillitsanker</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>


#### 2.3 Forretningsregler for attributtet "point-of-care"

<table>
    <tr>
        <td>ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td> Bruk av innholdet i attributtet "point-of-care"</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>Identiteten til den juridiske personen skal benyttes til tilgangsstyring hos Tillitsankeret.<br>
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
        <td>Ansvarlig</td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td> Angivelse av innholdet i attributtet "point-of-care"</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>Attributtet skal inneholde helsepersonellets arbeidssted, som også kan omtales som behandlingsstedet helsepersonellet formelt er tilknyttet. Det er den registrerte underenheten i Brønnøysundregisteret som helsepersonellet formelt utfører sitt arbeide ved som skal oppgis.<br>
        Det er et generelt krav til alle norske virksomheter at aktivitet skal kunne rapporteres per geografisk sted og per registrert næringskode i Brønnøysund som det drives virksomhet ved, og derfor skal det være registrert slike underenheter i Brønnøysundregisteret for de fleste virksomheter i Norge.
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID </td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td> Angivelse av innholdet i attributtet "point-of-care" for virksomheter uten underliggende enheter</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>For virksomheter som eventuelt ikke har registrert noen underliggende enheter i Brønnøysundregistrene skal den overordnede enheten oppgis i dette attributtet.<br>
        Verdien i "legal-entity" og "point-of-care" vil i slike tilfeller være lik.
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Korrekt bruk av attributtet "point-of-care".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen dokumenterer behandlingsstedet som helsepersonellet yter helsehjelp ved når tilgangen til pasientens helseopplysninger ble gitt av konsumenten. Denne informasjonen vil, sammen med annen informasjon i attesten, dokumentere grunnlaget for at tilgang blir gitt av kilder.<br>
            Attributtet vil også inngå i pasientjournalens innsynslogg hos kildene. 
            Denne opplysningen SKAL benyttes ved:
            <ul>
                <li>Lovpålagt etterfølgende kontroll av tilgangene hos kilder.</li>
                <li>Visning i løsningen for digitalt innbyggerinnsyn i tilgangslogg fra kilder dersom dette elementet på generelt grunnlag vurderes å gjøre tilgangene mer forståelige for innbyggere.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>Tillitsanker</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

#### 2.4 Forretningsregler for attributtet "department"

<table>
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Overordnede regler for bruk av attributtet "department".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            I virksomheter som er organisert i flere lokalt definerte underliggende enheter enn de som fremkommer av offentlig registrering i Brønnøysundregistrene, er det et krav at attesten formidler informasjon om hvilken av disse lokalt definerte enhetene helsepersonellet tilhører.<br> 
            Det er ikke et krav om å formidle noe i dette attributtet fra virksomheter uten lokalt definerte underliggende enheter ut over det som fremkommer av offentlig registrering i Brønnøysundregistrene.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Korrekt detaljeringsnivå for attributtet "department".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Hvilket detaljeringsnivå innenfor et potensielt større hierarki av lokalt definerte enheter som er riktig å legge i attesten vil i stor grad avhenge av hva som er praktisk mulig ut fra tilgjengelige registreringer av helsepersonellets organisasjonstilhørighet, og det må derfor vurderes av konsumentvirksomheten.<br><br>
            Ved flere mulige valg bør det vektlegges hva som i størst mulig grad kan bidra til å avklare hva som er bakgrunnen for tilgangen. Som hovedregel bør dette være et så detaljert nivå som mulig heller enn et mer overordnet nivå, og likevel et nivå pasienten og eksternt helsepersonell med størst sannsynlighet har et forhold til fremfor mer administrative og formelle nivåer som bare internt personell forholder seg til.<br>
            I noen tilfeller kan det være behov for å avgi et mer overordnet nivå av hensyn til behov for særlig diskresjon som virksomheten måtte ha behov for ved enkelte mer spesielle enheter.<br>Det kan også være relevant i vurderingen hvilket nivå pasienter eller eksternt personell bør kontakte dersom det er spørsmål om tilgangen har vært legitimt begrunnet, hvis det er ønskelig at slike spørsmål i størst mulig grad håndteres av for eksempel nærmeste leder.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Korrekt bruk av attributtet "department".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen vil i første rekke benyttes som et av flere elementer fra attesten som i sum dokumenterer grunnlaget for at tilgang blir gitt, og dermed inngå i pasientjournalens innsynslogg. Denne opplysningen vil benyttes ved lovpålagt etterfølgende kontroll av tilgangene, samt eventuelt vises i løsningen for digitalt innbyggerinnsyn i tilgangslogg dersom dette elementet på generelt grunnlag vurderes å gjøre tilgangene mer forståelige for innbyggere.<br> 
            Denne opplysningen SKAL benyttes ved:
            <ul>
                <li>Lovpålagt etterfølgende kontroll av tilgangene hos kilder.</li>
                <li>Visning i løsningen for digitalt innbyggerinnsyn i tilgangslogg fra kilder dersom dette elementet på generelt grunnlag vurderes å gjøre tilgangene mer forståelige for innbyggere.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av verdi for attributtet "department" for mindre virksomheter</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td> Attributtet er ikke relevant for mindre virksomheter uten et organiasjonshierarki.<br>
             Det er derfor ikke obligatorisk å legge det ved i attesten.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av verdi for attributtet "department" for kommunale virksomheter </td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td> 
            Bruk attributtet "department" for å angi:
            <ul>
                <li>Aktuell skole i skolehelsetjenesten</li>
                <li>Avdeling eller spesifikk enhet i sykehjemskontekst dersom det er relevant</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av verdi for attributtet "department" for Helseforetak i spesialisthelsetjenesten </td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td> 
            Bruk attributtet "department" for å angi:
            <ul>
                <li>?</li>
                <li>?</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Granuleringsnivå for angivelse av "department"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td> Det er virksomheten hvor helsepersonellet jobber som må vurdere hvilket granuleringsnivå som vil være hensiktsmessig for å beskrive hvilken avdeling eller enhet helsepersonellet helsepersonellet yter helsehjelp hos.<br>
             Granularitetsnivået må gi verdi i følgende scenario:
             <ul>
                <li>ved oppfølging av henvendelser fra andre virksomheter</li>
                <li>ved logganalyse og loggoppfølging i egen virksomhet</li>
                <li>ved informasjon til pasienten</li>
            <ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li> 
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av "assigner" og "system" for lokale identifikatorer for attributtet "department"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>"System" og "assigner" skal angis selv om konsumenten har lokale identifikatorer som brukes for å beskrive avdeling/organisasjonsenhet.<br>
        I slike tilfeller skal:
        <ul>
            <li>verdien for attributtet "assigner" skal settes til org.nr for juridisk enhet. 
            <li>verdien for attributtet "system" skal settes til en globalt unik identifikator for å sikre at de er entydige over tid.<br>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li> 
            </ul>  
        </td>
    </tr>
</table>



#### 2.5 Forretningsregler for attributtet "hpr-nr"
<table>
    <tr>
        <td>ID </td><td> ATT-X </td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av verdi for attributtet "hpr-nr" for helsepersonell uten lisens/autorisasjon</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Det kan forekomme at helsepersonell uten lisens eller autorisasjon i HPR trenger tilgang på helseopplysninger. Derfor er ikke attributtet "hpr-nr" påkrevd.<br>
            Attributtet "hpr-nr" skal inkluderes i datamodellen dersom den fysiske personen har et innslag i HPR.
            <ul>
                <li>Attributtet skal angis dersom den fysiske personen har et innslag i HPR.</li>
                <li>Attributtet kan utelates fra attesten dersom helsepersonellet ikke har et innslag i HPR</li>
            </ul> 
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

#### 2.6 Forretningsregler for attributtet "authorization"
<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av verdi for attributtet "hpr-nr" for helsepersonell uten lisens/autorisasjon </td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            Det kan forekomme at helsepersonell uten lisens eller autorisasjon i HPR trenger tilgang på helseopplysninger. Derfor er ikke attributtet "hpr-nr" påkrevd.<br>
            Attributtet "hpr-nr" skal inkluderes i datamodellen dersom den fysiske personen har et innslag i HPR.
            <ul>
                <li>Attributtet skal angis dersom den fysiske personen har et innslag i HPR.</li>
                <li>Attributtet kan utelates fra attesten dersom helsepersonellet ikke har et innslag i HPR</li>
            </ul> 
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Håndtering av helsepersonell med flere autorisasjoner i HPR</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            I tilfeller hvor helsepersonellet har flere autorisasjoner i helsepersonellregisteret skal konsumenten, så godt som mulig, bruke autorisasjonen som ligger nærmest den funksjonelle rollen helsepersonellet har i sin behandling av pasienten.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Kontroll av korrekte autorisasjoner i tillitsankeret</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            Tillitsankeret skal kontrollere at den angitte autorisasjonen eksisterer i helsepersonellregisteret for det aktuelle helsepersonellet.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

### 3. Forretningsregler for beskrivelse av behandlerrelasjon - attributt: "care-relation"
#### 3.1 Forretningsregler for attributtet "healthcare-service"

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av verdi for attributtet "healthcare-service"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Konsumerende virksomhet må selv avgjøre hvilke verdier for angivelse av attributtet "healthcare-service" som best beskriver typen helsetjeneste som leveres ved virksomheten hvor helsepersonellet yter helsehjelp.<br>
            Verdien som angis for attributtet "healthcare-service" skal være definert i ett av de følgende kodeverkene:
            <ul>
                <li><a href="https://volven.no/produkt.asp?open_f=true&id=495806&catID=3&subID=8&subCat=163&oid=8655">Tjenestetyper innen spesialisthelsetjenesten (OID=2.16.578.1.12.4.1.1.8655)</a></li>
                <li><a href="https://volven.no/produkt.asp?id=507406&catID=3&subID=8">UTGÅTT Tjenestetyper innen spesialisthelsetjenesten (OID=2.16.578.1.12.4.1.1.8627)</a></li>
                <li><a href="https://volven.no/produkt.asp?id=507306&catID=3&subID=8">Fagområde (OID=2.16.578.1.12.4.1.1.8451)</a></li>
                <li><a href="https://volven.no/produkt.asp?open_f=true&id=496329&catID=3&subID=8&subCat=163&oid=8668">Tjenestetyper for spesialisthelsetjenesten (OID=2.16.578.1.12.4.1.1.8668)</a></li>
                <li><a href="https://volven.no/produkt.asp?open_f=true&id=496326&catID=3&subID=8&subCat=163&oid=8663">Tjenestetyper for kommunal helse- og omsorgstjeneste mv (OID=2.16.578.1.12.4.1.1.8663)</a></li>
                <li><a href="https://volven.no/produkt.asp?open_f=true&id=496298&catID=3&subID=8&subCat=163&oid=8662">Fylkeskommunale tjenestetyper (OID=2.16.578.1.12.4.1.1.8662)</a></li>
                <li><a href="https://volven.no/produkt.asp?open_f=true&id=496327&catID=3&subID=8&subCat=163&oid=8664">Tjenestetyper for apotek og bandasjister (OID=2.16.578.1.12.4.1.1.8664)</a></li>
                <li><a href="https://volven.no/produkt.asp?open_f=true&id=496328&catID=3&subID=8&subCat=163&oid=8666">Felles tjenestetyper (OID=2.16.578.1.12.4.1.1.8666)</a></li>
            </ul>  
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>


#### 3.2 Forretningsregler for attributtet "purpose-of-use"
<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av kode "TREAT" som verdi for attributtet "purpose-of-use"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td><em>TREAT</em> (Treatment)<br>
            Skal benyttes når forespørsel om tilgang til helsedata skjer i direkte forbindelse med ytelse av helsehjelp som ikke er å regne som akutt. Tilgangsbeslutning hos konsument følger standard regler for tilgangsstyring. 
            Eksempler:
            <ul>
                <li>Planlagt legekonsultasjon hos spesialist</li>
                <li>Behandling hos fastlege som ikke faller under øyeblikkelig hjelp</li>
                <li>Oppfølging av behandlingsplan i virksomhet innen primærhelsetjenesten</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av kode "ETREAT" som verdi for attributtet "purpose-of-use"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td><em>ETREAT</em> (Emergency Treatment)<br>
            Skal benyttes når forespørsel om tilgang til helsedata skjer i direkte forbindelse med ytelse av helsehjelp innen akuttkjeden. Tilgangsbeslutning hos konsument følger standard regler for tilgangsstyring. 
            Eksempler:
            <ul>
                <li>Behandling ved akuttmottak på sykehus eller legevakt</li>
                <li>Behandling i ambulanse, via kontakt med AMK eller legevaktsentral</li>
                <li>Øyeblikkelig hjelp hos fastlege</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av kode "COC" som verdi for attributtet "purpose-of-use"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td><em>COC</em> (coordination of care)<br>
            Skal benyttes når forespørsel om tilgang til helsedata ikke skjer i direkte forbindelse med den kliniske utførelsen av helsehjelp. Tilgangsbeslutning hos konsument følger standard regler for tilgangsstyring. 
            Eksempler:
            <ul>
                <li>Saksbehandling ved tildeling av kommunale helsetjenester</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Angivelse av kode "BTG" som verdi for attributtet "purpose-of-use"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td><em>BTG (Break the glass)<em><br>
            Skal benyttes når forespørsel om tilgang til helsedata skjer i direkte forbindelse med ytelse av helsehjelp og en overstyring av normale tilgangsregler er nødvendig for umiddelbar tilgang. Tilgangsbeslutning hos konsument følger ikke standard regler for tilgangsstyring.<br> 
            Eksempler:
            <ul>
                <li>Helsepersonell som yter akutt helsehjelp utenfor egen virksomhet</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

#### 3.3 Forretningsregler for attributtet "purpose-of-use-details"

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Gyldige kodeverk for angivelse av verdi for "purpose-of-use-details"</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            Informasjonen i attributtet kan beskrives ved bruk av forskjellige kodeverk avhengig av hvilke helsetjenester pasienten mottar.
            <ul>
                <li>For attestering av helsepersonell i spesialisthelsetjenesten skal følgende kodeverk benyttes: <a href="https://hl7norway.github.io/AuditEvent/currentbuild/CodeSystem-carerelation.html">HL7 Norway: care relation</a></li>                
                <li>For attestering av helsepersonell i sykehjemstjenesten skal følgende kodeverk benyttes:<a href="https://volven.no/produkt.asp?open_f=true&id=494341&catID=3&subID=8&subCat=140&oid=9151">Volvens kodeverk 9151</a></li>
                <li>Dersom det finnes andre eksisterende kodeverk som har samme formål kan disse også benyttes.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>


#### 3.4 Forretningsregler for attributtet "decision-ref"

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Informasjon til helsepersonellet om bruk av "user_reason" i attributtet "decision-ref".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Ved bruk av attributtet "user_reason" når helsepersonellet selv angir formål eller begrunnelse for tilgangen til helseopplysningene må helsepersonellet informeres om at denne informasjonen kan bli brukt i forbindelse med logganalyse og loggoppfølging eller bli vist til pasienten.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>konsument/innhentende</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Gyldige tegn for "user_reason" i attributtet "decision-ref".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Ettersom verdien i attributtet "user_reason" er basert på inntastet tekst fra bruker er det en risiko for at en ondsinnet aktør kan utføre sikkerhetsangrep ved å manipulere data i dette feltet. Verdien i attributtet blir transportert, behandlet og lagret i forskjellige systemer på tvers av virksomhetene i verdikjeden.<br>
            Derfor skal det være usannsynlig at det kan utføres sikkerhetsangrep ved bruk av innholdet i attributtet. Verdien skal kun inneholde alfanumeriske tegn, samt utvalgte spesialtegn.<br>
            Tekstverdien skal sikres mot forskjellige typer angrep, som: 
            <ul>
                <li>SQL injection angrep</li>
                <li>JSON SQL injection angrep</li>
                <li>XSS angrep</li>                
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal kontrolleres og håndheves av:
            <ul>
                <li>konsument/innhentende</li>
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Maksimalt antall tegn for "user_reason" i attributtet "decision-ref".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Ettersom verdien i attributtet "user_reason" er basert på inntastet tekst fra bruker er det en risiko for at en ondsinnet aktør kan utføre sikkerhetsangrep ved å manipulere data i dette feltet.<br>
            Derfor skal det være usannsynlig at det kan utføres sikkerhetsangrep ved bruk av innholdet i attributtet.<br> 
            Verdien for attributtet "user_reason" skal inneholde <b>maksimalt 250 tegn</b>.<br>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal kontrolleres og håndheves av:
            <ul>
                <li>konsument/innhentende</li>
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-X</td>
    </tr>
    <tr>
        <td>Navn</td>
        <td>Gyldige verdi for "user_selected" i attributtet "decision-ref".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Verdien for attributtet "user_selected" skal være av typen <em>boolean</em>.<br>
            Verdien angir om helsepersonellet har gitt seg selv tilgang til pasientens helseopplysninger, eller om tilgangen er systemutledet.
            <ul>
                <li>Dersom tilgangen er systemutledet, dvs basert på informasjon om helsepersonellet og pasienten som er registeret i PAS/EPJ (eventuelt i annet fagsystem), skal verdien være <em>false</em>.</li>
                <li>Dersom tilgangen er gitt av helsepersonellet selv (selvautorisasjon) skal verdien være <em>true</em>.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal kontrolleres og håndheves av:
            <ul>
                <li>konsument/innhentende</li>
                <li>dokumentkilde/utleverende</li>
                <li>tillitsanker/NHN</li>
            </ul>  
        </td>
    </tr>
</table>

### 4. Forretningsregler for beskrivelse av pasienten - attributt: "patient"

#### 4.1 Forretningsregler for attributtet "patient_id"


#### 4.2 Forretningsregler for attributtet "point-of-care"


#### 4.3 Forretningsregler for attributtet "department"
           
