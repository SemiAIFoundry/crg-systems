# CRG Systems 1.3.0

CRG Systems is a standalone product for realization modeling, decision certification, evidence and qualification workflows, change control, portable verification, and controlled physical feedback. This public-runtime distribution includes the Python application, CRG Studio, command-line tools, secured API server, and independent JavaScript verifier.

## License

Research, education, and other noncommercial use are permitted with the attribution required by `LICENSE.md`. Commercial use requires a separate written license from Semi AI Foundry, LLC. See `LICENSE.md` and `COMMERCIAL_LICENSE.md`.

## Install

```sh
python3 -m venv .venv
. .venv/bin/activate
python -m pip --isolated install --require-hashes -r requirements.lock
python -m pip --isolated install --no-index --only-binary=:all: --find-links wheels crg-systems==1.3.0
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
npm install --global ./crg-verifier-js-1.3.0.tgz
crg-verify-js --help
```

The `sdk-assets/` directory contains local-install Python and JavaScript client artifacts; they are not registry publications. Verify every file with `SHA256SUMS`; `MANIFEST.json` provides the same hash-bound inventory in machine-readable form.
