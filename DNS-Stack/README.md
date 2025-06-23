# 🔐 AWS-Hosted DNS Stack with Pi-hole + Unbound

    A secure, recursive DNS filtering stack hosted on AWS EC2 using Docker Compose. Features include ad/tracker blocking, DNSSEC, 
    DNS-over-TLS, DNS-over-HTTPS (DoH), and strict network controls. Built for speed, privacy, and resiliency.

## 🗂️ Features

    📦 Pi-hole for ad and tracker blocking

    🔁 Unbound as a recursive resolver (no third-party DNS)

    🔐 DNSSEC and DNS-over-TLS support

    🔒 Optional native DoH (via Unbound or cloudflared)

    🧩 Docker Compose for orchestration

    ☁️ AWS EC2 deployment with custom VPC, subnet, and hardened security groups

    🧪 Health checks, dig diagnostics, and client-side DoH browser setup

    🎯 Minimal resource use (~150MB RAM on t2.micro)

## 🖼️ Architecture

Client → (DoH / plain DNS) → EC2 Elastic IP:53/443
          → Pi-hole (port 53) → Unbound (port 53 or DoH) → Root DNS
