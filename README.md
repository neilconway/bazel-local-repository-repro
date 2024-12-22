# bazel-local-repository-repro

Observed Behavior:

## Bazel 7.1.1

```
$ USE_BAZEL_VERSION=7.1.1 bazelisk build //...
Starting local Bazel server and connecting to it...
INFO: Analyzed target //:baz (69 packages loaded, 347 targets configured).
INFO: From Linking libbaz.a:
warning: /Library/Developer/CommandLineTools/usr/bin/libtool: archive library: bazel-out/darwin_arm64-fastbuild/bin/libbaz.a the table of contents is empty (no object file members in the library define global symbols)
INFO: Found 1 target...
Target //:baz up-to-date:
  bazel-bin/libbaz.a
INFO: Elapsed time: 2.403s, Critical Path: 0.14s
INFO: 5 processes: 2 internal, 3 darwin-sandbox.
INFO: Build completed successfully, 5 total actions
$ USE_BAZEL_VERSION=7.1.1 bazelisk clean --expunge
```

## Bazel 8.0.0

```
$ USE_BAZEL_VERSION=8.0.0 bazelisk build //...
Starting local Bazel server and connecting to it...
WARNING: Couldn't auto load rules or symbols, because no dependency on module/repository 'rules_android' found. This will result in a failure if there's a reference to those rules or symbols.
ERROR: no such package '@@[unknown repo 'repo2' requested from @@]//': The repository '@@[unknown repo 'repo2' requested from @@]' could not be resolved: No repository visible as '@repo2' from main repository. Was the repository introduced in WORKSPACE? The WORKSPACE file is disabled by default in Bazel 8 (late 2024) and will be removed in Bazel 9 (late 2025), please migrate to Bzlmod. See https://bazel.build/external/migration
ERROR: /Users/neilconway/bazel-local-repository-repro/BUILD.bazel:1:11: no such package '@@[unknown repo 'repo2' requested from @@]//': The repository '@@[unknown repo 'repo2' requested from @@]' could not be resolved: No repository visible as '@repo2' from main repository. Was the repository introduced in WORKSPACE? The WORKSPACE file is disabled by default in Bazel 8 (late 2024) and will be removed in Bazel 9 (late 2025), please migrate to Bzlmod. See https://bazel.build/external/migration and referenced by '//:baz'
ERROR: Analysis of target '//:baz' failed; build aborted: Analysis failed
INFO: Elapsed time: 3.204s, Critical Path: 0.01s
INFO: 1 process: 1 internal.
ERROR: Build did NOT complete successfully
```
