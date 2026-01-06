---
name: domain-dns-ops
description: >
  Buy domains on Namecheap and set up Cloudflare DNS programmatically.
---

# Domain/DNS Ops

Use the `domain-ops` CLI tool at `~/code/cj/tools/domain-ops/`.

## Commands

```bash
domain-ops check <domain>     # Check availability + pricing
domain-ops buy <domain>       # Full workflow: buy → CF zone → DNS setup
domain-ops setup-cf <domain>  # Just Cloudflare setup (already own domain)
```

## Environment Setup

```bash
# Namecheap
export NAMECHEAP_API_USER=your_username
export NAMECHEAP_API_KEY=your_api_key
export NAMECHEAP_USERNAME=your_username
export NAMECHEAP_CLIENT_IP=$(curl -s ifconfig.me)
# export NAMECHEAP_SANDBOX=1  # Optional: use sandbox for testing

# Cloudflare
export CLOUDFLARE_API_TOKEN=your_token  # Zone:Edit, DNS:Edit perms
```

## Full Workflow

```bash
# 1. Check domain availability
domain-ops check example.com

# 2. Purchase and set up (interactive)
domain-ops buy example.com
#   → Confirms price
#   → Registers domain
#   → Creates CF zone
#   → Sets nameservers
#   → Prompts for DNS records (A, CNAME, MX, TXT)
```

## API Access Requirements

**Namecheap:**
- $50+ balance OR 20+ domains OR $50+ purchases in 2 years
- Whitelist IP: Profile → Tools → API Access
- Sandbox: https://sandbox.namecheap.com

**Cloudflare:**
- Create token: https://dash.cloudflare.com/profile/api-tokens
- Permissions: Zone:Edit, DNS:Edit (All zones or specific account)

## Build

```bash
cd ~/code/cj/tools/domain-ops
go build
```
