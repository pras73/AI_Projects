Summary
The Multimodal Clinical Decision Support System (CDSS) is a real-time healthcare agent engineered for emergency room triage and clinical risk stratification. It processes three distinct data modalities simultaneously:

Numerical Physiological Vitals: Evaluated deterministically via the National Early Warning Score (NEWS2).

Unstructured Narrative Complaints: Queried against evidence-based medical guidelines using Retrieval-Augmented Generation (RAG).

Medical Imagery: Analyzed via computer vision models to caption visual findings.

Why This Architecture Matters
Standard Large Language Models (LLMs) frequently hallucinate when evaluating numerical thresholds or doing arithmetic. In healthcare, a miscalculated score can lead to improper triage.

This project solves that problem through a Hybrid AI Pattern:

Deterministic Engine: Handles vital sign scoring and hardcoded safety red-flags via explicit Python algorithms.

Generative & Retrieval Pipelines: Handles semantic literature searching (ChromaDB) and visual feature analysis (Transformers).


 In-Depth Component Explanations
 A. The NEWS2 Vitals Engine (calculate_news_score)
 Purpose: Provides non-hallucinatory risk scoring.Mechanism: Checks numeric vital inputs against hardcoded clinical thresholds established by the National Health Service (NHS) NEWS2 framework.Why Python instead of an LLM prompt? LLMs struggle with multi-step range evaluations. Pure Python guarantees 100% mathematical determinism.
 B. Vector Database Retrieval (vector_db)
 Purpose: Ingests unstructured chief complaints and fetches exact medical protocols.Mechanism: Converts clinical text into 384-dimensional dense vectors using all-MiniLM-L6-v2. Performs cosine similarity search inside ChromaDB.
 Benefit: Ensures that clinical recommendations are grounded directly in vetted medical literature rather than generative model memory.
 C. Vision Transformer Pipeline (vision_analyzer)
 Purpose: Inspects uploaded medical scans or clinical photographs.
 Mechanism: Uses the Salesforce/blip-image-captioning-base multimodal architecture to generate descriptive text representations of input images.
 D. Red-Flag Safety Intercepts
 Purpose: Prevents high-risk patients from being downgraded by language synthesis.
 Mechanism: Scans inputs for critical bounds. If triggered, forces priority escalation and displays explicit alert badges.
