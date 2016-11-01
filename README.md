Demo app for Jenkins and Azure Service Fabric upgrades

## Background
Very simple Golang web app container listening on port 8001

SF Manifests will handle deployment and upgrade on SF Linux cluster 

## Instructions

Jenkins task to run below CLI commands. Had to manually install Azure CLI on Jenkins container. 

  ```
  APP_VERSION="1.1.${BUILD_NUMBER}"
  azure servicefabric application package copy cddemo fabric:ImageStore
  azure servicefabric application type register cddemo
  azure servicefabric application upgrade start --application-name fabric:/cddemoapp --target-application-type-version $APP_VERSION --rolling-upgrade-mode UnmonitoredAuto --upgrade-replica-set-check-timeout-in-seconds 100 --force-restart true
  ```