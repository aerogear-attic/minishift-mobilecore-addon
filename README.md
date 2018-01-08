#Minishift Mobile Core addon

## Set up
If you have not yet, [Install minishift](https://docs.openshift.org/latest/minishift/getting-started/installing.html).

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
export DOCKERHUB_ORG=<docker hub org>
minishift config set addon-env DOCKERHUB_USERNAME=${DOCKERHUB_USERNAME},DOCKERHUB_PASSWORD='${DOCKERHUB_PASSWORD}',DOCKERHUB_ORG=${DOCKERHUB_ORG}
```

## Check Minishift version
Minishift needs to be at least 1.11.0, check as follows
```sh
$ minishift version
minishift v1.11.0+4459917
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

