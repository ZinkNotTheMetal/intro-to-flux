# Flux bootstrap for Github

- [Resource](https://fluxcd.io/flux/installation/bootstrap/github/)

1. Generate a GitHub PAT
2. Use our container to store the GITHUB_TOKEN
    ```sh
    export GITHUB_TOKEN=<gh-token>
    ```

3. Setup GitHub Personal Account
    ```sh
    flux bootstrap github \
        --token-auth \
        --owner=zinknotthemetal \
        --repository=intro-to-flux \
        --branch=main \
        --path=fluxcd/clusters \
        --personal
    ```