[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v2.0%20adopted-ff69b4.svg)](CODE_OF_CONDUCT.md)
# API for Digital Public Goods

Application Programming Interface (API) for Digital Public Goods, available at https://api.digitalpublicgoods.net.

This API provides an alternative method of accessing the information available at https://github.com/DPGAlliance/publicgoods-candidates. 

Yet for another alternative, a more user-friendly version, you can browse the [Digital Public Goods Registry](https://digitalpublicgoods.net/registry).

## Architecture

This API leverages [GitHub Pages](https://pages.github.com/) for hosting, and [GitHub Actions](https://github.com/features/actions) for automatic syncing its contents with the source of truth that lives in the [Digital Public Goods repository](https://github.com/DGPAlliance/publicgoods-candidates).

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
	"dpg/{dpg}": "https://api.digitalpublicgoods.net/dpg/{dpg}/",
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
    "id": "african-storybook",
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
GET /dpg/{dpg}/
```

#### Parameters

Name | Type | In | Description
---|---|---|---
`dpg` | string | path | Kebab case name of the digital public good, refer to the `id` field returned in the listing of all digital public goods at `/dpgs/`.

#### Code Samples

**Shell**

```bash
curl https://api.digitalpublicgoods.net/dpg/african-storybook/
```
```bash
curl -L https://api.digitalpublicgoods.net/dpg/african-storybook
```

#### Default Response
```
Status: 200 OK
```
```json
{
  "id": "african-storybook",
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
    "id": "@firma",
    "name": "@firma",
    "description": "Suite of solutions for digital identities and electronic signatures, aimed at public administrations for the implementation of authentication and electronic signatures in a streamlined and effective manner.",
    "website": "https://administracionelectronica.gob.es/ctt/clienteafirma",
    "license": [
      {
        "spdx": "GPL-2.0",
        "licenseURL": "https://github.com/ctt-gob-es/clienteafirma/blob/master/license/LICENSE.txt"
      }
    ],
    "SDGs": [
      {
        "SDGNumber": 3
      },
      {
        "SDGNumber": 16
      }
    ],
    "sectors": [],
    "type": [
      "software"
    ],
    "repositoryURL": "https://github.com/ctt-gob-es/clienteafirma",
    "organizations": [
      {
        "name": "Technology Transfer Center, Government of Spain",
        "website": "https://administracionelectronica.gob.es/",
        "org_type": "owner"
      }
    ],
    "stage": "nominee"
  }
]
```

### Get a nominee for a digital public goods

Retrieve an individual nominee for digital public goods.

```bash
GET /nominee/{nominee}/
```

#### Parameters

Name | Type | In | Description
---|---|---|---
`nominee` | string | path | Kebab case name of the nominee, refer to the `id` field returned in the listing of all nominees at `/nominees/`.

#### Code Samples

**Shell**

```bash
curl https://api.digitalpublicgoods.net/nominee/\@firma/
```
```bash
curl -L https://api.digitalpublicgoods.net/nominee/\@firma
```

#### Default Response
```
Status: 200 OK
```
```json
{
  "id": "@firma",
  "name": "@firma",
  "description": "Suite of solutions for digital identities and electronic signatures, aimed at public administrations for the implementation of authentication and electronic signatures in a streamlined and effective manner.",
  "website": "https://administracionelectronica.gob.es/ctt/clienteafirma",
  "license": [
    {
      "spdx": "GPL-2.0",
      "licenseURL": "https://github.com/ctt-gob-es/clienteafirma/blob/master/license/LICENSE.txt"
    }
  ],
  "SDGs": [
    {
      "SDGNumber": 3
    },
    {
      "SDGNumber": 16
    }
  ],
  "sectors": [],
  "type": [
    "software"
  ],
  "repositoryURL": "https://github.com/ctt-gob-es/clienteafirma",
  "organizations": [
    {
      "name": "Technology Transfer Center, Government of Spain",
      "website": "https://administracionelectronica.gob.es/",
      "org_type": "owner"
    }
  ],
  "stage": "nominee"
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
