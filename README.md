# helm-charts

+ GitOps for Customer Runner Image Building
+ Repo for helm charts image
+ Custom Runner Github Actions Kubernetes


1. Install Helm
2. Add Helm repo - helm repo add --username <USERNAME> --password <GITHUB_PAT> thesis https://raw.githubusercontent.com/UQThesisENGG7817/helm-charts/gh-pages
3. helm repo update thesis - to retrieve the latest versions of the packages.
4. helm search repo thesis to see the charts.
5. Install - helm install <chart-name> thesis/<chart-name>
6. Uninstall - helm delete <chart-name>