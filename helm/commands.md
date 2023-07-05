#### Commands Reference

`helm version`
version.BuildInfo{Version:"v3.9.3", GitCommit:"414ff28d4029ae8c8b05d62aa06c7fe3dee2bc58", GitTreeState:"clean", GoVersion:"go1.17.13"}

`helm repo add bitnami https://charts.bitnami.com/bitnami`
"bitnami" has been added to your repositories

`helm repo list` or `helm repo ls`
NAME    URL                               
bitnami https://charts.bitnami.com/bitnami

`helm search repo mysql`
NAME                    CHART VERSION   APP VERSION     DESCRIPTION                                       
bitnami/mysql           9.10.4          8.0.33          MySQL is a fast, reliable, scalable, and easy t...
bitnami/phpmyadmin      11.1.3          5.2.1           phpMyAdmin is a free software tool written in P...
bitnami/mariadb         12.2.5          10.11.4         MariaDB is an open source, community-developed ...

`helm search repo mysql --version 7.3.2`
NAME                    CHART VERSION   APP VERSION     DESCRIPTION                                       
bitnami/mariadb-galera  7.3.2           10.6.8          MariaDB Galera is a multi-primary database clus...

`helm repo remove bitnami`
"bitnami" has been removed from your repositories

`helm install mysql bitnami/mysql -n temp`
To install MySQL in specific namespace.

`helm list -n temp`
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
mysql   temp            1               2023-06-27 12:04:01.063933022 +0000 UTC deployed        mysql-9.10.4    8.0.33

`helm uninstall mysql -n temp`
release "mysql" uninstalled

`helm install mysql bitnami/mysql --values values.yaml`
With custom configuration.

`helm repo update`
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈
Clears local cache and pulls the latest chart from the configured repo.

`helm upgrade mysql bitnami/mysql --set image.pullPolicy=Always`
Imperative command to upgrade app/chart.

`helm upgrade mysql bitnami/mysql --values values.yaml`
Upgrade to latest version chart.

`helm upgrade mysql bitnami/mysql --reuse-values`
To reuse the values config while upgrading.

`helm uninstall mysql --keep-history`
Uninstall chart and retain version history.

`helm install mysql bitnami/mysql --dry-run`
Dry-run to check if the chart is deployable.

`helm template mysql bitnami/mysql --values values.yaml`
Generates YAML templates for kubernetes deployment.

`helm get notes mysql`
Get release notes for deployed app through helm chart.

`helm get values mysql`
Get user supplied values for the specified chart.

`helm get values mysql --all`
Get all predefined values for the specified chart.

`helm get values mysql --revision 1`
Get user supplied values for the specified chart in revision(version) 1.

`helm get manifest mysql --revision 1`
Get k8s objects manifest for the specified chart in revision(version) 1.

`helm history mysql`
REVISION        UPDATED                         STATUS          CHART           APP VERSION     DESCRIPTION     
1               Tue Jun 27 15:47:42 2023        deployed        mysql-9.10.4    8.0.33          Install complete

`helm rollback mysql 1`
Rollback was a success! Happy Helming!
EVISION        UPDATED                         STATUS          CHART           APP VERSION     DESCRIPTION     
1               Tue Jun 27 15:47:42 2023        superseded      mysql-9.10.4    8.0.33          Install complete
2               Tue Jun 27 16:13:46 2023        superseded      mysql-9.10.4    8.0.33          Upgrade complete
3               Tue Jun 27 16:16:43 2023        deployed        mysql-9.10.4    8.0.33          Rollback to 1

`helm install apache bitnami/apache -n test-ns --create-namespace`
Creates Namespace, Installs apache chart.

`helm upgrade --install apache bitnami/apache`
Upgrade if already installed or just install. Useful in CI/CD.

`helm install bitnami/apache --generate-name --name-template "webserver-{{randAlpha 7 | lower}}"`
Generate name, template with lower, random alphabets for chart.

`helm install apache bitnami/apache --wait --timeout 7m`
Default wait time is 5m. timeout is set to 7m. Measures to mark deployment healthy/unhealthy. Includes image pull, deployment status.

`helm install apache bitnami/apache --atomic`
Avoid failure, rollbacks to previous successful revision. Useful in CI/CD.

`helm upgrade tomcat bitnami/tomcat --force`
Delete existing deployment, deploys new one, create pods. It will have downtime.

