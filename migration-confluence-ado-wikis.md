# Confluence to Azure DevOps Wikis migrator

## Product overview

Say hello to the **Confluence to Azure DevOps Wikis migrator** from **Solidify**! With our powerful migration tool, you can easily transfer all of your Confluence pages to Azure DevOps Wikis with just a few easy steps.

Our migrator tool will preserve all of your Confluence content and formatting, and transfer it seamlessly to Azure DevOps Wikis. You will save time, streamline your documentation process, and eliminate the headache of managing multiple platforms. Plus, with our easy-to-use interface, you'll be up and running in minutes.

Don't let managing your documentation hold you back. Move your Confluence pages to Azure DevOps Wikis experience the power of seamless documentation management.

## Supported data

Confluence Pages will be migrated to Azure DevOps Wikis in the popular **markdown** format, including the follow data:

- Unlimited amount of Confluence spaces
- Content tree (parentship, not order)
- Text formatting
  - bold, italic, underline, strikethrough, etc...
  - superscript, subscript
  - Colored text
  - Quotes
  - Lists
  - Action points
  - Code blocks
  - Text alignment (left/right/center)
  - Text indentation
- Images/Attachments
- Tables
- Page links (within the same confluence instance)
- Links between Confluence Pages to Jira Issues (provided that the Jira Migrator has already been run)
  - Links From Confluence Pages to Jira Issues
  - Links from Jira Issues to Confluence pages (Only weblinks/remotelinks and links inside the Description field)
- Nested data such as lists inside tables.
- Page labels
- Comments
- The status macro
- Etc (all basic markdown elements)

### Unsupported data

The following data is unsupported as of today:

