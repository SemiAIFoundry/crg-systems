# CRG Systems 1.4.0

CRG Systems is a standalone product for realization modeling, decision certification, evidence and qualification workflows, change control, portable verification, and controlled physical feedback. This public-runtime distribution includes the Python application, CRG Studio, command-line tools, secured API server, and independent JavaScript verifier.

> **Theory and publication record:** See the
> [Computation-Realization Geometry research and validation corpus](https://github.com/SemiAIFoundry/computation-realization-geometry)
> and the canonical manuscript,
> [*A Communication Theory of Computation Realization*](https://doi.org/10.5281/zenodo.22048090).

## What is Computation-Realization Geometry?

Computation-Realization Geometry (CRG) starts from a distinction that ordinary
software and systems descriptions often blur: a **computation** states the
meaning, relations, and obligations that must be preserved, while a
**realization** is one legal way to implement that computation under particular
resource, technology, interface, physical, and operating constraints. The same
computation can admit many realizations, and choosing one too early can destroy
valuable alternatives or make later changes unnecessarily expensive.

CRG represents those legal realizations as a resource-conditioned feasible
family. It records how candidates compare across measures such as cost,
latency, energy, reliability, qualification status, and implementation risk;
identifies retained and frontier alternatives; and makes losses of optionality
explicit. A **safe commitment** is therefore not merely a selected design. It
is a selection accompanied by evidence showing which alternatives remain
legal, which were excluded, which assumptions justify the exclusion, and what
must be rechecked when those assumptions change.

CRG Systems operationalizes that model. It binds decisions to canonical
records, registries, hashes, witnesses, approvals, conversions, and lifecycle
evidence so that a result can be reviewed, reproduced, challenged, migrated,
or independently verified. It is designed to work alongside compilers,
optimizers, EDA and simulation tools, laboratory systems, databases, and
engineering workflows rather than replacing them.

## Theoretical foundation and publications

The separate
[Computation-Realization Geometry repository](https://github.com/SemiAIFoundry/computation-realization-geometry)
is the public scientific companion to this implementation. It provides the
theoretical foundation, finalized manuscript and DOI crosswalk, reproduction
programs, theorem checks, benchmark inputs, retained numerical results, figures,
negative controls, and machine-readable integrity records. Its
[publication corpus](https://github.com/SemiAIFoundry/computation-realization-geometry/tree/main/manuscripts)
is the authoritative entry point for the full publication record and
specialist manuscripts. The canonical integrated theory is:

> Fitih M. Cinnor, *A Communication Theory of Computation Realization:
> Resource-Conditioned Geometry of Legal Realizations and the Safe-Commitment
> Law*, 2026. [doi:10.5281/zenodo.22048090](https://doi.org/10.5281/zenodo.22048090).

## License

Research, education, and other noncommercial use are permitted with the attribution required by `LICENSE.md`. Commercial use requires a separate written license from Semi AI Foundry, LLC. See `LICENSE.md` and `COMMERCIAL_LICENSE.md`.

## Install

```sh
python3 -m venv .venv
. .venv/bin/activate
python -m pip --isolated install --require-hashes -r requirements.lock
python -m pip --isolated install --no-index --only-binary=:all: --find-links wheels crg-systems==1.4.0
python -m pip check
```

Python 3.10 through 3.14 is supported; CPython 3.12 is the validated release runtime. Third-party terms and exact dependency identity are recorded in `SBOM.cdx.json`.

## Local Studio

```sh
crg-studio --insecure-development --allow-loopback-http --host 127.0.0.1 --port 8731 --root .crg-data
```

Never expose the insecure-development profile to another host or network. Production use requires authenticated principals, TLS, protected storage, backups, and deployment-owned key custody.

## JavaScript verifier

```sh
npm install --global ./crg-verifier-js-1.4.0.tgz
crg-verify-js --help
```

The `sdk-assets/` directory contains local-install Python and JavaScript client artifacts; they are not registry publications. Verify every file with `SHA256SUMS`; `MANIFEST.json` provides the same hash-bound inventory in machine-readable form.
