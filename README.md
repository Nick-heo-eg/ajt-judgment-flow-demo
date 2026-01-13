# AJT Judgment Flow Demo

**Status**: Non-normative / Educational visualization

This repository demonstrates AJT (Audit Judgment Trail) judgment flow through visual diagrams.

**This is NOT a constitutional document.** For normative rules, see:
- [AJT Layer Architecture (Constitutional)](https://github.com/Nick-heo-eg/cognitive-infrastructure-constitution/blob/main/judgment/AJT_LAYER_ARCHITECTURE.md)

---

## Purpose

AJT is not a rule table. It is a flowing structure.

**This visualization shows:**
- How judgment traces move through 5 layers
- Where judgment and accountability separate
- Why Indeterminate is a terminal state
- What happens when Layer 5 is absent

**The key insight:**
> A judgment that doesn't reach Layer 5 (Accountability) has no effect on reality.

---

## Basic Flow Diagram

```mermaid
graph TD
    Start([Request]) --> L1[L1: Process Control]

    L1 -->|Allow| L2[L2: Safety Gate]

    L2 -->|Allow| L3[L3: Evidence]
    L2 -->|Hold| L3
    L2 -->|Stop| L3

    L3 -->|Sufficient| L4[L4: Judgment]
    L3 -->|Insufficient| L4

    L4 -->|Stop| L5[L5: Accountability]
    L4 -->|Allow| L5
    L4 -->|Indeterminate| End_Ind([Terminal])

    L5 --> Exec[Execution]

    style L4 fill:#f9f,stroke:#333,stroke-width:4px
    style L5 fill:#9ff,stroke:#333,stroke-width:4px
    style End_Ind fill:#ff9,stroke:#333,stroke-width:2px
```

---

## Key Visualization Principles

### 1. Layer 4 is the Branching Point

```mermaid
graph LR
    L4[L4: Judgment] --> Stop
    L4 --> Allow
    L4 --> Indeterminate

    Stop --> L5[L5]
    Allow --> L5
    Indeterminate --> Terminal([Terminal])

    style L4 fill:#f9f
    style Terminal fill:#ff9
```

**What this shows:**
- Stop/Allow continue to Layer 5
- Indeterminate terminates immediately
- No automatic retry from Indeterminate

---

### 2. Judgment Without Accountability Has No Effect

```mermaid
graph TD
    L4_Stop[L4: Stop] -.->|No L5| NoEffect([No Block])
    L4_Stop -->|With L5| L5[L5: Accountability]
    L5 --> Block[Block Effect]

    style NoEffect fill:#fcc,stroke-dasharray: 5 5
    style Block fill:#cfc
```

**What this shows:**
- A Stop judgment alone does not block
- Layer 5 (Accountability) must execute
- If Layer 5 fails, the entire operation fails

---

### 3. Indeterminate is Complete, Not Incomplete

```mermaid
graph LR
    Insufficient[L3: Insufficient] --> L4[L4]
    L4 --> Indeterminate([Indeterminate])

    Indeterminate -.->|❌ No Retry| X1[X]
    Indeterminate -.->|❌ No Implicit Allow| X2[X]
    Indeterminate -.->|❌ No Escalate| X3[X]

    Indeterminate -->|✅ Human Required| Human[Human Decision]

    style Indeterminate fill:#ff9
    style X1 fill:#fcc
    style X2 fill:#fcc
    style X3 fill:#fcc
    style Human fill:#cfc
```

**What this shows:**
- Indeterminate is a formal judgment result
- It is terminal (no automatic continuation)
- Human intervention is required

---

### 4. State Language by Layer

```mermaid
graph TD
    L1[L1: Process<br/>Allow / Pause] --> L2[L2: Gate<br/>Stop / Hold / Allow]
    L2 --> L3[L3: Evidence<br/>Sufficient / Insufficient]
    L3 --> L4[L4: Judgment<br/>Stop / Allow / Indet]
    L4 --> L5[L5: Accountability<br/>Logs Only]

    style L1 fill:#e1f5e1
    style L2 fill:#ffe1e1
    style L3 fill:#e1e1ff
    style L4 fill:#f9f
    style L5 fill:#9ff
```

**What this shows:**
- Each layer has fixed state language
- Hold appears only in Layer 1, 2
- Indeterminate appears only in Layer 4
- Layer 5 has no state language (logs only)

---

## External Exposure vs Internal States

```mermaid
graph TD
    subgraph External["External (API/UI)"]
        Ext_Stop[Stop]
        Ext_Allow[Allow]
        Ext_Indet[Indet]
    end

    subgraph Internal["Internal Only"]
        Int_Pause[Pause]
        Int_Hold[Hold]
        Int_Suff[Sufficient]
        Int_Insuff[Insufficient]
    end

    L4[L4] --> Ext_Stop
    L4 --> Ext_Allow
    L4 --> Ext_Indet

    L1[L1] -.-> Int_Pause
    L2[L2] -.-> Int_Hold
    L3[L3] -.-> Int_Suff
    L3 -.-> Int_Insuff

    style External fill:#cfc
    style Internal fill:#fcc
```

**What this shows:**
- Only Layer 4 states are exposed externally
- Hold/Pause are internal only
- Users see only Stop/Allow/Indeterminate

---

## What This Visualization Is NOT

This repository does NOT contain:
- ❌ Constitutional rules
- ❌ Normative specifications
- ❌ Implementation requirements
- ❌ Executable code

This repository DOES contain:
- ✅ Educational diagrams
- ✅ Flow visualizations
- ✅ Conceptual demonstrations
- ✅ Teaching materials

---

## Constitutional Authority

All normative rules are defined in:
- [AJT Layer Architecture](https://github.com/Nick-heo-eg/cognitive-infrastructure-constitution/blob/main/judgment/AJT_LAYER_ARCHITECTURE.md)

If any visualization conflicts with the constitution, the constitution prevails.

---

## Related Resources

- [AJT Explanatory Docs](https://github.com/Nick-heo-eg/ajt-explanatory-docs) — Why judgment and accountability are separated
- [Judgment Experiment Logs](https://github.com/Nick-heo-eg/judgment-experiment-logs) — Case studies

---

## Future Enhancements

**Phase 2 (Planned):**
- Interactive D3.js animation showing token movement
- Step-by-step judgment trace visualization
- Layer-by-layer state transitions with timing

**Principle:**
> AJT is not a table to read. It is a flow to watch.

---

**Last Updated**: 2026-01-13
**Repository Type**: Non-normative educational visualization