- Attachments larger than 25MB (see <https://learn.microsoft.com/en-us/azure/devops/user-guide/service-limits?view=azure-devops#wiki>)
- Content tree, order of pages
- Third party apps and integrations
- Macros
- Graphs and Charts
- Links to pages in other Confluence instances
- Inline Comments
- Layouts (columns and sidebars)
- Page versioning
- Whiteboards
- Template library
- Space and Page permissions
- Page insights, analytics
- Team calendars
- Automations
- Admin controls
- Release tracks
- Security & Compliance
  - Atlassian Access (SSO, SCIM, Active Directory Sync)
  - Audit logs
  - IP allowlisting
- Archived pages (you will need to restore any archived pages you wish to preserve)
- Checklists inside table cells
- Citation blocks inside table cells
- Page ownership
- Page authorship
- Page links to other confluence spaces

### Full list of supported elements

A full list of supported standard confluence elements can be found here: <https://github.com/solidify/atlassian-migration-suite-docs/blob/main/confluence-supported-elements.md>

## Process overview

Here is an overview of the Confluence to Azure DevOps Wiki migration process:

1. **Confluence Export:**
   - Export content from Confluence using Confluence's export features.
   - Ensure the exported data includes pages, attachments, and any other relevant content.

2. **Transformation (Run confluence_ado_migrator.exe):**
   - Run a transformation program (confluence_ado_migrator.exe) on the exported Confluence data.
   - The program converts Confluence-specific HTML content to Markdown.

3. **Azure DevOps Wiki Import (Git Push):**
   - Initialize a local Git repository to store the transformed content.
   - Add the transformed content to the local repository.
   - Commit the changes and push the repository to the Azure DevOps Wiki Git repository.

4. **Verification and Cleanup:**
   - Verify the migrated content in Azure DevOps Wiki to ensure formatting, links, and attachments are correctly imported.
   - Address any discrepancies or issues identified during verification.

5. **Testing and User Validation:**
   - Conduct testing to ensure the migrated content meets expectations and is accessible in Azure DevOps Wiki.
   - Inform and involve relevant users or stakeholders for validation.
   - Provide training or documentation for users transitioning from Confluence to Azure DevOps Wiki.

6. **Cleanup:**
   - (Optional) Use a regex search-replace feature in any modern IDE to scrub the new Wiki repository from unwanted content and formatting.

7. **Finalization:**
   - Once validated, consider finalizing the migration by decommissioning the Confluence instance or adjusting access permissions.
   - Update documentation and communication channels to reflect the new location of documentation in Azure DevOps Wiki.

## Argument explanations
  
| Argument | Required | Description | Example |
|----------|----------|-------------|---------|
| --url    | \* | The URL of the Confluence site. | --url "https://example.atlassian.net" |
| --confluence-space-key  | \* | The key of the Confluence space to export. The space key can be found in the URL of the space, for example `https://xyz.atlassian.net/wiki/spaces/<SPACE KEY>/overview` | --confluence-space-key SOLIDIFY |
| --auth-method | \* | The authentication method to use against the Confluence Rest API. Must be either "basic" or "token" | --auth-method "basic" |
| --username | \* | The username or email address used for authentication. | --username "john.doe@solidify.se" |
| --password | \* | The API key or password for authentication. | --password "abc123" |
| --token |  | The Oauth API token for authentication. Use only if --auth-method == "token" | --token "abc123" |
| --api-version | \* | The Confluence API version to use. (cloud/server) | --api-version "cloud" |
| --src-path | \* | The path to the local export folder where Confluence data was exported. | --src-path "C:\path\to\local\export\folder\SOLIDIFY" |
| --out-path | \* | The path to the target folder where the exported data will be stored. | --out-path "C:\path\to\target\folder" |
| --license-file-path | \* | The path to the license file.| --license-file-path "C:\Temp\license.json" |
| --confluence-space-name | \* | Confluence space **name** (In Confluence, go to Space Settings > Space Details. Here, the **Name** is the space name.) | --confluence-space-name "Solidify Wiki" |
| --ado-url | \* |  ADO URL, including organization/collection. | --ado-url "https://dev.azure.com/solidifydemo" |
| --ado-project | \* | ADO project name. | --ado-project "ContosoAir" |
| --ado-work-items-project | \* | ADO project name where the imported Jira Issues reside. Can be the same as or different from `--ado-project`. | --ado-work-items-project "ContosoAir" |
| --ado-pat | \* | ADO personal access token. | --ado-pat "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" |
| --ado-jira-id-field |  | The field in ADO containing the Jira issue ID. | --ado-jira-id-field "Custom.JiraID" |
| --ado-wiki-name | \* | Name of wiki in ADO | --ado-wiki-name "ContosoAir.wiki" |
| --jira-url |  | URL to your jira instance. | --jira-url "https://solidifydemo.atlassian.net" |
| --include-page-labels |  | Should page labels be migrated? (y/n) | --include-page-labels "y" |
| --include-page-comments |  | Should page comments be exported from the Confluence Rest API? set to false if comments are already included in the HTML Export (y/n) | --include-page-comments "y" |
| --pure-markdown |  | Only write pure markdown elements and no html? Excluding html elements will disable special formatted elements such as colored text and content inside table cells. The resulting page will be more human-readable though. (y/n) | --pure-markdown "n" |
| --log-level |  | Log level (info/debug/warning/error/critical) | --log-level "info" |
| --no-ssl-verify |  | Add this parameter if you want to skip the SSL verification against your Confluence Server. (y/n) | --no-ssl-verify "y" |
| --regenerate-mapping-files |  | Should mappings files be regenerated? Use this flag if you want to start fresh. Default: no (y/n) | --regenerate-mapping-files "n" |
| --node-memory-size |  | Override the max-old-space-size Node option? Set this to a higher value if you are experiencing 'JavaScript heap out of 'memory' errors (type: integer, default: 2048). | --node-memory-size 4096 |
| --max-retry-count |  | Override the max retry count for Confluence and ADO Rest Api calls? (type: integer, default: 3). | --max-retry-count 3 |
| --get-jira-issue-ids-from-journal-file |  | Flag indicating wether to get the issue-WI mappings from the Jira Migrator journal file or not. Default: no (y/n) | --get-jira-issue-ids-from-journal-file "y" |
| --journal-file-path |  | Path to the Jira Migrator journal file. | --journal-file-path "D:\workspace\itemsJournal.txt" |
| --turndown-service-path |  | Path to the turndown.js file, unless it is in the same directory as confluence_ado_migrator.exe. | --turndown-service-path "C:\tools\confluence-ado-migrator\turndown.js" |

## Auth scheme options

Here are usage examples for the different auth scheme options available

### Basic auth

Use your Confluence (Atlassian) username and login password.

```ps1
--auth-method "basic" --username "john.doe@solidify.se" --password "abc123"
```

### Bearer (OAuth access token)

User your Confluence (Atlassian) Rest API Token.

```ps1
--auth-method "token" --token "abc123"
```

## Requirements

### Hardware requirements/VM Specs

The VM should run on the Standard_B2s Azure service plan (minimum), or equivalent hardware specs:

- Operating System: Windows-based 64bit or Equivalent Windows Professional/Enterprise
  - 2 vCPUs
  - 4 GiB Memory
  - 8 GiB Swap space
  - 128 GiB Storage (SSD/HDD) (or as needed)
  - A stable internet connection

### Software requirements

The following software should be installed on the machine:

- Git client (<https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>)
  - `core.longpaths` enabled in git config (`git config --system core.longpaths true`)
  - system longpaths registry key set (<https://learn.microsoft.com/en-gb/windows/win32/fileio/maximum-file-path-limitation?tabs=registry#enable-long-paths-in-windows-10-version-1607-and-later>)
  - Git LFS (optional if you want to bring big attachments into Git LFS) (<https://git-lfs.com/>)
- NodeJS 16.0.0+
- npm 7.10.0+

### Network requirements

The migration occurs in two steps, first exporting from Confluence, then importing to Azure DevOps.

- During the **Confluence export** and **transformation** steps, the machine will need a stable internet connection and access to the **Confluence server** or **Confluence cloud**.
- During the **ADO import** (git push) step, the machine will need a stable internet connection and access to the **ADO Server** or **ADO Services**.

You do not need access to ADO during the export, and similarly you do not need access to Confluence during the import.

If you do not have an internet connection during the export, the tool will not be able to run.

### Required permissions

#### Confluence

The user running the migration must have:

- **Space admin** permission in the Confluence space

#### Azure DevOps (ADO)

The user running the migration must have:

- **Contributor** access in the target ADO project
- **force push** permission in the target wiki or repository.

## Benchmark

Previous tests have show that a **1 GB Confluence** space takes **less than 20 minutes** to migrate, provided that the recommended system requirements are met, and that all the necessary configuration is in place and that the html exporter has already been run.

### [Optional] Requirements for fixing links to ADO Work Items

In order to enable the automatic link mapping functionality for Jira Issues to ADO Work Items, there are a few prerequisite steps:

- Ensure that you have set up a custom text field in Azure DevOps for holding the reference to the original issue key, on each relevant Work Item Type, for example **Custom.JiraReferenceID**. This field can be hidden or removed later.
- Ensure that you have mapped the issue key field in your Jira AzureDevOps Migrator **config.json** file, for example:

    ```json
    {
      "source": "key",
      "target": "Custom.JiraReferenceID"
    }
    ```

- Run the Jira AzureDevOps migration
- When you run the Confluence migrator CLI (confluence_ado_migrator.exe), supply the parameter `--ado-jira-id-field Custom.JiraReferenceID`
- You are now set up for using the link mapping functionality!

### [Optional] Consolidating confluence space into an existing ADO Wiki hierarchy

The tool can be used to migrate multiple Confluence spaces to a single target, or to a specific existing page hierarchy within an ADO Wiki.

After running the **Confluence to Azure DevOps Wikis migrator** locally to generate the wiki data, you will need to do the following:

- create a new folder (for example: `folderA`) in your wiki inside **Azure DevOps Wikis** (not locally, as this will not set up the required indexes)
- Do a `git export` to get your ADO Wiki files locally
- Paste the files generated by the **Confluence Azure DevOps Wiki migrator** inside `folderA`
- Do a `git commit` and `git push`

- Can it migrate multiple Confluence spaces into a single ADO Wiki?

### Review Attachments > 25MB with Custom attachments

Attachments larger than 25 MB will cause the **git push** to fail, due to upload size limits in Azure DevOps. Thus, you will need to review the attachment files larger than 25 MB and take action for each of the before you proceed with the import.

If your space has any pages with large attachments, the tool will generate a file named **report-large-attachments.json** in your migration workspace. You can review this file in order to large attachments.

There are multiple possibilities for preserving the large attachments:

- (Recommended) Move the attachments to a separate git repository on ADO and update the links. For a step-by-step guide, see the section **Alternative for storing large attachments: Use a separate git repository** at the end of this document.
- Move the attachments to a file share or a cloud storage and update the links manually.

### [Optional] Review Pages with Custom macros

Custom macros are not supported by the Confluence ADO Wikis Migrator. If your space has any pages with custom macros, the tool will generate a file named **report-pages-with-custom-macros.json** in your migration workspace. You can review this file in order to address pages with custom macros.

### Script: `post_migration_corrections.exe`

`post_migration_corrections` is a script for doing corrections after the Confluence to Azure DevOps (ADO) migration.

This script uses the mapping files generated by the ConfluenceAdoMigrator to do some post-migration operations. Currently these operations are:

- correct links from ADO WorkItems to ADO Wiki pages in the **Description** field and in **Hyperlink relations**.

#### Argument explanations

| Argument                   | Required | Description                                                                                                           | Example                                                      |
|-----------------------------|----------|-----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `--url`                     | *        | The URL of the Confluence site where post-migration corrections are needed.                                            | `--url "https://example.confluence.com"`                      |
| `--confluence-space-key`     | *        | The **key** of the Confluence space to modify. The space key is part of the space URL (e.g., `/spaces/<SPACE_KEY>`).    | `--confluence-space-key "YOUR_SPACE_KEY"`                     |
| `--license-file-path`        | *        | Path to the license file required for migration tools.                                                                | `--license-file-path "/path/to/license.json"`                 |
| `--ado-url`                 | *        | Azure DevOps (ADO) URL, including the organization/collection.                                                        | `--ado-url "https://dev.azure.com/yourorganization"`           |
| `--ado-work-items-project`   | *        | ADO project where the migrated work items are stored, such as those from Jira.                                         | `--ado-work-items-project "WorkItemsProjectName"`             |
| `--ado-pat`                 | *        | ADO personal access token (PAT) for authentication.                                                                   | `--ado-pat "<ADO personal access token>"`                     |
| `--log-level`                |          | Log verbosity level (`info`, `debug`, `warning`, `error`, `critical`). Defaults to `info`.                             | `--log-level "info"`                                          |
| `--no-ssl-verify`            |          | Set to `y` to skip SSL verification for Confluence Server. Defaults to `n`.                                            | `--no-ssl-verify "n"`                                         |
| `--max-retry-count`          |          | Maximum retry attempts for ADO Rest API calls. Default is `3`.                                                         | `--max-retry-count 3`                                         |

#### Usage example

```powershell
python3 post_migration_corrections.exe \
--url "https://your-confluence-server-url.com" \
--confluence-space-key "YOUR_SPACE_KEY" \
--license-file-path "/path/to/license.json" \
--ado-url "https://dev.azure.com/yourorganization" \
--ado-work-items-project "WorkItemsProjectName" \
--ado-pat "<ADO personal access token>" \
--log-level "info" \
--no-ssl-verify "n" \
--max-retry-count 3
```

## Step-by-step

Here's a step-by-step guide for using the Confluence to Azure DevOps Wikis migrator:

1. Export pages from Confluence to a local folder:
   - Log in to your Confluence account and navigate to the space containing the pages you want to migrate.
   - Click on the "Space tools" menu and select "Content Tools."
   - Click on "Export" and select "Export to HTML" from the dropdown menu.
   - Choose the pages you want to export and click "Next."
   - Select "Normal Export" and click "Next."
   - Choose a destination folder on your local machine and click "Export."
   - Wait for the export process to complete.

2. Run our CLI tool to convert the local Confluence resources to an Azure DevOps Wikis-compliant format:
   - Open a Powershell terminal or command prompt and navigate to the directory where the CLI tool is installed.
   - Run the command:

    ```powershell
        .\confluence_ado_migrator.exe `
        --url "https://xxx.atlassian.net" `
        --confluence-space-key "SOLIDIFY" `
        --auth-method "basic" `
        --username "john.doe@solidify.se" `
        --password "<confluence api key>" `
        --api-version "cloud" `
        --src-path "C:\path\to\local\export\folder" `
        --out-path "C:\path\to\target\folder" `
        --license-file-path "C:\Temp\license.json" `
        --confluence-space-name "Solidify Wiki" `
        --ado-url "https://dev.azure.com/solidifydemo" `
        --ado-project "ContosoAir" `
        --ado-work-items-project "ContosoAir" `
        --ado-pat "<ADO personal access token>" `
        --ado-jira-id-field "Custom.JiraID" `
        --jira-url "https://solidifydemo.atlassian.net" `
        --ado-wiki-name "ContosoAir.wiki" `
        --include-page-labels "y" `
        --pure-markdown "n" `
        --regenerate-mapping-files "n"
    ```

    where `C:\path\to\local\export\folder` is the path to the folder where you exported your Confluence pages and `C:\path\to\target\folder` is the path to the folder where you want to store the converted pages.

   - Copy all contents of the folder `devops-migration-confluence\extra-icons` to `$out-path\.images\icons`. The resulting folder structure should look like the following:

     - `$out-path\.images\icons`
       - `\emoticons`
       - `\priorities`

3. Run the following **powershell script** To find all attachments larger than **25 MB**.

   ```ps1
    $filesize=1024*1024*25 # 25GB
    $targetPath="C:\path\to\target\folder"
    Get-ChildItem $targetPath -Recurse | Where-Object { $_.Length -gt $filesize} | ForEach-Object { Write-Host -NoNewline (Get-Item $_); Write-Host -NoNewline (", size (MB): "); Write-Host($_.Length/1MB) }
   ```

   - Delete all files listed by the script.

4. Review Pages with large attachments

The file **report-large-attachments.json** in your migration workspace contains information on all large attachments. These files cannot be imported to ADO, and the **git push** step later in this guide will fail and give you an error if you try and push files larger than 25 MB.

5. Review Pages with custom macros

The file **report-pages-with-custom-macros.json** in your migration workspace contains all Confluence Pages with custom macros. These pages will be migrated, but some custom macros might not come over as expected.

6. Alternative 1: Import to Azure Devops Wiki (as project wiki)

- In your AzDo project, navigate to your project wiki.
- Create a new blank page if the project wiki is not already populated.
- Go to `More actions` > `Clone wiki` and copy the wiki clone url.
- On your local machine, open a terminal or command prompt and navigate to the target folder where your markdown files were generated
- Run the command `git init` to initialize a new Git repository in the folder.
- Add everything and commit: `git add .`, `git commit -m "Init"`
- Add the wiki url that you copied before as a new remote, for example: `git remote add origin https://dev.azure.com/{organization}/{project}/_git/{project}.wiki`
- Switch to the **wikiMaster** branch with `git checkout -b wikiMaster`.
- Push everything with `git push --set-upstream origin wikiMaster --force` (Warning, this will irreversibly overwrite your current Project Wiki).

Here is the full git script which you can use:

```ps1
git init
git add .
git commit -m "Init"
git remote add origin https://dev.azure.com/{organization}/{project}/_git/{project}.wiki
git checkout -b wikiMaster
git push --set-upstream origin wikiMaster --force
```

### Alternative 2: Import to Azure Devops Wiki (as code wiki)

- In your ADO project, create a new git repository where your wiki will reside.
- On your local machine, open a terminal or command prompt and navigate to the target folder where your markdown files were generated
- Run the command `git init` to initialize a new Git repository in the folder.
- Add everything and commit: `git add .`, `git commit -m "Init"`
- In the terminal or command prompt, run the command `git remote add origin https://dev.azure.com/{organization}/{project}/_git/{wiki repo name}`.
- Finally, run the command `git push --set-upstream origin master --force` to push the pages to the new Azure DevOps wiki.
- In Azure Devops Wikis, create a new Wiki with the "Publish code as wiki". Select the new repo and use "/" as the folder.

Here is the full git script which you can use:

```ps1
git init
git add .
git commit -m "Init"
git remote add origin https://dev.azure.com/{organization}/{project}/_git/{wiki repo name}
git checkout -b master
git push --set-upstream origin master --force
```

Congratulations! You've successfully migrated your Confluence pages to Azure DevOps Wikis using our migrator tool.

### Fix hyperlinks from Work Items to Confluence Pages using the Post Migration Corrections script

The **Post Migration Corrections script** correct links from ADO WorkItems to ADO Wiki pages in the **Description** field and in **Hyperlink relations**. If you have already imported your Jira Issues to Azure DevOps, you can use this script **after the git-import step** to correct any links to your old Confluence pages. They will then instead point to the correct Wiki pages in Azure DevOps.

#### Usage example

```powershell
.\post_migration_corrections.exe \
--url "https://your-confluence-server-url.com" \
--confluence-space-key "YOUR_SPACE_KEY" \
--license-file-path "/path/to/license.json" \
--ado-url "https://dev.azure.com/yourorganization" \
--ado-work-items-project "WorkItemsProjectName" \
--ado-pat "<ADO personal access token>" \
--log-level "info" \
--no-ssl-verify "n" \
--max-retry-count 3
```

## Post migration cleanup, how-to with Visual Studio Code

Visual Studio Code (VS Code) provides powerful tools for performing project-wide search and replace operations using regular expressions (regex). This allows you to efficiently find and modify text patterns across multiple files in your project. In this guide, we will the project-wide search and replace operation in VS Code to scrub the new Wiki repository from unwanted content and formatting.

   Below is a documentation on performing a project-wide search and replace with regex in Visual Studio Code, starting with opening the `--out-path` folder:

---

## Performing Project-Wide Search and Replace with Regex in Visual Studio Code

### Overview

Visual Studio Code (VS Code) provides powerful tools for performing project-wide search and replace operations using regular expressions (regex). This allows you to efficiently find and modify text patterns across multiple files in your project. In this guide, we'll walk through the process of performing a project-wide search and replace operation with regex in VS Code.

### Opening the `--out-path` Folder in Visual Studio Code

1. **Open VS Code**:
   - Launch Visual Studio Code on your computer.

2. **Open Folder**:
   - Use the "File" menu or the keyboard shortcut `Ctrl + K` followed by `Ctrl + O` to open the folder containing your project.

3. **Navigate to `--out-path` Folder**:
   - In the VS Code file explorer, navigate to the directory specified by the `--out-path` option. You can do this by clicking on folders in the file explorer until you reach the desired folder.

### Performing Project-Wide Search and Replace with Regex

1. **Open Search Panel**:
   - Use the keyboard shortcut `Ctrl + Shift + F` to open the search panel in VS Code.

2. **Enable Regex Search**:
   - Click on the icon with `.*` in the search panel to enable regex search mode. This allows you to use regular expressions in your search queries.

3. **Enter Search Query**:
   - Enter your regex search query in the search input field. You can use regex patterns to match specific text patterns in your project files.

4. **Perform Search**:
   - Press `Enter` to perform the search. VS Code will display a list of search results in the search panel.

5. **Review Search Results**:
   - Review the search results to ensure that they match the text patterns you want to replace.

6. **Perform Replace**:
   - Once you're satisfied with the search results, you can proceed with the replace operation. Click on the "Replace" button next to the search input field to open the replace input field.

7. **Enter Replace Pattern**:
   - Enter your regex replace pattern in the replace input field. You can use capture groups (`$1`, `$2`, etc.) to reference matched groups from your regex search query.

8. **Perform Replace**:
   - Click on the "Replace All" button to perform the replace operation. VS Code will replace all occurrences of the matched text patterns with the specified replace pattern in your project files.

### Using regex101.com to Build and Test Regular Expressions

1. **Open regex101.com**:
   - Open your web browser and navigate to [regex101.com](https://regex101.com/).

2. **Build and Test Regular Expressions**:
   - Use the regex101.com interface to build and test your regular expressions. You can enter sample text and see how your regex pattern matches against it. The website also provides explanations and highlights matched text for easier debugging.

3. **Refine and Test**:
   - Refine your regex pattern as needed based on the test results. Make adjustments until you achieve the desired matching behavior.

## Alternative for storing large attachments: Use a separate git repository

In order to get around the Azure DevOps Wikis upload size limit, you may resort to storing the attachments in any cloud storage solution.

**Our recommendation** is to store all attachments in a separate git repository in the same Azure DevOps project. This has the following major benefits:

- Attachments are rendered correctly inside the wiki.
- Traceability for all old attachments
- All data is stored inside a single location: Azure DevOps. No external cloud storage service required.

With this solution you will have two **git repositories** in the same ADO project, one containing the Wiki contents, and the other containing the migrated confluence attachments. In the future, adding an attachment from the Wiki edit menu will cause the attachment to be stored in the **.attachments** folder in the **Wiki repo**. Here is an example of the project structure:

- **ADO Project**: example-project
  - **Wiki repo**: example-project-wiki
  - **Attachments repo**: example-project-wiki-attachments

Here's a step-by-step guide for the post-migration step of storing large attachment files in a separate Azure DevOps git repository as part of the Confluence to Azure DevOps Wikis migration solution:

1. **Locate and Copy Attachments from Migration Output:**
   - After running the `confluence_ado_migrator.exe` to transform the data, locate the `.attachments` folder in the **output directory** generated by the migration tool.
   - Copy the contents of the `.attachments` folder to a new folder on your hard drive. Let's call this folder "large-wiki-attachments". The resulting folder should look like this:

   ```txt
   large-wiki-attachments/
   ├── 12345/
   │   └── example1.png
   ├── 67890/
   │   └── example2.png
   ├── 23456/
   │   └── example3.png
   ├── 78901/
   │   └── example4.png
   └── 34567/
       └── example5.png
   ```

2. **Create a New Azure DevOps Git Repository:**
   - Log in to Azure DevOps and navigate to the project where you want to store the large attachments.
   - Create a new git repository to hold the large attachments.
   - Grab the clone URL of the newly created repository.

3. **Initialize Local Repository and Push Files:**
   - Open a terminal or command prompt and navigate to the "large-wiki-attachments" folder.
   - Initialize a new git repository locally inside the "large-wiki-attachments" folder using the command `git init`.
   - Add the Azure DevOps git repository's clone URL as the "origin" remote using the command `git remote add origin <clone-url>`.
   - Use `git add .`, `git commit`, and `git push` commands to add, commit, and push the files to the Azure DevOps git repository.

4. **Get Azure DevOps REST API URL:**
   - Navigate to the Azure DevOps project settings and find the REST API URL for fetching files inside the repositories. This URL will be used to construct the file endpoint URL in the next step.

5. **Replace Attachment Links in Confluence Output:**
   - Inside the output folder where the Confluence contents were exported, open Visual Studio Code.
   - Use the keyboard shortcut `Ctrl + Shift + F` to open the search panel in VS Code.
   - Click on the icon with `.*` in the search panel to enable regex search mode. This allows you to use regular expressions in your search queries.
   - Enter your regex search query in the search input field. You can use regex patterns to match specific text patterns in your project files:

     ```txt
     Find:          !\[\]\(\.attachments\/\d+\/([\w.-]+\.*)
     Replace with:  https://dev.azure.com/[MyOrganization]/[MyProject]/_apis/git/repositories/[large-wiki-attachments]/items?path=/$1&download=true
     ```

   - In the above query, replace `[MyOrganization]`, `[MyProject]` and `[large-wiki-attachments]` with the appropriate values (ADO organization, ADO project and git repo name), or replace the whole ADO URL with your ADO Server URL.

6. **Push Confluence Output Folder to Azure DevOps Wiki:**
   - Commit the changes made in the output folder using git.
   - Push the committed changes to the Azure DevOps wiki repository.

7. **Review the results**

   - Review your Azure DevOps Wiki and ensure that the attachments are being rendered as expected.

## Solution for Self service-based migrations

Solidify offers a self-service solution for the Confluence to ADO Wiki Migrator, which enables organizations to automate the migration process of many Confluence spaces, thus saving time and effort.

The self-service solution is powered by Azure Pipelines, and the intention is to set up a Build Agent with the necessary tooling. The entrypoint for the end users will be an **Azure Pipeline** with some amount of customization.

The Self Service solution is part of our Professional Services offering. Contact us at [support.jira-migrator@solidify.dev](mailto:support.jira-migrator@solidify.dev) for more information.

## Troubleshooting

### "javascript heap out of memory" error message

This error can usually be resolved by setting the environment variable: “NODE_OPTIONS=–max_old_space_size=4096"

### Missing Pages in the Target folder

A frequent issue when exporting a Confluence site is that not all pages were selected during the export process. For example, if the **homepage** is not included, the export will fail to list the homepage or its child pages. This issue is typically indicated by error messages in the **log-turndown file**.

#### Steps to Verify:

1. **Check the Homepage File in the Export**:
   - Identify the `pageId` of your homepage. For instance, if your homepage has the `pageId` **950530**, there should be an `.html` file in the `source` directory of the export with "950530" in its filename.
   - If this file is missing, the homepage was not included in the export.

2. **Split Large Spaces**:
   - If the space is too large to export in one go, perform multiple exports for different sections of the space.
   - Combine the contents of the resulting `.zip` files to create a complete export.

#### Example:
For the space at `https://solidifydemo.atlassian.net/wiki/spaces/PMT/overview?homepageId=950530`, ensure that a file with "950530" exists in the `source` directory. If it does not, re-export the site, ensuring the homepage and its child pages are selected.

#### Notice about script file encoding

This error has also been shown to appear if the command used to run the Confluence ADO Migrator .exe is stored in a .ps1-file and the .ps1 file does not have UTF-16 encoding. Try changing the encoding of the script to UTF-16 and run again.

### Page is not migrated due to view+edit restrictions

If a Confluence Page is protected by view or edit restrictions, the page might not be exported as expected. You may need to disable page restrictions in order to ensure that these pages are exported by Confluence.

### Confluence API OAuth error: Current user not permitted to use Confluence

When using the confluence-ado-migrator.exe with Confluence cloud (atlassian.net) and with **--log-level="debug"**, you may receive a 403: Unauthorized HTTP response with the message "Current user not permitted to use Confluence".

The solution is usually to edit your API credentials in the script parameters. The following configuration usually works:

```
--auth-method "basic"
--username "[email]"
--password "[API token]"
```

Alternatively, the following configuration may also work:

```
--auth-method "token"
--token "[API token]"
```

### SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate

To address this error message, you can use a custom certificate store. Set the `REQUESTS_CA_BUNDLE` environment variable to the desired file path before running the tool:

```bash
$env:REQUESTS_CA_BUNDLE = "C:\example\cacert.pem"
```
