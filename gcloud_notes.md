`gcloud beta container --project "k8s-in-action-270211" clusters create "kubia" --zone "us-central1-c" --no-enable-basic-auth --cluster-version "1.14.10-gke.17" --machine-type "n1-standard-1" --image-type "COS" --disk-type "pd-standard" --disk-size "100" --metadata disable-legacy-endpoints=true --scopes "https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --num-nodes "3" --enable-stackdriver-kubernetes --enable-ip-alias --network "projects/k8s-in-action-270211/global/networks/default" --subnetwork "projects/k8s-in-action-270211/regions/us-central1/subnetworks/default" --default-max-pods-per-node "110" --addons HorizontalPodAutoscaling,HttpLoadBalancing --enable-autoupgrade --enable-autorepair`



`gcloud container --project "k8s-in-action-270211" clusters create "kubia" --zone "us-central1-c" --machine-type "n1-standard-1"`

`gcloud container --project "pair-monitor" clusters create "pair-monitor-backend-dev" --zone "us-central1-c" --machine-type "n1-standard-1"`


if error is auth failure then

`gcloud container clusters get-credentials kubia`


sample yaml file
```yaml
apiVersion: v1
kind: Pod
metadata:
name: kubia-manual
spec:
containers:
- image: luksa/kubia
name: kubia
ports:
- containerPort: 8080
protocol: TCP
```
`kubectl create -f kubia-manual.yaml`


pair-monitor service account key ffb1edb5f56af3a6c22a9c8299b00ac85f241f7e


https://humanitec.com/blog/how-to-set-up-a-kubernetes-cluster-on-gcp

Pod manifest
------
```yaml
apiVersion: v1
kind: Pod
metadata:
	name: kubia-manual
labels:
	creation_method: manual
	env: prod
spec:
	containers:
		- image: luksa/kubia
	      name: kubia
		  ports:
			- containerPort: 8080
			  protocol: TCP
		  livenessProbe:
			httpGet:
				path: /
				port: 8080
```

```bash
k config set-context $(k config current-context) --namespace custom-namespace
```