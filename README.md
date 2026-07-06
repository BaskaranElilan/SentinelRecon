# SentinelRecon

SentinelRecon is a Python-based toolkit for information gathering and reconnaissance. It provides an interactive CLI and a large collection of modules for DNS, network, web application, and threat-intelligence checks.

## Legal Disclaimer

This tool is intended for educational and ethical use only. The author is not liable for illegal use or misuse of this tool. Users are solely responsible for their actions and must ensure they have explicit permission to scan target systems.

## Repository

GitHub: [BaskaranElilan/SentinelRecon](https://github.com/BaskaranElilan/SentinelRecon)

## Branding Assets

Logo and screenshot URLs can be added after upload.

Suggested paths:

```text
assets/logo.png
assets/screenshot-cli.png
assets/screenshot-modules.png
```

## Installation

### Run directly

```bash
git clone https://github.com/BaskaranElilan/SentinelRecon.git
cd SentinelRecon
pip install -r requirements.txt
python -m sentinelrecon
```

### Editable install

```bash
pip install -e .
sentinelrecon
```

### Full Linux install

```bash
git clone https://github.com/BaskaranElilan/SentinelRecon.git
cd SentinelRecon
chmod +x install.sh
sudo ./install.sh
sentinelrecon
```

### Docker

```bash
git clone https://github.com/BaskaranElilan/SentinelRecon.git
cd SentinelRecon
docker build -t sentinel-recon:latest .
docker run -it --rm -v $(pwd)/results:/app/results sentinel-recon:latest
```

## Usage

Launch SentinelRecon:

```bash
sentinelrecon

# or run from the source folder
python -m sentinelrecon
```

Browse modules:

```text
sentinelrecon> modules
```

Select a module:

```text
sentinelrecon> use 1
```

Set target and options:

```text
sentinelrecon> set target example.com
sentinelrecon> set threads 10
```

Run the selected module:

```text
sentinelrecon> run
```

## Commands

| Command | Category | Description | Example |
|---------|----------|-------------|---------|
| `modules` | Discovery | List all modules | `modules` |
| `modules -d` | Discovery | List modules with details | `modules -d` |
| `search` | Discovery | Search by keyword | `search ssl` |
| `use` | Selection | Select module | `use 42` |
| `helpmod` | Help | Module help | `helpmod 42` |
| `set target` | Config | Set target | `set target example.com` |
| `set` | Config | Set options | `set threads 20` |
| `unset` | Config | Unset options | `unset target` |
| `opts` | Config | Show options | `opts` |
| `scope` | Config | Show config | `scope` |
| `profile` | Config | Apply profile | `profile speed` |
| `run` | Execute | Run selected module | `run` |
| `runall` | Execute | Run a category | `runall infra` |
| `runfav` | Execute | Run favorite modules | `runfav` |
| `last` | Execute | Re-run last module | `last` |
| `fav` | Favorites | Manage favorites | `fav add 42` |
| `show modules` | Info | Browse modules | `show modules` |
| `show api_status` | Info | Check API configuration | `show api_status` |
| `info` | Info | Project info | `info` |
| `recent` | Info | Recent modules | `recent` |
| `viewout` | Output | View cached output | `viewout` |
| `grepout` | Output | Search output | `grepout "192.168"` |
| `clear` | Utility | Clear screen | `clear` |
| `banner` | Utility | Show banner | `banner` |
| `reset` | Utility | Reset config | `reset` |
| `exit` | Utility | Exit SentinelRecon | `exit` |
| `quit` | Utility | Exit SentinelRecon | `quit` |
| `help` | Help | Show help | `help` |

## Modules

SentinelRecon includes 135 reconnaissance modules across:

- Network and infrastructure analysis
- Web application analysis
- Security and threat intelligence

Use the interactive CLI to browse the full catalog:

```text
sentinelrecon> modules
sentinelrecon> modules -d
sentinelrecon> search dns
```

## API Keys

Some modules support external APIs. Configure them as environment variables:

```bash
export VIRUSTOTAL_API_KEY="your_key_here"
export SHODAN_API_KEY="your_key_here"
export CENSYS_API_ID="your_id_here"
export CENSYS_API_SECRET="your_secret_here"
export GOOGLE_API_KEY="your_key_here"
export HIBP_API_KEY="your_key_here"
```

Check API status:

```text
sentinelrecon> show api_status
```

## Development

```bash
pip install -e ".[dev]"
python -m sentinelrecon
```

Build package:

```bash
python -m build
```

## License

This project is released under the MIT License. See [LICENSE](LICENSE).
