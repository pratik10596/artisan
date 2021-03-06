<img src="https://github.com/gatblau/artisan/raw/master/artisan.png" width="150" align="right"/>

# Java Recipe - Quarkus & OpenShift Pipelines

This recipe provides a quick start for a Java Web Service using Quarkus and Tekton pipelines in OpenShift

## Getting Started

Ensure you have the following:
- artisan CLI installed
- this recipe is available from an Artisan registry and you know the {{registry-url}}
- oc client installed
- tkn client installed (optional)

Then follow the steps below:

```bash
# open the recipe in a folder where the project files will be located
art open {{registry-url}}/recipe/java-quarkus quarkus

# go into the project directory
cd quarkus/project

# initialise the project with the maven group and artefact id you want to use as follows:
art run -i init

# ensure you are logged in OpenShift using the oc CLI
oc login ...

# create the tekton pipeline in OpenShift as follows:
oc apply -f _build/flows/s2p_tkn.yaml

```

If you intend to store the pipeline resources in Git they should be encrypted first as follows:

```bash
## TLDR

# if you want to store the flow definition in git you MUST encrypt it as it contains
# all the credentials required by the pipeline
# you can use artisan to pgp encrypt it - ensure you have an encryption key pair stored in a safe place
# then to encrypt the pipeline resources:
art pgp encrypt -p path/to/public/key _build/flows/s2p_tkn.yaml

# the tekton definition can be deleted
rm _build/flows/s2p_tkn.yaml
```