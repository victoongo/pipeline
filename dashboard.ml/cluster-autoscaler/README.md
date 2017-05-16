https://github.com/kubernetes/kops/tree/master/addons/cluster-autoscaler

Notes from README:

# Cluster Autoscaler Addon

Note that you likely want to change `AWS_REGION` and `GROUP_NAME`, and probably `MIN_NODES` and `MAX_NODES`

```bash
CLOUD_PROVIDER=aws
IMAGE=gcr.io/google_containers/cluster-autoscaler:v0.4.0
MIN_NODES=1
MAX_NODES=2
AWS_REGION=us-west-2
GROUP_NAME="nodes.your.domain.com"
SSL_CERT_PATH="/etc/ssl/certs/ca-certificates.crt" # ("/etc/ssl/certs" for gce)

addon=cluster-autoscaler.yml
wget -O ${addon} https://raw.githubusercontent.com/kubernetes/kops/master/addons/cluster-autoscaler/v1.4.0.yaml

sed -i -e "s@{{CLOUD_PROVIDER}}@${CLOUD_PROVIDER}@g" "${addon}"
sed -i -e "s@{{IMAGE}}@${IMAGE}@g" "${addon}"
sed -i -e "s@{{MIN_NODES}}@${MIN_NODES}@g" "${addon}"
sed -i -e "s@{{MAX_NODES}}@${MAX_NODES}@g" "${addon}"
sed -i -e "s@{{GROUP_NAME}}@${GROUP_NAME}@g" "${addon}"
sed -i -e "s@{{AWS_REGION}}@${AWS_REGION}@g" "${addon}"
sed -i -e "s@{{SSL_CERT_PATH}}@${SSL_CERT_PATH}@g" "${addon}"

kubectl create -f ${addon}
```
