# GitHub Actions Docker

A collection of Docker related GitHub actions.

## Actions

### Build and Push

Build and push a docker image using a Dockerfile.

#### Example

```yaml
  - uses: aboutbits/github-actions-docker/build-push@v1
    with:
      username: ${{ github.actor }}
      password: ${{ secrets.GITHUB_TOKEN }}
      docker-image: ghcr.io/aboutbits/my-app
      docker-tag: latest
      build-args: |
        ARG1=abc
        ARG2=xyz
```

Push several tags of the same image with `docker-tags`, and build without push (e.g. in a pull request) with
`push: false`. With `load: true`, a later step can run the image, for example for a smoke test:

```yaml
  - uses: aboutbits/github-actions-docker/build-push@v1
    with:
      username: ${{ github.actor }}
      password: ${{ secrets.GITHUB_TOKEN }}
      docker-image: ghcr.io/aboutbits/my-app
      docker-tags: |
        1.2.3
        1.2.3-${{ github.sha }}
      platforms: linux/amd64,linux/arm64

  - uses: aboutbits/github-actions-docker/build-push@v1
    with:
      docker-image: my-app
      docker-tag: test
      push: false
      load: true
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name                | Required/Default | Description                                                                              |
|---------------------|------------------|------------------------------------------------------------------------------------------|
| `registry`          | `ghcr.io`        | Docker registry                                                                          |
| `username`          | if `push`        | Registry username                                                                        |
| `password`          | if `push`        | Registry password                                                                        |
| `docker-image`      | required         | Docker image name                                                                        |
| `docker-tag`        | /                | Docker image tag. Set either `docker-tag` or `docker-tags`.                              |
| `docker-tags`       | /                | Docker image tags, one per line. Set either `docker-tag` or `docker-tags`.               |
| `push`              | `true`           | Push the image to the registry. If `false`, the image is only built.                     |
| `load`              | `false`          | Load the image into the local Docker daemon. Works only for a single platform.           |
| `working-directory` | `.`              | The working directory                                                                    |
| `dockerfile`        | `Dockerfile`     | Path to the Dockerfile. (default {working-directory}/Dockerfile)                         |
| `build-args`        | /                | List of build-time variables                                                             |
| `platforms`         | /                | Target platforms for the build (comma-separated or multi-line string)                    |

#### Outputs

| Name     | Description  |
|----------|--------------|
| `digest` | Image digest |

## Build & Publish

To build and publish the action, visit the GitHub Actions page of the repository and trigger the workflow "Release Package" manually.

## Information

About Bits is a company based in South Tyrol, Italy. You can find more information about us on [our website](https://aboutbits.it).

### Support

For support, please contact [info@aboutbits.it](mailto:info@aboutbits.it).

### Credits

- [All Contributors](../../contributors)

### License

The MIT License (MIT). Please see the [license file](license.md) for more information.
