# Collibra Utilities

A collection of utilities for administering and extending Collibra: workflows, scripts and other helpers.

## Contents

| Utility | Type | Description |
|---|---|---|
| [Manage Dashboard Files](workflows/manageDashboardFiles.bpmn) | Workflow (.bpmn) | Upload or delete files used by custom dashboards |

## Workflows

### Manage Dashboard Files

`workflows/manageDashboardFiles.bpmn`

This workflow uploads or deletes files used by custom dashboards. The files live in a folder under the Collibra `dgc` data directory. It replaces the separate *Upload Dashboard Files* and *Delete Dashboard Files* workflows.

**Upload**

- Validates the file name and checks the extension against an allow-list.
- If the file already exists, asks the person who started the workflow to confirm the overwrite.

**Delete**

- The person who started the workflow picks the file from a dropdown of the files currently in the folder.
- They can cancel before anything is removed.

All actions are logged with the name of the person who started the workflow.

**Configuration variables** (editable on the workflow definition page)

| Variable | Default | Purpose |
|---|---|---|
| `section` | `custom-dashboards` | Folder under the `dgc` data directory |
| `allowedExtensions` | `png,jpg,jpeg,gif,svg,html,css,js` | Comma-separated upload allow-list |

**Deploy**

1. In Collibra, go to **Settings > Workflows > Definitions**, select **Upload**, and choose the `.bpmn` file.
2. Enable the workflow as a global workflow.
3. Restrict who can start it to system administrators, since it writes to the server's file system.

> **Security note.** `html`, `svg` and `js` files can contain scripts. Remove them from `allowedExtensions` unless your dashboards need them.

## Contributing

1. Add each utility in a folder that matches its type, such as `workflows/`.
2. Add a row to the Contents table.
3. Add a short section that covers what the utility does, how to configure it and how to deploy it.

## Disclaimer

These utilities are provided as-is and are not officially supported by Collibra. Test them in a non-production environment before you deploy.
