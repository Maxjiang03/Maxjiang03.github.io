---
title: "Hierarchical Detection of Malicious Command Lines Using Random Forest and Context-Aware LSTM"
collection: publications
permalink: /publication/2026-hierarchical-malicious-command-lines
date: 2026-05-01
venue: "Cyber Science 2026"
status: "Accepted"
excerpt: "**[Accepted — to appear, Cyber Science 2026]** Yixian Jiang and Qinzheng Hu (equal contribution), with Pavandeep Singh Baxi. A hierarchical framework combining feature-based machine learning with sequence-aware LSTM modeling — Random Forest is strongest for single-command detection, while RF+LSTM is best for command-stream (multi-step) detection."
paperurl: "/files/jiang2026-hierarchical-command-detection.pdf"
codeurl: ""
citation: 'Yixian Jiang, Qinzheng Hu, Pavandeep Singh Baxi. "Hierarchical Detection of Malicious Command Lines Using Random Forest and Context-Aware LSTM." Cyber Science 2026. (Yixian Jiang and Qinzheng Hu contributed equally.)'
---

**Yixian Jiang**, Qinzheng Hu, Pavandeep Singh Baxi — School of Computing Science, University of Glasgow.
*Yixian Jiang and Qinzheng Hu contributed equally to the manuscript.*

Accepted at **Cyber Science 2026** (to appear). The paper proposes a hierarchical framework for
detecting malicious command-line activity that combines feature-based machine learning with
sequence-aware (LSTM) modeling within a single evaluation setting. At the single-command level it
compares rule-based detection, a hybrid logistic-regression classifier, and a random forest over a
shared 172-dimensional feature representation; at the sequence level these models are extended with
LSTM-based context modeling. Random forest gives the strongest single-command performance, while the
RF+LSTM model performs best for command-stream analysis of multi-step behaviour. The system is
implemented as a Rust-based prototype with lightweight deobfuscation and feature extraction.

<!-- TODO: add codeurl once a public repository exists; do not invent a URL. -->
