# PubMed Research Toolkit

An older Python research-automation project for publication search, metadata export and resumable collection.

## Problem and approach

Literature review involves repeated searches and metadata collection. These scripts collect PubMed search results into JSON and include checkpoint and retry logic for interrupted jobs, providing inputs for further research analysis.

## What is in the repository

- `pubmed_search.py`: uses `pymed` to query PubMed and writes `data.json`. The current query and dates are hard-coded for a 2020 search; edit and review them before use.
- `pubmed_central.py`: historical PMID-based downloader with lock-file progress, failed-item tracking and resume/retry options.
- `pubmed_info.py` and `pubmed_info.reader.py`: exploratory metadata and PDF-reading utilities.
- `requirements.txt`: the actual pinned dependencies, including Requests, lxml, pymed, BeautifulSoup, pdfminer and fake-useragent. These are older pins, not a tested modern environment.

The project has not been validated against current PubMed/PMC pages or current Python dependencies. No download throughput, guaranteed reliability or production scale is claimed.

## Access policy and modernization

The legacy downloader scrapes HTML and contains proxy-pool code. It is not the recommended path for a current automated or bulk PMC collection.

PMC restricts automated content retrieval to its approved services, including the PMC Cloud Service, OAI-PMH, E-Utilities and BioC API. Use those services and respect article licenses. Do not rotate proxies to bypass access controls, rate limits or a 403 response. [PMC developer guidance](https://pmc.ncbi.nlm.nih.gov/tools/developers/).

Before using this project for a new collection:

1. Replace the legacy HTML downloader with an approved retrieval service.
2. Configure the query, date range and request limits explicitly.
3. Update dependencies and validate the environment in isolation.
4. Test retry, resume, output paths, missing PDFs and partial downloads.
5. Preserve metadata provenance and confirm rights for each collection.

## Historical command interface

The following flags describe the legacy implementation, not an endorsement to use it for current bulk retrieval:

```text
pubmed_central.py <PMIDs or source JSON>
-o, --output-dir
--resume
--retry
```

Source JSON consists of records with a numeric `pmid` field. The current output directory is assembled by string concatenation, so custom paths require review, including a trailing directory separator.

Publication search is configured in the script and invoked with `python pubmed_search.py`; it is not a general query CLI.

## Attribution and licensing

Author credited by the existing project documentation: Timothy Balch, [CodeBalch25](https://github.com/CodeBalch25).

Preserve attribution and verify licensing of the source and retrieved publications before reuse. This documentation update does not grant new license rights.
