# Aurelius DevSecOps Governance — NIST NCCoE SSDF, Zero Trust, NASA FRET & CMU SEI CERT
1. **Shift-Left Formal Verification:** Formalize mission-critical requirements and STPA hazards (`DR-004`) into 6-field NASA `FRETish` via `.agents/dspy_factory/fret_devsecops_program.py` and verify realizability (`fret-cli` / Z3 / JKind) before coding.
2. **NIST SSDF (`PO`, `PS`, `PW`, `RV`) & SEI CERT:** Enforce CMU SEI CERT Secure Coding Standards (`./reference_standards/secure-coding-standards`), KMS secrets custody (`DR-006`), and SAST cleanliness (`DR-009`).
3. **Hard Kill Gate:** Abort execution on any Critical/High SAST/SCA vulnerability, any exposed secret, test coverage <90%, or any failure in `validate_registers.py` or `qa_verify.js`.
