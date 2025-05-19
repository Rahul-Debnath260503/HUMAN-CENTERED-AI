
# 📘 Indian Law Legal QA Assistant (FAISS-Powered)

This project implements a Legal Question Answering system for Indian Law, utilizing a combination of pre-defined Question-Answer pairs and a PDF document. It leverages Sentence Transformers for semantic search and FAISS for efficient similarity retrieval, providing relevant information based on user queries.

## Features

*   **Hybrid Retrieval:** Searches for answers in both a curated CSV file and a PDF document.
*   **Semantic Search:** Uses sentence embeddings to understand the meaning of questions and find semantically similar answers or relevant text.
*   **Efficient Retrieval:** Employs FAISS (Facebook AI Similarity Search) for fast nearest-neighbor lookup in the embedding space.
*   **Intuitive UI:** Provides a user-friendly interface powered by Gradio for easy interaction.
*   **Source Fallback:** If a strong match is not found in the QA pairs, it attempts to retrieve relevant text from the PDF document.

## Project Structure

The project is implemented as a single script in a Google Colab notebook, divided into the following main sections:

1.  **Setup:** Installs necessary libraries.
2.  **Imports:** Imports required modules.
3.  **Data Loading:**
    *   Loads QA pairs from a CSV file.
    *   Extracts and chunks text from a PDF document.
4.  **Embeddings:** Generates sentence embeddings for questions and PDF chunks using a pre-trained Sentence Transformer model.
5.  **FAISS Indexing:** Builds FAISS indexes for the generated embeddings to enable fast similarity search.
6.  **Hybrid QA Retrieval Function:** Defines a function to process user queries, perform searches in both QA and PDF sources, and format the response.
7.  **Gradio UI:** Creates and launches a web interface using Gradio to interact with the QA system.

## Setup and Installation

This project is designed to run in Google Colab.

1.  **Open the Notebook:** Open the Colab notebook containing the provided code.
2.  **Run the Setup Cell:** Execute the cell containing the `!pip install` commands to install all required libraries. This includes:
    *   `transformers`
    *   `datasets`
    *   `faiss-cpu`
    *   `sentence-transformers`
    *   `gradio`
    *   `pandas`
    *   `PyMuPDF`

## Data

*   **`FINAL_MERGE_IPC_Final_all.csv`:** This CSV file should contain at least two columns: "Question" and "Answer", providing curated legal QA pairs.
*   **`merged.pdf`:** This PDF file is used as an additional source of information. The text from this PDF is extracted and chunked to be used for retrieval if a direct answer is not found in the CSV.

**Note:** Ensure these files are uploaded to your Google Drive or the Colab environment at the specified paths (`/content/FINAL_MERGE_IPC_Final_all.csv` and `/content/merged.pdf`).

## How it Works

1.  **Load Data:** The system loads questions and answers from the CSV and text chunks from the PDF.
2.  **Embeddings:** Both questions (from CSV) and text chunks (from PDF) are converted into numerical vectors (embeddings) using the `all-MiniLM-L6-v2` Sentence Transformer model.
3.  **FAISS Indexing:** These embeddings are then indexed using FAISS, creating structures optimized for finding the most similar embeddings quickly.
4.  **User Query:** When a user enters a question, it is also converted into an embedding.
5.  **Hybrid Search:**
    *   The system first searches the FAISS index of question embeddings to find the most similar pre-defined questions. The corresponding answers are retrieved.
    *   If the similarity score from the QA search indicates a poor match (above a certain threshold), the system then searches the FAISS index of PDF chunk embeddings to find the most relevant text snippet from the PDF.
6.  **Response Generation:** The system combines the retrieved answers from the CSV and/or the relevant text from the PDF to form a comprehensive response, presented in Markdown format.
7.  **Gradio Interface:** The Gradio interface allows users to input their questions and view the generated responses in a web browser. The `share=True` parameter in `interface.launch()` provides a public shareable link.

## Usage

1.  Ensure the required libraries are installed and the data files (`.csv` and `.pdf`) are in the correct locations.
2.  Run all the code cells in the notebook sequentially.
3.  Once the Gradio interface is launched, a local URL and potentially a public shareable link will be displayed.
4.  Open the provided URL in your web browser.
5.  Enter your legal question in the text box and press Enter or click the "Submit" button.
6.  The system will process your question and display the relevant information below.

## Libraries Used

*   `transformers`: For potentially using models, although primarily `sentence-transformers` is used for embeddings.
*   `datasets`: Often used for handling datasets, though not explicitly used for loading in this script.
*   `faiss-cpu`: For building and searching the FAISS indexes on the CPU.
*   `sentence-transformers`: For generating sentence embeddings.
*   `gradio`: For creating the web-based user interface.
*   `pandas`: For reading and processing the CSV file.
*   `PyMuPDF` (`fitz`): For extracting text from the PDF document.
*   `numpy`: For numerical operations, especially with embeddings and FAISS.
*   `torch`: Used by the underlying models (Sentence Transformers).
*   `os`: For checking file existence.

## Acknowledgments

*   **Sentence Transformers:** For providing easy-to-use models for generating sentence embeddings.
*   **FAISS:** For enabling efficient similarity search.
*   **Gradio:** For simplifying the creation of machine learning demos.
*   **PyMuPDF:** For efficient PDF processing.

---

This README provides a detailed overview of your project. You can easily adapt this structure and content when creating your report. Remember to expand on each section with more technical details and analysis for a formal report.