`helm upgrade tomcat bitnami/tomcat --cleanup-on-failure`
Not good for debugging, cleans up failed upgrade.

`helm uninstall $(helm list | awk 'NF=1' | awk 'NR>=2')`
release "apache-1687884819" uninstalled
release "mysql" uninstalled
release "webserver-xizkwcb" uninstalled

---

`helm create demo-chart`
Creates a custom chart with default nginx configuration.

`helm install demo-chart ./demo-chart/`
Installs demo-chart.

`helm package demo-chart`
Successfully packaged chart and saved it to: ./demo-chart-0.1.0.tgz

`helm package demo-chart -u`
Packages helm chart but updates dependencies(other charts) first.

`helm lint demo-chart`
==> Linting demo-chart - Checks syntax for all the template within chart.
[INFO] Chart.yaml: icon is recommended
1 chart(s) linted, 0 chart(s) failed

`helm dependency update demo-chart`
Updates chart with dependencies.

`helm test app-release`
Tests app release with helm hook test.

`helm repo index charts-repo/`
Generates index.yaml for local chart repository. Can be used after packaging other chart in local repo.

---

`python3 -m http.server --bind 127.0.0.1 8080`
Hosts chart repo on web server.

`helm repo add local-repo http://localhost:8080`
Adds local-repo to the list of chart repositories.

`helm install second-chart local-repo/second-chart`
Installs local-repo's second-chart.

---

`helm pull local-repo/second-chart`
Pulls chart from local-repo with .tgz extension.

`helm repo add gitrepo https://abhilashindulkar.github.io/githelmrepo`
Adds git repo to the list of chart repositories.

---
`export HELM_EXPERIMENTAL_OCI=1`
Enables OCI.

`docker run -d --name oci-registry -p 5000:5000 registry`
Runs OCI registry as container on docker environment.

`helm push demo-chart-0.1.tar.gz oci://localhost:5000/helm-charts`
Push packaged chart to OCI registry named helm-charts.

`helm pull oci://localhost:5000/helm-charts/second-chart --version 0.1.0`
Pulls second chart from OCI registry to local.

 `helm install second-chart oci://localhost:6000/helm-charts/second-chart --version 0.1.0`
 Installs second-chart through OCI registry with specified chart version.

 ---

 ##### Chart Security

 PGP - Pretty Good Privacy.
 GPG - GNU Private Guard, open source implementation of PGP for encrypting files. Provides digital encryption & signing services using OpenPGP standard.

`gpg --version`

gpg (GnuPG) 2.2.27
libgcrypt 1.9.4

`gpg --full-generate-key`
Generate encryption keys.

`gpg --export-secret-keys > cust-secring.gpg`
Export kbx extensioned keys to secring.gpg in ~/.gnupg/ directory.

`helm package --sign --key user@goog.com --keyring ~/.gnupg/cust-secring.gpg new-chart -d charts-repo`
Packages helm chart under chart-repo directory, encrypts with GNUPG private key. Also creates provenance file that digital signature.

`helm verify chart-repo/new-chart-0.1.0.tgz --keyring ~/.gnupg/cust-secring.gpg`
Verifies digital signature of Packaged chart.

`helm install --verify --keyring ~/.gnupg/cust-secring.gpg new-chart localrepo/new-chart`
Verifies Helm chart's digital signature, Installs at the same time.

---

##### Howto - Starters

`helm env HELM_DATA_HOME`
Gets the directory where starters are stored.
Example - /home/abhilash/.local/share/helm. Create a helm directory if it doesn not exist and within it, a subdirectory called starters.

Move a chart (reusable) to starters directory. Rename it if necessary. Replace all the manifest files chart name reference with <CHARTNAME> as a placeholder. Once done, save all the files.

`helm create --starter starter-reusable-chart demo-chart`
Uses starter chart to create demo-chart.

---

##### Howto - Plugins

`helm plugin list`
List all plugins. A Plugin has to defined with usage, executable command.

`helm plugin install plugin-name`
Installs an existing plugin. To install a custom one, specify a path to plugin.yaml file.
Example - 
```
helm plugin install .
Installed plugin: echoplugin

helm echoplugin 
The plugin echoplugin is located in /home/abhilash/.local/share/helm/plugins/custom-plugin
```
`helm plugin update plugin-name`
Updates a plugin.

`helm plugin remove plugin-name`
Removes/Deletes a plugin.
