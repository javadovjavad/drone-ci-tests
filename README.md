1. # KOPS create Cluster ###

  export KOPS_STATE_STORE="s3://ecs-ha-tfstate-test"
  export MASTER_SIZE="t2.medium"
  export NODE_SIZE="t2.medium"
  export ZONES="eu-central-1a,eu-central-1b,eu-central-1c"
  kops create cluster agayibov.tl.scntl.com \
  --node-count 3 \
  --zones $ZONES \
  --node-size $NODE_SIZE \
  --master-size $MASTER_SIZE \
  --master-zones $ZONES \
  --networking cilium \
  --topology private \
  --bastion="true" \
  --yes


2. ## Istio deploy cluster ##  Run these commands in terminal |                                       
  1) istioctl install
  2) kubectl label namespace default istio-injection=enabled  

3. ## Deploy demo project to k8s cluster with helm.

  helm install release1 test-helm/

4. ## Create istio-gateway and virtualservice for web application

   1) kubectl apply -f istio-gateway.yaml
   2) kubectl apply -f istio-virtualservice.yaml
