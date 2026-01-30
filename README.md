# Smart Contract Security Audit Agents

A collection of Claude agents and Trail of Bits skills for conducting comprehensive smart contract security audits.

## Overview

This toolkit provides a systematic approach to smart contract security auditing, combining:

- **9 Specialized Agents** for different phases of security analysis
- **20+ Trail of Bits Skills** for vulnerability detection across multiple blockchain platforms
- **Structured Workflow** from context building to report generation

---

## Setup

### Step 1: Copy to Your Project

Copy the `.claude` folder to the root of your smart contract project:

```bash
cp -r /path/to/smart-contract-audit-agents/.claude /path/to/your-project/
```

### Step 2: Create Output Directories

Create the required output folders for agents to store their findings:

```bash
mkdir -p agent-outputs/scoping
mkdir -p agent-outputs/findings
mkdir -p agent-outputs/triaged
mkdir -p agent-outputs/red-team
```

**Directory purposes:**
| Directory | Purpose | Written by |
|-----------|---------|------------|
| `agent-outputs/scoping/` | Architecture, context, entry points | context-builder, entry-point-mapper |
| `agent-outputs/findings/` | Raw vulnerability findings | smart-contract-auditor, static-analyzer, access-control-reviewer, upgrade-safety-reviewer |
| `agent-outputs/red-team/` | Adversarial attack analysis | red-team-attacker |
| `agent-outputs/triaged/` | Validated findings after triage | finding-triager |

### Step 3: Install Prerequisites

```bash
# Slither (static analysis for Solidity)
pip install slither-analyzer

# Foundry (for testing and building)
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

### Step 4: Verify Setup

Your project structure should look like:

```
your-project/
├── .claude/
│   ├── agents/           # 9 specialized audit agents
│   ├── skills/           # 20+ Trail of Bits skills
│   └── plugins/          # Plugin source files
├── agent-outputs/
│   ├── scoping/          # Context and entry point analysis
│   ├── findings/         # Raw vulnerability findings
│   ├── red-team/         # Adversarial analysis
│   └── triaged/          # Validated findings
├── src/                  # Your smart contracts
└── test/                 # Your tests
```

---

## Audit Workflow

### Agent Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           PHASE 1: SCOPING                                   │
│                                                                              │
│   @context-builder ─────┬──────► agent-outputs/scoping/                     │
│   @entry-point-mapper ──┘                                                    │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           PHASE 2: ANALYSIS                                  │
│                                                                              │
│   @static-analyzer ───────────────────────────► agent-outputs/findings/     │
│   @access-control-reviewer ───────────────────► agent-outputs/findings/     │
│   @upgrade-safety-reviewer ───────────────────► agent-outputs/findings/     │
│   @smart-contract-auditor ◄── reads scoping ──► agent-outputs/findings/     │
│   @red-team-attacker ─────────────────────────► agent-outputs/red-team/     │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           PHASE 3: TRIAGE                                    │
│                                                                              │
│   @finding-triager ◄── reads findings + red-team ──► agent-outputs/triaged/ │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           PHASE 4: REPORTING                                 │
│                                                                              │
│   @report-generator ◄── reads triaged ──► SECURITY_AUDIT_REPORT.md          │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Recommended Execution Order

| Order | Agent | Purpose | Reads From | Writes To |
|-------|-------|---------|------------|-----------|
| 1 | `@context-builder` | Build architectural understanding | Source code | `agent-outputs/scoping/` |
| 2 | `@entry-point-mapper` | Map attack surfaces | Source code | `agent-outputs/scoping/` |
| 3 | `@static-analyzer` | Run Slither/Semgrep | Source code | `agent-outputs/findings/` |
| 4 | `@access-control-reviewer` | Audit roles and permissions | Source code | `agent-outputs/findings/` |
| 5 | `@upgrade-safety-reviewer` | Check proxy patterns | Source code | `agent-outputs/findings/` |
| 6 | `@smart-contract-auditor` | Deep vulnerability hunting | `agent-outputs/scoping/` | `agent-outputs/findings/` |
| 7 | `@red-team-attacker` | Adversarial attack simulation | Source code | `agent-outputs/red-team/` |
| 8 | `@finding-triager` | Validate findings | `agent-outputs/findings/`, `agent-outputs/red-team/` | `agent-outputs/triaged/` |
| 9 | `@report-generator` | Generate audit report | `agent-outputs/triaged/` | `SECURITY_AUDIT_REPORT.md` |

---

## Agents

| Agent | Purpose | Model |
|-------|---------|-------|
| `context-builder` | Build architectural understanding before auditing | opus |
| `entry-point-mapper` | Map all external functions and attack surface | opus |
| `static-analyzer` | Run Slither/Semgrep and interpret results | opus |
| `access-control-reviewer` | Deep dive into RBAC and permissions | opus |
| `upgrade-safety-reviewer` | Audit proxy patterns and storage safety | opus |
| `smart-contract-auditor` | Manual vulnerability hunting | opus |
| `red-team-attacker` | Adversarial attack simulation and exploitation | opus |
| `finding-triager` | Validate findings, detect false positives | opus |
| `report-generator` | Compile findings into professional report | opus |

---

## Included Skills (Trail of Bits)

### Vulnerability Scanners
| Skill | Platform | Patterns |
|-------|----------|----------|
| `algorand-vulnerability-scanner` | Algorand/TEAL | 11 vulnerability patterns |
| `cairo-vulnerability-scanner` | StarkNet/Cairo | 6 vulnerability patterns |
| `cosmos-vulnerability-scanner` | Cosmos SDK | 9 vulnerability patterns |
| `solana-vulnerability-scanner` | Solana/Anchor | 6 vulnerability patterns |
| `substrate-vulnerability-scanner` | Substrate/Polkadot | 7 vulnerability patterns |
| `ton-vulnerability-scanner` | TON/FunC | 3 vulnerability patterns |

### Development Guidelines
| Skill | Purpose |
|-------|---------|
| `audit-prep-assistant` | Prepare codebase for security reviews |
| `code-maturity-assessor` | 9-category code maturity evaluation |
| `guidelines-advisor` | Development best practices advisor |
| `secure-workflow-guide` | 5-step secure development workflow |
| `token-integration-analyzer` | Token security and weird patterns |

### Analysis Skills
| Skill | Purpose |
|-------|---------|
| `entry-point-analyzer` | Systematic attack surface mapping |
| `audit-context-building` | Ultra-granular code analysis methodology |
| `property-based-testing` | Fuzz testing guidance |
| `differential-review` | Security-focused code change review |
| `variant-analysis` | Find similar vulnerability patterns |
| `semgrep` | Semgrep rule application |
| `codeql` | CodeQL query execution |
| `sarif-parsing` | SARIF output processing |

---

## Usage Examples

### Running a Full Audit

```bash
# 1. Set up your project
cd /path/to/your-project
cp -r /path/to/smart-contract-audit-agents/.claude .
mkdir -p agent-outputs/{scoping,findings,triaged,red-team}

