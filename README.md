# Codefresh runner installation - helm chart

This helm chart will install Codefresh runner into your Kubernetes cluster. 
For additional information regarding "Codefresh Runner" look here: [https://codefresh.io/docs/docs/administration/codefresh-runner/](https://codefresh.io/docs/docs/administration/codefresh-runner/)


This helm chart support both Helm2 and Helm3.

## Prerequisite
1. If you are working on air-gapped environment (without internet access), make sure to push the image "codefresh/cli" into your local registry before proceeding with the installation, And set `image.repository` to your local repository.

2. Before you start to install this helm chart make sure you have a Codefresh API token, follow this doc for HOW-TO generate it: [https://codefresh.io/docs/docs/integrations/google-marketplace/#step-0---create-a-codefresh-api-key](https://codefresh.io/docs/docs/integrations/google-marketplace/#step-0---create-a-codefresh-api-key)
3. Clone this repo and pack the helm chart by executing:

`git clone https://github.com/codefresh-io/runner-installtion.git`

## Installation
1. Edit the file `values.yaml`. VERY IMPORTANT!!!

`helm install --namespace <NAMESPACE> --timeout 1500 <RELEASE-NAME> runner-installation`

## values.yaml parameters - all fields are MANDATORY
|                      |Description                                 |Default                 |
|----------------------|--------------------------------------------|------------------------|
|env.codefreshToken    |"Codefresh API Token."                      |<TOKEN_ID_YOU_GENERATED>|
|env.codefreshAgentName|"Codefresh agent name."                     |"defaultAgent"          |
|env.codefreshURL      |"Codefresh custom url, for on-prem install".|"https://g.codefresh.io"|
|image.repository      |"The codefresh-cli image path".             |codefresh/cli           |
|image.imagePullSecrets|"list of kubernetes pull images secrets     | []  (empty list)       |




env:
  codefreshToken: <TOKEN_ID_YOU_GENERATED>
  codefreshAgentName: "defaultAgent"
  codefreshURL: "https://g.codefresh.io"
  #codefreshKubeNamespace: "default"
