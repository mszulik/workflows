# Workflows

This repository stores GitHub Action workflow files for reuse. Check below for explanations for each workflow.

A workflow that uses another workflow is referred to as a "caller" workflow. The reusable workflow is a "called" workflow.

## Usage

### General

To call a reusable workflow, define a job without steps and reference the workflow file in the `uses` keyword:

```yml
jobs:
  your-job-name:
    name: A concise name for your job
    uses: username/repository/.github/workflows/workflow.yml@main
```

If a reusable workflow expects `Inputs` and `Secrets`, they can be passed like this:

```yml
...
    uses: the/path/to/your/workflow/file.yml@main
    with:
      an-input: 1234
    secrets:
      a-multiline-secret: |
        SECRET1="${{ secrets.SECRET1 }}"
        SECRET2="${{ secrets.SECRET2 }}"
      another-secret: ${{ secrets.SECRET3 }}
```

> [!NOTE]
> 
> `Inputs` are non-sensitive variables of the type boolean, number or string.
> 
> `Secrets` are sensitive variables which will not be shown in workflow logs.
>
> A multiline secret can be used to pass an arbitrary amount of secrets to a called workflow, e.g. env variables. 

If all required `Secrets` are already in any secret store, they can be inherited to the called workflow:

```yml
...
    secrets: inherit
```

As soon as one `Secret` is explicitly specified, all other `Secrets` also have to be specified. 

### Docker Build & Push



### PullPreview

## Development
