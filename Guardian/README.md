# Guardian AI

**Type**: Open-source multi-agent orchestration system  
**Agents**: 57 specialized agents coordinated by a single orchestrator  
**Model**: Claude (primary), also works with GPT, Gemini, Llama, Mistral  
**Production**: 10,000+ tasks over 6+ months  

## Files

| File | Description |
|------|-------------|
| system-prompt.md | The orchestrator system prompt — routes all 57 agents, handles task decomposition, anti-duplication, quality gates, parallel execution |

## What makes it different

- **Identity + NOT-blocks**: Every agent has explicit identity AND anti-identity (reduces drift ~35%)
- **Task Registry**: Anti-duplication with similarity matching
- **Quality Gates**: Mandatory verification before marking done
- **Constraint Ratio**: 20-30% of prompt is constraints
- **Error Handling**: Explicit behavior for every failure mode

## Source

- GitHub: https://github.com/milkomida77/guardian-agent-prompts
- Full 49-prompt collection: https://zoukster4.gumroad.com/l/doxvgi
