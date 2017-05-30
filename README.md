# NuGetReflector

This tool mirrors an NuGet repository to another NuGet server. This can be used to clone public repositories or used to make private repositories redundant.

---

# Install

### Needs:

* Python >= 2.7
* Python < 3 
* Pip
* [DotNet CLI](https://github.com/dotnet/cli)

#### Step 1:

Install the DotNet CLI. Instructions can be found on [their repository](https://github.com/dotnet/cli).

#### Step 2:

Locate the `dotnet` binary and make note of the path.

On OS X:

```bash
which dotnet;
# /usr/local/share/dotnet/dotnet
```

On Linux:

It depends on your distro or where you extract the tarball.

On Windows:

Have not tested on Windows.

#### Step 3:

Get the source and configure options.

```shell
cd /opt;
git clone https://github.com/MelonSmasher/NuGetReflector.git;
cd NuGetReflector;
cp config/config.example.yaml config/config.yaml;
vi config/config.yaml; # Fill out your settings, see config options below.
pip install -r requirements.txt;
```

# Config options:

- `remote:`
   - `url:` - remote repo to mirror # Default: https://chocolatey.org/
   - `json_api:` - request json from remote API # Default false

- `local:`
  - `url:` - local repo to host mirror # Default: http://localhost/
  - `json_api:` - request json from local API # Default false
  - `api_key:` - local repo api key # Default: null
  - `package_storage_path:` - Local path to store packages # Default: storage/packages/
  - `dotnet_path:` - Path to dontnet executable # Default: false # Example: /usr/local/share/dotnet/dotnet

- `hash:`
  - `verify_downloads:` - Verify downloaded package hash. You should leave this enabled # Default: true
  - `verify_uploaded:` - Verify package hash after it has been uploaded to the mirror. You should leave this enabled # Default: true

# Usage:

#### Manually

```bash
./reflector.sh;
```

#### Cron Job

Runs every 12 hours:

```bash
0 */12 * * * /opt/NuGetReflector/reflector.sh 2>&1 /opt/NuGetReflector/storage/log/cron.log
```
