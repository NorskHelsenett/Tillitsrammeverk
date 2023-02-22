# Sammenligning av helsepersonellets rolle fra forskjellige kilder

Dette dokumentet inneholder en oversikt over flere forskjellige kodesystemer
* HL7: Practitioner role
* HPR: Autorisasjoner
* Styrk-08 (ISCO-08)
* HSØ roller
* Snomed-ct: Practitioner role

## HL7 - Practitioner Role
Url: https://terminology.hl7.org/5.0.0/CodeSystem-practitioner-role.html

oid: urn:oid:2.16.840.1.113883.4.642.1.1132


| Kode          | Kategori          | Definisjon |
| ---           | ---               | --- |
| doctor        | Doctor            | A qualified/registered medical practitioner |
| nurse         | Nurse             | A practitioner with nursing experience that may be qualified/registered |
| pharmacist    | Pharmacist        | A qualified/registered/licensed pharmacist |
| researcher    | Researcher        | A practitioner that may perform research |
| teacher       | Teacher/educator  | Someone who is able to provide educational services |
| ict           | ICT professional  | Someone who is qualified in Information and Communication Technologies |


## Autorisasjoner i HPR
Definisjon: https://lovdata.no/lov/1999-07-02-64/§48

oid: 9060

Volven: https://volven.no/produkt.asp?open_f=true&id=492955&catID=3&subID=8&subCat=61&oid=9060

| Kode | Kategori |
| --- | --- |
| AA | Ambulansearbeider            |
| AT | Apotektekniker               |
| AU | Audiograf                    |
| BI | Bioingeniør                  |
| ET | Ergoterapeut                 |
| FA | Provisorfarmasøyt            |
| FA | Reseptarfarmasøyt            |
| FB | Fiskehelsebiolog             |
| FO | Fotterapeut                  |
| FT | Fysioterapeut                |
| HE | Helsesekretær                |
| HF | Helsefagarbeider             |
| HP | Hjelpepleier                 |
| JO | Jordmor                      |
| KE | Klinisk ernæringsfysiolog    |
| KI | Kiropraktor                  |
| LE | Lege                         |
| NP | Naprapat                     |
| OA | Omsorgsarbeider              |
| OI | Ortopediingeniør             |
| OP | Optiker                      |
| OR | Ortoptist                    |
| OS | Osteopat                     |
| PE | Perfusjonist                 |
| PM | Paramedisiner                | 
| PS | Psykolog                     |
| RA | Radiograf                    |
| SP | Sykepleier                   |
| TH | Tannhelsesekretær            |
| TL | Tannlege                     |
| TP | Tannpleier                   |
| TT | Tanntekniker                 |
| VE | Veterinær                    |
| VP | Vernepleier                  |
| XX | Ukjent/uspesifisert          |
| MT | Manuellterapeut              |

## Styrk-08 (ISCO-08)
FNs yrkesklassifisering

Brukes for å beskrive "funksjonell rolle" i EHDSI

| Kode | Klassifisering | HPR |
| --- | --- | --- |
| **221**  | **Leger**                                           | -  |
| 2211     | Allmennpraktiserende leger                          | LE |
| 2212     | Legespesialister                                    | LE |
| **222**  | **Sykepleiere og spesialsykepleiere**               | -  |
| 2221     | Spesialsykepleiere                                  | SP |
| 2222     | Jordmødre                                           | JO |
| 2223     | Sykepleiere                                         | SP |
| 2224     | Vernepleiere                                        | VP |
| **225**  | **Veterinærer**                                     | -  |
| 2250     | Veterinærer                                         | VE |
| **226**  | **Andre medisinske yrker**                          | -  |
| 2261     | Tannleger                                           | TL |
| 2262     | Farmasøyter                                         | FA |
| 2263     | Helse- og miljørådgivere                            |    |
| 2264     | Fysioterapeuter                                     | FT |
| 2265     | Ernæringsfysiologer                                 | KE |
| 2266     | Audiografer og logopeder                            | AU |
| 2267     | Ergoterapeuter                                      | ET |
| 2269     | Kiropraktorer mv.                                   | KI |
| **32**   | **Helserelaterte yrker**                            | -  |
| **321**  | **Radiografer, proteseteknikere, reseptarer mv.**   | -  |
| 3211     | Radiografer mv.                                     | RA |
| 3212     | Bioingeniører                                       | BI |
| 3213     | Reseptarer                                          | ?  |
| 3214     | Protese- og tannteknikere                           |    |
| **323**  | **Yrker innen alternativ medisin**                  | -  |
| 3230     | Yrker innen alternativ medisin                      |    |
| **324**  | **Dyrepleiere**                                     | -  |
| 3240     | Dyrepleiere                                         |    |
| **325**  | **Andre helseyrker**                                | -  |
| 3251     | Tannpleiere                                         | TP |
| 3254     | Optikere                                            | OP |
| 3256     | Helsesekretærer                                     | HE |
| 3257     | Helse- og miljøkontrollører                         |    |
| 3258     | Ambulansepersonell                                  | AA |
| 3259     | Andre helseyrker                                    |    |
| **53**   | **Pleie- og omsorgsarbeidere**                      | -  |
| **532**  | **Pleiemedarbeidere**                               | -  |
| 5321     | Helsefagarbeidere                                   | HF |
| 5322     | Hjemmehjelper                                       | ?  |
| 5329     | Andre pleiemedarbeidere                             | ?  |

## HSØ sine rolledefinisjoner

