`helm install tomcat bitnami/tomcat`

NAME: tomcat
LAST DEPLOYED: Tue Jun 27 13:13:35 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: tomcat
CHART VERSION: 10.9.3
APP VERSION: 10.1.10

** Please be patient while the chart is being deployed **

1. Get the Tomcat URL by running:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        Watch the status with: `kubectl get svc --namespace default -w tomcat`

  `export SERVICE_IP=$(kubectl get svc --namespace default tomcat --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")`
  `echo "Tomcat URL:            http://$SERVICE_IP/"`
  `echo "Tomcat Management URL: http://$SERVICE_IP/manager"`

2. Login with the following credentials

  `echo Username: user`
  `echo Password: $(kubectl get secret --namespace default tomcat -o jsonpath="{.data.tomcat-password}" | base64 -d)`
  