# 2. Start Claude Code
claude

# 3. Run agents in order
> Use @context-builder to analyze the smart contracts in src/
> Use @entry-point-mapper to map all entry points
> Use @static-analyzer to run Slither on the codebase
> Use @smart-contract-auditor to perform deep security analysis
> Use @red-team-attacker to find exploitable vulnerabilities
> Use @finding-triager to validate all findings
> Use @report-generator to create the audit report
```

### Running Specific Agents

```bash
# Just context building
> Use @context-builder to analyze src/Token.sol and document the architecture

# Just access control review
> Use @access-control-reviewer to audit the role-based access control in src/

# Just upgrade safety
> Use @upgrade-safety-reviewer to check the UUPS proxy implementation
```

---

## Customization

### Adding Protocol-Specific Checks

Edit `.claude/agents/smart-contract-auditor.md` to add protocol-specific vulnerability patterns:

```markdown
### 11. Your Protocol Patterns
For [Your Protocol]:
- [ ] Custom check 1
- [ ] Custom check 2
- [ ] Custom check 3
```

### Adjusting Model Selection

Each agent specifies its model in the frontmatter. Change `opus` to `sonnet` for faster/cheaper analysis:

```yaml
---
name: smart-contract-auditor
model: sonnet  # Changed from opus
---
```

### Adding New Skills

Create a new skill in `.claude/skills/your-skill/SKILL.md`:

```markdown
---
name: your-skill
description: What this skill does
---

# Your Skill

Instructions for Claude when this skill is loaded...
```

Then reference it in an agent:

```markdown
### Your Skill
Read: `.claude/skills/your-skill/SKILL.md`
- What it provides
```

---

## File Structure

```
.claude/
├── agents/
│   ├── access-control-reviewer.md
│   ├── context-builder.md
│   ├── entry-point-mapper.md
│   ├── finding-triager.md
│   ├── red-team-attacker.md
│   ├── report-generator.md
│   ├── smart-contract-auditor.md
│   ├── static-analyzer.md
│   └── upgrade-safety-reviewer.md
├── skills/
│   ├── algorand-vulnerability-scanner/
│   ├── audit-context-building/
│   ├── cairo-vulnerability-scanner/
│   ├── code-maturity-assessor/
│   ├── codeql/
│   ├── cosmos-vulnerability-scanner/
│   ├── differential-review/
│   ├── entry-point-analyzer/
│   ├── guidelines-advisor/
│   ├── property-based-testing/
│   ├── sarif-parsing/
│   ├── semgrep/
│   ├── solana-vulnerability-scanner/
│   ├── substrate-vulnerability-scanner/
│   ├── token-integration-analyzer/
│   ├── ton-vulnerability-scanner/
│   └── variant-analysis/
└── plugins/
    └── ... (plugin source files)

agent-outputs/
├── scoping/      # Architecture and entry point documentation
├── findings/     # Raw vulnerability findings
├── red-team/     # Adversarial attack analysis
└── triaged/      # Validated findings ready for reporting
```

---

## Troubleshooting

### Slither Not Found

```bash
pip install slither-analyzer
# or
pip3 install slither-analyzer
```

### Foundry Not Found

```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

### Agent Can't Find Skill Files

Ensure you copied the entire `.claude` folder:

```bash
ls -la .claude/skills/
# Should show 15+ skill directories
```

### Agent Outputs Not Being Saved

Ensure output directories exist:

```bash
mkdir -p agent-outputs/{scoping,findings,triaged,red-team}
```

---

## Credits

- **Trail of Bits** - Building Secure Contracts framework and skills
- **Slither** - Static analysis for Solidity
- **OpenZeppelin** - Security patterns and contracts

## License

MIT License - Feel free to use and modify for your security audits.
