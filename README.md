# Claude Code Report: Unclonable Encryption Research

This repository contains two research reports on **unclonable encryption** — a quantum cryptographic primitive that uses the quantum no-cloning theorem to produce ciphertexts that cannot be duplicated for two independent decryptors.

## Reports

### 1. [Thesis Directions in Unclonable Encryption: Five Research Frontiers](./claude_report_with_research_directions.md)

A detailed analysis of five open research directions suitable for thesis work, covering:

- Defining a public-key analog of the fake-key property
- The evolution of unclonable encryption from 2020 to 2026
- The unexplored triangle connecting fake-key, non-committing encryption, and quantum deniability
- Unclonable functional encryption (Mehta-Müller 2024)
- The one-to-many fake-key generalization

### 2. [Unclonable Encryption and the Elusive Public-Key Fake-Key Property](./public_key_encryption_with_fake-key_property_report.md)

A focused survey on why the fake-key property (Ananth-Kaleoglu, TCC 2021) has not been extended to the public-key setting, including:

- The structural barrier between private-key and public-key fake-key constructions
- A chronological map of progress from 2021 to 2026
- Classical equivocality notions (lossy encryption, dual-mode encryption, somewhere equivocal encryption) and their roles in UE proofs
- What a public-key fake-key property would require

## Background

The fake-key property allows an efficient algorithm to produce a fake decryption key that makes a real ciphertext decrypt to any chosen message, indistinguishable from a genuine key-ciphertext pair. Introduced by Ananth and Kaleoglu (TCC 2021), it remains the central open challenge in public-key unclonable encryption — no construction achieves public-key UE through a direct fake-key argument without heavy machinery such as functional encryption or indistinguishability obfuscation.

Recent landmarks include the unconditional existence of an uncloneable bit (Bhattacharyya, Broadbent, and Culf, March 2026) and the first multi-copy secure unclonable encryption (Çakan et al., 2025).

## Generated with

[Claude Code](https://claude.ai/code) — reports generated via the Claude API (claude-sonnet-4-6).
