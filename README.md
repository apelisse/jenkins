# Deploy Jenkins continuous integration pipeline within a Kubernetes cluster

From within the top directory (containing Kube-manifest.yaml), run the following test:

`kinflate inflate -f .`

which will output the YAML to stdout. Check the output YAML.

In order to run jenkins within the Kubernetes cluster, pipe the output to
`kubectl apply`:

`kinflate inflate -f . | kubectl apply -f -`

which should start at least one pod.

## Check Jenkins has started

`kubectl get pods`

should show a pod named `jenkins-<random>-<more-random>`.

Now find the external IP for the Jenkins service:

`kubectl get svc`

which should show something like:

```bash
$ k get svc
NAME                TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)          AGE
jenkins-discovery   ClusterIP      10.11.241.76   <none>            50000/TCP        1h
jenkins-ui          LoadBalancer   10.11.255.24   104.197.155.226   8080:32633/TCP   1h
```

In a browser, go to the CLUSTER-IP:PORT for the jenkins-ui service:

`http://104.197.155.226:8080`

This should show the Jenkins UI.
