# Traefik Ingress Controller

## Main Goal

This repository is intead to help deploying Traefik 2 <https://traefik.io/> as an Ingress Controller for Kubernetes.

See more on what is an Ingress controller following this link <https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/>

## Installation

To deploy Traefik here is an all-in-one command (dev mode)

```bash
kubectl create ns traefik
curl https://raw.githubusercontent.com/xavierbaude/Traefik-Ingress-Controller/master/files/traefik-ig.yaml | kubectl apply -f - -n traefik
```

For production usage, you have to store TLS certificate to an external place such a PVC

```bash
kubectl create ns traefik
curl https://raw.githubusercontent.com/xavierbaude/Traefik-Ingress-Controller/master/files/traefik-ig-pvc.yaml | kubectl apply -f - -n traefik
```

Note : to make TLS working, change the default email, if not you will get "Unable to obtain ACME certificate" error message...

## Usage

This setup enable both Ingress & IngressRoute object. Main advantage of IngressRoute is the certificate Management.
You can find some examples in the directory "examples".

You can access to traefik dasboard with a private loadbalancer.

With this deploiement, the tlsChallenge is enabled and the name of the certResolver is "sample".
Get more information here: <https://docs.traefik.io/https/acme/>

Prometheus export is also enable for metrics.

Finally accesslog are enabled, you can get it from the stdout of the traefik pod.

Enjoy.

## Next step

You should now redirect traffik to your ingress, so simply create a dns wildcard entry which point to the IP of the Loadbalancer.

ex:
```bash
*.foo.bar -> 1.1.1.1
```
