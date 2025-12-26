Prompt Engineering for Mathematics: Unified State Exam Baseline

This repository contains a specialized prompt engineering framework designed to solve Russian Unified State Exam (Mathematics) problems using Large Language Models (LLMs). The project was developed for a Kaggle competition focused on optimizing LLM performance for mathematical reasoning and standardized test accuracy.
Project Overview

The primary objective is to develop a robust generation pipeline and prompt architecture that enables an LLM (specifically Gemini 1.5 Flash) to solve mathematics problems with high precision. The dataset consists of problems sourced from the Open Problem Bank for the Unified State Exam, requiring the model to interpret TeX notation and output strictly formatted numerical answers.
Key Objectives

    Implement a high-accuracy prompt strategy for mathematical reasoning.

    Develop a robust extraction pipeline for numerical values.

    Utilize consensus-based voting to improve reliability.

    Adhere to strict formatting constraints (integer or finite decimal with dot separator).

Technical Implementation
1. Prompt Architecture

The solution employs a Few-Shot Chain-of-Thought (CoT) prompting strategy. By providing the model with a structured SYSTEM_INSTRUCTION and diverse examples (Algebra, Geometry, Probability, and Arithmetic), the model is conditioned to:

    Identify the problem type before attempting a solution.

    Extract variables and given information.

    Execute step-by-step reasoning with explicit verification.

    Standardize the final output using LaTeX \boxed{} tags.

2. Consensus Mechanism (Majority Voting)

To mitigate model hallucination and stochastic errors, the pipeline implements a majority voting system:

    Each problem is processed n times (defaulting to 3 samples).

    The answers are extracted and compared using a Counter object.

    The most frequent result is selected as the final answer, significantly increasing the probability of correctness over a single-pass inference.

3. Numerical Extraction Pipeline

Since LLM outputs can be verbose, a multi-stage regex-based extraction utility was built:

    Primary Method: Extracts content from LaTeX \boxed{} tags.

    Secondary Method: Identifies keyword patterns such as "Final Answer:" or "Result:".

    Fallback Method: Retrieves the last valid numerical value in the text while filtering for outliers (e.g., year markers or problem IDs).

Dataset Description

The competition utilizes the following data structures:

    train.csv: Training set containing problem statements and labels.

    test_with_translation.csv: Test set including automatic translations for multilingual processing.

    Target Format: Answers must be single numbers (integers or decimals using the "." separator).

Requirements

The following libraries are required to run the notebook:

    google-generativeai

    pandas

    tqdm

    re (Standard Library)

    collections (Standard Library)

Usage

    Clone the repository.

    Ensure you have a valid API key for the Gemini API (or the TapSage/Metis proxy as configured in the notebook).

    Place the competition data in the /kaggle/input/ directory or update the file paths in the script.

    Execute the Jupyter Notebook to generate the submission.csv file.

Acknowledgments

    Source Data: Open problem bank for the Unified State Exam (Mathematics).

    Competition Platform: Kaggle Prompt Engineering Challenge. 
