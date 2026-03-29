<img src="https://openmlst-web.vercel.app/logo.svg" alt="OpenMLST" height="52">

# openmlst-data

Hash-addressed allele registry for [OpenMLST](https://openmlst-web.vercel.app).

## What this is

This repository is the OpenMLST allele registry — a plain-text, git-versioned database of MLST allele sequences indexed by SHA-1 hash.

One directory per scheme, one file per locus:

```
{scheme}/{locus}.txt
```

Each line is allele N (line 1 = allele 1). Format is tab-separated:

```
sha1hash<TAB>sequence<TAB>accession
```

- **sha1hash** — SHA-1 of the lowercase sequence
- **sequence** — full allele sequence in uppercase
- **accession** — assembly accession of first observation (may be blank for seeded alleles)

Blank lines are placeholders that preserve allele number alignment.

## Data provenance and cutoff

> **Important:** This registry contains only MLST allele data that was publicly available as of **31 December 2024**.

PubMLST ([pubmlst.org](https://pubmlst.org)) and the Pasteur BIGSdb instance ([bigsdb.pasteur.fr](https://bigsdb.pasteur.fr)) changed their data access policy on **1 January 2025**: alleles and profiles added after that date require authenticated API access and are not available to anonymous users. The full policy statement is available on the PubMLST website.

**What this means for this registry:**

- Alleles seeded before January 2025 were sourced from PubMLST and Pasteur BIGSdb while that data was publicly accessible.
- Allele integers in this registry match the corresponding PubMLST integers for all pre-2025 alleles.
- **No allele sequence data beyond 31 December 2024 has been obtained from PubMLST or Pasteur.** We do not redistribute any data that falls under their post-2024 access restrictions.
- Alleles added to this registry after January 2025 are community-contributed submissions received through the OpenMLST API. These are independently assigned integers and are not sourced from PubMLST.

If you need access to alleles submitted to PubMLST after December 2024, please register at [pubmlst.org](https://pubmlst.org) and use their authenticated API.

## Registry growth after the cutoff

Novel alleles observed by OpenMLST users are submitted via the [openmlst-web API](https://openmlst-web.vercel.app/docs) and appended to this registry. Community alleles receive stable integer identifiers that are consistent within OpenMLST but may differ from any numbers PubMLST independently assigns post-2025.

Every submission is a git commit — the full history is auditable.

## Schemes

Schemes follow the PubMLST database naming convention (e.g. `pubmlst_escherichia_seqdef`). Schemes from the Pasteur BIGSdb instance use the same convention (e.g. `pubmlst_klebsiella_seqdef`).

## Usage

The registry is consumed by:

- [openmlst-client](https://github.com/OpenMLST/openmlst-client) — CLI tool (`pixi run openmlst`)
- [openmlst-web](https://github.com/OpenMLST/openmlst-web) — web caller and API

See the [documentation](https://openmlst-web.vercel.app/docs) for integration details.

## Contributing

Submit novel alleles via the API:

```bash
POST https://openmlst-web.vercel.app/api/allele
[{ "scheme": "pubmlst_escherichia_seqdef", "locus": "icd", "sequence": "atg..." }]
```

Direct pull requests to this repository are not accepted — all submissions must go through the validated API.

## Governance

OpenMLST is community-governed. See the [governance page](https://openmlst-web.vercel.app/governance) for the steering group, terms of reference, and meeting minutes.
