# Job Resume Matching System

This project implements a system that matches uploaded resumes with relevant job descriptions based on a cosine similarity algorithm. It features a user-friendly graphical interface built with tkinter for resume uploading and displaying matching job positions.

## Table of Contents
- [Features](#features)
- [How It Works](#how-it-works)
- [Dataset](#dataset)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Libraries Used](#libraries-used)

## Features
- **Resume Upload**: Easily upload your resume (PDF format) through a tkinter GUI.
- **Text Extraction**: Extracts text content from PDF resumes for analysis.
- **Job Description Indexing**: Indexes a dataset of job descriptions using TF-IDF (Term Frequency-Inverse Document Frequency) for efficient searching.
- **Cosine Similarity Matching**: Calculates the cosine similarity between the uploaded resume and job descriptions to find the most relevant matches.
- **Interactive Results Display**: Presents matched job positions in a sidebar, allowing users to view detailed company information and job descriptions.
- **Stemming and Stopword Removal**: Utilizes NLTK's Porter Stemmer and custom stopwords for improved text processing and accuracy.

## How It Works
The system operates in several key steps:

1. **GUI for Upload**: A tkinter window prompts the user to upload a PDF resume.
2. **Resume Processing**:
   - The uploaded PDF is saved to a dataset folder.
   - pdfminer is used to extract plain text from the PDF.
   - The extracted text is then tokenized, lowercased, and preprocessed by removing stopwords and applying stemming using the Porter Stemmer.
3. **Job Description Indexing (Offline)**:
   - A data.csv file containing job descriptions is loaded.
   - Each job description undergoes the same preprocessing steps (tokenization, stopword removal, stemming).
   - An inverted index is created, storing the frequency of each term in every job description.
   - TF-IDF vectors are generated for all job descriptions, which represent their content numerically.
4. **Query Vector Creation**: The processed resume text is converted into a query vector using the same TF-IDF scheme as the job descriptions.
5. **Cosine Similarity Calculation**: The cosine similarity between the resume's query vector and each job description's TF-IDF vector is calculated. This metric determines how "similar" the resume is to each job description.
6. **Results Display**:
   - Job descriptions with a cosine similarity score above a certain threshold (currently 0.08) are considered matches.
   - The matched job positions are displayed in a new tkinter window, ordered by their similarity score (highest first).
   - Clicking on a job position in the sidebar reveals its company name and full job description.

## Dataset
The project expects a `data.csv` file within a `dataset/` directory. This CSV should contain the following columns:

- `docid`: Unique document ID.
- `company`: Name of the company.
- `position`: Job position title.
- `url`: (Optional) URL to the job posting.
- `location`: Job location.
- `headquarters`: Company headquarters.
- `employees`: Number of employees.
- `founded`: Year company was founded.
- `industry`: Industry of the company.
- `Job Description`: The full text of the job description.

Additionally, a `stopwords.txt` file is required in a `stopwords/` directory, containing one stopword per line.

## Prerequisites
Before running the application, ensure you have the following installed:
- Python 3.x
- pip (Python package installer)

## Installation
1. Clone the repository:
```bash
git clone https://github.com/Jatin-Kesnani/Job-Resume-Matching-System.git
cd job-resume-matching-system

## Libraries Used

| Library | Purpose |
|---------|---------|
| `tkinter` | Building the graphical user interface |
| `pandas` | Data manipulation and CSV reading |
| `nltk` (Natural Language Toolkit) | Text processing |
| &nbsp;&nbsp;`PorterStemmer` | Word stemming |
| &nbsp;&nbsp;`stopwords` | Stopword filtering (via stopwords.txt) |
| `pdfminer.six` | PDF text extraction |
| `shutil` | File operations |
| `os` | Path handling |
| `re` | Regular expressions (tokenizer) |
| `math` | Mathematical operations for TF-IDF and cosine similarity |
