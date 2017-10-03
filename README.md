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
