# Contribution to Enmeshed

You can contribute to Enmeshed with issues and PRs. Simply filing issues for problems you encounter is a great way to contribute. Contributing bug fixes or features is greatly appreciated. You can have a look at already filed bugs or feature requests in our [feedback repository](https://github.com/nmshd/feedback/issues) to get started.

## Reporting Issues

We always welcome bug reports, API proposals, feature requests and overall feedback. Here are a few tips on how you can make reporting your issue as effective as possible.

### Identify Where to Report

The Enmeshed codebase is distributed across multiple repositories in the [nmshd organization](https://github.com/nmshd). But since it might be difficult to identify the correct repository your bug is related to, we introduced our [feedback repository](https://github.com/nmshd/feedback/issues), where you can centrally raise issues.

### Finding Existing Issues

Before filing a new issue, please search our [open issues](https://github.com/nmshd/feedback/issues) to check if it already exists.

If you do find an existing issue, please include your own feedback in the discussion. Do consider upvoting (👍 reaction) the original post, as this helps us prioritize popular issues in our backlog.

### Writing a Good Bug Report

Good bug reports make it easier for maintainers to verify and root cause the underlying problem. The better a bug report, the faster the problem will be resolved. Ideally, a bug report should contain the following information:

- A high-level description of the problem.
- A _minimal reproduction_, i.e. the smallest size of code/configuration required to reproduce the wrong behavior.
- A description of the _expected behavior_, contrasted with the _actual behavior_ observed.
- Information on the environment (where applicable): OS/distro, CPU arch, SDK version, etc.
- Used Enmeshed components (App, Connector), Enmeshed Component/Runtime/SDK version(s)
- Additional information, e.g. is it a regression from previous versions? Are there any known workarounds?

When ready to submit a bug report, please use the [Bug Report issue template](https://github.com/nmshd/feedback/issues/new?assignees=&labels=bug&template=bug_report.md&title=%5BBUG%5D+).

#### Why are Minimal Reproductions Important?

A reproduction lets maintainers verify the presence of a bug, and diagnose the issue using a debugger. A _minimal_ reproduction is the smallest possible console application demonstrating that bug. Minimal reproductions are generally preferable since they:

1. Focus debugging efforts on a simple code snippet,
2. Ensure that the problem is not caused by unrelated dependencies/configuration,
3. Avoid the need to share production codebases.

#### Are Minimal Reproductions Required?

In certain cases, creating a minimal reproduction might not be practical (e.g. due to nondeterministic factors, external dependencies). In such cases you would be asked to provide as much information as possible, for example what you did exactly before the application ran into an error. If maintainers are unable to root cause the problem, they might still close the issue as not actionable. While not required, minimal reproductions are strongly encouraged and will significantly improve the chances of your issue being prioritized and fixed by the maintainers.

#### How to Create a Minimal Reproduction

The best way to create a minimal reproduction is gradually removing code and dependencies from a reproducing app, until the problem no longer occurs. A good minimal reproduction:

- Excludes all unnecessary types, methods, code blocks, source files, dependencies (npm, nuget, ...) and project configurations.
- Contains documentation or code comments illustrating expected vs actual behavior.
- If possible, avoids performing any unneeded IO or system calls.

## Contributing Changes

Project maintainers will merge changes that improve the product significantly.

Maintainers will not merge changes that have narrowly-defined benefits, due to compatibility risk. Companies are building products on top of Enmeshed. We may revert changes if they are found to be breaking.

### DOs and DON'Ts

Please do:

- **DO** follow our coding style. These are enforced by prettier as well as ESlint, which are executed by our CI-pipelines.
- **DO** include tests when adding new features. When fixing bugs, start with adding a test that highlights how the current behavior is broken.
- **DO** keep the discussions focused. When a new or related topic comes up it's often better to create new issue than to side track the discussion.
- **DO** blog and tweet (or whatever) about your contributions, frequently!

Please do not:

- **DON'T** make PRs for style changes.
- **DON'T** surprise us with big pull requests. Instead, file an issue and start a discussion so we can agree on a direction before you invest a large amount of time.
- **DON'T** commit code that you didn't write. If you find code that you think is a good fit to add to Enmeshed, file an issue and start a discussion before proceeding.
- **DON'T** submit PRs that alter licensing related files or headers. If you believe there's a problem with them, file an issue and we'll be happy to discuss it.

### Breaking Changes

Contributions must maintain API signature and behavioral compatibility. Contributions that include breaking changes will be rejected for the current release and can only be considered for the next major release. Please file an issue to discuss your idea or change if you believe that it may affect compatibility.

### Suggested Workflow

We use and recommend the following workflow:

1. Create an issue for your work.
   - You can skip this step for trivial changes.
   - Reuse an existing issue on the topic, if there is one.
   - Get agreement from the team and the community that your proposed change is a good one.
   - Clearly state that you are going to take on implementing it, if that's the case.
2. Create a personal fork of the repository on GitHub (if you don't already have one).
3. In your fork, create a branch off of main (if your change affects the current version) or the release-branch you want to contribute to (if you want to contribute to a future release).
   - Name the branch according to our [branching guide](#branching-guide).
   - Branches are useful since they isolate your changes from incoming changes from upstream. They also enable you to create multiple PRs from the same fork.
4. Make and commit your changes to your branch.
   - You can run static code checks by running `npm run lint`.
   - You can run tests locally by running `npm run test:local:node`.
   - Please follow our [Commit Messages](#commit-messages) guidance.
5. Add new tests corresponding to your change, if applicable.
6. Build the repository with your changes.
   - Make sure that the builds are clean.
   - Make sure that the tests are all passing, including your new tests.
7. Make sure your branch has all changes from the main/release branch of the source repository.
8. Increment the npm package version in the package.json (adhere to [semantic versioning](https://semver.org/)). Run `npm i` to make sure the change is propagated to package-lock.json.
9. Create a pull request (PR) against the repository's **main** branch or the **release/\*** branch of the release you want to contribute to.
   - State in the description what issue or improvement your change is addressing (write `closing nmshd/feedback#<issue-id>` in a separate line).
   - Check if all the continuous integration checks are passing.
10. Wait for feedback or approval of your changes from the team.
11. When the PR is approved and all checks are green, your PR will be merged by the team.
    - This will automatically trigger our continuous deployment pipeline, which builds and publishes a new version.
    - You can delete the branch you used for making the change.

### Branching Guide

Branches must match the following pattern:

```text
<type>/<description>
```

- `<type>`: must be one of `chore`, `feature` or `bugfix`
- `description`: concise description of the changes

### Commit Messages

Please format commit messages as follows:

```text
<type>: Summary of the change

Optionally provide more detail after the first line. Leave one blank line below the summary.
```

- `<type>`: must be one of `chore`, `feat`, `fix`, `refactor`, `test`

Also do your best to factor commits appropriately, not too large with unrelated things in the same commit, and not too small with the same small change applied N times in N different commits.

### PR - CI Process

The Enmeshed continuous integration (CI) pipeline will automatically perform the required builds and run tests (static code checks as well as unit/integration tests) for PRs. Every step of the CI process needs to succeed before the PR can be merged.

### PR Feedback

One or more Enmeshed team members will review every PR prior to merge.

There are lots of thoughts and [approaches](https://github.com/antlr/antlr4-cpp/blob/master/CONTRIBUTING.md#emoji) for how to efficiently discuss changes. It is best to be clear and explicit with your feedback. Please be patient with people who might not understand the finer details about your approach to feedback.

## Code of Conduct

Enmeshed has a [Code of Conduct](/CODE_OF_CONDUCT.md) to which all contributors must adhere.
