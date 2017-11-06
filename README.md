# Istio on OpenShift / Kubernetes - local demo environment.


## Description
This set of playbooks installs Istio on top of an existing openshift cluster. Besides the main Istio components, certain monitoring or tracing addons such as prometheus, grafana, zipkin or skydive can be installed as well by adjusting the following booleans defined in `setup_istio_local.yml`.

```
vars:
        bookinfo_demo: True
        hola_demo: True
        addons: False
        skydive: False
```

## Requirements

Packages `git` and `maven` (for java based demo)

Download OpenShift client tools equal or greater than version 3.7 from https://github.com/openshift/origin/releases and place it in your `$PATH`

```
$ which oc
/usr/bin/oc

$ oc version
oc v3.7.0-alpha.1+fdbd3dc
kubernetes v1.7.0+695f48a16f
features: Basic-Auth GSSAPI Kerberos SPNEGO
```

Run `oc cluster up --skip-registry-check=true`

If you run into issues make sure you have a [working docker environment](https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md#linux)

Most common issues should be solved by
 * installing libselinux-python, if Fedora based.
 * creating a group called `docker`, adding your user to this group and restarting docker (or rebooting your host on some cases)
 * Adding `--insecure-registry 172.30.0.0/16` to the docker daemon startup options



## Installing
```
$ ansible-playbook setup_istio_local.yml
```
