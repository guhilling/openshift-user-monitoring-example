# openshift-user-monitoring-example

Before adding the resources enable user workload monitoring by configuring cluster-monitoring-config. This will depend on your version. So it's probably best to check the docs:

* 4.9: https://docs.openshift.com/container-platform/4.9/monitoring/enabling-monitoring-for-user-defined-projects.html
* 4.6: https://docs.openshift.com/container-platform/4.6/monitoring/enabling-monitoring-for-user-defined-projects.html

## Create the demo project

```oc apply -k .```

This will create a deployment, service, servicemonitor and prometheusrule. The deployment will create 2 pods to be monitored.
If you want to access the metrics manually you need to expose the service as a route or ingress. 

Metrics are available at the ```metrics``` context.

## Use the service monitor

You should be able to see the values in the _openshift_ prometheus view. It is actually _collected_ by the user-monitoring prometheus.

## Test the alerting rule

The alert will start to fire right away. It will be visible in the default alertmanager-ui as well as the alert overview _but_ you need to manually remove the default filter on the alerts to ```Source==Platform```.

You can also see it in the Thanos-Ruler UI.
