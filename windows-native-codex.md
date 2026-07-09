# Windows Native Codex Setup

This guide explains how to set up Codex natively on Windows using the company-provided Azure OpenAI deployment.

Administrator access is not required for the tested setup.

## Prerequisites

You need:

- Windows
- Visual Studio Code
- Access to the target Git repository
- Company-provided Azure OpenAI endpoint
- Company-provided model name
- Company-provided API key

> Never commit API keys or include them in documentation or screenshots.

## 1. Open the Repository in Native Windows

Open the repository in a native Windows VS Code window.

The path should look like:

```text
C:\Users\<USERNAME>\projects\<REPOSITORY>
```

Do not use a WSL path such as:

```text
/home/<USERNAME>/projects/<REPOSITORY>
```

## 2. Create the Codex Configuration

Create the following file:

```text
C:\Users\<USERNAME>\.codex\config.toml
```

Add:

```toml
model = "<COMPANY_MODEL_NAME>"
model_provider = "azure"
model_reasoning_effort = "high"

[model_providers.azure]
name = "Azure OpenAI"
base_url = "<COMPANY_AZURE_OPENAI_BASE_URL>"
env_key = "AZURE_OPENAI_API_KEY"
wire_api = "responses"
```

Replace the placeholders with the values provided through the approved internal company channel.

Do not add the API key to this file.

## 3. Set the API Key

Open PowerShell and run:

```powershell
[Environment]::SetEnvironmentVariable(
    "AZURE_OPENAI_API_KEY",
    "<YOUR_API_KEY>",
    "User"
)
```

Replace `<YOUR_API_KEY>` with the real API key.

The final `"User"` is the Windows environment-variable scope. It is not your username.

## 4. Restart VS Code

After setting the environment variable:

1. Close all VS Code windows.
2. Reopen VS Code.
3. Open the native Windows repository again.

## 5. Verify the Environment Variable

Open a new PowerShell terminal in VS Code and run:

```powershell
$env:AZURE_OPENAI_API_KEY
```

If a value is displayed, the environment variable is available.

Do not include the output in screenshots.

## 6. Start Codex

Open Codex in VS Code.

If Windows setup or administrator access is unavailable, continue without completing the optional administrator-level setup.

The tested configuration works with:

- the Codex configuration file
- the company Azure OpenAI deployment
- the user-level `AZURE_OPENAI_API_KEY`

## 7. Test the Setup

Use a read-only prompt first:

```text
Briefly introduce this repository. Do not modify anything.
```

Confirm that Codex can:

- access the repository
- inspect files
- understand the project structure
- return a response without modifying files

## Troubleshooting

### Missing environment variable

If Codex reports:

```text
Missing environment variable: AZURE_OPENAI_API_KEY
```

verify the saved value:

```powershell
[Environment]::GetEnvironmentVariable(
    "AZURE_OPENAI_API_KEY",
    "User"
)
```

Then completely restart VS Code.

### Wrong environment

Make sure VS Code is running in native Windows.

The repository path should begin with:

```text
C:\
```

and not:

```text
/home/
```

or:

```text
\\wsl.localhost\
```

## Security

- Never commit API keys.
- Never include API keys in screenshots.
- Use environment variables for secrets.
- Use only the approved company Azure OpenAI deployment for company code and data.

## Result

The Windows Native Codex setup was successfully tested using the company-provided Azure OpenAI deployment.

Administrator access is not required for the tested workflow.
