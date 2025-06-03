# BAREC Shared Task 2025: Arabic Readability Assessment

The BAREC Shared Task 2025 will take place at The Third Arabic Natural Language Processing Conference (ArabicNLP 2025) at EMNLP 2025.

## Task Description:

## Data:

## Evaluation:

## Requirements:

You will need to have [conda](https://docs.conda.io/en/latest/miniconda.html) installed. To setup the environment, you would need to run:

```bash
git clone https://github.com/CAMeL-Lab/barec-shared-task-2025.git
cd barec-shared-task-2025

conda create -n barec python=3.9

conda activate barec

pip install -r requirements.txt
```

### Running the Evaluation

To evaluate your predictions, use the provided evaluation script. The script requires three arguments:

- `--output`: Path to your output CSV file containing predictions.
- `--split`: The data split to evaluate on (`Dev` or `Test`).
- `--task`: The task type (`Sent` for sentence-level or `Doc` for document-level readability).

To evaluate your system's output, you would need to run:

```bash
python scripts/eval.py --output /path/to/output_csv --split [Dev|Test] --task [Sent|Doc]
```

Example usage:

```bash
python scripts/eval.py --output examples/Dev_Sentence_Level.csv --split Dev --task Sent
```

### Output CSV Format

Your output CSV file should have the following columns:

- For sentence-level tasks (`--task Sent`):
  - `Sentence ID`: The unique identifier for each sentence.
  - `Prediction`: Your predicted readability level for each sentence (integer between 1 and 19).

- For document-level tasks (`--task Doc`):
  - `Document ID`: The unique identifier for each document.
  - `Prediction`: Your predicted readability level for each document (integer between 1 and 19).

**Example (Sentence-level):**

| Sentence ID | Prediction |
|-------------|------------|
| 1001        | 7          |
| 1002        | 12         |
| ...         | ...        |

**Example (Document-level):**

| Document ID | Prediction |
|-------------|------------|
| 2001        | 5          |
| 2002        | 14         |
| ...         | ...        |

Make sure the IDs in your output file match exactly those in the provided split (Dev or Test) for the chosen task.


## Organizers:

[Khalid Elmadani](https://nyuad.nyu.edu/en/research/faculty-labs-and-projects/computational-approaches-to-modeling-language-lab/researchers/khalid-ahmed.html)

[Bashar Alhafni](https://www.basharalhafni.com/)

[Hanada Taha-Thomure](https://hanadataha.com/)

[Nizar Habash](https://www.nizarhabash.com/)


## License:

This repo is available under the MIT license. See the [LICENSE](LICENSE) for more info.

## References:
