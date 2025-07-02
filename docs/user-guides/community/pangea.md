# Pangea AI Guard integration

Pangea's [AI Guard](https://pangea.cloud/services/ai-guard/) service is a robust security solution that protects data
and interactions with LLMs within AI-powered applications. It ensures sensitive information such as secrets and
personally identifiable information (PII) is safeguarded, blocks malicious content, and captures application events in
an audit trail.

The following environment variable is required to use the Pangea AI Guard integration:

- `PANGEA_API_TOKEN`: Pangea API token with access to the AI Guard service.

There is also an optional environment variable:

- `PANGEA_BASE_URL_TEMPLATE`: Template for constructing the base URL for API requests. The placeholder `{SERVICE_NAME}`
  will be replaced with the service name slug. Defaults to `https://{SERVICE_NAME}.aws.us.pangea.cloud`.

## Setup

Colang v1:

```yaml
# config.yml

rails:
  config:
    pangea:
      input:
        recipe: pangea_prompt_guard
      output:
        recipe: pangea_llm_response_guard

  input:
    flows:
      - pangea ai guard input

  output:
    flows:
      - pangea ai guard output
```

Colang v2:

```yaml
# config.yml

colang_version: "2.x"

rails:
  config:
    pangea:
      input:
        recipe: pangea_prompt_guard
      output:
        recipe: pangea_llm_response_guard
```

```
# rails.co

import guardrails
import nemoguardrails.library.pangea

flow input rails $input_text
    pangea ai guard input

flow output rails $output_text
    pangea ai guard output
```
