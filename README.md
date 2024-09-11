# Setting Up Local AI Models with Continue.dev in VS Code

This guide explains how to install and use local AI models with the Continue.dev extension in Visual Studio Code in linux operating system. By following these steps, you will be able to run AI models locally on your machine, connect them with Continue.dev, and enhance your coding experience.

## Prerequisites

- **Visual Studio Code**: Make sure you have the latest version installed.
- **Ollama**: A local AI model runner.
- **Continue.dev Extension**: Available on the Visual Studio Code Marketplace.

## Step 1: Install Ollama

Ollama allows you to run various AI models locally. 

1. **Open a terminal** and run the following command to install Ollama:

    ```bash
    curl -fsSL https://ollama.com/install.sh | sh
    ```

2. **Follow the on-screen instructions**. You may need to provide your sudo password to complete the installation.

3. **Verify the installation** by running:

    ```bash
    ollama --version
    ```

   This should display the version of Ollama installed on your machine.

## Step 2: Install and Run a Local AI Model

1. **Choose a model** from the [Ollama library](https://ollama.com/library). For this example, we'll use the "CodeQwen" model. 

2. **Pull the desired model** to run locally:

    ```bash
    ollama pull codeqwen
    ```

3. **Run the model** with Ollama:

    ```bash
    ollama run codeqwen
    ```

   This command will start the Ollama service and run the CodeQwen model locally on `http://localhost:11434`.

## Step 3: Install the Continue.dev Extension in VS Code

1. **Open Visual Studio Code**.

2. **Install the Continue.dev extension**:
   - Go to the **Extensions** view by clicking on the Extensions icon in the sidebar or pressing `Ctrl+Shift+X`.
   - Search for "Continue.dev".
   - Click **Install**.

3. **Restart VS Code** to make sure the extension is fully integrated.

## Step 4: Configure Continue.dev to Use the Local AI Model

1. **Create or edit the `config.json` file** for Continue.dev:

   - The configuration file is usually located at `~/.continue/config.json`. Create this file if it does not exist.

2. **Copy and paste the following configuration** into the `config.json` file:

    ```json
    {
      "models": [
        {
          "model": "AUTODETECT",
          "title": "Ollama",
          "provider": "ollama",
          "apiBase": "http://localhost:11434"
        }
      ],
      "customCommands": [
        {
          "name": "test",
          "prompt": "{{{ input }}}\n\nWrite a comprehensive set of unit tests for the selected code. It should setup, run tests that check for correctness including important edge cases, and teardown. Ensure that the tests are complete and sophisticated. Give the tests just as chat output, don't edit any file.",
          "description": "Write unit tests for highlighted code"
        }
      ],
      "tabAutocompleteModel": {
        "title": "Tab Autocomplete Model",
        "provider": "ollama",
        "model": "starcoder2:3b",
        "apiBase": "http://localhost:11434"
      },
      "contextProviders": [
        {
          "name": "code",
          "params": {}
        },
        {
          "name": "docs",
          "params": {}
        },
        {
          "name": "diff",
          "params": {}
        },
        {
          "name": "terminal",
          "params": {}
        },
        {
          "name": "problems",
          "params": {}
        },
        {
          "name": "folder",
          "params": {}
        },
        {
          "name": "codebase",
          "params": {}
        }
      ],
      "slashCommands": [
        {
          "name": "edit",
          "description": "Edit selected code"
        },
        {
          "name": "comment",
          "description": "Write comments for the selected code"
        },
        {
          "name": "share",
          "description": "Export the current chat session to markdown"
        },
        {
          "name": "cmd",
          "description": "Generate a shell command"
        },
        {
          "name": "commit",
          "description": "Generate a git commit message"
        }
      ]
    }
    ```

3. **Save the `config.json` file**.

## Step 5: Use Continue.dev in VS Code

1. **Open a project** in Visual Studio Code where you want to use Continue.dev.

2. **Activate Continue.dev**:
   - Open the **Command Palette** by pressing `Ctrl+Shift+P`.
   - Type **"Continue.dev"** and select **"Start Continue.dev Session"**.

3. **Use Commands and Features**:
   - You can now use the commands defined in your `config.json` file. For example, you can use the `/test` command to generate unit tests for your code.

## Step 6: Find the Best Free Models

To find the best ranking free models, you can use [EvalPlus's leaderboard](https://evalplus.github.io/leaderboard.html) to compare different models based on their performance and features.

## Step 7: Verify the Integration

1. **Test the integration** by running a simple command in Continue.dev and verifying that it uses the local model.
   
2. **Check the logs** for Ollama and Continue.dev to make sure there are no errors:

   - For **Ollama**, use:
     ```bash
     sudo journalctl -u ollama -f
     ```
   - For **Continue.dev**, look for any output or logs in the VS Code terminal.

## Troubleshooting

- **500 Internal Server Error**: Ensure the `apiBase` in `config.json` is set to `http://localhost:11434` and that Ollama is running.
- **Model Not Found**: Verify that the model name in Ollama matches exactly with the model you downloaded.
- **Connection Issues**: Confirm there are no firewall or network restrictions preventing communication to `127.0.0.1:11434`.

By following these steps, you can set up a local AI model with Ollama and use it seamlessly in VS Code with the Continue.dev extension!

## Conclusion

With the local AI model setup, you can now leverage powerful AI tools directly within your coding environment, enhancing your productivity and coding experience.

---

Feel free to reach out if you have any questions or need further assistance!
