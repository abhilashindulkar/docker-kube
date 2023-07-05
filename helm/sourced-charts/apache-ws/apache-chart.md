`helm install bitnami/apache --generate-name --name-template "webserver-{{randAlpha 7 | lower}}"`

NAME: webserver-xizkwcb
LAST DEPLOYED: Tue Jun 27 16:29:45 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: apache
CHART VERSION: 9.6.3
APP VERSION: 2.4.57

** Please be patient while the chart is being deployed **

1. Get the Apache URL by running:

** Please ensure an external IP is associated to the webserver-xizkwcb-apache service before proceeding **
** Watch the status using: `kubectl get svc --namespace default -w webserver-xizkwcb-apache` **

  `export SERVICE_IP=$(kubectl get svc --namespace default webserver-xizkwcb-apache --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")`
  `echo URL            : http://$SERVICE_IP/`


WARNING: You did not provide a custom web application. Apache will be deployed with a default page. Check the README section "Deploying your custom web application" in https://github.com/bitnami/charts/blob/main/bitnami/apache/README.md#deploying-a-custom-web-application.