| HPR | Nasjonalt rollenavn | Kommentar |
| --- | --- | --- |
| 	| Aktivitør	| |
| 	| Anestesisykepleier | |
| 	| Arkiv og skanning	| Regionene har i dag mange varianter av denne rollen |
| 	| Assistent	| Tidligere "pleieassistent" hos noen |
| X	| Audiograf	| |
| 	| Audiografstudent	| |
| 	| Barnepleier	| |
| X	| Bioingeniør	| |
| 	| Bioingeniørstudent	| |
| 	| Brukerstøtte IKT	| For bemanning på IKT-organisasjonenes Helpdesk. Se også systemforvaltningsrollene. |
| X	| Ergoterapeut	| |
| 	| Ergoterapeutstudent	| |
| 	| Farmasøyt	| |
| 	| Farmasøytstudent	| |
| 	| Forløpskoordinator| Omfatter pasientflyt/Ventelistekoordinator/Inntakskonsulent/Operasjonskoordinator |
| 	| Forsker	| |
| 	| Fotograf	| |
| 	| Fysiker	| |
| 	| Fysikerstudent	| |
| X	| Fysioterapeut	| |
| 	| Fysioterapeutstudent	| |
| 	| Genetisk veileder	| |
| X | Helsefagarbeider	| |
| 	| Helsefagarbeiderlærling	| |
| 	| Idrettspedagog	| |
| 	| Intensivsykepleier	| |
| 	| Intensivsykepleierstudent	| |
| X	| Jordmor	| |
| 	| Jordmorstudent	| |
| X	| Kiropraktor	| |
| X	| Klinisk ernæringsfysiolog	| |
| 	| Klinisk ernæringsfysiologstudent	| |
| 	| Kodekontroller	| |
| 	| Kontrollkommisjon	| Kontrollkommisjonen er innenfor psykiatri. Se også rollen Tilsynsmyndighet |
| 	| Kvalitetssikring	| Kodekontroll, kontroll journalføring, stikkprøvekontroll av journalsnoking, etc |
| 	| Leder	| |
| X	| Lege	| Tre legeroller: Overlege, Lege og Turnuslege |
| 	| Legestudent	| |
| 	| Logoped	| |
| 	| Logopedstudent	| |
| 	| Miljøterapeut	| Stort sett samme tilganger som sykepleier |
| 	| Musikkterapeut	| |
| 	| Operasjonssykepleier | |	
| X	| Optiker	| |
| X	| Ortopediingeniør	| |
| X	| Ortoptist | Øyespesialist, ikke lege |
| 	| Overlege	| Tre legeroller: Overlege, Lege og Turnuslege |
| 	| Pedagog	| |
| X	| Perfusjonist | |	
| X	| Psykolog	| |
| 	| Psykologspesialist	| |
| 	| Psykologstudent	| |
| X	| Radiograf	| |
| 	| Radiografstudent	| |
| 	| Sekretær	| Regionene har mange varianter av denne rollen, bl.a. "Kontor" og "Postsekretær" |
| 	| Sekretær lab/radiologi	| |
| 	| Sentralbord	| |
| 	| Sexolog	| |
| 	| Skrivetjenester	| |
| 	| Sosionom	| |
| 	| Sosionomstudent	| |
| 	| Stråleterapeut	| |
| X	| Sykepleier	| |
| 	| Sykepleierstudent	| |
| 	| Systemforvaltning EPJ	| Vedlikehold av kodeverk, sikre regionale standarder, etc., både HF og IKT |
| 	| Systemforvaltning Lab | Vedlikehold av kodeverk, sikre regionale standarder, etc., både HF og IKT |
| 	| Systemforvaltning Radiologi | Vedlikehold av kodeverk, sikre regionale standarder, etc., både HF og IKT |
| X	| Tannlege	| |
| X	| Tannpleier	| |
| 	| Tilsynsmyndighet | Tidsbegrenset tilgang for eksternt tilsyn |
| 	| Turnuslege | Tre legeroller: Overlege, Lege og Turnuslege |
| X	| Vernepleier	| |
| 	| Vernepleierstudent	| |
| 	| Yrkeshygieniker	| |
| 	| Økonomi analyse	| Brukes der de to øvrige økonomirollene vil gi for store tilganger. |
| 	| Økonomi kontroller HF | Økonomiansatte som trenger tilgang til journalinformasjon for å kontrollere DRG og medisinske registreringer. |
| 	| Økonomi regnskap	| For ansatte i økonomiavdelinger |


