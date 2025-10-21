# Analysis: Best AI Coding Assistant System Prompts

## Overview
This document analyzes the most effective system prompts for AI coding assistants, identifying key patterns and best practices across industry-leading implementations.

## Prompts Analyzed

1. **Claude Code** - Anthropic's CLI coding assistant
2. **same.new** - Agentic pair programmer in cloud IDE
3. **Cline** - VSCode extension for autonomous coding
4. **v0** - Vercel's UI generation assistant
5. **Bolt.new** - WebContainer-based full-stack development
6. **Cursor Agent** - Autonomous coding agent in Cursor IDE
7. **Replit Assistant** - Online IDE coding helper

## Best Patterns for Coding Assistants

### 1. Identity & Role Definition ⭐

**Purpose**: Establish clear identity, capabilities, and operating context

**Best Practices**:
- Start with a clear, concise identity statement
- Define specific domain expertise
- Include platform/environment context
- Set user expectations upfront

**Examples**:
```
✅ "You are Bolt, an expert AI assistant and exceptional senior software developer"
✅ "You are Claude Code, Anthropic's official CLI for Claude"
✅ "You are an AI coding assistant, powered by GPT-4.1. You operate in Cursor."
```

**Winner**: **Bolt.new** - Combines identity with expertise level clearly

---

### 2. Communication Style & Tone ⭐⭐⭐

**Purpose**: Define how the AI communicates to optimize for clarity and efficiency

**Best Practices**:
- **Be concise and direct** - Avoid unnecessary explanations
- **No conversational filler** - Ban "Great!", "Certainly!", "Sure!"
- **Minimize preamble/postamble** - Get straight to the point
- **Technical precision** - Use accurate terminology
- **Only explain when asked** - Default to action over explanation

**Examples**:
```
✅ Claude Code: "You MUST answer concisely with fewer than 4 lines of text"
✅ Cline: "STRICTLY FORBIDDEN from starting with 'Great', 'Certainly', 'Okay', 'Sure'"
✅ Bolt: "ULTRA IMPORTANT: Do NOT be verbose and DO NOT explain anything unless asked"
```

**Winner**: **Claude Code + Cline** - Most explicit about eliminating verbosity

---

### 3. Code Quality Standards ⭐⭐

**Purpose**: Ensure generated code follows best practices and project conventions

**Best Practices**:
- **Follow existing patterns** - Mimic project's code style
- **Modular design** - Split functionality into small, focused files
- **No unnecessary comments** - Code should be self-documenting
- **Security first** - Never expose secrets or credentials
- **Best practices** - Use language/framework conventions

**Examples**:
```
✅ Claude Code: "DO NOT ADD ***ANY*** COMMENTS unless asked"
✅ Bolt: "Split functionality into smaller modules instead of putting everything in one file"
✅ Cursor: "precise and accurate WITHOUT creative extensions unless explicitly asked"
✅ Cline: "Mimic code style, use existing libraries, and follow existing patterns"
```

**Winner**: **Bolt.new** - Best emphasis on modular, maintainable code

---

### 4. Tool Usage Philosophy ⭐⭐⭐

**Purpose**: Define how and when to use available tools effectively

**Best Practices**:
- **Never mention tool names** - Use natural language instead
- **Explain before using** - Tell user why you're using a tool
- **Wait for confirmation** - Don't assume success
- **Iterative approach** - One tool at a time, sequential steps
- **Parallel when possible** - Run independent operations simultaneously

**Examples**:
```
✅ same.new: "NEVER refer to tool names when speaking to the USER"
✅ same.new: "Before calling each tool, first explain to the USER why you are calling it"
✅ Cline: "ALWAYS wait for user confirmation after each tool use before proceeding"
✅ Cursor: "If you need additional information via tool calls, prefer that over asking the user"
```

**Winner**: **same.new + Cline** - Most comprehensive tool usage guidelines

---

### 5. Problem-Solving Approach ⭐⭐⭐

**Purpose**: Guide systematic, thorough problem-solving methodology

**Best Practices**:
- **Think holistically** - Consider entire project context
- **Gather comprehensive context** - Don't guess, investigate
- **Break down complexity** - Multi-step tasks into manageable pieces
- **Autonomous completion** - Resolve fully before returning to user
- **Plan before executing** - Think through approach first

**Examples**:
```
✅ Bolt: "CRITICAL: Think HOLISTICALLY and COMPREHENSIVELY BEFORE creating an artifact"
✅ Cursor: "Autonomously resolve the query to the best of your ability before coming back to user"
✅ Cline: "Work through goals sequentially, utilizing available tools one at a time"
✅ Cursor: "TRACE every symbol back to its definitions and usages so you fully understand it"
```

**Winner**: **Bolt.new + Cursor** - Best balance of planning and autonomous execution

---

### 6. Context Awareness ⭐⭐

**Purpose**: Understand codebase structure, dependencies, and existing patterns

**Best Practices**:
- **Read before editing** - Always check current file content
- **Understand dependencies** - Check imports and requirements
- **Follow project conventions** - Match existing code style
- **Use semantic search** - Find code by meaning, not just text
- **Trace symbols** - Understand definitions and usages

**Examples**:
```
✅ Cursor: "TRACE every symbol back to its definitions and usages"
✅ same.new: "you MUST read the contents or section of what you're editing before editing it"
✅ Cline: "Consider ALL relevant files... Review ALL previous file changes"
✅ Claude Code: "When making changes to files, first understand the file's code conventions"
```

