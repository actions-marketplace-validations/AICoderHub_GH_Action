# AICoder GH Action

This GitHub Action uses AICoder to automatically generate pull requests that can improve the code in your files based on the prompts you provide.

## Usage

To use this action in your GitHub workflow, you can add a step in your workflow file that uses this action.

Here is a sample step:

```yaml
- name: AICoder GH Action
  uses: AICoderHub/aicoder-gh-action@<version>
  with:
    INPUT_MODE: 'desired-mode'
    INPUT_PROMPT: 'desired-prompt'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    TEMPLATE_FILES: '/path/to/template/file1 /path/to/template/file2'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: ''/path/to/file/to/modify'
```

The allowed modes are: `file-enhancer`, `file-generator`, `file-security`, `file-optimizer`, `file-comments`, `file-bugfixer`.

## Requirements

The **`GITHUB_TOKEN`** must be enabled with **write** permissions and **Pull request** create permissions for the actions to properly work.

## Inputs
The action takes the following inputs:

- `INPUT_MODE` (required): The mode of operation.
- `INPUT_PROMPT` (optional): The prompt for the AI.
- `INPUT_API_KEY` (required): Your OpenAI API Key. For security, please store this as a secret in your repository.
- `INPUT_MODEL` (optional): The model to use for AI.
- `TEMPLATE_FILES` (optional): The template files for file-generator mode.
- `ORIGIN_BRANCH` (required): The origin branch to checkout.
- `TO_BRANCH` (required): The branch to commit changes.
- `CHECK_PATH` (optional): The file/folder path to check and apply changes.

*Only one of `CHECK_PATH` or `TEMPLATE_FILES` must be provided.*