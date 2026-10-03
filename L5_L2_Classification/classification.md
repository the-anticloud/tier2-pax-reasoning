# L5 Narrow / L2 General Classification — PAX_REASONING
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Multi-hop reasoning and chain-of-thought module for PAX 27B

## L5 Narrow
PAX_REASONING operates at L5 Narrow within its specialized scope: multi-hop reasoning and chain-of-thought module for pax 27b.
It does not generalize outside this function. PAX 27B inference is scoped to this module's
specific input/output contract. All outputs are deterministically validated before AIOSS append.

## L2 General
PAX_REASONING is available to all 9 Anticloud deployment tiers. Any tier project that needs
multi-hop reasoning and chain-of-thought module for pax 27b capability calls PAX_REASONING without reconfiguration. Same API across all domains.

## PAX Integration
PAX 27B interfaces with PAX_REASONING as a specialized inference module. Inputs are preprocessed
to PAX_REASONING's schema, PAX generates outputs within that schema, and results are AIOSS-chained
before being returned to the calling module.

## AIOSS Audit Relevance
Every reasoning trace (premises hash + inference steps hash + conclusion hash + confidence) is appended to the AIOSS chain.
H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n)
Full reproducible audit trail, verifiable offline without cloud.

## Regulatory
NIST AI RMF 1.0 (explainability), ISO/IEC 42001 (transparent AI)
