# GitHub Actions Docker

A collection of GitHub actions for Docker.

## Build and Push

Build and push a docker image using a Dockerfile.

### Example

```yaml
  - uses: aboutbits/github-actions-docker/build-push@v1
    with:
      username: ${{ github.actor }}
      password: ${{ secrets.GITHUB_TOKEN }}
      docker-image: ghcr.io/aboutbits/my-app
      docker-tag: latest
```

## Versioning

In order to have a versioning in place and working, create lightweight tags that point to the appropriate minor release versions.

Creating a new minor release:

```bash
git tag v1
git push --tags
```

Replacing an already existing minor release:

```bash
git tag -d v1
git push origin :refs/tags/v1
git tag v1
git push --tags
```

## Information

About Bits is a company based in South Tyrol, Italy. You can find more information about us on [our website](https://aboutbits.it).

### Support

For support, please contact [info@aboutbits.it](mailto:info@aboutbits.it).

### Credits

- [All Contributors](../../contributors)

### License

The MIT License (MIT). Please see the [license file](license.md) for more information.
