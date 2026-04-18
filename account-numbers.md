# Karbo Account Numbers (H–I–C)

## Overview

Karbo introduces **short account numbers** as a usability layer on top of standard CryptoNote addresses.

Instead of sharing long base58 addresses, users can register a compact identifier of the form:
```
H-I-C
```

Where:
- **H** — block height containing the registration transaction  
- **I** — transaction index within the block (non-zero; coinbase excluded)  
- **C** — Luhn checksum digit for error detection  

This creates a **deterministic, human-friendly reference** to a blockchain-anchored address.

---

## Motivation

CryptoNote addresses are:
- Long and error-prone  
- Difficult to communicate verbally or visually  
- Inconvenient for repeated use  

Account numbers solve this by providing:
- Short, structured identifiers  
- Built-in typo detection (Luhn check)  
- Deterministic lookup via blockchain data  

Importantly, this system does **not replace addresses**, but acts as a **reference layer**.

---

## Registration Mechanism

To obtain an account number, a user submits a **registration transaction** containing their standard Karbo address.

Once included in a block:

- The transaction’s **block height (H)** and **index (I)** are fixed  
- The **account number is derived deterministically**
- A **Luhn checksum (C)** is appended for validation  

### Properties

- One registration → one account number  
- Multiple registrations → multiple account numbers (same address possible)  
- No central registry or naming authority  

---

## Resolution Process

When a wallet receives an account number:

1. Parse `(H, I, C)`
2. Validate checksum `C`
3. Retrieve block at height `H`
4. Extract transaction at index `I`
5. Read embedded address from registration transaction  

The result is the **original Karbo address**.

---

## Security Model

### Blockchain Anchoring

Account numbers inherit security from:
- Proof-of-Work consensus  
- Block immutability over time  

However, they rely on **probabilistic finality**.

---

### Reorganization Risk

Short account numbers are derived from block position, not from cryptographic commitment alone.

In rare cases, a blockchain reorganization may:
- Replace a recent block  
- Insert a different transaction at the same `(H, I)` position  

This could result in:

> The same account number temporarily resolving to a different address.

This is not a flaw in implementation, but a consequence of decentralized consensus.

---

## Finality Recommendations

To mitigate reorg-related risks:

### Confirmation Policy

- **Low-value use:** ≥ 10 confirmations  
- **High-value use:** ≥ 20–60 confirmations  

Until then, account numbers should be treated as **not yet final**.

---

### Usage Guidelines

- Do not publish newly created account numbers immediately  
- Prefer reusing established numbers  
- Verify resolved address for high-value transfers  
- Monitor for unexpected resolution changes shortly after registration  

---

## Fraud Considerations

An attacker could theoretically:
1. Observe a freshly registered account number  
2. Exploit a short reorg window  
3. Replace the original registration with their own  

This attack is:
- Time-limited (only during early confirmations)  
- Computationally expensive  
- Detectable with standard confirmation practices  

Following confirmation guidelines effectively mitigates this risk.

---

## Advantages

- Human-readable identifiers  
- No additional infrastructure required  
- Fully on-chain and deterministic  
- Compatible with existing CryptoNote model  

---

## Limitations

- Not instantly final  
- Requires blockchain lookup  
- No inherent name semantics (numeric only)  

---

## Conclusion

Karbo account numbers provide a **practical usability improvement** without compromising decentralization.

They strike a balance between:
- Human-friendly interaction  
- Trustless blockchain verification  

When used with proper confirmation awareness, they are a **safe and effective abstraction layer** over standard addresses.

See detailed [Paper on Karbo Account Numbers](Karbo_Account_Numbers.pdf)