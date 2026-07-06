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
