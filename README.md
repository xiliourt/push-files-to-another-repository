# github-action-push-to-another-repository

Used to push generated files from a directory from Git Action step into another repository on Github.

E.g.
Repository pandoc-test contains Markdown and a Git Action to generate, using Pandoc, an output: HTML, PDF, odt, epub, etc.

Repository pandoc-test-output: contains only the generated files from the first Git Action. Pushed here with github-action-push-to-another-repository

And pandoc-test-output can have Git Pages to give access to the files (or just links to the raw version of the files)

## Inputs
### `source-files` (argument)
From the repository that this Git Action is executed the files to be pushed into the repository. This argument supports multiple space-separated filenames and globbing.

### `destination-directory` (argument) [optional]
The directory in the destination repository to copy the source files into.

### `destination-github-username` (argument)
For the repository `https://github.com/nkoppel/push-to-another-repository-output` is `nkoppel`. It's also used for the `Author:` in the generated git messages.

### `destination-repository-name` (argument)
For the repository `https://github.com/nkoppel/push-to-another-repository-output` is `push-to-another-repository-output`

### `user-email` (argument)
The email that will be used for the commit in the destination-repository-name.

### `destination-repository-username` (argument) [optional]
The Username/Organization for the destination repository, if different from `destination-github-username`. For the repository `https://github.com/nkoppel/push-to-another-repository-output` is `nkoppel`.

### `target-branch` (argument) [optional]
The branch name for the destination repository, if different from `master`.

### `commit-message` (argument) [optional]
The commit message to be used in the output repository. Optional and defaults to "Update from $REPOSITORY_URL@commit".

The string `ORIGIN_COMMIT` is replaced by `$REPOSITORY_URL@commit`.

### `API_TOKEN_GITHUB` (environment)
E.g.:
  `API_TOKEN_GITHUB: ${{ secrets.API_TOKEN_GITHUB }}`

Generate your personal token following the steps:
* Go to the Github Settings (on the right hand side on the profile picture)
* On the left hand side pane click on "Developer Settings"
* Click on "Personal Access Tokens" (also available at https://github.com/settings/tokens)
* Generate a new token, choose "Repo". Copy the token.

Then make the token available to the Github Action following the steps:
* Go to the Github page for the repository that you push from, click on "Settings"
* On the left hand side pane click on "Secrets"
* Click on "Add a new secret" and name it "API_TOKEN_GITHUB"

## Example usage
```yaml
      - name: Pushes to another repository
        uses: nkoppel/push-files-to-another-repository@master
        env:
          API_TOKEN_GITHUB: ${{ secrets.API_TOKEN_GITHUB }}
        with:
          source-files: 'output/*'
          destination-github-username: 'nkoppel'
          destination-repository-name: 'pandoc-test-output'
          user-email: nathankoppel0@gmail.com
```