## SNOMED CT
Hentet fra [HL7-FHIR R4](http://hl7.org/fhir/R4/valueset-practitioner-role.html)
oid: 2.16.840.1.113883.4.642.3.439


| Code | System | Display |
| --- | --- | --- | 
| 1421009 | http://snomed.info/sct | Specialized surgeon | 
| 3430008 | http://snomed.info/sct | Radiation therapist	
| 3842006 | http://snomed.info/sct | Chiropractor	|
| 4162009 | http://snomed.info/sct | Dental assistant |
| 5275007 | http://snomed.info/sct | NA - Nursing auxiliary	|
| 6816002 | http://snomed.info/sct | Specialized nurse	|
| 6868009 | http://snomed.info/sct | Hospital administrator	|
| 8724009 | http://snomed.info/sct | Plastic surgeon	|
| 11661002 | http://snomed.info/sct	| Neuropathologist	|
| 11911009 | http://snomed.info/sct	| Nephrologist	|
| 11935004 | http://snomed.info/sct	| Obstetrician	|
| 13580004 | http://snomed.info/sct	| School dental assistant	|
| 14698002 | http://snomed.info/sct	| Medical microbiologist	|
| 17561000 | http://snomed.info/sct	| Cardiologist	|
| 18803008 | http://snomed.info/sct	| Dermatologist	|
| 18850004 | http://snomed.info/sct	| Laboratory hematologist	|
| 19244007 | http://snomed.info/sct	| Gerodontist	|
| 20145008 | http://snomed.info/sct	| Removable prosthodontist	|
| 21365001 | http://snomed.info/sct	| Specialized dentist	|
| 21450003 | http://snomed.info/sct	| Neuropsychiatrist	|
| 22515006 | http://snomed.info/sct	| Medical assistant	|
| 22731001 | http://snomed.info/sct	| Orthopedic surgeon	|
| 22983004 | http://snomed.info/sct	| Thoracic surgeon	|
| 23278007 | http://snomed.info/sct	| Community health physician	|
| 24430003 | http://snomed.info/sct	| Physical medicine specialist	|
| 24590004 | http://snomed.info/sct	| Urologist	|
| 25961008 | http://snomed.info/sct	| Electroencephalography specialist	|
| 26042002 | http://snomed.info/sct	| Dental hygienist	|
| 26369006 | http://snomed.info/sct	| Public health nurse	|
| 28229004 | http://snomed.info/sct	| Optometrist	|
| 28411006 | http://snomed.info/sct	| Neonatologist	|
| 28544002 | http://snomed.info/sct	| Chemical pathologist	|
| 36682004 | http://snomed.info/sct	| PT - Physiotherapist	|
| 37154003 | http://snomed.info/sct	| Periodontist	|
| 37504001 | http://snomed.info/sct	| Orthodontist	|
| 39677007 | http://snomed.info/sct	| Internal medicine specialist	|
| 40127002 | http://snomed.info/sct	| Dietitian (general)	|
| 40204001 | http://snomed.info/sct	| Hematologist	|
| 40570005 | http://snomed.info/sct	| Interpreter	|
| 41672002 | http://snomed.info/sct	| Respiratory physician	|
| 41904004 | http://snomed.info/sct	| Medical X-ray technician	|
| 43702002 | http://snomed.info/sct	| Occupational health nurse	|
| 44652006 | http://snomed.info/sct	| Pharmaceutical assistant	|
| 45419001 | http://snomed.info/sct	| Masseur	|
| 45440000 | http://snomed.info/sct	| Rheumatologist	|
| 45544007 | http://snomed.info/sct	| Neurosurgeon	|
| 45956004 | http://snomed.info/sct	| Sanitarian	|
| 46255001 | http://snomed.info/sct	| Pharmacist	|
| 48740002 | http://snomed.info/sct	| Philologist	|
| 49203003 | http://snomed.info/sct	| Dispensing optometrist	|
| 49993003 | http://snomed.info/sct	| Maxillofacial surgeon	|
| 50149000 | http://snomed.info/sct	| Endodontist	|
| 54503009 | http://snomed.info/sct	| Faith healer	|
| 56397003 | http://snomed.info/sct	| Neurologist	|
| 56466003 | http://snomed.info/sct	| Community physician	|
| 56542007 | http://snomed.info/sct	| Medical record administrator	|
| 56545009 | http://snomed.info/sct	| Cardiovascular surgeon	|
| 57654006 | http://snomed.info/sct	| Fixed prosthodontist	|
| 59058001 | http://snomed.info/sct	| General physician	|
| 59169001 | http://snomed.info/sct	| Orthopedic technician	|
| 59944000 | http://snomed.info/sct	| Psychologist	|
| 60008001 | http://snomed.info/sct	| Community-based dietitian	|
| 61207006 | http://snomed.info/sct	| Medical pathologist	|
| 61246008 | http://snomed.info/sct	| Laboratory medicine specialist	|
| 61345009 | http://snomed.info/sct	| Otorhinolaryngologist	|
| 61894003 | http://snomed.info/sct	| Endocrinologist	|
| 62247001 | http://snomed.info/sct	| Family medicine specialist	|
| 63098009 | http://snomed.info/sct	| Clinical immunologist	|
| 66476003 | http://snomed.info/sct	| Oral pathologist	|
| 66862007 | http://snomed.info/sct	| Radiologist	|
| 68867008 | http://snomed.info/sct	| Public health dentist	|
| 68950000 | http://snomed.info/sct	| Prosthodontist	|
| 69280009 | http://snomed.info/sct	| Specialized physician	|
| 71838004 | http://snomed.info/sct	| Gastroenterologist	|
| 73265009 | http://snomed.info/sct	| Nursing aid	|
| 75271001 | http://snomed.info/sct	| MW - Midwife	|
| 76166008 | http://snomed.info/sct	| Practical aid (pharmacy)	|
| 76231001 | http://snomed.info/sct	| Osteopath	|
| 76899008 | http://snomed.info/sct	| Infectious diseases physician	|
| 78703002 | http://snomed.info/sct	| General surgeon	|
| 78729002 | http://snomed.info/sct	| Diagnostic radiologist	|
| 79898004 | http://snomed.info/sct	| Auxiliary midwife	|
| 80409005 | http://snomed.info/sct	| Translator	|
| 80546007 | http://snomed.info/sct	| OT - Occupational therapist	|
| 80584001 | http://snomed.info/sct	| Psychiatrist	|
| 80933006 | http://snomed.info/sct	| Nuclear medicine physician	|
| 81464008 | http://snomed.info/sct	| Clinical pathologist	|
| 82296001 | http://snomed.info/sct	| Pediatrician	|
| 83189004 | http://snomed.info/sct	| Other professional nurse	|
| 83273008 | http://snomed.info/sct	| Anatomic pathologist	|
| 83685006 | http://snomed.info/sct	| Gynecologist	|
| 85733003 | http://snomed.info/sct	| General pathologist	|
| 88189002 | http://snomed.info/sct	| Anesthesiologist	|
| 88475002 | http://snomed.info/sct	| Other dietitians and public health nutritionists	|
| 90201008 | http://snomed.info/sct	| Pediatric dentist	|
| 90655003 | http://snomed.info/sct	| Care of the elderly physician	|
| 106289002 | http://snomed.info/sct | Dental surgeon	|
| 106291005 | http://snomed.info/sct | Dietician AND/OR public health nutritionist	|
| 106292003 | http://snomed.info/sct | Nurse	|
| 106293008 | http://snomed.info/sct | Nursing personnel	|
| 106294002 | http://snomed.info/sct | Midwifery personnel|	
| 106296000 | http://snomed.info/sct | Physiotherapist AND/OR occupational therapist	|
| 106330007 | http://snomed.info/sct | Philologist, translator AND/OR interpreter	|
| 112247003 | http://snomed.info/sct | Medical doctor	|
| 158965000 | http://snomed.info/sct | Medical practitioner |	
| 158966004 | http://snomed.info/sct | Medical administrator - national	|
| 158967008 | http://snomed.info/sct | Consultant physician	|
| 158968003 | http://snomed.info/sct | Consultant surgeon	|
| 158969006 | http://snomed.info/sct | Consultant gynecology and obstetrics	|
| 158970007 | http://snomed.info/sct | Anesthetist	|
| 158971006 | http://snomed.info/sct | Hospital registrar	|
| 158972004 | http://snomed.info/sct | House officer	|
| 158973009 | http://snomed.info/sct | Occupational physician	|
| 158974003 | http://snomed.info/sct | Clinical medical officer	|
| 158975002 | http://snomed.info/sct | Medical practitioner - teaching	|
| 158977005 | http://snomed.info/sct | Dental administrator	|
| 158978000 | http://snomed.info/sct | Dental consultant	|
| 158979008 | http://snomed.info/sct | Dental general practitioner	|
| 158980006 | http://snomed.info/sct | Dental practitioner - teaching|	
| 158983008 | http://snomed.info/sct | Nurse administrator - national|	
| 158984002 | http://snomed.info/sct | Nursing officer - region	|
| 158985001 | http://snomed.info/sct | Nursing officer - district|	
| 158986000 | http://snomed.info/sct | Nursing administrator - professional body	|
| 158987009 | http://snomed.info/sct | Nursing officer - division	|
| 158988004 | http://snomed.info/sct | Nurse education director	|
| 158989007 | http://snomed.info/sct | Occupational health nursing officer	|
| 158990003 | http://snomed.info/sct | Nursing officer	|
| 158992006 | http://snomed.info/sct | Midwifery sister	|
| 158993001 | http://snomed.info/sct | Nursing sister (theatre)	|
| 158994007 | http://snomed.info/sct | Staff nurse	|
| 158995008 | http://snomed.info/sct | Staff midwife	|
| 158996009 | http://snomed.info/sct | State enrolled nurse	|
| 158997000 | http://snomed.info/sct | District nurse	|
| 158998005 | http://snomed.info/sct | Private nurse	|
| 158999002 | http://snomed.info/sct | Community midwife	|
| 159001001 | http://snomed.info/sct | Clinic nurse	|
| 159002008 | http://snomed.info/sct | Practice nurse|	
| 159003003 | http://snomed.info/sct | School nurse	|
| 159004009 | http://snomed.info/sct | Nurse - teaching	|
| 159005005 | http://snomed.info/sct | Student nurse	|
| 159006006 | http://snomed.info/sct | Dental nurse	|
| 159007002 | http://snomed.info/sct | Community pediatric nurse	|
| 159010009 | http://snomed.info/sct | Hospital pharmacist	|
| 159011008 | http://snomed.info/sct | Retail pharmacist	|
| 159012001 | http://snomed.info/sct | Industrial pharmacist	|
| 159013006 | http://snomed.info/sct | Pharmaceutical officer H.A.	|
| 159014000 | http://snomed.info/sct | Trainee pharmacist	|
| 159016003 | http://snomed.info/sct | Medical radiographer	|
| 159017007 | http://snomed.info/sct | Diagnostic radiographer|	
| 159018002 | http://snomed.info/sct | Therapeutic radiographer|	
| 159019005 | http://snomed.info/sct | Trainee radiographer	|
| 159021000 | http://snomed.info/sct | Ophthalmic optician	|
| 159022007 | http://snomed.info/sct | Trainee optician	|
| 159025009 | http://snomed.info/sct | Remedial gymnast	|
| 159026005 | http://snomed.info/sct | Speech and language therapist	|
| 159027001 | http://snomed.info/sct | Orthoptist	|
| 159028006 | http://snomed.info/sct | Trainee remedial therapist	|
| 159033005 | http://snomed.info/sct | Dietician	|
| 159034004 | http://snomed.info/sct | Podiatrist|	
| 159035003 | http://snomed.info/sct | Dental auxiliary	|
| 159036002 | http://snomed.info/sct | ECG technician	|
| 159037006 | http://snomed.info/sct | EEG technician	|
| 159038001 | http://snomed.info/sct | Artificial limb fitter	|
| 159039009 | http://snomed.info/sct | AT - Audiology technician	|
| 159040006 | http://snomed.info/sct | Pharmacy technician	|
| 159041005 | http://snomed.info/sct | Trainee medical technician	|
| 159141008 | http://snomed.info/sct | Geneticist	|
| 159972006 | http://snomed.info/sct | Surgical corset fitter	|
| 160008000 | http://snomed.info/sct | Dental technician	|
| 224529009 | http://snomed.info/sct | Clinical assistant|	
| 224530004 | http://snomed.info/sct | Senior registrar	|
| 224531000 | http://snomed.info/sct | Registrar	|
| 224532007 | http://snomed.info/sct | Senior house officer	|
| 224533002 | http://snomed.info/sct | MO - Medical officer	|
| 224534008 | http://snomed.info/sct | Health visitor, nurse/midwife	|
| 224535009 | http://snomed.info/sct | Registered nurse	|
| 224536005 | http://snomed.info/sct | Midwifery tutor	|
| 224537001 | http://snomed.info/sct | Accident and Emergency nurse	|
| 224538006 | http://snomed.info/sct | Triage nurse	|
| 224540001 | http://snomed.info/sct | Community nurse|	
| 224541002 | http://snomed.info/sct | Nursing continence advisor	|
| 224542009 | http://snomed.info/sct | Coronary care nurse	|
| 224543004 | http://snomed.info/sct | Diabetic nurse	|
| 224544005 | http://snomed.info/sct | Family planning nurse	|
| 224545006 | http://snomed.info/sct | Care of the elderly nurse	|
| 224546007 | http://snomed.info/sct | ICN - Infection control nurse	|
| 224547003 | http://snomed.info/sct | Intensive therapy nurse	|
| 224548008 | http://snomed.info/sct | Learning disabilities nurse|	
| 224549000 | http://snomed.info/sct | Neonatal nurse	|
| 224550000 | http://snomed.info/sct | Neurology nurse	|
| 224551001 | http://snomed.info/sct | Industrial nurse	|
| 224552008 | http://snomed.info/sct | Oncology nurse	|
| 224553003 | http://snomed.info/sct | Macmillan nurse	|
| 224554009 | http://snomed.info/sct | Marie Curie nurse	|
| 224555005 | http://snomed.info/sct | Pain control nurse	|
| 224556006 | http://snomed.info/sct | Palliative care nurse	|
| 224557002 | http://snomed.info/sct | Chemotherapy nurse	|
| 224558007 | http://snomed.info/sct | Radiotherapy nurse	|
| 224559004 | http://snomed.info/sct | PACU nurse	|
| 224560009 | http://snomed.info/sct | Stomatherapist	|
| 224561008 | http://snomed.info/sct | Theatre nurse	|
| 224562001 | http://snomed.info/sct | Pediatric nurse	|
| 224563006 | http://snomed.info/sct | Psychiatric nurse	|
| 224564000 | http://snomed.info/sct | Community mental health nurse	|
| 224565004 | http://snomed.info/sct | Renal nurse	|
| 224566003 | http://snomed.info/sct | Hemodialysis nurse	|
| 224567007 | http://snomed.info/sct | Wound care nurse	|
| 224569005 | http://snomed.info/sct | Nurse grade	|
| 224570006 | http://snomed.info/sct | Clinical nurse specialist	|
| 224571005 | http://snomed.info/sct | Nurse practitioner	|
| 224572003 | http://snomed.info/sct | Nursing sister	|
| 224573008 | http://snomed.info/sct | CN - Charge nurse	|
| 224574002 | http://snomed.info/sct | Ward manager	|
| 224575001 | http://snomed.info/sct | Nursing team leader	|
| 224576000 | http://snomed.info/sct | Nursing assistant	|
| 224577009 | http://snomed.info/sct | Healthcare assistant	|
| 224578004 | http://snomed.info/sct | Nursery nurse	|
| 224579007 | http://snomed.info/sct | Healthcare service manager	|
| 224580005 | http://snomed.info/sct | Occupational health service manager	|
| 224581009 | http://snomed.info/sct | Community nurse manager	|
| 224583007 | http://snomed.info/sct | Behavior therapist	|
| 224584001 | http://snomed.info/sct | Behavior therapy assistant	|
| 224585000 | http://snomed.info/sct | Drama therapist	|
| 224586004 | http://snomed.info/sct | Domiciliary occupational therapist	|
| 224587008 | http://snomed.info/sct | Occupational therapy helper	|
| 224588003 | http://snomed.info/sct | Psychotherapist	|
| 224589006 | http://snomed.info/sct | Community-based physiotherapist	|
| 224590002 | http://snomed.info/sct | Play therapist	|
| 224591003 | http://snomed.info/sct | Play specialist	|
| 224592005 | http://snomed.info/sct | Play leader	|
| 224593000 | http://snomed.info/sct | Community-based speech/language therapist	|
| 224594006 | http://snomed.info/sct | Speech/language assistant	|
| 224595007 | http://snomed.info/sct | Professional counselor	|
| 224596008 | http://snomed.info/sct | Marriage guidance counselor	|
| 224597004 | http://snomed.info/sct | Trained nurse counselor	|
| 224598009 | http://snomed.info/sct | Trained social worker counselor	|
| 224599001 | http://snomed.info/sct | Trained personnel counselor	|
| 224600003 | http://snomed.info/sct | Psychoanalyst	|
| 224601004 | http://snomed.info/sct | Assistant psychologist	|
| 224602006 | http://snomed.info/sct | Community-based podiatrist |	
| 224603001 | http://snomed.info/sct | Foot care worker	|
| 224604007 | http://snomed.info/sct | Audiometrician	|
| 224605008 | http://snomed.info/sct | Audiometrist	|
| 224606009 | http://snomed.info/sct | Technical healthcare occupation	|
| 224607000 | http://snomed.info/sct | Occupational therapy technical instructor	|
| 224608005 | http://snomed.info/sct | Administrative healthcare staff	|
| 224609002 | http://snomed.info/sct | Complementary health worker	|
| 224610007 | http://snomed.info/sct | Supporting services personnel	|
| 224614003 | http://snomed.info/sct | Research associate	|
| 224615002 | http://snomed.info/sct | Research nurse	|
| 224620002 | http://snomed.info/sct | Human aid to communication	|
| 224621003 | http://snomed.info/sct | Palantypist	|
| 224622005 | http://snomed.info/sct | Note taker	|
| 224623000 | http://snomed.info/sct | Cuer	|
| 224624006 | http://snomed.info/sct | Lipspeaker	|
| 224625007 | http://snomed.info/sct | Interpreter for British sign language	|
| 224626008 | http://snomed.info/sct | Interpreter for Signs supporting English	|
| 224936003 | http://snomed.info/sct | General practitioner locum	|
| 225726006 | http://snomed.info/sct | Lactation consultant	|
| 225727002 | http://snomed.info/sct | Midwife counselor	|
| 265937000 | http://snomed.info/sct | Nursing occupation	|
| 265939002 | http://snomed.info/sct | Medical/dental technicians	|
| 283875005 | http://snomed.info/sct | Parkinson disease nurse	|
| 302211009 | http://snomed.info/sct | Specialist registrar	|
| 303124005 | http://snomed.info/sct | Member of mental health review tribunal	|
| 303129000 | http://snomed.info/sct | Hospital manager	|
| 303133007 | http://snomed.info/sct | Responsible medical officer	|
| 303134001 | http://snomed.info/sct | Independent doctor	|
| 304291006 | http://snomed.info/sct | Bereavement counselor	|
| 304292004 | http://snomed.info/sct | Surgeon	|
| 307988006 | http://snomed.info/sct | Medical technician	|
| 308002005 | http://snomed.info/sct | Remedial therapist	|
| 309294001 | http://snomed.info/sct | Accident and Emergency doctor	|
| 309295000 | http://snomed.info/sct | Clinical oncologist	|
| 309296004 | http://snomed.info/sct | Family planning doctor	|
| 309322005 | http://snomed.info/sct | Associate general practitioner	|
| 309323000 | http://snomed.info/sct | Partner of general practitioner	|
| 309324006 | http://snomed.info/sct | Assistant GP	|
| 309326008 | http://snomed.info/sct | Deputizing general practitioner	|
| 309327004 | http://snomed.info/sct | General practitioner registrar	|
| 309328009 | http://snomed.info/sct | Ambulatory pediatrician	|
| 309329001 | http://snomed.info/sct | Community pediatrician	|
| 309330006 | http://snomed.info/sct | Pediatric cardiologist	|
| 309331005 | http://snomed.info/sct | Pediatric endocrinologist	|
| 309332003 | http://snomed.info/sct | Pediatric gastroenterologist	|
| 309333008 | http://snomed.info/sct | Pediatric nephrologist	|
| 309334002 | http://snomed.info/sct | Pediatric neurologist	|
| 309335001 | http://snomed.info/sct | Pediatric rheumatologist	|
| 309336000 | http://snomed.info/sct | Pediatric oncologist	|
| 309337009 | http://snomed.info/sct | Pain management specialist	|
| 309338004 | http://snomed.info/sct | Intensive care specialist	|
| 309339007 | http://snomed.info/sct | Adult intensive care specialist	|
| 309340009 | http://snomed.info/sct | Pediatric intensive care specialist |	
| 309341008 | http://snomed.info/sct | Blood transfusion doctor	|
| 309342001 | http://snomed.info/sct | Histopathologist	|
| 309343006 | http://snomed.info/sct | Physician	|
| 309345004 | http://snomed.info/sct | Chest physician	|
| 309346003 | http://snomed.info/sct | Thoracic physician	|
| 309347007 | http://snomed.info/sct | Clinical hematologist	|
| 309348002 | http://snomed.info/sct | Clinical neurophysiologist	|
| 309349005 | http://snomed.info/sct | Clinical physiologist	|
| 309350005 | http://snomed.info/sct | Diabetologist	|
| 309351009 | http://snomed.info/sct | Andrologist	|
| 309352002 | http://snomed.info/sct | Neuroendocrinologist	|
| 309353007 | http://snomed.info/sct | Reproductive endocrinologist	|
| 309354001 | http://snomed.info/sct | Thyroidologist	|
| 309355000 | http://snomed.info/sct | Clinical geneticist |	
| 309356004 | http://snomed.info/sct | Clinical cytogeneticist	|
| 309357008 | http://snomed.info/sct | Clinical molecular geneticist	|
| 309358003 | http://snomed.info/sct | Genitourinary medicine physician	|
| 309359006 | http://snomed.info/sct | Palliative care physician	|
| 309360001 | http://snomed.info/sct | Rehabilitation physician	|
| 309361002 | http://snomed.info/sct | Child and adolescent psychiatrist	|
| 309362009 | http://snomed.info/sct | Forensic psychiatrist	|
| 309363004 | http://snomed.info/sct | Liaison psychiatrist	|
| 309364005 | http://snomed.info/sct | Psychogeriatrician	|
| 309365006 | http://snomed.info/sct | Psychiatrist for mental handicap	|
| 309366007 | http://snomed.info/sct | Rehabilitation psychiatrist	|
| 309367003 | http://snomed.info/sct | Obstetrician and gynecologist	|
| 309368008 | http://snomed.info/sct | Breast surgeon	|
| 309369000 | http://snomed.info/sct | Cardiothoracic surgeon	|
| 309371000 | http://snomed.info/sct | Cardiac surgeon	|
| 309372007 | http://snomed.info/sct | Ear, nose and throat surgeon	|
| 309373002 | http://snomed.info/sct | Endocrine surgeon	|
| 309374008 | http://snomed.info/sct | Thyroid surgeon	|
| 309375009 | http://snomed.info/sct | Pituitary surgeon	|
| 309376005 | http://snomed.info/sct | Gastrointestinal surgeon	|
| 309377001 | http://snomed.info/sct | General gastrointestinal surgeon	|
| 309378006 | http://snomed.info/sct | Upper gastrointestinal surgeon	|
| 309379003 | http://snomed.info/sct | Colorectal surgeon	|
| 309380000 | http://snomed.info/sct | Hand surgeon	|
| 309381001 | http://snomed.info/sct | Hepatobiliary surgeon	|
| 309382008 | http://snomed.info/sct | Ophthalmic surgeon	|
| 309383003 | http://snomed.info/sct | Pediatric surgeon	|
| 309384009 | http://snomed.info/sct | Pancreatic surgeon	|
| 309385005 | http://snomed.info/sct | Transplant surgeon	|
| 309386006 | http://snomed.info/sct | Trauma surgeon	|
| 309388007 | http://snomed.info/sct | Vascular surgeon	|
| 309389004 | http://snomed.info/sct | Medical practitioner grade	|
| 309390008 | http://snomed.info/sct | Hospital consultant	|
| 309391007 | http://snomed.info/sct | Visiting specialist registrar	|
| 309392000 | http://snomed.info/sct | Research registrar	|
| 309393005 | http://snomed.info/sct | General practitioner grade	|
| 309394004 | http://snomed.info/sct | General practitioner principal	|
| 309395003 | http://snomed.info/sct | Hospital specialist	|
| 309396002 | http://snomed.info/sct | Associate specialist	|
| 309397006 | http://snomed.info/sct | Research fellow	|
| 309398001 | http://snomed.info/sct | Allied health professional	|
| 309399009 | http://snomed.info/sct | Hospital dietitian	|
| 309400002 | http://snomed.info/sct | Domiciliary physiotherapist	|
| 309401003 | http://snomed.info/sct | General practitioner-based physiotherapist	|
| 309402005 | http://snomed.info/sct | Hospital-based physiotherapist	|
| 309403000 | http://snomed.info/sct | Private physiotherapist	|
| 309404006 | http://snomed.info/sct | Physiotherapy assistant	|
| 309409001 | http://snomed.info/sct | Hospital-based speech and language therapist	|
| 309410006 | http://snomed.info/sct | Arts therapist	|
| 309411005 | http://snomed.info/sct | Dance therapist	|
| 309412003 | http://snomed.info/sct | Music therapist	|
| 309413008 | http://snomed.info/sct | Renal dietitian	|
| 309414002 | http://snomed.info/sct | Liver dietitian	|
| 309415001 | http://snomed.info/sct | Oncology dietitian	|
| 309416000 | http://snomed.info/sct | Pediatric dietitian	|
| 309417009 | http://snomed.info/sct | Diabetes dietitian	|
| 309418004 | http://snomed.info/sct | Audiologist	|
| 309419007 | http://snomed.info/sct | Hearing therapist	|
| 309420001 | http://snomed.info/sct | Audiological scientist	|
| 309421002 | http://snomed.info/sct | Hearing aid dispenser	|
| 309422009 | http://snomed.info/sct | Community-based occupational therapist	|
| 309423004 | http://snomed.info/sct | Hospital occupational therapist	|
| 309427003 | http://snomed.info/sct | Social services occupational therapist	|
| 309428008 | http://snomed.info/sct | Orthotist	|
| 309429000 | http://snomed.info/sct | Surgical fitter	|
| 309434001 | http://snomed.info/sct | Hospital-based podiatrist	|
| 309435000 | http://snomed.info/sct | Podiatry assistant	|
| 309436004 | http://snomed.info/sct | Lymphedema nurse	|
| 309437008 | http://snomed.info/sct | Community learning disabilities nurse	|
| 309439006 | http://snomed.info/sct | Clinical nurse teacher	|
| 309440008 | http://snomed.info/sct | Community practice nurse teacher	|
| 309441007 | http://snomed.info/sct | Nurse tutor	|
| 309442000 | http://snomed.info/sct | Nurse teacher practitioner	|
| 309443005 | http://snomed.info/sct | Nurse lecturer practitioner	|
| 309444004 | http://snomed.info/sct | Outreach nurse	|
| 309445003 | http://snomed.info/sct | Anesthetic nurse	|
| 309446002 | http://snomed.info/sct | Nurse manager	|
| 309450009 | http://snomed.info/sct | Nurse administrator	|
| 309452001 | http://snomed.info/sct | Midwifery grade	|
| 309453006 | http://snomed.info/sct | Midwife	|
| 309454000 | http://snomed.info/sct | Student midwife	|
| 309455004 | http://snomed.info/sct | Parentcraft sister |	
| 309459005 | http://snomed.info/sct | Healthcare professional grade	|
| 309460000 | http://snomed.info/sct | Restorative dentist	|
| 310170009 | http://snomed.info/sct | Pediatric audiologist	|
| 310171008 | http://snomed.info/sct | Immunopathologist	|
| 310172001 | http://snomed.info/sct | Audiological physician	|
| 310173006 | http://snomed.info/sct | Clinical pharmacologist	|
| 310174000 | http://snomed.info/sct | Private doctor	|
| 310175004 | http://snomed.info/sct | Agency nurse	|
| 310176003 | http://snomed.info/sct | Behavioral therapist nurse	|
| 310177007 | http://snomed.info/sct | Cardiac rehabilitation nurse	|
| 310178002 | http://snomed.info/sct | Genitourinary nurse	|
| 310179005 | http://snomed.info/sct | Rheumatology nurse specialist	|
| 310180008 | http://snomed.info/sct | Continence nurse	|
| 310181007 | http://snomed.info/sct | Contact tracing nurse	|
| 310182000 | http://snomed.info/sct | General nurse	|
| 310183005 | http://snomed.info/sct | Nurse for the mentally handicapped	|
| 310184004 | http://snomed.info/sct | Liaison nurse	|
| 310185003 | http://snomed.info/sct | Diabetic liaison nurse	|
| 310186002 | http://snomed.info/sct | Nurse psychotherapist	|
| 310187006 | http://snomed.info/sct | Company nurse	|
| 310188001 | http://snomed.info/sct | Hospital midwife	|
| 310189009 | http://snomed.info/sct | Genetic counselor	|
| 310190000 | http://snomed.info/sct | Mental health counselor	|
| 310191001 | http://snomed.info/sct | Clinical psychologist	|
| 310192008 | http://snomed.info/sct | Educational psychologist	| 
| 310193003 | http://snomed.info/sct | Coroner	|
| 310194009 | http://snomed.info/sct | Appliance officer	|
| 310512001 | http://snomed.info/sct | Medical oncologist	|
| 311441001 | http://snomed.info/sct | School medical officer	|
| 312485001 | http://snomed.info/sct | Integrated midwife	|
| 372102007 | http://snomed.info/sct | RN First Assist	|
| 387619007 | http://snomed.info/sct | Optician	|
| 394572006 | http://snomed.info/sct | Medical secretary	|
| 394618009 | http://snomed.info/sct | Hospital nurse	|
| 397824005 | http://snomed.info/sct | Consultant anesthetist	|
| 397897005 | http://snomed.info/sct | Paramedic	|
| 397903001 | http://snomed.info/sct | Staff grade obstetrician	|
| 397908005 | http://snomed.info/sct | Staff grade practitioner	|
| 398130009 | http://snomed.info/sct | Medical student	|
| 398238009 | http://snomed.info/sct | Acting obstetric registrar	|
| 404940000 | http://snomed.info/sct | Physiotherapist technical instructor	|
| 405277009 | http://snomed.info/sct | Resident physician	|
| 405278004 | http://snomed.info/sct | Certified registered nurse anesthetist	|
| 405279007 | http://snomed.info/sct | Attending physician	|
| 405623001 | http://snomed.info/sct | Assigned practitioner	|
| 405684005 | http://snomed.info/sct | Professional initiating surgical case	|
| 405685006 | http://snomed.info/sct | Professional providing staff relief during surgical procedure	|
| 408798009 | http://snomed.info/sct | Consultant pediatrician	|
| 408799001 | http://snomed.info/sct | Consultant neonatologist	|
| 409974004 | http://snomed.info/sct | Health educator	|
| 409975003 | http://snomed.info/sct | Certified health education specialist	|
| 413854007 | http://snomed.info/sct | Circulating nurse	|
| 415075003 | http://snomed.info/sct | Perioperative nurse	|
| 415506007 | http://snomed.info/sct | Scrub nurse	|
| 416160000 | http://snomed.info/sct | Fellow of American Academy of Osteopathy	|
| 420409002 | http://snomed.info/sct | Oculoplastic surgeon	|
| 420678001 | http://snomed.info/sct | Retinal surgeon	|
| 421841007 | http://snomed.info/sct | Admitting physician	|
| 422140007 | http://snomed.info/sct | Medical ophthalmologist	|
| 422234006 | http://snomed.info/sct | Ophthalmologist	|
| 432100008 | http://snomed.info/sct | Health coach	|
| 442867008 | http://snomed.info/sct | Respiratory therapist	|
| 443090005 | http://snomed.info/sct | Podiatric surgeon	|
| 444912007 | http://snomed.info/sct | Hypnotherapist	|
| 445313000 | http://snomed.info/sct | Asthma nurse specialist	|
| 445451001 | http://snomed.info/sct | Nurse case manager	|
| 446050000 | http://snomed.info/sct | PCP - Primary care physician	|
| 446701002 | http://snomed.info/sct | Addiction medicine specialist	|
| 449161006 | http://snomed.info/sct | PA - physician assistant	|
| 471302004 | http://snomed.info/sct | Government midwife	|
| 3981000175106 | http://snomed.info/sct | Nurse complex case manager	
| 231189271000087109 | http://snomed.info/sct | Naturopath	|
| 236749831000087105 | http://snomed.info/sct | Prosthetist	|
| 258508741000087105 | http://snomed.info/sct | Hip and knee surgeon |
| 260767431000087107 | http://snomed.info/sct | Hepatologist |
| 285631911000087106 | http://snomed.info/sct | Shoulder surgeon |	
| 291705421000087106 | http://snomed.info/sct | Interventional radiologist |
| 341320851000087105 | http://snomed.info/sct | Pediatric radiologist |
| 368890881000087105 | http://snomed.info/sct | Emergency medicine specialist |
| 398480381000087106 | http://snomed.info/sct | Family medicine specialist - palliative care |
| 416186861000087101 | http://snomed.info/sct | Surgical oncologist |
| 450044741000087104 | http://snomed.info/sct | Acupuncturist |
| 465511991000087105 | http://snomed.info/sct | Pediatric orthopedic surgeon |
| 494782281000087101 | http://snomed.info/sct | Pediatric hematologist |
| 619197631000087102 | http://snomed.info/sct | Neuroradiologist |
| 623630151000087105 | http://snomed.info/sct | Family medicine specialist - anesthetist |
| 666997781000087107 | http://snomed.info/sct | Doula |
| 673825031000087109 | http://snomed.info/sct | Traditional herbal medicine specialist |
| 682131381000087105 | http://snomed.info/sct | Occupational medicine specialist |
| 724111801000087104 | http://snomed.info/sct | Pediatric emergency medicine specialist |
| 747936471000087102 | http://snomed.info/sct | Family medicine specialist - care of the elderly |
| 766788081000087100 | http://snomed.info/sct | Travel medicine specialist |
| 767205061000087108 | http://snomed.info/sct | Spine surgeon |
| 813758161000087106 | http://snomed.info/sct | Maternal or fetal medicine specialist |
| 822410621000087104 | http://snomed.info/sct | Massage therapist |
| 847240411000087102 | http://snomed.info/sct | Hospitalist |
| 853827051000087104 | http://snomed.info/sct | Sports medicine specialist |
| 926871431000087103 | http://snomed.info/sct | Pediatric respirologist |
| 954544641000087107 | http://snomed.info/sct | Homeopath |
| 956387501000087102 | http://snomed.info/sct | Family medicine specialist - emergency medicine |
| 969118571000087109 | http://snomed.info/sct | Pediatric hematologist or oncologist |
| 984095901000087105 | http://snomed.info/sct | Foot and ankle surgeon |
| 990928611000087105 | http://snomed.info/sct | Invasive cardiologist |
| 999480451000087102 | http://snomed.info/sct | Case manager| 
| 999480461000087104 | http://snomed.info/sct | Kinesthesiologist|