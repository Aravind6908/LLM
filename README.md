# **Building a Retrieval-Augmented Generation (RAG) System Using UMBC ISSS Data**

### **Introduction**

Retrieval-Augmented Generation (RAG) is a cutting-edge approach in natural language processing (NLP). It combines the power of retrieval systems with generative models, enabling precise and contextually aware responses to user queries. In this project, we built a RAG system leveraging UMBC ISSS (International Student & Scholar Services) data to provide meaningful responses by utilizing a retrieval pipeline backed by FAISS and BM25 and a generator powered by GPT-3.5.

### **Objective** 

The goal of this project was to create an efficient RAG system that:

1. Processes and breaks down large, unstructured text data (sourced from Word documents).

2. Preprocesses and embeds the text data for effective retrieval.

3. Ranks and retrieves the most relevant chunks using cross-encoders.

4. Generates accurate and user-friendly responses tailored to a given query.

### **System Workflow**

#### **1. Data Source and Preprocessing**

The input for our system was a collection of Word documents containing UMBC ISSS data. To make this information machine-readable and queryable, the preprocessing involved:

* Extracting text from Word documents using libraries like python-docx.

* Cleaning the extracted text to remove noise, such as special characters and URLs.

* Breaking down the cleaned text into semantically meaningful chunks using sentence tokenization and token size limits.

* Adding contextual metadata to each chunk, including DocumentID, ChunkID, and Text, and saving them as JSON files.



#### **2. Embedding the Data**

Once the data was preprocessed, we utilized Sentence Transformers to embed the text into high-dimensional vector representations. This embedding phase was crucial for enabling similarity-based retrieval.

**Key Steps:**

* Used pre-trained models from the Sentence Transformers library (e.g., all-mpnet-base-v2).

* Converted each JSON chunk’s text field into an embedding vector.

* Stored the embeddings in a FAISS index for efficient similarity searches.

#### **3. Retrieval Pipeline**

Retrieval was implemented using a hybrid approach:

1. **BM25:** A traditional sparse vector retrieval method that quickly identifies potentially relevant chunks based on keyword matching.

2. **FAISS:** A dense vector retrieval method used for precise similarity scoring based on embeddings.

3. **Cross-Encoders:** Leveraging models like BERT for re-ranking the retrieved documents, ensuring the highest relevance for user queries.

This combination ensured both speed and accuracy in identifying the top-ranked documents for any given query.

#### **4. Generative Response**

To craft meaningful and query-specific responses:

* Generator Model: GPT-3.5 was used to generate natural language responses.

* Optimization: The generator took the query along with the top-ranked retrieved chunks as context, ensuring the response was both accurate and comprehensive.


### **Implementation Details**

#### **Preprocessing Notebook**

The preprocessing pipeline was implemented in Python using Jupyter Notebook. Key components included:

* **Text Extraction:** Extracted text from Word documents and other supported file formats.

* **JSON Chunking:** Divided the text into smaller JSON chunks based on semantic and token size constraints.

**Contextual Metadata:** Added context to each chunk to improve retrieval performance.

#### **RAG Pipeline Notebook**

The main RAG pipeline combined the retrieval and generation processes:

**Embedding Phase:**

* Imported pre-trained models from Sentence Transformers.

* Indexed embeddings using FAISS for dense similarity searches.

**Retrieval Phase:**

* Initial document filtering using BM25.

* Dense retrieval via FAISS.

* Re-ranking the results using BERT-based cross-encoders for enhanced relevance.

**Response Generation:**

* Integrated GPT-3.5 for generating human-like responses.

* Provided the query and top-ranked chunks as input context to the generator.

### **Challenges and Solutions**

**Challenge:** Processing large Word documents efficiently.

* **Solution:** Implemented robust preprocessing scripts to automate text extraction and segmentation.

**Challenge:** Balancing retrieval speed and accuracy.

* **Solution:** Hybrid retrieval with BM25 for speed and FAISS + cross-encoders for precision.

**Challenge:** Ensuring coherent and context-aware responses.

* **Solution:** GPT-3.5 was optimized to generate responses tailored to the retrieved content.


### **Results and Applications**

The RAG system successfully demonstrated:

**Efficient Retrieval:** Rapid identification of relevant text chunks.

* **Accurate Generation:** Context-aware responses that addressed user queries comprehensively.

* **Scalability:** A modular architecture that can handle additional datasets or integrate with other domains seamlessly.

Potential applications include:

* Assisting international students with quick answers to frequently asked questions.

* Supporting administrative tasks by summarizing or reformatting ISSS information.

* Enhancing user experience through personalized query handling.


### **Conclusion**

This project showcased the potential of RAG systems in making large-scale unstructured data actionable and user-friendly. By combining advanced retrieval mechanisms with state-of-the-art generative models, we bridged the gap between static document repositories and dynamic, query-driven information access.

Stay tuned for a step-by-step guide on replicating this pipeline for your own data sources!
