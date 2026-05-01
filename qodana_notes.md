# Qodana Cloud exploration notes - raw observations

I registered in Qodana Cloud using GitHub.

## Authentication and account creation

On the first screen, Qodana Cloud shows a “Log in with JetBrains Account” button. The product uses JetBrains Account for authentication.

JetBrains Account supports multiple login and registration methods:

- Google
- GitHub
- Apple
- GitLab
- WeChat
- Bitbucket
- Email

When I clicked “Create an account”, the page looked almost the same as the login page. The main difference was the text: the login page says “Log in”, and the registration page says “Create an account”. The available authentication methods looked the same.

After login/registration, Qodana Cloud showed Terms of Service. There was a checkbox for receiving Qodana educational materials and news. The user can accept and continue or decline.

## Trial and account deletion observations

After I deleted my account and tried to log in again using the JetBrains Account, Qodana showed a message that a trial license had already been used for my JetBrains Account organization. The page offered two options: buy a license or learn how to join an existing organization.

I am not sure if this is expected behavior or a bug, but it is important for onboarding because account deletion can block a user from continuing with the same organization/trial.

I also tried logging in again in incognito mode using a Google account. In that case, the trial setup worked again. This may be expected if trials are account-based, but it could also be a possible risk if users can repeatedly get trial access with different accounts.

## Organization setup

During setup, Qodana asks the user to select a country and enter an organization name.

After organization setup, Qodana asks: “Do you want to run Qodana locally or set it up in your CI/CD pipeline?”

The page shows several options:

- Run locally
- Set it up in your CI/CD pipeline
- Not ready yet? View demo projects
- Skip this step and set up later

## Demo projects

I opened “View demo projects”.

The demo project page shows samples by programming language. Available tabs include:

- Go
- JavaScript
- .NET
- Java
- PHP
- Python

The page also says that Qodana supports over 20 languages and 7 linters. There is a “More about Linters” link that opens Qodana documentation. I do not think this documentation page should be a main test flow, because it is informational and not a core product workflow, but it can be noted as part of navigation.

On the demo samples page, each project card shows useful summary information:

- project name
- branch
- date/time of analysis
- number of problems
- coverage status
- license audit / suspicious licenses status

Examples I saw:

- Go / kubernetes: 31K problems, coverage not enabled, 237 suspicious licenses.
- Go / moby: 4K problems, coverage not enabled, 410 suspicious licenses.
- JavaScript / keystone: 2K problems, coverage not enabled, no suspicious licenses.
- JavaScript / express: 291 problems, 100% lines covered, no suspicious licenses.

## Demo report page

I opened a demo report, for example the Go/kubernetes sample.

The report page shows:

- current problems
- baseline problems
- inspections
- license audit status
- code coverage status
- total problems count
- total files count
- filters by files/folders, severity, category, type, and tags
- grouping by file
- an option to move selected problems to baseline
- a list of problems with category and type

Some examples of problems shown in the report:

- hardcoded password detected
- deprecated element
- unused constant
- redundant type conversion
- redundant import alias
- unused global variable
- unhandled error

The page also shows that the user is viewing Demo mode.

## Run locally setup flow

I checked the “Run locally” setup flow.

In the “Run locally” flow, there are two options:

- CLI
- JetBrains IDE

In the CLI option, Qodana shows installation instructions:

- install Qodana CLI with Homebrew on macOS/Linux
- alternatively install using a curl installer
- run analysis using a `QODANA_TOKEN` and `qodana scan`
- wait until results appear in Qodana Cloud

In the JetBrains IDE option, Qodana shows that the user needs a JetBrains IDE version 2023.2 or newer.

The IDE flow says:

- open the Problems tool window
- open the Qodana tab
- add Qodana Project Token
- click Run
- wait for analysis results to appear in Qodana Cloud

The CLI and IDE setup flows are similar in purpose, but they target different user environments. CLI is for terminal-based usage, while IDE setup is for users who want to run Qodana from a JetBrains IDE.

## CI/CD setup flow

I opened the “Set it up in your CI/CD pipeline” flow.

Qodana asks the user to choose a preferred CI/CD tool or run Qodana locally.

Available options:

- GitHub Actions
- Jenkins
- GitLab CI/CD
- Azure Pipelines
- Bitbucket Cloud
- CircleCI
- TeamCity
- Run locally

There is also a note that Qodana can be integrated into any CI/CD tool using Docker images. Clicking the Docker images link opens Qodana documentation.

I selected GitHub Actions. Qodana opened the “Set up Qodana in GitHub Actions” flow and asked me to choose a GitHub account or organization and repository. There is also a “Manage GitHub account” link.

I created and selected a test repository called `qodana-cloud-test-project` to avoid using my main repositories.

After selecting the repository, Qodana showed a setup page for GitHub Actions with two modes:

- Automatically
- Manually

In the automatic setup mode, Qodana shows three main steps:

1. Choose the programming language to analyze.
2. Allow Qodana to save a secret and create configuration files pull request.
3. View analysis results after the first Qodana job run.

The language selection step says that only one programming language can currently be selected per project. There is also a link to supported languages and linters documentation.

The automatic setup step explains that Qodana will add a `QODANA_TOKEN` GitHub repository secret and create a pull request with a default `qodana.yaml` configuration file and a GitHub workflow configuration file.

The final step says that analysis results will be displayed in Qodana Cloud after the first Qodana job run.

This flow is important because it connects Qodana Cloud to a real repository and CI pipeline. It also includes permission-sensitive actions, such as adding a GitHub secret and creating a pull request.

## Possible important flows noticed so far

1. New user onboarding and organization setup.
2. Explore demo project report.
3. Run Qodana locally using CLI or JetBrains IDE.
4. Set up Qodana in a CI/CD pipeline with GitHub Actions.

## Possible observations / risks

- Login and registration screens are very similar, which is not necessarily bad, but should be checked for clarity.
- Account deletion and trial license behavior may block the user from continuing with the same JetBrains Account organization.
- Trial behavior may depend on account identity, which could be important for trial abuse prevention.
- Demo projects are useful because they let a new user understand the product before setting up their own repository.
- The demo report contains a lot of information, so filters and grouping are important for usability.
- Local setup depends on the user correctly copying and using the Qodana token.
- GitHub Actions setup includes sensitive repository changes: adding a repository secret and creating a pull request with configuration files.
- The GitHub Actions setup flow should clearly explain what access Qodana needs and what files/secrets it will create.
- The language selection step currently supports only one language per project, which may be important for repositories with multiple languages.
- The product should clearly explain when results will appear after a scan, because analysis can take several minutes.