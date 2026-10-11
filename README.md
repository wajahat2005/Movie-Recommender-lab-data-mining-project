# MovieLens Movie Recommender – Data Mining Project

## Project question

Which recommendation approach gives the most useful movie recommendations on
the MovieLens dataset?

We compare three families of recommenders:

1. **Content-based filtering** – recommends movies similar to ones a user liked,
   using movie features (genres, tags).
2. **Collaborative filtering** – learns from the ratings of many users:
   - user/item **k-Nearest Neighbours (kNN)**
   - matrix factorisation with **SVD**
3. **Association rules** – mines "users who liked X also liked Y" rules
   (Apriori / FP-Growth).

The approaches are evaluated on the same train/test split using rating-error
and ranking metrics.

## Dataset and citation

We use the **MovieLens** dataset collected by GroupLens Research at the
University of Minnesota: <https://grouplens.org/datasets/movielens/>

> F. Maxwell Harper and Joseph A. Konstan. 2015. The MovieLens Datasets:
> History and Context. *ACM Transactions on Interactive Intelligent Systems
> (TiiS)* 5, 4, Article 19 (December 2015), 19 pages.
> <https://doi.org/10.1145/2827872>

**License:** The dataset is provided by GroupLens under its own usage license
(research/education use, no redistribution, must cite the paper above). See the
README included in the dataset download for the full terms. For this reason
the data is **not** included in this repository – it is downloaded at runtime
into `data/`, which is git-ignored.

## Repository structure

```
notebooks/     Colab notebooks (EDA, recommenders, evaluation)
src/           Reusable Python helper code
app/           Streamlit demo app
reports/       Final report, figures, slides
requirements.txt
```

## How to run in Google Colab

1. Open [Google Colab](https://colab.research.google.com/) and choose
   **File → Open notebook → GitHub**, then paste
   `https://github.com/wajahat2005/Movie-Recommender-lab-data-mining-project`
   and pick a notebook from `notebooks/`.
2. Keep the default **CPU** runtime (no GPU is needed).
3. Run the first cells, which clone the repo, install dependencies and download
   the dataset:
   ```python
   !git clone https://github.com/wajahat2005/Movie-Recommender-lab-data-mining-project.git
   %cd Movie-Recommender-lab-data-mining-project
   !pip install -q -r requirements.txt
   ```
4. Run the remaining cells top to bottom. All randomness uses seed `42`, so
   results are reproducible.

## How to use `src/data.py`

After `%cd` into the repo (step 3 above), load the data in any notebook with:

```python
from src.data import load_data, load_ml32m_sample

# MovieLens "latest-small" (~100k ratings) – our main dataset.
# Downloads into data/ the first time, then reuses the local copy.
data = load_data()
ratings = data["ratings"]   # userId, movieId, rating, timestamp (datetime)
movies  = data["movies"]    # movieId, title, genres (list, e.g. ["Comedy", "Romance"])
tags    = data["tags"]      # userId, movieId, tag, timestamp (datetime)
links   = data["links"]     # movieId, imdbId, tmdbId

# Optional: a bigger dataset – 5% of the users of MovieLens 32M with ALL of
# their ratings (~1.6M ratings). First call downloads a ~240 MB zip.
big = load_ml32m_sample(frac=0.05)   # same keys as load_data()
```

Movies with no genres get an empty list `[]`. User sampling is fixed with
seed `42`, so every teammate gets the same users.

## How to run the app

Locally (Python 3.10+):

```bash
pip install -r requirements.txt
streamlit run app/app.py
```

Then open the URL Streamlit prints (usually <http://localhost:8501>).

## Contribution log

| Member | Student ID | Main responsibilities | Contribution summary |
|--------|------------|-----------------------|----------------------|
| M wajahat | 520355 | data lead |  |
| Member 2 |  |  |  |
| Member 3 |  |  |  |
