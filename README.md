# 🛡️ XSS Pro Scanner 2050 — Elite Edition

**AI-Powered Next-Gen XSS Detection Framework**  
Built by [Dev Kumar](https://github.com/devkumar-swipe) for elite bug bounty hunting and automated web app security analysis.

![Banner](https://img.shields.io/badge/XSS-Scanner-green?style=for-the-badge)
![Version](https://img.shields.io/badge/version-2050.2--Elite-blue?style=for-the-badge)
![OS](https://img.shields.io/badge/Linux-Kali%2FDebian%20Recommended-critical?style=for-the-badge)

---

## 📌 Features

- 🔍 Reflected, Stored, and DOM-based XSS Detection
- 🧠 Smart FUZZ Payload Injection (query/path/fragment/header-aware)
- 🌐 Full browser support using Playwright (headless Chromium)
- 🕸️ Auto Proxy Rotation with HTTP/SOCKS5 + Verification
- ⚙️ Concurrent Scanning with `--threads` option
- 📂 Multi-URL scanning via `--list urls.txt`
- ♻️ Resume scans from logs with `--continue`
- 📊 Report output in JSON, HTML, or Terminal

---
![image](https://github.com/user-attachments/assets/860afe17-43a3-45d1-a018-9d65489a4bd8)
---

## 🐧 OS Compatibility

> ✅ **Recommended OS:** Kali Linux, Parrot OS, Debian-based Linux  
> ⚠️ MacOS or Windows (WSL) may partially work but are unsupported for Playwright browser injection.

---

## ⚙️ Installation

### 1. Clone the repo

```bash
https://github.com/devkumar-swipe/XSS-Pro-Scanner.git
cd xss-pro-scanner
```
## 2. Install dependencies
```bash
sudo apt update
sudo apt install python3 python3-pip libwebkit2gtk-4.0-dev -y
pip3 install -r requirements.txt
playwright install
```
## 3. Global call
you can run it from anywhere in your terminal by just typing its name. Here’s a simple way to do that:
1. First, make sure the script (xsschamp.py) is executable:
   ```bash
   chmod +x ~/xsschamp.py
   ```
2. Then create a symlink (shortcut) to a directory that’s in your PATH, like /usr/local/bin:
   ```bash
   sudo ln -s ~/xsschamp.py /usr/local/bin/xsschamp
   ```
3. Now, you can run the tool globally by just typing:
   ```bash
   xsschamp
   ```
---

## Usage
🔹 Basic Scan (Single URL)
```bash
python3 xsschamp.py "https://target.com/search?q=FUZZ" --mode active --type reflected
```
🔹 Scan from List
```bash
python3 xsschamp.py --list urls.txt --type all --threads 20 --output final_report.html
```
🔹 Resume Scan (After Interruption)
```bash
python3 xsschamp.py --continue scan_log.json --output resumed_report.json
```
## More Usage 
1. Passive Scan for Information Gathering Only
```bash
xsschamp --mode passive https://example.com/search?q=test
```
   Only gathers information without injecting any payloads.

2. Active Scan for Reflected XSS on URL Parameter
```bash
xsschamp --mode active --type reflected https://example.com/search?q=FUZZ
```
   Actively injects XSS payloads into q parameter in URL.

3. Scan for Stored XSS with POST Data Injection
```bash
xsschamp --mode active --type stored --post "username=admin&comment=FUZZ" https://example.com/comment
```
   Injects payloads into comment POST parameter to find stored XSS.

4. Using Custom Payloads File
```bash
xsschamp --payloads mycustompayloads.txt --mode active https://example.com/search?q=FUZZ
```
   Uses your own payload list instead of defaults.

5. Routing Requests Through Proxies
```bash
xsschamp --proxy socks5.txt --protocol socks5 --mode active https://example.com/search?q=FUZZ
```
   All requests go through SOCKS5 proxies defined in socks5.txt.

6. Outputting Results to a JSON File
```bash
xsschamp --output results.json --format json --mode active https://example.com/search?q=FUZZ
```
   Results saved as a JSON file for further processing.

7. DOM-Based XSS Scan
```bash
xsschamp --mode dom https://example.com/page?param=FUZZ
```
   Scans for client-side DOM-based XSS vulnerabilities.

---

## CLI Options
Flag	Description
-  --list	(File with URLs to scan)
-  --mode	(active, passive, or dom)
-  --type	(reflected, stored, all)
-  --post	(POST body with FUZZ marker)
-  --payloads	(Custom payload file)
-  --proxy	(Proxy list file (e.g., socks5.txt))
-  --protocol	(http, socks4, socks5, or auto)
-  --threads	(Number of concurrent requests)
-  --continue	(Resume from previous scan log)
-  --output	(Save report to file)
-  --format	(Output format: console, json, or html)


| Option       | Description                                                                        | Example / Detail                                                                            |
| ------------ | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `-h, --help` | Show this help message and exit                                                    | `xsschamp -h`                                                                               |
| `--mode`     | The scanning mode:                                                                 | `passive` (only gather info), `active` (inject payloads), or `dom` (DOM-based XSS scanning) |
| `--type`     | What kind of XSS to scan for:                                                      | `reflected` (in URL), `stored` (in stored data), or `all`                                   |
| `--post`     | POST data for scanning stored XSS vulnerabilities (injection in POST body)         | `--post "username=admin&comment=FUZZ"`                                                      |
| `--payloads` | Specify a file that contains custom XSS payloads to use instead of defaults        | `--payloads mypayloads.txt`                                                                 |
| `--proxy`    | Use a proxy list file for routing traffic                                          | `--proxy socks5.txt`                                                                        |
| `--protocol` | Proxy protocol: HTTP, SOCKS4, SOCKS5, or auto (auto-detect based on proxy file)    | `--protocol socks5`                                                                         |
| `--output`   | Output the scan results to a file                                                  | `--output results.json`                                                                     |
| `--format`   | Format of the output report                                                        | `console` (default), `json`, or `html`                                                      |
| `url`        | The target URL to scan. Use the keyword `FUZZ` in the URL to mark injection points | `https://example.com/search?q=FUZZ`                                                         |



## Output Formats
report.json: Structured output

report.html: Visual summary (clickable)

console: Color-rich CLI output

## 📚 Requirements
See requirements.txt for pinned versions.
```bash
httpx
aiohttp
playwright
rich
argcomplete
loguru
beautifulsoup4
lxml
PySocks
```
## Install with:

```bash
pip3 install -r requirements.txt
playwright install
```

## 🤝 Contributing
PRs welcome!
Open an issue to propose features or report bugs.

## 🧠 Author
AwesomeVed
Cybersecurity Student • Bug Bounty Hunter
devkumarmahto204@outlook.com


