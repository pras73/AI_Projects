An end-to-end, privacy-preserving NLP pipeline designed to detect online grooming, predatory behavior, and cyberbullying across live, multi-turn chat environments.

Traditional moderation systems rely on static keyword blacklists or single-turn text classifiers. These approaches fail to capture gradual manipulative behavior (grooming) and context-dependent harassment, while often logging sensitive user data. This pipeline addresses these limitations using a privacy-first PII scrubbing layer, a fine-tuned Transformer model, and a sliding-window context engine that evaluates rolling conversation histories.

Key Features

Privacy-Preserving PII Redaction Engine: Automatically scrubs Personally Identifiable Information (PII)—including person names, locations, phone numbers, emails, and physical addresses—using spaCy Named Entity Recognition (NER) and high-speed regular expressions before model inference or logging (COPPA-compliant design).

Multi-Class Transformer Classifier: Fine-tuned lightweight Transformer (DistilBERT / DeBERTa) optimized for low-latency multi-class safety categorization:

0: SAFE

1: CYBERBULLYING

2: GROOMING_PREDATORY

Context-Aware Sliding Window: Tracks user state over time using a rolling window queue. It calculates exponential moving averages for risk scores to catch multi-turn manipulation tactics that bypass single-turn filters.

 Multi-Tier Risk Escalation: Generates structured, prioritized ThreatAlert objects categorized across four severity levels (LOW, MEDIUM, HIGH, CRITICAL) with confidence scores and context snapshots.
