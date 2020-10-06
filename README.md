# openshift-karma


    $ oc create namespace openshift-karma
    
    $ oc adm policy add-cluster-role-to-user -n openshift-karma -z default cluster-monitoring-view
