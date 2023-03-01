# CI

Shared helpers to dry out common CI scripts used by plugins.

LogStash plugins by convention store their own configurations under `.ci/` and `.buildkite/` folders.
This common `.ci` is meant to be a common ot an optional replacement for most `.ci/*` files.


## How to use common script in Buildkite?

In plugin's pipeline definition (example `.buildkite/pipeline.yml`), pull the this common script and exclude intersected files


```
mkdir -p .ci && curl -sL https://github.com/mashhurs/.ci/archive/main.tar.gz | tar zxvf - --skip-old-files --strip-components=1 -C .ci --wildcards '*Dockerfile*' '*docker*' '*.sh'

```

### TODO

- Currently, as we are moving to Buildkite, the run config is located under `.buildkite/pipeline.yml` and it frequently changes. We may make a common shell script under this repository where all plugins can leverage.

- Travis configs are removed. Some of them belong to performance test configurations. Let's also make a common config for the performance tests as well.


### Custom behaviour

If the plugin follows conventions and (unit) tests all run using `rspec`, simply
place your own shell scripts in the .ci folder
