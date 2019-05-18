# Fusera Server Deployment

## Instructions

1. Edit igv-server-deployment.yaml to specify object storage locations for your ngc file and accession IDs file. 

2. Create the proxy server. This compute instance will incur charges. You can delete it when not in use with `gcloud` or in the GCP console https://console.cloud.google.com/dm/deployments.
```shell
gcloud deployment-manager deployments create test-deployment --config igv-server-deployment.yaml
```

3. Create an SSH tunnel to authenticate and encrypt your access to the data. There are 3 levels of security that prevent the proxy server from being accessed externally. SSH tunneling allows your client machine to make requests to the server. Exiting out of the SSH session will close the tunnel.
```shell
gcloud compute ssh igv-server -- -L 8080:localhost:8080
```
4. In IGV, go to `File > Open URL` and enter:
```
http://localhost:8080/<accession_id>/<sample_id>.b38.irc.v1.cram
```
