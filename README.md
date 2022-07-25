# consul-hashicorp

## How to install Consul Service mesh in AWS.

```
root@dev-server01:~# cat values.yaml
global:
  name: consul
  datacenter: hashidc1
ui:
  enabled: true
  service:
    type: LoadBalancer
root@dev-server01:~#


root@dev-server01:~# helm repo add hashicorp https://helm.releases.hashicorp.com

root@dev-server01:~# helm repo list
NAME            URL
localstack      https://helm.localstack.cloud
bitnami         https://charts.bitnami.com/bitnami
stable          https://charts.helm.sh/stable
hashicorp       https://helm.releases.hashicorp.com


root@dev-server01:~# helm install --values values.yaml consul hashicorp/consul --create-namespace --namespace consul --version "0.43.0"
NAME: consul
LAST DEPLOYED: Mon Jul 25 21:24:11 2022
NAMESPACE: consul
STATUS: deployed
REVISION: 1
NOTES:
Thank you for installing HashiCorp Consul!

Your release is named consul.

To learn more about the release, run:

  $ helm status consul
  $ helm get all consul

Consul on Kubernetes Documentation:
https://www.consul.io/docs/platform/k8s

Consul on Kubernetes CLI Reference:
https://www.consul.io/docs/k8s/k8s-cli

root@dev-server01:~# kubectl get services --namespace consul
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)        AGE
consul-dns      ClusterIP      10.100.179.122   <none>      53/TCP,53/UDP    4m24s
consul-server   ClusterIP      None             <none>    8500/TCP,8301/TCP,8301/UDP,8302/TCP,8302/UDP,8300/TCP,8600/TCP,8600/UDP   4m24s
consul-ui       LoadBalancer   10.100.25.248    xxxxx.ap-south-1.elb.amazonaws.com   80:31872/TCP        4m24s
root@dev-server01:~#


```
