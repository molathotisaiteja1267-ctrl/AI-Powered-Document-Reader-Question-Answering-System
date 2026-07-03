# AI Powered Document Reader & Question Answering System

An intelligent system that transforms document reading into interactive knowledge retrieval through natural language queries.

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Solution](#solution)
- [System Architecture](#system-architecture)
- [Technologies Used](#technologies-used)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Performance](#performance)
- [Limitations](#limitations)
- [Future Enhancements](#future-enhancements)
- [Author](#author)

## Overview

This project builds an intelligent system that reads documents and answers questions using Artificial Intelligence and Natural Language Processing. The core technology is called **Retrieval-Augmented Generation (RAG)**.

Instead of spending 20-30 minutes manually searching through hundreds of pages, you can now get accurate answers in 2-3 seconds. For example, simply ask "What are the key findings in Chapter 3?" or "Explain the methodology used in this research paper" and receive precise, document-grounded responses instantly.

## Problem Statement

We live in a digital age with vast resources - research papers, textbooks, IS codes, and technical manuals. Yet finding specific information from hundreds of pages remains time-consuming and frustrating.

**Traditional Methods Fall Short:**
- **Reading Everything**: Reading a 200-page document manually is extremely time-consuming
- **Ctrl+F Search**: Finds exact words only, misses concepts and related information
- **Using Index**: Still requires navigating multiple pages and takes significant time

## Solution

This project implements a RAG-based system with two core components:

### Retrieval
Find the most relevant parts of the uploaded document using semantic search.

### Generation
Generate a proper, accurate answer based on what was found using Large Language Models.

### Why Not Just Use ChatGPT?
ChatGPT doesn't know about your specific documents. With this system, you upload your own files and ask questions directly about them - making it far more targeted and reliable.

**Privacy & Security Benefits:**
- In ChatGPT or other AI platforms, you cannot upload your personal or company confidential data
- This system runs locally and doesn't store your data on any external server
- Complete data privacy - your documents never leave your environment
- Ideal for sensitive documents like legal files, company reports, or proprietary research

## System Architecture

The system follows a two-part design:

### Part 1: Document Processing (One-time per document)
1. **PDF Upload**: Upload document to AWS S3
2. **Text Extraction**: Extract text using PyPDF2
3. **Chunking**: Break document into 600-word chunks with 150-word overlap
4. **Embedding**: Convert chunks to 384-dimensional vectors using Sentence-BERT
5. **Storage**: Store embeddings in FAISS database

### Part 2: Question Answering (Every query)
1. **Question Embedding**: Convert user question to 384-dimensional vector
2. **Semantic Search**: Find top 3 most similar chunks from FAISS database
3. **Answer Generation**: Send chunks + question to GROQ LLM to generate answer

## Technologies Used

- **Python 3.9**: Core programming language with extensive AI/ML library support
- **Sentence-BERT (all-MiniLM-L6-v2)**: High-quality, fast, open-source embedding model
- **GROQ**: Large Language Models for high-quality answer generation
- **PyPDF2**: Simple and reliable PDF text extraction library
- **FAISS**: Facebook's vector database for extremely fast similarity search at scale
- **Streamlit**: Rapid web application framework for building interactive UIs

## Features

- Upload PDF documents and ask questions in plain English
- Understands meaning, not just keywords (semantic search)
- Generates accurate, document-grounded answers
- Delivers results in 3-4 seconds
- Handles documents up to 1000+ pages
- Clean and intuitive user interface
- Complete data privacy - runs locally without external data storage

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/ai-document-qa-system.git
cd ai-document-qa-system

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Add your GROQ API key to .env file
```

## Usage

```bash
# Run the Streamlit application
streamlit run app.py
```

1. Open your browser and navigate to `http://localhost:8501`
2. Upload a PDF document using the file uploader
3. Wait for document processing to complete
4. Enter your question in the text input field
5. Click "Get Answer" to receive AI-generated response

## Performance

### Document Processing Speed
- 60 pages: 5 seconds
- 350 pages: 8 seconds
- 500 pages: 12 seconds
- 1000+ pages: 20 seconds

### Question Answering Speed
Consistently takes just 1 second regardless of document size

### Answer Quality (50 Questions Tested)
- **Relevance**: 4.3/5
- **Accuracy**: 4.1/5
- **Clarity & Explanation**: 4.2/5
- **Overall Score**: 4.1/5.0
- **Success Rate**: 82% of answers rated good or excellent

## Limitations

### Current Limitations
- **No Image/Table Reading**: Cannot process diagrams, tables, or visual content within documents
- **English Only**: Does not support Hindi or other regional languages currently
- **No Maths**: Cannot perform mathematical calculations from document data
- **Multi-Section Queries**: Struggles with questions requiring synthesis across multiple sections

### Key Challenges During Development
- **Chunk size tuning**: Too small = insufficient context; too large = irrelevant noise. 600 words found optimal
- **Memory management**: Large documents consume significant RAM - required careful optimization
- **Prompt design**: AI answer quality depended heavily on how the prompt was structured

## Future Enhancements

- **Image Support**: Read diagrams and tables from documents
- **Multi-Language**: Support Hindi and other Indian languages
- **Show Sources**: Highlight exactly where answers come from
- **Mobile App**: Extend accessibility to smartphones
- **Mathematical Reasoning**: Add capability to perform calculations from document data
- **Multi-Document Search**: Query across multiple documents simultaneously

## Author

**Molathoti Sai Teja**
- Roll No: 24065068
- Project Guide: Dr. Suresh Kumar, Associate Professor, IIT BHU

## Acknowledgments

This project successfully demonstrates how AI can solve a real student problem - delivering document answers in 2 seconds instead of 20-30 minutes of manual searching, with 82% of answers rated good or excellent across 1,200+ pages.

Building this system taught me that successful AI applications require clear problem understanding, proper tool selection, and thorough testing. It has been a truly valuable learning experience.

---

**Note**: This project represents a practical application of Natural Language Processing and Retrieval-Augmented Generation techniques.
