# Who Should I Vote For? Partisan Bias in AI Voting Advice for German Election
This project asks whether large language models exhibit systematic partisan bias when advising
voters in Germany. With AI chatbots increasingly serving as intermediaries for political
information, we evaluate how four models from North America, Europe and China recommend
parties given varied demographic attributes and policy stances, in the context of the upcoming
German federal (2029) and Berlin state (2026) elections.

To do this, we ask Gemini 3.1 Flash Lite, Mistral Large 3, Qwen Flash, and Grok 4.20
(Non-Reasoning) to recommend a party to thousands of synthetic voter profiles that vary
demographics, geography and policy stance. Everything behind that is collected here: the
prompts, the raw model responses, the coded citation data, and the notebooks that produced the
figures and regressions. Full design, results and discussion are in the final paper.

## Repository structure

```
├── Data/
│   ├── BTW/                         # 2029 federal election (Bundestagswahl)
│   │   ├── Day1/                    # Raw model responses, batch of 2026-06-26
│   │   ├── Day2/                    # Raw model responses, batch of 2026-07-05
│   │   ├── Day3/                    # Raw model responses, batch of 2026-07-31
│   │   ├── Prompt_Setup/            # Profile grid and policy stance definitions
│   │   ├── Web_Search/              # Grok citation excursus (raw responses + coded sources)
│   │   └── batch_requests_{gemini,grok,mistral,qwen}.json
│   └── LTW_B/                       # 2026 Berlin state election (Landtagswahl Berlin)
│       ├── Day1/                    # Raw model responses, single batch of 2026-07-08
│       ├── Prompt_Setup/            # Profile grid and policy stance definitions
│       └── batch_requests_{gemini,grok,mistral,qwen}.json
├── Notebooks/
│   ├── 01_Data_Collection.ipynb     # Prompt construction, batch submission, retrieval
│   └── 02_Data_Analysis.ipynb       # Cleaning, entropy/overlap, OLS regressions, figures
├── Final_paper.pdf                  # Final paper
├── Presentation_final_15_July.pdf   # Final presentation
├── requirements.txt
└── README.md
```

## Reading the data

- `batch_requests_*.json` are the exact payloads sent to each provider's Batch API. The full
  prompt text for every profile is recoverable from them.
- `Day*/` holds the returned responses, one file per model, before any cleaning. The federal
  design was collected three times to allow date fixed effects; Berlin once, for cost reasons.
- Recommendations are extracted from the **first line** of each response. Refusals and
  ambiguous answers are coded as `Refusal` and treated as a category alongside the nine parties.
- All prompts were run with web search disabled and a 200-token cap, except the Grok citation
  excursus in `BTW/Web_Search/`, which was run with search enabled.

## Setup

```bash
pip install -r requirements.txt
```

Collection additionally requires API keys for all four providers.

## Reproducing

Run `Notebooks/02_Data_Analysis.ipynb` to regenerate every figure and regression table from the
data in this repository. No API keys needed.

`Notebooks/01_Data_Collection.ipynb` re-collects from the providers. This costs money and will
not reproduce the numbers in the paper. Two of the four models changed measurably within our
five-week collection window, so any new batch is a fresh snapshot rather than a replication.
