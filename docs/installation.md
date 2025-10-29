# Installation Guide

## Windows

### Method 1: PowerShell (Recommended)

```powershell
# Run as Administrator
iwr -useb https://megav.app/install-windows.ps1 | iex
```

### Method 2: Manual Download

1. Download [MegaV-VPN-Windows.zip](https://github.com/Romaxa55/MegaV-VPN/releases/latest)
2. Extract to `C:\Program Files\MegaV`
3. Run `install.bat`

## macOS

### Method 1: Homebrew (Recommended)

```bash
brew tap romaxa55/megav
brew install megav-vpn
```

### Method 2: Direct Install

```bash
curl -fsSL https://megav.app/install.sh | sh
```

## Linux

### Ubuntu/Debian

```bash
# Add repository
curl -fsSL https://megav.app/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/megav-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/megav-archive-keyring.gpg] https://apt.megav.app stable main" | sudo tee /etc/apt/sources.list.d/megav.list

# Install
sudo apt update
sudo apt install megav-vpn
```

### Fedora/RHEL

```bash
# Add repository
sudo dnf config-manager --add-repo https://rpm.megav.app/fedora/megav.repo

# Install
sudo dnf install megav-vpn
```

### Arch Linux

```bash
yay -S megav-vpn
```

### Universal Script

```bash
curl -fsSL https://megav.app/install.sh | sh
```

## Android

1. Install from [Google Play](https://play.google.com/store/apps/details?id=com.megav.vpn)
2. Or download APK from [releases](https://github.com/Romaxa55/MegaV-VPN/releases)

## iOS

Install from [App Store](https://apps.apple.com/app/megav-vpn)

## Verification

After installation, verify:

```bash
megav --version
megav test-connection
```

## First Run

```bash
# Connect to nearest server
megav connect

# Choose specific region
megav connect --region us

# List available servers
megav servers
```

## Troubleshooting

### Connection Issues

```bash
# Test connectivity
megav diagnose

# Reset configuration
megav reset

# View logs
megav logs
```

### Firewall Configuration

Allow these ports:
- **443/tcp** - VLESS over TLS
- **80/tcp** - Fallback HTTP

## System Requirements

- **Windows:** 10/11 (64-bit)
- **macOS:** 11.0+
- **Linux:** Kernel 4.4+
- **Android:** 7.0+
- **iOS:** 13.0+

## Next Steps

- [Configuration Guide](configuration.md)
- [FAQ](faq.md)
- [Troubleshooting](troubleshooting.md)

