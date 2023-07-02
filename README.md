# AICoder GH Action

This GitHub Action uses AICoder to automatically generate pull requests that can improve the code in your files based on the prompts you provide.

## Usage

To use this action in your GitHub workflow, you can add a step in your workflow file that uses this action.

Here is a sample step:

```yaml
- name: AICoder GH Action
  uses: AICoderHub/GH_Action
  with:
    INPUT_MODE: 'desired-mode'
    INPUT_PROMPT: 'desired-prompt'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    TEMPLATE_FILES: '/path/to/template/file1 /path/to/template/file2'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: '/path/to/file/to/modify'
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

## Examples

*The following examples use the path to a file, but note that the path can also be a folder and therefore every file inside the folder will be used.*

<details>
  <summary>Modify a code based on a custom prompt</summary>
  
**Note** that the prompt can be a string, a file path (I'll need to be inside the repo) or a URL.

```yaml
- name: AICoder GH Action
  uses: AICoderHub/GH_Action
  with:
    INPUT_MODE: 'file-enhancer'
    INPUT_PROMPT: 'https://gist.github.com/youraccount/prompt.md'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: '/path/to/file/to/modify'
```

A PR will be generated with the changes.

</details>

<details>
  <summary>Search for backdoors and security vulnerabilities</summary>

```yaml
- name: AICoder GH Action
  uses: AICoderHub/GH_Action
  with:
    INPUT_MODE: 'file-security'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: '/path/to/file/to/modify'
```

A PR will be generated with the recommended changes.

</details>


<details>
  <summary>Optimize a code</summary>

```yaml
- name: AICoder GH Action
  uses: AICoderHub/GH_Action
  with:
    INPUT_MODE: 'file-optimizer'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: '/path/to/file/to/modify'
```

A PR will be generated with the recommended changes.

</details>

<details>
  <summary>Find and fix bugs</summary>

```yaml
- name: AICoder GH Action
  uses: AICoderHub/GH_Action
  with:
    INPUT_MODE: 'file-bugfixer'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: '/path/to/file/to/modify'
```

A PR will be generated with the recommended changes.

</details>

<details>
  <summary>Add comments to a file</summary>

```yaml
- name: AICoder GH Action
  uses: AICoderHub/GH_Action
  with:
    INPUT_MODE: 'file-comments'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: '/path/to/file/to/modify'
```

A PR will be generated with the recommended changes.

</details>

<details>
  <summary>Generate a file based on other files as templates</summary>

```yaml
- name: AICoder GH Action
  uses: AICoderHub/GH_Action
  with:
    INPUT_MODE: 'file-generator'
    INPUT_PROMPT: 'https://gist.github.com/youraccount/prompt.md'
    INPUT_API_KEY: ${{ secrets.OPENAI_API_KEY }}
    INPUT_MODEL: 'gpt-4'
    TEMPLATE_FILES: '/path/to/template/file1 /path/to/template/file2'
    ORIGIN_BRANCH: 'aicoder'
    TO_BRANCH: 'main'
    CHECK_PATH: '/path/to/file/to/create'
```

A PR will be generated with the recommended changes.

</details>