# Chaos professor operator 

## Build new one
```
operator-sdk new chaos-professor-operator \
  --type=helm \
  --helm-chart=chaos-professor-0.1.1.tgz

sed -i 's|REPLACE_IMAGE|quay.io/openshift-examples/chaos-professor-operator:latest|g' deploy/operator.yaml

```

## Deploy operator direct
```
# Requires cluster-admin!
oc apply -f deploy/crds/charts.helm.k8s.io_chaosprofessors_crd.yaml

oc apply -f deploy/service_account.yaml
oc apply -f deploy/role.yaml
oc apply -f deploy/role_binding.yaml
oc apply -f deploy/operator.yaml
oc wait --for=condition=available deployment/chaos-professor-operator
oc apply -f deploy/crds/charts.helm.k8s.io_v1alpha1_chaosprofessor_cr.yaml
```

## Bundle operator

https://sdk.operatorframework.io/docs/olm-integration/user-guide/#creating-a-bundle

#### Generate CSV

```
$ operator-sdk generate csv --csv-version 0.1.0
INFO[0000] Generating CSV manifest version 0.1.0
INFO[0000] Fill in the following required fields in file chaos-professor-operator.clusterserviceversion.yaml:
	spec.description
	spec.keywords
	spec.provider
INFO[0000] CSV manifest generated successfully
```

#### Create annotations & Dockerfile

```
operator-sdk bundle create \
  --package chaos-professor-operator \
  --generate-only \
  --channels beta,stable \
  --default-channel beta
```

#### Validate bundle

```
operator-sdk bundle validate deploy/olm-catalog/chaos-professor-operator/
```

#### Build bundle image

```
docker build -f bundle.Dockerfile -t quay.io/openshift-examples/chaos-professor-operator-bundle:v0.1.0 .
```


### Build index for olm catalog source
#### Initial

```
opm index add \
  --build-tool docker \
  --bundles quay.io/openshift-examples/chaos-professor-operator-bundle:v0.1.0 \
  --tag  quay.io/openshift-examples/chaos-professor-operator-index:latest

docker push quay.io/openshift-examples/chaos-professor-operator-index:latest
```

#### Update / add new version

TBD