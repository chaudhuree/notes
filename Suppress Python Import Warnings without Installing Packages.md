# If you are seeing missing import or module source warnings in VS Code / Pylance and want to suppress them without installing the missing packages, create a configuration file at the root of your project:

**File path:** `./pyrightconfig.json`

```json
{
  "reportMissingImports": "none",
  "reportMissingModuleSource": "none"
}

```

**What this does:**

* `reportMissingImports: "none"` — Hides warnings for packages that aren't installed in your active environment.
* `reportMissingModuleSource: "none"` — Stops the language server from complaining when it can't resolve the source code for an import.

Restart VS Code or reload your window after saving the file for the changes to apply.
