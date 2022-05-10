## Grafana files explained
/dashboards/dashboard.yaml - Configuration yaml for grafana provisioning to automatically take .json files as dashboards  

NOTE: dashboards refer to a datasource using its UID, defined in the datasources.yaml

/datasources/datasources.yaml - Configuration yaml for grafana provisioning to automatically define datasources  

NOTE: datasource URL is currently hardcoded in yaml, consider to have it from ENV
