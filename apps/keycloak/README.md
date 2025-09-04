# Keycloak setup

This directory contains files related to the Keycloak identity provider used by Bahmni.

## Initial setup
1. Start Keycloak with docker compose:
   ```bash
   docker compose up -d keycloak
   ```
2. Sign in at [http://localhost:8081](http://localhost:8081) with the admin credentials from `.env` (`KEYCLOAK_ADMIN_USER`/`KEYCLOAK_ADMIN_PASSWORD`).
3. Create a realm matching `KEYCLOAK_REALM`.
4. Create clients for the Bahmni services using the IDs defined in `.env`:
   - `KEYCLOAK_CLIENT_OPENMRS`
   - `KEYCLOAK_CLIENT_ODOO`
   - `KEYCLOAK_CLIENT_OPENELIS`
   - `KEYCLOAK_CLIENT_BAHMNI_WEB`
5. Configure redirect URIs and grant types for each client as required.
6. Restart the Bahmni containers so they can authenticate against Keycloak.

Realm export files placed in this directory will be mounted into the Keycloak container for import on startup.
