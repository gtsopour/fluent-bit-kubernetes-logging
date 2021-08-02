# Kubernetes Logging with Fluent Bit

[Fluent Bit](https://fluentbit.io) is an open source Log Processor and Forwarder which allows you to collect any data like metrics and logs from different sources, enrich them with filters and send them to multiple destinations. It's the preferred choice for containerized environments like Kubernetes as it enriches the logs with Kubernetes metadata. Fluent Bit is designed with performance in mind: high throughput with low CPU and Memory usage. Fluent Bit is a CNCF (Cloud Native Computing Foundation) subproject under the umbrella of Fluentd.

[Fluent Bit](https://fluentbit.io) must be deployed as a DaemonSet so that it will be available on every node of your Kubernetes cluster.

## Create a Kubernetes namespace
Please create a new namespace with the name logging for the Fluent Bit deployment.

`kubectl create namespace logging`

## Create RBAC resources for Fluent Bit
[Fluent Bit](https://fluentbit.io) must be deployed as a DaemonSet so that it will be available on every node of the Kubernetes cluster. To get started run the following commands to create the service account and role setup.

### Create ServiceAccount
`kubectl create -f https://raw.githubusercontent.com/gtsopour/fluent-bit-kubernetes-logging/master/fluent-bit-service-account.yaml`

### Create ClusterRole
`kubectl create -f https://raw.githubusercontent.com/gtsopour/fluent-bit-kubernetes-logging/master/fluent-bit-role.yaml`

### Create ClusterRoleBinding
`kubectl create -f https://raw.githubusercontent.com/gtsopour/fluent-bit-kubernetes-logging/master/fluent-bit-role-binding.yaml`

## Create Fluent Bit ConfigMap
The next step is to create a ConfigMap that will be used by the Fluent Bit DaemonSet.

`kubectl create -f https://raw.githubusercontent.com/gtsopour/fluent-bit-kubernetes-logging/master/fluent-bit-configmap.yaml`

## Create Fluent Bit DaemonSet
The next step is to create the Fluent Bit DaemonSet ready to be used with the Elasticsearch on a normal Kubernetes Cluster.

### Create Elasticsearch ConfigMap
`kubectl create -f https://raw.githubusercontent.com/gtsopour/fluent-bit-kubernetes-logging/master/elasticsearch-configmap.yaml`

### Create Elasticsearch Secret
`kubectl create -f https://raw.githubusercontent.com/gtsopour/fluent-bit-kubernetes-logging/master/elasticsearch-secret.yaml`

### Create DaemonSet
`kubectl create -f https://raw.githubusercontent.com/gtsopour/fluent-bit-kubernetes-logging/master/fluent-bit-ds.yaml`

