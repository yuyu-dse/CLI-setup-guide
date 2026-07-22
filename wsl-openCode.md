# WSL OpenCode

This guide explains how to set up and configure OpenCode on WSL.

The main setup path in this guide uses Azure AI Foundry with an Azure OpenAI resource. A generic OpenCode provider setup path is also included for other providers.

> OpenCode recommends WSL for the best Windows compatibility.

## 1. Prerequisites

Before starting, make sure you have:

- WSL
- One OpenCode installation method available: Chocolatey, Scoop, or npm
- Access to an Azure OpenAI resource
- Access to Azure AI Foundry
- A deployed model in Azure AI Foundry
- The Azure OpenAI resource name
- The Azure OpenAI API key
- The Azure AI Foundry deployment or model name

The Azure resource name, deployment name, model name, and API key should be provided by the team.

> Never store API keys, passwords, screenshots containing secrets, or any other sensitive information in this repository.

## 2. Install OpenCode

Choose one of the following installation methods.

Using install script (most simple):

```powershell
curl -fsSL https://opencode.ai/install | bash
```

Using npm (Node.js is needed to be installed as prerequisite):

```powershell
npm install -g opencode-ai
```

Using Homebrew
```powershell
brew install anomalyco/tap/opencode
```

After installation, restart your session & verify that OpenCode is available:

```powershell
source ~/.bashrc
opencode --version
```

## 3. Prepare the Azure AI Foundry Setup

For the Azure setup, you need the following values:

- Azure OpenAI resource name
- Azure OpenAI API key
- Azure AI Foundry deployment name
- Model name

The Azure OpenAI endpoint usually follows this format:

```text
https://<azure-resource-name>.openai.azure.com/
```

Use only the resource name when setting the OpenCode environment variable. For example, if the endpoint is:

```text
https://my-ai-resource.openai.azure.com/
```

then the resource name is:

```text
my-ai-resource
```

Important:

- The Azure AI Foundry deployment name should match the model name used in OpenCode.
- Confirm that the deployed model is available to your Azure OpenAI resource.
- Do not copy API keys or endpoint screenshots into this repository.

## 4. Set up conifg file

Open the config file in nano editor (or any editor of your choice)

```powershell
nano ~/.config/opencode/opencode.jsonc
```

Replace with new config, filling in your own model name & endpoint: 

```text
{
  "$schema": "https://opencode.ai/config.json",
  "model": "[Model name]",
  "theme": "opencode",
  "autoupdate": true,
  "provider": {
    "azure": {
      "options": {
        "baseURL": "[Azure OpenAI endpoint]"
      },
      "models": {
        "[Model Name]": {
          "name": "[Model name]"
        }
      }
    }
  }
}
```

Save it.

## 5. Select the Azure Model

Inside OpenCode, run:

```text
/models
```

Select the model that matches the Azure AI Foundry deployment.

Confirm that:

- the Azure provider is available;
- the deployed model appears in the model list;
- the selected model name matches the Azure AI Foundry deployment name.

## 6. Connect OpenCode to Azure

Inside OpenCode, with deployed model selected, run:

```text
/connect
```

Then:

1. Search for **Azure**.
2. Select the Azure OpenAI provider.
3. Paste the Azure OpenAI API key when prompted.

OpenCode stores provider credentials outside the project repository.

> Do not paste the API key into any Markdown file, project config file, or committed script.


## 7. Generic OpenCode Provider Setup

If you are not using Azure, the general OpenCode setup flow is:

```powershell
opencode
```

Inside OpenCode, connect a provider:

```text
/connect
```

Select the provider, then follow the authentication prompts.

Common provider options include:

- OpenCode Zen
- OpenAI
- Anthropic
- GitHub Copilot
- OpenRouter
- local or custom OpenAI-compatible providers

After connecting the provider, select a model:

```text
/models
```

The exact credentials and environment variables depend on the selected provider.

## 8. Initialize OpenCode in a Project

Navigate to the project folder:

```powershell
cd C:\path\to\project
```

Start OpenCode:

```powershell
opencode
```

Inside OpenCode, initialize the project:

```text
/init
```

This lets OpenCode analyze the project and create an `AGENTS.md` file in the project root.

The `AGENTS.md` file can be committed if it only contains project guidance and does not contain secrets.

Note: The global configurations reside in `%USERPROFILE%\.config\opencode\opencode.json` and project-level configurations reside in the project root.

## 9. Verify the Setup

After setup is complete, send a simple test prompt in OpenCode:

```text
Explain this repository structure.
```

Confirm that:

- OpenCode starts successfully;
- the Azure provider or selected provider is connected;
- the expected model is selected;
- OpenCode can successfully process a request;
- OpenCode can read project files when permitted;
- no secrets were added to the repository.

## 10. Troubleshooting

### `opencode` command not found

Close and reopen PowerShell, then try again:

```powershell
opencode --version
```

If the command is still unavailable, confirm that Chocolatey, Scoop, or npm installed OpenCode successfully and that the install location is on the Windows `PATH`.

### Chocolatey or Scoop installation fails

Company-managed devices may require administrator approval or software policy approval.

If installation is blocked, contact the administrator or use an approved installation method.

### Azure model does not appear in `/models`

Confirm that:

- the Azure OpenAI API key is valid;
- the Azure resource name is correct;
- `AZURE_RESOURCE_NAME` is set in the same PowerShell session that started OpenCode;
- the model is deployed in Azure AI Foundry;
- the deployment name matches the model name expected by OpenCode.

### Authentication fails

Reconnect the Azure provider:

```text
/connect
```

Then select Azure again and enter the API key provided by the team.

### Network or endpoint errors

Confirm that the machine can reach the Azure OpenAI endpoint.

Company proxy, VPN, or firewall rules may block the request.

### API Versioning

While OpenCode defaults to a standard version, custom enterprise deployments may reject requests if the default version is deprecated; So, If authentication succeeds but the model fails to process prompts, it may be needed to explicitly define the required Azure API version in opencode.json configuration.

### Native Windows behavior differs from WSL

Some OpenCode behavior may be more reliable in WSL. If native Windows setup is blocked by shell, terminal, or permission issues, consider testing the setup in WSL as a fallback.
