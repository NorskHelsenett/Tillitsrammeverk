# Forretningsregler for bruk av attest
## Sammendrag
Dette dokumentet beskriver forretningsregler knyttet til attestering av helsepersonellets grunnlag for tilgang til pasientens helseopplysninger i kjøretid.

Forretningsreglene omfatter forberedende faser, kjøretidsfasen samt oppfølgingsarbeid etter delingen har funnet sted.

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
| patient       | "identifier"             | Unik identifikator for pasienten                                                                  | 
| patient       | "point-of-care"  	       | Virksomheten hvor pasienten mottar behandling <br>Kan være lik verdi som i "legal-entity"         | 
| patient       | "department"             | Avdeling/org.enhet hvor pasienten mottar helsehjelp                                        	   | 

En attest er ikke knyttet til en spesifikk internettprotokoll, eller et spesifikt format, men skal kunne serialiseres ved bruk av forskjellige formater, som f.eks. JSON, XML og CBOR, og benyttes i forskjellige protokoller (som http, amqp, smtp osv). 

Noen forretningsregler vil kunne være spesifikke for enkelte protokoller eller serialiseringsformater.

## Dokumentets status
| Versjon | Dokumentets status | dato |
| --- | --- | --- |
| -0 | Utkast | 27.10.2023 |

Dette dokumentet utgjør ikke en formell standard, men inngår som en del av et kravsett knyttet til tillitsrammeverk for deling av helseopplysninger i helse- og omsorgssektoren.
Spesifikasjonen bør ikke benyttes uten føringene som ligger til grunn i tillitsrammeverket.

Spesifikasjonen skal versjoneres for å støtte endringer over tid.

## Innholdsfortegnelse

## Innledning
Denne spesifikasjonen definerer felles regler som skal benyttes i forbindelse med attestering av helsepersonells grunnlag for tilgang til helseopplysninger ved deling av helseopplysninger via tekniske grensesnitt, og baserer seg på [datamodell for attestering som er angitt i egen spesifikasjon.](informasjons_og_datamodell.md). 

Et felles regelverk vil sikre at alle aktører som er involvert i delingen benytter samme metode for å utføre attestering og at attester håndteres likt i kjøretid og benyttes til samme formål etter at helseopplysningene er delt.

Reglene definert i denne spesifikasjonen omfatter:
<ul>
    <li>Hvilke formål en attest skal benyttes for.</li>
    <li>Hvilke verdier som er gyldige for de enkelte attributter.</li>
    <li>Hvordan en attest skal behandles hos den enkelte aktør.</li>
    <li>Hvordan sikkerhets- og personvernshensyn skal ivaretas hos den enkelte aktør.</li>
</ul>

Datamodellen som skal brukes til attestering og reglene skissert i denne spesifikasjonen, er ment å være gjenbrukbare for ulike protokoller og tekniske løsninger. Spesifikasjonene peker derfor ikke på konkrete tekniske protokoller, tjenester eller tekniske løsninger.

Så lenge de overordnede kravene blir tilfredsstilt står hver enkelt løsning, som skal ta i bruk attestering av helsepersonellets grunnlag for tilgang til helseopplysninger, fritt til å velge teknologi og implementasjonsdetaljer for attestering og overføring av attest.

