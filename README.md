<div align="center">
  <img src="./logo.png" alt="Logo Alt Text" width="200" />
</div>

# z0L Security Audit Portfolio

Welcome to my **Web3 security audit portfolio**, a collection of my independent audits, contest submissions, and research write-ups.

Each entry documents findings, proof-of-concepts, and mitigation recommendations with professional formatting and reproducible tests.

---

## 🧩 Contest Findings

| Title | Platform | Severity | Status | Link |
|-------|-----------|-----------|--------|------|
| `Float128::toPackedFloat` Fails to Promote to L Size When Exponent Is Critically Low | Code4rena – Forte: Float128 Solidity Library | High | ✅ **Valid (Rewarded)** | [View Report](https://github.com/z0Ld3v/z0L-audits/blob/main/audit-contests/Code4rena/2025-04-forte-float128-solidity-library/finding1.md) |
| `Ln::ln()` Fails to Validate Negative Inputs, Causing Division-by-Zero Panics | Code4rena – Forte: Float128 Solidity Library | High | ✅ **Valid (Rewarded)** | [View Report](https://github.com/z0Ld3v/z0L-audits/blob/main/audit-contests/Code4rena/2025-04-forte-float128-solidity-library/finding2.md) |
| Unauthorized Token Transfer via Insufficient Access Control | Sherlock – Crestal Network | Medium | ⚠️ **Valid (No Reward)** | [View Report](https://github.com/z0Ld3v/z0L-audits/blob/main/audit-contests/Sherlock/2025-03-crestal-network/unauthorized-token-transfer.md) |

---

## 🚧 Practice & False-Positives

| Title | Platform | Status | Link |
|--------|-----------|--------|------|
| Reward Manipulation in Referral Logic | Code4rena – Nudge | ❌ **Invalid (Intended Behavior)** | [View Report](https://github.com/z0Ld3v/z0L-audits/blob/main/practice-audits/false-positives/code4rena/2025-03-nudge/rewardmanipulation.md) |

Even invalid or duplicate findings are kept here for **transparency and learning value**.

Every false positive sharpens reasoning and pattern recognition.

---

## 🔍 My Audit Process

1. **Recon & Surface Mapping** – Identify actors, roles, trust boundaries  
2. **Code Reading & Control Flow** – Trace key invariants, modifiers, and permission logic  
3. **Access Control & Auth Checks** – Verify function visibility, role dependencies  
4. **Math, Precision & Overflow** – Detect unsafe arithmetic, rounding drift, or precision mismatches  
5. **External Calls & Reentrancy** – Locate potential unsafe calls, pull vs. push payment patterns  
6. **State Management & Edge Cases** – Simulate abnormal flows (late joins, zero values, skipped states)  
7. **Testing & PoCs** – Reproduce behavior via Foundry, Anvil fork, or minimal Solidity harness  
8. **Impact Analysis & Recommendations** – Evaluate severity, realism, and potential mitigations  

---

## 📚 Current Focus

- Rebuilding deep audit workflow using Foundry invariant testing  
- Studying high-impact DeFi exploits and real audit reports  
- Preparing for upcoming contests  
- Writing concise, reproducible case studies for each finding

---

## 👤 About

I’m **Z**, a Web3 security researcher and Solidity developer with a focus on precision math, access control, and protocol-level logic flaws.  
I audit for correctness, realism, and economic resilience, not just syntax.

---

## 🛠️ Contact

- **Twitter/X:** [@z0ls3c](https://x.com/z0Ld3v)
- **Email:** <a href="mailto:z0ls3c@proton.me">Proton</a>

---
