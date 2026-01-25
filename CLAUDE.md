# Smart Contract Audit Configuration

This file configures Claude Code for maximum-coverage smart contract security auditing.

## Audit Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| **Thoroughness** | MAXIMUM | Use full compute budget for all analysis |
| **Model** | claude-opus-4-5 | All agents use Opus for maximum capability |
| **Extended Thinking** | ENABLED | 128k token thinking budget |
| **Parallel Agents** | Up to 8 | Maximum concurrent agent execution |
| **Target Coverage** | 99%+ | Minimum acceptable coverage (any missed bug is catastrophic) |
| **Iterations** | Up to 5 | Re-analysis iterations for gaps |

## Agent Inventory

### Core Analysis Agents (9)
| Agent | Purpose |
|-------|---------|
| `@context-builder` | Architecture mapping and trust boundaries |
| `@entry-point-mapper` | Attack surface identification |
| `@static-analyzer` | Slither/Semgrep automated scanning |
| `@access-control-reviewer` | RBAC and permission analysis |
| `@upgrade-safety-reviewer` | Proxy and storage safety |
| `@smart-contract-auditor` | First-principles vulnerability hunting |
| `@solidity-quirks-analyst` | Token quirks, arithmetic, gas/DoS, language pitfalls |
| `@finding-triager` | False positive elimination |
| `@report-generator` | Professional report compilation |

### Specialized Gap Coverage Agents (8)
| Agent | Purpose |
|-------|---------|
| `@l2-rollup-reviewer` | L2/rollup specific vulnerabilities |
| `@mev-ordering-analyst` | Front-running and MEV vectors |
| `@crypto-analyst` | Cryptographic implementation review |
| `@economic-attack-modeler` | Game theory and incentive analysis |
| `@formal-verifier` | Invariant extraction and verification |
| `@oracle-analyst` | Price feed and oracle security |
| `@cross-contract-analyst` | Composability and callback risks |
| `@external-integration-analyst` | External protocol quirks (EAS, Uniswap, Aave, etc.) |

### Adversarial Agents (3)
| Agent | Purpose |
|-------|---------|
| `@red-team-attacker` | Adversarial attack construction |
| `@devils-advocate` | Challenge and validate findings |
| `@historical-exploit-comparator` | Pattern match against known exploits |

### Coordination Agents (4)
| Agent | Purpose |
|-------|---------|
| `@audit-orchestrator` | Master pipeline controller |
| `@anomaly-detector` | Unknown pattern detection |
| `@consensus-aggregator` | Multi-agent finding aggregation |
| `@coverage-gap-analyzer` | Coverage verification |

## Coverage Requirements

### Function Coverage
- Every public/external function analyzed by 3+ agents
- Value-moving functions analyzed by 5+ agents
- Admin functions require access control review

### Vulnerability Class Coverage
All classes must be explicitly checked:
- [ ] Reentrancy (all types)
- [ ] Access control
- [ ] Integer issues
- [ ] Oracle manipulation
- [ ] Flash loan attacks
- [ ] MEV/front-running
- [ ] Signature issues
- [ ] Upgrade vulnerabilities
- [ ] DoS vectors
- [ ] Logic errors
- [ ] Economic attacks
- [ ] Cross-contract issues
- [ ] L2-specific issues (if applicable)
- [ ] Cryptographic issues

### Entry Point Coverage
- Every entry point has threat model
- Every external call has risk assessment

## Execution

### Full Autonomous Audit
```
@audit-orchestrator Perform comprehensive security audit of all Solidity contracts in ./contracts/
```

### Manual Phase Execution
```
Phase 1: @context-builder + @historical-exploit-comparator
Phase 2: @entry-point-mapper + @static-analyzer
Phase 3: @smart-contract-auditor + @access-control-reviewer + @upgrade-safety-reviewer + specialized agents
Phase 4: @oracle-analyst + @cross-contract-analyst + @formal-verifier + @red-team-attacker + @devils-advocate
Phase 5: @consensus-aggregator + @finding-triager + @coverage-gap-analyzer
Phase 6: @anomaly-detector (dynamic spawning)
Phase 7: Iteration if needed
Phase 8: @report-generator
```

## Output Structure

Audit outputs are written to `.audit/`:
```
.audit/
├── context/
│   ├── ARCHITECTURE.md
│   └── HISTORICAL_PATTERNS.md
├── surface/
│   ├── ENTRY_POINTS.md
│   └── STATIC_ANALYSIS.md
├── findings/
│   ├── [agent-name].md (per agent)
│   └── dynamic/
│       └── *.md (dynamically spawned agents)
├── consensus/
│   ├── AGGREGATED_FINDINGS.md
│   ├── VALIDATED_FINDINGS.md
│   └── COVERAGE_REPORT.md
└── FINAL_REPORT.md
```

## Quality Gates

### Before Report Generation
- [ ] Function coverage >= 99%
- [ ] Vulnerability class coverage = 100% (every class must be explicitly checked)
- [ ] Entry point coverage >= 99%
- [ ] All HIGH+ findings validated by @devils-advocate
- [ ] No unreviewed critical functions (value-moving functions require 100% coverage)
- [ ] Coverage gap analysis complete
- [ ] Any missed vulnerability could be catastrophic - err on the side of over-analysis

### Finding Confidence Thresholds
| Confidence | Action |
|------------|--------|
| >= 0.9 | Include with high confidence |
| 0.7 - 0.9 | Include in report |
| 0.5 - 0.7 | Include with caveat |
| < 0.5 | Flag for human review |

## Dynamic Agent Spawning

When `@anomaly-detector` identifies novel patterns:
1. Pattern is classified by type
2. Dynamic specialist is spawned using `_dynamic-specialist-template.md`
3. Findings are collected to `.audit/findings/dynamic/`
4. Results feed into consensus aggregation

## Iteration Rules

Re-analysis is triggered when:
- Function coverage < 99%
- Vulnerability class not explicitly checked
- High-risk function has shallow coverage
- Novel pattern identified

Maximum iterations: 5 (to allow thorough coverage at 99% target)
