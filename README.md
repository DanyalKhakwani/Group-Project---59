## Group Project - 59

---

## Research Question

> Do pull requests (PR) topic patterns and contribution network differ in popular data science libraries (pandas) and newer projects (Modin), and do these differences reflect meaningful variation in community sustainability?

---

## Project Structure
```
project/
│
├── prs_pandas.csv            ← 1000 PRs from pandas-dev/pandas
├── prs_reviews_pandas.csv        ← Reviews for first 300 PRs (network edges)
├── prs_modin.csv             ← 1000 PRs from modin-project/modin
├── prs_reviews_modin.csv         ← Reviews for first 300 PRs (network edges)
│
├── Data Collection.ipynb  ← API calls 
└── README.md
```
---

## Repos Under Study

| Repo | Role | PRs collected |
|---|---|---|
| `pandas-dev/pandas` | Mature, widely-adopted baseline | 1000 |
| `modin-project/modin` | Smaller, newer comparison repo | 1000 |

---

## Data Collected

### Dataset 1 — PR Metadata (`*_prs.csv`)
1000 PRs per repo. Used for **topic modelling**.

| Column | Description |
|---|---|
| `pr_id` | PR number |
| `pr_title` | Title of the PR |
| `pr_author` | GitHub username who opened the PR |
| `state` | closed / merged |
| `created_at` | When the PR was opened |
| `merged_at` | When the PR was merged (null if not merged) |
| `body` | PR description text — primary NLP input | This is the variable used for topic modelling

### Dataset 2 — PR Reviews (`*_reviews.csv`)
Reviews for the first 300 PRs per repo. Used for **network analysis**.

| Column | Description |
|---|---|
| `pr_id` | PR number (joins to Dataset 1) |
| `pr_author` | GitHub username who opened the PR |
| `reviewed_by` | GitHub username who reviewed the PR |
| `review_state` | APPROVED / CHANGES_REQUESTED / COMMENTED |
| `review_text` | Text of the review (may be empty) |
| `reviewed_at` | Timestamp of the review |

---


### GitHub Token
You need a personal access token to run the data collection notebook.

1. Go to github.com → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate a new token with `public_repo` scope
3. Set expiry to 90 days
4. Paste it into the `GITHUB_TOKEN` variable at the top of `01_data_collection.ipynb`

> **Important:** Never commit your token to the repository. The collection notebook is already in `.gitignore` — do not move it out.

### `.gitignore`
Make sure your `.gitignore` includes:
```
01_data_collection.ipynb
*.token
.env
```


