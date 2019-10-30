# aws-nlb-with-nginx-ingress-kubernetes

## Usage

1. Create secrets

``` bash
$ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=mydomain.com/O=mydomain.com"

$ kubectl create secret tls tls-secret --key tls.key --cert tls.crt
```

2. Apply kube manifests

``` bash
$ kubectl apply -f 01-mandatory-ngnix-obj.yaml

$ kubectl apply -f 02-aws-nlb-service.yaml

$ kubectl apply -f 03-app-blue-svc.yaml

$ kubectl apply -f 04-app-red-scv.yaml

$ kubectl apply -f 05-nginx-ingress.yaml

```

3. Configure A Record in AWS Route53 with the DNS value of NLB

4. Test with the URLs 'http://subdomain.mydomain.com/bluesvc', 'http://subdomain.mydomain.com/redsvc'

