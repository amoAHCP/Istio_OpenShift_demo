# Istio on OpenShift - local demo
OpenShift based Envoy local demo environment. Uses `oc cluster up`.

## Instructions
Download OpenShift client tools equal or greater than version 3.7 from https://github.com/openshift/origin/releases and place it under `/usr/bin`.

```
[rlourenc@localhost ~]$ which oc
/usr/bin/oc

[rlourenc@localhost ~]$ oc version
oc v3.7.0-alpha.1+fdbd3dc
kubernetes v1.7.0+695f48a16f
features: Basic-Auth GSSAPI Kerberos SPNEGO
```

Make sure you have a [working docker environment](https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md#linux) and run `sudo oc cluster up`. 

```
Starting OpenShift using openshift/origin:v3.7.0-alpha.1 ...             
OpenShift server started.    

The server is accessible via web console at:   
    https://127.0.0.1:8443                     

You are logged in as:                          
    User:     developer                        
    Password: <any value>                      

To login as administrator:                     
    oc login -u system:admin
```
