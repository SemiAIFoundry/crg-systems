# CRG Systems 1.0.0

CRG Systems is a standalone product for realization modeling, decision
certification, evidence and qualification workflows, change control, portable
verification, and controlled physical feedback. This distribution includes
the Python application, CRG Studio browser interface, command-line tools,
secured API server, and an independent Node.js verifier.

CRG Systems is developed by semiAIfoundry Research, a research group within
Semi AI Foundry, LLC.

## License

Research, education, and other noncommercial use are permitted with the
attribution required by `LICENSE.md`. No separate commercial license is needed
for those uses.

**Any commercial use requires a separate written commercial license from
Semi AI Foundry, LLC.** This includes production or staging deployment for
commercial activity, commercial products or services, paid consulting,
customer deliverables, and revenue-supporting internal use.

Read `LICENSE.md` and `COMMERCIAL_LICENSE.md` before installing or using the
software. Commercial licensing requests:
https://semiaifoundry.com/contact/

## Requirements

- 64-bit CPython 3.10 through 3.14; CPython 3.12 is the validated release
  runtime.
- Linux with glibc 2.28+ or musl 1.2+ on x86-64 or AArch64; macOS 12+ on
  Apple silicon; or Windows on x86-64.
- Internet access during installation for pinned third-party dependencies.
- Node.js 22 or newer only for the independent JavaScript verifier.

## Install

From this directory:

```sh
python3 -m venv .venv
. .venv/bin/activate
python -m pip --isolated install --index-url https://pypi.org/simple \
  --require-hashes -r requirements.lock
python -m pip --isolated install --no-index --only-binary=:all: \
  --find-links wheels crg-systems==1.0.0
python -m pip check
```

The first command installs only hash-locked third-party wheels from the
configured Python package index. The second command disables package indexes
and installs CRG Systems exclusively from the included `wheels/` directory.

Third-party dependencies remain under their respective licenses, recorded in
`SBOM.cdx.json`. Those terms do not grant commercial rights in CRG Systems.

## Start CRG Studio locally

```sh
crg-studio --insecure-development --allow-loopback-http \
  --host 127.0.0.1 --port 8731 --root .crg-data
```

Open <http://127.0.0.1:8731/studio/>. Never expose the insecure-development
profile to another host or network.

## Secured deployment

Create secrets in your secret manager, adapt `config/security.example.json`,
and provide a TLS certificate and key:

```sh
export CRG_PASSWORD_PEPPER='<at least 32 random bytes>'
export CRG_OPERATOR_PASSWORD='<a long unique password>'
export CRG_LOCAL_KEK_BASE64='<base64 encoding of 32 random bytes>'

crg-studio --root /srv/crg \
  --security-config /etc/crg/security.json \
  --tls-cert /etc/crg/tls/server.crt \
  --tls-key /etc/crg/tls/server.key \
  --host 0.0.0.0 --port 8731
```

Production deployments must use authenticated principals, TLS, protected
storage, backups, production cryptography, and deployment-owned key custody.

## Product commands

- `crg` — command-line product interface
- `crg-studio` — secured API and standalone browser product
- `crg-serve` — headless API server
- `crg-worker` — durable external worker
- `crg-admin` — integrity, backup, restore, and federation administration
- `crg verify` — independent Python verification workflow
- `crg conformance` — compatibility and conformance workflow

Run a command with `--help` for its options.

## Independent JavaScript verifier

```sh
npm install --global ./crg-verifier-js-1.0.0.tgz
crg-verify-js --help
```

## Integrity and security

`SHA256SUMS` verifies the integrity of every file in this directory;
`MANIFEST.json` provides the same inventory in machine-readable form. The
checksum for the download archive is published beside it.

Follow `SECURITY.md` to report a vulnerability. Do not disclose exploitable
details publicly before coordinated review.
