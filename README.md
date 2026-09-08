# Llaminar corpora

The canonical home for all published Llaminar tuning and certification corpora.
The source repository pins this repository as its optional `corpora/` submodule;
normal source builds and checkouts do not require these payloads.

Organize corpus families at the top level. NativeVNNI generations live under
`native_vnni_dispatch/<backend>/<architecture>/<inventory>-<configuration>/`.
Payloads use Git LFS by default. Small manifests, documentation, and generated
policy source remain reviewable in ordinary Git.

## Materialize selected evidence

From the Llaminar source checkout:

```bash
GIT_LFS_SKIP_SMUDGE=1 git submodule update --init -- corpora
git -C corpora lfs pull --include 'native_vnni_dispatch/cpu/**' --exclude ''
```

Narrow the include pattern to an exact generation when possible. To materialize
all evidence explicitly, run `git -C corpora lfs pull --include '*' --exclude ''`.
Never initialize or download the corpus submodule during an ordinary source
build, container build, or unit/preflight gate.

## Publish

Collect and certify in the source repository's ignored work directories. Publish
only complete generations through the family's sealer/verifier. Preserve every
payload byte and its manifest provenance; never edit a sealed generation in place.
New corpus families belong here too, not in the source repository.

Commit the generation in this repository and push its Git LFS objects and commit
before updating the source repository's `corpora` gitlink. Then commit and push
the gitlink with the consuming code or policy update. If deliberately bypassing
push hooks, run `git lfs push origin HEAD` before `git push --no-verify` so the
remote commit never references unavailable payloads.

Installed dispatch tables and small device-free test fixtures remain in the
source repository; they are not a reason to require a corpus checkout at runtime.

The initial NativeVNNI snapshot was imported unchanged from Llaminar commit
`a05fd069f`, formerly at `benchmark_results/native_vnni_dispatch/corpora/`.
