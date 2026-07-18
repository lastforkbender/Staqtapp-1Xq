# Staqtapp 1Xq

Staqtapp 1Xq is a Beta intelligent storage engine for Python. It combines an
authoritative storage execution plane with bounded discrete mathematics,
storage management, and an embedded governed-AI subsystem that can observe,
reason, learn bounded patterns, and propose improvements without acquiring
direct mutation authority.

**Staqtapp executes. 1Xq reasons. Improvement proposes. Reality confirms.**

Staqtapp 1Xq is its own intelligent-storage-engine product. It is not
Staqtapp-1X or Staqtapp-TDS, and it makes no compatibility, protocol,
telemetry-architecture, or migration claim for either product.

[Download the 2.2.5H API Quick Programmer Reference
(PDF)](https://github.com/lastforkbender/Staqtapp-1Xq/blob/v2.2.5/docs/STAQTAPP_1Xq_API_Quick_Programmer_Reference_2.2.5H.pdf)

Release `2.2.5H` is distributed as `staqtapp-1xq==2.2.5`. It is a
foundation-hardening candidate with a Beta classifier. Local Linux storage,
governance, clean-wheel, and off-screen PyQt5 validation pass; the external
Ubuntu/Windows/macOS CI matrix and native-desktop checks remain public-release
gates.

## Why 1Xq is an intelligent storage engine

1Xq does not bolt an unrestricted model onto a storage API. It creates a
governed mathematical loop between real storage behavior and bounded learning:

1. Staqtapp executes typed reads, writes, transactions, persistence, integrity,
   and recovery.
2. 1Xq consumes bounded source records from storage geometry, computational
   memory, paired pressure trials, property lineage, and intelligence cycles.
3. Integer-only projections turn those observations into reproducible Q16
   bins, percentiles, counts, lineage marks, and relationship distributions.
4. Bounded learning components can detect recurring phase motifs, estimate
   transition probabilities, classify synthetic counterfactuals, or rank
   candidate properties.
5. A candidate can reach real operations only through an immutable, scoped,
   budgeted, expiring, fenced activation directive.
6. Real operation receipts and sealed `REALITY` evidence must verify before
   governance can consider promotion. Rejected, stale, repeated, shadow,
   synthetic, demo, and derived-fingerprint records remain separate.

| Source record | Discrete projection | Learning link | Storage-management link |
|---|---|---|---|
| Interval geometry | Occupancy bins; density, fragmentation, locality, merge/split counts | Detect changing geometric regimes | Propose compaction or placement changes |
| Computational memory | Layer population; age, reuse, compacted bytes, promotions, evictions | Bound retained classifications and reuse patterns | Propose retention or tiering changes |
| Paired pressure trials | Ordered latency curve; integer p50/p95/p99; recovery Q16 | Compare candidates without fixed baseline-first bias | Qualify performance and recovery |
| Evolution lineage | Generation exposure and rollback marks | Preserve parent/candidate relationships | Control rollout and exact fallback |
| Intelligence ledger | Evidence-class counts and cycle edges | Connect bounded reasoning cycles | Preserve traceable learning context |

A stable signature is a deterministic grouping and replay identity. It is not
proof, evidence, or promotion authority. Hash-derived console data is labeled
`DERIVED_FINGERPRINT`.

See the [product boundary](docs/PRODUCT_BOUNDARY.md), [determinism
contract](docs/2.2.5H/DETERMINISM_CONTRACT.md), and [evidence and integrity
model](docs/2.2.5H/EVIDENCE_AND_INTEGRITY.md).

## Install

### Core engine

After publication:

```bash
python -m pip install "staqtapp-1xq==2.2.5"
```

From a source checkout:

```bash
python -m pip install .
```

Optional accelerated typed JSON:

```bash
python -m pip install "staqtapp-1xq[fastjson]==2.2.5"
```

### Qt operations console

Yes, the PyQt5 application is included in the distribution. The wheel contains
`staqtapp.console`, the application/worker/adapter/model/theme modules, all
seven SVG resources, and the `staqtapp-console` entry point. Qt is optional and
stays outside the storage hot path.

Published-package installation:

```bash
python -m pip install "staqtapp-1xq[console]==2.2.5"
python -c "import PyQt5, psutil, staqtapp.console; print('console ready')"
staqtapp-console
```

Source-checkout installation:

```bash
python -m pip install ".[console]"
staqtapp-console
```

The `console` extra installs `PyQt5>=5.15.10` and `psutil>=5.9`. Headless
deployments can install only the core package.

## Ten-minute storage path

```python
from pathlib import Path
import staqtapp

staqtapp.configure(storage_dir=Path("./data"))
staqtapp.makevfs("accounts", "Production", "Primary")

staqtapp.set_value("user_1001", {
    "name": "Rob",
    "active": True,
    "balance": 500,
})

user = staqtapp.get_value("user_1001")
assert user["balance"] == 500
```

Variable names match `[A-Za-z_][A-Za-z0-9_]*`. VFS names may additionally use
hyphens; directory and folder names begin with a letter and contain letters or
hyphens.

New governed integrations should import the explicit boundary at
`staqtapp.public_api`. The package root remains a compatibility facade.

## Embedded AI and storage integration

The following example builds a deterministic projection from real, typed source
records and stores it through a Staqtapp transaction. The projection remains
non-authoritative until the evidence path verifies it.

```python
import staqtapp
from staqtapp.public_api import (
    BoundedMathematicalAggregator,
    IntervalGeometryObservation,
    MathematicalDataClass,
    MathematicalSourceBundle,
)

source = MathematicalSourceBundle(
    interval_geometry=(
        IntervalGeometryObservation(
            interval_density_q16=32_000,
            fragmentation_q16=4_100,
            merge_count=8,
            split_count=2,
            occupancy_q16=48_000,
            depth=4,
            locality_q16=52_000,
        ),
    ),
    data_class=MathematicalDataClass.REALITY,
    source_ids=("runtime-sample:17",),
    evidence_qualified=False,
)

projection = BoundedMathematicalAggregator(
    max_records_per_source=256
).aggregate(source, bins=8)

record = {
    "signature": projection.signature,
    "data_class": projection.data_class.value,
    "evidence_qualified": projection.evidence_qualified,
    "truncated": projection.truncated,
    "measures": {item.key: item.value for item in projection.measures},
}

result = staqtapp.run_transaction([
    ("set_value", ("cycle_projection", record)),
    ("set_value", ("cycle_status", "observed")),
])
assert result
```

The complete executable version is
[`examples/embedded_ai_storage.py`](examples/embedded_ai_storage.py) and is
exercised by the test suite.

## Atomic multi-operation updates

`run_transaction()` is single-VFS, mutation-only, read-your-own-writes, and
all-or-nothing.

```python
staqtapp.set_value("temporary", "remove after commit")

result = staqtapp.run_transaction([
    ("set_value", ("balance", 400)),
    ("set_value", ("status", "paid")),
    ("removevar", ("temporary",)),
])

if not result:
    print(result.failure.error_type, result.failure.message)
```

## Optional adaptive write batching

Immediate durability is the default. Batching creates an explicit
queued-versus-durable boundary.

```python
staqtapp.configure(
    write_batching=True,
    batch_max_operations=100,
    batch_max_wait_ms=5,
)

receipt = staqtapp.set_value("event_1", {"type": "login"})
result = staqtapp.flush_writes()  # durability barrier
```

## Integrity, revisions, and recovery

```python
staqtapp.set_value("blob", "x" * 8192)
staqtapp.rebuild_read_index()
chunk = staqtapp.read_payload_range("blob", start=4096, length=1024)

report = staqtapp.verify_integrity(deep=True)
revisions = staqtapp.list_revisions(limit=10)

staqtapp.optimize_vfs()
staqtapp.compact_vfs(keep_revisions=32)
```

Verify before recovery. `repair_vfs()` uses a declared valid source and does
not invent an unrecorded outcome.

## Non-halting result model

Ordinary storage API failures return a false-valued `CallFailure` instead of
escaping into the host application's control loop.

```python
result = staqtapp.get_value("missing")
if not result:
    print(result.error_type, result.message)

# Execution continues.
staqtapp.set_value("next_operation", "ready")
```

Authority and integrity boundaries still use typed governance exceptions where
continuing would violate the contract.

## Governed activation and evidence

`ActivationRouter` consumes an already-authorized directive, selects a baseline
or candidate generation deterministically, and writes a receipt. It does not
reason or execute storage. `ScopedStorageExecutionGateway` invokes exactly the
handler selected by that receipt.

`EvidenceVerifier` derives authority only after checking canonical digests,
trusted collector HMAC, runtime/storage/workload/candidate/scope bindings,
measurement digests, exact receipt exposure, evidence class, and durable
anti-replay state. A caller cannot set `authoritative=True`.

| Data class | Intended use | Promotion authority |
|---|---|---|
| `REALITY` | Measured real operation outcomes | Only after complete verification and consumption |
| `SHADOW` | Non-dispatch evaluation | Never |
| `SYNTHETIC` | Counterfactual/generated scenario | Never |
| `DEMO` | Presentation fixture | Never |
| `DERIVED_FINGERPRINT` | Hash-derived display identity | Never; not evidence |

See the [activation routing
specification](docs/2.2.5H/ACTIVATION_ROUTING_SPEC.md) and [state, concurrency,
and administration
contract](docs/2.2.5H/STATE_CONCURRENCY_ADMIN.md).

## Command-line tools

```bash
staqtapp --help
staqtapp-1xq --help
staqtapp-console
```

Offline journal and evidence verification is diagnostic only. It cannot consume
the authoritative anti-replay record or grant promotion authority.

## Qt application screenshots — all eight pages

The console uses responsive Qt layouts with a documented minimum size of
1100 x 700. Local PyQt5 5.15.11 / Qt 5.15.14 validation exercised the event
loop, real adapter, worker refresh, pause/resume/drain acknowledgements, manual
refresh, resizing, all eight pages, and clean thread shutdown. The images below
come from the packaged Qt application connected to a seeded, real local 1Xq
VFS/runtime qualification session: 24 verified storage write/read round trips,
24 durable intelligence-ledger cycles, and live scheduler state. No screenshot
uses a mock or visual fixture. This bounded release-qualification session is
not represented as production telemetry. Twelve frames rendered without a
detected empty page, clipping issue, severe Qt message, or shutdown hang.

Overview, Runtime, Scheduler, and Intelligence are functional 2.2.5H surfaces.
Evolution, Pressure, Audit, and Settings are explicit foundation workspaces;
they are included below for honest full-page coverage and are not represented
as completed 2.2.6 features.

<p align="center"><strong>01 — Overview</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/01-overview-1440x900.png" alt="Staqtapp 1Xq Overview running a verified local qualification session" width="100%">
</p>
<p align="center"><strong>02 — Runtime</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/02-runtime-1440x900.png" alt="Staqtapp 1Xq Runtime running a verified local qualification session" width="100%">
</p>
<p align="center"><strong>03 — Evolution — foundation workspace</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/03-evolution-1440x900.png" alt="Staqtapp 1Xq Evolution foundation workspace" width="100%">
</p>
<p align="center"><strong>04 — Pressure — foundation workspace</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/04-pressure-1440x900.png" alt="Staqtapp 1Xq Pressure foundation workspace" width="100%">
</p>
<p align="center"><strong>05 — Scheduler</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/05-scheduler-1440x900.png" alt="Staqtapp 1Xq Scheduler showing completed leased and queued qualification jobs" width="100%">
</p>
<p align="center"><strong>06 — Intelligence</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/06-intelligence-1440x900.png" alt="Staqtapp 1Xq Intelligence showing durable qualification cycles" width="100%">
</p>
<p align="center"><strong>07 — Audit — foundation workspace</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/07-audit-1440x900.png" alt="Staqtapp 1Xq Audit foundation workspace" width="100%">
</p>
<p align="center"><strong>08 — Settings — foundation workspace</strong><br>
  <img src="https://raw.githubusercontent.com/lastforkbender/Staqtapp-1Xq/v2.2.5/docs/screenshots/console_pages/08-settings-1440x900.png" alt="Staqtapp 1Xq Settings foundation workspace" width="100%">
</p>

Linux off-screen validation does not replace native-compositor, accessibility,
multiple-DPI/font, Windows, or macOS validation.

GitHub and PyPI render this same `README.md`. The PNG bytes live in the GitHub
repository under `docs/screenshots/console_pages/`; PyPI retrieves them through
the absolute, immutable `v2.2.5` URLs above rather than from the wheel or
sdist. Release order is therefore mandatory: push the exact release commit,
create tag `v2.2.5`, pass
`python scripts/validate_published_media.py --remote`, and only then publish the
already validated distributions to PyPI. The remote gate requires every PNG and
the API PDF to be byte-identical to the release candidate.

## Documentation

- [API Quick Programmer Reference
  (PDF)](https://github.com/lastforkbender/Staqtapp-1Xq/blob/v2.2.5/docs/STAQTAPP_1Xq_API_Quick_Programmer_Reference_2.2.5H.pdf)
- [API manual policy](docs/API_MANUAL_POLICY.md)
- [Recovery guide](docs/RECOVERY_GUIDE.md)
- [Security model](docs/SECURITY_MODEL.md)
- [Determinism contract](docs/2.2.5H/DETERMINISM_CONTRACT.md)
- [Evidence and integrity model](docs/2.2.5H/EVIDENCE_AND_INTEGRITY.md)
- [Activation routing specification](docs/2.2.5H/ACTIVATION_ROUTING_SPEC.md)
- [Claim Registry](docs/2.2.5H/CLAIM_REGISTRY.md)
- [Operations console](docs/OPERATIONS_CONSOLE.md)
- [2.2.5H hardening report](docs/2.2.5H/FOUNDATION_HARDENING_REPORT.md)

The versioned quick reference documents the implemented 2.2.5H programmer
path. The final exhaustive API manual remains scheduled after the phase-2.3.7
public API freeze.

## Development validation

```bash
python -m pip install ".[dev,console,docs]"
python -m pytest
python scripts/validate_console_visual.py docs/screenshots/console_pages
python scripts/validate_published_media.py
python scripts/build_api_quick_reference.py
python scripts/validate_api_quick_reference.py --record-visual-pass
python -m build
python -m twine check dist/*
```

The supplied CI workflow targets Python 3.10 and 3.12 on Ubuntu, Windows, and
macOS. The release must not be described as cross-platform validated until
that matrix passes for the exact candidate.

## License

MIT. See [LICENSE](LICENSE).
