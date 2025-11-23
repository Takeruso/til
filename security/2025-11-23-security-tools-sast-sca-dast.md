# 📝 TIL — Security Tool Classification (SAST / SCA / DAST)

## 1. What I Learned (Abstract)

Security tools fall into three fundamentally different categories:
- **SAST** (code analysis)
- **SCA** (dependency analysis)  
- **DAST** (runtime attack testing)

Understanding these distinctions prevents confusion during tool selection.

---

## 2. Concrete Understanding (Examples & My Notes)

### 🔹 SAST — Static Analysis of Source Code

**Purpose:** Detect vulnerabilities directly in the code logic

**Tools:** SonarCloud, CodeQL

**My Observation:**
- ✅ Lightweight configuration and naturally integrates into CI/CD
- ✅ Easiest to adopt for individual developers and small teams

---

### 🔹 SCA — Dependency Vulnerability Analysis

**Purpose:** Detect known CVE vulnerabilities in packages

**Tools:** Snyk, npm audit

**My Observation:**
- ✅ Can be checked immediately during `npm install` workflow with near-zero implementation cost
- ✅ Especially critical for JavaScript projects with heavy external dependencies

---

### 🔹 DAST — Runtime Attack Simulation

**Purpose:** Attack the running app to verify real exploitability

**Tools:** OWASP ZAP

**My Observation:**
- ❌ Heavy setup and difficult to use without prior knowledge
- ❌ Requires mock/test environment preparation, resulting in high overhead

---

## 3. Why This Matters

1. **Prevents misconception:** Avoid the false belief that "npm audit alone ensures security"
2. **Enables comparison:** Understanding which category each tool belongs to makes comparison easier
3. **Improves decision-making:** Can determine which tools to incorporate into CI/CD pipelines in the future

---

## 4. Implementation Insights

| Tool | Implementation Difficulty | Notes |
|------|--------------------------|-------|
| SonarCloud | Easy | Continuous analysis runs automatically once integrated into CI/CD |
| npm audit | Very Easy | Built into npm workflow |
| OWASP ZAP | Hard | Requires extensive preparation (scan target URL, authentication, mode settings, etc.) |

---

## 5. Next Actions (Concrete Improvement Plan)

### A. Break down why DAST (ZAP) was difficult

- [ ] ① Identify scan target pages
- [ ] ② Handle authentication (login state)
- [ ] ③ Understand container version vs CLI version differences
- → Retry after separating these concerns

### B. Integrate SAST + SCA into pokemon-trainer-hub CI

- [ ] GitHub Actions → SonarCloud integration
- [ ] npm audit → Implement `npm audit --audit-level=high` in pipeline

### C. Evaluate SAST applicability to Mira project

- [ ] Assess whether SonarCloud can be applied to Mira project

---

## 6. Key Takeaway

The three-category framework (SAST/SCA/DAST) provides a clear mental model for:
- Understanding tool capabilities at a glance
- Making informed decisions about which tools to implement
- Avoiding false confidence from partial security measures
