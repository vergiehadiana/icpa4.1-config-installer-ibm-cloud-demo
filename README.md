# icpa4.1-config-installer-ibm-cloud-demo
This is for Demo Only

Usage : 
oc login --token=<token-openshift-credentials> --server=<server-openshift-login>

export ENTITLED_REGISTRY=cp.icr.io
export ENTITLED_REGISTRY_USER=cp
export ENTITLED_REGISTRY_KEY=<copy-entitlement-registry-token-from:https://myibm.ibm.com/products-services/containerlibrary>
export OPENSHIFT_TOKEN=<token-openshift-credentials>
export OPENSHIFT_URL=<server-openshift-login>
docker login "$ENTITLED_REGISTRY" -u "$ENTITLED_REGISTRY_USER" -p "$ENTITLED_REGISTRY_KEY"

mkdir data; docker run -v $PWD/data:/data:z -u 0 -e LICENSE=accept "$ENTITLED_REGISTRY/cp/icpa/icpa-installer:4.1.1" cp -r "data/*" /data;

docker run -v ~/.kube:/root/.kube:z -u 0 -t -v $PWD/data:/installer/data:z -e LICENSE=accept -e ENTITLED_REGISTRY -e ENTITLED_REGISTRY_USER -e ENTITLED_REGISTRY_KEY -e OPENSHIFT_URL -e OPENSHIFT_TOKEN "$ENTITLED_REGISTRY/cp/icpa/icpa-installer:4.1.1" check | tee install-check-icpa4.1.log
docker run -v ~/.kube:/root/.kube:z -u 0 -t -v $PWD/data:/installer/data:z -e LICENSE=accept -e ENTITLED_REGISTRY -e ENTITLED_REGISTRY_USER -e ENTITLED_REGISTRY_KEY -e OPENSHIFT_URL -e OPENSHIFT_TOKEN "$ENTITLED_REGISTRY/cp/icpa/icpa-installer:4.1.1" install -v | tee install-icpa4.1.log
