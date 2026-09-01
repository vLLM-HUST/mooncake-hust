# vLLM-HUST fork policy

This repository is the vLLM-HUST thin fork of
[`kvcache-ai/Mooncake`](https://github.com/kvcache-ai/Mooncake). Upstream
remains the source of truth for Mooncake Store, Transfer Engine, connectors,
transports, packaging, and lifecycle behavior.

Upstream already provides Ascend NPU CI, aarch64 NPU wheels, arm64 wheels, and
multi-architecture image publishing. The HUST fork therefore starts with no
core implementation delta. It exists to pin validated upstream revisions and
to carry only narrowly scoped Ascend/arm64 fixes that are proven necessary on
vLLM-HUST hosts.

The vLLM-HUST Extension Manager treats Mooncake as an external KV service. It
may discover compatibility, render connector configuration, and check service
health, but it does not own Mooncake's internal storage/transport lifecycle or
delete KV data.

The fork does not operate self-hosted GitHub runners. Automated portable tests
use GitHub-hosted runners. Ascend/NPU acceptance runs on demand on separately
operated hosts and is recorded as external evidence rather than requiring a
permanent Actions runner.

## Synchronizing upstream

```bash
git fetch upstream
git switch main
git merge --ff-only upstream/main
git push origin main
```

Any HUST patch should include an Ascend/arm64 reproduction and should be
proposed upstream when it is generally useful.
