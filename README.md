# Knative Demo - Conf42 Kube Native 2023

This repository is part of the talk titled "Beyond Traditional DevOps: A Dive into Serverless with Kubernetes using Knative" given at [Conf42 Kube Native 2023](https://www.conf42.com/Kube_Native_2023_Karan_Jagtiani_devops_serverless_knative).

## Repository Contents

1. [hello-world.yaml](./hello-world.yaml): YAML file that creates a sample serverless application.
2. [min-scale.yaml](./min-scale.yaml): YAML file with a more verbose configuration for the sample serverless application.

## Prerequisites

1. Docker - [Link](https://docs.docker.com/engine/install/)
2. KinD - [Link](https://kind.sigs.k8s.io/)
3. Knative CLI - [Link](https://knative.dev/docs/client/install-kn/)
4. Kubectx (Optional) - [Link](https://github.com/ahmetb/kubectx#installation)
5. Hey (Optional) - [Link](https://github.com/rakyll/hey)
6. Set `k` as an alias for the `kubectl` command - If you don't want to do this, please replace `k` with `kubectl` in the commands below.
7. Clone this repository to your local system and change the directory: `cd conf42-kube-native-talk-knative-demo`.

## Demo Commands

**1. Quickly start the KinD cluster using the Knative CLI:**

```
kn quickstart kind
```

**2. Get the clusters using the KinD command to verify that the cluster was created:**

```
kind get clusters
```

**3. [OPTIONAL] Get the cluster context using `kubectx`.**

**4. Retrieve all namespaces in Kubernetes:**

```
k get namespaces
```

**5. Retrieve all resources/objects in the `knative-serving` namespace:**

```
k get all -n knative-serving
```

**6. Get the diff on the first YAML file:**

```
k diff -f hello-world.yaml
```

**7. Apply the first YAML file to create the sample serverless application:**

```
k apply -f hello-world.yaml
```

**8. Retrieve the pods in the default namespace:**

```
k get po
```

or

```
k get po --watch
```

**9. Retrieve the installed Knative services:**

```
k get ksvc
```

**10. Test the serverless application using `curl`:**

```
curl http://hello.default.127.0.0.1.sslip.io/
```

**11. [OPTIONAL] Load test the serverless application using:**

```
hey -z 10s -c 100 \
  $(kn service describe hello -o url) \
  && k get po
```

**12. Get the diff on the second YAML file:**

```
k diff -f min-scale.yaml
```

**13. Apply the second YAML file to apply the new annotations to the sample serverless application:**

```
k apply -f min-scale.yaml
```

**14. Retrieve the pods in the default namespace:**

```
k get po
```

or

```
k get po --watch
```

**15. Describe one of the pods that are running to see the configuration of the pod:**

```
k describe po <pod-name>
```

`<pod-name>` needs to be replaced with the name of one of the pods created after applying the second YAML file.

**16. [OPTIONAL] Load test the serverless application again to observe the difference in performance after the new changes, using:**

```
hey -z 10s -c 100 \
  $(kn service describe hello -o url) \
  && k get po
```

## Conclusion

Through this talk and repository, I hope you learned about creating a serverless infrastructure right within a Kubernetes setup using the Knative tool.

If you learned something new from the talk or want to show support, 🌟 star this repository!

If you wish to connect with me, chat about cloud-native concepts or anything related to tech, you can find all of my social links [here](https://karanjagtiani/links).

### Have fun serving!