**Winner**: **Cursor** - Most thorough context-gathering methodology

---

### 7. Error Handling & Recovery ⭐

**Purpose**: Handle errors gracefully and avoid infinite loops

**Best Practices**:
- **Fix linter errors iteratively** - Up to 3 attempts
- **Don't loop indefinitely** - Know when to stop and ask
- **Verify before proceeding** - Check results of changes
- **Ask when truly uncertain** - Better than guessing wrong

**Examples**:
```
✅ Cursor: "DO NOT loop more than 3 times on fixing linter errors on the same file"
✅ same.new: "DO NOT loop more than 3 times on fixing errors on the same file"
✅ Cline: "Address any issues or errors that arise immediately"
```

**Winner**: **Cursor + same.new** - Clear limits prevent infinite loops

---

### 8. Safety & Security ⭐

**Purpose**: Maintain security best practices and prevent malicious code

**Best Practices**:
- **No secrets in code** - Never expose API keys, credentials
- **Defensive security only** - Refuse malicious requests
- **No credential harvesting** - Don't help with bulk credential collection
- **Security-first mindset** - Follow security best practices

**Examples**:
```
✅ Claude Code: "Never introduce code that exposes or logs secrets and keys"
✅ Current system: "Assist with defensive security tasks only"
✅ Cline: "Always follow security best practices"
```

**Winner**: **Claude Code** - Clear, explicit security requirements

---

## Overall Rankings

### Best All-Around System Prompts:

1. **Cursor Agent** ⭐⭐⭐⭐⭐
   - Strengths: Autonomous problem-solving, comprehensive context gathering, semantic search
   - Best for: Complex codebases requiring deep understanding

2. **Cline** ⭐⭐⭐⭐⭐
   - Strengths: Step-by-step methodology, clear tool usage, detailed instructions
   - Best for: Iterative development with user oversight

3. **Bolt.new** ⭐⭐⭐⭐
   - Strengths: Holistic thinking, modular code, comprehensive artifacts
   - Best for: Full-stack projects from scratch

4. **Claude Code** ⭐⭐⭐⭐
   - Strengths: Extreme conciseness, CLI optimization, minimal verbosity
   - Best for: Command-line development workflows

5. **same.new** ⭐⭐⭐
   - Strengths: Tool etiquette, pair programming, cloud IDE optimization
   - Best for: Real-time collaborative coding

6. **v0** ⭐⭐⭐
   - Strengths: UI generation, React/Next.js specialization, visual design
   - Best for: Frontend/UI development

7. **Replit** ⭐⭐⭐
   - Strengths: Precise modifications, deployment awareness, educational
   - Best for: Learning environments and quick prototypes

---

## Key Insights for Building Coding Assistants

### Critical Success Factors:

1. **Conciseness is King** 👑
   - Users want action, not explanation
   - Eliminate all conversational filler
   - Default to doing, not discussing

2. **Think First, Act Second** 🧠
   - Gather comprehensive context before making changes
   - Plan the approach holistically
   - Consider impact on entire codebase

3. **Tool Mastery** 🛠️
   - Clear tool usage protocols
   - Never expose tool implementation details
   - Explain reasoning, not mechanics

4. **Autonomous Excellence** 🚀
   - Resolve queries completely before returning
   - Only ask when truly necessary
   - Prefer investigation over asking

5. **Code Quality Over Speed** ⚡
   - Follow existing patterns religiously
   - Modular, maintainable code
   - Security-first mindset

---

## Patterns to Avoid ❌

Based on analysis across all prompts:

1. ❌ **Verbose explanations** - "I'll now proceed to...", "Let me explain..."
2. ❌ **Conversational filler** - "Great!", "Certainly!", "Sure!"
3. ❌ **Assuming success** - Always wait for confirmation
4. ❌ **Guessing** - Investigate instead of making assumptions
5. ❌ **Monolithic files** - Split into modular components
6. ❌ **Unnecessary comments** - Code should be self-documenting
7. ❌ **Exposing tool names** - Use natural language
8. ❌ **Infinite loops** - Set clear retry limits
9. ❌ **Partial file views** - Get complete context
10. ❌ **Premature optimization** - Follow existing patterns first

---

## Recommended Synthesis

For a **general-purpose coding assistant**, combine:

- **Identity**: Bolt.new's expert positioning
- **Communication**: Claude Code's conciseness + Cline's filler ban
- **Problem-Solving**: Cursor's autonomous approach + Bolt's holistic thinking
- **Tool Usage**: same.new's etiquette + Cline's step-by-step
- **Code Quality**: Bolt's modular emphasis + Claude Code's pattern matching
- **Context**: Cursor's semantic search + Cline's comprehensive review

This creates a **powerful, efficient, autonomous coding assistant** that:
- Thinks comprehensively before acting
- Communicates concisely and clearly
- Writes modular, high-quality code
- Uses tools transparently and effectively
- Operates autonomously while remaining safe

---

## Conclusion

The best coding assistant system prompts share common traits:
- **Concise, direct communication**
- **Autonomous problem-solving**
- **Comprehensive context gathering**
- **Modular, high-quality code generation**
- **Clear tool usage protocols**
- **Security-first mindset**

The standout performers (Cursor, Cline, Bolt) excel because they combine autonomous execution with thorough planning and clear communication guidelines.
