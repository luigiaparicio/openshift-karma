# openshift-karma


    $ oc create namespace openshift-karma
    
    $ oc adm policy add-cluster-role-to-user -n openshift-karma -z default cluster-monitoring-view
    
    $ oc create secret generic karma --from-file=karma.yaml -n openshift-karma
    
  ## Editing Deployment
      
      ...
      spec:
      volumes:
        - name: karma-config
          secret:
            secretName: karma
            defaultMode: 420
      containers:
        - resources: {}
          terminationMessagePath: /dev/termination-log
          name: karma-alerts
          env:
            - name: CONFIG_FILE
              value: /config/karma.yaml
          ports:
            - containerPort: 8080
              protocol: TCP
          imagePullPolicy: Always
          volumeMounts:
            - name: karma-config
              readOnly: true
              mountPath: /config
          terminationMessagePolicy: File
      ...    
         
         
         
 
          
