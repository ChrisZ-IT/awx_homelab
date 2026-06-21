# awx_homelab
My homelab k8s deployment of awx

My quick notes on how I deployed this(and some troubleshooting steps I had to do). I plan to come back later and clean this up a bit. This deployment uses istio ingress gateway. I deployed istio ingress gateway in my cluster to learn how to use it. This was the deployment I used to learn how to use istio.

1. Modify `storage.yml` with your storage class and persistent volume (This is setup to use nfs off my synology) and apply

2. Install the awx operator helm chart
    https://github.com/ansible-community/awx-operator-helm

    - `helm install awx awx-operator/awx-operator --namespace awx --create-namespace -f values.yml` (modify your `values.yml`)

3. If helm does not deploy the the awx resource
    - Give it 5-10 minute then run `kubectl get awx -n awx` if get back `no resources found`
        - You should at least get the `controller-manager` pod so look at its logs for any errors
        - if its just sitting at stuff like `"msg":"Starting workers","controller":"awxmeshingress-controller"` the manager is waiting for the awx resource to send signal to start. Follow the next 2 steps to kick it a little
    - Find broken api services `kubectl get apiservice | grep -E "False|Unknown"`
        - Resolve any issues you find/delete them(I assume you know what you are doing here)
    - If helm does not deploy the awx resource you can modify and apply `awx.yml`
4. Modify `service.yml` with your FQDN and apply once the `ansible-awx-service` is up and it has endpoints attached to it