## Bakgrunn
Aktørene i helse- og omsorgssektoren har samlet seg rundt en felles modell som skisserer tillitsgrunnlaget for å dele helseopplysninger mellom helsepersonell på tvers av virksomhetene i sektoren. Les mer om felles tillitsmodell her: [https://www.ehelse.no/standardisering/standarder/anbefaling-av-tillitsmodell-for-data-og-dokumentdeling/](https://www.ehelse.no/standardisering/standarder/anbefaling-av-tillitsmodell-for-data-og-dokumentdeling/_/attachment/inline/4b78b44e-dbfe-4f13-9527-4b47e19a5585:a1003d97d50492bed6eb8064a936354b88a5abf0/Anbefaling%20av%20tillitsmodell%20for%20data-%20og%20dokumentdeling.pdf).

Tillitsmodellen konkretiseres i et [tillitsrammeverk](https://www.nhn.no/tjenester/kjernejournal/deling-av-journaldokumenter-gjennom-kjernejournal/Beskrivelse%20av%20tillitsrammeverk.pdf) som består av vilkår knyttet til bruken av tillitstjenestene. Det er medlemsordningen Helsenettet som danner de ytre rammene for økosystemet hvor tillitsrammeverket skal virke. Et grunnleggende vilkår i tillitsrammeverket er at medlemmene av Helsenettet plikter å etterleve kravene i [norm for informasjonssikkerhet og personvern i helse- og omsorgssektoren](https://www.ehelse.no/normen/normen-for-informasjonssikkerhet-og-personvern-i-helse-og-omsorgssektoren). 

Denne spesifikasjonen er utarbeidet i forbindelse med Pasientens Journaldokumenter (PJD), som er den første anvendelsen av tillitsrammeverket. 

## Ordliste

## Spesifikasjon av forretningsregler
Spesifikasjonen definerer felles regler som beskriver hvordan helsepersonellets grunnlag for tilgang til helseopplysninger skal attesteres og krav knyttet hvordan attesten skal benyttes. Spesifikasjonen definerer hvilke kodeverk og verdier som er gyldige for hvert attributt.

### Formålet med forretningsregler
Forretningsreglene skal anvendes av programvare- og systemleverandører ved implementasjon av programvare som brukes ved deling av helseopplysninger på tvers av virksomheter i sektoren.

Forretningsreglene gir også et utgangspunkt for kvalitetssikring/testing av systemene som skal implementere attesteringsfunksjonalitet eller behandle attester.

### Konvensjoner brukt i spesifikasjonen

#### Bruk av modalverb i spesifikasjonen
Modalverb brukt i spesifikasjonen skal forstås på følgende måte:
<table>
    <tr>
        <td>SKAL/MÅ</td>
        <td>Absolutt krav</td>
    </tr>
    <tr>
        <td>BØR</td>
        <td>Anbefalt krav</td>
    </tr>
    <tr>
        <td>KAN</td>
        <td>Valgfritt krav</td>
    </tr>
</table>

#### Begreper brukt i spesifikasjonen
Hver regel i spesifikasjonen er beskrevet i følgende format:
<table>
    <tr>
        <td>Begrep</td>
        <td>Definisjon</td>
    </tr>
    <tr>
        <td>ID</td>
        <td>En unik identifikator for regelen som er spesifisert</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>Navn på attributtet som skal benyttes til attestering</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>En kort forklaring på hvilken informasjon attributtet inneholder</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>En kort overordnet beskrivelse av regelen</td>
    </tr>
    <tr>
        <td>Regel</td>
        <td>En detaljert beskrivelse av den aktuelle regelen</td>
    </tr>
    <tr>
        <td>Ansvarlig</td> 
        <td>En beskrivelse av hvilke(n) aktør(er) som er ansvarlig for å håndheve regelen</td>
    </tr>
</table>


### 1. Generelle forretningsregler knyttet til attestering av helsepersonellets grunnlag for tilgang
##### (Mulig at dette går inn i et generelt tillitsrammeverk og tas ut av forretningskrav for PJD..)
<table>
    <tr>
        <td> ID </td>
        <td> ATT-1 </td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Serialisering av attest</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>
            En attest SKAL formatteres til ett av følgende format: 
            <ul>
                <li>JSON</li> 
                <li>XML</li>
            </ul>
            Det er den aktuelle tjenesten som skal konsumeres som avgjør hvilket format som forventes. Serialiseringsdetaljer blir spesifisert i relevant dokumentasjon av den aktuelle løsningen. 
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av:. 
            <ul>
                <li>Konsument</li> 
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td> ID </td>
        <td> ATT-2 </td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Håndtering av sporbarhet</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>
            Attestens sporbarhet skal ivaretas, slik at attesten:
            <ul>
                <li>Ivaretar attributtenes integritet under transport og lagring</li>
                <li>Entydig, og med høy grad av sannsynlighet, kan knyttes til den konsumerende virksomheten som besluttet tilgangen</li>
            </ul>            
            Sporbarhet SKAL ivaretas ved bruk av digital signatur og standardiserte signeringsformater, som f.eks.:
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
                <li>Konsument</li> 
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-3 </td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Sikring av konfidensialitet for informasjon om behandling av pasient.</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>
            Informasjon som beskriver behandlingsrelasjonen mellom helsepersonellet og pasienten kan være sensitiv og taushetsbelagt, og krever ivaretagelse av konfidensialitet.
            Attesten SKAL:
            <ul>
                <li>Overføres ved bruk av kryptert transportlag, f.eks. ved bruk av TLS for transport via http.</li>
                <li>Krypteres ved lagring over tid</li>                    
            </ul>
            Konfidensialitet KAN ivaretas ved bruk av meldingskryptering (ende-til-ende), og standardiserte krypteringsformater som f.eks.:
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
                <li>Konsument</li>
                <li>Dokumentkilde</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-4 </td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Knytning mellom attest og pasientens identitet</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>Når en attest gjelder helsepersonellets grunnlag for tilgang til en spesifikk pasient SKAL attesten entydig knyttes til pasienten som er inne til behandling, slik at den ikke kan brukes for tilgang til andre pasienter.<br>
        Pasientens identifikator SKAL være forståelig for parten som mottar attesten.<br><br>
        Denne regelen gjelder også i tilfeller hvor attesten gjelder for flere spesifikke pasienter.<br>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av:. 
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
        <td> ATT-5 </td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Bruk av identifikatorer i attest for håndheving av sperringer</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>Ved forespørsler hvor et helsepersonell ber om tilgang til en eller flere spesifikke pasienter SKAL informasjon i en attest brukes til å håndheve sperringer hos data- eller dokumentkilde.<br>
        Det SKAL være mulig å kontrollere at helsepersonellet som har tjenstlig behov for pasientens helseopplysninger ikke er sperret for tilgang av pasienten.<br>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av:. 
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
        <td> ATT-6 </td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Attest som ikke gjelder en spesifikk pasient eller flere pasienter</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>I noen tilfeller hvor pasienten ikke er kjent KAN attesten benyttes uten binding til en spesifikk pasient.<br>
            En attest uten binding til pasient BØR bare kunne benyttes for tilgang til et smalt sett av opplysninger om pasienten.<br><br>
            Eksempler på slike tilfeller kan være:
            <ul>
                <li>henting av en oversikt over pasienter som er innkommende til en legevakt i ambulanser, eller</li>
                <li>oversikt over pasienter som er innlagt ved en gitt enhet.</li> 
            </ul>    
            Når helsepersonellet trenger å se mer detaljert informasjon om en spesifikk pasient SKAL attesten være knyttet til denne pasienten.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td> 
        <td>
            Denne regelen håndheves av:. 
            <ul>
                <li>Konsument</li>
                <li>Dokumentkilde</li>
            </ul>
        </td>
    </tr>
</table>

### 2. Forretningsregler for beskrivelse av helsepersonellet - attributt: "practitioner"
Attributtet "practitioner" består av seks underliggende attributt som beskriver helsepersonellet som attesten gjelder for.
| | |
| --- | --- |
| practitioner  | "identifier"             | Helsepersonellets fødselsnummer og navn fra folkeregisteret                                       | 
| practitioner  | "hpr-nr"                 | Helsepersonellets HPR-nummer, dersom det finnes                                                   | 
| practitioner  | "authorization"     	    | Helsepersonellets autorisasjon, dersom den finnes                                                 | 
| practitioner  | "legal-entity"           | Den juridisk ansvarlige virksomheten hvor helsepersonellet jobber sitt org.nr og navn.            | 
| practitioner  | "point-of-care"          | Behandlingsstedets org.nr. og navn.<br>Kan være lik verdi som i "legal-entity"                    | 
| practitioner  | "department"             | Avdeling/org.enhet hvor helsepersonellet yter helsehjelp                                          | 

#### 2.1 Forretningsregler for attributtet "identifier"

<table>
    <tr>
        <td> ID </td>
        <td> ATT-7 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"identifier"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets fødselsnummer og navn fra folkeregisteret</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li> 
                <li>Dokumentkilde</li>
                <li>NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-8</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"identifier"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets fødselsnummer og navn fra folkeregisteret</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Visning av innholdet i attributtet "identifier" i innbyggerens tilgangslogg.</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td> Ved anvendelse av attest som informasjonskilde for løsning som viser tilgangslogg til innbyggeren, gjelder følgende regler:
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
                <li>Konsument</li> 
                <li>Dokumentkilde</li>
                <li>NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-9</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"identifier"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets fødselsnummer og navn fra folkeregisteret</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li> 
                <li>Dokumentkilde</li>
                <li>NHN</li>
            </ul>
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-10</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"identifier"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets fødselsnummer og navn fra folkeregisteret</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Gyldig identifikator for identifisering av den fysiske personen i attributtet "identifier" </td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td> Identifikatoren som skal brukes til å identifisere den fysiske personen SKAL være registrert i Folkeregisteret. <br/>
            Identifikatoren skal være en av følgende: 
            <ul>
                <li>F-Nummer (2.16.578.1.12.4.1.4.1)</li>
                <li>D-Nummer (2.16.578.1.12.4.1.4.2)</li>                
            </ul>
            Dersom identifikator brukt til å identifisere helsepersonellet ikke er et av de nevnte fødselsnumre SKAL forespørselen avvises. 
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td> Denne regelen skal håndheves av alle aktører som mottar en attest som følger en http melding.
            <ul>
                <li>Konsument</li> 
                <li>Dokumentkilde</li>
                <li>NHN</li>
            </ul>
        </td>
    </tr>
</table>


<table>
    <tr>
        <td> ID </td>
        <td> ATT-11 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"identifier"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets fødselsnummer og navn fra folkeregisteret</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Validering av informasjon i attributtet "identifier".</td>
    </tr>
    <tr>
        <td> Regel </td>
        <td>Mottaker av attest SKAL kontrollere og validere at identifikator som identifiserer den fysiske personen i attributtet "identifier" i attesten tilsvarer identifikatoren som identifiserer brukeren etter en vellykket autentisering.<br>
        Dersom identifikator i attest ikke tilsvarer identifikator for autentisert bruker SKAL forespørselen avvises.</td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td> Denne regelen skal håndheves av alle aktører som mottar en attest som følger en http melding.
            <ul>
                <li>Konsument</li> 
                <li>Dokumentkilde</li>
                <li>NHN</li>
            </ul>            
        </td>
    </tr>
</table>


#### 2.2 Forretningsregler for attributtet "legal-entity"

<table>
    <tr>
        <td>ID</td>
        <td> ATT-15 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"legal-entity"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Hovedenheten (den juridisk ansvarlige virksomheten) hvor helsepersonellet jobber sitt org.nr og navn.</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt angivelse av "legal-entity"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Attributtet "legal-entity" SKAL inneholde helsepersonellets virksomhetstilhørighet.<br>
            Det er hovedenheten hvor helsepersonellet yter helsehjelp som skal angis.<br> 
            Verdien for attributtet SKAL være identifikatoren som er registrert i Brønnøysundregisteret.<br><br>
            Eksempler på hovedenhet er:
            <ul>
                <li>Oslo Kommune</li>
                <li>Oslo universitetssykehus HF</li>
            </ul>
            For personell som er innleid og formelt ansatt hos et vikarbyrå eller tilsvarende virksomhet er det ikke virksomheten som helsepersonellet er innleid fra som skal angis, men hovedenheten hvor helsepersonellet yter helsehjelp.
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
        <td> ATT-16 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"legal-entity"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Hovedenheten (den juridisk ansvarlige virksomheten) hvor helsepersonellet jobber sitt org.nr og navn.</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt bruk av attributtet "legal-entity"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen dokumenterer hvilken hovedenhet som er ansvarlig for personellets tilgang, og SKAL inngå i pasientjournalens innsynslogg hos data- og dokumentkilde.<br><br> 
            Denne opplysningen SKAL benyttes ved:
            <ul>
                <li>Lovpålagt dokumentasjon av grunnlaget for tilgang til helseopplysninger hos kilder.</li>
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
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID </td>
        <td>ATT-12</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"legal-entity"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Hovedenheten (den juridisk ansvarlige virksomheten) hvor helsepersonellet jobber sitt org.nr og navn.</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Tilgangsstyring basert på "legal-entity" hos tillitsanker</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td> Identiteten til hovedenheten SKAL benyttes i forbindelse med tilgangsstyring hos Tillitsankeret. Tillitsankeret SKAL kontrollere at hovedenheten:
            <ul>
                <li>har gyldig medlemsskap i Helsenettet</li>
                <li>har akseptert vilkår for medlemssskap i Helsenettet</li>
                <li>har gyldig avtale om tilgang til fellestjenester hovedenheten til enhver tid bruker</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>NHN</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID </td>
        <td> ATT-13 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"legal-entity"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Hovedenheten (den juridisk ansvarlige virksomheten) hvor helsepersonellet jobber sitt org.nr og navn.</td>
    </tr>    
    <tr>
        <td> Beskrivelse av regel </td>
        <td> Krav til sporbarhet for attributtet "legal-entity"</a></td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Attributtet "legal-entity" SKAL entydig og med stor sannsynlighet (uavviselig) knyttes til hovedenheten som har behandlingsansvar for personopplysningene, og som er ansvarlig for ansettelsesforholdet til  helsepersonellet som yter helsehjelp.<br><br>
            Tillitsnivået (LoA) SKAL tilsvare knytningen mellom virksomheten og identifikasjonsmiddel som angitt i identifikasjonsnivåforskriften.<br>
            Det skal være usannsynlig at verdien som angis i "legal-entity" kan endres eller manipuleres i sikkerhetsangrep under transport, eller ved lagring.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Kilde</li>
            </ul>  
        </td>
    </tr>
</table>



#### 2.3 Forretningsregler for attributtet "point-of-care"

<table>
    <tr>
        <td>ID </td>
        <td> ATT-18 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"point-of-care"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Behandlingsstedets org.nr. og navn.</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt angivelse av innholdet i attributtet "point-of-care"</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>Attributtet SKAL inneholde identifikator for helsepersonellets arbeidssted, altså behandlingsstedet som helsepersonellet formelt er tilknyttet.<br> 
        Verdien SKAL angi underenheten som er registrert i Brønnøysundregisteret, hvor helsepersonellet formelt utfører sitt arbeid.<br><br>
        Alle norske virksomheter er påkrevd å rapportere aktivitet per geografisk sted og per registrert næringskode i Brønnøysund. Det antas at de fleste norske virksomheter har registrerte underenheter i Brønnøysundregisteret.
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
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
        <td>ID </td>
        <td> ATT-19 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"point-of-care"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Behandlingsstedets org.nr. og navn.</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td> Angivelse av innholdet i attributtet "point-of-care" for virksomheter uten underliggende enheter</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>For virksomheter uten underenheter registrert i Brønnøysundregistrene SKAL hovedenheten oppgis i "point-of-care".<br>
        Verdien i "legal-entity" og "point-of-care" vil i slike tilfeller være lik.
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
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
        <td> ATT-20 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"point-of-care"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Behandlingsstedets org.nr. og navn.</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt bruk av attributtet "point-of-care".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Attributtet dokumenterer behandlingsstedet hvor helsepersonellet yter helsehjelp når tilgangen til pasientens helseopplysninger ble gitt av konsumenten.<br>
            Attributtet utgjør en del av informasjonen som brukes av data- og dokumentkilder for å dokumentere grunnlaget for at tilgang blir gitt.<br>
            Attributtet vil også brukes hos data- og dokumentkilden i innbyggers innsynslogg for pasienten. 
            Denne opplysningen SKAL benyttes ved:
            <ul>
                <li>Lovpålagt etterfølgende kontroll av tilgangene hos kilder.</li>
                <li>Visning i innbyggers innsynslogg for tilganger dersom dette elementet vurderes å gjøre tilgangene mer forståelige for innbyggere.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

#### 2.4 Forretningsregler for attributtet "department"

<table>
    <tr>
        <td>ID</td>
        <td> ATT-21 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Overordnede regler for bruk av attributtet "department".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Noen virksomheter er organisert i underliggende enheter som ikke er registrert i enhetsregisteret.<br> 
            For slike virksomheter SKAL konsumenten attestere hvilken enhet helsepersonellet tilhører.<br>
            Enhet uten registrering i enhetsregisteret SKAL angis i attributtet "department".<br><br>
            Det er ikke påkrevd å attestere underliggende enheter for virksomheter som ikke er organisert i lunderliggende enheter som ikke er registrert i enhetsregisteret.
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
        <td> ATT-22 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt detaljeringsnivå for attributtet "department".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Riktig detaljeringsnivå for angivelse av attributtet "department" må vurderes av konsumenten.<br>
            Vurderingen kan påvirkes av hvilke registreringer av helsepersonellets organisasjonstilhørighet som finnes i systemet.<br><br>
            Konsumenten bør tilstrebe å angi en verdi som i størst mulig grad bidrar beskriver bakgrunnen for tilgangen.<br><br>
            Prinsipper for detaljeringsnivå ved angivelse av "department":
            <ul>
                <li>bør være et så detaljert nivå som mulig heller enn et mer overordnet nivå</li>
                <li>bør være et nivå pasienten og eksternt helsepersonell har et forhold til</li>
                <li>vurder å avgi enhet som pasienter eller eksternt personell bør kontakte ved spørsmål om gyldig grunnlag for tilgang, hvis det er ønskelig at nærmeste leder er ansvarlig for slike henvendelser</li>
                <li>unngå administrative og formelle nivåer som bare gir mening for internt personell</li>
                <li>unngå å avgi navn på enheter som gjør det mulig å utlede sensitiv kontekst<li>
            </ul>
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
        <td> ATT-23 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt bruk av attributtet "department".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen KAN inngå i attestering av helsepersonellets grunnlaget for tilgang til helseopplysninger, og skal dokumenteres i pasientjournalens innsynslogg.<br>Dersom den er del av attesten vil opplysningen benyttes ved lovpålagt etterfølgende kontroll av tilgangene, samt eventuelt vises i løsningen for digitalt innbyggerinnsyn i tilgangslogg dersom dette elementet på bidrar til å gjøre innslagene i tilgangsloggen mer forståelige for innbyggere.<br> 
            Denne opplysningen KAN benyttes ved:
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
        <td>ATT-25</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Angivelse av verdi for attributtet "department" for kommunale virksomheter </td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td> 
            Attributtet "department" KAN f.eks. brukes for å angi:
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-26</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-28</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>      
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Angivelse av "authority" og "system" ved bruk av lokale identifikatorer for attributtet "department"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>Dersom attributtet "department" er en del av attesten SKAL "System" og "authority" angis selv om konsumenten bruker lokale identifikatorer til å beskrive avdeling/organisasjonsenhet.<br>
        I slike tilfeller SKAL:
        <ul>
            <li>verdien for attributtet "authority" settes til org.nr for juridisk enhet. 
            <li>verdien for attributtet "system" settes til en globalt unik identifikator, som er stabil over tid</li>
            <li>konsumenten skal sørge for at identifikatoren er entydig over tid.</li>
        </ul>        
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
        <td>ATT-24</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-27</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor helsepersonellet yter helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li> 
            </ul>  
        </td>
    </tr>
</table>





#### 2.5 Forretningsregler for attributtet "hpr-nr"
<table>
    <tr>
        <td>ID </td>
        <td> ATT-29 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"hpr-nr"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets HPR-nummer, dersom det finnes</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Angivelse av verdi for attributtet "hpr-nr" for helsepersonell uten lisens/autorisasjon</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Det kan forekomme at helsepersonell uten lisens eller autorisasjon i HPR trenger tilgang på helseopplysninger. Derfor er ikke attributtet "hpr-nr" påkrevd.<br>
            <ul>
                <li>Attributtet "hpr-nr" SKAL angis dersom den fysiske personen har et innslag i HPR.</li>
                <li>Attributtet SKAL utelates fra attesten dersom helsepersonellet ikke har et innslag i HPR</li>
            </ul> 
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

#### 2.6 Forretningsregler for attributtet "authorization"

<table>
    <tr>
        <td>ID</td>
        <td>ATT-32</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"authorization"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets autorisasjon, dersom den finnes</td>
    </tr>                
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Kontroll av korrekte autorisasjoner</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            Alle aktører skal være trygge på at den angitte autorisasjonen eksisterer i helsepersonellregisteret for det aktuelle helsepersonellet.
            <br>
            Dersom den angitte autorisasjonen ikke stemmer overens med autorisasjoner som er registrert i helsepersonellet SKAL forespørselen avvises.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Kilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-31</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"authorization"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets autorisasjon, dersom den finnes</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Håndtering av helsepersonell med flere autorisasjoner i HPR</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            I tilfeller hvor helsepersonellet har flere autorisasjoner i helsepersonellregisteret BØR konsumenten, så godt som mulig, bruke autorisasjonen som ligger nærmest den funksjonelle rollen helsepersonellet har i sin behandling av pasienten.
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



### 3. Forretningsregler for beskrivelse av behandlerrelasjon - attributt: "care-relation"

Attributtet "care-relation" består av fire underliggende attributter, som beskriver behandlerrelasjonen som attesten gjelder for.
|||
| --- | --- | --- |
| care-relation | "healthcare-service"     | Helsetjenestetyper som leveres ved virksomheten                                                   | 
| care-relation | "purpose-of-use"         | Helsepersonellets formål med helseopplysningene (til hva de skal brukes)                          | 
| care-relation | "purpose-of-use-details" | Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes) | 
| care-relation | "decision-ref"           | Referanse til lokal tilgangsbeslutning                                                            | 

#### 3.1 Forretningsregler for attributtet "healthcare-service"

<table>
    <tr>
        <td>ID</td>
        <td>ATT-37</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"healthcare-service"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsetjenestetyper som leveres ved virksomheten</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Angivelse av verdi for attributtet "healthcare-service"</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Konsumerende virksomhet må selv avgjøre hvilke verdier for angivelse av attributtet "healthcare-service" som best beskriver typen helsetjeneste som leveres ved virksomheten hvor helsepersonellet yter helsehjelp.<br><br>
            Det er flere kodeverk som er aktuelle for å beskrive helsehjelpstjeneste, de fleste er koblet til tjenestebasert adressering, se detaljert beskrivelse under attributtet i informasjonsmodellen.<br>
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-33</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"healthcare-service"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsetjenestetyper som leveres ved virksomheten</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Bruk av "healthcare-service" for å angi helsehjelpstjeneste</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Attributtet "healthcare-service" (helsehjelpstjeneste) angir hvilken type helsetjenester som leveres/ytes til pasienten ved virksomheten der helsepersonellet jobber. Helsehjelpstjenesten som dokumenteres inngår i grunnlaget for at helsepersonellet trenger tilgang til pasientens helseopplysninger.<br>
            Et alternativ til begrepet <em>helsehjelpstjeneste</em> er <em>fagområde</em>, som beskriver det tilsvarende grunnlaget i spesialisthelsetjenesten.
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
        <td> ATT-34 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"healthcare-service"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsetjenestetyper som leveres ved virksomheten</td>
    </tr>        
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt bruk av attributtet "healthcare-service".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Attributtet "healthcare-service" skal inngå i attesten som i sum dokumenterer grunnlaget for at tilgang blir gitt, og skal inngå i innbyggers innsynslogg. Denne opplysningen vil benyttes ved lovpålagt etterfølgende kontroll av tilgangene, samt eventuelt vises i innbyggerens innsynslogg for tilganger dersom dette elementet gjør tilgangene mer forståelige for innbyggere.<br> 
            Denne opplysningen SKAL benyttes ved:
            <ul>
                <li>Lovpålagt etterfølgende kontroll av tilgangene hos kilder.</li>
                <li>Visning i løsningen for digitalt innbyggerinnsyn i tilgangslogg fra kilder for å gjøre tilgangene mer forståelige for innbyggere.</li>
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
        <td>ATT-35</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"healthcare-service"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsetjenestetyper som leveres ved virksomheten</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Håndtering av tilfeller hvor det finnes flere mulige verdier for helsehjelpstjeneste eller fagområde knyttet til tilganger som helsepersonellet har til pasienten</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Ved flere mulige verdier for helsehjelptjeneste eller fagområde knyttet til tilganger som helsepersonellet har til pasienten skal verdien som i størst mulig grad kan bidra til å avklare hva som er bakgrunnen for tilgangen vektlegges.<br>
            Som hovedregel bør det være så presist som mulig heller enn et mer overordnet nivå, men likevel et nivå pasienten og eksternt helsepersonell med størst sannsynlighet har et forhold til.
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
        <td>ATT-36</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"healthcare-service"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsetjenestetyper som leveres ved virksomheten</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Håndtering av tilfeller hvor helsehjelpstjeneste eller fagområde ikke er knyttet til tilganger som helsepersonellet har til pasienten</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Det er ikke alltid slik at helsehjelpstjeneste eller fagområde er registrert og knyttet til tilganger som helsepersonellet har til pasienten, for eksempel:
            <ul>
                <li>Når pasienten ikke er i et planlagt forløp hos virksomheten, men behandles eksternt</li>
                <li>Dersom pasienten ønsker dialog i etterkant av et avsluttet forløp</li>
                <li>Det har oppstått en akuttsituasjon som krever rask tilgang til pasienten</li>
            </ul>
            I slike tilfeller vil det ikke være nødvendig å oppgi verdi for attributtet "healthcare-service".<br>
            For spesialisthelsetjenesten skal manglende verdi i "healthcare-service" kunne forklares av verdien som formidles i "purpose-of-use-details".
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




#### 3.2 Forretningsregler for attributtet "purpose-of-use"

<table>
    <tr>
        <td>ID</td>
        <td>ATT-38</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-39</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-40</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-41</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>    
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>

#### 3.3 Forretningsregler for attributtet "purpose-of-use-details"

<table>
    <tr>
        <td>ID</td>
        <td>ATT-43</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use-details"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Overordnede retningslinjer for angivelse av "purpose-of-use-details"</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            Intensjonen bak attesteringen er å best mulig kunne formidle grunnlaget for tilgang som er dokumentert i helsepersonellets virksomhet.<br>
            Attributtet "purpose-of-use-details" skal formidle den spesifikke hendelsen aller aktiviteten som er bakgrunnen for at helsepersonellet har fått tilgang til pasientens helseopplysninger i egen virksomhet.<br> 
            Dette attributtet utfyller andre attributter, slik at det i sum dannes et forståelig bilde av bakgrunnen for tilgangen.<br>
            Begrepene "hendelse" eller "aktivitet" er ikke nødvendigvis gode begreper for alle virksomhetstyper eller alle typer helsehjelpstjenester.<br>
            <br>
            Et utgangspunkt for å vurdere hvilke registreringer som er best egnet for å avgi riktig informasjon i attributtet kan være følgende to scenarier:
            <ul>
                <li>Hvordan dokumenteres den spesifikke tilgangen et helsepersonell har fått når pasient mottar helsehjelp i øyeblikket</li>
                <li>Hvordan dokumenteres tilsvarende tilgang når pasienten tidligere mottok helsehjelp fra virksomheten som nå er avsluttet, og det i ettertid er nødvendig med ny tilgang fra det samme helsepersonellet for eksempel som følge av en henvendelse fra pasienten eller pasientens nåværende behandler der de yter helsehjelp til pasienten?</li>
            </ul>
            <br>
            I spesialisthelsetjenesten kan en <em>hendelse</em> eller <em>aktivitet</em> for eksempel være at en pasient:
            <ul>
                <li>trenger å få vurdert en henvisning,</li>
                <li>er planlagt å møte til en konsultasjon,</li>
                <li>er under behandling i en poliklinisk konsultasjon eller er innlagt,</li>
                <li>skal følges opp av helsepersonellet som er på vakt eller lignende.</li>
            </ul>
            Det kan også være at pasienten, pasientens pårørende/verge eller pasientens eksterne behandler har tatt kontakt med helsepersonellet som gjør det nødvendig for helsepersonellet å få tilgang til pasientens helseopplysninger for å sikre at riktig helsehjelp blir gitt til pasienten.<br>
            Et eksempel på kodeverk som representer spesialisthelsetjenestens aktuelle aktiviteter/hendelser finnes som et utgangspunkt for eventuell nasjonal standardisering hos HL7 Norge.
            <br>
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
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
        <td>ATT-45</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use-details"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Foreslåtte kodeverk for angivelse av verdi for "purpose-of-use-details"</td>
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
            For avtalespesialister er relevante eksempler ...<br>
            Hos legekontor er det ofte ...<br>
            <br>
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
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
        <td> ATT-42 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use-details"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>        
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt bruk av attributtet "purpose-of-use-details".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen vil sammen med annen informasjon i attesten dokumentere grunnlaget for at tilgang blir gitt, og kan inngå i pasientjournalens innsynslogg. Denne opplysningen vil benyttes ved lovpålagt etterfølgende kontroll av tilgangene, samt eventuelt vises i innbyggers innsynslogg for tilganger gitt hos datakilder dersom informasjonen gjør tilgangene mer forståelige for innbyggere.<br> 
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
        <td>ATT-44</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"purpose-of-use-details"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Detaljert beskrivelse av helsepersonellets formål med helseopplysningene (til hva de skal brukes)</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Retningslinjer dersom det finnes flere mulige verdier for "purpose-of-use-details"</td>
    </tr>
    <tr>    
        <td>Regel</td>
        <td>
            Ved flere mulige valg bør det vektlegges hva som i størst mulig grad kan bidra til å avklare hva som er bakgrunnen for tilgangen.<br> 
            Som hovedregel bør det være så presist som mulig heller enn et mer overordnet nivå, men likevel et nivå pasienten og eksternt helsepersonell med størst sannsynlighet har et forhold til.
        </td>
    </tr>
    <tr>
        <td>Ansvarlig</td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
            </ul>  
        </td>
    </tr>
</table>



#### 3.4 Forretningsregler for attributtet "decision-ref"

<table>
    <tr>
        <td>ID</td>
        <td> ATT-46 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"decision-ref"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Referanse til lokal tilgangsbeslutning</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Formål med, og bruk av attributtet "decision-ref".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Attributtet skal formidle informasjon om helsepersonellet har tatt seg selv tilgang (selvautorisasjon), eller om det er en automatisert (systemavledet) tilgangsbeslutning. Det er også tilrettelagt for at en mer utdypende systemavledet beskrivelse kan formidles for å sikre best mulig forståelse av grunnlaget for tilgangen.
            <br>
            Formålet med dette attributtet er at alle parter i en kjede av involverte virksomheter og systemer, skal kunne gjenfinne logginnslag som har opphav fra den opprinnelige tilgangsbeslutningen hos konsument.<br><br>
            Denne opplysningen SKAL benyttes på følgende måte:
            <ul>
                <li>Dersom etterfølgende kontroll av tilgangene hos kilder fører til behov for videre oppfølging hos konsument skal "decision-ref" oppgis ved henvendelser.</li>
                <li>Dersom "decision-ref" oppgis ved henvendelse fra data- eller dokumentkilde skal det være mulig for konsument å framstille informasjon som beskriver beslutningen om tilgang i sitt system, slik at de kan vurdere hvorvidt tilgangen var gyldig.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td>ATT-47</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"decision-ref"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Referanse til lokal tilgangsbeslutning</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Overordnet beskrivelse av angivelse av verdi for attributtet "decision-ref".</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            Attributtet er en referanse til den lokale tilgangsbeslutningen hos konsumenten.<br> 
            Med tilgangsbeslutning menes det som er dokumentert hos en konsument i forbindelse med at et helsepersonell har fått tilgang:<br><br>
            Vi skiller mellom to brukstilfeller for verdien i attributtet "decision-ref":
            <ul>
                <li>tilgang til flere pasienter</li>
                <li>tilgang til en spesifikk pasient</li>
            </ul>
            <strong>Tilgang til flere pasienter</strong><br>
            Etter pålogging i lokalt EPJ vil helsepersonellet navigere seg fram til de aktuelle pasientene de skal yte helsehjelp til.<br> 
            Helsepersonellet må da gis tilgang til en oversikt over pasienter som de potensielt skal behandle. . 
            <br>
            I tilfeller hvor oversikten hentes fra andre virksomheter er det <em>referanse til denne tilgangsbeslutningen som skal oppgis</em><br>
            <br><br>
            <strong>Tilgang til en spesifikk pasient</strong><br>
            Hvis helsepersonellet trenger tilgang til mer detaljert informasjon om en spesifikk pasient må det foreligge en referanse til den <em>spesifikke tilgangsbeslutningen for tilgang til denne pasienten</em>.<br>
            Tilgangsbeslutningen er utgangspunktet for videre tilgang til andre virksomheter og nasjonale løsninger.<br> 
            Det er den mest spesifikke tilgangsbeslutningen som til enhver tid skal identifiseres.
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
        <td>ATT-48</td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"decision-ref"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Referanse til lokal tilgangsbeslutning</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
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
                <li>Konsument</li>
                <li>Dokumentkilde</li>
                <li>NHN</li>
            </ul>  
        </td>
    </tr>
</table>

### 4. Forretningsregler for beskrivelse av pasienten - attributt: "patient"
Attributtet "patient" består av tre underliggende attributter som beskriver pasienten attesten gjelder for. 

| | | |
| --- | --- | --- |
| patient       | "identifier"             | Unik identifikator for pasienten                                                                  | 
| patient       | "point-of-care"  	       | Virksomheten hvor pasienten mottar behandling <br>Kan være lik verdi som i "legal-entity"         | 
| patient       | "department"             | Avdeling/org.enhet hvor pasienten mottar helsehjelp                                        	   | 


#### 4.1 Forretningsregler for attributtet "identifier" for pasient

#### 4.2 Forretningsregler for attributtet "point-of-care" for pasient

<table>
    <tr>
        <td>ID</td>
        <td> ATT-49 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"point-of-care"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Virksomheten hvor pasienten mottar behandling</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Angivelse av attributtet "point-of-care" for pasient.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Attributtet skal inneholde pasientens behandlingssted så fremt behandlingen foregår i helsepersonellets egen virksomhet, og det er registrert en kontakt med en organisasjonsenhet i helsepersonellets egen virksomhet som er grunnlaget for tilgangen. Det er den registrerte underenheten i Brønnøysundregisteret som pasientens kontakt tilhører som skal oppgis.
            <br>
            Det er et generelt krav til alle norske virksomheter at aktivitet skal kunne rapporteres per geografisk sted og per registrert næringskode i Brønnøysund som det drives virksomhet ved, og derfor skal det være registrert slike underenheter i Brønnøysundregisteret for de fleste virksomheter i Norge.
            <br>
            Det er altså kun når pasienten har en registrert kontakt i helsepersonellets egen virksomhet, og helsehjelp knyttet til denne kontakten er grunnlaget for at helsepersonellet trenger tilgang til helseopplysningene for pasienten, at dette attributtet skal formidle den offisielle underenheten pasienten har sin registrerte kontakt ved. Informasjonen skal formidles uavhengig av om helsepersonellet trenger tilgangen som følge av helsehjelp de selv yter direkte til pasienten, eller indirekte som følge av at de trenger tilgangen for å bistå kolleger i egen virksomhet.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-50 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"point-of-care"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Virksomheten hvor pasienten mottar behandling</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Angivelse av attributtet "point-of-care" for pasient for virksomheter uten underenheter.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            For virksomheter som eventuelt ikke har registrert noen underliggende enheter i Brønnøysundregistrene skal den overordnede enheten oppgis i dette attributtet så lenge kriteriene for at dette attributtet skal brukes er oppfylt.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-51 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"point-of-care"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Virksomheten hvor pasienten mottar behandling</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Unntak fra bruk av attributtet "point-of-care" for pasient.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Dersom pasienten behandles ved en annen virksomhet enn helsepersonellets, for eksempel ved behov for tilgang for å kunne bistå en kollega i en annen virksomhet som har pasienten til behandling hos seg, eller dersom pasienten selv eller pårørende har henvendt seg uten at dette er knyttet til en registrert kontakt med helsepersonellets virksomhet, skal ikke dette attributtet benyttes.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-52 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"point-of-care"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Virksomheten hvor pasienten mottar behandling</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt bruk av attributtet "point-of-care" for pasient.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen vil i første rekke benyttes som et av flere elementer fra attesten som i sum dokumenterer grunnlaget for at tilgang blir gitt, og dermed inngå i pasientjournalens innsynslogg. Denne opplysningen vil benyttes ved lovpålagt etterfølgende kontroll av tilgangene, samt eventuelt vises i løsningen for digitalt innbyggerinnsyn i tilgangslogg fra datakilder dersom dette elementet på generelt grunnlag vurderes å gjøre tilgangene mer forståelige for innbyggere.<br> 
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



#### 4.3 Forretningsregler for attributtet "department" for pasient
<table>
    <tr>
        <td>ID</td>
        <td> ATT-53 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor pasienten mottar helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Overordnede regler for bruk av attributtet "department" for pasient.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>
            I virksomheter som er organisert i flere lokalt definerte underliggende enheter enn de som fremkommer av offentlig registrering i Brønnøysundregistrene, er det et krav at attesten formidler informasjon om hvilken av disse lokalt definerte enhetene pasienten mottar behandling ved i forbindelse med tilgangen helsepersonellet ønsker å oppnå. Det er ikke et krav om å formidle noe i dette attributtet fra virksomheter uten lokalt definerte underliggende enheter ut over det som fremkommer av offentlig registrering i Brønnøysundregistrene.
            <br>
            Det er altså kun når pasienten har en registrert kontakt i helsepersonellets egen virksomhet, og helsehjelp knyttet til denne kontakten er grunnlaget for at helsepersonellet trenger tilgang til helseopplysningene for pasienten, at dette attributtet skal formidle enheten pasienten har sin registrerte kontakt ved. Informasjonen skal formidles uavhengig av om helsepersonellet trenger tilgangen som følge av helsehjelp de selv yter direkte til pasienten, eller indirekte som følge av at de trenger tilgangen for å bistå kolleger i egen virksomhet.
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
        <td> ATT-54 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor pasienten mottar helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt detaljeringsnivå for attributtet "department" for pasient.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Hvilket detaljeringsnivå innenfor et potensielt større hierarki av lokalt definerte enheter som er riktig å legge i attesten må vurderes av konsumentvirksomheten, ut fra hva som i størst mulig grad bidrar til å avklare hva som er bakgrunnen for tilgangen. Som hovedregel bør dette være et så detaljert nivå som mulig heller enn et mer overordnet nivå, og likevel et nivå pasienten og eksternt helsepersonell med størst sannsynlighet har et forhold til fremfor mer administrative og formelle nivåer som bare internt personell forholder seg til.<br> 
            I noen tilfeller kan det være behov for å avgi et mer overordnet nivå av hensyn til behov for særlig diskresjon som virksomheten måtte ha behov for ved enkelte mer spesielle enheter.
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
        <td> ATT-55 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor pasienten mottar helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Angivelse av attributtet "department" for pasient ved virksomheter uten underenheter.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            For virksomheter som eventuelt ikke har registrert noen underliggende enheter i Brønnøysundregistrene skal den overordnede enheten oppgis i dette attributtet så lenge kriteriene for at dette attributtet skal brukes er oppfylt.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-56 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor pasienten mottar helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Unntak fra bruk av attributtet "department" for pasient.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Dersom pasienten behandles ved en annen virksomhet enn helsepersonellets, for eksempel ved behov for tilgang for å kunne bistå en kollega i en annen virksomhet som har pasienten til behandling hos seg, eller dersom pasienten selv eller pårørende har henvendt seg uten at dette er knyttet til en registrert kontakt med helsepersonellets virksomhet, skal ikke dette attributtet benyttes.
        </td>
    </tr>
    <tr>
        <td> Ansvarlig </td>
        <td>
            Denne regelen skal håndheves av:
            <ul>
                <li>Konsument</li>
                <li>NHN</li>
                <li>Dokumentkilde</li>
            </ul>  
        </td>
    </tr>
</table>

<table>
    <tr>
        <td>ID</td>
        <td> ATT-57 </td>
    </tr>
    <tr>
        <td>Attributt</td>
        <td>"department"</td>
    </tr>
    <tr>
        <td>Beskrivelse av attributt</td>
        <td>Avdeling/org.enhet hvor pasienten mottar helsehjelp</td>
    </tr>
    <tr>
        <td>Beskrivelse av regel</td>
        <td>Korrekt bruk av attributtet "point-of-care" for pasient.</td>
    </tr>
    <tr>    
        <td> Regel </td>
        <td>  
            Informasjonen inngår som et av flere elementer fra attesten som dokumenterer grunnlaget for at tilgang blir gitt, og dermed inngå i innbyggers innsynslogg. Denne opplysningen vil benyttes ved lovpålagt etterfølgende kontroll av tilgangene, samt eventuelt vises i løsningen for innbyggers innsynslogg for tilganger fra datakilder dersom dette elementet gjør tilgangene mer forståelige for innbyggere.<br> 
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