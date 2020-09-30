# Codefresh runner installation - helm chart

This helm chart will install Codefresh runner into your Kubernetes cluster. 
For additional information regarding "Codefresh Runner" look here: [https://codefresh.io/docs/docs/administration/codefresh-runner/](https://codefresh.io/docs/docs/administration/codefresh-runner/)


This helm chart support both Helm2 and Helm3.

## Prerequisite
1. If you are working on air-gapped environment (without internet access), make sure to push the image "codefresh/cli" into your local registry before proceeding with the installation, And set `image.repository` to your local repository.

2. Before you start to install this helm chart make sure you have a Codefresh API token, follow this doc for HOW-TO generate it: [https://codefresh.io/docs/docs/integrations/google-marketplace/#step-0---create-a-codefresh-api-key](https://codefresh.io/docs/docs/integrations/google-marketplace/#step-0---create-a-codefresh-api-key)
3. Clone this repo and pack the helm chart by executing:

`git clone https://github.com/codefresh-io/runner-installation.git`

## Installation
1. Edit the file `values.yaml`. VERY IMPORTANT!!!

1. Create namespace `kubectl create ns <NAMESPACE>`

1. (Optional) If using k8s secrets for your token, create a secret using: `kubectl create secret generic codefresh-secrets --from-literal=token=<TOKEN_ID_YOU_GENERATED> -n <NAMESPACE>` or follow [steps from the kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/secret/#creating-a-secret)

1. Run helm installation: `helm install --namespace <NAMESPACE> --timeout 1500s <RELEASE-NAME> .`

## values.yaml parameters - all fields are MANDATORY
|                            |Description                                 |Default                 |
|----------------------------|--------------------------------------------|------------------------|
|env.codefreshToken          |"Codefresh API Token."                      |<TOKEN_ID_YOU_GENERATED>|
|env.codefreshTokenSecret    |"Codefresh API Token, secret references"    |                        |
|env.codefreshAgentName      |"Codefresh agent name."                     |"defaultAgent"          |
|env.codefreshURL            |"Codefresh custom url, for on-prem install".|"https://g.codefresh.io"|
|image.repository            |"The codefresh-cli image path".             |codefresh/cli           |
|image.imagePullSecrets      |"list of kubernetes pull images secrets     | []  (empty list)       |




env:
  codefreshToken: <TOKEN_ID_YOU_GENERATED>
  codefreshAgentName: "defaultAgent"
  codefreshURL: "https://g.codefresh.io"
  #codefreshKubeNamespace: "default"
