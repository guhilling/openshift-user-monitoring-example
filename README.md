# openshift-user-monitoring-example

Before adding the resources enable user workload monitoring by configuring cluster-monitoring-config. This will depend on your version. So it's probably best to check the docs:

* 4.9: https://docs.openshift.com/container-platform/4.9/monitoring/enabling-monitoring-for-user-defined-projects.html
* 4.5: https://docs.openshift.com/container-platform/4.5/monitoring/monitoring-your-own-services.html#enabling-monitoring-of-your-own-services_monitoring-your-own-services

## Create the demo project

```oc apply -f example-app-all.yaml```

This will create a namespace, deployment and service. The deployment will create 2 pods to be monitored.
If you want to access the metrics manually you need to expose the service as a route or ingress. 

Metrics are available at the ```metrics``` context.

## Create the service monitor

```oc apply -f example-app-service-monitor.yaml```

You should be able to see the values in the _openshift_ prometheus view.

## Create the alerting rule

```oc apply -f example-app-alerting-rule.yaml```

The alert will start to fire right away. It will be visible in the default alertmanager-ui but _not_ in the alert overview.

You can also see it in the Thanos-Ruler UI. The corresponding route is available in the ```user-workload-monitoring``` namespace.