# Fusera Server Deployment

## Instructions

1. Edit igv-server-template.jinja to specify object storage locations for your ngc file and accession IDs file. 

2. Create the server that acts as a proxy:
```shell
gcloud deployment-manager deployments create test-deployment --config igv-server-deployment.yaml
```

3. Create an SSH tunnel to authenticate and encrypt your access to the data:
```shell
gcloud compute ssh igv-server -- -L 8080:localhost:8080
```
4. In IGV, go to `File > Open URL` and enter:
```
http://localhost:8080/<accession_id>/<sample_id>.b38.irc.v1.cram
```
