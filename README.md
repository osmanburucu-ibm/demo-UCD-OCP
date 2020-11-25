# demo-UCD-OCP

demoing for deploying apps to openshift using urbancode deploy

## Kubetoy

[UCD Application Export json](KubeToy.json)

## Setup

### KubeToy App

#### KubeToy Settings

* ![KubeToy App](attachments/Kubetoy-App-Settings.png)

#### Environments

* ![KubeToy ENV](attachments/Kubetoy-App-Environments.png)

#### ENV Resources

* ![KubeToy ENV-res](attachments/Kubetoy-App-ENV-resources.png)

#### ENV Properties
  
* oc-project: ozdemo01
* oc-token: Token to get from [copy login commands]
* oc-url: url to get from [copy login commands]
* ![KubeToy ENV-res](attachments/Kubetoy-App-ENV-properties.png)

### KubeToy component

#### component configuration

* Source Configuration Type: git
* [Repository url](https://github.com/IBM-ICP-CoC/KubeToy.git): <https://github.com/IBM-ICP-CoC/KubeToy.git>

* ![Kubetoy component config 1](attachments/Component-Kubetoy_configuration-01.png)
* ![Kubetoy component config 2](attachments/Component-Kubetoy_configuration-02.png)
* ![Kubetoy component config 3](attachments/Component-Kubetoy_configuration-03.png)

#### Processes

* Deploy
  * using mostly OCP Plugin steps
  * ![Deploy](attachments/Process-Deploy.png)
    * STEPS
      * ![List files](attachments/List_files.png) and ![List Deployment files](attachments/List_Deployment_files.png) are shell steps to show downloaded files
      * Login:
        * ![OCP Plugin Login Step](attachments/ocp-plugin-login.png)
        * for the token field i have used the reference
        *

         ~~~sh
         ${p:environment/oc-token}
         ~~~

      * Apply:
        * ![OCP Plugin Apply Step](attachments/ocp-plugin-apply.png)
        * File to use: kubetoy-all-in-one.yaml
        * for Access Token i have used:

        ~~~sh
         ${p:environment/oc-token}
        ~~~

      * Create Route:
        * ![Shell: create route](attachments/OpenShift_create_route.png)

        ~~~sh
        #!/bin/sh
        export KUBECONFIG=./kubeconfig
        oc expose service kubetoy-service -l name=kubetoy-route --name=kubetoy-route
        ~~~

        * no create route step available
      * OpenShift get Pods (Shell)

        ~~~sh
        oc login --token=${p:environment/oc-token} --server=${p:environment/oc-url}
        oc get pods
        ~~~

* Deploy-Kubetoy
  * uses shell commands
  * ![Deploy-Kubetoy](attachments/Process-Deploy-Kubetoy.png)
  * ![OpenShift Login and Display OpenShift Details](attachments/OpenShift_Login_and_Display_OpenShift_Details.png)
  * ![OpenShift Apply (shell)](attachments/OpenShift_Apply-Shell.png)
  * ![Create Route to Kubetoy (shell)](attachments/OpenShift_Create_Route_to_KubeToy-shell.png)
