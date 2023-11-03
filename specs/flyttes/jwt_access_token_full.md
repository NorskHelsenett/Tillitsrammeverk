

````JSON
{
     "iss": "https://helseid.nhn.no/",
     "sub": "5ba552d67",
     "aud": "https://kj.nhn.no/",
     "exp": 1639528912,
     "iat": 1618354090,
     "jti" : "dbe39bf3a3ba4238a513f51d6e1691c4",
     "client_id": "s6BhdRkqt3",
     "scope": "openid profile kjernejournal",

     "trust_framework":{
        "agreement": {
            "version": "1.0",
            "legal-entity": {
                "id": "123456789",
                "name": "Helsevirksomheten AS",
                "oid": "2.16.578.1.12.4.1.4.101"
            },
            "date": "14.02.2023",
            "id": "10001",
            "granting_body": {
                "id": "987654321",
                "name": "Norsk Helsenett SF",
                "oid": "2.16.578.1.12.4.1.4.101"
            }
	    },
        "attestation": {
           "practitioner": {
                "pid": {
                    "id": "20086600138",
                    "name": "August September",
                    "system": "urn:oid:2.16.578.1.12.4.1.4.1",
                    "authority": "https://www.skatteetaten.no"
                },
                 "hpr-nr": {
                   "id": "9144897",
                   "system": "urn:oid:2.16.578.1.12.4.1.4.4",
                   "authority": "https://www.helsedirektoratet.no/"
                 },
                 "authorization": {
                   "code": "LE",
                   "text": "Lege",
                   "system": "urn:oid:2.16.578.1.12.4.1.1.9060",
                   "assigner": "https://www.helsedirektoratet.no/"
                 }
	        },
            "care-relationship": {
                "legal-entity": {
                    "id": "100100673",
                    "name": "Norsk Helsenett SF Fagersta Testlegekontor",
                    "system": "urn:oid:2.16.578.1.12.4.1.4.101",
                    "authority": "https://www.skatteetaten.no"
                },
                "point-of-care": {
                    "id": "100100673",
                    "name": "Norsk Helsenett SF Fagersta Testlegekontor",
                    "system": "urn:oid:2.16.578.1.12.4.1.4.101",
                    "authority": "https://www.skatteetaten.no"
                },
            }, 
        }
     }

}
````