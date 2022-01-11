# Set Up Action Cache GitHub Action 

GitHub Action to configure an action cache with restore keys that consist of a prefix, the runner
OS, a cache name, and a suffix.


## Quickstart

Typically, a workflow will set up a cache directory to save workflow artifacts between runs. The
selection of values for the `key_prefix`, the `cache_name`, and the `key_suffix` are related to how
you want to the cache to match/invalidate. One should set the `cache_name` to a stable, meaningful
value. The `key_suffix` should be set to an expression that hashes a meaningful set of files in the
repository. The `key_prefix` need only be set if/when it is necessary to invalidate all previous
cache values.See [actions/cache](https://github.com/actions/cache) for more details.

```yaml
jobs:
  ubuntu_build:
    runs-on: ubuntu-20.04
    steps:
    - uses: actions/checkout@v2

    - name: Test Cache for CI
      uses: cgrindel/gha_set_up_action_cache@v1
      with:
        path: ~/.cache/my_cache
        key_prefix: "2022-01-10T16:19:15" 
        cache_name: gha_set_up_action_cache_ci
        key_suffix: ${{ hashFiles('**/foo.lock') }}
```
