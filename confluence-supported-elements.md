# Confluence Azure DevOps Wiki Migrator, supported elements

The following table is an index over which elements are supported by the Confluence Azure DevOps Wiki Migrator.

## Insert elements dialogue

The following table contains the status of each element in the **Insert elements** menu in Confluence. See the image below for an illustration

<img src="https://github.com/solidify-internal/atlassian-migration-suite/assets/104482922/e6b4341d-4f2f-47b7-852d-614db01dcaa2" alt="image" width="300"/>
<br /><br />

| Item                                      | <span style="color:green">Supported</span> | <span style="color:orange">Supported with limitations</span> |  <span style="color:green">Not supported</span> | Unable to verify | Comment |
|-------------------------------------------|----------|----------|----------|----------|----------|
| Action item                               | ✔️         |          |          |          |          |
| Activity Stream                           |          |          | ❌         |          |          |
| Agile Wallboard Gadget                    |          |          | ❌         |          |          |
| Anchor                                    |          |          | ❌         |          |          |
| Assigned to me                            |          |          | ❌         |          |          |
| Assets                                    |          |          |          | ✖️         |          |
| Attachments                               | ✔️         |          |          |          |          |
| Average Age Chart                         |          |          | ❌         |          |          |
| Average Number of Times in Status         |          |          | ❌         |          |          |
| Average Time in Status                    |          |          | ❌         |          |          |
| Blog Posts                                | ✔️         |          |          |          |          |
| Bullet list                               | ✔️         |          |          |          |          |
| Chart                                     |          | ✖️         |          |          | Charts are converted to images.         |
| Change History                            |          | ✖️         |          |          | Change history report is migrated but the links are broken. Older page versions are not migrated.         |
| Child pages (Children Display)            | ✔️         |          |          |          |          |
| Code snippet                              | ✔️         |          |          |          |          |
| Content Report Table                      |          | ✖️         |          |          | Content Report Table is migrated but the links are broken as of today (2024-06-27) (to do).         |
| Contributors                              |          | ✖️         |          |          | Migrated but the links to the user profiles are broken.         |
| Contributors Summary                      |          | ✖️         |          |          | Migrated but the links to the user profiles are broken.         |
| Create Confluence page                    |          |          | ❌         |          |          |
| Create from Template                      |          |          | ❌         |          |          |
| Create Jira issue                         | ✔️         |          |          |          |          |
| Custom panel                              |          | ✖️         |          |          | The contents of the panel are migrated, but not the styling.         |
| Date                                      | ✔️         |          |          |          |          |
| Days Remaining in Sprint Gadget           |          |          | ❌         |          |          |
| Decision                                  |          | ✖️         |          |          |  The contents of the panel are migrated, but not the styling.         |
| Decision report                           |          | ✖️         |          |          | A hyperlink to each ADO Wiki page in the report is injected into the markdown contents, but the links are broken as of today (2024-06-27) (to do).         |
| Divider                                   | ✔️         |          |          |          |          |
| Dropbox                                   |          |          |          | ✖️         |          |
| Emoji                                     | ✔️         |          |          |          |          |
| Error panel                               |          | ✖️         |          |          | The contents of the panel are migrated, but not the styling.         |
| Excerpt                                   | ✔️         |          |          |          |          |
| Expand                                    | ✔️         |          |          |          |          |
| Filter Results                            |          |          | ❌         |          |          |
| Filter by Label (Content by label)        |          | ✖️         |          |          | A hyperlink to each ADO Wiki page in the report is injected into the markdown contents, but the links are broken as of today (2024-06-27) (to do).         |
| Gallery                                   | ✔️         |          |          |          |          |
| Heading 1                                 | ✔️         |          |          |          |          |
| Heading 2                                 | ✔️         |          |          |          |          |
| Heading 3                                 | ✔️         |          |          |          |          |
| Heading 4                                 | ✔️         |          |          |          |          |
| Heading 5                                 | ✔️         |          |          |          |          |
| Heading 6                                 | ✔️         |          |          |          |          |
| Heat Map                                  |          |          | ❌         |          |          |
| Help                                      |          |          | ❌         |          |          |
| Iframe                                    |          |          | ❌         |          |          |
| Image, video or file                      | ✔️         |          |          |          |          |
| Include Page                              |          | ✖️         |          |          | A hyperlink to each included page is injected into the markdown contents, but the links are still pointing back to Confluence as of today (2024-06-27) (to do). |
| Info panel                                |          | ✖️         |          |          | The contents of the panel are migrated, but not the styling.         |
| Insert Confluence list                    |          |          | ❌         |          |          |
| Insert excerpt                            |          |          | ❌         |          |          |
| Issue Statistics                          |          |          | ❌         |          |          |
| Issues in progress                        |          |          | ❌         |          |          |
| Jira Charts                               |          |          | ❌         |          |          |
| Jira Issues                               |          |          | ❌         |          | The table is converted to a Jira JQL filter hyperlink.         |
| Jira Issues Calendar                      |          |          | ❌         |          |          |
| Jira Legacy                               | ✔️         |          |          |          |          |
| Jira Premium plan                         |          |          |          | ✖️         |          |
| Jira Road Map                             |          |          | ❌         |          |          |
| Jira timeline                             |          |          | ❌         |          | The timeline is converted to a Jira hyperlink.         |
| JSM Incident Timeline                     |          |          |          | ✖️         |          |
| JSM Incident Timeline EU                  |          |          |          | ✖️         |          |
| Labels Gadget                             |          |          | ❌         |          |          |
| Labels List                               |          | ✖️         |          |          |  The list is migrated but the hyperlinks are broken.        |
| Layouts                                   |          | ✖️         |          |          | The contents of the layouts are migrated as body test, and the columns are lost.         |
| Link                                      | ✔️         |          |          |          |          |
| Live Search                               |          |          | ❌         |          |          |
| Mention                                   |          | ✖️         |          |          | The person's name is migrated, but the hyperlink still points to Confluence.         |
| Note panel                                |          | ✖️         |          |          | The contents of the panel are migrated, but not the styling.         |
| Numbered list                             | ✔️         |          |          |          |          |
| Office Excel                              |          |          | ❌         |          | The document gets compressed to a single preview image.         |
| Office Powerpoint                         |          |          | ❌         |          | The document gets compressed to a single preview image.         |
| Office Word                               |          |          | ❌         |          | The document gets compressed to a single preview image.         |
| Opsgenie Incident Timeline                |          |          |          | ✖️         |          |
| Opsgenie Incident Timeline EU             |          |          |          | ✖️         |          |
| Page Index                                |          | ✖️         |          |          | The hyperlinks still point to Confluence. The index is migrated as a markdown table.         |
| Page Properties                           | ✔️         |          |          |          |          |
| Page Properties Report                    | ✔️         |          |          |          |          |
| Page Tree                                 |          |          | ❌         |          |          |
| Page Tree Search                          |          |          | ❌         |          |          |
| PDF                                       |          |          | ❌         |          | The document gets compressed to a single preview image.         |
| Pie Chart                                 |          |          | ❌         |          |          |
| Popular Labels                            |          | ✖️         |          |          | The list is migrated but the hyperlinks are broken.        |
| Profile Picture                           |          |          | ❌         |          |          |
| Projects                                  |          |          | ❌         |          |          |
| Quick links                               |          |          | ❌         |          |          |
| Quote                                     | ✔️         |          |          |          |          |
| Recently Created Chart                    |          |          | ❌         |          |          |
| Recently Updated Dashboard                |          |          | ❌         |          |          |
| Recent updates                            | ✔️         |          |          |          |          |
| Related Labels                            |          | ✖️         |          |          | The list is migrated but the hyperlinks are broken.        |
| Resolution Time                           |          |          | ❌         |          |          |
| Roadmap Planner                           |          |          |          | ✖️         |          |
| Shared Links Bookmarklet Button           |          |          | ❌         |          |          |
| Spaces List                               |          | ✖️         |          |          | The list is migrated but the hyperlinks are broken.         |
| Sprint Burndown Gadget                    |          |          | ❌         |          |          |
| Sprint Health Gadget                      |          |          | ❌         |          |          |
| Starred filters                           |          |          | ❌         |          |          |
| Status                                    | ✔️         |          |          |          |          |
| Success panel                             |          | ✖️         |          |          | The contents of the panel are migrated, but not the styling.         |
| Table                                     | ✔️         |          |          |          |          |
| Table of Content Zone                     | ✔️         |          |          |          |          |
| Table of contents                         |          | ✖️         |          |          | The TOC is migrated but the anchors are broken.         |
| Task report                               |          | ✖️         |          |          | The report is migrated but the hyperlinks are broken.         |
| Time Since Chart                          |          |          | ❌         |          |          |
| Time to First Response                    |          |          | ❌         |          |          |
| Two Dimensional Filter Statistics         |          |          | ❌         |          |          |
| User List                                 | ✔️         |          |          |          |          |
| User Profile                              |          | ✖️         |          |          | The user profile is migrated but the hyperlinks are broken.         |
| Voted Issues                              |          |          | ❌         |          |          |
| Warning panel                             |          | ✖️         |          |          | The contents of the panel are migrated, but not the styling.         |
| Watched Issues                            |          |          | ❌         |          |          |
| Widget Connector                          |          |          |          | ✖️         |          |
| Workload Pie Chart                        |          |          | ❌         |          |          |
