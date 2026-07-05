## Problem
- Kubenetes hosts an Nginx deployment with load balancer but the Nginx deployment is not shpwing up (the Nginx welcome page is not showing up)
- `manifest.yml` is the pod config

## Cause
- Main cause : the pod is not assigned any node to run. `kubectl get nodes` returns 2 nodes , 1 available.
  1. Ready node is not assigned a label that matches any values in `nodeSelector` of the pod (in `manifest.yml`)
  2. Ready node does not have sufficient memory for the pod config

## Fix:
  1. label node `kubectl label nodes node1 disk=ssd`
  2. apply to the config `kubectl apply -f manifest.yml` -> k8s looks at the config and compare against whatever is running on the cluster and update of there are any changes
  3. update the config using `vim` to reduce the memory needed to run the pod 

## Verify
- Run `curl 10.43.216.196` returns the default Nginx Welcome page.
