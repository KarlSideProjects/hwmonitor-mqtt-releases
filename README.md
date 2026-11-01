# HWMonitor MQTT Sender

Version **0.1.29** provides Nuitka-compiled installers for Windows x64, Linux x64 and Linux ARM64. This public repository distributes installation packages, installer scripts and documentation. Credentials and configuration stay on your machine.

[Download packages and checksums](https://github.com/KarlSideProjects/hwmonitor-mqtt-releases/releases/tag/v0.1.29). All platforms share the same version and source identity, recorded in `version.json`. Updates install a complete compiled package from this public repository.

Karl’s software is free for noncommercial use. Commercial use, including internal company use, requires Karl’s prior written permission. See [the license](LICENSE-NOTICE.md). Third-party components retain their own terms and notices inside each package. Previously granted GPL rights remain effective.

## Linux

Use 64-bit x64 or ARM64 Linux with glibc 2.31 or later. Bash, curl, jq, tar, sha256sum, runuser, od and flock are required. The standard Linux installation uses Docker Compose v2. Existing PVE detection and its native-service path remain available; a separate PVE installation test is not a release requirement. Run the installer when a Sender restart is acceptable and answer its local MQTT configuration prompts.

```bash
curl --fail --location https://github.com/KarlSideProjects/hwmonitor-mqtt-releases/releases/download/v0.1.29/install.sh --output install.sh
printf '%s  install.sh\n' 'ca35c033d9b131b9ba4571158e672e3ba76a3fe65694740d6d5490b356cc918d' | sha256sum --check -
sudo bash ./install.sh
```

The installer resolves the public latest release and verifies its version, package checksum and compiled executable identity. It refuses unrecognized installation directories and an existing PVE `sys-agent` container; arrange migration using your existing configuration before retrying.

## Windows

Open **64-bit PowerShell as Administrator**. Download and verify the script, then run it and answer the MQTT prompts.

```powershell
Invoke-WebRequest -Uri 'https://github.com/KarlSideProjects/hwmonitor-mqtt-releases/releases/download/v0.1.29/install.ps1' -OutFile '.\install.ps1'
if ((Get-FileHash '.\install.ps1' -Algorithm SHA256).Hash.ToLowerInvariant() -ne '950ba66be56e3423753bc671fed49c0bc02ce89f554eba52a285668307a0c842') { throw 'Installer checksum mismatch' }
Unblock-File '.\install.ps1'
.\install.ps1
```

The installer downloads complete compiled packages from this public repository and checks their version and hashes. Hardware monitoring also needs compatible LibreHardwareMonitor components, drivers and privileges. Successful installation does not establish sensor accuracy on every hardware model.
