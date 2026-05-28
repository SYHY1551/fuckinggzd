---
name: fuckinggzd
description: Use when working with Chinese thesis AIGC detection reports from GZD/格子达: analyze report hits, infer high-risk writing patterns, generate generic replacement passages, or apply quality-preserving revisions to DOCX while avoiding document-specific leakage.
---

# fuckinggzd

Use this skill for Chinese academic papers when the user provides a GZD/格子达 AIGC report and asks to analyze, reduce template-like writing, generate replacement passages, or apply revisions to a manuscript.

## Core stance

- Treat the task as improving thesis prose so it reads like a real project report, not as promising a detector score.
- Do not use hidden text, white text, tiny font, image-based正文, metadata tricks, or other formatting manipulation.
- Do not invent experiments, parameters, citations, formulas, devices, or conclusions.
- Preserve technical terms, numbers, units, formulas, figure/table references, citation numbers, and chapter logic.
- Default to producing a TXT replacement list. Edit DOCX only when the user explicitly provides a target DOCX and asks for direct application.

## Workflow

1. Read the report PDF and extract:
   - overall AIGC rate, risk level, suspected片段 count;
   - high/medium/low risk distribution;
   - each reported passage and any page/sequence number available.
2. If prior reports or rewritten TXT/DOCX versions are available, compare them:
   - identify which passages disappeared;
   - identify which passage types still trigger;
   - separate effective changes from changes that merely shifted wording.
3. Classify each hit before rewriting:
   - algorithm/theory explanation;
   - hardware signal chain;
   - software流程 or interrupt/buffer logic;
   - summary/conclusion;
   - literature/background;
   - formula/table/figure lead-in.
4. Rewrite according to class, then check quality and consistency.
5. Output either:
   - report analysis only, or
   - `【替换项XX】/定位/替换为` TXT-style entries, or
   - a revised DOCX plus a backup path if direct application was requested.

## Effective rewrite pattern

Use low-compression, coarse-grained, human project-report wording:

- Replace overly polished academic compression with slightly looser explanation.
- Add moderate connecting words such as `在实际处理时`, `从本设计来看`, `这里主要考虑`, `这样处理以后`, but vary them.
- Break perfect parallelism and avoid every paragraph following the same structure.
- Convert generic definitions into project-specific use:
  - less `X是一种...其优点是...因此本文选择...`;
  - more `本设计遇到的问题是...该方法在这里主要用来...实际限制在于...`.
- Keep some natural imperfection in rhythm, but do not make the thesis unprofessional.
- Prefer concrete implementation context over broad claims.

## Passage strategies

### Algorithm and theory

- Reduce textbook-style definitions.
- Keep only the part needed to explain why the method is referenced, rejected, or used.
- Preserve formulas and citation numbers exactly.
- Mention actual constraints when present in the manuscript: sampling rate, search range, buffer length, processor resources, signal characteristics, or threshold choices.

### Hardware

- Avoid pure component inventory.
- Describe how the signal moves and why each module is needed.
- Keep pin names, chip names, voltages, addresses, and bus/interface names unchanged.

### Software

- Avoid long `first/then/finally` procedure chains.
- Use event-driven wording around timer triggers, ADC conversion, DMA half/full callbacks, frame buffers, boundary checks, and display refresh.
- Keep variable names, frame lengths, interrupt names, and state flags if they already exist in the manuscript.

### Summary and background

- Reduce sweeping conclusions such as `具有重要意义`, `奠定基础`, `能够满足需求`, unless the paper already requires them.
- Prefer specific engineering outcomes and remaining limitations.
- Avoid making every paragraph end with a perfect conclusion sentence.

## Output rules

- For TXT replacement output:
  - use `【替换项XX】`;
  - include `定位：` when a section or first sentence is known;
  - include `替换为：` with copy-ready text;
  - do not include commentary inside the replacement text.
- For DOCX application:
  - create a timestamped backup first;
  - replace only mapped passages unless the user asks for broader restructuring;
  - verify paragraph count, key terms, citation numbers, and obvious leftover duplicates;
  - render or structurally inspect the DOCX when feasible.

## Quality checks

Before finalizing, verify:

- no technical data, units, formulas, or citations were lost;
- Chinese and English/digits spacing matches the user's requested style;
- no new experiment, result, or unsupported claim was introduced;
- no repeated or残缺 sentence remains;
- no specific paper title, author, school, report ID, score, or original passage is included in reusable skill files.

## Detector-inference notes

Common high-risk patterns in GZD-style reports:

- long, smooth, complete paragraphs with a `background -> method -> effect -> conclusion` arc;
- `definition -> advantages -> limitations -> selection` algorithm blocks;
- hardware流水账 that lists modules in a uniform chain;
- software流程 that reads like generated pseudocode prose;
- highly consistent paragraph rhythm across many sections;
- repeated or stitched-together text.

Effective reductions usually come from changing paragraph structure and compression level, not from synonym replacement alone.
