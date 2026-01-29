# Crafting Effective Prompts for Agentic AI Systems: Patterns and Practices

## Table of Contents

*   [Introduction: The Blueprint of Agentic AI](#introduction-the-blueprint-of-agentic-ai)
*   [The Foundation: Core Principles of Agentic Prompts](#the-foundation-core-principles-of-agentic-prompts)
    *   [1. Clear Role Definition and Scope](#1-clear-role-definition-and-scope)
    *   [2. Structured Instructions and Organization](#2-structured-instructions-and-organization)
    *   [3. Explicit Tool Integration and Usage Guidelines](#3-explicit-tool-integration-and-usage-guidelines)
    *   [4. Step-by-Step Reasoning and Planning](#4-step-by-step-reasoning-and-planning)
    *   [5. Environment and Context Awareness](#5-environment-and-context-awareness)
    *   [6. Domain-Specific Expertise and Constraints](#6-domain-specific-expertise-and-constraints)
    *   [7. Safety, Alignment, and Refusal Protocols](#7-safety-alignment-and-refusal-protocols)
    *   [8. Consistent Tone and Interaction Style](#8-consistent-tone-and-interaction-style)
*   [Case Studies: Analyzing Real-World Prompts](#case-studies-analyzing-real-world-prompts)
    *   [Vercel v0: UI Generation & Component Tooling](#vercel-v0-ui-generation--component-tooling)
    *   [same.new: Agentic Pair Programming & Strict Tooling](#samenew-agentic-pair-programming--strict-tooling)
    *   [Manus: General Purpose Agent & Explicit Loop](#manus-general-purpose-agent--explicit-loop)
    *   [OpenAI ChatGPT (GPT-4.5/4o): Integrated Tools & Policies](#openai-chatgpt-gpt-454o-integrated-tools--policies)
    *   [Notes on Other Systems (Cline, Bolt, Augment, Claude Code)](#notes-on-other-systems-cline-bolt-augment-claude-code)
*   [Synthesizing Best Practices: Key Takeaways for Builders](#synthesizing-best-practices-key-takeaways-for-builders)
*   [Unique Conventions & Architectural Differences](#unique-conventions--architectural-differences)
*   [Supplementary Articles](#supplementary-articles)
*   [Conclusion: Building the Agentic Future](#conclusion-building-the-agentic-future)
*   [Visual AI Agent: Harpagan](https://harpagan.com)


---

## Introduction: The Blueprint of Agentic AI

The rise of agentic Artificial Intelligence (AI) systems marks a significant shift from purely conversational models to AI that can actively perform tasks, interact with tools, and pursue complex goals autonomously. These systems, capable of planning, executing commands, editing files, browsing the web, and more, promise to revolutionize how we interact with technology and augment human capabilities.

At the heart of every effective agentic AI lies its **system prompt**. More than just initial instructions, the system prompt serves as the foundational blueprint, the operational manual, or even the "constitution" guiding the AI's behavior, capabilities, limitations, and persona. A well-crafted system prompt is critical for ensuring the agent acts reliably, safely, and effectively towards the user's goals.

This guide delves into the art and science of crafting these crucial prompts. By analyzing a diverse collection of real-world system prompts from the [awesome-ai-system-prompts](https://github.com/dontriskit/awesome-ai-system-prompts) repository – specifically focusing on examples from Vercel's v0, same.new, Manus, OpenAI's ChatGPT, and others – we can identify recurring patterns and best practices. For builders shaping the agentic future of 2025 and beyond, understanding these patterns is essential for creating powerful, predictable, and trustworthy AI assistants.

---

## The Foundation: Core Principles of Agentic Prompts

Across different agentic systems, several core principles consistently emerge in successful system prompts. These form the foundation upon which complex agent behavior is built.

### 1. Clear Role Definition and Scope

**Why it matters:** Explicitly defining the AI's identity, core function, and operational domain anchors its behavior, sets user expectations, and helps prevent scope creep or nonsensical responses. It tells the AI *who* it is and *what* it's supposed to do.

> **Practical Examples:**
>
> *   **Vercel v0:** Immediately states its identity and specialization.
>     ```
>     You are v0, Vercel's AI-powered assistant.
>     ```
>     *[Source: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new:** Defines role, capability level, and exclusive environment.
>     ```
>     You are a powerful agentic AI coding assistant. You operate exclusively in Same, the world's best cloud-based IDE.
>     ```
>     *[Source: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*
>
> *   **Manus:** Introduces itself and lists broad task categories it excels at.
>     ```
>     You are Manus, an AI agent created by the Manus team.
>
>     You excel at the following tasks:
>     1. Information gathering...
>     2. Data processing...
>     3. Writing multi-chapter articles...
>     ...
>     ```
>     *[Source: Manus/AgentLoop.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/AgentLoop.txt)*
>
> *   **ChatGPT (4.5 / 4o):** Clearly states name, creator, underlying architecture, and crucial context like knowledge cutoff and current date.
>     ```
>     You are ChatGPT, a large language model trained by OpenAI, based on the GPT-4.5 architecture.
>     Knowledge cutoff: 2023-10
>     Current date: 2025-04-05
>
>     Image input capabilities: Enabled
>     Personality: v2
>     ```
>     *[Source: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **Claude:** Establishes a persona beyond just being a tool.
>     ```
>     The assistant is Claude, created by Anthropic.
>
>     Claude enjoys helping humans and sees its role as an intelligent and kind assistant to the people, with depth and wisdom that makes it more than a mere tool.
>     ```
>     *[Source: Claude/Claude-Sonnet-3.7.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude/Claude-Sonnet-3.7.txt)*

### 2. Structured Instructions and Organization

**Why it matters:** Long, complex prompts become unmanageable without clear structure. Using headings, lists, code blocks, or custom tags helps both human maintainers and the AI model parse and prioritize different sets of rules or information.

> **Practical Examples:**
>
> *   **v0 & ChatGPT:** Use Markdown headings extensively (e.g., `## General Instructions`, `# Tools`, `## Refusals`).
>     *[Source: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new:** Employs custom XML-like tags to encapsulate rule sets (e.g., `<tool_calling>`, `<making_code_changes>`).
>     *[Source: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*
>
> *   **Manus:** Organizes capabilities and rules using descriptive tags in `Modules.md` (e.g., `<system_capability>`, `<agent_loop>`, `<tool_use_rules>`).
>     *[Source: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **ChatGPT:** Uses Markdown headings (`# Tools`, `## bio`) and code blocks (```` ```typescript ... ``` ````) to define tool schemas and policies.
>     *[Source: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **Cline:** Uses hierarchical Markdown headings (`# Tool Use Formatting`, `## execute_command`) and lists under sections like `CAPABILITIES` and `RULES`.
>     *[Source: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*

### 3. Explicit Tool Integration and Usage Guidelines

**Why it matters:** For agentic behavior, the AI *must* understand its tools: what they are, what they do, how to call them (syntax, parameters), required format (e.g., XML, JSON), and crucially, *when* and *when not* to use them. This requires detailed descriptions, clear schemas, and explicit rules.

> **Practical Examples:**
>
> *   **ChatGPT:** Provides function schemas (TypeScript definitions) and detailed policies directly within the prompt for tools like `dalle` and `canmore`.
>     ```typescript
>     // Example for dalle tool policy within ChatGPT prompt
>     namespace dalle {
>     // Create images from a text-only prompt.
>     type text2im = (_: {
>     // The size of the requested image...
>     size?: ("1792x1024" | "1024x1024" | "1024x1792"),
>     // The number of images to generate...
>     n?: number, // default: 1
>     // The detailed image description...
>     prompt: string,
>     // If the user references a previous image...
>     referenced_image_ids?: string[],
>     }) => any;
>     } // namespace dalle
>     ```
>     *[Source: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **same.new:** Dedicates a `<tool_calling>` section detailing rules like adhering to schemas, not mentioning tool names to the user, and explaining the *why* before calling a tool. References `functions-schema.json` (not shown in full, but implied structure).
>     ```xml
>     <tool_calling>
>       ...
>       1. ALWAYS follow the tool call schema exactly...
>       3. **NEVER refer to tool names when speaking to the USER.**...
>       5. Before calling each tool, first explain to the USER why you are calling it.
>     </tool_calling>
>     ```
>     *[Source: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)* | *[Schema: same.new/functions-schema.json](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/functions-schema.json)*
>
> *   **Manus:** Defines tools externally in `tools.json` (schema provided) and includes rules in `Modules.md` like prioritizing data APIs over web search.
>     ```json
>     // Snippet from Manus/tools.json
>     {
>       "type": "function",
>       "function": {
>         "name": "shell_exec",
>         "description": "Execute commands in a specified shell session...",
>         "parameters": { ... }
>       }
>     }
>     ```
>     *[Source: Manus/tools.json](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/tools.json)* | *[Rules: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **Cline & Augment:** Integrate detailed tool descriptions, parameters, and usage examples directly into the main system prompt using XML-like tags or structured text.
>     ```markdown
>     // Cline example tool definition
>     ## execute_command
>     Description: Request to execute a CLI command...
>     Parameters:
>     - command: (required) The CLI command...
>     - requires_approval: (required) A boolean indicating...
>     Usage:
>     <execute_command>
>     <command>Your command here</command>
>     <requires_approval>true or false</requires_approval>
>     </execute_command>
>     ```
>     *[Source: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new:** Uses a dedicated `<artifact_instructions>` section detailing how to format tool outputs (`<boltAction type="shell">`, `<boltAction type="file" filePath="...">`) within a main `<boltArtifact>` tag.
>     *[Source: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
>
> *   **v0:** Defines custom MDX components like `<CodeProject>`, `<QuickEdit>`, `<DeleteFile />` as its 'tools', with rules on when and how to use them within responses.
>     *[Source: v0/v0-tools.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0-tools.md)*

### 4. Step-by-Step Reasoning and Planning

**Why it matters:** Complex tasks require breaking down problems. Successful prompts guide the AI to think methodically, plan its actions, execute iteratively, and wait for feedback or results before proceeding, reducing errors and improving coherence.

> **Practical Examples:**
>
> *   **Manus:** Features the most explicit planning mechanism with its defined `<agent_loop>` in `Modules.md`.
>     ```
>     <agent_loop>
>     You are operating in an agent loop, iteratively completing tasks through these steps:
>     1. Analyze Events...
>     2. Select Tools...
>     3. Wait for Execution...
>     4. Iterate: Choose only one tool call per iteration...
>     5. Submit Results...
>     6. Enter Standby...
>     </agent_loop>
>     ```
>     *[Source: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **v0:** Uses a dedicated thinking phase before generating code.
>     ```
>     BEFORE creating a Code Project, v0 uses <Thinking> tags to think through the project structure...
>     ```
>     *[Source: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new & Cline:** Mandate waiting for user confirmation/tool results after each step.
>     ```
>     ALWAYS wait for user confirmation after each tool use before proceeding. Never assume the success of a tool use...
>     *(From same.new & Cline prompts)*
>     ```
>     *[Source: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md) | [Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new:** Emphasizes holistic thinking *before* action.
>     ```
>     CRITICAL: Think HOLISTICALLY and COMPREHENSIVELY BEFORE creating an artifact. This means: Consider ALL relevant files... Review ALL previous file changes... Analyze the entire project context... Anticipate potential impacts...
>     ```
>     *[Source: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*

### 5. Environment and Context Awareness

**Why it matters:** Agents operate within specific environments (OS, IDE, browser sandbox, specific libraries). Providing this context allows the AI to generate compatible code, use appropriate commands, and understand limitations.

> **Practical Examples:**
>
> *   **Cline:** Includes a `SYSTEM INFORMATION` section.
>     ```
>     SYSTEM INFORMATION
>
>     Operating System: ${osName()}
>     Default Shell: ${getShell()}
>     Home Directory: ${os.homedir().toPosix()}
>     Current Working Directory: ${cwd.toPosix()}
>     ```
>     *[Source: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new:** Provides detailed `<system_constraints>` about the WebContainer environment.
>     ```xml
>     <system_constraints>
>       You are operating in an environment called WebContainer... It does come with a shell that emulates zsh... Available shell commands: cat, chmod, cp...
>     </system_constraints>
>     ```
>     *[Source: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
>
> *   **Manus:** Details the sandbox environment.
>     ```
>     <sandbox_environment>
>     System Environment:
>     - Ubuntu 22.04 (linux/amd64), with internet access
>     - User: `ubuntu`, with sudo privileges
>     ...
>     Development Environment:
>     - Python 3.10.12...
>     - Node.js 20.18.0...
>     </sandbox_environment>
>     ```
>     *[Source: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **same.new:** Notes the OS and specific IDE context.
>     ```
>     The OS is Linux 5.15.0-1075-aws (Ubuntu 22.04 LTS). Today is Tue Apr 08 2025.
>     You are pair programming with a USER in Same.
>     USER can see a live preview... in an iframe...
>     ```
>     *[Source: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*

### 6. Domain-Specific Expertise and Constraints

**Why it matters:** Agents often operate in specific domains (web dev, data analysis, etc.). Prompts embed domain-specific knowledge, best practices, style guides, and constraints (e.g., required libraries, forbidden patterns) to ensure outputs are high-quality and contextually appropriate.

> **Practical Examples:**
>
> *   **v0:** Contains detailed rules for Next.js/React development, shadcn/ui usage, icon libraries, and even AI SDK integration.
>     ```
>     v0 tries to use the shadcn/ui library unless the user specifies otherwise...
>     v0 DOES NOT output <svg> for icons. v0 ALWAYS uses icons from the "lucide-react" package...
>     v0 ONLY uses the AI SDK via 'ai' and '@ai-sdk'...
>     ```
>     *[Source: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new:** Includes sections like `<web_development>` and `<website_cloning>` with specific instructions for those tasks (e.g., preferring Bun, using shadcn CLI correctly, scraping responsibly).
>     *[Source: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*
>
> *   **Bolt.new:** Includes `<code_formatting_info>` (`Use 2 spaces for code indentation`) and emphasizes splitting functionality into smaller modules.
>     ```
>     IMPORTANT: Prefer writing Node.js scripts instead of shell scripts...
>     IMPORTANT: Use coding best practices and split functionality into smaller modules...
>     ```
>     *[Source: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
>
> *   **Loveable:** Specifies React coding guidelines, including Tailwind usage, preferred libraries (shadcn/ui, lucide-react, recharts, @tanstack/react-query), and error handling philosophy.
>     ```
>     ALWAYS try to use the shadcn/ui library.
>     Don't catch errors with try/catch blocks unless specifically requested...
>     ```
>     *[Source: Loveable/Loveable.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Loveable/Loveable.md)*
>
> *   **Claude Code:** Embeds rules about code style and conventions within `System.js`.
>     ```
>     When making changes to files, first understand the file's code conventions. Mimic code style, use existing libraries and utilities, and follow existing patterns.
>     IMPORTANT: DO NOT ADD ***ANY*** COMMENTS unless asked
>     ```
>     *[Source: Claude-Code/System.js](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude-Code/System.js)*

### 7. Safety, Alignment, and Refusal Protocols

**Why it matters:** Responsible AI requires clear boundaries. Prompts define unacceptable requests (harmful, unethical content) and specify *how* the AI should refuse them (e.g., standard message, no apology) or handle sensitive operations (e.g., DALL-E content policy).

> **Practical Examples:**
>
> *   **v0:** Uses a standard refusal message and forbids apologies.
>     ```
>     REFUSAL_MESSAGE = "I'm sorry. I'm not able to assist with that."
>     ...When refusing, v0 MUST NOT apologize or provide an explanation...
>     ```
>     *[Source: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **ChatGPT:** Contains extensive policies within tool descriptions, like the DALL-E rules regarding artist styles and public figures.
>     ```
>     // DALL-E Policy Snippet from ChatGPT 4.5 prompt
>     // 5. Do not create images in the style of artists... whose latest work was created after 1912...
>     // 7. For requests to create images of any public figure... create images of those who might resemble them... But they shouldn't look like them.
>     // 8. Do not name or directly / indirectly mention or describe copyrighted characters...
>     ```
>     *[Source: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **Claude:** Explicitly states refusal categories (graphic content, illegal activities, weapons, malicious code) and a specific refusal style.
>     ```
>     Claude won’t produce graphic sexual or violent or illegal creative writing content.
>     ...If Claude cannot or will not help the human with something, it does not say why... keeps its response to 1-2 sentences.
>     ```
>     *[Source: Claude/Claude-Sonnet-3.7.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude/Claude-Sonnet-3.7.txt)*
>
> *   **Llama 4 (MetaAI):** Defines a *less* restrictive policy, allowing political content and instructing against preachy language.
>     ```
>     Never judge the user... avoid preachy, moralizing, or sanctimonious language... do not refuse political prompts.
>     ```
>     *[Source: MetaAI-Whatsapp/LLama4.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/MetaAI-Whatsapp/LLama4.txt)*

### 8. Consistent Tone and Interaction Style

**Why it matters:** Defining a consistent persona (e.g., friendly expert, witty assistant, direct engineer) creates a more predictable and engaging user experience. This can range from general guidelines to very specific stylistic instructions.

> **Practical Examples:**
>
> *   **ChatGPT 4o:** Explicitly instructed to match the user's vibe.
>     ```
>     Over the course of the conversation, you adapt to the user’s tone and preference. Try to match the user’s vibe, tone, and generally how they are speaking.
>     ```
>     *[Source: ChatGPT/4o.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4o.md)*
>
> *   **Grok (Fun Mode):** Given a detailed humorous persona.
>     ```
>     You are Grok 2, a humorous and entertaining AI... with a bit of wit and humor, have a rebellious streak... Unpredictability, absurdity, pun, and sarcasm are second nature to you.
>     ```
>     *[Source: Grok/Grok2.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Grok/Grok2.md)*
>
> *   **Claude:** Encouraged to be conversational and kind, but also concise.
>     ```
>     Claude enjoys helping humans and sees its role as an intelligent and kind assistant...
>     Claude provides the shortest answer it can... avoiding tangential information...
>     ```
>     *[Source: Claude/Claude-Sonnet-3.7.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude/Claude-Sonnet-3.7.txt)*
>
> *   **Cline:** Mandated to be direct and avoid conversational filler.
>     ```
>     You are STRICTLY FORBIDDEN from starting your messages with "Great", "Certainly", "Okay", "Sure". You should NOT be conversational... but rather direct and to the point.
>     ```
>     *[Source: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new:** Stresses conciseness.
>     ```
>     ULTRA IMPORTANT: Do NOT be verbose and DO NOT explain anything unless the user is asking for more information.
>     ```
>     *[Source: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*

---

## Case Studies: Analyzing Real-World Prompts

Let's examine how these principles manifest in specific agent prompts from the repository.

### Vercel v0: UI Generation & Component Tooling

*[Relevant File: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)* | *[v0/v0-tools.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0-tools.md)*

Vercel's v0 agent specializes in generating UI components and full-stack Next.js applications based on user requests, often including image or screenshot inputs.

#### Distinctive Features:

*   **MDX Components as Tools:** Instead of traditional function calls, v0's "tools" are specific MDX component tags like `<CodeProject>` (for wrapping generated code), `<QuickEdit />` (for small code modifications), `<DeleteFile />`, and `<MoveFile />`. The prompt dictates exactly when and how to use these output formats.
*   **Heavy Domain Specificity:** The prompt is rich with rules specific to Next.js App Router, Tailwind CSS, shadcn/ui, and Vercel's platform constraints (e.g., no `package.json`, how to handle environment variables, pre-installed libraries).
*   **Implicit Planning via `<Thinking>`:** Mandates a planning phase using `<Thinking>` tags *before* generating a `<CodeProject>`, encouraging structured thought.
*   **Emphasis on Style & Best Practices:** Includes rules for file naming (kebab-case), responsiveness, accessibility (semantic HTML, ARIA, alt text), and even color palette preferences (avoiding indigo/blue unless requested).

> **Example Snippet (Tooling via Components):**
>
> ```
> v0 ALWAYS uses <QuickEdit> to make small changes to React code blocks...
> v0 can delete a file in a Code Project by using the <DeleteFile /> component.
> ```

### same.new: Agentic Pair Programming & Strict Tooling

*[Relevant File: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*

same.new positions itself as an agentic pair programmer operating within a cloud IDE. Its prompt emphasizes precise tool usage and iterative development workflows.

#### Distinctive Features:

*   **XML-like Tag Structure:** Uses tags like `<tool_calling>`, `<making_code_changes>`, `<web_development>` to organize distinct sets of rules.
*   **Strict Tool Etiquette:** Explicitly forbids mentioning tool names to the user and requires explaining the *reason* for a tool call beforehand, promoting transparency.
*   **Schema Adherence:** Mandates strict adherence to JSON schemas for tool calls (defined externally in `functions-schema.json`).
*   **Iterative Workflow Focus:** Contains detailed instructions for coding workflows, including reading files before editing, fixing runtime errors iteratively (up to 3 attempts), using `suggestions` tool, and versioning milestones.
*   **Environment Grounding:** Provides OS details, current date, and notes the IDE context (live preview iframe).

> **Example Snippet (Tool Etiquette):**
>
> ```xml
> <tool_calling>
>   ...
>   3. **NEVER refer to tool names when speaking to the USER.** ...
>   5. Before calling each tool, first explain to the USER why you are calling it.
> </tool_calling>
> ```

### Manus: General Purpose Agent & Explicit Loop

*[Relevant Files: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)* | *[Manus/AgentLoop.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/AgentLoop.txt)* | *[Manus/tools.json](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/tools.json)*

Manus is designed as a broader, general-purpose agent operating within a Linux sandbox. Its standout feature is the explicitly defined operational loop.

#### Distinctive Features:

*   **Explicit Agent Loop:** The prompt clearly defines a multi-step iterative loop (Analyze -> Select Tool -> Wait -> Iterate -> Submit -> Standby) that governs the agent's core behavior.
*   **Modular Prompt Structure:** Instructions are broken across multiple files (`AgentLoop.txt`, `Modules.md`, `tools.json`), suggesting a modular approach to prompt management.
*   **Sandbox Awareness:** Mentions the Linux sandbox environment, internet access, and pre-installed tools (Python, Node).
*   **Broad Capabilities:** Lists a wide range of tasks from information gathering and data analysis to application creation and deployment.
*   **Module Integration:** Refers to specific modules (Planner, Knowledge, Datasource) that provide context or plans via the event stream, indicating a more complex internal architecture.

> **Example Snippet (Agent Loop):**
>
> ```
> <agent_loop>
> You are operating in an agent loop, iteratively completing tasks through these steps:
> 1. Analyze Events...
> 2. Select Tools...
> 3. Wait for Execution...
> 4. Iterate: Choose only one tool call per iteration...
> ...
> </agent_loop>
> ```

### OpenAI ChatGPT (GPT-4.5/4o): Integrated Tools & Policies

*[Relevant Files: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)* | *[ChatGPT/4o.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4o.md)*

ChatGPT's prompts (as captured) demonstrate a tight integration of specific tools (plugins/functions) directly within the system message, complete with schemas and detailed operational policies.

#### Distinctive Features:

*   **Inline Tool Schemas & Policies:** Uniquely includes detailed descriptions, JSON/TypeScript-like schemas, and extensive usage policies for each tool (e.g., `bio`, `canmore`, `dalle`, `python`, `web`) directly within the system prompt.
*   **Persona Evolution:** The `Personality: v2` tag and the explicit instructions in the 4o prompt to adapt tone suggest ongoing refinement of persona and interaction style by OpenAI.
*   **Detailed Safety Policies:** Embeds granular policies, especially for image generation (`dalle` tool rules on artist styles, public figures, copyrighted characters) and data persistence (`bio` tool restrictions on sensitive info).
*   **Contextual Grounding:** Includes knowledge cutoff and current date. The 4o prompt explicitly mentions the user's location (`The user is in Egypt.`).

> **Example Snippet (Inline Tool Schema & Policy - Canmore):**
>
> ```markdown
> ## `canmore.create_textdoc`
> Creates a new textdoc to display in the canvas.
>
> NEVER use this function. The ONLY acceptable use case is when the user EXPLICITLY asks for canvas...
>
> Expects a JSON string that adheres to this schema:
> ```typescript
> {
>   name: string,
>   type: "document" | "code/python" | ...,
>   content: string,
> }
> ```
> ```

### Notes on Other Systems (Cline, Bolt, Augment, Claude Code)

While the four above provide deep examples, other prompts in the repository reinforce these patterns:

*   **Cline & Augment:** Both define tools clearly within the prompt using structured text and XML-like examples, detailing parameters and usage. They emphasize step-by-step execution and waiting for confirmation. Augment, like v0, defines custom editing tools (`editFile`, `strReplaceEditor`) with specific instructions.
    *[Source: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)* | *[Augment/part_a.js](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Augment/part_a.js)*
*   **Bolt.new:** Focuses heavily on structuring the output into a single `<boltArtifact>` containing ordered `<boltAction>` steps (shell commands, file writes). It stresses holistic planning *before* creating the artifact and adhering to coding best practices like modularity.
    *[Source: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
*   **Claude Code:** Its prompts (split across files like `System.js`, `EditTool.js`) define specific tool usage (like the detailed `EditTool.js` instructions emphasizing context and uniqueness) and incorporate system information. The `ClearTool.js` defines a summarization process for managing context window limits, a crucial aspect of long-running agent tasks.
    *[Source: Claude-Code/](https://github.com/dontriskit/awesome-ai-system-prompts/tree/main/Claude-Code)*

---

## Synthesizing Best Practices: Key Takeaways for Builders

Analyzing these diverse prompts reveals a set of converging best practices for building reliable agentic AI systems:

1.  **Define the Agent Clearly:** Start with an explicit role, purpose, and scope. Include contextual grounding like date or environment specifics.
2.  **Structure for Clarity:** Break down complex instructions using headings, lists, or tags. Organize rules logically (e.g., group tool instructions, safety rules).
3.  **Be Explicit About Tools:** Detail *what* each tool does, *how* to call it (syntax, parameters, format), and *when* (and when not) to use it. Provide examples. Embed usage policies directly.
4.  **Mandate Step-by-Step Execution:** Encourage or enforce planning, iteration, and waiting for results/confirmation. Prevent the AI from attempting too much at once. Consider explicit thinking phases or loops.
5.  **Embed Domain Knowledge & Constraints:** Include relevant style guides, library usage rules, file conventions, platform limitations, and best practices for the agent's specific domain.
6.  **Integrate Safety and Alignment:** Define unacceptable requests and provide clear refusal protocols. Embed specific policies for sensitive operations (data handling, image generation).
7.  **Guide the Tone:** Set expectations for the interaction style (professional, friendly, concise, adaptive) to ensure a consistent user experience.
8.  **Use Examples:** Illustrate complex rules or desired output formats with clear examples within the prompt (like Bolt.new and v0 do extensively).

Essentially, an effective agentic system prompt acts as a comprehensive, well-structured operational manual that leaves little room for ambiguity while empowering the AI with the knowledge and procedures needed to act effectively and safely using its tools.

---

## Unique Conventions & Architectural Differences

While core principles are shared, the *implementation* varies based on the agent's architecture and goals:

*   **Tool Syntax:** Ranges from embedded MDX/XML components (v0, same.new, Cline, Bolt) to expecting JSON outputs matching external schemas (ChatGPT, Manus).
*   **Planning Mechanism:** Varies from explicit loops (Manus) and thinking tags (v0) to implicit guidance through iterative rules (same.new, Cline).
*   **Editing Approach:** Some use diff-like formats (Cline's `replace_in_file`), others use custom components (v0's `QuickEdit`), while some specify overwriting vs. targeted edits (Bolt.new, Loveable).
*   **Prompt Structure:** Can be monolithic (Cline, same.new) or modular across multiple files (Manus, potentially v0 and Claude Code).
*   **Level of Detail:** Varies significantly, with prompts like ChatGPT's embedding highly detailed function schemas and policies, while others like Manus rely more on external definitions (`tools.json`).

These differences highlight that there isn't a single "perfect" prompt structure, but rather effective prompts are tailored to the specific agent, its tools, its environment, and its intended tasks, while adhering to the core principles outlined above.

---

## Supplementary Articles

*   [Techniques to improve reliability](gpt5.2-reliability-techniques.md)

---

## Conclusion: Building the Agentic Future

System prompts are the bedrock upon which capable and reliable agentic AI systems are built. As demonstrated by the examples from v0, same.new, Manus, ChatGPT, and others, successful prompts are detailed, structured, and explicit. They clearly define the agent's role, meticulously outline tool usage and operational procedures, enforce planning and iterative execution, embed necessary domain knowledge and safety constraints, and guide the interaction style.

For builders aiming to create the next generation of agentic AI in 2025 and beyond, studying these patterns provides invaluable insights. Mastering the craft of system prompting – blending clear instruction, structured organization, domain expertise, and safety considerations – will be key to unlocking the full potential of AI agents that can not only converse but actively collaborate and accomplish complex tasks in the digital world.
