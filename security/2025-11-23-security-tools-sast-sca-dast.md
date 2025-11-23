# Security Tools Classification (SAST, SCA, DAST)

## 1. What I Learned Today (Abstract)
Security-related tools can be organized into three categories: **SAST, SCA, and DAST**.

## 2. Concrete Examples

### SAST (Static Application Security Testing)
- **Purpose**: Static analysis of vulnerabilities in code itself
- **Tool Examples**: SonarCloud, CodeQL
- **Hands-on Experience**: ✅ **Quite easy to implement**

### SCA (Software Composition Analysis)
- **Purpose**: Check for known vulnerabilities in dependent packages
- **Tool Examples**: Snyk, npm audit
- **Hands-on Experience**: ✅ **Simple - just run `npm install`**

### DAST (Dynamic Application Security Testing)
- **Purpose**: Attack testing from external perspective by running the application
- **Tool Examples**: OWASP ZAP
- **Hands-on Experience**: ❌ **Difficult to set up**

## 3. Why It Matters (Practical Value)

- Different tools have different implementation complexities, enabling project-specific selection
- Avoids the misconception that **"running npm audit = secure"**
- Helps identify which category a feature-rich tool belongs to when evaluating new solutions

## 4. Implementation-Level Insights (New)

| Tool | Ease of Implementation | Notes |
|------|----------------------|-------|
| SonarCloud | Easy | Can be automated after initial setup |
| npm audit | Easy | Already integrated into `npm install` workflow |
| OWASP ZAP | Difficult | Requires separate environment setup; needs thoughtful configuration |

## 5. Next Actions
- [ ] Investigate what made OWASP ZAP difficult to implement
- [ ] Integrate SonarCloud/npm audit into CI/CD pipeline
- [ ] Review documentation to lower DAST adoption barriers
