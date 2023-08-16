[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v2.0%20adopted-ff69b4.svg)](CODE_OF_CONDUCT.md)
# API for Digital Public Goods

Application Programming Interface (API) for Digital Public Goods, available at https://api.digitalpublicgoods.net.

This API provides an alternative method of accessing the information available at https://github.com/DPGAlliance/publicgoods-candidates. 

Yet for another alternative, a more user-friendly version, you can browse the [Digital Public Goods Registry](https://digitalpublicgoods.net/registry).

## Architecture

This API leverages [GitHub Pages](https://pages.github.com/) for hosting, and [GitHub Actions](https://github.com/features/actions) for automatic syncing its contents with the source of truth that lives in the [Digital Public Goods repository](https://github.com/DPGAlliance/publicgoods-candidates).

Because of the structure imposed by **GitHub Pages**, all the JSON files are stored inside the `docs/` folder, and served from there. The files for each individual endpoint (e.g. `dpg/{dpg}/` and `nominee/{nominee}/`) are pregenerated and stored in correspondingly-named folders with a `index.json` file inside through [this script](https://github.com/DPGAlliance/publicgoods-candidates/blob/master/scripts/api.js), which is triggred to run automatically anytime new relevant changes are pushed to the `master` branch of the [DPGAlliance/publicgoods-candidates repo](https://github.com/DPGAlliance/publicgoods-candidates). This folder and file structure accomplishes making the API available in the static infrastructure that GitHub Pages provides.

⚠️ Please note the trailing `/` at the end of all endpoints, which is an artifact of this setup. If you do not include it, you need your code to follow automatic redirects. Any endpoint without trailing slash returns a `301` redirect to the same path with a trailing slash.

## Reference

### List all available endpoints

List all endpoints available through this API.

```
GET /
```
#### Code Samples

**Shell**

```bash
curl https://api.digitalpublicgoods.net
```

#### Default Response

```
Status: 200 OK
```
```json
{
	"dpgs": "https://api.digitalpublicgoods.net/dpgs",
	"dpg/{dpg}": "https://api.digitalpublicgoods.net/dpg/{id}/",
	"nominees": "https://api.digitalpublicgoods.net/nominees",
	"nominee/{nominee}": "https://api.digitalpublicgoods.net/nominee/{nominee}"
}
```

### List digital public goods

List all digital public goods screened against the [Digital Public Goods Standard](https://github.com/DPGAlliance/DPG-Standard/).

```
GET /dpgs/
```

#### Code Samples

**Shell**

```bash
curl https://api.digitalpublicgoods.net/dpgs/
```
```bash
curl -L https://api.digitalpublicgoods.net/dpgs
```

#### Default Response

```
Status: 200 OK
```
```json
[
  {
    "id": "10275",
    "name": "African Storybook",
    "description": "Open access to picture storybooks in the languages of Africa. For children’s literacy, enjoyment and imagination.",
    "website": "https://www.africanstorybook.org/",
    "license": [
      {
        "spdx": "CC-BY-SA-4.0",
        "licenseURL": "https://creativecommons.org/licenses/by-sa/4.0/"
      }
    ],
    "SDGs": [
      {
        "SDGNumber": 4
      }
    ],
    "sectors": [],
    "type": [
      "content"
    ],
    "organizations": [
      {
        "name": "Saide",
        "org_type": "owner"
      }
    ],
    "stage": "DPG"
  }
]
```

### Get a digital public good

Retrieve an individual digital public good.

```bash
GET /dpg/{id}/
```

#### Parameters

Name | Type | In | Description
---|---|---|---
`dpg` | string | path | Kebab case name of the digital public good, refer to the `id` field returned in the listing of all digital public goods at `/dpgs/`.

#### Code Samples

**Shell**

```bash
curl https://api.digitalpublicgoods.net/dpg/10275/
```
```bash
curl -L https://api.digitalpublicgoods.net/dpg/10275
```

#### Default Response
```
Status: 200 OK
```
```json
{
  "id": "10275",
  "name": "African Storybook",
  "description": "Open access to picture storybooks in the languages of Africa. For children’s literacy, enjoyment and imagination.",
  "website": "https://www.africanstorybook.org/",
  "license": [
    {
      "spdx": "CC-BY-SA-4.0",
      "licenseURL": "https://creativecommons.org/licenses/by-sa/4.0/"
    }
  ],
  "sdgs": {
		"sdg": [
			"SDG4: Quality Education"
					],
	"relevance": " The African Storybook webpage itself (https://www.africanstorybook.org) demonstrates that the 3696 storybooks and the 7586 translations are relevant to the Quality Education SDG. \r\nThere are also reviews of ASb at:\r\nhttps://www.alllanguageresources.com/african-storybook/\r\nhttps://allafrica.com/stories/202202110011.html - this review stresses the importance of quality storybooks in indigenous languages which is one of the features of ASb\r\n\r\nA published research article on ASb can be found here: https://onlinelibrary.wiley.com/doi/10.1111/modl.12374\r\n\r\nThe Scale of Solution details indicate all of the educational organisations that ASb works with\r\n\r\nJudith Uchidiuno has also reviewed several of the books on her Facebook page: https://www.facebook.com/people/African-Storybook-Reviews-Judith-Uchidiuno/100055884440164/\r\n\r\n"
	},
  "sectors": [],
  "type": [
    "content"
  ],
  "organizations": [
    {
      "name": "Saide",
      "org_type": "owner"
    }
  ],
  "stage": "DPG"
}
```

### List nominees for digital public goods

List all nominees for digital public goods, but exclude actual digital public goods.

```bash
GET /nominees/
```

#### Code Samples

**Shell**

```bash
curl https://api.digitalpublicgoods.net/nominees/
```
```bash
curl -L https://api.digitalpublicgoods.net/nominees
```

#### Default Response

```
Status: 200 OK
```
```json
[
  {
        "id": "10623",
        "name": "FormSG",
        "sectors": [],
        "stage": "nominee",
        "privacy": [
            {
                "privacyCompliance": "Personal Data protection Act of Singapore",
                "privacyComplianceURL": "Privacy Policy - https://form.gov.sg/privacy"
            }
        ],
        "organizations": [
            {
                "name": "FormSG",
                "website": "https://form.gov.sg ",
                "org_type": "owner",
                "contact_name": " Amit Samdarshi  ",
                "contact_email": "amit@open.gov.sg"
            }
        ],
        "platformIndependence": {
            "isPlatformIndependent": "Yes",
            "openAlternatives": [
                "There are multiple proprietary elements to note:\r\n- integrations with proprietary services",
                " like the Singapore National Identity system Singpass. This cannot be replaced",
                " but adopters may replace authentication systems with whatever identity platform of their country",
                " or disable the identity system altogether\r\n- AWS SQS: formSG operates on AWS and uses some AWS-specific tools",
                " like SQS for webhook retries. That could be replaced quite easily with open source solutions like RabbitMQ.\r\n- FormSG uses AWS SES to send emails. Any other SMTP mailing solution could work.\r\n- FormSG uses AWS S3 for its object store. A custom system for storage (even local with a local NAS)\r\n- For Monitoring and Observability",
                " FormSG integrates to DataDog. This is mostly non-intrusive in code",
                " and could be replaced with other providers. DataDog is a multi-tool system with tracing",
                " metrics",
                " RUM",
                " etc.",
                " each of those could be replaced by something else (open tracing solutions https://opentracing.io/",
                " statsd server https://github.com/statsd/statsd",
                " sentry https://github.com/getsentry/sentry",
                " etc.)\r\n- FormSG uses MongoDB (a document database)",
                " with the mongoose driver https://www.npmjs.com/package/mongoose. With substantial effort",
                " the database could be replaced with another document database like CouchDB."
            ]
        },
        "categories": [
            "Open Software"
        ],
        "description": "FormSG is a form builder tool that enables public officers to instantly create customisable forms with zero code or cost, to safely collect classified and sensitive data.",
        "website": "https://form.gov.sg ",
        "repositories": [
            {
                "name": "main",
                "url": "https://github.com/opengovsg/FormSG"
            }
        ],
        "sdgs": {
            "sdg": [
                "SDG16: Peace\u00b8 Justice and Strong Institutions"
            ],
            "relevance": "SDG INDICATOR 16.6.1 - Governmental expenditures within budgets\r\nFormSG as an open source government form builder provides access to justice for all and build effective, accountable and inclusive institutions at all levels. FormSG is used for government application forms, and also as a reporting and feedback platform by various public agencies.\r\n\r\nSDG INDICATOR 16.6.2 - Satisfaction with public services\r\nWe gather feedback from our members of public using FormSG and have gotten an average satisfaction rating of 4.66 out of 5 over 69,140 feedback submitted. \r\n\r\n"
        },
        "openlicenses": [
            {
                "openLicense": "MIT",
                "openLicenseEvidenceURLs": "https://github.com/opengovsg/FormSG/blob/develop/LICENSE.md"
            }
        ],
        "documentation": "Developer guide: https://github.com/opengovsg/FormSG/blob/develop/README.md\r\n\r\nPublic guide: https://guide.form.gov.sg/\r\n\r\nInformation and contact portal: https://www.developer.tech.gov.sg/products/categories/productivity-tools/formsg/overview.html",
        "NonPII": {
            "collectsNonPII": "Yes",
            "nonPIIAccessMechanism": "The data collected in FormSG can be downloaded in CSV format by the public officer who has created the form. Our form level secret key system ensures that only the person who owns secret key can access the data."
        },
        "dataPrivacySecurity": {
            "collectsPII": "PII data is collected and stored and distributed.",
            "typesOfPIIDataCollected": [
                "The fields are entirely dependent on the public officer who creates the form and how they name the fields (e.g. Name). If they create PII fields",
                " the data from that field would still be end to end encrypted",
                " just like any other field in FormSG forms.  "
            ],
            "dataPrivacySecurity": "We provide data privacy and security through strong end to end encryption created by using form level security keys which only form admin possesses."
        },
        "userContent": {
            "contentManagement": "Content is collected stored and distributed.",
            "contentTypes": [
                "Text and files"
            ],
            "contentManagementPolicy": "The solution does not have any censorship and relies entirely on self-governance of public officers. The platform guarantees that only public officers can log in, thanks to our domain-based OTP login system (i.e. only emails in .gov.sg domain can log in)."
        },
        "locations": {
            "developmentCountries": [
                "Singapore"
            ],
            "deploymentCountries": [
                "Singapore"
            ]
        },
        "deploymentCountriesDepartments": [
            "All statutory boards",
            " ministries and healthcare bodies associated with Singapore Government"
        ],
        "otherDeploymentOrganisations": [
            "Sri Lanka government has forked FormSG to create https://forms.gov.lk/ "
        ],
        "awardsReceived": [
            "MongoDB APAC Innovation Award 2023 for Positive Impact"
        ],
        "openStandards": [
            "* OIDC (used to integrate with the national identity system of Singapore) https://github.com/opengovsg/FormSG/blob/develop/src/app/modules/spcp/spcp.oidc.client.ts\r\n\r\n* Accessibility: We use React + Chakra",
            " and we have spent a lot of effort to make our form accessible. Examples in a) and b)\r\n\r\na)https://github.com/opengovsg/FormSG/blob/15e48f56f58df281706c1cb55072eb5bc4f128ac/frontend/src/components/Dropdown/components/MultiSelectCombobox/MultiSelectCombobox.tsx#L88-L106\r\nb)https://github.com/opengovsg/FormSG/blob/15e48f56f58df281706c1cb55072eb5bc4f128ac/frontend/src/components/NumberInput/NumberInput.tsx#L117-L135\r\n\r\n* JSON\r\n\r\n* JWT\r\n\r\n* HTML / CSS / TypeScript\r\n\r\n* Elliptic Curve Cryptography with tweetnacl (reference)\r\n- https://github.com/dchest/tweetnacl-js\r\n- https://github.com/opengovsg/formsg-javascript-sdk/blob/083556f5ef294ce165edb72f588d36706f0a5566/src/util/crypto.ts#L11-L22"
        ],
        "bestPractices": [
            "* agile w/ SCRUM\r\n\r\n* Unit tests\r\n\r\n* End-to-end tests\r\n\r\n* Cross Browser tests with Browserstack\r\n\r\n* Standalone self-contained frontend components that can be tested independently with chromatic and storybook\r\n* PR reviews with required 1 approval before merging. \r\n\r\n* Frontend changes must be approved by designer before a PR can be merged (done with github chromatic action)\r\n\r\n* Monolithic backend application\r\n\r\n* Namespace for API with version in path e.g. /api/v3/forms/<formid>\r\n\r\n* Strong type everything with typescript\r\n\r\n* Validation with joi\r\nhttps://www.npmjs.com/package/joi\r\n\r\n* Separation of model  and Data transfer Objects\r\nhttps://en.wikipedia.org/wiki/Data_transfer_object"
        ],
        "clearOwnership": [
            {
                "clearOwnershipName": "Open Government Products, Government Technology Agency of Singapore",
                "clearOwnershipURL": "https://www.open.gov.sg/products/formsg/ ;\r\n\r\nhttps://www.developer.tech.gov.sg/products/categories/productivity-tools/formsg/overview.html\r\n\r\n"
            }
        ],
        "protectionFromHarassment": {
            "facilitatesUserInteraction": "Yes",
            "harassmentPolicy": "Our main support channel is via Zendesk using the email address support@form.gov.sg or support form: go.gov.sg/formsg-support.  \r\n\r\nWe welcome contributions and provide contribution guidelines and code of conduct policies to ensure a safe and inclusive environment for all.\r\n\r\nContributing guidelines - https://github.com/opengovsg/FormSG/blob/develop/CONTRIBUTING.md ;\r\nCode of conduct - https://github.com/opengovsg/FormSG/blob/develop/CODE_OF_CONDUCT.md"
        },
        "aliases": "",
        "deploymentOrganisations": ""
    }
]
```

### Get a nominee for a digital public goods

Retrieve an individual nominee for digital public goods.

```bash
GET /nominee/{id}/
```

#### Parameters

Name | Type | In | Description
---|---|---|---
`nominee` | string | path | Kebab case name of the nominee, refer to the `id` field returned in the listing of all nominees at `/nominees/`.

#### Code Samples

**Shell**

```bash
curl https://api.digitalpublicgoods.net/nominee/10623/
```
```bash
curl -L https://api.digitalpublicgoods.net/nominee/10623
```

#### Default Response
```
Status: 200 OK
```
```json
{
        "id": "10623",
        "name": "FormSG",
        "sectors": [],
        "stage": "nominee",
        "privacy": [
            {
                "privacyCompliance": "Personal Data protection Act of Singapore",
                "privacyComplianceURL": "Privacy Policy - https://form.gov.sg/privacy"
            }
        ],
        "organizations": [
            {
                "name": "FormSG",
                "website": "https://form.gov.sg ",
                "org_type": "owner",
                "contact_name": " Amit Samdarshi  ",
                "contact_email": "amit@open.gov.sg"
            }
        ],
        "platformIndependence": {
            "isPlatformIndependent": "Yes",
            "openAlternatives": [
                "There are multiple proprietary elements to note:\r\n- integrations with proprietary services",
                " like the Singapore National Identity system Singpass. This cannot be replaced",
                " but adopters may replace authentication systems with whatever identity platform of their country",
                " or disable the identity system altogether\r\n- AWS SQS: formSG operates on AWS and uses some AWS-specific tools",
                " like SQS for webhook retries. That could be replaced quite easily with open source solutions like RabbitMQ.\r\n- FormSG uses AWS SES to send emails. Any other SMTP mailing solution could work.\r\n- FormSG uses AWS S3 for its object store. A custom system for storage (even local with a local NAS)\r\n- For Monitoring and Observability",
                " FormSG integrates to DataDog. This is mostly non-intrusive in code",
                " and could be replaced with other providers. DataDog is a multi-tool system with tracing",
                " metrics",
                " RUM",
                " etc.",
                " each of those could be replaced by something else (open tracing solutions https://opentracing.io/",
                " statsd server https://github.com/statsd/statsd",
                " sentry https://github.com/getsentry/sentry",
                " etc.)\r\n- FormSG uses MongoDB (a document database)",
                " with the mongoose driver https://www.npmjs.com/package/mongoose. With substantial effort",
                " the database could be replaced with another document database like CouchDB."
            ]
        },
        "categories": [
            "Open Software"
        ],
        "description": "FormSG is a form builder tool that enables public officers to instantly create customisable forms with zero code or cost, to safely collect classified and sensitive data.",
        "website": "https://form.gov.sg ",
        "repositories": [
            {
                "name": "main",
                "url": "https://github.com/opengovsg/FormSG"
            }
        ],
        "sdgs": {
            "sdg": [
                "SDG16: Peace\u00b8 Justice and Strong Institutions"
            ],
            "relevance": "SDG INDICATOR 16.6.1 - Governmental expenditures within budgets\r\nFormSG as an open source government form builder provides access to justice for all and build effective, accountable and inclusive institutions at all levels. FormSG is used for government application forms, and also as a reporting and feedback platform by various public agencies.\r\n\r\nSDG INDICATOR 16.6.2 - Satisfaction with public services\r\nWe gather feedback from our members of public using FormSG and have gotten an average satisfaction rating of 4.66 out of 5 over 69,140 feedback submitted. \r\n\r\n"
        },
        "openlicenses": [
            {
                "openLicense": "MIT",
                "openLicenseEvidenceURLs": "https://github.com/opengovsg/FormSG/blob/develop/LICENSE.md"
            }
        ],
        "documentation": "Developer guide: https://github.com/opengovsg/FormSG/blob/develop/README.md\r\n\r\nPublic guide: https://guide.form.gov.sg/\r\n\r\nInformation and contact portal: https://www.developer.tech.gov.sg/products/categories/productivity-tools/formsg/overview.html",
        "NonPII": {
            "collectsNonPII": "Yes",
            "nonPIIAccessMechanism": "The data collected in FormSG can be downloaded in CSV format by the public officer who has created the form. Our form level secret key system ensures that only the person who owns secret key can access the data."
        },
        "dataPrivacySecurity": {
            "collectsPII": "PII data is collected and stored and distributed.",
            "typesOfPIIDataCollected": [
                "The fields are entirely dependent on the public officer who creates the form and how they name the fields (e.g. Name). If they create PII fields",
                " the data from that field would still be end to end encrypted",
                " just like any other field in FormSG forms.  "
            ],
            "dataPrivacySecurity": "We provide data privacy and security through strong end to end encryption created by using form level security keys which only form admin possesses."
        },
        "userContent": {
            "contentManagement": "Content is collected stored and distributed.",
            "contentTypes": [
                "Text and files"
            ],
            "contentManagementPolicy": "The solution does not have any censorship and relies entirely on self-governance of public officers. The platform guarantees that only public officers can log in, thanks to our domain-based OTP login system (i.e. only emails in .gov.sg domain can log in)."
        },
        "locations": {
            "developmentCountries": [
                "Singapore"
            ],
            "deploymentCountries": [
                "Singapore"
            ]
        },
        "deploymentCountriesDepartments": [
            "All statutory boards",
            " ministries and healthcare bodies associated with Singapore Government"
        ],
        "otherDeploymentOrganisations": [
            "Sri Lanka government has forked FormSG to create https://forms.gov.lk/ "
        ],
        "awardsReceived": [
            "MongoDB APAC Innovation Award 2023 for Positive Impact"
        ],
        "openStandards": [
            "* OIDC (used to integrate with the national identity system of Singapore) https://github.com/opengovsg/FormSG/blob/develop/src/app/modules/spcp/spcp.oidc.client.ts\r\n\r\n* Accessibility: We use React + Chakra",
            " and we have spent a lot of effort to make our form accessible. Examples in a) and b)\r\n\r\na)https://github.com/opengovsg/FormSG/blob/15e48f56f58df281706c1cb55072eb5bc4f128ac/frontend/src/components/Dropdown/components/MultiSelectCombobox/MultiSelectCombobox.tsx#L88-L106\r\nb)https://github.com/opengovsg/FormSG/blob/15e48f56f58df281706c1cb55072eb5bc4f128ac/frontend/src/components/NumberInput/NumberInput.tsx#L117-L135\r\n\r\n* JSON\r\n\r\n* JWT\r\n\r\n* HTML / CSS / TypeScript\r\n\r\n* Elliptic Curve Cryptography with tweetnacl (reference)\r\n- https://github.com/dchest/tweetnacl-js\r\n- https://github.com/opengovsg/formsg-javascript-sdk/blob/083556f5ef294ce165edb72f588d36706f0a5566/src/util/crypto.ts#L11-L22"
        ],
        "bestPractices": [
            "* agile w/ SCRUM\r\n\r\n* Unit tests\r\n\r\n* End-to-end tests\r\n\r\n* Cross Browser tests with Browserstack\r\n\r\n* Standalone self-contained frontend components that can be tested independently with chromatic and storybook\r\n* PR reviews with required 1 approval before merging. \r\n\r\n* Frontend changes must be approved by designer before a PR can be merged (done with github chromatic action)\r\n\r\n* Monolithic backend application\r\n\r\n* Namespace for API with version in path e.g. /api/v3/forms/<formid>\r\n\r\n* Strong type everything with typescript\r\n\r\n* Validation with joi\r\nhttps://www.npmjs.com/package/joi\r\n\r\n* Separation of model  and Data transfer Objects\r\nhttps://en.wikipedia.org/wiki/Data_transfer_object"
        ],
        "clearOwnership": [
            {
                "clearOwnershipName": "Open Government Products, Government Technology Agency of Singapore",
                "clearOwnershipURL": "https://www.open.gov.sg/products/formsg/ ;\r\n\r\nhttps://www.developer.tech.gov.sg/products/categories/productivity-tools/formsg/overview.html\r\n\r\n"
            }
        ],
        "protectionFromHarassment": {
            "facilitatesUserInteraction": "Yes",
            "harassmentPolicy": "Our main support channel is via Zendesk using the email address support@form.gov.sg or support form: go.gov.sg/formsg-support.  \r\n\r\nWe welcome contributions and provide contribution guidelines and code of conduct policies to ensure a safe and inclusive environment for all.\r\n\r\nContributing guidelines - https://github.com/opengovsg/FormSG/blob/develop/CONTRIBUTING.md ;\r\nCode of conduct - https://github.com/opengovsg/FormSG/blob/develop/CODE_OF_CONDUCT.md"
        },
        "aliases": "",
        "deploymentOrganisations": ""
    }
```

## :memo: License

```
This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.
```

This repository is licensed under the same terms as the [Digital Public Goods repository](https://github.com/DPGAlliance/publicgoods-candidates): all the information compiled and aggregated in this repository is already in the public domain, thus we dedicate this software to the public domain. As a result, we impose no limitations nor requirements of any kind of how you use it or reuse it. As a courtesy on your part, we would very much appreciate hearing from you either on how you are using the information in this repo, or any great ideas on how we can collaborate together.
Email us at hello@digitalpublicgoods.net 💌
