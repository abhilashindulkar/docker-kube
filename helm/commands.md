## Linux Tweet App deployment through helm chart.

Refer the below commands:

* Creates a helm chart, update values.yaml with required docker image.
`helm create linux-tweet-app`

* Package Helm chart & store it into charts-repo.
`helm package linux-tweet-app -d charts-repo`

* Generate index.yaml under charts-repo.
`helm repo index charts-repo/`

* Lint/Check syntax.
`helm lint linux-tweet-app`

* Install helm chart.
`helm install linux-tweet-app ./linux-tweet-app`

* Remove/Delete helm chart.
`helm uninstall linux-tweet-app`