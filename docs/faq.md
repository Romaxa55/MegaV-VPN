# Frequently Asked Questions

## General

### What is MegaV VPN?

MegaV VPN is a free, open-source VPN service built on the VLESS protocol. It provides military-grade encryption and works reliably in restrictive networks like China, Russia, and Iran.

### Is it really free?

Yes! MegaV VPN is completely free with:
- Unlimited bandwidth
- No speed throttling
- No connection time limits
- No credit card required

We're funded by donations and optional premium features.

### How is it different from other VPNs?

Traditional VPNs use protocols (OpenVPN, WireGuard) that are easily detected by Deep Packet Inspection. MegaV uses VLESS protocol which:
- Has no protocol signatures
- Looks like regular HTTPS traffic
- Supports CDN fronting
- Achieves 800+ Mbps speeds

[Technical details →](https://megav.hashnode.dev/vless-protocol-technical-deep-dive)

## Privacy & Security

### Do you keep logs?

**No.** We have a strict no-logs policy:
- No connection logs
- No activity logs
- No IP address logs
- No DNS query logs

### What encryption do you use?

- **AES-256-GCM** - Industry standard
- **ChaCha20-Poly1305** - For mobile devices
- **TLS 1.3** - Transport layer
- **Perfect Forward Secrecy**

### Can you see my traffic?

No. All traffic is end-to-end encrypted. Even if someone compromises our servers, they cannot decrypt past sessions (Perfect Forward Secrecy).

### Where are you based?

We're a decentralized organization with no single jurisdiction. Our infrastructure is distributed across privacy-friendly countries.

## Technical

### What is VLESS?

VLESS is a lightweight proxy protocol that:
- Removes unnecessary features from VMess
- Reduces overhead
- Improves performance
- Harder to detect by DPI

### Why not WireGuard?

WireGuard is fast but easily blocked:
- Static header structure
- Predictable traffic patterns
- UDP-based (often blocked)

VLESS uses TCP and looks like HTTPS, making it much harder to block.

### How does CDN fronting work?

Your traffic appears to go to Cloudflare/CloudFront but actually reaches our VPN server:
```
You → [Cloudflare] → Our Server
```
Firewall sees: "User visiting Cloudflare" ✅  
Reality: You're using VPN 🔐

### What's the difference between transports?

| Transport | Speed | Compatibility | Detection Risk |
|-----------|-------|---------------|----------------|
| TCP+XTLS | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| WebSocket | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| gRPC | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

## Usage

### Does it work in China?

Yes! Tested uptime:
- **94%** success rate
- Works on all major ISPs
- Regular updates to bypass new blocks

### Does it work in Russia?

Yes! Especially after the 2024 VPN crackdowns. Most VPNs stopped working, but VLESS-based solutions maintain 90%+ uptime.

### Can I use it on multiple devices?

Yes! One account works on:
- Unlimited devices
- Simultaneous connections
- All platforms

### Can I torrent?

Yes, torrenting is allowed. However:
- Be aware of local laws
- We recommend port forwarding for better speeds
- Some servers are optimized for P2P

### Why is my speed slow?

Try these:

1. Choose nearest server:
```bash
megav servers --sort-by latency
megav connect --region auto
```

2. Use XTLS transport:
```bash
megav connect --transport tcp --xtls
```

3. Disable unnecessary features:
```bash
megav connect --preset speed
```

### Can I use it for Netflix/streaming?

Some servers work with streaming services. Try:
```bash
megav servers --filter streaming
```

Note: Streaming detection bypasses violate ToS of streaming services. Use at your own risk.

## Advanced

### Can I self-host?

Yes! See [VLESS-Configs](https://github.com/Romaxa55/VLESS-Configs) for server configs.

### Can I contribute?

Absolutely! We need:
- Code contributions
- Documentation
- Translations
- Server donations
- Bug reports

See [CONTRIBUTING.md](../CONTRIBUTING.md)

### What about IPv6?

Currently IPv4 only. IPv6 support planned for Q2 2025.

### What about split tunneling?

Yes, supported via routing rules:

```json
{
  "routing": {
    "rules": [
      {"type": "direct", "domains": ["*.local"]},
      {"type": "proxy", "domains": ["*"]}
    ]
  }
}
```

### Can I use my own DNS?

Yes:

```json
{
  "dns": {
    "servers": ["1.1.1.1", "8.8.8.8"]
  }
}
```

### Does it protect against WebRTC leaks?

Yes, when using our browser extension. For desktop app, you need to disable WebRTC manually in browser settings.

## Troubleshooting

### Connection keeps dropping

See [Troubleshooting Guide](troubleshooting.md#connection-drops-frequently)

### Getting blocked after few minutes

Enable CDN fronting:
```bash
megav connect --preset stealth
```

### High battery usage on mobile

Enable battery saving mode:
```bash
megav connect --preset battery-saver
```

## Support

### How do I report a bug?

1. Generate support bundle:
```bash
megav support-bundle
```

2. Open issue on [GitHub](https://github.com/Romaxa55/MegaV-VPN/issues)

### How do I request a feature?

Open a [feature request](https://github.com/Romaxa55/MegaV-VPN/issues/new?template=feature_request.md)

### Where can I get help?

- [GitHub Discussions](https://github.com/Romaxa55/MegaV-VPN/discussions)
- [Telegram Channel](https://t.me/megavvpn)
- [Email Support](mailto:support@megav.app)

## Business

### Can I use it commercially?

Yes, under MIT license. Attribution appreciated but not required.

### Do you offer paid plans?

Currently no. We're exploring:
- Priority support
- Dedicated IPs
- Custom server locations

### Can I donate?

Yes! We accept:
- Bitcoin
- Ethereum
- PayPal
- GitHub Sponsors

[Donate →](https://megav.app/donate)

