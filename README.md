# k8s-ocis

A collection of kubectl yaml files to deploy ocis onto kubernetes. Customisation is provided via kustomize. Official helm still beta.

# Requirements

- Kustomize
- Kubernetes Cluster (I'd recommend RKE2 from Rancher)

These are not necessary but useful if you want to store your data outside the cluster.

- TrueNAS
- Democratic-csi (For auto creating NFS/ISCSI shares on TrueNAS)

## Kustomize

Pretty simple to install. It does come with kubectl but if you want the latest one you can use docker.

`docker pull k8s.gcr.io/kustomize/kustomize:v3.8.7`

Then running a command via it:

`docker run k8s.gcr.io/kustomize/kustomize:v3.8.7 version`

# Install/Deployment

Copy the example overlays folder so you can customise to your liking. I have provided examples of changing the most common things,
but you can change most parts via kustomize.

Example Values:

**OCIS_OIDC_ISSUER**:

`https://keycloak_url/realms/home`

## Via kubectl

Build the templates to see what they look like without applying.

`kubectl kustomize overlays/custom`

Deploy to the cluster.

`kubectl apply -k overlays/custom`

## Via docker kustomize

Build the templates to see what they look like without applying.

`docker run -v  absolute_path_to_checkout:/k8s k8s.gcr.io/kustomize/kustomize:v3.8.7 build /k8s/overlays/custom`

Deploy to the cluster.

`docker run -v  absolute_path_to_checkout:/k8s k8s.gcr.io/kustomize/kustomize:v3.8.7 build /k8s/overlays/custom  | kubectl apply -f -`

More info: [Kustomize](https://github.com/kubernetes-sigs/kustomize)

