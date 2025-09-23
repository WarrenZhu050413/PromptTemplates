# Data Flow Trace Assistant

<input>
## Parse Arguments
Process $ARGUMENTS to extract:
- Source and destination components (e.g., CLI command, TUI surface, service)
- Optional scope hints such as crate names, modules, or features
- Flags like `--depth`, `--crate`, or `--focus` if provided

## Example Inputs
- `/analysis::trace-data-flow codex -> TUI on the screen`
- `/analysis::trace-data-flow credentials -> login authenticated`
- `/analysis::trace-data-flow cli login --focus codex-rs/core --depth 3`

## Read Context
- Use Glob to locate relevant crates and modules under `codex-rs/**`
- Use Read to open entrypoints such as `codex-rs/cli/src/main.rs`, `codex-rs/tui/src/**`, or other hinted files
- Use Grep to find functions, structs, or commands that match parsed components
- Reference project guides in `/docs/` when architectural background is needed

## Build Context
- Map arguments to specific crates, modules, and primary functions
- Collect snippets of key functions and struct definitions involved in the flow
- Record related configuration (e.g., command registrations, routing tables)
- Prepare a working outline of the anticipated call chain for validation
</input>

<workflow>
## Phase 1: Scope the Flow
- Confirm the starting command or trigger (CLI invocation, credential ingress, etc.)
- Identify likely crates/modules for the destination component
- List candidate functions and files to inspect based on parsed hints

## Phase 2: Trace Interactions
- Follow call sites using Grep to hop between functions and modules
- Read source files to understand how data or control transitions occur
- Note intermediate structures (parsers, dispatchers, handlers, UI renderers)
- Capture important arguments, return values, and state mutations along the path
- **For each step, identify what invokes it** (caller function, event trigger, async task, etc.)

## Phase 3: Validate and Prepare Summary
- Cross-check the discovered flow against project documentation or command registrations
- Fill gaps by inspecting adjacent modules or helper functions
- Ensure each step in the path connects logically from source to destination
- Highlight open questions or TODOs if parts of the flow remain uncertain

## Tools to Use:
- Read: inspect Rust source, configs, and docs
- Grep: locate function definitions and call sites
- Glob: discover relevant files by pattern
- Bash: run `cargo metadata --format-version 1` or other read-only commands for crate insights if helpful
</workflow>

<output>
## Format
- Present the trace as a numbered sequence showing data/control flow transitions
- Use concise labels of the form `Component: detail` with optional indented sub-steps
- **For each step, specify what invokes it** (e.g., "← called by X", "← triggered when Y", "← invoked via Z")
- Include short explanations of how data moves or which function handles the step

## Style
- Be direct, technical, and reference concrete symbols (functions, structs, files)
- Mention unresolved questions or forks explicitly
- Avoid excessive formatting beyond numbered lists and light indentation

## Example Output:
```
1. OS: codex login → passes args to your binary
   ← Invoked by: User typing command in terminal

2. main() → calls arg0_dispatch_or_else
   ← Invoked by: OS process initialization (entry point)
   
3. arg0_dispatch_or_else → creates codex_linux_sandbox_exe, calls your closure
   ← Invoked by: main() at line 160
   
4. closure → calls cli_main with that path
   ← Invoked by: arg0_dispatch_or_else async executor
   
5. cli_main → invokes MultitoolCli::parse() to read "login"
   ← Invoked by: closure at line 161
   
6. Login subcommand → authenticates via credentials flow
   ← Invoked by: clap parser matching "login" subcommand
```
</output>

<clarification>
## When to Ask Questions
- Parsed components have multiple plausible matches across crates or services
- The requested flow spans unimplemented or external systems
- Destructive or stateful commands would be required to verify behavior
- Input lacks either a clear source or destination component

## What to Clarify
- Exact crate or module when names repeat (e.g., `codex-rs/core` vs `codex-cli`)
- Desired depth of trace (high-level overview vs function-by-function)
- Whether to include related background such as configuration loading or feature flags
- Acceptance of inferred links when source evidence is indirect

## How to Ask
- State the ambiguity and list likely interpretations
- Recommend the option that best fits existing architecture patterns
- Use concise yes/no or numbered choices to keep the conversation efficient
</clarification>
