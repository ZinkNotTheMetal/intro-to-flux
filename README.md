# Introduction to Flux CD

- [Website](https://fluxcd.io)

## Resources

### YouTube

- [Techno Tim](https://www.youtube.com/watch?v=PFLimPh5-wo)
- [That DevOps Guy (with Kind)](https://www.youtube.com/watch?v=X5W_706-jSY)
- [Anais](https://www.youtube.com/watch?v=X5W_706-jSY)

## Steps (for running locally)

1. Install kind
2. Install flux (cli)
3. Bootstrap flux in a repository

## Install 'kind'

Kind is available for install on all major package versions

- [Kind Quickstart](https://kind.sigs.k8s.io/docs/user/quick-start/#installing-with-a-package-manager)

## Create a kubernetes cluster w/ Kind

```sh
kind create cluster --name fluxcd-cluster --image kindest/node:v1.29.0
```

## Run a container to work in

Alpine Linux:

- Mount your local .kube directory into /root/.kube
- This will configure your kubectl config automatically

### Windows

```sh
docker run -it --rm -v C:/Users/wzink/.kube:/root/.kube -v C:/Work:/work -w /work --net host alpine:latest sh
```

### Mac

```sh
docker run -it --rm -v ~/.kube:/root/.kube -v ~/Work:/work -w /work --net host alpine:latest sh
```

### Install the following tools in the container

Note: If running into SSL errors move from https into http
command: `sed -ie "s/https/http/g" /etc/apk/repositories`

1. Install Curl

   ```sh
   apk add --no-cache curl
   ```

2. Install [kubectl](https://devcoops.com/install-kubectl-on-alpine-linux/#:~:text=Install%20Kubectl%20on%20Alpine%20Linux%201%20curl%20-LO,%2Bx%20.%2Fkubectl%204%20mv%20.%2Fkubectl%20%2Fusr%2Fbin%2Fkubectl%20Conclusion%20)

   ```sh
   curl -kLO https://storage.googleapis.com/kubernetes-release/release/$(curl -ks https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

   chmod +x ./kubectl

   mv ./kubectl /usr/bin/kubectl
   ```

### Run Kubectl command

```sh
kubectl get nodes
```

## Bootstrap Flux

There are multiple ways to start with Flux (called bootstraping)

- [Flux Bootstrap documentation](https://fluxcd.io/flux/installation/bootstrap/)

1. Git server
2. Gitea
3. GitHub
4. GitLab
5. BitBucket
6. AWS CodeCommit
7. Azure DevOps
8. Google Cloud Source

## Downloading flux command-line utility

- We get this utility from the GitHub [Flux Releases page](https://github.com/fluxcd/flux2/releases)
- As of 1/9/24 - v.2.2.2 is latest

Commands to install within our container

```sh
curl -o /tmp/flux.tar.gz -skLO https://github.com/fluxcd/flux2/releases/download/v2.2.2/flux_2.2.2_linux_amd64.tar.gz
tar -C /tmp/ -zxvf /tmp/flux.tar.gz
mv /tmp/flux /usr/local/bin/flux
chmod +x /usr/local/bin/flux
```

### Check to ensure our cluster is ok

```sh
flux check --pre
```

### Next Steps

- Go to docs/FLUX_WITH_GITHUB.md
