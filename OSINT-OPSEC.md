# OSINT OpSec: GitHub Threat Landscape for OSINT Practitioners

> **Last Updated:** January 2026
>
> This document covers active threats targeting OSINT researchers, security professionals, and developers through malicious GitHub repositories. If you work with OSINT tools, you are a target. This is the threat landscape you operate in.

---

## Table of Contents

- [Why This Matters](#why-this-matters)
- [Active Campaigns](#active-campaigns)
  - [1. Stargazers Ghost Network (DaaS Infrastructure)](#1-stargazers-ghost-network-daas-infrastructure)
  - [2. PyStoreRAT - Fake OSINT and GPT Tools](#2-pystorerat---fake-osint-and-gpt-tools)
  - [3. Webrat - Fake CVE Exploit PoCs](#3-webrat---fake-cve-exploit-pocs)
  - [4. Banana Squad - Trojanized Hacking Tools](#4-banana-squad---trojanized-hacking-tools)
  - [5. SmartLoader/Lumma - AI-Generated Repos](#5-smartloaderlumma---ai-generated-repos)
- [How To Verify OSINT Repositories](#how-to-verify-osint-repositories)
- [Red Flags Checklist](#red-flags-checklist)
- [Indicators of Compromise (IOCs)](#indicators-of-compromise-iocs)
- [Hardening Your Own Repos](#hardening-your-own-repos)
- [Primary Sources](#primary-sources)

---

## Why This Matters

Between 2024 and 2026, five major campaigns were discovered using GitHub as a malware distribution platform. They share a common pattern:

1. Create repositories that **look like legitimate OSINT/security tools**
2. Use **AI-generated content** to appear credible (READMEs, commit history, code comments)
3. **Inflate stars and forks** using bot networks to gain visibility
4. Wait for trust to build, then **inject malicious payloads** via "maintenance" commits
5. Promote across **YouTube, X/Twitter, and security forums**

These campaigns specifically target people who clone and run security tools. That means **OSINT researchers, penetration testers, bug bounty hunters, and infosec students** are the primary victims.

Unlike the reporters and researchers at Check Point, Morphisec, or Kaspersky who write about these campaigns, people who **maintain and curate OSINT tool repositories** face additional risk: malicious pull requests submitted to inject backdoors into trusted collections.

---

## Active Campaigns

### 1. Stargazers Ghost Network (DaaS Infrastructure)

| Detail | Information |
|--------|-------------|
| **Discovered By** | Check Point Research |
| **Published** | July 24, 2024 |
| **Threat Actor** | "Stargazer Goblin" |
| **Status** | Active (infrastructure persists despite takedowns) |

**What It Is:**
A Distribution-as-a-Service (DaaS) operation running 3,000+ ghost GitHub accounts. Other criminals pay Stargazer Goblin to distribute their malware through these accounts.

**Scale:**
- 3,000+ active ghost accounts
- Estimated $100,000+ total revenue
- ~$8,000 earned in a single month (mid-2024)
- 1,300+ victims infected in 4 days during one campaign (January 2024)

**How It Works:**
- Ghost accounts are segmented by role: some star repos, some host phishing templates, some serve malicious releases
- Pricing: $10 to star 100 repos, $2 for an aged account with repository history
- Automated recovery: when GitHub bans accounts, the network detects and replaces them
- Cross-platform amplification across YouTube, Discord, Instagram, X/Twitter, and Facebook

**Malware Delivered:**
Atlantida Stealer, Rhadamanthys, RisePro, Lumma Stealer, RedLine

**GitHub Response:**
~1,559 repositories removed since May 2024. 200+ remained active at time of reporting.

**Law Enforcement:**
No arrests or indictments reported for the operators.

**Source:** [Check Point Research - Stargazers Ghost Network](https://research.checkpoint.com/2024/stargazers-ghost-network/)

---

### 2. PyStoreRAT - Fake OSINT and GPT Tools

| Detail | Information |
|--------|-------------|
| **Discovered By** | Morphisec Threat Labs (researcher: Yonatan Edri) |
| **Published** | December 11, 2025 |
| **Attribution** | Unknown; Russian-language artifacts found in codebase |
| **Status** | Repos removed; campaign likely to resurface |

**What It Is:**
A campaign creating fake GitHub repositories disguised as OSINT tools, GPT/AI chat wrappers, and DeFi crypto bots. After building trust and GitHub trending visibility, malicious "maintenance" commits injected the PyStoreRAT backdoor.

**Timeline:**
- Mid-June 2025: First malicious repositories appeared
- Summer 2025: Steady stream of new repos, social media promotion
- October-November 2025: Malicious "maintenance" commits injected
- December 11, 2025: Morphisec published findings

**The Trap (Step by Step):**
1. Create new GitHub accounts or reactivate dormant ones
2. Publish polished, AI-generated projects with professional READMEs
3. Promote via YouTube and X/Twitter
4. Artificially inflate stars and forks (Stargazers Ghost Network techniques)
5. Several repos climbed onto GitHub's trending page
6. Wait for trust to build
7. Push subtle "maintenance" commits containing the backdoor
8. Many tools displayed only static menus or non-interactive UIs and never actually worked

**Fake Repo Themes:**
- OSINT tools (e.g., "OSINT360-GPT")
- GPT/AI chat wrappers
- DeFi/crypto trading bots
- Security utilities

**PyStoreRAT Capabilities:**
- Modular, multi-stage implant
- Executes: EXE, DLL, PowerShell, MSI, Python, JavaScript, HTA modules
- Deploys Rhadamanthys infostealer as secondary payload
- Targets crypto wallets: Ledger Live, Trezor, Exodus, Atomic, Guarda, BitBox02
- Persistence: Scheduled task disguised as "NVIDIA App SelfUpdate" (runs every 10 minutes)
- Spreads via USB/removable media using malicious LNK files
- Rotating C2 infrastructure using GitHub-hosted nodes and disposable domains
- Encrypted C2 communications

**Attribution Clues:**
- Russian-language string found in code
- Coding patterns consistent with Eastern European origin

**Sources:**
- [Morphisec - PyStoreRAT Full Report](https://www.morphisec.com/blog/pystorerat-a-new-ai-driven-supply-chain-malware-campaign-targeting-it-osint-professionals/)
- [The Hacker News - PyStoreRAT](https://thehackernews.com/2025/12/fake-osint-and-gpt-utility-github-repos.html)
- [Hackread - Repo Names and Screenshots](https://hackread.com/pystorerat-rat-malware-github-osint-researchers/)

---

### 3. Webrat - Fake CVE Exploit PoCs

| Detail | Information |
|--------|-------------|
| **Discovered By** | Kaspersky (Solar 4RAYS team) |
| **Published** | December 23, 2025 |
| **Attribution** | Unknown |
| **Status** | All 15 repos removed; pattern likely to repeat |

**What It Is:**
15 malicious repositories hosting fake proof-of-concept exploits for real, high-profile CVEs. Targeted junior security researchers and infosec students who would naturally seek out PoC code.

**Timeline:**
- Active since at least September 2025
- Kaspersky discovered in October 2025
- Published December 23, 2025

**Known Malicious Repositories (now removed):**
- `RedFoxNxploits/CVE-2025-10294-Poc`
- `FixingPhantom/CVE-2025-10294`
- `h4xnz/CVE-2025-10294-POC`
- `usjnx72726w/CVE-2025-59295`
- 11+ additional repositories

**How It Works:**
- Repos named after real CVEs with high CVSS scores (8.8-9.8)
- AI-generated READMEs with detailed technical write-ups
- Password-protected ZIP with password hidden in the filename
- Inside: decoy DLL + batch file + main executable (rasmanesc.exe)
- Threat actors monitored cybersecurity news to identify trending vulnerabilities

**Webrat Capabilities:**
- Steals credentials from Steam, Discord, Telegram
- Steals crypto wallet data
- Webcam and screen surveillance
- Keylogging
- Disables Windows Defender
- Privilege escalation

**Source:** [Kaspersky Securelist - Webrat](https://securelist.com/webrat-distributed-via-github/118555/)

---

### 4. Banana Squad - Trojanized Hacking Tools

| Detail | Information |
|--------|-------------|
| **Discovered By** | ReversingLabs |
| **Published** | June 2025 |
| **Threat Actor** | "Banana Squad" (bananasquad[.]ru, 1312services[.]ru, 1312stealer[.]ru) |
| **Status** | 67+ repos removed; infrastructure Russian-hosted |

**What It Is:**
200+ trojanized repositories impersonating legitimate hacking tools: credential stealers, vulnerability scanners, Discord account cleaners, and Python utilities.

**Timeline:**
- Initial activity: April 2023
- First spotted by Checkmarx: October 2023
- Full campaign documented by ReversingLabs: June 2025

**Stealth Techniques:**
- Exploited GitHub's UI: long strings of spaces push malicious code off-screen to the right, invisible in normal browser view
- Repo names identical to legitimate repos (typosquatting)
- "About" sections packed with SEO keywords and flame/rocket emojis (AI-generated)
- Automated GitHub Actions workflows simulated active development

**Backdoor Variants:**
1. Visual Studio PreBuild events (found in 111 repos)
2. Python scripts
3. Screensaver files
4. JavaScript: 17,000 lines of obfuscated code in Electron apps

**Final Payloads:**
AsyncRAT, Remcos RAT, Lumma Stealer. Also disables Windows Defender and deletes shadow copies.

**Source:** [The Hacker News - Banana Squad](https://thehackernews.com/2025/06/67-trojanized-github-repositories-found.html)

---

### 5. SmartLoader/Lumma - AI-Generated Repos

| Detail | Information |
|--------|-------------|
| **Discovered By** | Trend Micro |
| **Published** | March 2025 |
| **Related** | Microsoft tracked parallel malvertising campaign (Dec 2024, ~1M devices) |
| **Status** | Ongoing |

**What It Is:**
Fake repos disguised as gaming cheats, cracked software, and system tools. AI-generated README files serve as the primary lure. Malicious files stored in GitHub Releases section.

**Scale:**
- Microsoft detected campaign impacting nearly 1,000,000 devices globally
- Attack originated from illegal streaming websites with malvertising redirectors leading to GitHub

**Malware:**
SmartLoader (loader) delivering Lumma Stealer (infostealer)

**Sources:**
- [Trend Micro - AI-Assisted Fake Repos](https://www.trendmicro.com/en_us/research/25/c/ai-assisted-fake-github-repositories.html)
- [Microsoft Security Blog - Malvertising Campaign](https://www.microsoft.com/en-us/security/blog/2025/03/06/malvertising-campaign-leads-to-info-stealers-hosted-on-github/)

---

## How To Verify OSINT Repositories

Before cloning, installing, or running any OSINT tool from GitHub:

### 1. Check Account History
- When was the account created?
- Does it have consistent activity over months/years?
- Are there real interactions (issues, discussions, PRs with other real users)?

### 2. Inspect Star/Fork Patterns
- Use [GitHub Star History](https://star-history.com/) to check for sudden spikes
- Do the stargazers have real profiles with their own repos, or are they empty accounts?
- A repo with 500 stars but 0 open issues and 0 PRs is suspicious

### 3. Read the Code Before Running
- If a Python tool has `import os; os.system()` calling external URLs, that is a red flag
- Check for obfuscated code, base64 encoded strings, or calls to mshta.exe
- Scroll right in the GitHub UI to check for hidden code (Banana Squad technique)

### 4. Check Commit History
- Were there "maintenance" commits that introduced new functionality months after initial release?
- Does the commit history look organic or was it all pushed in a single day?

### 5. Cross-Reference
- Is the tool mentioned in established OSINT communities (OSINT Framework, Awesome OSINT, cipher387's lists)?
- Can you find reviews or mentions from known researchers?
- Does the author have a presence outside GitHub?

### 6. Sandbox First
- Run unknown tools in a VM or container, never on your host machine
- Monitor network connections during execution
- Check what files the tool accesses beyond its stated purpose

---

## Red Flags Checklist

- [ ] Brand new account with polished, professional repo
- [ ] Many stars/forks but zero issues, PRs, or discussions
- [ ] AI-generated README (overly polished, generic language, lots of emojis)
- [ ] Password-protected ZIPs in releases
- [ ] Tool displays static menus or doesn't actually work
- [ ] "Maintenance" commits that add obfuscated code after initial release
- [ ] No real community engagement (no responses to issues, no contributor history)
- [ ] Calls to mshta.exe, encoded PowerShell, or suspicious external URLs in code
- [ ] Horizontal scrolling reveals hidden code in GitHub UI
- [ ] Scheduled tasks or persistence mechanisms unrelated to the tool's function
- [ ] Tool requests permissions far beyond its stated purpose

---

## Indicators of Compromise (IOCs)

### PyStoreRAT
- Persistence: Scheduled task named "NVIDIA App SelfUpdate" (every 10 min or at login)
- Execution: mshta.exe launched via cmd.exe (checks for CrowdStrike Falcon or Cybereason first)
- Lateral: LNK files replacing documents on removable drives
- Wallet targeting: Ledger Live, Trezor, Exodus, Atomic, Guarda, BitBox02
- Full IOC list: [Morphisec Report (downloadable)](https://www.morphisec.com/blog/pystorerat-a-new-ai-driven-supply-chain-malware-campaign-targeting-it-osint-professionals/)

### Webrat
- Executable: `rasmanesc.exe` inside password-protected ZIPs
- Password embedded in filename
- Contains decoy DLL + batch file
- Full IOC list: [Kaspersky Securelist](https://securelist.com/webrat-distributed-via-github/118555/)

### Banana Squad
- C2 domains: `bananasquad[.]ru`, `1312services[.]ru`, `1312stealer[.]ru`
- Payloads: AsyncRAT, Remcos, Lumma Stealer
- Technique: Hidden code via horizontal whitespace in source files

### General Detection
- Unexpected scheduled tasks
- mshta.exe spawned by Python or Node processes
- Outbound connections to recently registered domains
- PowerShell encoded commands executed by development tools

---

## Hardening Your Own Repos

If you maintain an OSINT tools list or curated repository:

1. **Enable branch protection** on main/master
2. **Require PR reviews** before merging (even solo maintainers should use PRs)
3. **Never merge PRs that add executable code or scripts** without thorough review
4. **Vet every external link** before adding it to a curated list
5. **Check contributor accounts** for the same red flags listed above
6. **Use signed commits** (GPG) to prove authorship
7. **Monitor for forks** that may be distributing modified malicious versions of your repo
8. **Add a security policy** (SECURITY.md) so people can report suspicious forks

---

## Primary Sources

| Organization | Report | Date |
|-------------|--------|------|
| Check Point Research | [Stargazers Ghost Network](https://research.checkpoint.com/2024/stargazers-ghost-network/) | July 2024 |
| Morphisec | [PyStoreRAT Campaign](https://www.morphisec.com/blog/pystorerat-a-new-ai-driven-supply-chain-malware-campaign-targeting-it-osint-professionals/) | December 2025 |
| Kaspersky (Securelist) | [Webrat via Fake PoCs](https://securelist.com/webrat-distributed-via-github/118555/) | December 2025 |
| ReversingLabs | [Banana Squad](https://www.reversinglabs.com/blog/threat-actor-banana-squad-exploits-github-repos-in-new-campaign) | June 2025 |
| Trend Micro | [AI-Assisted Fake Repos](https://www.trendmicro.com/en_us/research/25/c/ai-assisted-fake-github-repositories.html) | March 2025 |
| Microsoft | [Malvertising via GitHub](https://www.microsoft.com/en-us/security/blog/2025/03/06/malvertising-campaign-leads-to-info-stealers-hosted-on-github/) | March 2025 |
| The Hacker News | [PyStoreRAT Coverage](https://thehackernews.com/2025/12/fake-osint-and-gpt-utility-github-repos.html) | December 2025 |
| Hackread | [Malicious Repo List](https://hackread.com/pystorerat-rat-malware-github-osint-researchers/) | December 2025 |
| IBM | [3000 Ghost Accounts](https://www.ibm.com/think/news/3000-ghost-accounts-github-malware) | July 2024 |

---

## Related Resources

For a curated list of verified OSINT tools and APIs, see:
- [APIs for OSINT](https://github.com/An0myl0u5-Lite/API-s-for-OSINT) - Curated OSINT API collection

---

*This document is provided for defensive and educational purposes. Stay vigilant.*
