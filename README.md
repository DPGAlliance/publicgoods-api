# API for Digital Public Goods

Application Programming Interface (API) for Digital Public Goods. 

Refer to the [Digital Public Goods repository](https://github.com/unicef/publicgoods-candidates) for additional documentation.

## Overview

This repository provides a *static* snapshot of an API that can be accessed at `https://api.digitalpublicgoods.net`, where only `GET` endpoints are available.

This API provides an alternative method of accessing the information available at https://github.com/unicef/publicgoods-candidates. 

Yet for another alternative, a more user-friendly version, you can browse the [Digital Public Goods Registry](https://digitalpublicgoods.net/registry).

## Architecture

This API leverages [GitHub Pages](https://pages.github.com/) for hosting, and [GitHub Actions](https://github.com/features/actions) for automatic syncing its contents with the source of truth that lives in the [Digital Public Goods repository](https://github.com/unicef/publicgoods-candidates).

Because of the structure imposed by **GitHub Pages**, all the JSON files are stored inside the `docs/` folder, and served from there. For convenience a softlink is provided from `api/` to `docs/`. The files for each individual endpoint (e.g. `dpg/{dpg}/` and `nominee/{nominee}/`) are pregenerated and stored in correspondingly-named folders with a `index.json` file inside. This folder and file structure accomplishes making the API available in the static infrastrcture that GitHub Pages provides.

⚠️ Please note the trailing `/` at the end of all endpoints, which is an artifact of this setup. If you do not include it, you need your code to follow automatic redirects. Any endpoint without trailing slash returns a `301` redirect to the same path with a trailing slash.

## Reference

### List digital public goods

List all digital public goods screened against the [Digital Public Goods Standard](https://github.com/DPGAlliance/DPG-Standard/).

```bash
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
