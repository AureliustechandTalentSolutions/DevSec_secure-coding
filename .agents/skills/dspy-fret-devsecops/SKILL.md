---
name: dspy-fret-devsecops
description: Programmatic formalization and DevSecOps synthesis using Stanford DSPy Signatures, dspy.Refine (with Z3/JKind/Bandit rewards), NASA FRET, and OWASP DefectDojo.
---
# DSPy + NASA FRET + DevSecOps Engineering Skill
1. Run `.agents/dspy_factory/fret_devsecops_program.py` to compile unstructured requirements into 6-field NASA `FRETish` and verify realizability via `fret-cli` and Z3.
2. Scan all code with Bandit, Semgrep, TruffleHog, Checkov, and Trivy, saving SARIF/JSON outputs to `./.reports/`.
3. Push scan results to OWASP DefectDojo via the `defectdojo` MCP server and update OSCAL and Omega approval records.
