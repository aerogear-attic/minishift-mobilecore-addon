# Minishift Mobile Core Add-on

## Set up
[Install minishift](https://docs.openshift.org/latest/minishift/getting-started/installing.html)  
[Install OC](https://docs.openshift.org/latest/cli_reference/get_started_cli.html#installing-the-cli)

Enable minishift experimental addons:
```sh
export MINISHIFT_ENABLE_EXPERIMENTAL=y
```

After Cloning this repo it will need to be added to the minishift addons catalog, this cannot be done from inside the directory, add it like so:
```sh
cd ..
minishift addon install -f minishift-mobilecore-addon/
minishift addons enable mobilecore
```

A few config values are required for this addon to function, as follows:
```sh
export DOCKERHUB_USERNAME=<docker hub username>
export DOCKERHUB_PASSWORD=<docker hub password>
export DOCKERHUB_ORG=<docker hub org, use 'aerogearcatalog' if you do not have your own>
minishift config set addon-env DOCKERHUB_USERNAME=${DOCKERHUB_USERNAME},DOCKERHUB_PASSWORD="${DOCKERHUB_PASSWORD}",DOCKERHUB_ORG=${DOCKERHUB_ORG}
```

## Check Minishift version
Minishift needs to be at least 1.11.0, check as follows
```sh
$ minishift version
minishift v1.11.0+4459917
```

## Configure Minishift
Although the default MiniShift will function just fine, for the best results, it is best to configure MiniShift to start with extra CPUs and RAM, this can be done with the following commands:
```sh
minishift config set cpus 4
minishift config set memory 4096
```

## Starting Minishift with Mobile Core enabled
Minishift must be both stopped and deleted for this to come up smoothly:
```sh
minishift stop
minishift delete
```

Create a new Minishift cluster with service catalog and the mobilecore with the following command:
```sh
minishift start --openshift-version 3.7.0 --service-catalog
```

If you did not enable the addon, you will need to apply it manually:
```sh
minishift addons apply mobilecore
```

## Troubleshooting
Generally most issues with this plugin can be resolved by doing a stop and delete, i.e.:
```sh
minishift stop
minishift delete
minishift start --openshift-version 3.7.0 --service-catalog
```

It is also possible that the addon-env config value is misconfigured, to confirm the values are correct you can review them by running:
```sh
minishift config get addon-env
```
