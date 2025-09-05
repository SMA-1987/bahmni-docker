# Module Toggles

Bahmni Docker allows features to be enabled or disabled at runtime.
The configuration lives in `/apps/module-toggles.json` and is loaded
when `run-bahmni.sh` starts the stack.

```json
{
  "registration": true,
  "billing": false,
  "reports": true,
  "appointments": true
}
```

Each key represents a supported module and the boolean value indicates
whether the module is enabled by default.

The `run-bahmni.sh` script reads this file and exposes the content to
all containers using the `MODULE_TOGGLES` environment variable.  Bahmni
services should inspect this variable on startup and hide their routes
or UI elements when a module is disabled.

To override a module's state, edit `apps/module-toggles.json` and
restart Bahmni:

```bash
cd bahmni-lite   # or bahmni-standard
./run-bahmni.sh
```

The stack will restart using the updated module configuration.
