<h1>FAQ Chatbot with LangChain and FAISS</h1>
  <p>
    This project implements an FAQ chatbot that leverages LangChain, FAISS, and HuggingFace models to retrieve and answer user queries based on a pre-built FAQ dataset.
    It uses normalized document embeddings for cosine-similarity–based retrieval and generates responses using a FLAN-T5 model hosted on HuggingFace.
  </p>
  
  <h2>Table of Contents</h2>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#features">Features</a></li>
    <li><a href="#installation">Installation</a></li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#how-it-works">How It Works</a></li>
    <li><a href="#dependencies">Dependencies</a></li>
    <li><a href="#license">License</a></li>
  </ul>
  
  <h2 id="overview">Overview</h2>
  <p>
    The FAQ Chatbot loads a JSON-based FAQ dataset (each entry contains a question and an answer) and then:
  </p>
  <ol>
    <li>Formats each FAQ item as a document.</li>
    <li>Creates embeddings for each document using the <code>sentence-transformers/all-MiniLM-L6-v2</code> model.</li>
    <li>Normalizes these embeddings to convert L2 distances into cosine similarity values.</li>
    <li>Builds a FAISS index (vector store) to enable efficient document retrieval.</li>
    <li>Uses LangChain's <code>ConversationalRetrievalChain</code> and conversation memory to maintain dialogue context.</li>
    <li>Generates final responses by retrieving the most similar FAQ documents and providing them as context to a FLAN-T5 model hosted on HuggingFace.</li>
  </ol>

  <h2 id="features">Features</h2>
  <ul>
    <li><strong>Document Embedding &amp; Normalization:</strong> Embeddings are normalized so that cosine similarity is used for retrieval.</li>
    <li><strong>FAISS Vector Store:</strong> Uses FAISS to index and retrieve FAQ documents efficiently.</li>
    <li><strong>Conversational Memory:</strong> Maintains conversation history with LangChain's <code>ConversationBufferMemory</code>.</li>
    <li><strong>HuggingFaceHub Integration:</strong> Utilizes a FLAN-T5 model to generate responses based on the retrieved context.</li>
    <li><strong>Debug Information:</strong> Outputs similarity scores and source documents for verification and debugging.</li>
  </ul>

  <h2 id="installation">Installation</h2>
  <ol>
    <li>
      <strong>Clone the repository:</strong>
      <pre><code>git clone https://github.com/yourusername/faq-chatbot.git
cd faq-chatbot</code></pre>
    </li>
    <li>
      <strong>Create a virtual environment:</strong>
      <pre><code>python3 -m venv venv
source venv/bin/activate   </code></pre>
    </li>
    <li>
      <strong>Install the dependencies:</strong>
      <pre><code>pip install numpy langchain faiss-cpu transformers huggingface_hub</code></pre>
    </li>
    <li>
      <strong>Download the FAQ dataset:</strong>
      <p>Ensure that the file <code>Ecommerce_FAQ_Chatbot_dataset.json</code> is in the same directory as your code.</p>
    </li>
  </ol>

  <h2 id="usage">Usage</h2>
  <p>To run the chatbot, execute the following command:</p>
  <pre><code>python chatbot.py</code></pre>
  <p>
    After launching, you will see the prompt:
  </p>
  <pre><code>FAQ Chatbot is ready. Type your questions (or type 'exit' to quit):</code></pre>
  <p>
    Enter your query and the chatbot will generate an answer based on the top-3 most similar FAQ documents along with debug output showing similarity scores.
  </p>

  <h2 id="how-it-works">How It Works</h2>
  <ol>
    <li>
      <strong>Data Loading &amp; Preprocessing:</strong>
      <p>The FAQ dataset (JSON file) is loaded and each entry is formatted as <code>Q: [question]</code> and <code>A: [answer]</code>. The documents are then printed for initial verification.</p>
    </li>
    <li>
      <strong>Embedding Generation:</strong>
      <p>An embedding model (<code>sentence-transformers/all-MiniLM-L6-v2</code>) is used to generate embeddings for each document. These embeddings are normalized to unit vectors to enable cosine similarity comparisons.</p>
    </li>
    <li>
      <strong>Vector Store Construction:</strong>
      <p>Each document and its corresponding normalized embedding are combined into pairs. FAISS builds an index from these pairs for fast similarity-based retrieval.</p>
    </li>
    <li>
      <strong>Conversational Retrieval Chain:</strong>
      <p>A retriever is created from the FAISS index and integrated with LangChain's <code>ConversationalRetrievalChain</code>. Conversation memory is maintained using <code>ConversationBufferMemory</code> (configured to store only the chatbot's answer) to track dialogue context. Retrieved documents serve as context for the FLAN-T5 model hosted on HuggingFace to generate responses.</p>
    </li>
    <li>
      <strong>User Interaction:</strong>
      <p>When a user inputs a query, the chatbot retrieves the most relevant FAQ documents, passes the context to the language model, and returns a generated answer. Debug information, including source document details and similarity scores, is printed to the console.</p>
    </li>
  </ol>

  <h2 id="dependencies">Dependencies</h2>
  <ul>
    <li>Python 3.8+</li>
    <li>numpy – For numerical operations</li>
    <li>langchain – For chaining language model calls and managing conversation memory</li>
    <li>faiss-cpu – FAISS vector store for efficient similarity search</li>
    <li>transformers – HuggingFace library for tokenization and model inference</li>
    <li>huggingface_hub – For accessing models and tokens from HuggingFace</li>
  </ul>
  <p>To install all dependencies, run:</p>
  <pre><code>pip install numpy langchain faiss-cpu transformers huggingface_hub</code></pre>

  <h2 id="license">License</h2>
  <p>
    This project is open source and available under the <a href="LICENSE">MIT License</a>.
  </p>