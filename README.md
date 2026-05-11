# pre-install

## Structure
- The [`catalogs/maximo-operator-catalog/operators`](catalogs/maximo-operator-catalog/operators/) folder contains the base resource definitions to install the operators
- The [`catalogs/maximo-operator-catalog/v9-251127-amd64`](catalogs/maximo-operator-catalog/v9-251127-amd64/) folders contain overlays that ensure the correct version of the operator is used to align with the tested combination of versions that are verified by IBM.


## Usage
Do not directly use the content of [`catalogs/maximo-operator-catalog/operators`](catalogs/maximo-operator-catalog/operators/), instead choose a specific catalog version and use the appropriate overlay from there, for example:

- **Don't** use [`catalogs/maximo-operator-catalog/operators/ibm-mas`](catalogs/maximo-operator-catalog/operators/ibm-mas)
- **Do** use [`catalogs/maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.0`](catalogs/maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.0) or [`catalogs/maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.1`](catalogs/maximo-operator-catalog/v9-251127-amd64/ibm-mas/9.1), which ensure the `9.0.17` or `9.1.6` version of the operator from that catalog update will be installed.


## Example
Refer to [`examples/instances/dev1`](examples/instances/dev1/) for an example showing how to use the files in this repository to pre-install the operators for a MAS 9.1 install of Core, Manage, and Visual Inspection using the November 2025 catalog update. For required dependencies refer to [`examples/dependencies`](examples/dependencies/).


```bash
kustomize build examples/instances/dev1
```

See [`examples/instances/dev1/resources.yaml`](examples/instances/dev1/resources.yaml) to view the result of this kustomize command.


## Maintenance
The content in [`catalogs/maximo-operator-catalog/operators`](catalogs/maximo-operator-catalog/operators/) will be largely static, and with the release of each new operator catalog we will publish a new overlay setting the appropriate values for each operator on all supported release channels.
