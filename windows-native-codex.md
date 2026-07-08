# Windows Native Codex

This guide explains how to set up and configure Codex natively on Windows.

> WSL and Linux setup are outside the scope of this guide. You can simply turn to [WSL Codex](./wsl-codex.md)

## 1. Prerequisites

Before starting, make sure you have:

- Windows System
- VS Code
- Codex extension for VS Code
- An Azure OpenAI endpoint
- Model name
- An API key

The Azure OpenAI endpoint, model name, and API key should be provided by the team. And it should never be leaked by any means.

> Never store API keys, passwords, or any other secret information in this repository.

## 2. Install the Codex Extension

1. Open VS Code.
2. Open the **Extensions** panel.
3. Search for **Codex**.
4. Install the extension.
5. Open the **Codex** panel.

At this stage, do not enter API key directly into the Codex login screen.

## 3. Create the Codex Configuration File

Open Windows PowerShell and check whether the Codex configuration directory exists:

```powershell
Test-Path "$HOME\.codex"
```

If the directory does not exist, create it:

```powershell
New-Item -ItemType Directory -Path "$HOME\.codex"
```

Open or create the Codex configuration file:

```powershell
notepad "$HOME\.codex\config.toml"
```

The file is located at:

```text
C:\Users\<username>\.codex\config.toml
```

Add the following configuration:

```toml
model = "<model-name>"
model_provider = "azure"

[model_providers.azure]
name = "Azure OpenAI"
base_url = "<azure-openai-base-url>"
env_key = "AZURE_OPENAI_API_KEY"
wire_api = "responses"
```

Attention:

- `<model-name>` with the model name provided by the team.
- `<azure-openai-base-url>` with the Azure OpenAI base URL provided for the setup.

Save the file.

> Do not store the API key directly in `config.toml`.

## 4. Configure the API Key

The API key should be stored in the `AZURE_OPENAI_API_KEY` environment variable.

To avoid displaying the API key directly in PowerShell, use:

```powershell
$secure = Read-Host "Paste API key" -AsSecureString
$ptr = [Runtime.InteropServices.Marshal]::SecureStringToBSTR($secure)
$env:AZURE_OPENAI_API_KEY = [Runtime.InteropServices.Marshal]::PtrToStringBSTR($ptr)
[Runtime.InteropServices.Marshal]::ZeroFreeBSTR($ptr)
```

When prompted:

```text
Paste API key:
```

paste the API key provided by the team and press **Enter**.

> This method stores the API key only in the current PowerShell session.

## 5. Start Visual Studio Code

Close all open Visual Studio Code windows.

From the same PowerShell session in which the API key was configured, start Visual Studio Code:

```powershell
code
```

Starting Visual Studio Code from the same PowerShell session allows it to inherit the `AZURE_OPENAI_API_KEY` environment variable.

## 6. Open Codex

In Visual Studio Code:

1. Open the **Codex** panel.
2. Continue with the Windows setup.
3. Follow the setup instructions shown by Codex.

Codex may request permission to install the Windows sandbox.

On company-managed devices, administrator approval may be required.

> Status: Pending final verification after administrator approval.

## 7. Verify the Setup

After the Windows setup is complete, send a simple test prompt in Codex.

Confirm that:

- the Azure endpoint is reachable;
- the configured model is available;
- the API key is recognized;
- Codex can successfully process a request;
- Codex can operate correctly in the Windows environment.

> Status: Pending final verification.


############# NOT FINISHED 
# Need authentication from Admin to Proceed