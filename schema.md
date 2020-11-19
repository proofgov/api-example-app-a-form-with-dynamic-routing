# Proof Form Config Schemata

## What is a Schemata?

The plural form of schema is schemata or schemas

## What is a Form Schema?

A form schema is mata data of how to render a form submission. It includes the sections and fields of a submission.

## Section

Sections are used to divide the fields. An example of sections are "User Details" and "Building Information".

## Field

A field is one data point. A field has a `binding` attribute (think of this as a lookup id), a user readable `label` attribute and a `type` attribute (string, number, date, checkbox, multiple choice).

## From Schema Schema

This is the schema Proof validates all incoming FormSchemas againts.

```json
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "id": "FORM",
  "title": "a form builder schema",
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    },
    "cuid": {
      "type": "string"
    },
    "title": {
      "type": "string"
    },
    "created_at": {
      "type": "string"
    },
    "sections": {
      "title": "form sections",
      "type": "array",
      "minItems": 1,
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string"
          },
          "label": {
            "type": "string"
          },
          "fields": {
            "title": "section fields",
            "type": "array",
            "minItems": 1,
            "items": {
              "allOf": [
                {
                  "title": "Field Values",
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string"
                    },
                    "binding": {
                      "type": "string"
                    },
                    "label": {
                      "type": "string"
                    }
                  },
                  "required": ["binding", "label", "type"]
                },
                {
                  "oneOf": [
                    {
                      "title": "Checkbox type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "checkbox"
                        }
                      }
                    },
                    {
                      "title": "Date and DateTime types",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "^(date|datetime)?$"
                        }
                      },
                      "additionalProperties": {
                        "type": "string"
                      }
                    },
                    {
                      "title": "Dropdown type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "^(dropdown|multicheck)?$"
                        },
                        "choices": {
                          "type": "array",
                          "minItems": 1,
                          "items": {
                            "type": "object",
                            "properties": {
                              "label": {
                                "type": "string"
                              },
                              "value": {
                                "anyOf": [
                                  {
                                    "type": "boolean"
                                  },
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "string"
                                  }
                                ]
                              }
                            }
                          }
                        }
                      },
                      "additionalProperties": {
                        "type": "string"
                      }
                    },
                    {
                      "title": "Email type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "e-mail"
                        }
                      }
                    },
                    {
                      "title": "File Upload type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "^file$"
                        }
                      }
                    },
                    {
                      "title": "HTML type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "html"
                        },
                        "markup": {
                          "type": "string"
                        }
                      }
                    },
                    {
                      "title": "Number type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "^number$"
                        }
                      },
                      "additionalProperties": {
                        "type": "string"
                      }
                    },
                    {
                      "title": "Text type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "^(text|long-text|string)?$"
                        }
                      },
                      "additionalProperties": {
                        "type": "string"
                      }
                    },
                    {
                      "title": "Tabular Data type",
                      "type": "object",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "tabular"
                        },
                        "fields": {
                          "title": "Tabular field items",
                          "type": "array",
                          "items": {
                            "allOf": [
                              {
                                "title": "Tabular Values",
                                "type": "object",
                                "properties": {
                                  "id": {
                                    "type": "string"
                                  },
                                  "binding": {
                                    "type": "string"
                                  },
                                  "label": {
                                    "type": "string"
                                  }
                                },
                                "required": ["binding", "label", "type"]
                              },
                              {
                                "oneOf": [
                                  {
                                    "title": "Checkbox type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "checkbox"
                                      }
                                    }
                                  },
                                  {
                                    "title": "Date and DateTime types",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "^(date|datetime)?$"
                                      }
                                    },
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  {
                                    "title": "Dropdown type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "^(dropdown|multicheck)?$"
                                      },
                                      "choices": {
                                        "type": "array",
                                        "minItems": 1,
                                        "items": {
                                          "type": "object",
                                          "properties": {
                                            "label": {
                                              "type": "string"
                                            },
                                            "value": {
                                              "anyOf": [
                                                {
                                                  "type": "boolean"
                                                },
                                                {
                                                  "type": "number"
                                                },
                                                {
                                                  "type": "string"
                                                }
                                              ]
                                            }
                                          }
                                        }
                                      }
                                    },
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  {
                                    "title": "Email type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "e-mail"
                                      }
                                    }
                                  },
                                  {
                                    "title": "File Upload type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "^file$"
                                      }
                                    }
                                  },
                                  {
                                    "title": "HTML type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "html"
                                      },
                                      "markup": {
                                        "type": "string"
                                      }
                                    }
                                  },
                                  {
                                    "title": "Number type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "^number$"
                                      }
                                    },
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  {
                                    "title": "Text type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "^(text|long-text|string)?$"
                                      }
                                    },
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  {
                                    "title": "Unknown type",
                                    "properties": {
                                      "type": {
                                        "type": "string",
                                        "pattern": "^unknown$"
                                      }
                                    }
                                  }
                                ]
                              }
                            ]
                          }
                        }
                      },
                      "required": ["fields"]
                    },
                    {
                      "title": "Unknown type",
                      "properties": {
                        "type": {
                          "type": "string",
                          "pattern": "^unknown$"
                        }
                      }
                    }
                  ]
                }
              ]
            }
          }
        }
      },
      "required": ["fields"]
    }
  },
  "required": ["sections"]
}
```

You can test your own Form Config Schema at [JSON Schema Validator](https://www.jsonschemavalidator.net/s/tEIvqp1J)
