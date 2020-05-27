# Demo helm chart of chaos professor 👨‍🏫

## How to deploy

```
git clone ..
helm install chaos-professor .
```

## Package

```
helm package .
helm install  chaos-professor chaos-professor-0.1.0.tgz
```

## Upgrade

...
$ helm list
NAME           	NAMESPACE	REVISION	UPDATED                              	STATUS  	CHART                	APP VERSION
chaos-professor	helm-demo	1       	2020-05-27 23:10:23.135905 +0200 CEST	deployed	chaos-professor-0.1.0

$ helm upgrade chaos-professor .
Release "chaos-professor" has been upgraded. Happy Helming!
NAME: chaos-professor
LAST DEPLOYED: Wed May 27 23:29:32 2020
NAMESPACE: helm-demo
STATUS: deployed
REVISION: 2
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace helm-demo -l "app.kubernetes.io/name=chaos-professor,app.kubernetes.io/instance=chaos-professor" -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl port-forward $POD_NAME 8080:80

$ helm list
NAME           	NAMESPACE	REVISION	UPDATED                              	STATUS  	CHART                	APP VERSION
chaos-professor	helm-demo	2       	2020-05-27 23:29:32.256814 +0200 CEST	deployed	chaos-professor-0.1.1
...