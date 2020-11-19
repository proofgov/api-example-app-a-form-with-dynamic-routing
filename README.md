# Examples for using Proof's API for Form related interactions

This documentation will give you with information on how to create and manage form configurations, as well as, submit data for the given form configuration and work with the results of the submission.

Proof, at the momment, supports 3 types of form providers; [FormHero](https://www.formhero.com/), [Drupal Webforms](https://www.drupal.org/project/webform) and an generic form provider which we call Proof forms.

This documantaion will cover how to use the Proof provider forms.

## Requirements

Before you can interface with Proof's API, you need two pieces of information:

- URL for Proof's app endpoint ([app.proofgov.com](https://app.proofgov.com))
- API token (obtained from Proof's systems)

For all examples below we will use the following

```js
axios = require('axios') // learn more at: https://github.com/axios/axios#axios-api
PROOF_API_HOST = process.env.PROOF_API_HOST
PROOF_API_TOKEN = process.env.PROOF_API_TOKEN
```

### Providing the API token to Proof.

Any request you make to Proof's backend will need an API token. To send your token, you must send it via the header `Authorization`.

Example:

```js
axios({
  headers: {
    Authorization: `Bearer ${PROOF_API_TOKEN}`,
  },
})
```

## Getting Started

All the examples below will use Javascript and [axios](https://github.com/axios/axios#axios-api).

### Form Configuration

#### Creating a new configuration

Form configrations need an unique identifier (thoughout Proof's tenants). We recommend prefixing all your `provider_identifier` with a company name or government name to make sure it is truely unique.

For this example, we will use `company-name/access-form` as the `provider_identifier`.

```js
axios({
  method: 'POST',
  url: `${PROOF_API_HOST}/api/forms`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
  data: {
    form_config: {
      provider_identifier: 'company-name/access-form',
    },
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": {
      "id": 1,
      "cacheKey": "form_configs/1",
      "createdAt": "2020-11-18T22:28:04.203+0000",
      "displayKey": "1",
      "errors": {},
      "formHeroIdentifier": null,
      "intakeUrl": null,
      "logs": [],
      "provider": "proof",
      "providerIdentifier": "company-name/access-form",
      "slug": "1",
      "submitFlowChain": [
        [
          "FormSubmissions::CreateAndLinkParentRoutingFlow",
          [
            {}
          ],
          {}
        ]
      ],
      "updatedAt": "2020-11-18T22:28:04.203+0000",
      "webhookUrl": null
    },
    "meta": {
      "policy": {
        "modelId": 1,
        "modelType": "FormConfig",
        "userId": 4,
        "create": true,
        "exportAllSubmissions": true,
        "showAnalytics": true,
        "update": true,
        "updateFlow": true,
        "destroy": true,
        "querySubmissions": true,
        "authorized": true,
        "submit": true,
        "show": true,
        "new": true,
        "edit": true,
        "export": true,
        "visibilityMode": 1,
        "permittedAttributes": [
          "provider",
          "provider_identifier"
        ]
      }
    }
  }
  ```
</details>

#### List available configurations

```js
axios({
  method: 'GET',
  url: `${PROOF_API_HOST}/api/forms`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": [
      {
        "id": 1,
        "cacheKey": "form_configs/1",
        "createdAt": "2020-11-12T21:09:29.136+0000",
        "displayKey": "1",
        "errors": {},
        "formHeroIdentifier": null,
        "intakeUrl": null,
        "logs": [],
        "provider": "proof",
        "providerIdentifier": "company-name/access-form",
        "slug": "1",
        "submitFlowChain": [
          [
            "FormSubmissions::CreateAndLinkParentRoutingFlow",
            [
              {}
            ],
            {}
          ]
        ],
        "updatedAt": "2020-11-12T21:09:29.136+0000",
        "webhookUrl": null
      }
    ],
    "meta": {}
  }
  ```
</details>

#### Update a form configuration

To update a configuration's provider_identifier, you must target the `slug` of the form config in the URL (aka `1`)

```js
axios({
  method: 'PUT',
  url: `${PROOF_API_HOST}/api/forms/1`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
  data: {
    form_config: {
      provider_identifier: 'company-name/access-form-changed',
    },
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
    {
      "data": {
        "id": 1,
        "cacheKey": "form_configs/1",
        "createdAt": "2020-11-12T21:09:29.136+0000",
        "displayKey": "1",
        "errors": {},
        "formHeroIdentifier": null,
        "intakeUrl": null,
        "logs": [],
        "provider": "proof",
        "providerIdentifier": "company-name/access-form-changed",
        "slug": "1",
        "submitFlowChain": [
          [
            "FormSubmissions::CreateAndLinkParentRoutingFlow",
            [
              {}
            ],
            {}
          ]
        ],
        "updatedAt": "2020-11-12T23:16:37.630+0000",
        "webhookUrl": null
      },
      "meta": {}
    }
  ```
</details>

#### Deleting a form configuration

To delete a configuration, you must target the `slug` attribute value of the form config in the URL (aka `3`)

```js
axios({
  method: 'DELETE',
  url: `${PROOF_API_HOST}/api/forms/3`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": {
      "id": 3,
      "cacheKey": "form_configs/3",
      "createdAt": "2020-11-12T23:50:14.007+0000",
      "displayKey": "3",
      "errors": {},
      "formHeroIdentifier": null,
      "intakeUrl": null,
      "logs": [],
      "provider": "proof",
      "providerIdentifier": "company-name/access-form-2",
      "slug": "3",
      "submitFlowChain": [
        [
          "FormSubmissions::CreateAndLinkParentRoutingFlow",
          [
            {}
          ],
          {}
        ]
      ],
      "updatedAt": "2020-11-12T23:50:14.007+0000",
      "webhookUrl": null
    },
    "meta": {}
  }
  ```
</details>

**NOTE: You are unable to delete a form configuration that has any submissions associated with it.**

### Working with Schemata for your form config

Schemata tell Proof how to render your form (and it's sbumission) when you submits data to the Proof application.

Learn more about [Proof Form Schema](schema.md)

Note that we are targetting the form config with the `slug` value of 1 in the below examples.

#### Creating a new schema

Note: Your schema must meet some requirements outlined in the [Proof Form Schema section](schema.md)

If you choose not to provide a version, Proof will autogenerate a version number.

```js
axios({
  method: 'POST',
  url: `${PROOF_API_HOST}/api/forms/1/schemata`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
  data: {
    version: 'v3',
    schema: {
      sections: [
        {
          label: 'User Details',
          fields: [
            {
              binding: 'user.first_name',
              label: 'First Name',
              type: 'string',
            },
            {
              binding: 'user.last_name',
              label: 'Last Name',
              type: 'string',
            },
            {
              binding: 'user.age',
              label: 'Age',
              type: 'number',
            },
          ],
        },
      ],
    },
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 201
  
  ```json
  {
    "data": {
      "version": "v3",
      "slug": "v3",
      "schema": {
        "sections": [
          {
            "fields": [
              {
                "binding": "user.first_name",
                "label": "First Name",
                "type": "string"
              },
              {
                "binding": "user.last_name",
                "label": "Last Name",
                "type": "string"
              },
              {
                "binding": "user.age",
                "label": "Age",
                "type": "number"
              }
            ],
            "label": "User Details"
          }
        ]
      }
    },
    "meta": {}
  }
  ```
</details>

#### List schemata

```js
axios({
  method: 'GET',
  url: `${PROOF_API_HOST}/api/forms/1/schemata`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": [
      {
        "version": "v2",
        "slug": "v2",
        "schema": {
          "sections": [
            {
              "label": "User Details",
              "fields": [
                {
                  "type": "string",
                  "label": "First Name",
                  "binding": "user.first_name"
                },
                {
                  "type": "string",
                  "label": "Last Name",
                  "binding": "user.last_name"
                },
                {
                  "type": "number",
                  "label": "User Age",
                  "binding": "user.age"
                }
              ]
            }
          ]
        }
      },
      {
        "version": "v3",
        "slug": "v3",
        "schema": {
          "sections": [
            {
              "label": "User Details",
              "fields": [
                {
                  "type": "string",
                  "label": "First Name",
                  "binding": "user.first_name"
                },
                {
                  "type": "string",
                  "label": "Last Name",
                  "binding": "user.last_name"
                },
                {
                  "type": "number",
                  "label": "Age",
                  "binding": "user.age"
                }
              ]
            }
          ]
        }
      }
    ],
    "meta": {}
  }
  ```
</details>

#### Get a specific schema version

To target a specific schema version, you must provide the `slug` attribute value of the schema in the URL (aka `v3`). Note if your slug has a `.` in the name, you must encode it in the URL (`.` = `%2E`).

```js
axios({
  method: 'GET',
  url: `${PROOF_API_HOST}/api/forms/1/schemata/v3`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": {
      "version": "v3",
      "slug": "v3",
      "schema": {
        "sections": [
          {
            "label": "User Details",
            "fields": [
              {
                "type": "string",
                "label": "First Name",
                "binding": "user.first_name"
              },
              {
                "type": "string",
                "label": "Last Name",
                "binding": "user.last_name"
              },
              {
                "type": "number",
                "label": "Age",
                "binding": "user.age"
              }
            ]
          }
        ]
      }
    },
    "meta": {}
  }
  ```
</details>

#### Update a specific schema version

To update a specific schema version, you must target the `slug` attribute value of the schema in the URL (aka `v3`). Note if your slug has a `.` in the name, you must encode it in the URL (`.` = `%2E`).

Please note that you **must provide a complete schema** to update. We currently do not support partial updates.

```js
axios({
  method: 'PUT',
  url: `${PROOF_API_HOST}/api/forms/1/schemata/v3`,
  headers: {
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
    'Content-Type': 'application/json; charset=utf-8',
  },
  data: {
    sections: [
      {
        label: 'User Details',
        id: 'main-section',
        fields: [
          {
            binding: 'user.first_name',
            label: 'First Name Changed',
            type: 'string',
          },
          {
            binding: 'user.last_name',
            label: 'Last Name Changed',
            type: 'string',
          },
          {
            binding: 'user.birthYear',
            label: 'Birth Year',
            type: 'number',
          },
        ],
      },
    ],
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": {
      "version": "v3",
      "slug": "v3",
      "schema": {
        "sections": [
          {
            "fields": [
              {
                "binding": "user.first_name",
                "label": "First Name Changed",
                "type": "string"
              },
              {
                "binding": "user.last_name",
                "label": "Last Name Changed",
                "type": "string"
              },
              {
                "binding": "user.birthYear",
                "label": "Birth Year",
                "type": "number"
              }
            ],
            "label": "User Details",
            "id": "main-section"
          }
        ]
      }
    },
    "meta": {}
  }
  ```
</details>

#### Delete a schema

To delete a specific schema version, you must target the `slug` attribute value of the schema in the URL (aka `v2`). Note if your slug has a `.` in the name, you must encode it in the URL (`.` = `%2E`).

```js
axios({
  method: 'DELETE',
  url: `${PROOF_API_HOST}/api/forms/1/schemata/v2`,
  headers: {
    Authorization: `Bearer ${PROOF_API_TOKEN}`,
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": {
      "version": "v2",
      "slug": "v2",
      "schema": {
        "sections": [
          {
            "label": "User Details",
            "fields": [
              {
                "type": "string",
                "label": "First Name",
                "binding": "user.first_name"
              },
              {
                "type": "string",
                "label": "Last Name",
                "binding": "user.last_name"
              },
              {
                "type": "number",
                "label": "User Age",
                "binding": "user.age"
              }
            ]
          }
        ]
      }
    },
    "meta": {}
  }
  ```
</details>

### Submitting form data

Form Submissions are treated uniquely, as Proof will always accept submissions, even if we do not know how to process them. This is because Proof does NOT want to lose data. Submissions that are processed correctly will return a status code of `201` (Created). Submissions that DO NOT get processed by the backend will return a status code of `202` (Accepted). Note: At the moment, you will NOT be able to find submissions that returned a status code of `202`. To do something with those submissions, you will have to reach out to support at Proof to locate and act on submission that were not processed correctly.

There are two ways to submit form data.

1. [Targeted Submission](#targeted-submission)
2. [General Submission](#general-submission)

#### Targeted Submission

Targeted submissions refer to how the URL and submission data look like. Targeted submission have the form config ID in the URL to ensure Proof processes the submission using the correct form configration. The submission data does not require anything specific.

The URL structure looks like this; `${PROOF_API_HOST}/forms/proof/1/submit`. This URL does not reference the API namespace and he Form Config ID (`1`) is being targeted in the URL.

Also note that there is no `Authorization` token in the header. This endpoint will take public submissions.

```js
axios({
  method: 'POST',
  url: `${PROOF_API_HOST}/forms/proof/1/submit`,
  headers: {
    'Content-Type': 'application/json; charset=utf-8',
  },
  data: {
    'user.first_name': 'Frank',
    'user.age': '31',
    'user.last_name': 'Johns',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 201
  
  ```json
    {
      "data": {
        "id": 2,
        "cache_key": "form_submissions/2",
        "data": {
          "user.first_name": "Frank",
          "user.last_name": "Johns",
          "user.age": "31"
        },
        "display_key": "2",
        "errors": {},
        "form_config_id": 1,
        "host": {
          "id": 36,
          "cache_key": "routings/36",
          "closed_on": null,
          "creator_id": 3,
          "deadline": null,
          "display_key": "PROOF-36",
          "errors": {},
          "extension_values": [],
          "priority": null,
          "routing_type": null,
          "slug": "PROOF-36",
          "status": "open",
          "steps_summary": {
            "total": 0,
            "completed": 0,
            "progress": 0
          },
          "title": null,
          "unit": {
            "id": 3,
            "acronym": "DU",
            "cache_key": "units/3",
            "created_at": "2020-11-18T22:14:45.685+0000",
            "display_key": "3",
            "errors": {},
            "is_default": true,
            "name": "Default Unit",
            "sequence_id": null,
            "sharepoint_library_name": null,
            "slug": "3",
            "updated_at": "2020-11-18T22:14:45.685+0000",
            "using_sharepoint": false
          },
          "unit_id": 3,
          "url": "/routings/PROOF-36"
        },
        "slug": "2"
      },
      "meta": {}
    }
  ```
</details>

#### General Submission

General submissions refer to how the URL and sumbittion data are structured. General submissions do NOT provide a form config in the URL, however, the submission data must include an attribute of `proof.provider_identifier` with the value that matches your Form Config's `provider_identifier`.

URL structure looks like `${PROOF_API_HOST}/forms/proof/submit`. Note that the URL is not referencing the API namespace nor a Form Config ID.

Also note that there is no `Authorization` token in the header. This endpoint will take public submissions.

```js
axios({
  method: 'POST',
  url: `${PROOF_API_HOST}/forms/proof/submit`,
  headers: {
    'Content-Type': 'application/json; charset=utf-8',
  },
  data: {
    'proof.provider_identifier': 'company-name/access-form',
    'user.last_name': 'Franklin',
    'user.age': '73',
    'user.first_name': 'Steve',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 201

NOTE: that `form_config_id` set correctly to `1`

```json
{
  "data": {
    "id": 3,
    "cache_key": "form_submissions/3",
    "data": {
      "proof.provider_identifier": "company-name/access-form",
      "user.first_name": "Steve",
      "user.age": "73",
      "user.last_name": "Franklin"
    },
    "display_key": "3",
    "errors": {},
    "form_config_id": 1,
    "host": {
      "id": 37,
      "cache_key": "routings/37",
      "closed_on": null,
      "creator_id": 3,
      "deadline": null,
      "display_key": "PROOF-37",
      "errors": {},
      "extension_values": [],
      "priority": null,
      "routing_type": null,
      "slug": "PROOF-37",
      "status": "open",
      "steps_summary": {
        "total": 0,
        "completed": 0,
        "progress": 0
      },
      "title": null,
      "unit": {
        "id": 3,
        "acronym": "DU",
        "cache_key": "units/3",
        "created_at": "2020-11-18T22:14:45.685+0000",
        "display_key": "3",
        "errors": {},
        "is_default": true,
        "name": "Default Unit",
        "sequence_id": null,
        "sharepoint_library_name": null,
        "slug": "3",
        "updated_at": "2020-11-18T22:14:45.685+0000",
        "using_sharepoint": false
      },
      "unit_id": 3,
      "url": "/routings/PROOF-37"
    },
    "slug": "3"
  },
  "meta": {}
}
```

</details>

#### Debugging a form submission

In some cases, You might want to see how Proof is matching your submission data. For this, Proof provides a `debug` url.

```js
axios({
  method: 'POST',
  url: `${PROOF_API_HOST}/forms/proof/1/submit/debug`,
  headers: {
    'Content-Type': 'application/json; charset=utf-8',
  },
  data: {
    'user.first_name': 'Steve',
    'user.missing_binding': 'This is not in the schema',
    'user.last_name': 'Franklin',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "schema_version": "v3",
    "available_bindings": {
      "user.first_name": {
        "type": "string",
        "label": "First Name",
        "binding": "user.first_name"
      },
      "user.last_name": {
        "type": "string",
        "label": "Last Name",
        "binding": "user.last_name"
      },
      "user.age": {
        "type": "number",
        "label": "User Age",
        "binding": "user.age"
      }
    },
    "matches": {
      "user.first_name": {
        "type": "string",
        "label": "First Name",
        "binding": "user.first_name"
      },
      "user.last_name": {
        "type": "string",
        "label": "Last Name",
        "binding": "user.last_name"
      },
      "user.missing_binding": null
    }
  }
  ```
</details>

### Working with Form Submissions

#### Listing submissions

```js
axios({
  method: 'GET',
  url: `${PROOF_API_HOST}/api/forms/1/submissions`,
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": [
      {
        "id": 2,
        "cache_key": "form_submissions/2",
        "data": {
          "user.age": "31",
          "user.last_name": "Johns",
          "user.first_name": "Frank"
        },
        "display_key": "2",
        "errors": {},
        "form_config_id": 1,
        "host": {
          "id": 36,
          "cache_key": "routings/36",
          "closed_on": null,
          "creator_id": 3,
          "deadline": null,
          "display_key": "PROOF-36",
          "errors": {},
          "extension_values": [],
          "priority": null,
          "routing_type": null,
          "slug": "PROOF-36",
          "status": "open",
          "steps_summary": {
            "total": 0,
            "completed": 0,
            "progress": 0
          },
          "title": null,
          "unit": {
            "id": 3,
            "acronym": "DU",
            "cache_key": "units/3",
            "created_at": "2020-11-18T22:14:45.685+0000",
            "display_key": "3",
            "errors": {},
            "is_default": true,
            "name": "Default Unit",
            "sequence_id": null,
            "sharepoint_library_name": null,
            "slug": "3",
            "updated_at": "2020-11-18T22:14:45.685+0000",
            "using_sharepoint": false
          },
          "unit_id": 3,
          "url": "/routings/PROOF-36"
        },
        "slug": "2"
      },
      {
        "id": 3,
        "cache_key": "form_submissions/3",
        "data": {
          "user.age": "73",
          "user.last_name": "Franklin",
          "user.first_name": "Steve",
          "proof.provider_identifier": "company-name/access-form"
        },
        "display_key": "3",
        "errors": {},
        "form_config_id": 1,
        "host": {
          "id": 37,
          "cache_key": "routings/37",
          "closed_on": null,
          "creator_id": 3,
          "deadline": null,
          "display_key": "PROOF-37",
          "errors": {},
          "extension_values": [],
          "priority": null,
          "routing_type": null,
          "slug": "PROOF-37",
          "status": "open",
          "steps_summary": {
            "total": 0,
            "completed": 0,
            "progress": 0
          },
          "title": null,
          "unit": {
            "id": 3,
            "acronym": "DU",
            "cache_key": "units/3",
            "created_at": "2020-11-18T22:14:45.685+0000",
            "display_key": "3",
            "errors": {},
            "is_default": true,
            "name": "Default Unit",
            "sequence_id": null,
            "sharepoint_library_name": null,
            "slug": "3",
            "updated_at": "2020-11-18T22:14:45.685+0000",
            "using_sharepoint": false
          },
          "unit_id": 3,
          "url": "/routings/PROOF-37"
        },
        "slug": "3"
      }
    ],
    "meta": {
      "pagination": {
        "current_page": 1,
        "total_pages": 1,
        "total_count": 2,
        "per_page": 25
      }
    }
  }
  ```
</details>

#### Get a specific Form Submission

To taget a specific form submission, you must provide the `slug` value (`2`) of the form submission

```js
axios({
  method: 'GET',
  url: `${PROOF_API_HOST}/api/forms/1/submissions/2`,
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
    {
      "data": {
        "id": 2,
        "cache_key": "form_submissions/2",
        "data": {
          "user.age": "31",
          "user.last_name": "Johns",
          "user.first_name": "Frank"
        },
        "display_key": "2",
        "errors": {},
        "form_config_id": 1,
        "host": {
          "id": 36,
          "cache_key": "routings/36",
          "closed_on": null,
          "creator_id": 3,
          "deadline": null,
          "display_key": "PROOF-36",
          "errors": {},
          "extension_values": [],
          "priority": null,
          "routing_type": null,
          "slug": "PROOF-36",
          "status": "open",
          "steps_summary": {
            "total": 0,
            "completed": 0,
            "progress": 0
          },
          "title": null,
          "unit": {
            "id": 3,
            "acronym": "DU",
            "cache_key": "units/3",
            "created_at": "2020-11-18T22:14:45.685+0000",
            "display_key": "3",
            "errors": {},
            "is_default": true,
            "name": "Default Unit",
            "sequence_id": null,
            "sharepoint_library_name": null,
            "slug": "3",
            "updated_at": "2020-11-18T22:14:45.685+0000",
            "using_sharepoint": false
          },
          "unit_id": 3,
          "url": "/routings/PROOF-36"
        },
        "schema": {
          "sections": [
            {
              "label": "User Details",
              "fields": [
                {
                  "type": "string",
                  "label": "First Name",
                  "binding": "user.first_name"
                },
                {
                  "type": "string",
                  "label": "Last Name",
                  "binding": "user.last_name"
                },
                {
                  "type": "number",
                  "label": "User Age",
                  "binding": "user.age"
                }
              ]
            }
          ]
        },
        "slug": "2"
      },
      "meta": {
        "policy": {
          "model_id": 2,
          "model_type": "FormSubmission",
          "user_id": 4,
          "destroy": true,
          "authorized": true,
          "show": true,
          "update": true,
          "create": true,
          "new": true,
          "edit": true,
          "export": true,
          "visibility_mode": 1,
          "permitted_attributes": []
        }
      }
    }
  ```
</details>

#### Update data on a specific form submission

You must provide the full data object to replace the current submission data

```js
axios({
  method: 'PUT',
  url: `${PROOF_API_HOST}/api/forms/1/submissions/2`,
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
  },
  data: {
    submission: {
      data: {
        'user.age': '32',
        'user.first_name': 'Frank',
        'user.last_name': 'Johnson',
      },
    },
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": {
      "id": 2,
      "cache_key": "form_submissions/2",
      "data": {
        "user.age": "32",
        "user.last_name": "Johnson",
        "user.first_name": "Frank"
      },
      "display_key": "2",
      "errors": {},
      "form_config_id": 1,
      "host": {
        "id": 36,
        "cache_key": "routings/36",
        "closed_on": null,
        "creator_id": 3,
        "deadline": null,
        "display_key": "PROOF-36",
        "errors": {},
        "extension_values": [],
        "priority": null,
        "routing_type": null,
        "slug": "PROOF-36",
        "status": "open",
        "steps_summary": {
          "total": 0,
          "completed": 0,
          "progress": 0
        },
        "title": null,
        "unit": {
          "id": 3,
          "acronym": "DU",
          "cache_key": "units/3",
          "created_at": "2020-11-18T22:14:45.685+0000",
          "display_key": "3",
          "errors": {},
          "is_default": true,
          "name": "Default Unit",
          "sequence_id": null,
          "sharepoint_library_name": null,
          "slug": "3",
          "updated_at": "2020-11-18T22:14:45.685+0000",
          "using_sharepoint": false
        },
        "unit_id": 3,
        "url": "/routings/PROOF-36"
      },
      "schema": {
        "sections": [
          {
            "label": "User Details",
            "fields": [
              {
                "type": "string",
                "label": "First Name",
                "binding": "user.first_name"
              },
              {
                "type": "string",
                "label": "Last Name",
                "binding": "user.last_name"
              },
              {
                "type": "number",
                "label": "User Age",
                "binding": "user.age"
              }
            ]
          }
        ]
      },
      "slug": "2"
    },
    "meta": {
      "policy": {
        "model_id": 2,
        "model_type": "FormSubmission",
        "user_id": 4,
        "destroy": true,
        "authorized": true,
        "show": true,
        "update": true,
        "create": true,
        "new": true,
        "edit": true,
        "export": true,
        "visibility_mode": 1,
        "permitted_attributes": []
      }
    }
  }
  ```
</details>

#### Update only a spcific binding on a form submission

In most cases, you will only want to update a specific binding, Proof provides a URL to do this: `api/forms/1/submissions/2/binding`. You must provide `binding` and `value`.

```js
axios({
  method: 'PUT',
  url: `${PROOF_API_HOST}/api/forms/1/submissions/2/binding`,
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${PROOF_API_TOKEN}`,
  },
  data: {
    value: 'Bob',
    binding: 'user.first_name',
  },
})
```

<details>
  <summary>Server Response</summary>
  Status Code: 200
  
  ```json
  {
    "data": {
      "id": 2,
      "cache_key": "form_submissions/2",
      "data": {
        "user.age": "32",
        "user.last_name": "Johnson",
        "user.first_name": "Bob"
      },
      "display_key": "2",
      "errors": {},
      "form_config_id": 1,
      "host": {
        "id": 36,
        "cache_key": "routings/36",
        "closed_on": null,
        "creator_id": 3,
        "deadline": null,
        "display_key": "PROOF-36",
        "errors": {},
        "extension_values": [],
        "priority": null,
        "routing_type": null,
        "slug": "PROOF-36",
        "status": "open",
        "steps_summary": {
          "total": 0,
          "completed": 0,
          "progress": 0
        },
        "title": null,
        "unit": {
          "id": 3,
          "acronym": "DU",
          "cache_key": "units/3",
          "created_at": "2020-11-18T22:14:45.685+0000",
          "display_key": "3",
          "errors": {},
          "is_default": true,
          "name": "Default Unit",
          "sequence_id": null,
          "sharepoint_library_name": null,
          "slug": "3",
          "updated_at": "2020-11-18T22:14:45.685+0000",
          "using_sharepoint": false
        },
        "unit_id": 3,
        "url": "/routings/PROOF-36"
      },
      "schema": {
        "sections": [
          {
            "label": "User Details",
            "fields": [
              {
                "type": "string",
                "label": "First Name",
                "binding": "user.first_name"
              },
              {
                "type": "string",
                "label": "Last Name",
                "binding": "user.last_name"
              },
              {
                "type": "number",
                "label": "User Age",
                "binding": "user.age"
              }
            ]
          }
        ]
      },
      "slug": "2"
    },
    "meta": {
      "policy": {
        "model_id": 2,
        "model_type": "FormSubmission",
        "user_id": 4,
        "destroy": true,
        "authorized": true,
        "show": true,
        "update": true,
        "create": true,
        "new": true,
        "edit": true,
        "export": true,
        "visibility_mode": 1,
        "permitted_attributes": []
      }
    }
  }
  ```
</details>
