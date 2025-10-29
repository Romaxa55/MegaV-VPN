# Configuration Guide

## Basic Configuration

Default config location: `~/.config/megav/config.json`

### Minimal Config

```json
{
  "server": "auto",
  "protocol": "vless",
  "encryption": "aes-256-gcm"
}
```

### Full Config

```json
{
  "server": "us-west-1.megav.app",
  "protocol": "vless",
  "transport": "tcp",
  "encryption": "aes-256-gcm",
  "tls": {
    "enabled": true,
    "version": "1.3",
    "sni": "cloudflare.com"
  },
  "routing": {
    "mode": "rule",
    "rules": [
      {
        "type": "direct",
        "domains": ["localhost", "*.local"]
      },
      {
        "type": "proxy",
        "domains": ["*"]
      }
    ]
  },
  "dns": {
    "servers": ["1.1.1.1", "8.8.8.8"],
    "doh": true
  },
  "advanced": {
    "mux": true,
    "mux_concurrency": 8,
    "buffer_size": 512,
    "keepalive": 30
  }
}
```

## Transport Options

### TCP (Default, Fastest)

```json
{
  "transport": "tcp",
  "tls": {
    "enabled": true,
    "version": "1.3"
  }
}
```

### WebSocket (Best Compatibility)

```json
{
  "transport": "ws",
  "ws": {
    "path": "/websocket",
    "headers": {
      "Host": "cloudflare.com"
    }
  }
}
```

### gRPC (Looks Like Microservices)

```json
{
  "transport": "grpc",
  "grpc": {
    "serviceName": "GunService"
  }
}
```

## Routing Rules

### Split Tunneling

```json
{
  "routing": {
    "mode": "rule",
    "rules": [
      {
        "type": "direct",
        "domains": ["*.local", "192.168.*", "10.*"]
      },
      {
        "type": "direct",
        "geoip": ["private"]
      },
      {
        "type": "proxy",
        "domains": ["*"]
      }
    ]
  }
}
```

### China Routing

```json
{
  "routing": {
    "mode": "rule",
    "rules": [
      {
        "type": "direct",
        "geoip": ["cn"]
      },
      {
        "type": "proxy",
        "domains": ["google.com", "youtube.com", "twitter.com"]
      }
    ]
  }
}
```

## DNS Configuration

### DNS over HTTPS

```json
{
  "dns": {
    "servers": [
      "https://1.1.1.1/dns-query",
      "https://8.8.8.8/dns-query"
    ]
  }
}
```

### Custom DNS Rules

```json
{
  "dns": {
    "servers": [
      {
        "address": "1.1.1.1",
        "domains": ["*"]
      },
      {
        "address": "119.29.29.29",
        "domains": ["*.cn"]
      }
    ]
  }
}
```

## Performance Tuning

### Maximum Speed

```json
{
  "advanced": {
    "mux": false,
    "buffer_size": 2048,
    "congestion_control": "bbr",
    "tcp_fast_open": true
  }
}
```

### Battery Saving (Mobile)

```json
{
  "advanced": {
    "mux": true,
    "mux_concurrency": 4,
    "buffer_size": 128,
    "keepalive": 60
  }
}
```

## Environment Variables

```bash
# Config file location
export MEGAV_CONFIG="/path/to/config.json"

# Log level (debug, info, warn, error)
export MEGAV_LOG_LEVEL="info"

# Data directory
export MEGAV_DATA_DIR="~/.config/megav"
```

## CLI Override

```bash
# Override server
megav connect --server us-west-1.megav.app

# Override transport
megav connect --transport ws

# Override routing mode
megav connect --routing bypass-cn
```

## Presets

### Preset: Maximum Privacy

```bash
megav connect --preset privacy
```

Enables:
- No logs
- DNS leak protection
- IPv6 leak protection
- Kill switch

### Preset: Maximum Speed

```bash
megav connect --preset speed
```

Enables:
- XTLS-Vision
- TCP transport
- BBR congestion control

### Preset: Maximum Compatibility

```bash
megav connect --preset compatibility
```

Enables:
- WebSocket transport
- CDN fronting
- Multiplexing

## Troubleshooting Config

```bash
# Validate config
megav config validate

# Show active config
megav config show

# Reset to defaults
megav config reset
```

