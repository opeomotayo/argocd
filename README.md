<!-- 1. Install Argo CD -->
kubectl create namespace argocd
kubectl apply -n argocd -f argocd

<!-- 2. Access The Argo CD API Server -->
kubectl apply -n argocd -f argocd/argocd-server-svc.yaml
#kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

<!-- 3. Download Argo CD CLI -->
brew install argocd

<!-- 4. Login Using The CLI -->
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
argocd login <ARGOCD_SERVER>
argocd account update-password

<!-- 5. Register A Cluster To Deploy Apps To -->
kubectl config get-contexts -o name
argocd cluster add docker-desktop

