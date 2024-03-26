# GCP monioring



https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm search repo prometheus-community/kube-prometheus-stack --versions


helm upgrade --install prometheus-operator prometheus-community/kube-prometheus-stack \
    -n monitoring --create-namespace -f values.yaml 

kubectl get all -n monitoring


kubectl port-forward service/prometheus-operator-grafana 8080:80 -n monitoring

kubectl port-forward service/prometheus-operated 8080:9090 -n monitoring



kubectl get secret --namespace monitoring prometheus-operator-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

kubectl get secret neurorobotics-wildcard-tls --namespace=feagi -o yaml | sed 's/namespace: .*/namespace: monitoring/' | kubectl apply -f -



kubectl port-forward service/alertmanager-operated 8080:9093 -n monitoring
kubectl port-forward service/alertmanager-operated 8080:9093 -n monitoring