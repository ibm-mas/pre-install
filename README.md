# pre-install

## Overview
This repository contains Kubernetes resource definitions and kustomize configurations for pre-installing IBM Maximo Application Suite (MAS) RBAC.

## Directory Structure

### Catalogs

#### [`catalogs/maximo-operator-catalog/`](catalogs/maximo-operator-catalog/)
Contains IBM Maximo operators organized into:

- **[`operators/`](catalogs/maximo-operator-catalog/operators/)** - Base resource definitions for all operators including:
  - **Core MAS**: [`ibm-mas/`](catalogs/maximo-operator-catalog/operators/ibm-mas/) - Core MAS operator
  - **Applications**:
    - [`ibm-mas-manage/`](catalogs/maximo-operator-catalog/operators/ibm-mas-manage/) - Manage
    - [`ibm-mas-monitor/`](catalogs/maximo-operator-catalog/operators/ibm-mas-monitor/) - Monitor
    - [`ibm-mas-predict/`](catalogs/maximo-operator-catalog/operators/ibm-mas-predict/) - Predict
    - [`ibm-mas-visualinspection/`](catalogs/maximo-operator-catalog/operators/ibm-mas-visualinspection/) - Visual Inspection
    - [`ibm-mas-optimizer/`](catalogs/maximo-operator-catalog/operators/ibm-mas-optimizer/) - Optimizer
    - [`ibm-mas-iot/`](catalogs/maximo-operator-catalog/operators/ibm-mas-iot/) - IoT
    - [`ibm-mas-facilities/`](catalogs/maximo-operator-catalog/operators/ibm-mas-facilities/) - Facilities
    - [`ibm-mas-arcgis/`](catalogs/maximo-operator-catalog/operators/ibm-mas-arcgis/) - ArcGIS
  - **Services**:
    - [`ibm-aiservice/`](catalogs/maximo-operator-catalog/operators/ibm-aiservice/) - AI Service
    - [`ibm-sls/`](catalogs/maximo-operator-catalog/operators/ibm-sls/) - Suite License Service
    - [`ibm-truststore-mgr/`](catalogs/maximo-operator-catalog/operators/ibm-truststore-mgr/) - Truststore Manager
  - **Dependencies**:
    - [`ibm-operator-catalog/`](catalogs/maximo-operator-catalog/operators/ibm-operator-catalog/) - IBM Operator Catalog
    - [`db2u/`](catalogs/maximo-operator-catalog/operators/db2u/) - Db2 Universal
    - [`eclipse-amlen/`](catalogs/maximo-operator-catalog/operators/eclipse-amlen/) - Eclipse Amlen

#### [`catalogs/redhat-certified-operator-catalog/`](catalogs/redhat-certified-operator-catalog/)
Red Hat certified operators:
- [`operators/ibm-data-reporter/`](catalogs/redhat-certified-operator-catalog/operators/ibm-data-reporter/) - IBM Data Reporter
- [`operators/ibm-metrics/`](catalogs/redhat-certified-operator-catalog/operators/ibm-metrics/) - IBM Metrics

#### [`catalogs/redhat-operator-catalog/`](catalogs/redhat-operator-catalog/)
Red Hat platform operators:
- [`operators/openshift-cert-manager-operator/`](catalogs/redhat-operator-catalog/operators/openshift-cert-manager-operator/) - OpenShift Cert Manager

### OpenShift Platform
- **[`openshift-platform/`](openshift-platform/)** - Platform-level configurations

## RBAC Configurations

Each operator includes comprehensive RBAC (Role-Based Access Control) configurations in their respective `rbac/` subdirectories. These configurations provide fine-grained access control for MAS operators and applications.

### RBAC Structure

Each operator's RBAC directory contains:

**Version-Specific Roles** (Currently for MAS 9.2):
   - **ClusterRole**: Cluster-wide permissions for core MAS services
   - **Role (Non-Essential)**: Namespace-scoped permissions for application-specific operations

### RBAC Types

#### ClusterRole (Cluster-wide permissions)
Located in `rbac/9.2/cluster-role-*.yml` files, these define cluster-wide permissions for MAS components.


#### Role (Namespace-scoped, Non-Essential)
Located in `rbac/9.2/role-non-essential-*.yaml` files, these define namespace-specific permissions.

### Using RBAC Configurations

RBAC configurations are modular and can be applied independently or as part of a complete deployment:

```bash
# Apply RBAC for a specific operator
kustomize build catalogs/maximo-operator-catalog/operators/ibm-mas/rbac/9.2 | oc apply -f -

# Apply RBAC for an application
kustomize build catalogs/maximo-operator-catalog/operators/ibm-mas-manage/rbac/9.2 | oc apply -f -
```

**Note**: RBAC files use template variables (e.g., `{{ mas_instance_id }}`) that must be replaced with actual values before applying.

 **💡 Note**: If you don't want to manually apply RBAC configurations for each operator/application using kustomize, you can use the **MAS CLI pre-install command** to apply RBACs for all applications at once. For more information about this command, refer to the [Pre install documentation](github.com/ibm-mas/cli/blob/master/docs/commands/pre-install.md).

## Maintenance

The content in [`catalogs/maximo-operator-catalog/operators`](catalogs/maximo-operator-catalog/operators/) contains base resource definitions (namespace, operatorgroup, subscription, RBAC) that remain largely static. RBAC configurations are versioned to support different MAS releases and will be updated as new minor versions are released.