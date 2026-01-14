# Jira Azure DevOps migrator PRO - Bootstrapper utility

The **Jira Azure DevOps migrator Bootstrapper Utility** is a script that scaffolds JSON config files for the **Jira Azure DevOps migrator**. The script is designed to help with getting started migrating issues from Jira to Azure DevOps as smoothly as possible and with as little configuration as possible.

The script can also produce reports on the following available resources in Jira, and assist with mapping these:

- Fields
- States
- Users

The script does the following:

- Scaffolds a `config.json` file based on a simplified `metaconfig.json`, which you can then customize to suit your specific migration needs.
- Produces a `available-fields.json` file, which contains a report of all available **fields** in your Jira instance, to help you with field mapping.
- Produces a `available-states.json` file, which contains a report of all available **statues** in your Jira instance, to help you with state mapping.
- Produces a `available-users.csv` file, which contains a report of all available **users** in your Jira instance, to assist with user mapping.
- Produces a `users-generated.txt` file, which is a suggestion for a `users.txt` file. It includes all user mappings that the tool could discern automatically. You can base your own `users.txt` file on this file.

## Usage

1. Set up your `metaconfig.json` file
1. Run `jira-migrator-bootstrapper.exe`

`jira-migrator-bootstrapper.exe` takes the following parameters:

| Option                         | Description                                                       | Parameter Type |
| ------------------------------ | ----------------------------------------------------------------- | -------------- |
| `--meta-config-path`           | Path to the metaconfig.json file.                                 | string         |
| `--base-url`                   | Base URL of the Jira instance.                                    | string         |
| `--project-key`                | Key of the Jira project.                                          | string         |
| `--username`                   | Jira username.                                                    | string         |
| `--password`                   | Jira API token.                                                   | string         |
| `--license-file-path`          | License file path.                                                | string         |
| `--issue-replay-pagesize`      | During issue replay, what page size should we use? Default = 50   | int            |
| `--issue-replay-stop-at`       | During issue replay, how many issues should we maximum replay? Set this to a lower value if the program does not terminate within a reasonable time. Doing so might mean that not all available states are reported. Default = all issues in the project  | int            |
| `--only-project-level-users`   | Add this flag if you only want the users of the Jira Project (SourceProject in the metaconfig.json) to appear in the report. Otherwise all users in the entire organization will be outputted. | string         |
| `--auth-scheme`                | Auth scheme to use for the Jira Rest API. Must be either 'basic' or 'bearer'. Default = 'basic' | string             |
| `--jira-server-8-4-or-newer`   | Add this flag if you are using Jira Server version 8.4.x or later | boolean        |
| `--timeout`                    | Override the timeout used for all Jira Rest API Queries (seconds). Default = 30    | int            |
| `--no-ssl-verify`              | Add this flag if you want to skip the SSL verification against your Jira Server    | boolean        |
| `--log-level`                  | Logging level (info/debug/warning/error/critical).                | string         |

### Usage examples

#### Jira Cloud or Server < 8.4.0

```powershell
.\jira-migrator-bootstrapper.exe --base-url https://solidifydemo.atlassian.net/ --project-key AGILEDEMO --username alexander.hjelm@solidify.dev --password xxxxxx --license-file-path C:\Temp\solidifydemo.atlassian.net.20XX-XX-XX.json --issue-replay-pagesize 50 --issue-replay-stop-at 1000 --log-level info
```

#### Jira Server >= 8.4.0

```powershell
.\jira-migrator-bootstrapper.exe --base-url https://solidifydemo.atlassian.net/ --project-key AGILEDEMO --username alexander.hjelm@solidify.dev --password xxxxxx --license-file-path C:\Temp\solidifydemo.atlassian.net.20XX-XX-XX.json --issue-replay-pagesize 50 --issue-replay-stop-at 1000 --jira-server-8-4-or-newer --log-level info
```

## Meta configuration file details

The script will require the `metaconfig.json` file to be present and populated. Here is an example file and explanation of each property:

```json
{
    "SourceProject": "Agile-Demo",
    "TargetProject": "TargetProject",
    "SourceProjectKey": "AGILEDEMO",
    "Workspace": "C:\\Temp\\jira-migrator-bootstrapper",
    "UsingJiraCloud": "true",
    "ExportReleases": "true",
    "BaseAreaPath": "Migrated",
    "BaseIterationPath": "Migrated",
    "ProcessTemplate": "Agile"
}
```

- `SourceProject`: Name of the source Jira project.
- `TargetProject`: Name of the target Azure DevOps project.
- `SourceProjectKey`: Key of the source Jira project.
- `Workspace`: The path to the workspace where the Bootstrapper Utility is located.
- `UsingJiraCloud`: Indicates whether we are using Jira Cloud or Jira Server. Must be either `true` or `false`.
- `ExportReleases`: Indicates whether to export releases or not. Must be either `true` or `false`.
- `BaseAreaPath`: Base area path for the migrated issues in Azure DevOps.
- `BaseIterationPath`: Base iteration path for the migrated issues in Azure DevOps.
- `ProcessTemplate`: The process template to be used in Azure DevOps. Must be either `Agile`, `Basic`, `CMMI` or `Scrum`.

## SSL Configuration

Below are the options for managing SSL behavior:

#### **Skipping SSL Verification**

To bypass SSL verification when connecting to the Jira Server, use the `--no-ssl-verify` flag

#### **Debugging SSL Certificate Store Path**

When the `--log-level` parameter is set to `debug`, the tool logs the path to the certificate store used for SSL verification:

```
2024-11-13 10:44:42,243 : DEBUG : Using certificate store at path (put any SSL certificates here): 
C:\Users\Alexander\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.9_qbz5n2kfra8p0\LocalCache\local-packages\Python39\site-packages\certifi\cacert.pem
```

#### **Specifying a Custom Certificate Store**
To use a custom certificate store, set the `REQUESTS_CA_BUNDLE` environment variable to the desired file path before running the tool:

```bash
$env:REQUESTS_CA_BUNDLE = "C:\temp\cacert.pem"
```
