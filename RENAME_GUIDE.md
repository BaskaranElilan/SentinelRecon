# SentinelRecon Project Checklist

These are the project details now applied to the repo.

## Confirmed Details

- Project name: `SentinelRecon`
- Author: `Elilan Baskaran`
- GitHub repository: `https://github.com/BaskaranElilan/SentinelRecon`
- License: `MIT`
- Python package/distribution name: `sentinel-recon`
- CLI command: `sentinelrecon`
- Docker image: `sentinel-recon:latest`
- Docker container: `sentinel-recon`
- Internal Python package: `sentinelrecon`

The internal package has been fully renamed to `sentinelrecon`:

```python
from sentinelrecon.cli.main import main
python -m sentinelrecon
```

## Branding Already Updated

- `README.md`
- `pyproject.toml`
- `Dockerfile`
- `docker-compose.yml`
- `Makefile`
- `install.sh`
- `uninstall-sentinelrecon.sh`
- `sentinelrecon/cli/logo.py`
- `sentinelrecon/cli/main.py`
- `sentinelrecon/cli/constants.py`
- `sentinelrecon/core/catalog_cache.py`
- `sentinelrecon/core/utils.py`
- `sentinelrecon/config/settings.py`
- `sentinelrecon/config/modules.json`
- `LICENSE`

## Details To Add Later

Add these after you upload your branding assets:

- Logo path or URL: `__________`
- CLI screenshot path or URL: `__________`
- Modules screenshot path or URL: `__________`
- Project website, optional: `__________`
- Contact email, optional: `__________`

Suggested repo paths:

```text
assets/logo.png
assets/screenshot-cli.png
assets/screenshot-modules.png
```

After uploading assets, update the `Branding Assets` section in `README.md`.

## Commands To Use

Run from source:

```bash
python -m sentinelrecon
```

Install editable command:

```bash
pip install -e .
sentinelrecon
```

Docker:

```bash
docker build -t sentinel-recon:latest .
docker run -it --rm sentinel-recon:latest
```

Linux installer:

```bash
chmod +x install.sh
sudo ./install.sh
sentinelrecon
```

## Package Name

```text
sentinelrecon/
```

Use these internal references:

```text
python -m sentinelrecon
import sentinelrecon
from sentinelrecon...
```
