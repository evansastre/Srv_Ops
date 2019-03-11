# Kubernetes

{% embed url="https://www.zhihu.com/topic/20054173/hot" %}



![](../../.gitbook/assets/image%20%282%29.png)

![](../../.gitbook/assets/image%20%286%29.png)

![](../../.gitbook/assets/image%20%284%29.png)

Use kubernetes  deploy nginx

```text
kubectl apply -f ./nginx.yaml
```

{% code-tabs %}
{% code-tabs-item title="nginx.yaml" %}
```text
apiVersion: apps/v1
 kind: Deployment
 metadata:
   name: nginx
 spec:
   replicas: 3
   selector:
     matchLabels:
       app-name: my-nginx
   template:
     metadata:
       labels:
         app-name: my-nginx
     spec:
       containers:
         - name: nginx
           image: nginx
 ---
 apiVersion: v1
 kind: Service
 metadata:
   name: nginx
 spec:
   selector:
     app-name: my-nginx
   type: ClusterIP
   ports:
     - name: http
       port: 80
       protocol: TCP
       targetPort: 80

```
{% endcode-tabs-item %}
{% endcode-tabs %}



Operators

[https://github.com/operator-framework/awesome-operators](https://github.com/operator-framework/awesome-operators)

