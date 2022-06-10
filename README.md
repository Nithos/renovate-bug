# Renovate Bug

Renovate parser correctly *FAILS* when processing the Renovate configuration file as `foo` is not a valid preset value.
However the configuration validator tool passes with the same configuration.

## Fails as intended
During procesing it fails correctly with validation error: `Cannot find preset's package (foo)`
```sh
docker run --rm -v $PWD/renovate.json5:/usr/src/app/renovate.json5 -e RENOVATE_TOKEN=token -e RENOVATE_REPOSITORIES=repo-path -it renovate/renovate
```

## Passes using the validator
The config validator tool does not detect the bad configuration but it
```sh
docker run --rm -v $PWD/renovate.json5:/usr/src/app/renovate.json5 -e RENOVATE_TOKEN=token -e RENOVATE_REPOSITORIES=repo-path -it renovate/renovate renovate-config-validator
```

> Bad configuration fields not added to the `extends` preset section seem to be detected correctly.