# Bili Up Finder: LLM + Playwright

[中文版本](README.md) | English

## Project Overview

Bili Up Finder is based on LLM + Playwright, designed to help users search for Bilibili content creators (Up主) based on keywords. It provides features such as keyword expansion, relevance judgment, and using an AI assistant to generate reports.

## Configuration Instructions

1. Ensure Python 3.12 or higher is installed.

2. Install [uv](https://docs.astral.sh/uv/getting-started/installation/).

3. Configure the API key for OpenAI/DeepSeek (DeepSeek recommended) in the environment variables or `.env` file:

   ```bash
   export OPENAI_API_KEY="your_api_key_here"
   export DEEPSEEK_API_KEY="your_api_key_here"
   ```

## Usage Example

Generate a search query report:

```bash
   uv run -m bili_up_finder -q "Photography" -n 10  
```

The generated report will be saved in the `reports` directory.

## Project Workflow

```mermaid
flowchart TD
  A[Define target audience to follow<br/>e.g., Travel Vlog + desired number of creators] --> B[AI expands search keywords]
  B --> C((Search))
  C --> D[Videos]
  D --> E[Select sorting<br/>Comprehensive / Most views / Most danmaku / Most likes / Most favorites]
  E --> F[Open each video]
  F --> G[Check title + tags]

  G -- Yes --> H[Go to creator homepage]
  H --> I[Open uploads]
  I --> J[Review many upload titles to confirm they match the search topic]

  J -- Yes --> K{Total uploads > threshold?}
  J -- No --> F

  K -- Yes --> L[Record creator name<br/>Download avatar<br/>Save profile URL]
  K -- No --> F

  L --> M[Add name to list to avoid duplicate follows]
  M --> N{Reached desired number of creators?}

  N -- Yes --> O[Generate report]
  N -- No --> F

  G -- No --> F
```

<div style="color: red;">
NB: This workflow is intended as a reference example of integrating LLM with Playwright, demonstrating the basic process and implementation approach. The current implementation focuses on functionality demonstration without extensive optimization for accuracy or performance. Future improvements can be made to prompt design, data processing logic, and execution strategies to enhance the accuracy and stability of the final output.
</div>


## TO-DO

- [ ] Support incremental search.
- [ ] Add local caching. If the search keyword is similar and the quantity is less than the cached amount, return results directly.

## License

This project is licensed under the MIT License.
