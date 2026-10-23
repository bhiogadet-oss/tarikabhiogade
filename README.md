# Zero-Trust Network Access (ZTNA) — Policy Engine Demo

**Student:** Tarika Bhiogade  
**Institute:** Sandip University  
**Submission date:** 23 October 2026

## Project description
This project demonstrates the core ideas behind Zero-Trust Network Access: verify each request, apply least privilege, require multi-factor authentication (MFA) for sensitive resources, check device compliance, deny unknown resources by default, and record access decisions in an audit log.

The topic corresponds to suggestion 9: **Zero-Trust Network Access — use Cloudflare Tunnels and MFA to secure internal admin consoles.** This submission implements a local policy-engine simulation and includes deployment guidance; it does not claim that a live Cloudflare Tunnel has been provisioned.

## Technologies used
- Python 3.9 or later
- Python standard library (`dataclasses`, `datetime`, `json`, `pathlib`, `typing`)
- Jupyter Notebook (optional, to run the `.ipynb` file)
- Cloudflare Tunnel / Cloudflare Access and an identity provider (deployment extension, not required for the simulation)

## Files
- `Tarika_Bhiogade_ZeroTrustNetworkAccess.ipynb` — notebook version
- `Tarika_Bhiogade_ZeroTrustNetworkAccess.py` — runnable Python script
- `requirements.txt` — dependencies
- `Tarika_Bhiogade_ProjectReport.docx` — project report

## Setup and run
1. Install Python 3.9+.
2. (Optional) Create a virtual environment.
3. Install optional notebook support with `pip install -r requirements.txt` if you want to use Jupyter.
4. Run the script:
   ```bash
   python Tarika_Bhiogade_ZeroTrustNetworkAccess.py
   ```
   Or open the `.ipynb` file in Jupyter Notebook and run the cells in order.
5. The program prints ALLOW/DENY decisions and appends events to `ztna_audit.log` in the current working directory.

## Sample policy behaviour
- `admin` + `admin-console` + MFA verified + compliant device → ALLOW
- `viewer` requesting `admin-console` → DENY (not authorized)
- `security-analyst` requesting `incident-dashboard` without MFA → DENY
- `auditor` requesting `public-status` → ALLOW
- Any request to an unknown resource → DENY

## Security and limitations
MFA and device compliance are simulated values supplied to the policy engine. This is not a real identity system and must not be exposed as a production service. A real deployment should put Cloudflare Access (or an equivalent identity-aware proxy) in front of internal applications, route traffic through a Cloudflare Tunnel, enforce MFA with an identity provider, configure device posture checks, use HTTPS, apply least privilege, and protect/retain audit logs. Do not commit API tokens, credentials, or private configuration files.

## Dataset
No external dataset is required. The program uses a small, synthetic list of access requests defined in the source code. This avoids including personal or confidential information.
