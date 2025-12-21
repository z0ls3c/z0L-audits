<div align="center">
  <img src="./logo.png" alt="Logo Alt Text" width="200" />
</div>

# z0L Security Portfolio

Welcome! This is my **smart contract security audit portfolio**, documenting both solo practice work and real contest findings.

---

## ⭐ Highlights

These entries showcase my findings, impact analysis, and remediation guidance.

| Finding Title | Platform | Severity | Status | Link |
|---------------|----------|----------|--------|------|
| Float128::toPackedFloat Fails to Promote to L Size When Exponent Is Critically Low | Code4rena – Forte | High | Valid | ./audit-contests/forte-float128/float128-toPackedFloat/README.md |
| Ln::ln() Fails to Validate Negative Inputs, Causing Division-by-Zero Panics | Code4rena – Forte | High | Valid | ./audit-contests/forte-float128/ln-negative-inputs/README.md |

*More findings and practice audits coming soon.*

---

## 📁 Structure

- **audit-contests/** — Real contest reports and validated findings  
- **practice-audits/** — Independent practice audits on public protocols  
- **templates/** — Report and test templates I use for consistency  

---

## 🧠 Audit Methodology

My process includes:
1. **Surface mapping** — identify boundaries, actors, and trust assumptions  
2. **Access control & auth checks**  
3. **Math & overflow analysis**  
4. **External call & reentrancy review**  
5. **Edge cases & invariants**  
6. **Proof of concept & mitigation recommendations**

*(See `templates/audit-checklist.md` for a checklist)*

---

## 📝 About Me

I’m a Web3 security researcher focused on Solidity and Foundry-based testing, with experience in public contests (Code4rena) and independent case studies.

---

## 📬 Stay in Touch

LinkedIn: https://linkedin.com/in/your-profile  
Github: https://github.com/z0Ld3v
