Table of Contents
=================

   * [Requirement](#requirement)
   * [Practice](#practice)
      * [Use label selectors to schedule Pods.](#use-label-selectors-to-schedule-pods)
      * [Understand the role of DaemonSets](#understand-the-role-of-daemonsets)

# Requirement

5% - Scheduling
```
• Use label selectors to schedule Pods.
• Understand the role of DaemonSets.
• Understand how resource limits can affect Pod scheduling.
• Understand how to run multiple schedulers and how to configure Pods to use them.
• Manually schedule a pod without a scheduler.
• Display scheduler events.
• Know how to configure the Kubernetes scheduler.
```

# Practice

Here we assume you already have a running k8s cluster.

(If you don't have, you can check [challenges-kubernetes](https://github.com/DennyZhang/challenges-kubernetes) repo. And finish [Scenario-101](https://github.com/DennyZhang/challenges-kubernetes/tree/master/Scenario-101))

## Use label selectors to schedule Pods.

- Get pods by selectors
```
Denny-Laptop:Scenario-101 DennyZhang$ kubectl get pods -l app="nginx"
NAME                                READY     STATUS    RESTARTS   AGE
nginx-deployment-6d8f46cfb7-csjkc   1/1       Running   3          3m
nginx-deployment-6d8f46cfb7-pfjt4   1/1       Running   3          3m
```

- Check pod setting
```
Denny-Laptop:Scenario-101 DennyZhang$ kubectl describe pod nginx-deployment-6d8f46cfb7-csjkc | grep -iE "(label|selector)"
Labels:         app=nginx
Node-Selectors:  <none>
```

- Scale pods by label selectors
```
Denny-Laptop:Scenario-101 DennyZhang$ kubectl scale --replicas=3 deployment/nginx-deployment
deployment "nginx-deployment" scaled

Denny-Laptop:Scenario-101 DennyZhang$ kubectl get pods -l app="nginx"
NAME                                READY     STATUS    RESTARTS   AGE
nginx-deployment-6d8f46cfb7-csjkc   1/1       Running   7          9m
nginx-deployment-6d8f46cfb7-pfjt4   1/1       Running   7          9m
nginx-deployment-6d8f46cfb7-zhs96   1/1       Running   0          22s
```

TODO: What's the difference in between the concepts of labels and selectors?

## Understand the role of DaemonSets
