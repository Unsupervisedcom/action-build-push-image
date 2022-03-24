<!-- start title -->

# GitHub Action:Build and Push image

<!-- end title -->
<!-- start description -->

Builds an image, pushes to google artifact registry, and caches to gha as well as the `cache` tag. Specifically designed to work with google artifact registry. This is also designed to work on a release trigger by default, and will push latest, and the release tag.

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: Unsupervisedcom/action-build-push-image@undefined
  with:
    # the path of the dockerfile to use for the build
    # Default: ./Dockerfile
    dockerfile: ""

    # gcloud service account credentials json
    credentials-json: ""

    # gcloud project id
    project-id: ""

    # artifact registry region
    # Default: us-central1
    region: ""

    # artifact registry repository
    # Default: images
    repository: ""

    # docker build secrets, comma separated string key=value
    # Default:
    secrets: ""

    # docker build secret files, this is better suited for json and things like that
    # Default:
    secret-files: ""

    # whether to pull submodules for image build
    # Default: false
    submodules: ""

    # tag name, excluding tag version, such as `myapp`
    # Default: ${{ github.event.repository.name }}
    tag-name: ""

    # git tags to push, comma separated string such as `latest,v1.0.0`
    # Default: latest,${{ github.event.release.tag_name }}
    tag-versions: ""

    # git hub token
    # Default:
    token: ""

    # git tag version to use for the registry cache
    # Default: cache
    cache-tag-version: ""

    # This action mounts the google application credentials file as a secret. The
    # default value of GOOGLE_APPLICATION_CREDENTIALS makes it really easy to use in
    # dockerfiles for private dependencies. See graphql-apollo-typescript for an
    # example. This configuration allows you to override the default value and use
    # some other secret name.
    # Default: GOOGLE_APPLICATION_CREDENTIALS
    credentials-json-secret-name: ""
```

<!-- end usage -->
   <!-- start inputs -->

| **Input**                          | **Description**                                                                                                                                                                                                                                                                                                                            |                  **Default**                  | **Required** |
| :--------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------: | :----------: |
| **`dockerfile`**                   | the path of the dockerfile to use for the build                                                                                                                                                                                                                                                                                            |                `./Dockerfile`                 |  **false**   |
| **`credentials-json`**             | gcloud service account credentials json                                                                                                                                                                                                                                                                                                    |                                               |   **true**   |
| **`project-id`**                   | gcloud project id                                                                                                                                                                                                                                                                                                                          |                                               |   **true**   |
| **`region`**                       | artifact registry region                                                                                                                                                                                                                                                                                                                   |                 `us-central1`                 |  **false**   |
| **`repository`**                   | artifact registry repository                                                                                                                                                                                                                                                                                                               |                   `images`                    |  **false**   |
| **`secrets`**                      | docker build secrets, comma separated string key=value                                                                                                                                                                                                                                                                                     |                                               |  **false**   |
| **`secret-files`**                 | docker build secret files, this is better suited for json and things like that                                                                                                                                                                                                                                                             |                                               |  **false**   |
| **`submodules`**                   | whether to pull submodules for image build                                                                                                                                                                                                                                                                                                 |                                               |  **false**   |
| **`tag-name`**                     | tag name, excluding tag version, such as `myapp`                                                                                                                                                                                                                                                                                           |     `${{ github.event.repository.name }}`     |  **false**   |
| **`tag-versions`**                 | git tags to push, comma separated string such as `latest,v1.0.0`                                                                                                                                                                                                                                                                           | `latest,${{ github.event.release.tag_name }}` |  **false**   |
| **`token`**                        | git hub token                                                                                                                                                                                                                                                                                                                              |                                               |  **false**   |
| **`cache-tag-version`**            | git tag version to use for the registry cache                                                                                                                                                                                                                                                                                              |                    `cache`                    |  **false**   |
| **`credentials-json-secret-name`** | This action mounts the google application credentials file as a secret. The default value of GOOGLE_APPLICATION_CREDENTIALS makes it really easy to use in dockerfiles for private dependencies. See graphql-apollo-typescript for an example. This configuration allows you to override the default value and use some other secret name. |       `GOOGLE_APPLICATION_CREDENTIALS`        |  **false**   |

<!-- end inputs -->
   <!-- start outputs -->

| **Output**      | **Description** | **Default** | **Required** |
| :-------------- | :-------------- | ----------- | ------------ |
| `random-number` | Random number   |             |              |

<!-- end outputs -->
   <!-- start examples -->

### Example usage that includes a docker secret

```yaml
name: Build and push image to GAR
on:
  release:
    types: [created]
jobs:
  build-push-image:
    runs-on: ubuntu-latest
    steps:
      - uses: Unsupervisedcom/action-build-push-image@v1
        with:
          credentials-json: ${{ secrets.GOOGLE_ARTIFACT_READ_WRITE }}
          project-id: ${{ secrets.GOOGLE_ARTIFACT_PROJECT_ID }}
          secrets: secret1=${{ secrets.SECRET_ONE }}
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
