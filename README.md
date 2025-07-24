# prod-grade-logstash-helmchart

Deploying and Optimizing a Production-Grade Logstash Helm Chart

A production-ready Logstash deployment on Kubernetes using the official Helm chart is built.  
This Logstash instance collects, transforms, and forwards logs to Elasticsearch for storage and visualization in Kibana.  
It also exposes metrics to Prometheus, which are visualized in Grafana dashboards. However, the grafana dashboard is to be manually imported on grafana UI with the json file in the folder.
The structure assumes prometheus and grafana are already installed(elasticsearch and kibana aswell) and the scrape config on prometheus.yml is to be manually added to an already existing prometheus.yml scrape config file.
The structure also assumes that Elasticsearch has a CA cert in the ca.crt which will be base64 coded and pasted in the secrets/logstash-tls-secret.yaml.
Also added are persistent storage, secure communication with TLS, environment-based secrets, and performance tuning with JVM and resource limits.

Tests
A dry run command :
helm upgrade --install logstash elastic/logstash \
 -f values/logstash-values.yaml \
 --namespace logstash \
 --dry-run \
 --debug
was ran after elastic https://helm.elastic.co repo was added using helm
The dry run confirmed the following:
Logstash will be installed with the correct config.

Your input plugins (Beats + HTTP) and output to Elasticsearch are recognized.

TLS is wired in via cacert.

Prometheus endpoint will be exposed on port 9800.

PVCs will be created and mounted.

Your resource requests and limits are valid.

Kubernetes manifests were rendered: StatefulSet, Services, ConfigMap, etc.
Generally meaning the helm chart is deployment ready.
