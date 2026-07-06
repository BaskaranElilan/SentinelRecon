# SentinelRecon

SentinelRecon is a Python-based information gathering and reconnaissance toolkit with an interactive CLI and a large module catalog for DNS, network, web application, and threat-intelligence checks.

GitHub: [BaskaranElilan/SentinelRecon](https://github.com/BaskaranElilan/SentinelRecon)

## Legal Disclaimer

This tool is intended for educational and ethical use only. Only scan systems you own or have explicit permission to test. The author is not responsible for misuse.

## Quick Start On Kali Linux

Kali blocks direct `pip install` into system Python. Use a virtual environment.

```bash
cd ~/Desktop
git clone https://github.com/BaskaranElilan/SentinelRecon.git
cd SentinelRecon

sudo apt update
sudo apt install -y python3-venv python3-pip

python3 -m venv venv
source venv/bin/activate

python -m pip install --upgrade pip
python -m pip install -r requirements.txt

python -m sentinelrecon
```

When the CLI opens:

```text
sentinelrecon> modules
sentinelrecon> use 20
sentinelrecon> set target example.com
sentinelrecon> run
```

Exit:

```text
sentinelrecon> exit
```

## Important Folder Rule

Run install commands from the project root:

```bash
~/Desktop/SentinelRecon
```

Do not run `pip install -r requirements.txt` from:

```bash
~/Desktop/SentinelRecon/sentinelrecon
```

If you see this error:

```text
Could not open requirements file: [Errno 2] No such file or directory: 'requirements.txt'
```

Fix it:

```bash
cd ~/Desktop/SentinelRecon
source venv/bin/activate
python -m pip install -r requirements.txt
```

## Updating The Project

If you already cloned the repo and something was fixed later:

```bash
cd ~/Desktop/SentinelRecon
git pull
source venv/bin/activate
python -m pip install -r requirements.txt
python -m sentinelrecon
```

Use this after seeing errors that were fixed in newer commits, such as `cmd2` parser compatibility errors.

## Kali Error: externally-managed-environment

If you run:

```bash
pip install -r requirements.txt
```

and get:

```text
error: externally-managed-environment
```

That is normal on Kali. Use a virtual environment:

```bash
cd ~/Desktop/SentinelRecon
python3 -m venv venv
source venv/bin/activate
python -m pip install -r requirements.txt
```

Do not use `--break-system-packages` unless you understand the risk.

## Run On Windows Without Docker

Open PowerShell:

```powershell
cd "G:\Cybersecurity Projects\Argus"
python -m venv venv
.\venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m sentinelrecon
```

If PowerShell blocks activation:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
.\venv\Scripts\Activate.ps1
```

## Run With Docker

Build:

```bash
docker build -t sentinel-recon:latest .
```

Run interactively:

```bash
docker run -it --rm sentinel-recon:latest
```

Save results to your current folder:

```bash
mkdir -p results
docker run -it --rm -v "$(pwd)/results:/app/results" sentinel-recon:latest
```

On Windows PowerShell:

```powershell
mkdir results
docker run -it --rm -v "${PWD}\results:/app/results" sentinel-recon:latest
```

## Run With Docker Compose

Use `docker compose run`, not only the Docker Desktop Start button:

```bash
docker compose run --rm sentinelrecon
```

On Windows PowerShell:

```powershell
docker compose run --rm sentinelrecon
```

## Docker Desktop Notes

If Docker Desktop shows a container that exits immediately, run the app from a terminal instead:

```bash
docker run -it --rm sentinel-recon:latest
```

The `-it` is required because SentinelRecon is an interactive CLI.

If Docker Desktop logs show:

```text
Usage: __main__.py [-h]
```

rebuild the latest image:

```bash
docker build -t sentinel-recon:latest .
```

If Docker Desktop Build History shows another name such as an old folder name, that is only Docker Desktop history metadata. The real image name is:

```text
sentinel-recon:latest
```

Check:

```bash
docker images sentinel-recon
```

## Common Errors And Fixes

### `requirements.txt` not found

You are in the wrong folder.

```bash
cd ~/Desktop/SentinelRecon
python -m pip install -r requirements.txt
```

### `The parser must be an instance of Cmd2ArgumentParser`

Update the repo:

```bash
cd ~/Desktop/SentinelRecon
git pull
source venv/bin/activate
python -m sentinelrecon
```

### Docker container exits after showing the banner

You started it without an interactive terminal. Use:

```bash
docker run -it --rm sentinel-recon:latest
```

### `TERM environment variable not set`

This can appear when input is piped or when Docker Desktop logs are not attached to a real terminal. Run with:

```bash
docker run -it --rm sentinel-recon:latest
```

### Docker build cannot find `requirements.txt`

Make sure your `.dockerignore` allows `requirements.txt`, then rebuild:

```bash
docker build -t sentinel-recon:latest .
```

## Tool List

SentinelRecon includes 134 tools across three categories.

### Network & Infrastructure

| ID | Tool | Description | Input |
|---:|---|---|---|
| 1 | Associated Hosts | Reverse host lookup to list domains sharing an IP. | Domain/IP |
| 2 | DNS Over HTTPS | Resolve DNS records via encrypted DoH endpoints. | Domain |
| 3 | DNS Records | Enumerate standard DNS RRsets (A, AAAA, MX, NS, etc.). | Domain |
| 4 | DNSSEC Check | Detect and validate DNSSEC configuration. | Domain |
| 5 | Domain Info | Registrar, creation/expiry, and zone metadata. | Domain |
| 6 | Domain Reputation Check | Aggregate trustworthiness indicators from reputation sources. | Domain |
| 7 | HTTP/2 and HTTP/3 Support Checker | Detect server support for HTTP/2 and HTTP/3 (QUIC). | Domain/URL |
| 8 | IP Info | Geo, ASN, and ownership info for target IPs. | IP/Domain |
| 9 | Open Ports Scan | TCP port scan to identify exposed services. | IP/Domain |
| 10 | Server Info | Gather server banners, stack hints, and versions. | Domain/URL |
| 11 | Server Location | Approximate server geolocation & hosting provider. | Domain/IP |
| 12 | SSL Chain Analysis | Retrieve cert chain; validate trust path & intermediates. | Domain/Host:Port |
| 13 | SSL Expiry Alert | Check certificate expiration window; warn when near expiry. | Domain/Host:Port |
| 14 | TLS Cipher Suites | Enumerate supported TLS cipher suites. | Domain/Host:Port |
| 15 | TLS Handshake Simulation | Simulate varied TLS client handshakes; flag issues. | Domain/Host:Port |
| 16 | Traceroute | Trace network hops to the destination. | Domain/IP |
| 17 | TXT Records | Retrieve TXT records (SPF, DKIM, verification tokens). | Domain |
| 18 | WHOIS Lookup | WHOIS/RDAP ownership data retrieval. | Domain/IP |
| 19 | Zone Transfer | Attempt AXFR to enumerate full DNS zone when misconfigured. | Domain |
| 20 | ASN Lookup | Map IPs/domains to ASNs & network orgs. | Domain/IP |
| 21 | Reverse IP Lookup | Enumerate domains hosted on a given IP. | IP |
| 22 | IP Range Scanner | Scan an IP range for live hosts & open ports. | CIDR/IP |
| 23 | RDAP Lookup | Structured domain/IP ownership via RDAP. | Domain/IP |
| 24 | NTP Information Leak Checker | Query NTP servers for version & info leak data. | IP/Domain |
| 25 | IPv6 Reachability Test | Validate IPv6 DNS + connection reachability vs IPv4. | Domain/IP |
| 26 | BGP Route Analysis | Inspect BGP announcements & paths for anomalies. | ASN/Prefix |
| 27 | CDN Detection | Detect CDN fronting (Cloudflare, Akamai, etc.). | Domain |
| 28 | Reverse DNS Scan | PTR sweeping to discover hostnames. | IP/Range |
| 29 | Network Timezone Detection | Approximate timezone from geo/latency/banner clues. | Domain/IP |
| 30 | Geo-DNS Footprint | Compare DNS answers across global resolvers; map geo/ASN variance. | Domain |
| 31 | SPF Network Extractor | Parse SPF includes/mx/a; expand & extract sending netblocks. | Domain/Email |
| 32 | NS Geo/ASN Diversity Analyzer | Assess authoritative NS geo & ASN concentration. | Domain |
| 33 | DNS SLA Latency Monitor | Measure resolver latency & SLA metrics; flag slow responders. | Domain |
| 34 | RPKI Route Validity Check | Validate route origins for target prefixes against RPKI VRPs. | Domain/IP |
| 35 | Recursive Nameserver Leak Test | Detect recursion enabled on authoritative nameservers. | Domain |
| 36 | Dual-Stack Behavior Profiler | Compare HTTP/TLS responses over IPv4 vs IPv6; flag diffs. | Domain |
| 37 | ICMP Reachability Matrix | Ping sweep; build loss/latency matrix; detect filtering. | Domain/IP/CIDR |
| 38 | IP Allocation History Tracker | Historical IP allocation & ownership timeline. | IP/Domain |
| 39 | Autonomous Neighbor Peering Map | Map upstream/downstream AS adjacencies. | ASN/Domain |
| 40 | TLS Session Resumption Map | Probe TLS session resumption across hosts. | Domain/IP/CIDR |
| 41 | Network Certificate Inventory | Collect certs across network; dedupe; list SANs & expiries. | Domain/IP/CIDR |
| 42 | SSH Banner & Key Fingerprinter | Grab SSH banners & fingerprints across hosts/ports. | Domain/IP/CIDR |
| 43 | SNMP Public Community Checker | Test SNMP v2c communities for info leakage. | Domain/IP/CIDR |
| 44 | UDP Service Sampler | Lightweight probes to classify common UDP services. | Domain/IP/CIDR |

### Web Application Analysis

| ID | Tool | Description | Input |
|---:|---|---|---|
| 45 | Archive History | Retrieve historical site snapshots. | Domain/URL |
| 46 | Broken Links Detection | Crawl site & detect broken links. | Domain/URL |
| 47 | Carbon Footprint | Estimate environmental impact of page loads. | Domain/URL |
| 48 | CMS Detection | Identify CMS platforms by signature. | Domain/URL |
| 49 | Cookies Analyzer | Inspect cookies for security/privacy attributes. | Domain/URL |
| 50 | Content Discovery | Discover hidden directories/files/endpoints. | Domain/URL |
| 51 | Crawler | Crawl site & map structure. | Domain/URL |
| 52 | Robots.txt Analyzer | Parse robots.txt for hidden/disallowed paths. | Domain/URL |
| 53 | Directory Finder | Scan for common unlisted directories. | Domain/URL |
| 54 | Email Harvesting | Extract emails from site pages. | Domain/URL |
| 55 | Performance Monitoring | Measure response time & load performance. | Domain/URL |
| 56 | Quality Metrics | Assess site UX/content quality heuristics. | Domain/URL |
| 57 | Redirect Chain | Follow redirects; analyze safety & loops. | URL |
| 58 | Sitemap Parsing | Parse sitemap.xml; enumerate URLs. | Domain/URL |
| 59 | Social Media Presence Scan | Identify linked social media profiles. | Domain/URL |
| 60 | Technology Stack Detection | Fingerprint technologies & frameworks in use. | Domain/URL |
| 61 | Third-Party Integrations | Discover external services integrated into site. | Domain/URL |
| 62 | JavaScript File Analyzer | Extract endpoints & secrets from JS files. | Domain/URL |
| 63 | CORS Misconfiguration Scanner | Detect overly permissive CORS settings. | Domain/URL |
| 64 | Login Page Brute Identifier | Locate & fingerprint login/auth pages. | Domain/URL |
| 65 | Hidden Parameter Discovery | Fuzz hidden GET/POST parameters. | Domain/URL |
| 66 | Clickjacking Test | Check anti-framing headers & behavior. | Domain/URL |
| 67 | Form Grabber | Enumerate forms & field metadata. | Domain/URL |
| 68 | Favicon Hashing | MD5 hash favicon to infer technologies. | Domain/URL |
| 69 | HTML Comments Extractor | Parse HTML comments for hidden notes/secrets. | Domain/URL |
| 70 | CAPTCHA Presence Checker | Detect CAPTCHA widgets across pages. | Domain/URL |
| 71 | JavaScript Obfuscation Detector | Highlight obfuscated or packed JS. | Domain/URL |
| 72 | Virtual Host Fuzzer | Host header brute to reveal hidden vhosts. | Domain |
| 73 | Session Cookie Lifetime Checker | Measure session cookie longevity. | Domain/URL |
| 74 | HTML5 Feature Abuse Detector | Spot risky HTML5 API usage. | Domain/URL |
| 75 | Autocomplete Vulnerability Checker | Detect sensitive fields with autocomplete enabled. | Domain/URL |
| 76 | Embedded Object Hunter | Find embedded PDFs/SWF/objects. | Domain/URL |
| 77 | Multi-Language URL Tester | Probe language/locale path handling. | Domain/URL |
| 78 | Pixel Tracker Finder | Detect tracking pixel beacons. | Domain/URL |
| 79 | SEO Abuse Detector | Spot hidden/abusive SEO content. | Domain/URL |
| 80 | Dependency JS/CDN Scanner | Inventory external JS libs & versions. | Domain/URL |
| 81 | WebSocket Endpoint Sniffer | Discover ws:// / wss:// endpoints. | Domain/URL |
| 82 | API Schema Grabber | Attempt to fetch OpenAPI/Swagger schemas. | Domain/URL |
| 83 | Lazy-Load Resource Finder | Detect resources loaded dynamically (scroll/JS). | Domain/URL |
| 84 | HTTP Method Enumerator | Crawl & test supported HTTP verbs per URL. | Domain/URL |
| 85 | GraphQL Introspection Probe | Discover GraphQL endpoints; attempt schema introspection. | Domain/URL |
| 86 | File Upload Surface Finder | Crawl & detect file upload forms/JS hints. | Domain/URL |
| 87 | DOM Sink Scanner | Scan HTML/JS for XSS sinks (eval, innerHTML, etc.). | Domain/URL |
| 88 | Cache Behavior Analyzer | Compare caching behavior; detect poisoning risks. | Domain/URL |
| 89 | Cookie Scope Diff Across Subdomains | Aggregate Set-Cookie across crawl; scope & flag analysis. | Domain/URL |
| 90 | CSP Deep Analyzer | Collect & parse CSP headers; risk scoring. | Domain/URL |
| 91 | Third-Party Script Risk Profiler | Inventory external script hosts; categorize & score. | Domain/URL |
| 92 | Static Asset Fingerprinter | Hash JS/CSS; extract library versions; flag outdated. | Domain/URL |

### Security & Threat Intelligence

| ID | Tool | Description | Input |
|---:|---|---|---|
| 93 | Censys Reconnaissance | Enumerate exposed assets via Censys (API). | Domain/IP |
| 94 | Certificate Authority Recon | Examine CA issuance & trust relationships. | Domain |
| 95 | Data Leak Detection | Check for public data leaks & sensitive exposures. | Domain |
| 96 | Exposed Environment Files Checker | Detect exposed .env/config files. | Domain/URL |
| 97 | Firewall Detection | Identify firewall/WAF presence heuristically. | Domain/IP |
| 98 | Global Ranking | Retrieve global popularity ranking metrics. | Domain |
| 99 | HTTP Headers | Extract HTTP response headers. | Domain/URL |
| 100 | HTTP Security Features | Evaluate security headers (HSTS, CSP, etc.). | Domain/URL |
| 101 | Malware & Phishing Check | Check blocklists for malware/phishing indicators. | Domain/URL |
| 102 | Pastebin Monitoring | Search paste sites for leaked data mentions. | Domain |
| 103 | Privacy & GDPR Compliance | Basic privacy/GDPR checks (policies, consent). | Domain/URL |
| 104 | Security.txt Check | Retrieve & parse security.txt disclosure info. | Domain |
| 105 | Shodan Reconnaissance | Query Shodan for exposed services & vulns. | Domain/IP |
| 106 | SSL Labs Report | Pull detailed SSL Labs TLS assessment. | Domain |
| 107 | SSL Pinning Check | Check for SSL/TLS pinning indicators. | Domain/URL |
| 108 | Subdomain Enumeration | Discover subdomains via multiple techniques. | Domain |
| 109 | Subdomain Takeover | Test for dangling DNS entries vulnerable to takeover. | Domain |
| 110 | VirusTotal Scan | Lookup reputation & detections in VirusTotal. | Domain/IP/URL |
| 111 | CT Log Query | Query certificate transparency logs for issued certs. | Domain |
| 112 | Breached Credentials Lookup | Check breach datasets for exposed credentials. | Domain/Email |
| 113 | Cloud Bucket Exposure | Detect open S3/Azure/GCP buckets tied to domain. | Domain |
| 114 | JWT Token Analyzer | Decode and inspect JWT algorithms & claims. | Token/String |
| 115 | Exposed API Endpoints | Crawl and list publicly reachable API endpoints. | Domain/URL |
| 116 | Git Repository Exposure Check | Detect exposed .git directories and artifacts. | Domain/URL |
| 117 | Typosquat Domain Checker | Generate and check typo variants for malicious domains. | Domain |
| 118 | SPF / DKIM / DMARC Validator | Assess email auth posture and alignment. | Domain/Email |
| 119 | Open Redirect Finder | Probe redirect parameters for open redirect vulnerabilities. | Domain/URL |
| 120 | Rate-Limit & WAF Bypass Test | Probe throttling and WAF bypass behaviors. | Domain/URL |
| 121 | Security Changelog Diff | Compare security header/config changes over time. | Domain/URL |
| 122 | Session Hijacking (Passive) | Analyze cookie/session flags for hijacking risk. | Domain/URL |
| 123 | Rogue Certificate Check | Detect suspicious or duplicate certificates. | Domain |
| 124 | JS Malware Scanner | Heuristic scan of JavaScript for malware indicators. | Domain/URL |
| 125 | Cloud Service Enumeration | Detect exposed cloud/devops services (Jira, Jenkins, etc.). | Domain |
| 126 | Rogue Subdomain Resolver | Monitor for newly resolving previously dead subdomains. | Domain |
| 127 | Bug Bounty Program Finder | Identify bug bounty/disclosure program links. | Domain |
| 128 | Custom Wordlist Generator | Build tailored recon wordlists (paths, usernames, emails). | Domain |
| 129 | Threat Feed Correlator | Aggregate multi-feed reputation & threat intelligence. | Domain/IP |
| 130 | Attack Surface Delta | Diff two SentinelRecon reports; highlight adds/removals. | Target Label |
| 131 | Passive CVE Mapper | Map discovered product/version hints to NVD CVEs. | Domain/URL |
| 132 | Security Contact Gap Finder | Collect security contacts from security.txt, WHOIS, site. | Domain |
| 133 | Domain Shadowing Detector | CT + passive DNS to spot high-entropy subdomain bursts. | Domain |
| 134 | IP Reputation Trending | Compare AbuseIPDB & VT metrics across time windows. | Domain/IP/CIDR |

## CLI Commands

| Command | Description |
|---|---|
| `modules` | List available modules |
| `modules -d` | List modules with details |
| `search dns` | Search modules |
| `use 20` | Select a module by ID |
| `set target example.com` | Set target |
| `set threads 10` | Set thread count |
| `opts` | Show selected module options |
| `run` | Run selected module |
| `run 20` | Run module ID 20 |
| `runall infrastructure` | Run infrastructure category |
| `show api_status` | Show API key status |
| `help` | Show CLI help |
| `exit` | Exit SentinelRecon |

## API Keys

Some modules work better with API keys:

```bash
export VIRUSTOTAL_API_KEY="your_key_here"
export SHODAN_API_KEY="your_key_here"
export CENSYS_API_ID="your_id_here"
export CENSYS_API_SECRET="your_secret_here"
export GOOGLE_API_KEY="your_key_here"
export HIBP_API_KEY="your_key_here"
```

Then:

```bash
python -m sentinelrecon
```

Inside the CLI:

```text
sentinelrecon> show api_status
```

## Developer Commands

```bash
python -m compileall sentinelrecon
python -m build
```

## License

This project is released under the MIT License. See [LICENSE](LICENSE).
