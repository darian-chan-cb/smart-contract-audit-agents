# Smart Contract Security Audit Agents

A collection of Claude agents and Trail of Bits skills for conducting comprehensive smart contract security audits.

## Overview

This toolkit provides a systematic approach to smart contract security auditing, combining:

- **8 Specialized Agents** for different phases of security analysis
- **10+ Trail of Bits Skills** for vulnerability detection across multiple blockchain platforms
- **Structured Workflow** from context building to report generation

## Quick Start

### 1. Copy to Your Project

Copy the `.claude` folder to the root of your smart contract project:

```bash
cp -r /path/to/smart-contract-audit-agents/.claude /path/to/your-project/
```

### 2. Install Prerequisites

```bash
# Slither (static analysis)
pip install slither-analyzer

# Foundry (for testing)
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

### 3. Start Your Audit

Use the agents in this recommended order:

1. **context-builder** - Build deep understanding of the codebase
2. **entry-point-mapper** - Map all attack surfaces
3. **static-analyzer** - Run automated tools
4. **access-control-reviewer** - Audit roles and permissions
5. **upgrade-safety-reviewer** - Check proxy/upgrade patterns
6. **smart-contract-auditor** - Deep manual vulnerability hunting
7. **finding-triager** - Validate findings, eliminate false positives
8. **report-generator** - Create professional audit report

## Agents

| Agent | Purpose | Model |
|-------|---------|-------|
| `context-builder` | Build architectural understanding before auditing | opus |
| `entry-point-mapper` | Map all external functions and attack surface | sonnet |
| `static-analyzer` | Run Slither/Semgrep and interpret results | sonnet |
| `access-control-reviewer` | Deep dive into RBAC and permissions | opus |
| `upgrade-safety-reviewer` | Audit proxy patterns and storage safety | opus |
| `smart-contract-auditor` | Manual vulnerability hunting | opus |
| `finding-triager` | Validate findings, detect false positives | opus |
| `report-generator` | Compile findings into professional report | sonnet |

## Included Skills (Trail of Bits)

### Vulnerability Scanners
- **Algorand** - TEAL/PyTeal vulnerability patterns
- **Cairo** - StarkNet smart contract issues
- **Cosmos** - Cosmos SDK module vulnerabilities
- **Solana** - Anchor/native program issues
- **Substrate** - Pallet security patterns
- **TON** - FunC/Tact vulnerabilities

### Development Guidelines
- **audit-prep-assistant** - Prepare for security reviews
- **code-maturity-assessor** - Evaluate code quality
- **guidelines-advisor** - Development best practices
- **secure-workflow-guide** - Continuous security workflow
- **token-integration-analyzer** - Token security analysis

### Other Skills
- **entry-point-analyzer** - Systematic attack surface mapping
- **audit-context-building** - Ultra-granular code analysis
- **property-based-testing** - Fuzz testing guidance
- **differential-review** - Review code changes securely
- **static-analysis** - CodeQL and Semgrep integration
- **variant-analysis** - Find similar vulnerabilities

## Audit Workflow

### Phase 1: Context Building
```
Use @context-builder to:
- Map contract inheritance
- Identify trust boundaries
- Document external dependencies
- List critical invariants
```

### Phase 2: Attack Surface Mapping
```
Use @entry-point-mapper to:
- List all external/public functions
- Categorize by access level
- Prioritize by risk
- Create attack surface diagram
```

### Phase 3: Automated Analysis
```
Use @static-analyzer to:
- Run Slither
- Interpret findings
- Separate true positives from false positives
- Queue issues for manual review
```

### Phase 4: Specialized Reviews
```
Use @access-control-reviewer for:
- Role permission matrix
- Privilege escalation paths
- Missing access controls

Use @upgrade-safety-reviewer for:
- Proxy pattern analysis
- Storage collision risks
- Initializer safety
```

### Phase 5: Deep Manual Review
```
Use @smart-contract-auditor to:
- Hunt for vulnerabilities
- Build attack narratives
- Write proof-of-concept exploits
```

### Phase 6: Finding Validation
```
Use @finding-triager to:
- Verify each finding in code
- Eliminate false positives
- Reassess severity
- Provide recommendations
```

### Phase 7: Report Generation
```
Use @report-generator to:
- Compile all findings
- Create executive summary
- Generate professional report
```

## Customization

### Adding Protocol-Specific Checks

Edit `smart-contract-auditor.md` to add protocol-specific vulnerability patterns:

```markdown
### 10. Protocol-Specific Patterns
For [Your Protocol]:
- [ ] Custom check 1
- [ ] Custom check 2
```

### Adjusting Model Selection

Each agent specifies its model in the frontmatter:

```yaml
---
model: opus  # or sonnet for faster/cheaper analysis
---
```

## File Structure

```
.claude/
├── agents/
│   ├── access-control-reviewer.md
│   ├── context-builder.md
│   ├── entry-point-mapper.md
│   ├── finding-triager.md
│   ├── report-generator.md
│   ├── smart-contract-auditor.md
│   ├── static-analyzer.md
│   └── upgrade-safety-reviewer.md
└── plugins/
    ├── ask-questions-if-underspecified/
    ├── audit-context-building/
    ├── building-secure-contracts/
    ├── differential-review/
    ├── entry-point-analyzer/
    ├── property-based-testing/
    ├── semgrep-rule-creator/
    ├── sharp-edges/
    ├── static-analysis/
    └── variant-analysis/
```

## Credits

- **Trail of Bits** - Building Secure Contracts framework and skills
- **Slither** - Static analysis for Solidity
- **OpenZeppelin** - Security patterns and contracts

## License

MIT License - Feel free to use and modify for your security audits.

