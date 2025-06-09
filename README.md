# BAREC Shared Task 2025: Arabic Readability Assessment

The BAREC Shared Task 2025 will take place at The Third Arabic Natural Language Processing Conference (ArabicNLP 2025) at EMNLP 2025.

***Click here to [register for the shared task](https://docs.google.com/forms/d/e/1FAIpQLSeSEHn3iPTQ2HCZ-t3DLGpJ5HjMld7xNFmGu87SOQ2ccywBKg/viewform)!***

## Task Description

The BAREC Shared Task 2025 focuses on fine-grained readability classification across 19 levels using the Balanced Arabic Readability Evaluation Corpus (BAREC), a dataset of over 1 million words. Participants will build models for both sentence- and document-level classification.

## Data

- **[The BAREC Corpus](https://huggingface.co/datasets/CAMeL-Lab/BAREC-Shared-Task-2025):** The BAREC Corpus ([Elmadani et al., 2025](https://arxiv.org/abs/2502.13520)) cconsists of 1,922 documents and 69,441 sentences classified into 19 readability levels. 

- **[The SAMER Corpus](https://camel.abudhabi.nyu.edu/samer-simplification-corpus/):** The SAMER Corpus ([Alhafni et al., 2024](https://aclanthology.org/2024.lrec-main.1398/)) consists of 4,289 documents and 20,358 fragments classified into three readability levels.

- **[The SAMER Lexicon](https://camel.abudhabi.nyu.edu/samer-readability-lexicon/):** The SAMER Lexicon ([Al Khalil et al., 2020](https://aclanthology.org/2020.lrec-1.373/)) is a 40K-lemma leveled readability lexicon. The lexicon consists of 40K lemma and part-of-speech pairs annotated into five readability levels.

## Shared Task Tracks

Participants can compete in one or more of the following tracks, each imposing different resource constraints:

- **Strict Track:** Models must be trained *exclusively* on the BAREC Corpus.
  - Sentence-level Readability Assessment: [CodaBench Link](https://www.codabench.org/competitions/9025/)
  - Document-level Readability Assessment: [CodaBench Link](https://www.codabench.org/competitions/9028/)

- **Constrained Track:** Models may use the BAREC Corpus, SAMER Corpus (including document, fragment, and word-level annotations), and the SAMER Lexicon.
  - Sentence-level Readability Assessment: [CodaBench Link](https://www.codabench.org/competitions/9026/)
  - Document-level Readability Assessment: [CodaBench Link](https://www.codabench.org/competitions/9029/)

- **Open Track:** No restrictions on external resources, allowing the use of any publicly available data.
  - Sentence-level Readability Assessment: [CodaBench Link](https://www.codabench.org/competitions/9027/)
  - Document-level Readability Assessment: [CodaBench Link](https://www.codabench.org/competitions/9030/)
  

With two sub-tasks and three tracks, the task results in a total of **six possible combinations**. Participants are allowed to compete in multiple sub-tasks and tracks.


## Evaluation

We define the Readability Assessment task as an ordinal classification task. The following metrics are used for evaluation:

- **Accuracy (Acc<sup>19</sup>):** The percentage of cases where reference and prediction classes match in the 19-level scheme.
- **Accuracy (Acc<sup>7</sup>, Acc<sup>5</sup>, Acc<sup>3</sup>):** The percentage of cases where reference and prediction classes match after collapsing the 19 levels into 7, 5, or 3 levels, respectively.
- **Adjacent Accuracy (±1 Acc<sup>19</sup>):** Also known as off-by-1 accuracy. The proportion of predictions that are either exactly correct or off by at most one level in the 19-level scheme.
- **Average Distance (Dist):** Also known as Mean Absolute Error (MAE). Measures the average absolute difference between predicted and true labels.
- **Quadratic Weighted Kappa (QWK):** An extension of Cohen’s Kappa that measures the agreement between predicted and true labels, applying a quadratic penalty to larger misclassifications (i.e., predictions farther from the true label are penalized more heavily).

We provide instructions on how to run the evaluation script below.

### Requirements:

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
  - `Prediction`: Your predicted readability level for each sentence (integer from 1 to 19).

- For document-level tasks (`--task Doc`):
  - `Document ID`: The unique identifier for each document.
  - `Prediction`: Your predicted readability level for each document (integer from 1 to 19).

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

### Example Output

After running the evaluation script, you will see output similar to the following in your terminal:

```
Evaluating Sentence-level readability on Dev split using examples/Dev_Sentence_Level.csv
Accuracy: 56.6211%
Accuracy +/-1: 69.8632%
Average absolute distance: 1.143776
Quadratic Cohen's Kappa: 80.0040%
Accuracy (7 levels): 65.8687%
Accuracy (5 levels): 70.2736%
Accuracy (3 levels): 76.4569%
Evaluation completed successfully.
```

Each metric reflects the performance of your predictions on the selected split and task.


## Organizers

[Khalid Elmadani](https://nyuad.nyu.edu/en/research/faculty-labs-and-projects/computational-approaches-to-modeling-language-lab/researchers/khalid-ahmed.html)

[Bashar Alhafni](https://www.basharalhafni.com/)

[Hanada Taha-Thomure](https://hanadataha.com/)

[Nizar Habash](https://www.nizarhabash.com/)


## License

This repo is available under the MIT license. See the [LICENSE](LICENSE) for more info.

## References

1. [A Large and Balanced Corpus for Fine-grained Arabic Readability Assessment](https://arxiv.org/abs/2502.13520). Khalid N. Elmadani, Nizar Habash, and Hanada Taha-Thomure. 2025. In Findings of the Association for Computational Linguistics: ACL 2025, Vienna, Austria.

2. [Guidelines for fine-grained sentence-level Arabic readability annotation](https://arxiv.org/abs/2410.08674). Nizar Habash, Hanada Taha-Thomure, Khalid N. Elmadani, Zeina Zeino, and Abdallah Abushmaes. 2025. In Proceedings of the 19th Linguistic Annotation Workshop (LAW-XIX), Vienna, Austria.

3. [The SAMER Arabic Text Simplification Corpus](https://aclanthology.org/2024.lrec-main.1398.pdf). Bashar Alhafni, Reem Hazim, Juan David Pineros Liberato, Muhamed Al Khalil, Nizar Habash. 2024. In Proceedings of the 2024 Joint International Conference on Computational Linguistics, Language Resources and Evaluation (LREC-COLING 2024). 
