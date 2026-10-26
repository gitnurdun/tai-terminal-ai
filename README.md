# tai — terminal AI

A Bash command helper that sends a natural-language request to a chat-completions API, prints the suggested shell command and an explanation, and offers an interactive review menu. It also has a short-lived chat mode.

## Requirements

Bash, `curl`, and `jq`. By default it uses the DeepSeek chat-completions endpoint and the `deepseek-chat` model. Set `TAI_API_KEY` or `TAI_API_KEY_FILE` for authentication. `TAI_API_URL`, `TAI_MODEL`, `TAI_TIMEOUT`, and `TAI_EDITOR` can be used to customize the endpoint, model, timeout, and editor. Keep key files outside this repository and do not commit credentials.

```bash
tai "show the largest files in this directory"
tai -i
tai -chat "explain shell pipes"
cat error.log | tai "summarize this error"
```

In interactive command mode, review the proposal, then press Enter to run, `e` to edit, `c` to copy, `r` to regenerate, or `q` to quit. `--quiet` prints only the command. `--run` executes the generated command without the review prompt.

## Data and command safety

Requests include the current directory, operating system, a short listing of current-directory filenames, the prompt, and any piped input. That context is sent to the configured API. Do not pipe private data or use the tool from a sensitive directory unless you intend to send that context. The command warning check is only a heuristic; generated commands run with the user's shell privileges. Inspect each command before execution and avoid `--run` unless you explicitly want immediate execution.

No license file was supplied, so this repository does not add a license.
