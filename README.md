# Agentic Adaptive RAG with LangGraph (აგენტური რაგ ჩატბოტი)

 RAG systems that know when to retrieve documents, search the web, or generate responses directly

An advanced Retrieval-Augmented Generation (RAG) system that intelligently integrates dynamic query analysis with self-correcting mechanisms to optimize response accuracy. Unlike traditional RAG approaches, this system adapts its strategy based on query complexity and context.

##  Key Features

- **  Intelligent Query Routing**: Automatically determines whether to use local documents, web search, or direct LLM generation
- **  Multi-Stage Quality Assurance**: Document relevance assessment, hallucination detection, and answer quality evaluation
- **  Self-Correcting Mechanisms**: Automatically triggers additional retrieval or regeneration when quality thresholds aren't met
- **  Hybrid Knowledge Sources**: Seamlessly combines local vector store with real-time web search
- **  Production-Ready**: Built with LangGraph for robust state management and workflow orchestration

##  System Architecture

The system implements three different retrieval strategies based on query complexity:

- **No Retrieval**: For queries answerable from parametric knowledge
- **Single-Step Retrieval**: For simple queries requiring document lookup
- **Multi-Hop Retrieval**: For complex queries requiring reasoning across multiple sources


##  Testing

Run the comprehensive test suite:

```bash
python -m pytest . -s -v
```

The test suite validates:
- Document relevance grading
- Hallucination detection
- Query routing logic
- Generation quality
- End-to-end workflow



##  Key Components

### State Management
The system uses a `GraphState` TypedDict that flows through all workflow nodes:
- `question`: User's input query
- `generation`: LLM's response
- `web_search`: Boolean flag for web search necessity
- `documents`: Retrieved documents from local and web sources

### Workflow Nodes

1. **Query Router**: Determines optimal information source (vectorstore vs. web search)
2. **Document Retriever**: Fetches relevant documents from local vector store
3. **Document Grader**: Evaluates document relevance and triggers web search if needed
4. **Web Search**: Queries external sources for additional information
5. **Generator**: Creates responses using retrieved context
6. **Quality Graders**: Assess hallucinations and answer relevance

### Decision Logic

The system implements intelligent decision-making at multiple points:
- Routes queries based on content domain
- Grades document relevance and triggers web search for insufficient results
- Detects hallucinations and regenerates responses when needed
- Evaluates answer quality and seeks additional information if required

## Performance Optimization

- **Chunk Size**: Optimized at 250 tokens for better embedding quality
- **Retrieval Limit**: Configurable number of documents retrieved
- **Web Search Results**: Limited to 3 results for efficiency
- **Caching**: Persistent Chroma vector store for faster subsequent queries

##  Advanced Features

### Quality Assurance Pipeline

1. **Document Relevance Scoring**: Binary classification of document relevance
2. **Hallucination Detection**: Verification that responses are grounded in evidence
3. **Answer Quality Assessment**: Evaluation of response completeness and relevance

### Adaptive Routing

The system intelligently routes queries based on:
- Content domain analysis
- Query complexity assessment
- Available knowledge sources
- Previous retrieval success rates

##  Future Enhancements

- [ ] **LLM Fallback State**: Direct LLM responses for conversational queries
- [ ] **Enhanced Router**: Three-way routing (vectorstore/websearch/llm_fallback)
- [ ] **Multi-Modal Support**: Image and document understanding
- [ ] **Conversation Memory**: Context preservation across interactions
- [ ] **Custom Evaluation Metrics**: Domain-specific quality assessment

