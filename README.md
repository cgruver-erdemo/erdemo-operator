# erdemo-operator

Ansible Operator for installing the Emergency Response demo.

## Quick Start
1. Login to an OpenShift cluster as a `cluster-admin`
2. Create a `CatalogSource` to import the Emergency Response Demo operator catalog.
```bash
oc apply -f - << EOF
apiVersion: operators.coreos.com/v1alpha1
kind: CatalogSource
metadata:
  name: erdemo-operators
  namespace: openshift-marketplace
spec:
  sourceType: grpc
  image: quay.io/akrohg/erdemo-operator-catalog:latest
  displayName: Emergency Response Demo Operator
  publisher: RedHatGov
EOF
```
3. Create a project named **erdemo-operator-system** for your operator deployment to live.
```bash
oc new-project erdemo-operator-system
```
4. In the OpenShift Web Console, navigate to **Operators -> OperatorHub** and search for "Emergency Response Demo Operator" in the **erdemo-operator-system** project. Select it and click **Install**
5. Set **Installation Mode** to *A specific namespace on the cluster* and set **Installed Namespace** to *erdemo-operator-system*.
6. Leave other options as default and click **Install** once more.
7. On the TSSC Operator page, create a new `ErDemo` CustomResource, setting the value of **mapToken** to match [your own mapbox API token](https://account.mapbox.com/access-tokens/).

## Development
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
