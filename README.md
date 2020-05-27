# Chaos professor operator 

## Build new one
```
operator-sdk new chaos-professor-operator \
  --type=helm \
  --helm-chart=chaos-professor-0.1.1.tgz

sed -i 's|REPLACE_IMAGE|quay.io/openshift-examples/chaos-professor-operator:latest|g' deploy/operator.yaml

```