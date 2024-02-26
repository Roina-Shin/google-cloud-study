### [Source of this study material : Google Cloud Developer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certified-professional-cloud-developer)

## Understanding Kubernetes Network Policies

- How do you decide **which pod is allowed to communicate with which pod and what kind of communication is allowed?**


- **Network Policy** can help with that.


### Sample NetworkPolicy YAML file


```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: my-network-policy
  namespace: demo-deployment
spec:
  podSelector:
    matchLabels:
      app: myapp1
  policyTypes:
    Ingress
  ingress:
    from:
      - ipBlock:
          cidr: 10.68.0.0/14
      - namespaceSelector:
          matchLabels:
            name: demo-deployment
      - podSelector:
          matchLabels:
            app: myapp1
    ports:
      - protocol: TCP
        port: 8080
```


- Control communication between pods based on:

  - Pod selectors

  - Namespaces

  - IP Blocks


- **The NetworkPolicy YAML** says that only inbound traffic from the **10.68.0.0/14** network range with **demo-deployment** namespace as well as the pod selector labels of **app: myapp1** can talk to each other.


- You can define egress and ingress in policyTypes in the same policy:


```
apiVersionL networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
spec:
  podSelector: {}
  policyTypes:
    - Ingress
    - Egress
```


- By default, if no policies exist in a namespace, then all ingress and egress traffic is allowed to and from pods in that namespace.


