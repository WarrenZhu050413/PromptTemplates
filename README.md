# PromptTemplates

A collection of custom prompt templates and commands for Claude Code CLI.

## Overview

This repository contains reusable prompt templates organized by category:
- **Analysis**: Templates for code analysis, codebase learning, and feature tracing
- **Implementation**: Templates for code generation and modifications
- **Planning**: Templates for project planning and query generation
- **Utility**: General utility templates for various tasks
- **Workflow**: Templates for complex workflows and automation

## Structure

Templates follow the naming convention: `global::<category>::<template-name>.md`

Each template contains structured prompts that can be invoked through Claude Code CLI to perform specific tasks consistently.

## Usage

These templates are designed to work with Claude Code CLI's command system. Place them in your `~/.claude/commands/` directory to use them.

## Categories

### Analysis
- `analyze-file`: Analyze individual files
- `codebase-onboarding`: Onboard to new codebases
- `feature-check`: Check for specific features
- `learn-codebase`: Deep dive into codebase structure
- `learn-pattern`: Learn coding patterns
- `pdf-academic-summary`: Summarize academic PDFs
- `trace-feature`: Trace feature implementations

### Implementation
- `add-pedagogical-comments`: Add educational comments to code

### Planning
- `generate-queries`: Generate search queries for tasks

### Utility
- `add-calendar-event`: Add events to calendar
- `add-permissions`: Add file permissions
- `agent-system-prompt`: System prompts for agents
- `codex`: Codex integration
- `day-summary`: Daily summaries
- `feature-request`: Feature request templates
- `setup-local-config`: Local configuration setup
- `socratic`: Socratic method prompts
- `tomorrow-summary`: Tomorrow's task summary
- `tool-summary`: Tool usage summaries
- `tutoring-report`: Tutoring session reports
- `update-docs`: Documentation updates
- `work-journal`: Work journal entries

### Workflow
- `check-email`: Email checking workflow
- `coursework-todo`: Coursework task management
- `infinite-orchestrator`: Complex orchestration workflow
- `track-assignment`: Assignment tracking
- `web-research`: Web research workflow