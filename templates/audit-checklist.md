# 🧩 z0L Audit Checklist

A quick, repeatable checklist for static review + dynamic testing.

---

## 1️⃣ Recon & Context
- [ ] Identify protocol purpose and architecture
- [ ] Enumerate actors (owner, users, oracles, adapters, DAO, etc.)
- [ ] Map trust boundaries and value flows
- [ ] Note any upgradeable patterns or proxies

---

## 2️⃣ Code Structure
- [ ] Understand key inheritance and modifiers
- [ ] Verify constructor or initializer parameters
- [ ] Identify external integrations (price feeds, routers, etc.)
- [ ] Confirm compiler version and optimization flags

---

## 3️⃣ Access Control
- [ ] Are all privileged functions `onlyOwner` / `onlyRole` guarded?
- [ ] Are critical paths (mint/burn/withdraw) protected?
- [ ] Can ownership be renounced or transferred securely?
- [ ] Look for unguarded setters or external calls

---

## 4️⃣ Math & Accounting
- [ ] Any unchecked arithmetic or casting?
- [ ] Floating-point or precision logic (scaling, decimals)?
- [ ] Division or modulo by zero risk?
- [ ] Unbounded loops tied to user input?

---

## 5️⃣ State & Lifecycle
- [ ] Validate correct state transitions
- [ ] Reentrancy surfaces after state updates?
- [ ] Proper pause/lock behavior?
- [ ] Are invariants (balances, totals) enforced?

---

## 6️⃣ External Calls
- [ ] Are low-level calls (`call`, `delegatecall`) handled safely?
- [ ] Pull vs. push payment model?
- [ ] SafeERC20 usage on external transfers?

---

## 7️⃣ Testing & Simulation
- [ ] Unit tests for happy and failure paths
- [ ] Foundry fuzz / invariant tests defined?
- [ ] Simulate griefing or DoS edge cases
- [ ] Mainnet-fork or Anvil scenarios (if applicable)

---

## 8️⃣ Reporting
- [ ] Clear title + severity rationale
- [ ] Reproducible PoC or test snippet
- [ ] Concise impact analysis (who, what, how bad)
- [ ] Recommended mitigation and developer notes
- [ ] Lessons learned section added

---

✅ **Goal:** Always leave a paper trail showing *reasoning, evidence, and reproducibility.*  
This checklist keeps every audit, contest or independent consistent and credible.
