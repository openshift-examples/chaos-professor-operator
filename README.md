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
