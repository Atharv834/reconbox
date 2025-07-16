# 🧰 ReconBox-Full

> **All-in-one Dockerized Reconnaissance Toolkit** — Everything you need for web reconnaissance, bug bounty, and red teaming, pre-installed in one container. No setup headaches. No dependency issues. Just pull and run.

---

## 🚀 Features

✅ Pre-installed **APT-based tools** (nmap, ffuf, gobuster, sqlmap, etc.)
✅ Pre-installed **Go-based recon tools** (subfinder, httpx, nuclei, etc.)
✅ Comes with **KXSS, GF-Patterns, WaybackURLs**, and more
✅ Uses `tee` to log results on-the-fly during scans
✅ All tools ready to use — **No extra installation or setup needed**
✅ Just mount your working directory and you're ready to go

---
## 🚀 Quick Start (No Local Setup Needed!)

Before using:


# Install Docker (if not already installed)
```bash
sudo apt-get install docker.io
```
# Pull the prebuilt image
```bash
docker pull lordofheaven/reconbox-full
```

## 🧩 Included Tools and Usage

### 📦 APT-Based Tools

| Tool               | Purpose                           | Docker Usage Example                                                                                                                        |
| ------------------ | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **nmap**           | Port scanning / service discovery | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full nmap -Pn example.com`                                                             |
| **ffuf**           | Fuzzing / Directory brute-force   | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full ffuf -u https://site.com/FUZZ -w /data/wordlist.txt \| tee /data/ffuf.txt`        |
| **gobuster**       | Directory and DNS enumeration     | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full gobuster dir -u https://site.com -w /data/wordlist.txt \| tee /data/gobuster.txt` |
| **sqlmap**         | SQLi exploitation                 | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full sqlmap -u 'https://site.com?id=1' --batch \| tee /data/sqlmap.txt`                |
| **dnsutils (dig)** | DNS resolution                    | `docker run --rm lordofheaven/reconbox-full dig example.com`                                                                                |
| **jq**             | JSON parsing                      | `docker run -it -v $PWD:/data lordofheaven/reconbox-full jq '.' /data/file.json`                                                            |
| **ping**           | ICMP ping                         | `docker run -it lordofheaven/reconbox-full ping example.com`                                                                                |
| **awscli**         | S3 bucket checks, AWS tools       | `docker run -it lordofheaven/reconbox-full aws s3 ls s3://bucket-name`                                                                      |

---

### 🦫 Go-Based Tools

| Tool            | Purpose                                    | Docker Usage Example                                                                                          |
| --------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------- |
| **subfinder**   | Passive subdomain enumeration              | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full subfinder -d example.com \| tee /data/subs.txt`     |
| **httpx**       | HTTP probing                               | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full httpx -l /data/subs.txt \| tee /data/httpx.txt`     |
| **nuclei**      | Vulnerability scanning                     | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full nuclei -l /data/httpx.txt \| tee /data/nuclei.txt`  |
| **katana**      | Web crawler                                | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full katana -u https://site.com \| tee /data/katana.txt` |
| **dnsx**        | Subdomain DNS resolution                   | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full dnsx -l /data/subs.txt \| tee /data/dnsx.txt`       |
| **naabu**       | Fast port scanning                         | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full naabu -l /data/subs.txt \| tee /data/ports.txt`     |
| **assetfinder** | Subdomain enumeration (alternative)        | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full assetfinder example.com \| tee /data/asset.txt`     |
| **waybackurls** | Fetch archived URLs                        | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full waybackurls example.com \| tee /data/wayback.txt`   |
| **kxss**        | Reflected XSS discovery                    | `docker run --rm -v $PWD:/data lordofheaven/reconbox-full kxss < /data/urls.txt \| tee /data/kxss.txt`        |
| **gf**          | Pattern-based URL grep (xss, lfi, ssrf...) | `docker run -it -v $PWD:/data lordofheaven/reconbox-full bash` → `gf xss /data/urls.txt \| tee /data/xss.txt` |

---

## 💡 Example Workflow

```bash
# 1. Find subdomains
subfinder -d target.com | tee /data/subs.txt

# 2. Probe for live domains
httpx -l /data/subs.txt | tee /data/httpx.txt

# 3. Run vulnerability scan
nuclei -l /data/httpx.txt | tee /data/nuclei.txt

# 4. Crawl and extract links
katana -u https://target.com | tee /data/katana.txt

# 5. Check for XSS patterns
cat /data/katana.txt | kxss | tee /data/kxss.txt
```

---

## 📦 Docker Image

📍 **Image**: `lordofheaven/reconbox-full`

No extra configuration required. Just pull the image, mount a working directory, and start recon.

---

## 👨‍💻 Author

Created with ❤️ by **[@lordofheaven](https://github.com/atharv834)**
Toolbox for bug bounty hunters, pentesters, and red teamers.
