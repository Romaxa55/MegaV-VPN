# Troubleshooting

## Connection Issues

### Can't Connect to Server

**Symptoms:** Connection timeout, "No route to host"

**Solutions:**

1. Check internet connection:
```bash
ping 1.1.1.1
```

2. Test DNS resolution:
```bash
nslookup megav.app
```

3. Try different transport:
```bash
megav connect --transport ws  # Try WebSocket
megav connect --transport grpc  # Try gRPC
```

4. Check firewall:
```bash
# Linux
sudo ufw status
sudo ufw allow 443/tcp

# macOS
sudo pfctl -sr

# Windows
Get-NetFirewallRule | Where DisplayName -like "*MegaV*"
```

### Connection Drops Frequently

**Solutions:**

1. Enable keepalive:
```json
{
  "advanced": {
    "keepalive": 30
  }
}
```

2. Try different server:
```bash
megav servers --sort-by latency
megav connect --server [lowest-latency]
```

3. Enable multiplexing:
```json
{
  "advanced": {
    "mux": true,
    "mux_concurrency": 8
  }
}
```

## Speed Issues

### Slow Download Speed

1. Test baseline speed:
```bash
megav disconnect
speedtest-cli
```

2. Test VPN speed:
```bash
megav connect
speedtest-cli
```

3. Try XTLS for maximum speed:
```bash
megav connect --transport tcp --xtls
```

4. Reduce encryption overhead:
```json
{
  "encryption": "chacha20-poly1305"  # Faster on mobile
}
```

### High Latency

1. Choose nearest server:
```bash
megav servers --sort-by distance
megav connect --region auto
```

2. Disable unnecessary features:
```json
{
  "advanced": {
    "mux": false,
    "buffer_size": 2048
  }
}
```

## Detection Issues

### VPN Blocked by ISP/Firewall

**Symptoms:** Connection works for few minutes then stops

**Solutions:**

1. Enable CDN fronting:
```json
{
  "tls": {
    "sni": "cloudflare.com"
  },
  "cdn": {
    "enabled": true,
    "domain": "cdn.cloudflare.net"
  }
}
```

2. Use WebSocket over TLS:
```bash
megav connect --transport ws --tls
```

3. Change port:
```bash
megav connect --port 443  # HTTPS port
megav connect --port 80   # HTTP port
```

### DNS Leaks

Test for leaks:
```bash
megav connect
curl https://1.1.1.1/cdn-cgi/trace
```

Fix:
```json
{
  "dns": {
    "servers": ["1.1.1.1"],
    "leak_protection": true
  }
}
```

## Platform-Specific Issues

### Linux: Permission Denied

```bash
# Add user to megav group
sudo usermod -aG megav $USER

# Or run with sudo
sudo megav connect
```

### macOS: System Extension Blocked

1. Go to System Preferences → Security & Privacy
2. Click "Allow" next to "System software from MegaV was blocked"
3. Restart MegaV

### Windows: TAP Driver Issues

```powershell
# Reinstall TAP driver
cd "C:\Program Files\MegaV"
.\tap-install.exe
```

### Android: Battery Optimization

1. Settings → Apps → MegaV
2. Battery → "Don't optimize"
3. Background restrictions → "Remove restrictions"

## Logs and Diagnostics

### View Logs

```bash
# Real-time logs
megav logs --follow

# Last 100 lines
megav logs --tail 100

# Debug level
megav logs --level debug
```

### Log Locations

- **Linux:** `~/.local/share/megav/logs/`
- **macOS:** `~/Library/Logs/MegaV/`
- **Windows:** `%APPDATA%\MegaV\logs\`
- **Android:** `/sdcard/Android/data/com.megav.vpn/logs/`

### Run Diagnostics

```bash
megav diagnose
```

This will check:
- Network connectivity
- DNS resolution
- Server availability
- Firewall rules
- Config validity

### Generate Support Bundle

```bash
megav support-bundle

# Uploads to: megav.app/support/[random-id]
# Share this ID with support team
```

## Error Messages

### "Certificate verification failed"

**Cause:** System time incorrect

**Fix:**
```bash
# Linux
sudo ntpdate -u pool.ntp.org

# macOS
sudo sntp -sS pool.ntp.org

# Windows
w32tm /resync
```

### "Too many connections"

**Cause:** Multiple instances running

**Fix:**
```bash
megav disconnect --all
pkill megav
megav connect
```

### "Invalid UUID"

**Cause:** Corrupted config or expired credentials

**Fix:**
```bash
megav config reset
megav login
```

## Still Having Issues?

1. Check [FAQ](faq.md)
2. Search [GitHub Issues](https://github.com/Romaxa55/MegaV-VPN/issues)
3. Join our [Telegram](https://t.me/megavvpn)
4. Open new issue with support bundle

