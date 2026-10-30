# Steam Genre Classification with In-Context Learning

Code relating to the seminar paper *"Classifying Steam Game Genres with In-Context Learning: An Ablation Study of ICL Technique and Description Scope"*.

## Notebooks

| Notebook | Purpose |
|---|---|
| `data_preprocessing.ipynb` | Preprocessing pipeline: Cleans and filters the Kaggle dataset, adds leakage flags, and creates the train/val/test splits in `data/`. |
| `ablation_study.ipynb` | Acutal experiment: Runs the model calls (zero-shot, few-shot random, few-shot kNN), evaluates each technique, and performs the joint evaluation. |

## Setup

```
pip install -r requirements.txt
```

Additionally required (not included):

- `data/games_march2025_cleaned.csv` from the Kaggle dataset [Steam Games Dataset 2025](https://www.kaggle.com/datasets/artermiloff/steam-games-dataset)
- `lid.176.bin` (fastText language identification model) in the project root, only for pre-processing
- `.env` in the project root with `KICONNECT_API_KEY=...` ([KI:connect.nrw](https://kiconnect.pages.rwth-aachen.de))

## Usage

1. Run `data_preprocessing.ipynb` once.
2. In `ablation_study.ipynb`, set `TECHNIQUE` (`zero_shot` | `few_shot_random` | `few_shot_knn`) and `RUN` (`pilot` | `main`), then run all cells. Repeat for each technique.
3. The section "Joint evaluation" at the end is independent of `TECHNIQUE` and `RUN` and writes the final results to `results/joint/`.

Raw model outputs (`results/raw/`), embeddings (`results/embeddings/`), and the zero-shot pilot outputs (`pilot_*.jsonl`) are cached. If they exist, the notebook only loads them and makes no API calls ("… done, 0 to go"). Delete a file to re-query the model; since outputs are not fully deterministic, results may then differ slightly.

## Outputs

- `results/joint/`: final results reported in the paper (`paper_table_main.csv`, `paper_table_differences.csv`)
- `results/{technique}_{run}/`: preliminary per-technique evaluation (B = 2,000, uncorrected)

## License

The code in this repository is licensed under the MIT License (see `LICENSE`).
The data in `data/` is derived from the [Steam Games Dataset 2025](https://www.kaggle.com/datasets/artermiloff/steam-games-dataset) by Artem Ermilov and is distributed under the MIT License (see `data/LICENSE`).