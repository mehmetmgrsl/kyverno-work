### Why Kyverno?

Kyverno allows cluster administrators to manage environment specific configurations independently of workload configurations and enforce configuration best practices for their clusters

### Example Use Cases
1. Ensure that your cluster has a rule mandating the inclusion of a specific label whenever a POD is created.
2. Ensure that your cluster has a rule mandating the inclusion of resource quota limits whenever a POD is created.

### Precondition
- K8S Cluster(s)

### Installation
```kubectl create -f https://github.com/kyverno/kyverno/releases/download/v1.10.0/install.yaml```

### Apply Policies
1. ```kubectl apply -f require-pod-labels.yml```
2. ```kubectl apply -f require-pod-requests-limits.yml```

### Test
1. ```kubectl run nginx-1 --image=nginx```

You will receive the error below:

```
Error from server: admission webhook "validate.kyverno.svc-fail" denied the request: 

resource Pod/default/nginx-1 was blocked due to the following policies 

require-labels:
  check-for-labels: 'validation error: The label `team` is required. rule check-for-labels
    failed at path /metadata/labels/team/'
require-requests-limits:
  validate-resources: 'validation error: CPU and memory resource requests and limits
    are required. rule validate-resources failed at path /spec/containers/0/resources/limits/'
```

2. ```kubectl apply -f example-pod.yml``` 

This will work: ```pod/nginx-2 created```


### Resources
1. https://kyverno.io/
2. https://kyverno.io/policies/
3. https://github.com/kyverno/policies/tree/main/best-practices/require-pod-requests-limits
3. [Enforce Kubernetes Security with Kyverno - Abhishek Veeramalla](https://www.youtube.com/watch?v=5ihkMblumD0)