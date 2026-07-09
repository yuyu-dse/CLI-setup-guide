# Coding Agent CLI Setup Guide

This repository contains setup guides for coding agents used with the company-provided Azure OpenAI deployment.

The goal is to document reproducible installation and configuration procedures across different development environments, with a focus on CLI-based coding agents.

## Available Guides

### WSL / Ubuntu

- [`wsl-opencode.md`](./wsl-opencode.md)

  Installation and configuration of OpenCode CLI inside WSL / Ubuntu.

- [`wsl-codex.md`](./wsl-codex.md)

  Installation and configuration notes for Codex in  WSL / Ubuntu.

### Windows Native

- [`windows-native-codex.md`](./windows-native-codex.md)

  Installation and configuration of Codex in native Windows.

- [`windows-native-opencode.md`](./windows-native-opencode.md)

  Installation and configuration notes for OpenCode in native Windows.

## Azure OpenAI Configuration

The coding agents documented in this repository use the company-provided Azure OpenAI deployment.

The required configuration may include:

- Azure OpenAI endpoint
- Azure model or deployment name
- Azure OpenAI API key

The exact endpoint, deployment name, and API key must be obtained through the approved internal company channel.

Do not store secrets directly in this repository.

## Security Notes

- Never commit API keys to Git.
- Never add API keys directly to documentation.
- Never include API keys in screenshots.
- Store secrets using environment variables or another approved secret-management method.
- Use only the company-provided Azure OpenAI deployment for company code and company data.
- Review `git diff` before committing changes.

## Repository Structure

```text
.
├── README.md
├── wsl-codex.md
├── wsl-opencode.md
├── windows-native-codex.md
└── windows-native-opencode.md 

