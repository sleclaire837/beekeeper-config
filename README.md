# Beekeeper Configuration

Beekeeper Configuration is used to group configuration (.yaml) files describing:
* Bee cluster setup in Kubernetes
* checks (integration tests), and
* simulations

Beekeeper Configuration .yaml files have several main blocks:
* **clusters** - defines clusters Beekeeper works with
* **node-groups** - defines Bee node groups that are part of the cluster. Node group is a collection of Bee nodes sharing same configuration parameters.
* **bee-configs** - defines Bee configuration that can be assigned to node-groups
* **checks** - defines checks Beekeeper can execute against the cluster
* **simulations** - defines simulations Beekeeper can execute against the cluster
* **stages** - defines stages for dynamic execution of checks and simulations

### Inheritance

Inheritance can be set through the field *_inherit*.

Clusters, node-groups and bee-configs blocks support inheritance. 

example:
```
bee-configs:
  light-node:
    _inherit: default
    full-node: false
```
This setting means that *light-node* bee-config will inherit all parameters from the *default* bee-config, overriding only *full-node* parameter.

### Action types

Action types can be set in every check or simulation definition.

Action types allow defining same check or simulation with different parameters.

example:
```
checks:
  pushsync-chunks:
    options:
      chunks-per-node: 1
      metrics-enabled:
      mode: chunks
      postage-amount: 1000
      postage-depth: 16
      postage-wait: 5s
      retries: 5
      retry-delay: 1s
      upload-node-count: 1
    timeout: 5m
    type: pushsync
  pushsync-light-chunks:
    options:
      chunks-per-node: 1
      metrics-enabled:
      mode: light-chunks
      postage-amount: 1000
      postage-depth: 16
      postage-wait: 5s
      retries: 5
      retry-delay: 1s
      upload-node-count: 1
    timeout: 5m
    type: pushsync
```
This setting means that pushsync check can be executed choosing *pushsync-chunks* or *pushsync-light-chunks* variation.
