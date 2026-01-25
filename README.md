# Smart Contract Security Audit Agents

A comprehensive Claude Code multi-agent system for conducting maximum-coverage smart contract security audits. Designed to approach 100% bug detection through parallel agent execution, adversarial validation, and dynamic agent spawning.

## Overview

This toolkit provides an autonomous, multi-agent approach to smart contract security auditing:

- **25 Specialized Agents** covering all vulnerability classes
- **8-Phase Autonomous Pipeline** with parallel execution
- **Dynamic Agent Spawning** for novel vulnerability patterns
- **Consensus Mechanism** for multi-agent finding validation
- **Coverage Verification** ensuring no blind spots
- **10+ Trail of Bits Skills** for platform-specific analysis

## Quick Start

### 1. Copy to Your Project

```bash
cp -r /path/to/smart-contract-audit-agents/.claude /path/to/your-project/
cp /path/to/smart-contract-audit-agents/CLAUDE.md /path/to/your-project/
```

### 2. Install Prerequisites

```bash
# Slither (static analysis)
pip install slither-analyzer

# Foundry (for testing and PoC)
curl -L https://foundry.paradigm.xyz | bash
foundryup

# Semgrep (optional)
pip install semgrep
```

### 3. Run Autonomous Audit

Single command to run complete audit:

```
@audit-orchestrator Perform comprehensive security audit of all Solidity contracts in ./contracts/
```

The orchestrator will:
1. Automatically invoke all 23 agents in correct sequence
2. Run agents in parallel where possible (up to 8 concurrent)
3. Handle inter-agent communication via `.audit/` directory
4. Iterate up to 5 times if coverage gaps found
5. Spawn dynamic agents for novel vulnerability patterns
6. Generate final report with all validated findings

## Agent Inventory

### Core Analysis Agents (9)
| Agent | Purpose |
|-------|---------|
| `@context-builder` | Architecture mapping and trust boundaries |
| `@entry-point-mapper` | Attack surface identification |
| `@static-analyzer` | Slither/Semgrep automated scanning |
| `@access-control-reviewer` | RBAC and permission analysis |
| `@upgrade-safety-reviewer` | Proxy and storage safety |
| `@smart-contract-auditor` | First-principles vulnerability hunting (novel bugs) |
| `@solidity-quirks-analyst` | Token quirks, arithmetic, gas/DoS, language pitfalls |
| `@finding-triager` | False positive elimination |
| `@report-generator` | Professional report compilation |

### Specialized Gap Coverage Agents (8)
| Agent | Purpose |
|-------|---------|
| `@l2-rollup-reviewer` | L2/rollup specific vulnerabilities (sequencer, bridges) |
| `@mev-ordering-analyst` | Front-running, sandwich attacks, MEV vectors |
| `@crypto-analyst` | Signature, hash, randomness vulnerabilities |
| `@economic-attack-modeler` | Flash loans, game theory, incentive attacks |
| `@formal-verifier` | Invariant extraction, Certora/Halmos integration |
| `@oracle-analyst` | Price feed manipulation, staleness, Chainlink |
| `@cross-contract-analyst` | Reentrancy, callbacks, composability risks |
| `@external-integration-analyst` | External protocol quirks (EAS, Uniswap, Aave, Lido, LayerZero) |

### Adversarial Agents (3)
| Agent | Purpose |
|-------|---------|
| `@red-team-attacker` | Offensive attack construction from attacker perspective |
| `@devils-advocate` | Challenge findings, prove false positives |
| `@historical-exploit-comparator` | Pattern match against 500+ historical exploits |

### Coordination Agents (5)
| Agent | Purpose |
|-------|---------|
| `@audit-orchestrator` | Master autonomous pipeline controller |
| `@anomaly-detector` | Detect unknown patterns, trigger dynamic spawning |
| `@consensus-aggregator` | Multi-agent finding aggregation and conflict resolution |
| `@coverage-gap-analyzer` | Verify complete coverage, identify blind spots |
| `@_dynamic-specialist-template` | Template for runtime agent spawning |

## Autonomous Pipeline

### 8-Phase Execution

```
┌─────────────────────────────────────────────────────────────────┐
│  SINGLE COMMAND: @audit-orchestrator "Audit contracts in /src" │
└─────────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 1: Foundation (parallel)                                    │
│   → context-builder + historical-exploit-comparator               │
└─────────────────────────────┼─────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 2: Attack Surface (parallel)                                │
│   → entry-point-mapper + static-analyzer                          │
└─────────────────────────────┼─────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 3: Deep Analysis (8 agents in parallel)                     │
│   → access-control, upgrade-safety, smart-contract-auditor        │
│   → solidity-quirks, l2-rollup, mev-ordering, crypto, economic    │
└─────────────────────────────┼─────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 4: Specialized (5 agents in parallel)                       │
│   → oracle, cross-contract, formal-verifier                       │
│   → red-team-attacker, devils-advocate                            │
└─────────────────────────────┼─────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 5: Consensus & Validation                                   │
│   → consensus-aggregator + finding-triager + coverage-gap         │
└─────────────────────────────┼─────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 6: Dynamic Agent Spawning                                   │
│   → anomaly-detector identifies novel patterns                    │
│   → Spawns specialized agents for unknown unknowns                │
└─────────────────────────────┼─────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 7: Iteration Loop                                           │
│   → If coverage < 99%: re-run targeted agents                     │
│   → Max 5 iterations                                              │
└─────────────────────────────┼─────────────────────────────────────┘
                              │
┌─────────────────────────────┼─────────────────────────────────────┐
│ PHASE 8: Report Generation                                        │
│   → report-generator compiles FINAL_REPORT.md                     │
└───────────────────────────────────────────────────────────────────┘
```

