kubectl create ns spring-petclinic
kubectl create secret generic app-insights-key -n spring-petclinic --from-literal=instrumentation-key=InstrumentationKey=210a5162-d8de-44d7-b13e-d19840733236;IngestionEndpoint=https://swedencentral-0.in.applicationinsights.azure.com/;LiveEndpoint=https://swedencentral.livediagnostics.monitor.azure.com/;ApplicationId=68d8a4cf-55aa-472b-8c14-920023891914

kubectl create secret generic appinsights-blob-secret -n spring-petclinic --from-literal=azurestorageaccountname=lysasc --from-literal=azurestorageaccountkey="sp=r&st=2025-12-24T23:18:24Z&se=2025-12-31T07:33:24Z&skoid=3be1baa4-f088-4261-97fa-d0df3d311d2c&sktid=9fd22a09-4fff-4e8b-9a26-89f025c58774&skt=2025-12-24T23:18:24Z&ske=2025-12-31T07:33:24Z&sks=b&skv=2024-11-04&spr=https&sv=2024-11-04&sr=c&sig=vL3TMErfzi19ZOYi1GpZveCzdxPm0y1rxWmCuq5cV6s%3D" --type=Opaque

az aks update --name ly-swc-aks-02 --resource-group lyantovski-sc-rg --enable-blob-driver

helm upgrade --install customers-db-mysql oci://registry-1.docker.io/bitnamicharts/mysql --namespace spring-petclinic --set image.tag=bitnamilegacy/mysql:9.4.0-debian-12-r1 --set auth.database=service_instance_db

helm install -n spring-petclinic vets-db-mysql oci://registry-1.docker.io/bitnamicharts/mysql --set auth.database=service_instance_db --set image.repository=bitnamilegacy/mysql

helm install -n spring-petclinic visits-db-mysql oci://registry-1.docker.io/bitnamicharts/mysql --set auth.database=service_instance_db --set image.repository=bitnamilegacy/mysql

