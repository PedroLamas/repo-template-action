# pedrolamas/handlebars-action

[![Project Maintenance](https://img.shields.io/maintenance/yes/2022.svg)](https://github.com/pedrolamas/handlebars-action 'GitHub Repository')
[![License](https://img.shields.io/github/license/pedrolamas/handlebars-action.svg)](https://github.com/pedrolamas/handlebars-action/blob/master/LICENSE 'License')

[![CI](https://github.com/pedrolamas/handlebars-action/workflows/CI/badge.svg)](https://github.com/pedrolamas/handlebars-action/actions 'Build Status')

[![Twitter Follow](https://img.shields.io/twitter/follow/pedrolamas?style=social)](https://twitter.com/pedrolamas '@pedrolamas')

**Transform files in your repository with Handlebars templating!**

This action will find files in the repository matching a specific search spec and process them as [Handlebars](https://handlebarsjs.com) templates, writing the transformed content back to the same file or a new one.

Templates can use the full expression syntax of Handlebars, including the built-in helpers.

## Usage

```yaml
- uses: pedrolamas/handlebars-action
  with:
    # Files to process
    # Default: '**/*.template'
    files: '**/*.template'

    # Output filename template
    # Default: '{{ file.dir }}/{{ file.name }}'
    output-filename: '{{ file.dir }}/{{ file.name }}'

    # Remove the input file
    # Default: false
    delete-input-file: true

    # HTML escape the rendered values
    # Default: false
    html-escape: false

    # Makes no real changes
    # default: false
    dry-run: false
```

## Available tags

### Environment variables

- `{{ env.[name] }}` - The value of the environment variable called `[name]`. For example, `{{ env.GITHUB_REPOSITORY }}` will return the value of the `$GITHUB_REPOSITORY` environment variable.

### Input file

- `{{ file.path }}` - The full path of the input file used as template.
- `{{ file.root }}` - The root of the input file path such as '/' or 'c:\'.
- `{{ file.dir }}` - The full directory path of the input file such as '/home/user/dir' or 'c:\path\dir'.
- `{{ file.base }}` - The input file name including extension (if any) such as 'index.html'.
- `{{ file.ext }}` - The input file extension (if any) such as '.html'.
- `{{ file.name }}` - The input file name without extension (if any) such as 'index'.

### Output file

- `{{ outputFile.path }}` - The full path of the output file used as template.
- `{{ outputFile.root }}` - The root of the output file path such as '/' or 'c:\'.
- `{{ outputFile.dir }}` - The full directory path of the output file such as '/home/user/dir' or 'c:\path\dir'.
- `{{ outputFile.base }}` - The output file name including extension (if any) such as 'index.html'.
- `{{ outputFile.ext }}` - The output file extension (if any) such as '.html'.
- `{{ outputFile.name }}` - The output file name without extension (if any) such as 'index'.

### GitHub context

- `{{ github.action }}` - The name of the action currently running, or the [id](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobsjob_idstepsid) of a step. For example, for an action, `__repo-owner_name-of-action-repo`.
- `{{ action_path }}` - The path where an action is located.
- `{{ action_repository }}` - For a step executing an action, this is the owner and repository name of the action. For example, `actions/checkout`.
- `{{ github.actor }}` - The name of the person or app that initiated the workflow. For example, `octocat`.
- `{{ github.api_url }}` - Returns the API URL. For example: `https://api.github.com`.
- `{{ github.base_ref }}` - Only set for forked repositories. The branch of the base repository.
- `{{ github.env }}` - The path on the runner to the file that sets environment variables from workflow commands.
- `{{ github.event_name }}` - The name of the webhook event that triggered the workflow.
- `{{ github.event_path }}` - The path of the file with the complete webhook event payload. For example, `/github/workflow/event.json`.
- `{{ github.graphql_url }}` - Returns the GraphQL API URL. For example: `https://api.github.com/graphql`.
- `{{ github.head_ref }}` - Only set for forked repositories. The branch of the head repository.
- `{{ github.job }}` - The [job_id](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#jobsjob_id) of the current job. For example, `greeting_job`.
- `{{ github.path }}` - The path on the runner to the file that sets system PATH variables from workflow commands.
- `{{ github.ref }}` - The branch or tag ref that triggered the workflow. For example, `refs/heads/feature-branch-1`. If neither a branch or tag is available for the event type, the variable will not exist.
- `{{ github.ref_name }}` - The branch or tag name that triggered the workflow run. For example, `feature-branch-1`.
- `{{ github.ref_protected }}` - `true` if branch protections are configured for the ref that triggered the workflow run.
- `{{ github.ref_type }}` - The type of ref that triggered the workflow run. Valid values are `branch` or `tag`.
- `{{ github.repository }}` - The owner and repository name. For example, `octocat/Hello-World`.
- `{{ github.repository_name }}` - The repository name. For example, `Hello-World`.
- `{{ github.repository_owner }}` - The repository owner's name. For example, `octocat`.
- `{{ github.retention_days }}` - The number of days that workflow run logs and artifacts are kept. For example, `90`.
- `{{ github.run_attempt }}` - A unique number for each attempt of a particular workflow run in a repository. This number begins at 1 for the workflow run's first attempt, and increments with each re-run. For example, `3`.
- `{{ github.run_id }}` - A unique number for each run within a repository. This number does not change if you re-run the workflow run.
- `{{ github.run_number }}` - A unique number for each run of a particular workflow in a repository. This number begins at 1 for the workflow's first run, and increments with each new run. This number does not change if you re-run the workflow run.
- `{{ github.server_url }}` - Returns the URL of the GitHub server. For example: `https://github.com`.
- `{{ github.sha }}` - The commit SHA that triggered the workflow. For example, `ffac537e6cbbf934b08745a378932722df287a53`.
- `{{ github.workflow }}` - The name of the workflow.
- `{{ github.workspace }}` - The GitHub workspace directory path. The workspace directory is a copy of your repository if your workflow uses the actions/checkout action. If you don't use the actions/checkout action, the directory will be empty. For example, `/home/runner/work/my-repo-name/my-repo-name`.
- `{{ github.runner_arch }}` - The architecture of the runner executing the job. Possible values are `X86`, `X64`, `ARM`, or `ARM64`.
- `{{ github.runner_name }}` - The name of the runner executing the job. For example, `Hosted Agent`.
- `{{ github.runner_os }}` - The operating system of the runner executing the job. Possible values are `Linux`, `Windows`, or `macOS`.
- `{{ github.runner_temp }}` - The path to a temporary directory on the runner. For example, `D:\a\_temp`.
- `{{ github.runner_tool_cache }}` - The path to the directory containing preinstalled tools for GitHub-hosted runners. For example, `C:\hostedtoolcache\windows`.

### Misc

- `{{ date }}` - The current date as output from `new Date().toString()`.

## License

MIT