## Vulnerability Coverage

### All Classes Explicitly Checked

- **Reentrancy** - Classic, cross-function, cross-contract, read-only, callbacks
- **Access Control** - Missing checks, role escalation, admin abuse
- **Integer Issues** - Overflow, underflow, precision loss, rounding
- **Oracle Manipulation** - Flash loan attacks, TWAP, staleness
- **MEV/Front-running** - Sandwich, JIT liquidity, time-bandit
- **Signature Issues** - Replay, malleability, missing validation
- **Upgrade Vulnerabilities** - Storage collision, initializer, authorization
- **Economic Attacks** - Flash loans, governance, incentive misalignment
- **Cross-Contract** - Composability, callbacks, delegatecall
- **L2-Specific** - Sequencer, bridges, L1-L2 messaging
- **Cryptographic** - ECDSA, VRF, commitment schemes
- **DoS Vectors** - Unbounded loops, gas griefing, permanent pause

## Dynamic Agent Spawning

For unknown vulnerabilities ("unknown unknowns"), the system can spawn specialized agents at runtime:

1. `@anomaly-detector` identifies novel code patterns
2. Classifies the pattern type (financial, governance, crypto, etc.)
3. Generates specialized agent prompt from template
4. Spawns dynamic agent for deep analysis
5. Integrates findings into consensus

**Example dynamic spawns:**
- Custom bonding curve → `dynamic-bonding-curve-specialist`
- Novel voting escrow → `dynamic-vote-escrow-specialist`
- Custom liquidation → `dynamic-liquidation-specialist`

## Consensus & Validation

### Multi-Agent Agreement

Findings are scored by consensus:
- **Unanimous** (all agents): 1.0 confidence
- **Supermajority** (2/3+): 0.85 confidence
- **Majority**: 0.70 confidence
- **Single specialized**: 0.60 confidence
- **Contested**: 0.40 → requires human review

### Adversarial Validation

- `@devils-advocate` challenges ALL findings
- Must survive scrutiny to be confirmed
- Findings that survive get confidence boost (+20%)
- Disproven findings are removed

## Output Structure

```
.audit/
├── context/
│   ├── ARCHITECTURE.md
│   └── HISTORICAL_PATTERNS.md
├── surface/
│   ├── ENTRY_POINTS.md
│   └── STATIC_ANALYSIS.md
├── findings/
│   ├── access-control.md
│   ├── upgrade-safety.md
│   ├── manual-audit.md
│   ├── l2-rollup.md
│   ├── mev-ordering.md
│   ├── crypto.md
│   ├── economic.md
│   ├── oracle.md
│   ├── cross-contract.md
│   ├── formal.md
│   ├── red-team.md
│   ├── devils-advocate.md
│   └── dynamic/
│       └── *.md
├── consensus/
│   ├── AGGREGATED_FINDINGS.md
│   ├── VALIDATED_FINDINGS.md
│   └── COVERAGE_REPORT.md
└── FINAL_REPORT.md
```

## Manual Agent Execution

For step-by-step control, invoke agents individually:

```bash
# Phase 1: Build context
@context-builder Analyze the architecture of contracts in ./src/

# Phase 2: Map attack surface
@entry-point-mapper Identify all entry points

# Phase 3: Run static analysis
@static-analyzer Run Slither and Semgrep on the codebase

# Phase 4: Deep analysis
@smart-contract-auditor Hunt for vulnerabilities in the core contracts

# ... continue through phases
```

## Trail of Bits Skills

### Vulnerability Scanners
- **Algorand** - TEAL/PyTeal patterns
- **Cairo** - StarkNet issues
- **Cosmos** - Cosmos SDK vulnerabilities
- **Solana** - Anchor/native program issues
- **Substrate** - Pallet security
- **TON** - FunC/Tact vulnerabilities

### Analysis Skills
- **entry-point-analyzer** - Attack surface mapping
- **audit-context-building** - Ultra-granular analysis
- **property-based-testing** - Fuzz testing guidance
- **differential-review** - Change review
- **static-analysis** - CodeQL/Semgrep integration
- **variant-analysis** - Similar vulnerability discovery

## Configuration

See `CLAUDE.md` for detailed configuration options including:
- Coverage thresholds
- Confidence scoring
- Iteration limits
- Quality gates

## File Structure

```
.claude/
├── agents/
│   ├── audit-orchestrator.md      # Master controller
│   ├── anomaly-detector.md        # Novel pattern detection
│   ├── _dynamic-specialist-template.md
│   ├── context-builder.md
│   ├── entry-point-mapper.md
│   ├── static-analyzer.md
│   ├── access-control-reviewer.md
│   ├── upgrade-safety-reviewer.md
│   ├── smart-contract-auditor.md
│   ├── solidity-quirks-analyst.md
│   ├── l2-rollup-reviewer.md
│   ├── mev-ordering-analyst.md
│   ├── crypto-analyst.md
│   ├── economic-attack-modeler.md
│   ├── formal-verifier.md
│   ├── oracle-analyst.md
│   ├── cross-contract-analyst.md
│   ├── external-integration-analyst.md
│   ├── red-team-attacker.md
│   ├── devils-advocate.md
│   ├── historical-exploit-comparator.md
│   ├── consensus-aggregator.md
│   ├── coverage-gap-analyzer.md
│   ├── finding-triager.md
│   └── report-generator.md
└── plugins/
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

- **Trail of Bits** - Building Secure Contracts framework
- **Slither** - Static analysis for Solidity
- **OpenZeppelin** - Security patterns and contracts
- **Rekt Database** - Historical exploit patterns

## License

MIT License - Use and modify freely for security audits.
