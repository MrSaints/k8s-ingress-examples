# k8s-ingress-examples

Examples / comparisons of various routing strategies in different Kubernetes "Ingress" controllers.

Ingress in this context, entails the routing (Layer 7) of external traffic (typically HTTP) into an internal service. The officially supported controllers are [GCE](https://github.com/kubernetes/ingress-gce/blob/master/README.md), and [Nginx](https://github.com/kubernetes/ingress-nginx/blob/master/README.md).

**Contributions welcomed.**

## Rationale

I have been using Kubernetes extensively at [Arachnys](https://www.arachnys.com/), and at [Courtsite](https://www.courtsite.my/). In the latter, we switched from Linkerd to Istio as the former felt slightly harder to configure, and to employ various routing strategies. To be fair, the former specialises in being a service mesh, not necessarily an "Ingress", and they can be used together. We had no prior experience in either solution, and we found it difficult to get documentation / working examples on routing in Kubernetes.

Thus, I decided to curate "Ingress" configurations (hopefully idiomatic) for different controllers for comparison, and educational purposes; and to determine what is, and what is not currently possible.

I mention "Ingress" in quotes because I want to distinguish the concept of routing configuration from Kubernetes' first-class Ingress resource. Several controllers introduces their own routing configuration through Custom Resource Definition (CRD), while others rely on Kubernetes' metadata, and annotations.

## Testing

I tested the various installations using [Kubernetes on DigitalOcean](https://cloud.digitalocean.com/) (not sponsored, but it was surprisingly fast, and easy).

Within each controller's directory, there are instructions on how you can get them quickly set-up. That is, assuming you are using "Kubernetes-as-a-Service" with RBAC enabled by default.

## Strategies

**Basic:**

We want to route traffic by hostname, and by path.

**Traffic shifting by weight:**

We want to "gradually roll out" our services to reduce the risk of our changes being exposed to everyone.
Thus, we want to gradually shift traffic from one version of a service to another by weight. e.g. 90% of traffic goes to production, 10% of traffic goes to staging.

**Traffic shifting by header:**

We want to test changes to a specific service in a production environment, but we do not want every user to experience the changes just yet.
Thus, we want to use a custom header value to shift traffic from one version of a service to another. e.g. Production frontend (SPA), staging backend.
