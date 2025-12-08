# pre-install
> [!IMPORTANT]
> This is a work in progress prototype and not ready for real-world usage, although we do welcome any feedback at this early stage of development.

## Structure
- The [`maximo-operator-catalog/operators`](maximo-operator-catalog/operators/) folder contains the base resource definitions to install the operators
- The [`maximo-operator-catalog/v9-251127-amd64`](maximo-operator-catalog/v9-251127-amd64/) folders contain overlays that ensure the correct version of the operator is used to align with the tested combination of versions that are verified by IBM.

## Usage
Do not directly use the content of [`maximo-operator-catalog/operators`](maximo-operator-catalog/operators/), instead choose a specific catalog version and use the appropriate overlay from there, for example:

- **Don't** use [`maximo-operator-catalog/operators/ibm-mas`](maximo-operator-catalog/operators/ibm-mas)
- **Do** use [`maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.0`](maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.0) or [`maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.1`](maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.1), which ensure the `9.0.17` or `9.1.6` version of the operator from that catalog update will be installed.


## Example
Refer to [`instances/dev1`](instances/dev1/) for an example showing how to use the files in this repository to pre-install the operators for a MAS 9.1 install of Core, Manage, and Visual Inspection using the November 2025 catalog update.

```bash
kustomize build instances/dev1
```

See [`instances/dev1/resources.yaml`](instances/dev1/resources.yaml) to view the result of this kustomize command.
