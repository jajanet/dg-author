# Dotguides Author Extension

The Dotguides Author extension is a Gemini CLI extension designed to help library maintainers automatically generate high-quality `.guides` content. By analyzing your repository and gathering specific context, it automates the creation of LLM-friendly documentation that improves the accuracy of coding agents using your library.

## What is Dotguides?

Dotguides is a system for shipping high-quality LLM guidance directly inside open-source packages.
* **Simple:** Content is just Markdown files in a `.guides` folder.
* **Token-efficient:** Aggregates guidance across dependencies to keep context compact.
* **Trustworthy:** Guidance is versioned and delivered alongside the package itself.

For more details on the Dotguides specification, see the [main Dotguides repository](https://github.com/google/dotguides).


## Features

* **Automated Repo Analysis**: Scans your codebase, `package.json`, and existing documentation to infer public API usage and structure.
* **Interactive Planning**: Guides you through a "Guidance Architect" workflow to capture core purpose, audience, and versioning policies.
* **Documentation Discovery**: Uses the `context7` MCP server to fetch and synthesize information from external documentation URLs.
* **Performance Comparison**: Includes tools to compare the latency and token usage of tasks performed with and without Dotguides.

## Prerequisites

* **Gemini CLI**: Version 0.4.0 or newer.
* **Context7 API Key**: This extension utilizes the `@upstash/context7-mcp` server which requires an API key, which is in `gemini-extension.json`

## Installation

Install the Author extension by running the following command from your terminal:

```bash
gemini extensions install [https://github.com/jajanet/dg-author](https://github.com/jajanet/dg-author)
```

If doing development locally on the author extension itself:

```bash
gemini extensions install your/local/authoring-ext/path
```

## Usage

This extension adds several commands to your Gemini CLI environment to assist in the authoring process.

### `/dotguides/author-v2`
The primary entry point for creating new guides. This command initiates the "Guidance Architect" workflow, which:
1.  Researches your library via a provided URL.
2.  Interactively drafts core files (`usage.md`, `setup.md`, `style.md`) inside your terminal.
3.  Generates a `DOTGUIDES.md` plan and deploying the `.guides` folder upon approval.

### `/dotguides/author`
A legacy workflow that analyzes the repository to create a `DOTGUIDES_PLAN.md`. It focuses on capturing a concise "Purpose Block" and analyzing code structure (entry points, build scripts, etc.) to minimize token usage for agents.

### `/context7-total`
Runs a full documentation discovery process using the `context7` MCP server. It searches for the best matching library documentation, retrieves it, and creates a plan to implement the `.guides` folder based on external findings.

### `/compare-guides-vs-reg-lookup`
A utility command to benchmark the effectiveness of your guides. It runs a specified task twice—once using your `.guides` and once using a standard lookup—and outputs a table comparing token usage, latency, and task success.
