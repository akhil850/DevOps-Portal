k8s - kOps


![ea449b487335eb502ae2045b13734e63.png](./_resources/b1bf9f7d8c4e430dacbcfd40a2cfeb75.png)

> **kOps is Kubernetes Operations.**

kOps is the easiest way to get a production grade Kubernetes cluster up and running. We like to think of it as kubectl for clusters.

kOps helps you create, destroy, upgrade and maintain production-grade, highly available, Kubernetes clusters from the command line. AWS (Amazon Web Services) is currently officially supported, with GCE and OpenStack in beta support

kOps CLI : https://kops.sigs.k8s.io/cli/kops/

<br>

### Running a demo deplyment
* * *

>Step 1 : Setup AWS CLI

> Step 2 : Create an S3 bucket to save the state file.
aws s3 mb s3://k8s-kops-akhbucket1 --region ap-south-1

>Step 3 : Save KOPS_STATE_STORE as env variable for easy cli operations
```
export KOPS_STATE_STORE="s3://k8s-kops-akhbucket1"
-- optional --
export MASTER_SIZE="t2.micro"
export NODE_SIZE="t2.micro"
export ZONES="ap-south-1a"
```

> Step 4 : create a cluster.
```
kops create cluster \
--name=justme.k8s.local \
--state=s3://k8s-kops-akhbucket1 \
--master-size t2.medium \
--master-volume-size 10 \
--master-count 1 \
--master-zones ap-south-1a \
--node-size t2.medium \
--node-volume-size 10 \
--node-count 2 \
--zones ap-south-1a \
--yes
```

![bd59b46345ab0323cdf835ec12132b60.png](./_resources/da1cacaab98b4cbe8e9dde4edf9b963d.png)
![e81602b655926c48f539ec92424745ff.png](./_resources/9ed4aaf5ae6f499bb3890aee5bdadfac.png)

<br>

### Deploying Nginx with LoadBalancing
***

>     kubectl create deploy demo-nginx --image=nginx -–replicas=2 --port=80

>     kubectl expose deployment demo-nginx --type=LoadBalancer

**Check Service :** 

![7491fb7cf64885cfa8e2d9ef6d55657c.png](./_resources/8a729f26edc44bb7aef5018a283feb2a.png)


**Access ELB as :** 

![f59b6ac605f88f6f8b5384b26fa0bbb2.png](./_resources/4aa568fc92c744fba82b4f726ffbdb9f.png)

* * *
* * *