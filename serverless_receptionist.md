## Signalwire AI Serverless Receptionist

In the realm of artificial intelligence and conversational systems, configuring virtual assistants to handle tasks and interactions is crucial. In this article, we'll dive into a JSON configuration snippet that outlines the behavior of the Signalwire AI Serverless Receptionist for customer support. Let's break down each component step by step.
Version and Sections

```
{
  "version": "1.0.0",
  "sections": {
    "main": [
      {
        // AI configuration details will go here
      }
    ]
  }
}

```

The configuration starts with a version identifier and a nested structure named "sections." Inside "sections," we have a main section where our AI configurations will reside.

## AI Configuration

```
{
  "ai": {
    "post_prompt_url": "https://webhook.site/1c67cc27-311e-4dff-a50a-435cb887f304",
    "params": {
      // Parameters for AI behavior
    },
    "prompt": {
      // Initial greeting and behavior instructions for the assistant
    },
    "SWAIG": {
      // AI functions and settings related to call handling
    },
    "post_prompt": {
      // Behavior after the conversation ends
    },
    "languages": [
      // Supported languages for the assistant
    ]
  }
}

```

## The AI section contains various settings and instructions for the virtual assistant's behavior. Here's a breakdown of the components:

-    post_prompt_url: A URL where the assistant can send data after prompts.
-    params: Parameters influencing AI behavior, such as debug settings and time zone.
-    prompt: Instructions for the initial greeting and behavior of the assistant, including confidence levels and response characteristics.
-    SWAIG: This section defines functions and settings related to call handling. Specifically, it includes a transfer function and associated data mappings.
-    post_prompt: Instructions for behavior after the conversation ends.
-    languages: List of supported languages along with their voice settings.

## AI Functions: Transfer Function

```

"functions": [
  {
    "meta_data": {
      // Target phone numbers for transfer
    },
    "function": "transfer",
    "data_map": {
      // Expressions for call transfer
    },
    "argument": {
      // Definition of the 'target' argument
    },
    "purpose": "use to transfer to a target"
  }
]

```

## Within the SWAIG section, we define a function for transferring calls. This function includes:

-    meta_data: A metadata section containing target phone numbers for transfer.
-    function: Specifies that this is a transfer function.
-    data_map: Expressions to control the transfer process based on conditions.
-    argument: Definition of the 'target' argument that specifies the transfer destination.
-    purpose: Describes the purpose of the function.

## Supported Languages

```

"languages": [
  {
    "code": "en-US",
    "voice": "gcloud.en-US-Standard-A",
    "name": "English (US)"
  },
  {
    "code": "es-US",
    "voice": "gcloud.es-US-Standard-B",
    "name": "Spanish (US)"
  }
]

```

The assistant supports multiple languages, each with a language code, voice setting, and name.
Conclusion

Configuring virtual assistants involves defining various aspects of their behavior, such as prompts, functions, and supported languages. This JSON configuration snippet offers insights into how a customer support virtual assistant can be configured to handle calls and interactions effectively.

## Full Example

```

{
  "version": "1.0.0",
  "sections": {
    "main": [
      {
        "ai": {
          "post_prompt_url": "https://webhook.site/1c67cc27-311e-4dff-a50a-435cb887f304",
          "params": {
            "debug_webhook_url": "https://webhook.site/1c67cc27-311e-4dff-a50a-435cb887f304",
            "debug_webhook_level": "true",
            "local_tz": "America/Chicago"
          },
          "prompt": {
            "text": "Your name is John and you are a Customer Support virtual assistant. Begin by greeting the caller. You can transfer to jim if asked.",
            "confidence": 0.1,
            "top_p": 0.1,
            "temperature": 0.1
          },
          "SWAIG": {
            "functions": [
              {
                "meta_data": {
                  "target_table": {
                    "jim": "+17247231200",
                    "abc": "+12345678910"
                  }
                },
                "function": "transfer",
                "data_map": {
                  "expressions": [
                    {
                      "output": {
                        "action": [
                          {
                            "say": "Please stand by while I connect your call."
                          },
                          {
                            "SWML": {
                              "version": "1.0.0",
                              "sections": {
                                "main": [
                                  {
                                    "connect": {
                                      "to": "${meta_data.target_table.${lc:args.target}}"
                                    }
                                  }
                                ]
                              }
                            }
                          },
                          {
                            "stop": "true"
                          }
                        ],
                        "response": "transferred, the call has ended."
                      },
                      "pattern": "\\w+",
                      "string": "${meta_data.target_table.${lc:args.target}}"
                    },
                    {
                      "pattern": ".*",
                      "string": "${args.target}",
                      "output": {
                        "response": "I'm sorry, I was unable to transfer your call to ${input.args.target}."
                      }
                    }
                  ]
                },
                "argument": {
                  "type": "object",
                  "properties": {
                    "target": {
                      "description": "the target to transfer to",
                      "type": "string"
                    }
                  }
                },
                "purpose": "use to transfer to a target"
              }
            ],
            "post_prompt": {
              "text": "Summarize conversation in json",
              "top_p": 0,
              "temperature": 0
            },
            "languages": [
              {
                "code": "en-US",
                "voice": "gcloud.en-US-Standard-A",
                "name": "English (US)"
              },
              {
                "code": "es-US",
                "voice": "gcloud.es-US-Standard-B",
                "name": "Spanish (US)"
              }
            ]
          }
        }
      }
    ]
  }
}

```
