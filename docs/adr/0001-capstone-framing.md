# ADR-0001: Capstone Framing — Bank Policy Q&A Assistant

- **Status:** Draft v1
- **Date:** 2026-11-19
- **Author:** Maruthi Prasad

## Context

Bank employees and customers need a straightforward way to find and understand information in bank policies without searching lengthy documents manually. This capstone will explore a retrieval-augmented assistant that answers questions using a policy corpus that will be generated later with help from an LLM; generated documents are a prototype dataset and must not be treated as authoritative bank policy.

## Decision — Solution Framing Canvas

| Box | Your answer |
|-----|-------------|
| **Inputs** | A user submits a natural-language question, and the system uses the generated bank-policy documents as its reference corpus. |
| **Outputs** | The system returns a concise answer grounded in retrieved policy passages, with citations to the source documents, or says when it cannot find sufficient support. |
| **Tools** | The system uses an LLM to draft answers, a retriever and vector store to find relevant policy passages, and a document-ingestion process to index the corpus. |
| **Memory** | The system does not retain conversation history between sessions; it uses only the current question and indexed policy corpus to produce an answer. |
| **Autonomy level** | This is a question-answering assistant, not an agent: it retrieves and explains policy but does not take actions or make decisions on a user's behalf. |
| **Decision boundaries** | It may summarize retrieved policy text, but must not invent policy, determine a person's eligibility, approve or deny requests, or perform banking actions; unsupported or consequential questions require human review. |

## Consequences

- **Positive:**
  - Users can find relevant policy information without manually searching every document.
  - Citations and an explicit fallback for unsupported questions make answers easier to verify.
  - Keeping the system read-only limits the impact of incorrect answers.
- **Negative / risks:**
  - LLM-generated policy documents may contain inaccuracies or omit important real-world requirements, so answers are only as trustworthy as this prototype corpus.
  - Retrieval can miss relevant passages, and the LLM can still misstate them; citations do not guarantee correctness.
  - Building and evaluating document ingestion, retrieval, and grounded answers adds complexity compared with a general-purpose chatbot.
- **Things we'll re-visit:**
  - How the corpus will be reviewed, versioned, and replaced with authoritative policies if the prototype moves beyond experimentation.
  - What evaluation and human-review rules are needed before anyone could rely on answers in a real banking setting.