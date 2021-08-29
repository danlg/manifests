## Notes Dan following ArgoCD experience & Body work discovery
- use manifest instead of argocd for now (better control & understanding of kubeflow)
- refine Value Prop

## Notes with Davis van der Spek

https://hub.docker.com/u/kubeflownotebooks

had to set up a user

Technologies David van der Spek mentioned:
https://harvesterhci.io/ to manage VM on prems or hybrid via K8S
- which is using Longhorn : a lightweight, reliable and easy-to-use distributed block storage system for Kubernetes. => https://longhorn.io/docs/1.1.2/what-is-longhorn/
- KubeVIRT: KubeVirt technology addresses the needs of development teams that have adopted or want to adopt Kubernetes but possess existing Virtual Machine-based workloads that cannot be easily containerized. More specifically, the technology provides a unified development platform where developers can build, modify, and deploy applications residing in both Application Containers as well as Virtual Machines in a common, shared environment.

- ISTIO: Istio service mesh allows to monitor, visualize, and manage traffic between pods and external services by injecting a proxy container - a sidecar - which forwards inbound and outbound traffic of a pod/virtual machine. This allows the sidecar to collect metadata about the proxied traffic and also actively interfere with it.
The main features of Istio are traffic shifting (migrating traffic from an old to new version of a service), dynamic request routing, fault injection or traffic mirroring for testing/debugging purposes, and more.

 in order for auth service to work, had to set up multiple service on which auth OIDC AuthService is dependent on: 
1. pvc 
2. csi-hostpath-driver
3. storage-provisioner  
4. profiles-deployment
5. add user profile
cat <<EOF | kubectl apply -f -
apiVersion: kubeflow.org/v1
kind: Profile
metadata:
  name: dan
spec:
  # Add fields here
  owner:
    kind: User
    name: dan@aitransfo.com
EOF
______
he mentioned kale



https://github.com/elyra-ai/elyra

 692  kubectl delete pod -n istio-system authservice-0
  693  k get pods -A
  694  kubectl delete pod -n istio-system authservice-0
  695  k get pods -A
  696  kubectl decribe pod -n istio-system authservice-0
  697  kubectl describe pod -n istio-system authservice-0
  698  minikube addons list
  699  k get pvc -A
  700  minikube addons enable csi-hostpath-driver 
  701  kubectl describe pod -n istio-system authservice-0
  702  k get pvc -A
  703  k  delete pvc -n istio-system   authservice-pvc
  704  k  get pvc -n istio-system   authservice-pvc
  705  kubectl apply -f -n istio-system https://github.com/kubeflow/manifests/raw/master/common/oidc-authservice/base/pvc.yaml
  706  kustomize build common/oidc-authservice/base | kubectl apply -f -
  707  k  get pvc -n istio-system   authservice-pvc
  708  k get pods -A
  709  k get pods -n istio-system 
  710  minikube addons list
  711  minikube addons enable kustomize build common/oidc-authservice/base | kubectl apply -f -
  712  minikube addons enable storage-provisioner 
  713  k get pods -A
  714  k get pods -n istio-system
  715  jobs
  716  fg 1
  717  kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
  720  k get pods -A
  721  find . -name "*.crt"
  722  ls -lrt
  723  minikube ssh
  724  k get pods -A
  725  cat <<EOF | kubectl apply -f -
  726  k get profile 
  727  k get namespaces
  728  k describe profile user
  729  k describe profile dan
  730  k get -n kubeflow pods
  731  kustomize build apps/profiles/upstream/overlays/kubeflow | kubectl apply -f -
  732  k get -n kubeflow pods
  733  kustomize build common/kubeflow-roles/base | kubectl apply -f -