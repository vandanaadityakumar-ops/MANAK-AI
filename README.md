# MANAK AI 🤖🇮🇳

> **AI-powered Intelligent Assistant for Indian Standards and BIS
> Services for Industries and Consumers**

**Smart India Hackathon 2026** · Problem Statement **SIH26107** · Theme
**Smart Automation** · Category **Software** · Team **RUSHLINERS**

------------------------------------------------------------------------

## 📌 Table of Contents

-   [Overview](#-overview)
-   [Problem Statement](#-problem-statement)
-   [Our Solution](#-our-solution)
-   [Core Features](#-core-features)
-   [How MANAK AI Works](#-how-manak-ai-works)
-   [System Architecture](#-system-architecture)
-   [Technology Stack](#-technology-stack)
-   [Major Components](#-major-components)
-   [RAG and Grounded Answers](#-rag-and-grounded-answers)
-   [Multimodal Interaction](#-multimodal-interaction)
-   [Compliance Readiness Engine](#-compliance-readiness-engine)
-   [Geospatial Laboratory Finder](#-geospatial-laboratory-finder)
-   [Automated Gazette Watchdog](#-automated-gazette-watchdog)
-   [Challenges and Mitigations](#-challenges-and-mitigations)
-   [Feasibility and Viability](#-feasibility-and-viability)
-   [Impact and Benefits](#-impact-and-benefits)
-   [Implementation Roadmap](#-implementation-roadmap)
-   [Project Workflow](#-project-workflow)
-   [Research and References](#-research-and-references)
-   [Prototype](#-prototype)
-   [Project Status and Scope Notes](#-project-status-and-scope-notes)

------------------------------------------------------------------------

# 🔎 Overview

**MANAK AI** is a proposed multimodal AI assistant designed to simplify
**Bureau of Indian Standards (BIS)** compliance, Indian Standards
discovery, product certification workflows, and related services for
industries, MSMEs, manufacturers, artisans, and consumers.

The system combines:

-   conversational AI,
-   multilingual text and voice interaction,
-   visual product/label scanning,
-   clause-level Retrieval-Augmented Generation (RAG),
-   hybrid vector + keyword search,
-   compliance-readiness assessment,
-   geospatial laboratory discovery,
-   and automated monitoring of e-Gazette updates.

The central idea is simple:

> **Turn complicated standards and regulatory documents into grounded,
> understandable, actionable answers.**

Instead of forcing a manufacturer or consumer to manually search lengthy
standards, gazettes, formulas, tables, and certification documents,
MANAK AI is designed to retrieve the relevant information and present it
through a user-friendly interface.

------------------------------------------------------------------------

# 🎯 Problem Statement

The project addresses **SIH26107: "AI-powered Intelligent Assistant for
Indian Standards and BIS Services for Industries and Consumers."**

The presentation identifies several practical problems:

### For industries and MSMEs

-   Standards can be difficult to discover and interpret.
-   Technical language creates a barrier for non-specialist users.
-   Certification and audit preparation can require significant time and
    consultancy.
-   Finding appropriate testing laboratories can be difficult.
-   Regulatory information changes as new Quality Control Orders (QCOs)
    and amendments are published.

### For consumers

-   Understanding ISI, CRS, and HUID-related information can be
    difficult.
-   Product/mark verification can require navigating multiple sources.
-   Technical standards are not written as conversational consumer
    guidance.

### For BIS/helpdesk operations

-   A large volume of incoming questions can be repetitive.
-   Routine queries can consume staff time that could otherwise be used
    for surveillance, audits, and higher-value work.

------------------------------------------------------------------------

# 💡 Our Solution: MANAK AI

MANAK AI acts as a **multimodal regulatory assistant**.

It is designed to accept natural-language questions, voice queries, and
product/label images, retrieve relevant information from a structured
BIS knowledge corpus, and return a grounded response with source and
clause information.

### Design goals

1.  **Accessibility**\
    Make standards easier to understand without requiring users to know
    regulatory terminology.

2.  **Grounding**\
    Keep responses tied to retrieved standards, clauses, and source
    metadata.

3.  **Multimodality**\
    Allow users to communicate through text, voice, and images.

4.  **Actionability**\
    Convert retrieved regulatory information into checklists, readiness
    information, lab suggestions, and next steps.

5.  **Up-to-dateness**\
    Monitor regulatory updates so the knowledge base can incorporate
    newly published QCOs and amendments.

------------------------------------------------------------------------

# ✨ Core Features

  -----------------------------------------------------------------------
  Feature                             What it does
  ----------------------------------- -----------------------------------
  💬 Multilingual Voice & Text        Supports natural queries in Hindi,
                                      Hinglish, English, and regional
                                      dialects

  📷 Visual Product Scanner           Accepts product, rating-plate, or
                                      label images for identification and
                                      standard mapping

  📚 Clause-Level RAG                 Retrieves relevant standards and
                                      clauses instead of relying only on
                                      model memory

  🔎 Hybrid Search                    Combines dense semantic retrieval
                                      with BM25 keyword/exact matching

  📊 Compliance Readiness             Calculates a factory/product
                                      readiness percentage based on the
                                      available compliance information

  🧪 Geospatial Lab Finder            Maps required testing parameters to
                                      nearby NABL/BIS-accredited
                                      laboratories

  📰 Gazette Watchdog                 Monitors e-Gazette content for
                                      newly published QCOs and amendments

  📝 Pre-Audit Checklists             Turns requirements into practical
                                      preparation steps

  🔗 Grounded Citations               Provides standard, year, clause,
                                      and source metadata with responses

  🏭 MSME Focus                       Reduces dependence on external
                                      consultancy for routine regulatory
                                      discovery
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# ⚙️ How MANAK AI Works

At a high level, the system follows this pipeline:

``` text
                 ┌─────────────────────────┐
                 │         USER            │
                 │ Text / Voice / Image    │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │     Next.js Client      │
                 │ Chat • Scanner • PDF    │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │    FastAPI Gateway      │
                 │ Intent + API Routing    │
                 └────────────┬────────────┘
                              │
                              ▼
              ┌──────────────────────────────────┐
              │       HYBRID RETRIEVAL           │
              │                                  │
              │  LlamaIndex + Qdrant             │
              │  Dense Vector + BM25 + Filters   │
              └───────────────┬──────────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ Context Assembly &      │
                 │ Grounding Guardrail     │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │   Google Gemini API      │
                 │ Large-context reasoning  │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ Verified Response       │
                 │ Answer + Citations +    │
                 │ Actions / Checklists    │
                 └─────────────────────────┘
```

------------------------------------------------------------------------

# 🏗️ System Architecture

The architecture shown in the SIH presentation separates the system into
a frontend, API/backend layer, retrieval layer, knowledge corpus,
reasoning layer, and response layer.

``` mermaid
flowchart TD
    A["User Query<br/>Text / Voice / Regional Language"] --> B["Next.js 14 + React<br/>shadcn/ui Client"]

    B --> C["Python FastAPI Gateway"]
    C --> D["Intent Router<br/>Standard Search / Scheme / Lab Finder / Hallmarking"]

    D --> E["Hybrid Retrieval Engine<br/>LlamaIndex + Qdrant"]

    E --> F["BIS Knowledge Corpus<br/>IS Standards + QCOs + Recognized Labs & HUID Registry"]
    E --> G["Qdrant Hybrid Vector DB<br/>Dense Vectors + BM25 + Payload Filters"]

    F --> E
    G --> E

    E --> H["Context Assembly<br/>Grounding / Validation Guardrail"]
    H --> I["Google Gemini API<br/>Large-context Regulatory Reasoning"]

    I --> J["Verified Client Response"]
    J --> K["Answer + Clause Citation"]
    J --> L["Nearest Lab"]
    J --> M["Compliance Checklist"]
```

### Architecture layers

#### 1. Presentation layer

Built around **Next.js 14, React, Tailwind CSS, and shadcn/ui**.

The presentation describes:

-   responsive chat interface,
-   split-screen PDF preview,
-   pre-audit readiness dashboard,
-   multimodal interaction.

#### 2. API and routing layer

A **Python FastAPI** backend acts as the gateway and intent router.

The presentation specifies:

-   asynchronous/high-concurrency FastAPI,
-   Server-Sent Events (SSE),
-   API gateway/routing,
-   intent classification.

#### 3. Retrieval layer

The retrieval layer uses:

-   **LlamaIndex**
-   **Qdrant**
-   dense vector search,
-   BM25 keyword search,
-   payload filtering.

This hybrid approach is intended to handle both semantic questions and
exact regulatory identifiers, standards codes, clauses, and technical
terminology.

#### 4. Knowledge layer

The proposed knowledge corpus includes:

-   Indian Standards,
-   Quality Control Orders (QCOs),
-   recognized laboratories,
-   HUID-related information.

The implementation roadmap specifically proposes ingesting **150+ key
IS/QCO documents** for the initial RAG corpus.

#### 5. Reasoning layer

**Google Gemini API** is used for large-context regulatory reasoning and
for translating complex specifications into understandable language and
step-by-step schemes.

#### 6. Response layer

The response is intended to be verified and actionable, including:

-   plain-language answers,
-   exact clause citations,
-   laboratory suggestions,
-   compliance checklists.

------------------------------------------------------------------------

# 🧠 RAG and Grounded Answers

One of the most important architectural choices in MANAK AI is its
**Retrieval-Augmented Generation (RAG)** approach.

A conventional LLM can generate fluent answers but may produce
information that is not supported by the underlying regulatory
documents.

MANAK AI instead follows:

``` text
Question
   │
   ▼
Understand intent
   │
   ▼
Retrieve relevant standards / clauses
   │
   ▼
Filter + rank evidence
   │
   ▼
Assemble grounded context
   │
   ▼
Generate response
   │
   ▼
Attach source + clause metadata
```

### Hybrid retrieval

The presentation specifies a hybrid Qdrant search using:

**Dense semantic retrieval**

Useful when the user asks a question using natural language that does
not exactly match the wording of a standard.

**BM25 / keyword retrieval**

Useful for:

-   IS codes,
-   clause numbers,
-   product names,
-   technical terms,
-   exact phrases.

**Payload filtering**

Useful for narrowing retrieval using structured metadata.

This combination is intended to reduce retrieval errors that can occur
when relying on semantic similarity alone.

------------------------------------------------------------------------

# 📄 Document Ingestion and Parsing

Regulatory documents can contain:

-   multiple columns,
-   nested tables,
-   formulas,
-   clause relationships,
-   complex layouts.

The project proposes using:

-   **Docling**
-   **LlamaParse**

for document parsing.

The extracted information is then transformed into structured data
suitable for indexing.

``` mermaid
flowchart LR
    A["BIS Standards / QCO PDFs"] --> B["Document Parser"]
    B --> C["Layout-aware Extraction"]
    C --> D["Tables"]
    C --> E["Clauses"]
    C --> F["Formulas"]
    C --> G["Metadata"]
    D --> H["Chunk + Metadata Pipeline"]
    E --> H
    F --> H
    G --> H
    H --> I["Embeddings + BM25 Index"]
    I --> J["Qdrant"]
```

The presentation specifically identifies **layout-aware extraction** as
a strategy for preserving tables, formulas, and clause relationships.

------------------------------------------------------------------------

# 🎙️ Multimodal Interaction

MANAK AI is designed around the principle that users should not have to
learn the language of bureaucracy before receiving help.

## Text

Users can ask questions naturally in:

-   English
-   Hindi
-   Hinglish
-   regional dialects

## Voice

The proposed voice interface allows users to speak queries instead of
typing them.

This is especially relevant for users who may be less comfortable with
technical English or conventional digital interfaces.

## Vision

The Visual Product Scanner allows users to:

1.  capture a product image,
2.  upload a rating plate or label,
3.  identify relevant visual information,
4.  map it to applicable standards or compliance information.

``` text
       📷 Product / Label
               │
               ▼
       ┌───────────────┐
       │ Vision Layer  │
       └───────┬───────┘
               │
               ▼
       Product / Mark Info
               │
               ▼
       Standard Mapping
               │
               ▼
       RAG Retrieval
               │
               ▼
      Grounded Explanation
```

------------------------------------------------------------------------

# 📊 Compliance Readiness Engine

The proposed **Dynamic Readiness Engine** converts regulatory
requirements into a practical readiness view.

The presentation describes this as a real-time factory compliance score
expressed as **"% Ready"**.

A conceptual flow is:

``` text
Applicable Standard
        │
        ▼
Required Conditions
        │
        ├── Documentation
        ├── Testing
        ├── Product Requirements
        ├── Process Requirements
        └── Other Compliance Items
        │
        ▼
Requirement Checklist
        │
        ▼
Completed / Missing Items
        │
        ▼
       % Ready
        │
        ▼
Pre-Audit Action Plan
```

> **Important:** The supplied presentation describes the readiness
> engine concept but does not specify the exact scoring formula or
> weighting methodology. The final implementation should define those
> rules explicitly.

------------------------------------------------------------------------

# 🧪 Geospatial Laboratory Finder

MANAK AI proposes a laboratory-discovery workflow that connects testing
requirements with nearby laboratories.

The presentation describes automatically pairing required IS test
parameters with nearby **NABL/BIS-accredited laboratories**.

``` text
Applicable Standard
        │
        ▼
Required Test Parameters
        │
        ▼
Laboratory Capability Matching
        │
        ▼
Location / Distance Filtering
        │
        ▼
Nearby Relevant Labs
        │
        ▼
User-facing Lab Suggestions
```

This can reduce the manual effort involved in determining which testing
facilities are relevant to a particular compliance requirement.

------------------------------------------------------------------------

# 📰 Automated Gazette Watchdog

Regulatory information changes.

MANAK AI proposes an automated monitoring layer that watches e-Gazette
publications for:

-   newly published QCOs,
-   amendments,
-   regulatory updates.

The proposed update pipeline is:

``` text
e-Gazette
    │
    ▼
Scheduled / Background Scraper
    │
    ▼
New Document Detection
    │
    ▼
Document Parsing
    │
    ▼
Versioning
    │
    ▼
RAG Re-indexing
    │
    ▼
Updated Knowledge Corpus
```

The presentation also proposes version control to distinguish active and
superseded standards.

------------------------------------------------------------------------

# 🧩 Major Components

## Frontend

**Technologies**

-   Next.js 14
-   React
-   Tailwind CSS
-   shadcn/ui

**Responsibilities**

-   conversational interface,
-   multimodal input,
-   PDF preview,
-   readiness dashboard,
-   displaying grounded answers and actions.

------------------------------------------------------------------------

## Backend

**Technology**

-   Python
-   FastAPI

**Responsibilities**

-   API gateway,
-   intent routing,
-   asynchronous request handling,
-   Server-Sent Events,
-   integration with retrieval and AI services.

------------------------------------------------------------------------

## AI / RAG

**Technologies**

-   Google Gemini API
-   LlamaIndex

**Responsibilities**

-   regulatory reasoning,
-   context orchestration,
-   document indexing/retrieval workflows,
-   large-context processing.

------------------------------------------------------------------------

## Vector Database

**Technology**

-   Qdrant

**Responsibilities**

-   dense vector retrieval,
-   hybrid retrieval,
-   BM25 support,
-   metadata/payload filtering.

------------------------------------------------------------------------

## Document Processing

**Technologies**

-   Docling
-   LlamaParse

**Responsibilities**

-   PDF parsing,
-   multi-column extraction,
-   table handling,
-   formula extraction,
-   clause-aware processing.

------------------------------------------------------------------------

## Deployment

The presentation identifies:

-   Docker
-   Google Cloud Run
-   containerized/serverless deployment

as part of the technical/deployment approach.

------------------------------------------------------------------------

# 🔐 Security, Auditability and Data Integrity

The presentation identifies data security and auditing as an important
challenge.

The proposed strategies include:

-   role-based access control (RBAC),
-   tamper-evident logs,
-   query tracking,
-   source metadata,
-   version control for standards.

The intended architecture therefore treats regulatory answers as
traceable information rather than opaque chatbot output.

------------------------------------------------------------------------

# ⚠️ Challenges and Mitigations

  -----------------------------------------------------------------------
  Challenge                           Proposed Strategy
  ----------------------------------- -----------------------------------
  AI hallucination                    Verified RAG with mandatory
                                      standard, clause, and source
                                      metadata

  Complex PDFs                        Layout-aware document parsing

  Tables/formulas/diagrams            Smart parsing preserving document
                                      structure

  Changing regulations                Gazette monitoring + version
                                      control

  Hinglish/regional ambiguity         Hybrid multilingual semantic +
                                      exact retrieval

  Data security                       RBAC + tamper-evident audit logs

  Outdated standards                  Active/superseded version tracking
  -----------------------------------------------------------------------

### Hallucination control

The project specifically proposes a **dual-pass validation / grounding
approach** in which responses must be connected to retrieved standard
and source metadata.

This is particularly important for regulatory applications because a
fluent but unsupported answer can be more dangerous than an obviously
incomplete one.

------------------------------------------------------------------------

# 📈 Feasibility and Viability

The SIH presentation divides feasibility and viability into four areas.

## Technical feasibility

The proposed stack uses established components:

-   LlamaIndex
-   Qdrant
-   FastAPI
-   Gemini
-   Docling
-   containerized deployment

The presentation also proposes caching and hybrid retrieval for
performance.

## Operational feasibility

The intended interface is designed to have a low learning curve:

-   speak naturally,
-   upload a photo,
-   ask a question,
-   receive a grounded response.

The system is also proposed as either:

-   a standalone application, or
-   an integration with Manakonline.

## Economic viability

The presentation estimates potential MSME savings of
**₹50,000--₹2,00,000 per certification cycle** by reducing third-party
consultancy dependency.

This is a project estimate presented in the SIH deck, not an
independently verified market-wide figure.

## Scalability and maintenance

The proposed architecture supports:

-   cloud-native scaling,
-   background Gazette synchronization,
-   modular LLM/vision components,
-   containerized deployment,
-   automated knowledge updates.

------------------------------------------------------------------------

# 🌍 Impact and Benefits

The presentation identifies several intended impact areas.

### 🏭 Manufacturing and MSMEs

-   easier standard discovery,
-   reduced regulatory friction,
-   faster pre-audit preparation,
-   reduced dependence on routine consultancy.

### 🇮🇳 Make in India

The project aims to reduce regulatory discovery and compliance friction
for local manufacturers and startups.

### 🛡️ Public safety

The presentation connects better standards awareness and compliance with
improved safety for products such as electronics, toys, and appliances.

### 👥 Consumers

The system is designed to make product/mark verification more
accessible, including ISI, CRS, and HUID-related information.

### 🧪 Testing laboratories

The proposed geospatial lab finder can help connect testing requirements
with relevant NABL/BIS-accredited laboratories.

### 🏢 BIS operations

Automating repetitive questions can reduce routine helpdesk workload and
allow staff to focus on more specialized activities.

------------------------------------------------------------------------

# 🗺️ Implementation Roadmap

The presentation proposes three broad phases.

## Phase 1: Foundation & Core RAG Pipeline

-   ingest 150+ key IS/QCO documents,
-   build clause-level RAG indexing,
-   launch citation-backed chat interface.

## Phase 2: Domain & Multilingual Support

-   add laboratory tools,
-   multilingual queries,
-   pre-audit checklists,
-   compliance scoring.

## Phase 3: Enterprise & Nationwide Scale

-   automated updates,
-   Manakonline integration,
-   administration tools,
-   audit logs,
-   cloud deployment.

``` mermaid
timeline
    title MANAK AI Implementation Roadmap
    Phase 1 : Foundation
            : Core RAG pipeline
            : 150+ key IS/QCO documents
            : Citation-backed chat
    Phase 2 : Domain Expansion
            : Lab finder
            : Multilingual support
            : Pre-audit checklists
            : Compliance scoring
    Phase 3 : Enterprise Scale
            : Gazette automation
            : Manakonline integration
            : Admin tools
            : Audit logs
            : Cloud deployment
```

------------------------------------------------------------------------

# 🔄 End-to-End Project Workflow

``` mermaid
flowchart TD
    U["User"] --> I{"Input Type?"}

    I -->|Text| T["Text Query"]
    I -->|Voice| V["Voice Query"]
    I -->|Image| P["Product / Label Image"]

    T --> R["Intent Router"]
    V --> R
    P --> R

    R --> S["Relevant Service"]

    S --> Q["Hybrid Retrieval"]
    Q --> D["BIS / Standards Knowledge Base"]
    Q --> L["Lab / Registry Data"]

    D --> C["Context Assembly"]
    L --> C

    C --> G["Gemini Reasoning"]
    G --> X["Grounding / Validation"]

    X --> A["Verified Answer"]
    X --> Z["Clause Citation"]
    X --> H["Checklist / Action"]
    X --> N["Lab Suggestion"]
```

------------------------------------------------------------------------

# 🖥️ User Experience Concept

The presentation depicts a user-facing interface containing elements
such as:

-   conversational search,
-   visual product scanning,
-   PDF/standard preview,
-   readiness information,
-   compliance assistance,
-   citation-backed answers.

The intended experience is:

``` text
ASK
 │
 ├── "What standard applies to my product?"
 ├── "Check this product label."
 ├── "Which tests are required?"
 ├── "How ready is my factory?"
 └── "Find an accredited lab near me."
 │
 ▼
UNDERSTAND
 │
 ▼
RETRIEVE
 │
 ▼
VERIFY
 │
 ▼
EXPLAIN
 │
 ▼
ACT
```

------------------------------------------------------------------------

# 🧪 Example Interaction

### Example: Manufacturer asks about a product

**User**

> "I manufacture this electrical product. Which Indian Standard applies
> and what tests do I need?"

**MANAK AI pipeline**

1.  Identify the product/query intent.
2.  Retrieve relevant standards.
3.  Match exact clauses and technical requirements.
4.  Assemble the relevant evidence.
5.  Use Gemini for explanation.
6.  Return a plain-language answer.
7.  Attach the relevant standard/clause metadata.
8.  Generate an actionable checklist.
9.  Identify relevant testing requirements.
10. Suggest appropriate nearby laboratories where the required data is
    available.

This illustrates the project's main philosophy:

> **From regulatory document → to understandable answer → to practical
> action.**

------------------------------------------------------------------------

# 📦 Suggested Repository Structure

The SIH presentation does not specify the exact source-code repository
structure. For implementation, a structure consistent with the
architecture could look like:

``` text
manak-ai/
│
├── frontend/
│   ├── app/
│   ├── components/
│   └── public/
│
├── backend/
│   ├── api/
│   ├── routers/
│   ├── services/
│   └── models/
│
├── rag/
│   ├── ingestion/
│   ├── parsing/
│   ├── retrieval/
│   └── indexing/
│
├── data/
│   ├── standards/
│   ├── qcos/
│   └── metadata/
│
├── scripts/
│   └── gazette_sync/
│
├── docs/
│
├── Dockerfile
├── README.md
└── .env.example
```

> **Note:** This is a recommended documentation-oriented structure, not
> a claim about the actual repository structure. The supplied SIH deck
> does not provide the project's source tree.

------------------------------------------------------------------------

# 🛠️ Technology Stack

  Layer                  Technology
  ---------------------- ---------------------------------------
  Frontend               Next.js 14, React
  UI                     Tailwind CSS, shadcn/ui
  Backend                Python, FastAPI
  Streaming              Server-Sent Events (SSE)
  LLM                    Google Gemini API
  RAG Framework          LlamaIndex
  Vector Database        Qdrant
  Retrieval              Dense Vector + BM25 + Payload Filters
  Document Parsing       Docling / LlamaParse
  Containerization       Docker
  Cloud Deployment       Google Cloud Run
  Regulatory Sources     BIS, e-Gazette
  Laboratory Ecosystem   NABL / BIS-accredited labs

------------------------------------------------------------------------

# 📚 Research and References

The SIH presentation references the following resources:

1.  **Bureau of Indian Standards Act, 2016 & Conformity Assessment
    Regulations**
2.  **Official Gazette of India / e-Gazette**
3.  **National Accreditation Board for Testing and Calibration
    Laboratories (NABL)**
4.  **LlamaIndex Data Framework Documentation**
5.  **Qdrant Vector Database Documentation**
6.  **Robertson, S. & Zaragoza, H. (2009), "The Probabilistic Relevance
    Framework: BM25 and Beyond"**

Relevant official/technical links supplied in the presentation:

-   BIS:
    https://www.bis.gov.in/the-bureau/bis-act-rules-and-regulations/
-   e-Gazette: https://egazette.gov.in/
-   NABL: https://nabl-india.org/
-   Qdrant: https://qdrant.tech/documentation/
-   LlamaIndex: https://developers.llamaindex.ai/python/framework/

------------------------------------------------------------------------

# 🚀 Prototype

The SIH presentation provides the following prototype URL:

**https://manak-8frzfvny3-rushliners.vercel.app/**

The deck also references a video explanation, but no video URL is
supplied in the extracted presentation content.

------------------------------------------------------------------------

# 📋 Project Scope Notes

This README is derived from the **six-page SIH 2026 presentation
supplied with the project**.

The presentation clearly specifies the proposed architecture, features,
technology stack, risks, benefits, and implementation roadmap. It does
**not** provide all repository-level implementation details, such as:

-   exact source-code modules,
-   database schema,
-   API endpoint specifications,
-   environment variables,
-   authentication implementation details,
-   exact compliance-score formula,
-   exact retrieval hyperparameters,
-   exact chunking strategy,
-   automated test suite,
-   CI/CD configuration,
-   production deployment configuration.

Those details should be added here when the actual source repository is
available.

------------------------------------------------------------------------

# 🧭 Development Checklist

For a production implementation, the following areas should be
explicitly documented and tested:

-   [ ] BIS/IS document ingestion
-   [ ] QCO ingestion
-   [ ] Layout-aware PDF parsing
-   [ ] Clause-level metadata
-   [ ] Dense vector indexing
-   [ ] BM25 indexing
-   [ ] Metadata filtering
-   [ ] RAG citation generation
-   [ ] Response grounding validation
-   [ ] Hindi/Hinglish support
-   [ ] Regional language handling
-   [ ] Voice input pipeline
-   [ ] Product image analysis
-   [ ] Compliance checklist generation
-   [ ] Readiness scoring rules
-   [ ] Laboratory matching logic
-   [ ] e-Gazette monitoring
-   [ ] Version control for regulatory documents
-   [ ] RBAC
-   [ ] Audit logs
-   [ ] Monitoring and observability
-   [ ] Automated tests
-   [ ] Production deployment

------------------------------------------------------------------------

# 🏁 Conclusion

**MANAK AI** is designed as more than a conventional chatbot.

Its architecture combines **multimodal interaction + regulatory document
retrieval + hybrid search + grounded generation + compliance workflows**
into a single assistant focused on Indian Standards and BIS services.

The key architectural principle is:

``` text
        KNOWLEDGE
            +
       RETRIEVAL
            +
        GROUNDING
            +
        REASONING
            +
        ACTION
            ↓
       MANAK AI
```

The project aims to turn standards from documents that users must hunt
through into information they can **ask for, verify, understand, and act
upon**.

------------------------------------------------------------------------

## 👥 Team

**Team:** RUSHLINERS

**Hackathon:** Smart India Hackathon 2026

**Problem Statement:** SIH26107

**Theme:** Smart Automation

**Category:** Software

------------------------------------------------------------------------

> Built for the Smart India Hackathon 2026 · MANAK AI · RUSHLINERS
