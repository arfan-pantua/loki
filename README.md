# Installing and configuring Loki

## Create Iam Policy using cli
- `aws iam create-policy --policy-name allow-to-s3-monitoring-bucket --policy-document file://<path-to-monitoring-storage-policy.json>`
## Create namespace
- `kubectl create namespace loki`
## Attach policy to cluster using eksctl and create service account
- `eksctl create iamserviceaccount --name loki-service-account --cluster dev-20220411 --namespace=loki --attach-policy-arn arn:aws:iam::706050889978:policy/allow-to-s3-monitoring-bucket --approve --override-existing-serviceaccounts`
## Helming
### Prometheus Helm
- `helm repo add stable https://grafana.github.io/helm-charts`
- `helm upgrade --install loki --namespace loki grafana/loki --values .\values.yaml`

## Moving from PVC to Object Storage

## Create temporary pod 
`kubectl apply -f pod-ubuntu.yaml -n loki`
## Install python 
- `apt update && apt -y upgrade`
- `apt install software-properties-common -y`
- `add-apt-repository ppa:deadsnakes/ppa -y`
- `apt update`
-`apt install python3.8 -y`
## Running python script
- ### Copy Paste file script.py to local container and `chmod +x script.py` and `.\script.py`
- ### create a directory,temporary, to put file decoded of chunks. in my example i put on /home/loki/chunks-copy/fake
- ## Copy index from chunks directory to temporary directory of chunks
## Install AWS CLI
- `apt install curl -y`
- `apt install zip -y`
- `apt install vim -y`
- `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"`
- `unzip awscliv2.zip`
- `./aws/install`

## Copy paste data to S3
- `aws configure`
- `aws s3 cp <localdir> s3://<bucket-name>/<dir>` {aws s3 cp chunks-copy s3://hx-loki-test --recursive}
