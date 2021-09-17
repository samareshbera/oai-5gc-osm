**OAI installation using Helm-Chart**

See OAI github repository [here](https://gitlab.eurecom.fr/oai/cn5g/oai-cn5g-fed/-/blob/helm-update/docs/DEPLOY_SA5G_HC.md)

Debug:
1. Check all files to have consistencies, specifically, values of `mcc` and `mnc`
2. Define the Static IP at `nr-ue` using [Calico](https://docs.projectcalico.org/networking/use-specific-ip)
3. Set `multus` to `false` in `value.yaml` file for each operator folder
4. Set all interfaces to `eth0` from `net1` (`net1` is used if `multus` is `true`)

Commands:
1. Check the Helm list: `helm list`
2. Check the kubernetes pods: `kubctl get pods -n oai` (`oai` is the namespace)
3. Check the logs of any pods: `kubectl logs -n oai -it <pod_id> -c <container_name>`
4. Go to bash of nr-ue: `kubectl exec -n oai -it <pod_id_nr_ue> -c <container_name_nr_ue> bash`
  -- Check the interfaces: `ip -br a` and `route -n` (if command not found, install package `net-tools`)
  -- Ping test directly: `ping -c4 google.com`
  -- Ping using tunnel: `ping -I oaitun_ue1 -c 4 google.com`
  -- All are successul -- you are DONE!


For multus (production grade deployment):
1. Set `multus` to `true` in `value.yaml` file for each operator file
