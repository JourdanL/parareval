# ParaReval dataset from : Identifying Reliable Evaluation Metrics for Scientific Text Revision

This repository contains the ParaReval dataset, a dataset of human pairwise evaluations of generated revisions.
The data used to generate the revisions are the [test set of the ParaRev corpus](https://huggingface.co/datasets/taln-ls2n/pararev).

### Data generation
For each datapoint in the dataset (258 revised paragraph* 2 annotated instructions = 516 datapoint), we generated 6 revised versions
using 6 different LLMs. We used: [CoEdIT-XL](https://huggingface.co/grammarly/coedit-xl), [Llama 3 8B Instruct](https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct),
[Llama 3 70B Instruct](https://huggingface.co/meta-llama/Meta-Llama-3-70B-Instruct), [Mistral 7B Instruct v0.2](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2), GPT 4o mini and GPT 4o

### Annotation

Given the original paragraph, the revision instruction and 2 generated revisions, annotators add to answer the following questions:
- **Q1A and Q1B Relatedness** x2: *Did model A/B address the instruction? {Yes strictly, Yes with additional modifications, No}*
- **Q2 Correctness**: *If it was your article and your instruction, which revisions would you consider acceptable? {Both, A only, B only, None}*
- **Q3 Preference**:  *If it was your article and your instruction, which revision would you prefer to include in your paper? {Both, A, B,None}*

Category-Specific Evaluation, *{Both, A, B, None}* are possible answers for each question:
- **Rewriting light**: *Which model improves the academic style and English the most?*
- **Rewriting medium**: *Which model improves the readability and structure the most?*
- **Rewriting heavy**: *Which model improves the readability and clarity the most?*
- **Concision**: *Which model manages the most to give a shorter version while keeping all the important ideas?*

  ### Data structure
The data are provided as a .jsonl file where one line correspond to one annotation

A datapoint is structured as follows:
- **"annotator"**: str, <annotator identifier\>
- **"id_paragraph"**: str, <paragraph identifier\>
- **"id_pairing"**: int, <unique datapoint identifier\>
- **"pararev_annot"**: str, "annot_1" or "annot_2", to align with ParaRev data
- **"model_A"**: str, <name of model used for revision A\>
- **"model_B"**: str, <name of model used for revision B\>
- **"original_paragraph"**: str, <full text of the paragraph original version\>
- **"reference_paragraph"**: str, <full text of the gold revision of the paragraph (by authors)\>
- **"model_A_paragraph"**: str, <full text of the revision proposed by model A\>
- **"model_B_paragraph"**: str, <full text of the revision proposed by model B\>
- **"labels"**: list of str, <revision intention label from ParaRev\>
- **"instruction"**: str, <revision intention instruction from ParaRev\>
- **"eval_annotation"**: dict
  - **"relatedness_A"**: str, <answer to Q1A\>
  - **"relatedness_B"**: str, <answer to Q1B\>
  - **"acceptable"**: str, <answer to Q2\>
  - **"correctness_A"**: Bool, <duplicate of acceptable but binary only for A\>
  - **"correctness_B"**: Bool, <duplicate of acceptable but binary only for B\>
  - **"preference"**: str, <answer to Q3\>
  - **"extended_choice"**: str, <see paper for definition, combination of Q1 to Q3 in case of Tie\>
  - ("Rewriting_light", "Rewriting medium", "Rewriting heavy", "Concision"): str, <answer to category-specific questions\>
 
### Citation

You can find the paper associated to this repository on [arXiv](https://arxiv.org/abs/2506.04772) or [HAL](https://hal.science/hal-05099650)


The paper will be published in august 2025 in the proceedings of ACL 2025.

For now, please cite it as:

	@misc{jourdan2025identifyingreliableevaluationmetrics,
  	title={Identifying Reliable Evaluation Metrics for Scientific Text Revision},
  	author={Léane Jourdan and Florian Boudin and Richard Dufour and Nicolas Hernandez},
  	year={2025},
  	eprint={2506.04772},
  	archivePrefix={arXiv},
  	primaryClass={cs.CL},
  	url={https://arxiv.org/abs/2506.04772} }
