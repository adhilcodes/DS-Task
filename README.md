# Technical Task for Data Scientist

Thank you for applying for a position with SAP. We would like to assess your technical skills further by working on two simple problems.


## Introduction

The purpose of this task is to assess the following:

- **Python proficiency**: ability to write good-quaility code
- **Machine learning knowledge**: ability to apply the appropriate feature engineering and modelling algorithms.
- **Learning aptitude**: ability to learn on the job

There are 2 parts to the task:

- **Part 1**: data preparation based on requirements
- **Part 2**: machine learning task

You will need the following:

- [Jupyter](https://jupyter.org/)
- [Python 3](https://www.python.org/)

Please use [pandas](https://pandas.pydata.org/) to load the data.
For accomplishing the tasks, you are free to choose which Python libraries you want to use.

## Instructions

1. Write your code, documentation and/or plots in a [jupyter notebook(s)](https://jupyter.org/)
2. Save your notebooks and output files (if any) in the `submit/` folder
3. When you are done, zip the whole project
4. Send us back the zip file in an email
5. If you are not sure of any of the intructions, please exercise your own judgement, note it down, and proceed accordingly

## Part 1 (data preparation)

Your team is working on a contract related project. Your colleagues want to train text classification models with contract text data, and they need your help to prepare data for the task. This task is about **filtering relevant contracts** and **merging them with labels**.

In `data/`, you are given 2 compressed pandas dataframes, `df_cases_200906.gzip` and `df_label_200906.gzip`.

About `df_cases_200906.gzip`:

- Each row represents a unique contract
- Schema:

     ```
      CaseId          A unique ID given to group of contracts
      FileName        File name of contract
      Language        Language of contract
      StartDate       Start date of contract's creation date
      DocumentType    Type of contract
      IsExecuted      Boolean describing the execution status of contract
      OcrText         OCR result of contract pdf
      QualityScore    A numeric float (0 to 1), to access the quality of text from OCR conversion
     ```

About `df_label_200906.gzip`

- Each row represents a unique Case ID
- Schema:

     ```
      CaseId     A unique ID given to group of contracts
      label_1    boolean (description of label is not needed for test)
      label_2    boolean (description of label is not needed for test)
     ```

---

#### Requirements

The main objective is to merge `label_1` and `label_2` into `df_cases_200906.gzip`, so that the team can train text classification models using data from the `OcrText` field

A `CaseId` can contain either one contract, or a group of contracts. However, each `CaseId` is given only 1 set of labels. Therefore, for each `CaseId`, you have to **concatentate** all `OcrText` fields of all **VALID** contracts.

Contracts are consider **INVALID** if any of the below conditions apply.

- `IsExecuted==False`
- `QualityScore<0.81`

The final prepared dataset should contain the following columns:

   ```
    CaseId          	A unique ID given to group of contracts
    ValidFileNames  	List of all valid file names
    InvalidFileNames	List of all invalid file names
    OcrText         	OCR result of contract pdf
    label_1    			boolean (description of label is not needed for test)
    label_2    			boolean (description of label is not needed for test)
   ```

Please export the final prepared dataset as `submit/df_final.gzip`.

Example of final prepared dataset:

- ![df_final_example](./misc/df_final_eg.png)

#### Notes

- You are required to code in a [Jupyter Notebook](https://jupyter.org/), using Python **3**
- Use this command to read gzip using [pandas](https://pandas.pydata.org/): `df = pd.read_pickle('df_cases_200906.gzip')`
- Save the following files into the `submit/` folder:
  - One Jupyter notebook, detailing the data preparation code
  - Final prepared dataset, `df_final.gzip`
- Please make your notebook clean and readable, your code should run top to bottom without any errors
- Please add runtime calculation and validate your output
- The following will be evaluated:
  - Code correctness
  - Readibility
  - Runtime
  - Validation

## Part 2

Your submission in this section is **NOT** to train the best model. It is to **help us assess your ability to learn and apply NLP modelling techniques.**

#### Instructions
- Dataset: https://www.kaggle.com/clmentbisaillon/fake-and-real-news-dataset
- Train 3 binary text-classfication models to detect Fake/True news, you are free to use
  - Any text processing/feature-engineering setup: Bag-of-words, TF-iDF, pretrained, FastText, GloVe, BERT, XLNET, RoBERTa, etc.
  - Any algorithms:  XGBoost, LightGBM, CNN, LSTM, etc.
- Sample your own train and test set, and report test-set's F1 scores and accuracy for each of your models.
- Add a summary section to describe why you chose to train those models, and which is the most preferred.
- **Please showcase your skills!**

#### Notes

- You are required to code in a [Jupyter Notebook](https://jupyter.org/), using Python **3**
- Example libraries/frameworks you can use: Sklearn, TensorFlow, Keras, Pytorch, Huggingface's transformers, etc.
- Feel free to take blocks of your code from existing public kaggle kernels or external tutorials online. Add a comment to indicate the source of your code if you do so.
- Save the following files into the `submit/` folder:
  - One Jupyter notebook, detailing your entire ML pipeline as per instructions.
- Do not submit any locally-saved embedding files.
- Do not attempt to hyper-parameter tune your models.
- If you lack CPU or GPU resources, feel free to re-sample your dataset to be smaller.
- Other than the points listed in instructions, there are no strict rules on what to include in your jupyter notebook. You are free to apply data cleaning and exploratory data analysis on top of whatever that is required.
- The following will be evaluated:
  - Code correctness
  - Readibility
  - Summary

---

Good luck!
