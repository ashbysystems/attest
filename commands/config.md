---
description: Configure Attest settings. Set the save location for decision logs and escalation records.
argument-hint: [save-path]
---

# /attest:config

Manage Attest plugin configuration.

## Behaviour

### If an argument is provided

The argument is a file path. Set it as the save location for all Attest decision logs and escalation records.

1. Validate the path exists and is a directory. If it does not exist, ask the reviewer if they want to create it.
2. Save the configuration to `${CLAUDE_PLUGIN_ROOT}/.config.json` as:
   ```json
   {
     "saveLocation": "[absolute path]"
   }
   ```
3. Confirm the save location has been set:
   > Save location set to: [path]
   > Decision logs and escalation records will be saved here.

### If no argument is provided

Display the current configuration:

1. Read `${CLAUDE_PLUGIN_ROOT}/.config.json` if it exists
2. Display:
   > **Attest Configuration**
   > - Save location: [configured path, or "Not configured (using current working directory)"]
   >
   > To change the save location, run `/attest:config [path]`

### Configuration file

Store configuration in `${CLAUDE_PLUGIN_ROOT}/.config.json`. If this file does not exist, all commands fall back to the current working directory for file storage.

### Shared directories

The save location can be a shared drive, mounted directory, or any path accessible to the user. Note to the reviewer:

> Decision logs are stored in your configured save location. Apply your organisation's existing data handling and retention policies.
