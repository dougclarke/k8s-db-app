# K8s Deployment Example

An example Kubernetes deployment for Wordpress with MySQL, persistant volumes, Kubernetes ConfigMaps and secrets. The Wordpress instances include horizontal pod autoscaling based on CPU utilization thresholds.

## Requirements

A Kubernetes cluster and the kubectl command-line tool configured to communicate with your cluster.

## How to use

Download the repository, configure a kustomization.yaml file and apply using kubectl.

You must set a user and root password for the MySQL server in kustomization.yaml.

    $ git clone https://github.com/dougclarke/k8s-db-app.git
    $ cp kustomization-example.yaml kustomization.yaml
    $ vi kustomization.yaml
    $ kubectl apply -k ./

## Accessing the cluster

To access the cluster by hostname through the ingress controller, add the cluster IP and the hostname to your systems hosts file.

    $ sudo bash -c "echo '192.168.99.101	k8s-db-app.local' >> /etc/hosts"


## Minikube ingress validation issue

    Internal error occurred: failed calling webhook "validate.nginx.ingress.kubernetes.io"

When testing with Minikube if you receive this error, simply remove the validation check using kubectl.

    $ kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission
    validatingwebhookconfiguration.admissionregistration.k8s.io "ingress-nginx-admission" deleted 


## Bring it down

    $ kubectl delete -k ./
