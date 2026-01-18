# awx_homelab
My homelab k8s deployment of awx

My quick notes on how I deployed this. I plan to come back later and clean this up a bit. This deployment uses istio ingress gateway. I deployed istio ingress gateway in my cluster to learn how to use it. This was the deployment I used to learn how to use istio.

1. Install the awx operator helm chart
    https://github.com/ansible-community/awx-operator-helm
    
2. Modify `service.yml` with your FQDN

3. Modify `storage.yml` with where you want your pv to be stored (`/opt/persistant_volumes/` is an NFS share off my nas I have mouted on each node in my cluster)

4. Deploy the resources `k apply -f .`
