# medium_X_analysis 
Hello, this is my jupyter notebook counterpart for my '2 Ways of Analyzing Geographic Culture Through X API v2 + British LLM?' article on Medium.com. Link --> https://medium.com/@adelnsahuc/analyzing-geographic-culture-through-x-api-v2-british-llm-53d26f832876?postPublishedType=repub

### steps 1.x are done in notebooks/x_api_culture_pipeline.ipynb

### steps 2.x are done in notebooks/x_api_culture_analysis.ipynb

Feel free to report issues. Notice that the findings should not be considered a complete analysis of these regions cultures as a set of peope from X do not represent the full cultural identity of any region, but it does give us some insights. 


##  Files and Schemas

**Config Files** (`configs/*.json`)
- Region settings: bio keywords, output paths, API limits
- Example: `uk.json`, `nyc.json`, `sg.json`

**Local Seeds** (`data/local_seeds/*.json`)
- Categorized seed accounts (sports, music, tech_lifestyle, comedy)
- Used as starting points to find regional users

**Users** (`data/users/*.jsonl`)
- User objects: `id`, `username`, `name`, `description`, `location`, `public_metrics`
- Filtered by bio keywords to confirm regional association

**Tweets** (`data/tweets/*.jsonl`)
- Tweet objects: `id`, `text`, `author_id`, `created_at`, `public_metrics`
- Collected from confirmed local users

**Adjacent Users** (`data/users_adjacent/*.jsonl`)
- Users found via mentions of seed accounts
- Same structure as users, before bio filtering

## Architecture

1. **Data Collection** (Pipeline Notebook)
   - Load region config and seed accounts
   - Resolve seeds via X API `/2/users/by`
   - Find adjacent users via `/2/tweets/search/recent` (mentions)
   - Filter adjacent users by bio keywords → confirmed locals
   - Collect tweets from confirmed locals via `/2/users/:id/tweets`

2. **Data Analysis** (Analysis Notebook)
   - Load pre-collected tweets for NYC, SG, UK
   - Sentiment analysis with NLTK VADER
   - Topic profiling with Empath dictionary
   - Dimensionality reduction with PCA/UMAP
   - Compare regional "cultural profiles" in topic space
