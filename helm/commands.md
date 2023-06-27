#### Commands Ref

`helm version`
version.BuildInfo{Version:"v3.9.3", GitCommit:"414ff28d4029ae8c8b05d62aa06c7fe3dee2bc58", GitTreeState:"clean", GoVersion:"go1.17.13"}

`helm repo add bitnami https://charts.bitnami.com/bitnami`
"bitnami" has been added to your repositories

`helm repo list`
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