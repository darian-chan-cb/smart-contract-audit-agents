# Smart Contract Security Audit

## Objective

You are tasked with performing a comprehensive smart contract security audit to identify all vulnerabilities within the Solidity smart contract protocol. This is a high-stakes audit with a 10-day time budget. Your goal is to deploy specialized subagents and ensure that **EVERY line of logic is analyzed at least 3 times** to achieve as close to 100% coverage as possible. No code path should be left unturned.

**Critical Requirements:**
- All agents MUST write their outputs to the `agent-outputs/` folder
- Each phase builds upon the previous phase's documented findings
- Agents should read previous phase outputs for context before starting their analysis

---

## Output Directory Structure

Before starting the audit, ensure the following directory structure exists:

```
agent-outputs/
├── scoping/
│   ├── scoping-agent-1.md
│   ├── scoping-agent-2.md
│   └── scoping-agent-3.md
├── findings/
│   ├── auditor-1-findings.md
│   ├── auditor-2-findings.md
│   └── auditor-3-findings.md
├── static-analysis/
│   └── slither-triage.md
├── triage/
│   ├── critical-high-medium/
│   │   └── [finding-id]-triage.md
│   ├── low-triage.md
│   └── informational-triage.md
├── red-team/
│   ├── red-team-1-findings.md
│   ├── red-team-2-findings.md
│   └── red-team-3-findings.md
└── final-report.md
```


## Phase 1: Scoping (3 Agents - Full Protocol Review)

### Purpose
Build comprehensive understanding of the entire protocol. Each agent reviews **ALL contracts** independently. This ensures every line of code is analyzed 3 times with 3 different agents.

### Agent Deployment
Deploy **3 context-builder subagents**, each analyzing the **ENTIRE protocol** independently

### Required Output Format for Each Scoping Agent
Each agent MUST write a markdown file containing, following the format specified in `.claude/skills/audit-context-building/resources/OUTPUT_REQUIREMENTS.md`


## Phase 2: Manual Line-by-Line Analysis (3 Agents - Full Protocol Review)

### Purpose
Deep vulnerability hunting with every line of code analyzed 3 times by different auditors.

### Prerequisites
- Agents MUST read all files from `agent-outputs/scoping/` before starting
- Use the high-risk areas identified in scoping to prioritize analysis

### Agent Deployment

Deploy **3 smart-contract-auditor subagents**, each analyzing the **ENTIRE protocol** independently.

**Output folder**: `agent-outputs/findings`

---

## Phase 3: Automated Static Analysis (1 Agent)

### Purpose
Run automated tools to catch issues humans might miss.

### Agent Deployment

Deploy **1 static-analyzer subagent** to:
1. Run Slither on the entire protocol
2. Parse and categorize all findings
3. Cross-reference with manual audit findings to identify new issues
4. Triage each finding as: True Positive, False Positive, or Already Found

**Output file**: `agent-outputs/static-analysis/slither-triage.md`

---

## Phase 4: Triage Findings (N Agents)

### Purpose
Validate all findings to eliminate false positives and confirm true positives.

### Prerequisites
- Compile all findings from:
  - `agent-outputs/findings/*.md`
  - `agent-outputs/static-analysis/slither-triage.md`
- Deduplicate findings that multiple auditors found

### Agent Deployment

#### For Critical, High, and Medium Findings:
Deploy **1 finding-triager subagent PER finding** to:
- Verify the vulnerability exists in the code
- Confirm the impact assessment is accurate
- Attempt to find mitigating factors
- Provide final verdict: Valid, Invalid, or Severity Adjustment

**Output files**: `agent-outputs/triage/critical-high-medium/[finding-id]-triage.md`

#### For Low Findings:
Deploy **1 finding-triager subagent** to batch triage all Low findings

**Output file**: `agent-outputs/triage/low-triage.md`

#### For Informational Findings:
Deploy **1 finding-triager subagent** to batch triage all Informational findings

**Output file**: `agent-outputs/triage/informational-triage.md`

---

## Phase 5: Report Generation (1 Agent)

### Purpose
Compile all validated findings into a professional audit report.

### Prerequisites
- Read all triage outputs from `agent-outputs/triage/`
- Only include findings marked as Valid

### Agent Deployment

Deploy **1 report-generator subagent** to create the final report containing:
1. Executive Summary
2. Scope and Methodology
3. Findings Summary Table
4. Detailed Findings (sorted by severity)
5. Recommendations
6. Appendix (files reviewed, tools used)

**Output file**: `agent-outputs/final-report.md`

---

## Phase 6: Red Team Review (3 Agents - Full Protocol Attack)

### Purpose
Final adversarial review to catch anything the audit missed.

### Prerequisites
- Agents MUST read the final report from `agent-outputs/final-report.md`
- Agents should try to find vulnerabilities NOT already in the report

### Agent Deployment

Deploy **3 red-team-attacker subagents**, to independently attack the protocol:

### Required Output Format

For each new vulnerability found:
1. Attack Vector
2. Prerequisites
3. Step-by-Step Exploit
4. Impact Assessment
5. Severity Rating

If no new vulnerabilities found, document:
1. Attack vectors attempted
2. Why each attack failed
3. Confirmation that the protocol handles the attack correctly

---

## Important Guidelines

### For All Agents:
1. **ALWAYS write outputs to the specified files** - Do not just return findings in response
2. **Read previous phase outputs** before starting analysis
3. **Include file:line references** for all findings
4. **Do not background agents** - Wait for each phase to complete before proceeding

### For the Orchestrating Agent:
1. Create the `agent-outputs/` directory structure before starting Phase 1
2. Verify each agent has written its output file before proceeding to next phase
3. After Phase 6, update the final report with any new Red Team findings
4. Ensure the final report is saved to `agent-outputs/final-report.md`

### Quality Checks:
- Every source file should be referenced in at least one scoping document
- Every function with external/public visibility should be analyzed
- Every finding should have a clear severity, location, and recommendation
- The final report should have zero duplicate findings
