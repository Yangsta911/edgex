# edgex
## how to run edgex natively
1）Run the following export flags
   ```
   export EDGEX_SECURITY_SECRET_STORE=false
   export EDGEX_CONFIG_PROVIDER=none
   export EDGEX_USE_REGISTRY=false
   export RETENTION_ENABLED=true
   export RETENTION_INTERVAL=1h (change base on amount of memory)
   export RETENTION_MAXCAP=150
   export RETENTION_MINCAP=5
   ```
3) Download the /res folder from this repository and edit the ip addresses to the actual ip address of device used.
4) Run the following commands to start up all of the individual services required.
    ```
    nohup core-metadata -cf=core-metadata-configuration.yaml > core-metadata.log 2>&1 &
    nohup core-data -cf=core-data-configuration.yaml  > core-data.log 2>&1 &
    nohup core-command -cf=core-command-configuration.yaml > core-command.log 2>&1 &
    nohup support-notifications -cf=support-notifications-configuration.yaml > support-notif.log 2>&1 &
    nohup support-scheduler -cf=support-scheduler-configuration.yaml  > support-scheduler.log 2>&1 &
    nohup app-service-configurable  -p=rules-engine > app-service-configurable.log 2>&1 &
    ```
5) Read the logs and use the edgex api to test that server is indeed running with following command.
   ```
   curl --location --globoff 'http://192.168.1.100:59880/api/v3/ping?=null' \
   --header 'Content-Type: application/json'
   ```
