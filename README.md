# PubMed Research Scraper Toolkit

Automated Python tools for searching, downloading, and analyzing research publications from PubMed and PubMed Central. Essential toolkit for researchers, data scientists, and bioinformatics professionals.

## Features

- **Automated PDF Download**: Bulk download PDFs from PubMed Central by PM IDs
- **Search & Query**: Advanced search functionality using PubMed API
- **Resume Capability**: Continue interrupted downloads from breakpoint
- **Retry Mechanism**: Automatic retry for failed downloads
- **Proxy Support**: Built-in proxy pool to bypass anti-scraping measures
- **Metadata Extraction**: Extract figures, text, and metadata from PDFs
- **JSON Output**: Structured data export for further analysis

## Tech Stack

- **Language**: Python 3.8+
- **APIs**: PubMed E-utilities, PubMed Central
- **Libraries**: 
  - Requests for HTTP operations
  - BeautifulSoup for HTML parsing
  - JSON for data storage
- **Features**: Web scraping, API integration, file I/O

## Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Setup

1. Clone the repository:
```bash
git clone https://github.com/CodeBalch25/Download-Publications-fro-Pubmed-.git
cd Download-Publications-fro-Pubmed-
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Components

### 1. pubmed_central.py - PDF Downloader

Download PDFs from PubMed Central using PMIDs (PubMed IDs).

**Features:**
- Resume from breakpoint
- Retry failed tasks
- Proxy pool support
- Batch downloading

**Usage:**
```bash
# Download specific PMIDs
python pubmed_central.py 29138661 29123944

# Download from JSON source file
python pubmed_central.py data.json -o ./output

# Resume interrupted download
python pubmed_central.py data.json --resume

# Retry failed downloads
python pubmed_central.py data.json --retry

# Use proxy pool
python pubmed_central.py data.json --use-proxy
```

**Arguments:**
- `-o, --output-dir`: Specify output directory
- `--resume`: Resume from existing lock file
- `--retry`: Retry failed tasks
- `--use-proxy`: Use proxy pool for requests

### 2. pubmed_search.py - Publication Search

Search and retrieve publication metadata from PubMed.

**Usage:**
```python
# Configure search query (modify in script)
query = "machine learning AND healthcare"
max_results = 1000

# Run search
python pubmed_search.py

# Output: data.json with search results
```

**Output Format (data.json):**
```json
[
    {
        "pmid": 29138661,
        "title": "Publication Title",
        "authors": ["Author 1", "Author 2"],
        "journal": "Journal Name",
        "year": 2020,
        "abstract": "Publication abstract..."
    }
]
```

### 3. pubmed_info.py - Metadata Extraction

Extract metadata, figures, and text from downloaded PDFs.

**Features:**
- PDF text extraction
- Figure extraction
- Metadata parsing
- Structured data export

**Status:** Work in Progress (WIP)

## PMID Source File Schema

```json
[
    {
        "pmid": 29138661,
        "title": "Optional title",
        "journal": "Optional journal name"
    },
    {
        "pmid": 29123944
    }
]
```

The `pmid` field is required; other fields are optional and will be ignored during download.

## Advanced Usage Examples

### Example 1: Search and Download Pipeline
```bash
# Step 1: Search for publications
python pubmed_search.py  # Generates data.json

# Step 2: Download PDFs from search results
python pubmed_central.py data.json -o ./research_papers
```

### Example 2: Download with Proxy Rotation
```bash
# For large batches or rate-limited scenarios
python pubmed_central.py data.json --use-proxy --retry
```

### Example 3: Resume After Network Interruption
```bash
# If download was interrupted
python pubmed_central.py data.json --resume
```

## Project Structure

```
Download-Publications-fro-Pubmed-/
├── pubmed_central.py       # PDF downloader
├── pubmed_search.py        # PubMed search tool
├── pubmed_info.py          # Metadata extractor (WIP)
├── pubmed_info.reader.py   # PDF reader utilities
├── requirements.txt        # Python dependencies
└── README.md              # Documentation
```

## Dependencies

```
requests>=2.28.0
beautifulsoup4>=4.11.0
lxml>=4.9.0
PyPDF2>=3.0.0
```

## Use Cases

1. **Literature Review**: Download hundreds of papers for systematic review
2. **Meta-Analysis**: Collect publications for quantitative analysis
3. **Research Database**: Build local repository of domain-specific papers
4. **Citation Analysis**: Gather papers for network analysis
5. **Text Mining**: Extract text for NLP and ML projects

## Performance

- **Speed**: Downloads ~100 PDFs per hour (depends on network and PMC server load)
- **Reliability**: Automatic retry mechanism ensures successful downloads
- **Scalability**: Handles thousands of PMIDs efficiently

## Features in Development

- [ ] Support for additional input formats (BibTeX, CSV)
- [ ] Parallel downloading for faster processing
- [ ] Enhanced metadata extraction
- [ ] Full-text search within downloaded papers
- [ ] Export to reference managers (Zotero, Mendeley)
- [ ] Citation network visualization

## API Rate Limits

**PubMed E-utilities Guidelines:**
- Maximum 3 requests per second without API key
- Maximum 10 requests per second with API key
- Use `--use-proxy` for larger batches

## Troubleshooting

**Issue: Download fails with 403 Forbidden**
- Solution: Use `--use-proxy` flag to rotate IP addresses

**Issue: Missing PDFs**
- Some papers may not have free full-text available on PMC
- Check if paper has open access or institutional access

**Issue: Slow downloads**
- PMC server load varies by time of day
- Consider spreading downloads over multiple sessions

## Legal & Ethical Considerations

- Respect publisher copyrights and terms of service
- Use for research and educational purposes only
- Adhere to fair use guidelines
- Do not redistribute copyrighted materials
- Follow PubMed Central usage policies

## Contributing

Contributions are welcome! Submit issues or pull requests.

## License

MIT License

## Author

**Timothy Balch** - [@CodeBalch25](https://github.com/CodeBalch25)

## Acknowledgments

- NCBI for PubMed and PubMed Central APIs
- Python community for excellent libraries
- Bioinformatics research community

## Citations

If you use this toolkit in your research, please cite:
```
@software{pubmed_scraper,
  author = {Balch, Timothy},
  title = {PubMed Research Scraper Toolkit},
  year = {2020},
  url = {https://github.com/CodeBalch25/Download-Publications-fro-Pubmed-}
}
```

## Tags

`web-scraping` `bioinformatics` `python` `research-tools` `pubmed` `data-science` `automation` `pdf-extraction` `literature-review` `academic-research`
