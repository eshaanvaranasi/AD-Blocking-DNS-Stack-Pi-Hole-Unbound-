# 🔐 AWS-Hosted DNS Stack with Pi-hole + Unbound

    A secure, recursive DNS filtering stack hosted on AWS EC2 using Docker Compose. Features include ad/tracker blocking, DNSSEC, 
    DNS-over-TLS, DNS-over-HTTPS (DoH), and strict network controls. Built for speed, privacy, and resiliency.

## 🗂️ Features

    📦 Pi-hole for ad and tracker blocking

    🔁 Unbound as a recursive resolver (no third-party DNS)

    🔐 DNSSEC and DNS-over-TLS support

    🔒 Optional native DoH (via Unbound or CloudFlare)

    🧩 Docker Compose for orchestration

    ☁️ AWS EC2 deployment with custom VPC, subnet, and hardened security groups

    🧪 Health checks, dig diagnostics, and client-side DoH browser setup

    🎯 Minimal resource use (~150MB RAM on t2.micro)

## 🖼️ Architecture

Client → (DoH / plain DNS) → EC2 Elastic IP:53/443
          → Pi-hole (port 53) → Unbound (port 53 or DoH) → Root DNS
---

## 🚀 Deployment

```bash
git clone https://github.com/YOUR_USERNAME/aws-dns-stack.git
cd aws-dns-stack

1. Launch EC2 Instance

    Ubuntu 22.04

    Instance type: t2.micro

    Custom VPC and subnet (e.g., 172.31.80.0/20)

    Associate Elastic IP

    Open ports 22, 53 (TCP+UDP), and optionally 443
2. Install Docker and Docker Compose

   sudo apt update && sudo apt install -y docker.io docker-compose

3. File Structure
.
├── docker-compose.yml
├── unbound/
│   ├── unbound.conf
│   └── certs/
│       ├── doh.pem
│       └── doh.key
├── unboundforward-records.conf (optional)
└── pihole-data/
--
🧪 Test Commands
Check Unbound:

docker exec unbound drill @127.0.0.1 -p 53 NS .

Check Pi-hole:

docker exec pihole dig @172.23.0.8 -p 53 google.com +short

Check DoH:

curl -H 'accept: application/dns-json' \
  'https://your.domain.com/dns-query?name=example.com&type=A'


