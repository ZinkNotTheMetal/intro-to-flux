# Flux bootstrap for Github

- [Resource](https://fluxcd.io/flux/installation/bootstrap/github/)

1. Generate a GitHub PAT
2. Use our container to store the GITHUB_TOKEN

    ```sh
    export GITHUB_TOKEN=<gh-token>
    ```

3. Setup GitHub Personal Account

    NOTE: Insert the cluster after /fluxcd/clusters/ on which cluster you want to deploy

    ```sh
    flux bootstrap github \
        --token-auth \
        --owner=zinknotthemetal \
        --repository=intro-to-flux \
        --branch=main \
        --path=fluxcd/clusters/local \
        --personal
    ```

4. Verify that flux is in place and working as expected

```sh
flux check

# flux tools installed by flux
kubectl -n flux-system get GitRepository
kubectl -n flux-system get Kustomization
```

## Installing an application through Flux CLI

We will install [Starboard](https://aquasecurity.github.io/starboard/v0.15.6/) as an example application into K8S

1. Define a namespace where this application will live

    ```sh
    kubectl create ns starboard-system
    ```

2. Tell Flux where the helm chart (starboard) lives

    ```sh
    flux create source helm starboard-operator --url https://aquasecurity.github.io/helm-charts/ --namespace starboard-system
    ```

3. Tell flux to release the helm chart

    ```sh
    flux create helmrelease starboard-operator --chart starboard-operator \
      --source HelmRepository/starboard-operator \
      --chart-version 0.10.12 \
      --namespace starboard-system
    ```

## Installing an application though Flux CLI and YAML files

1. Define a namespace where this application will live

    ```sh
    kubectl create ns starboard-system
    ```

2. Tell Flux where the helm chart (starboard) lives

   - Note: <location> will be where the git repo lives and we can put it inside a directory
   - i.e.: clusters/local/starboard-resource.yaml

    ```sh
    flux create source helm starboard-operator \
      --url https://aquasecurity.github.io/helm-charts/ \
      --namespace starboard-system \
      --export | tee <location>
    ```

3. Tell flux to release the helm chart

    ```sh
    flux create helmrelease starboard-operator \
      --chart starboard-operator \
      --source HelmRepository/starboard-operator \
      --chart-version 0.10.12 \
      --target-namespace starboard-system
      --interval 30s \
      --export | tee <location>
    ```