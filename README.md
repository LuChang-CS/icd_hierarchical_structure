# ICD Hierarchical Structure
The JSON file for the ICD-9-CM and ICD-10-CM codes, including diagnosis codes and procedure codes

The json files contain code, descriptions, and hierarchies of ICD codes.

The sources are [icd9data.com (2015 version)](http://www.icd9data.com/) and [icd10data.com (2023 version)](https://www.icd10data.com/).

There might be errors when collecting the data. If you find any error, please feel free to post an issue.

## Structure
```bash
ICD_HIERARCHICAL_STRUCTURE
│
├─ICD-9-CM
│    diagnosis_codes.json    # (4,828 KB) ICD-9-CM diagnosis code only
│    icd_codes.json          # (5,924 KB) ICD-9-CM codes, including diagnosis codes and procedure codes
│    procedure_codes.json    # (1,096 KB) ICD-9-CM procedure code only
│
└─ICD-10-CM
     diagnosis_codes.json    # (26,223 KB) ICD-10-CM diagnosis code only
     icd_codes.json          # (92,902 KB) ICD-10-CM codes, including diagnosis codes and procedure codes
     procedure_codes.json    # (66,680 KB) ICD-10-CM procedure code only
```

## Fields

### ICD-9-CM

```json
[
    {
        "code": "001-139",  // code name
        "desc": "Infectious And Parasitic Diseases",  // disease name
        "children": [  // children diseases
            {
                "code": "001-009",
                "desc": "Intestinal Infectious Diseases",
                "children": [
                    {
                        "code": "001",
                        "desc": "Cholera",
                        "children": [
                            {
                                "code": "001.0",
                                "desc": "Cholera due to vibrio cholerae",
                                "children": []
                            }
                        // ...
                        ]
                    }
                // ...
                ]
            }
        // ...
        ]
    }
    // ...
]
```

The fields of procedure codes are the same as diagnosis codes.

### ICD-10-CM

```json
[
    {
        "code": "A00-B99",  // code name
        "desc": "Certain infectious and parasitic diseases",  // disease name with abbreviations
        "children": [  // children diseases
            {
                "code": "A00-A09",
                "desc": "Intestinal infectious diseases",
                "children": [
                    // ...
                    {
                        "code": "A01",
                        "desc": "Typhoid and paratyphoid fevers",
                        "children": [
                            {
                                "code": "A01.0",
                                "desc": "Typhoid fever",
                                "children": [
                                    {
                                        "code": "A01.00",
                                        "desc": "\u2026\u2026 unspecified",
                                        "children": [],
                                        "desc_full": "Typhoid fever unspecified"    // full disease name
                                    },
                                // ...
                                ]
                            }
                        // ...
                        ]
                    }
                // ...
                ]
            }
        // ...
        ]
    }
    // ...
]
```

Note: in the diagnosis codes of [icd10data.com (2023 version)](https://www.icd10data.com/), some diseases contain abbreviations of their parent. For example:
```
A01 Typhoid and paratyphoid fevers
    A01.0 Typhoid fever
        A01.00 ...... unspecified
        A01.01 Typhoid meningitis
        A01.02 ...... with heart involvement
        A01.03 Typhoid pneumonia
        A01.04 Typhoid arthritis
        A01.05 Typhoid osteomyelitis
        A01.09 ...... with other complications
```
The parent disease name `A01.0 Typhoid fever` is simplified with `......` in `A01.00 ...... unspecified`. So I replaced `......` with the parent disease name and stored it in the field of `desc_full`.

The fields of procedure codes are the same as diagnosis codes except `desc_full`.


