# CI

Stromae V2 is hosted on github so we use Github Actions for continuous integration. The CI is divided into 4 files according to the actions, although I think a single file with conditions would be more readable.

## Github Secrets

If you fork the repository you will need to enable actions and to add some secrets.

| Secret Name             | Explication                                                                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| DOCKERHUB_REGISTRY_HOST | This is the registry host of the docker hub repository (usually the same as username but could change if your using bot )            |
| DOCKERHUB_USERNAME      | Docker hub username of the account which publish image                                                                               |
| DOCKERHUB_TOKEN         | The docker hub token linked with username                                                                                            |
| GITHUB_TOKEN            | [See official docs](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret) |

The `inseefr/stromae` projet publish docker image in the [`inseefr/stromae`](https://hub.docker.com/r/inseefr/stromae) dockerhub projet.

## Push on Branches named `v2-*` (except `v2-develop` and `v2-master`)

Each branch named `v2-*` will trigger a build and a docker stage at every push. See [`docker.yml`](https://github.com/InseeFr/Stromae/blob/083b8d05f51150cba6fcbdc6d89fda70121057ce/.github/workflows/docker.yml) file for more. The docker tag will be the name of the branch.

## Pull request on `v2-*`

Every pull request targeted on branch named `v2-*` will trigger a build stage. See [here](https://github.com/InseeFr/Stromae/blob/083b8d05f51150cba6fcbdc6d89fda70121057ce/.github/workflows/build.yml) for more.

## Push on branch `v2-develop`

Every push on v2-develop will trigger a build, release and docker stage. Unfortunately, if the version has not been updated you will encounter an error because release stage will try to make a github release that already exist. In `v2-develop`, release is a release candidate (`"version-in-package.json"-rc`) and same for docker tag. See [here](https://github.com/InseeFr/Stromae/blob/083b8d05f51150cba6fcbdc6d89fda70121057ce/.github/workflows/develop-release.yml) for more.

## Push on branch `v2-master`

This is the same as [`v2-develop`](ci.md#push-on-branch-v2-develop) except that it is not release candidate but real with `"version-in-package.json"`. See [here](https://github.com/InseeFr/Stromae/blob/083b8d05f51150cba6fcbdc6d89fda70121057ce/.github/workflows/release.yml) for more.
