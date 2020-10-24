# erdemo-operator

Ansible Operator for installing the Emergency Response demo.

To install:
1. Clone this repository and `cd` into it.
```
git clone https://github.com/andykrohg/erdemo-operator
cd erdemo-operator 
```
1. Ensure you're logged in with `oc` as a `cluster-admin`
1. Run `hack/operate.sh` to install the `CustomResourceDefinition` and accompanying assets, and to create a `Deployment` for the operator. It will be created in the `erdemo-operator-system` namespace.
1. Create an `ErDemo` Custom Resource: `oc apply -n erdemo-operator-system -f config/samples/apps_v1alpha1_erdemo.yaml`
1. Watch the progress in the logs of the `tssc-operator-controller-manager` pod.
