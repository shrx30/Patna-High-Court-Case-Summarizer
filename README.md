# Patna-High-Court-Case-Summarizer
# Legal Document Processing and Summarization

This project provides a Python script to process a CSV file containing legal document text, extract key information, and generate a summary for a specific case number using translation, Named Entity Recognition (NER), and a large language model.

## Features

* Reads legal document data from a CSV file.
* Selects specific document content based on a case number (filename).
* Translates Hindi legal text to English.
* Performs Named Entity Recognition (NER) to identify key entities.
* Generates a summary of the document using a large language model based on extracted entities.

## Prerequisites

Before running this script, ensure you have the following installed:

* Python 3.7 or higher
* `pip` (Python package installer)

You will also need a Google Cloud account and a Gemini API key.

## Installation

1.  **Save the provided Python code:** Save the core processing logic (which you can adapt from the Streamlit code or your notebook, focusing on the processing functions) as a Python file (e.g., `process_document.py`).
2.  **Install the required Python libraries** by running:

    ```bash
    pip install pandas spacy googletrans==4.0.0-rc1 google-generativeai
    ```
3.  **Download the SpaCy English model** by running:

    ```bash
    python -m spacy download en_core_web_sm
    ```

## How to Run

1.  **Set your Gemini API Key:** Set your API key as an environment variable named `GOOGLE_API_KEY`.
2.  **Prepare your CSV file:** Make sure you have a CSV file with at least `filename` and `content` columns in the same directory as your script, or be ready to provide the full path.
3.  **Run the Python script** from your terminal. You will need to modify the script to specify the path to your CSV and the case number you want to process.

    ```bash
    python process_document.py
    ```

    *(Note: You will need to add command-line argument parsing or modify the script to take file path and case number as input.)*

## Usage

Modify the Python script (`process_document.py`) to:

1.  Specify the path to your input CSV file.
2.  Specify the case number (value from the `filename` column) for which you want to generate a summary.
3.  Run the script from your terminal as shown above. The script will print the generated summary to the console.

## Project Steps Explained

The script processes the input CSV and generates a summary for a selected case number through the following automated steps, derived from the logic in your notebook:

1.  **Load CSV Data:** The script reads the specified CSV file into a pandas DataFrame. It expects columns named `filename` and `content`.
2.  **Select Case:** It filters the DataFrame to find the row where the `filename` matches the provided case number.
3.  **Translate Content:** The `content` of the selected case is translated from Hindi to English using the `googletrans` library. This is necessary as the subsequent NLP steps are performed on English text.
4.  **Named Entity Recognition (NER):** The translated English text is processed using the `en_core_web_sm` model from the spaCy library. This step identifies and categorizes key entities within the text, such as names of people, organizations, locations, and dates.
5.  **Generate Summary:** The extracted named entities are used as input for the Gemini 1.5 Pro model via the `google-generativeai` library. The model then generates a concise summary of the original document, focusing on the key information highlighted by the NER process. The generated summary is the final output of the script.

This script provides a command-line tool to process and summarize individual legal documents based on their case number within a CSV dataset.
