# Bahmni Docker

Refer this [Wiki Page](https://bahmni.atlassian.net/wiki/spaces/BAH/pages/299630726/Running+Bahmni+on+Docker) for Running Bahmni on Docker for detailed instructions.

## Running Bahmni LITE or STANDARD using docker compose:
1. Navigate to the relevant subfolder for your desired configuration. For example: `cd bahmni-lite`.
2. Execute the script: `./run-bahmni.sh`. This script provides various options such as start, stop, view logs, pull updates, reset, etc.
3. Before executing the above commands, ensure that your `.env` file in the sub-folder is correctly configured with the appropriate PROFILE.

Alternatively, if you wish to use docker compose commands directly, you can use the --env-file option to pass the environment variables files:
```shell
docker compose up --env-file .env
```

## Environment Variable Configuration For Bahmni Lite
The `.env` and `.env.dev` files are used for configuring environment variables for the Bahmni Lite Docker setup. 

The `.env` file points to the `1.0.0` image tag, which represents the stable and tested version of Bahmni Lite v1.0.0. We recommend using these images for production purposes. 
The `.env.dev` file points to the `latest` image version, which provides the most recent updates for development and testing purposes.

- By default `run-bahmni.sh` script runs with the `.env`, that uses the `1.0.0` images
```shell
run-bahmni.sh
```

- Instead if you wish to use the `latest` images, run the `run-bahmni.sh` script with the argument `.env.dev`
```shell
run-bahmni.sh .env.dev
```

- Additionally, you have the flexibility to create your own environment variable configuration. To do this, create a custom a `.env` file (eg: `.env.local`) and run the run-bahmni.sh script with the `.env.local` argument:
```shell
run-bahmni.sh .env.local
```

Please choose the appropriate environment variables file based on your requirements and make sure the respective `.env` or `.env-dev` file is properly configured before running the commands.

For detailed instructions and further information, please refer to the [Wiki Page](https://bahmni.atlassian.net/wiki/spaces/BAH/pages/299630726/Running+Bahmni+on+Docker) mentioned above.

## Orthanc PACS Integration

The `bahmni-standard` compose file now includes an [Orthanc](https://www.orthanc-server.com/) service for handling DICOM images. Orthanc exposes the HTTP interface on port `8042` and the DICOM listener on port `4242`. Default credentials are `admin`/`orthanc` and the data is persisted in the `orthanc-data` Docker volume.

The PACS integration container is configured to communicate with Orthanc by default. To customise the connection, update the following environment variables in the `.env` file:

```
PACS_SERVER_TYPE=ORTHANC
PACS_SERVER_URL=http://orthanc:8042
PACS_SERVER_USERNAME=admin
PACS_SERVER_PASSWORD=orthanc
```

An example viewer configuration for Bahmni UI is provided at `bahmni-standard/orthanc-viewer-config.json` which points the viewer to the Orthanc web explorer.
