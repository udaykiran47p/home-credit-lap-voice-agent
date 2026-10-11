# Home Credit Loan Against Property (LAP) — AI Voice Agent

An automated, telephony-first AI Voice Agent built for **Home Credit** to qualify existing customers for a pre-approved Loan Against Property (LAP) offer of up to ₹75,00,000 (75 Lakhs).

---

## 🎧 Live Test Calls & Public Audio Recordings

> **Note for Evaluators:** Click the links below to listen to the call recordings and view the aligned word-by-word transcripts directly on Retell AI.

| Scenario | Objective | Call Outcome | Public Recording Link (Audio + Transcript) |
| :--- | :--- | :--- | :--- |
| **Call 1: Golden Path** | Fully eligible customer answering all 7 criteria | **QUALIFIED** | [Listen to Call 1]([PASTE_RETELL_PUBLIC_LINK_1_HERE)](https://drive.google.com/file/d/1q-1fYwLD0CIrsarb_wXTXTwO39IXLWe7/view?usp=sharing) |
| **Call 2: Disqualification** | Agricultural farmland rejection | **DISQUALIFIED** | [Listen to Call 2]([PASTE_RETELL_PUBLIC_LINK_2_HERE])(https://drive.google.com/file/d/1LlKLf0sUqXl-oy8HtkHApgwk-bBff0-Z/view?usp=sharing) |
| **Call 3: Transfer Switch** | Existing loan balance transfer / EMI reduction | **TRANSFERRED** | [Listen to Call 3](PASTE_RETELL_PUBLIC_LINK_3_HERE) (https://drive.google.com/file/d/16w-FX1QKFl_QovWAphNN_9cSFxHz-iM_/view?usp=sharing)|
| **Call 4: Out-of-Order** | Multi-slot answers in a single utterance | **QUALIFIED** | [Listen to Call 4](PASTE_RETELL_PUBLIC_LINK_4_HERE) (https://drive.google.com/file/d/1wtzJxlGbxHDfnV8SaMsHKSqUguOLOx4I/view?usp=sharing)|

---

## 🏗️ Architecture & Business Logic

The agent is engineered as a **Finite State Machine (FSM)** with dynamic slot-filling and immediate boundary checks:

1. **Phase 0 — Identity & Name Discovery**:
   - The agent initiates the call by asking the customer's name.
   - Extracts and maintains the customer name in an internal JSON state object (`"customer_name": "<Name>"`).
   - Verifies customer availability (if busy, captures callback time and terminates).

2. **The 7 Qualification Gates**:
   - **Property Type**: Residential, Commercial, and Industrial are eligible. Agricultural properties trigger immediate polite disqualification.
   - **Ownership**: Sole and Joint ownership are eligible.
   - **Original Documents**: Mandatory to have physical originals; missing/disputed deeds cause immediate disqualification.
   - **Loan Amount**: Capped at ₹75 Lakhs. Requests above ₹75L trigger a negotiation rule offering the maximum ₹75L limit.
   - **Occupation & Income Mode**: Salaried and Self-Employed are eligible, but income must be documented via Bank deposit. Cash income causes immediate disqualification.
   - **Market Value**: Captures the customer's estimated property value.
   - **Tenure**: Strictly constrained between 3 and 15 years.

3. **Special Logic Switches**:
   - **Existing Loan / EMI Reduction**: Immediately switches out of the fresh loan flow to notify the customer that a specialized Loan Transfer team will call back.
   - **Zero Hallucination Guardrail**: The agent never invents interest rates or processing fees; it defers exact rates to the senior loan expert.
   - **Strict Handoff Gate**: The agent never announces qualification until all 7 criteria are verified.

---

## 📄 System Prompt
The production-ready prompt used for this agent is available at [`system_prompt.md`](./system_prompt.md).
