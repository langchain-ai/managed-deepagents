# Managed Deep Agents

Build and deploy production-ready deep agents on managed LangSmith infrastructure.

## Quickstart

### Python

```bash
uv tool install managed-deepagents
mda init my-agent
cd my-agent
uv sync
mda dev .
```

### TypeScript

```bash
npm install -g managed-deepagents
mda init my-agent
cd my-agent
npm install
mda dev .
```

Add your LangSmith and model provider API keys to the generated `.env` file. When the agent is ready, deploy it:

```bash
mda deploy .
```

For the complete walkthrough, see the [Managed Deep Agents quickstart](https://docs.langchain.com/langsmith/python/managed-deep-agents-quickstart).

## Documentation

- [Overview](https://docs.langchain.com/langsmith/python/managed-deep-agents-overview)
- [Project structure](https://docs.langchain.com/langsmith/python/managed-deep-agents-project-structure)
- [CLI reference](https://docs.langchain.com/langsmith/python/managed-deep-agents-cli)
- [Deploy an agent](https://docs.langchain.com/langsmith/python/managed-deep-agents-deploy)

## Project status

Managed Deep Agents is in public beta and available on LangSmith Cloud in the US region.

The Managed Deep Agents SDK is not open source during the beta. This repository is the public landing page and issue tracker for the project.

## Report an issue

Use [GitHub Issues](../../issues) to report SDK or CLI bugs and request features.

When reporting a bug, include:

- Your `managed-deepagents` version.
- Your language and runtime version.
- The command you ran.
- The complete error message or relevant logs.
- A minimal reproduction, when possible.

Do not include API keys, credentials, private agent instructions, or other sensitive information.

For documentation problems, [file an issue in the LangChain documentation repository](https://github.com/langchain-ai/docs/issues).