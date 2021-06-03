# karma


    $ oc create namespace karma
    
    $ oc create sa karma -n karma
    
    $ oc adm policy add-cluster-role-to-user -n karma -z karma cluster-monitoring-view
    
    $ oc create secret generic karma --from-file=karma.yaml -n karma
  
  ## Creating App
  
  +Add --> Conatiner Image
  
  - Image: lmierzwa/karma:latest
  - Name: karma
  - Route: Secured, Edge, Redirect
  
  
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
         
         
         
 
          
