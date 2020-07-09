# Propagating Updates

This chapter depicts important information about updating an existing WSO2 product deployment in a container platform.

## Contents

The following will be discussed in detail in the document.

* [When do we need to update?](#when-do-we-need-to-update?)
* [Simplest way to perform an update](#simplest-way-to-perform-an-update)
* [Achieve zero downtime](#achieve-zero-downtime)

### When do we need to update?

The following are some of the scenarios which instigates the need for an update to an existing
WSO2 product deployment in a container platform.

* Be abreast with product bug fixes and improvements by integrating [WSO2 Updates](https://wso2.com/updates)

* Updates to configuration files

* Updates to non-configuration resources

  For example,
    * Binaries such as, third-party libraries, Carbon extensions in the form of OSGi bundles, [Carbon Applications](https://docs.wso2.com/display/Carbon440/Working+with+Carbon+Applications)
    * Any security related artifacts such as, Java Keystore files

* Changes to installation resources

  For example,
    * Container image source
    * Kubernetes/Helm resources

### Simplest way to perform an update

We recommend the use of [official WSO2 product Helm Charts](https://hub.helm.sh/charts/wso2) for production grade WSO2 product deployments
in Kubernetes environments.

Hence, the simplest way to perform an update to an existing WSO2 product deployment is to use a [Helm based upgrade](https://helm.sh/docs/helm/helm_upgrade/).

1. Perform the required change(s).

   The following are some of the probable changes.
   
   * An update of [Helm Values](https://helm.sh/docs/chart_template_guide/values_files/) (e.g. update to the container
     image tag)
   * An update to configuration file(s)
   
2. Perform a Helm based upgrade.

   Kubernetes resources for WSO2 products utilize the most appropriate update strategy for the given scenario, depending on the involved WSO2 product profile.

**Note:**
> If you are not using Helm package manager to deploy WSO2 product Kubernetes resources, you may have to perform the
  update via Kubernetes client commands.
>
> For example in order to apply a configuration file change,
> - Recreate the existing ConfigMap corresponding to the changed file.
> - Perform a rollout to the [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment) /
    [StatefulSet](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/#rolling-update).

### Achieve zero downtime

The most popular update strategy utilized by WSO2 product Kubernetes resources is of type,
[rolling update](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/). Both resource types,
Deployment and [StatefulSet](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/#rolling-update)
primarily adopt this strategy.

The combined action of following factors ensure that a WSO2 product deployment maintains zero downtime during an update.

   * Rolling update strategy
   * High availability support for a given WSO2 product profile
