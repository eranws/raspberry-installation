# Grafana
The admin user and password for Grafana are currently defined hardcoded in the docker-compose.yml to admin:kivsee12
## Grafana files explained
/dashboards/dashboard.yaml - Configuration yaml for grafana provisioning to automatically take .json files as dashboards  

NOTE: dashboards refer to a datasource using its UID, defined in the datasources.yaml

NOTE2: Changes saved to dashboards from within Grafana UI are not taken back to above mapped files, dashboards should be exported and files rewritten or changes will be reverted at next docker bringup

/datasources/datasources.yaml - Configuration yaml for grafana provisioning to automatically define datasources  

NOTE: datasource URL is currently hardcoded in yaml, consider to change it to come from ENV parameter
