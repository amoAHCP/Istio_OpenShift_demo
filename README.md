# Istio on OpenShift - local demo
It uses istio-0.2.4 for demoing and blogging purposes.

## Description
This set of playbooks installs Istio on top of an existing openshift cluster. Besides the main Istio components, certain monitoring or tracing addons such as prometheus, grafana, zipkin or skydive can be installed as well by adjusting the following booleans defined in `setup_istio_local.yml`.

```
vars:
        demo_app: True
        addons: True
        skydive: True
```

Installing with every var set to True can use ~4/5Gb RAM and can take up to around ~15 minutes to finish.

## Requirements
Download OpenShift client tools equal or greater than version 3.7 from https://github.com/openshift/origin/releases and place it under `/usr/bin`.

```
$ which oc
/usr/bin/oc

$ oc version
oc v3.7.0-alpha.1+fdbd3dc
kubernetes v1.7.0+695f48a16f
features: Basic-Auth GSSAPI Kerberos SPNEGO
```

Run `sudo oc cluster up`. 
If you run into issues make sure you have a [working docker environment](https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md#linux)


## Installing
```
$ ansible-playbook setup_istio_local.yml
```

You might see something like the below even after the playbook is finished. This is because besides the [init-containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers) Envoy is deployed as a side car container called `istio-proxy` for each service component.

```
$ oc get pods                            
NAME                             READY     STATUS              RESTARTS   AGE
details-v1-2202528699-k89b3      0/2       Init:1/2            0          3m
grafana-3374311966-p4568         0/1       ContainerCreating   0          3m
istio-ca-1144596003-b80lx        1/1       Running             0          3m
istio-egress-4022046676-lc693    1/1       Running             0          3m
istio-ingress-2692470798-j8p9m   1/1       Running             0          3m
istio-mixer-971169182-1kqqg      0/2       ContainerCreating   0          3m
istio-pilot-953936588-q61p8      1/1       Running             0          3m
productpage-v1-849198989-3jxcj   0/2       Init:1/2            0          3m
prometheus-4086688911-dnl7t      1/1       Running             0          3m
ratings-v1-217391091-djq0d       0/2       Init:1/2            0          3m
reviews-v1-3397570414-0ljtn      0/2       Init:1/2            0          3m
reviews-v2-755907806-406vn       0/2       Init:1/2            0          3m
reviews-v3-1808066742-j54t2      0/2       Init:1/2            0          3m
servicegraph-3304329788-kmbj4    1/1       Running             0          3m
skydive-agent-kx7n3              0/1       ContainerCreating   0          3m
skydive-analyzer-1-deploy        0/1       ContainerCreating   0          3m
zipkin-3660596538-1gckb          1/1       Running             0          3m

```

Example:

$ oc logs productpage-v1-849198989-3jxcj -c istio-proxy 
Error from server (BadRequest): container "istio-proxy" in pod "productpage-v1-849198989-3jxcj" is waiting to start: PodInitializing

$ oc logs productpage-v1-849198989-3jxcj 
Error from server (BadRequest): a container name must be specified for pod productpage-v1-849198989-3jxcj, choose one of: [productpage istio-proxy] or one of the init containers: [istio-init enable-core-dump]

