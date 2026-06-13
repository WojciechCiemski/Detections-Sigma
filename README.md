# Detections Sigma

A curated collection of vendor-agnostic Sigma rules for SOC monitoring, threat hunting, detection engineering, and security lab work.

The repository now covers Windows behavior detections, Linux behavior detections, and CVE-focused rules for high-impact exploitation activity observed in 2025.

## Repository Layout

```text
rules/
  _templates/
    template_rule.yml
  cve/
    2025/
      cve-2025-*.yml
  linux/
    linux_*.yml
  windows/
    *.yml
tools/
  sigma_rule_checker.py
```

## Current Coverage

| Area | Rule Count | Focus |
|------|------------|-------|
| Windows | 26 | Credential access, PowerShell, LOLBins, WMI, services, script hosts, macro execution |
| Linux | 7 | SSH brute force, kernel modules, netcat listeners, shadow access, sudo anomalies, tmp execution, cron shells |
| CVE 2025 | 16 | Exploitation and post-exploitation indicators for widely abused vulnerabilities |

Total detection rules: 49.

## CVE 2025 Coverage

| Vulnerability | Coverage | Rule Files |
|---------------|----------|------------|
| CVE-2025-0282 Ivanti Connect Secure | Post-exploitation commands and SPAWN malware file indicators | `cve-2025-0282-ivanti-post-exploitation-commands.yml`, `cve-2025-0282-ivanti-spawn-malware-files.yml` |
| CVE-2025-24813 Apache Tomcat | Suspicious partial PUT upload behavior | `cve-2025-24813-tomcat-partial-put-abuse.yml` |
| CVE-2025-29927 Next.js | Middleware bypass header abuse | `cve-2025-29927-nextjs-middleware-bypass-header.yml` |
| CVE-2025-31324 SAP NetWeaver | Metadata uploader access and JSP webshell access | `cve-2025-31324-sap-metadata-uploader-access.yml`, `cve-2025-31324-sap-webshell-access.yml` |
| CVE-2025-31161 CrushFTP | AWS4-HMAC authentication bypass pattern | `cve-2025-31161-crushftp-aws4-hmac-auth-bypass.yml` |
| CVE-2025-3248 Langflow | Validate-code unauthenticated RCE attempts | `cve-2025-3248-langflow-validate-code-rce.yml` |
| CVE-2025-32756 Fortinet FortiVoice | FastCGI crash indicators and malware file IOCs | `cve-2025-32756-fortinet-fortivoice-fcgi-crash-iocs.yml`, `cve-2025-32756-fortinet-fortivoice-malware-file-iocs.yml` |
| CVE-2025-34028 Commvault | Deploy package traversal and JSP webshell access | `cve-2025-34028-commvault-deploy-webpackage-traversal.yml`, `cve-2025-34028-commvault-jsp-webshell-access.yml` |
| CVE-2025-4427 / CVE-2025-4428 Ivanti EPMM | Expression language and Java execution primitives | `cve-2025-4427-4428-ivanti-epmm-el-injection-api-request.yml` |
| CVE-2025-53770 SharePoint ToolShell | ToolPane request pattern and `spinstall0.aspx` access | `cve-2025-53770-sharepoint-toolshell-toolpane-request.yml`, `cve-2025-53770-sharepoint-spinstall0-machinekey-access.yml` |
| CVE-2025-59718 / CVE-2025-59719 Fortinet | FortiCloud SSO admin login and config download activity | `cve-2025-59718-59719-fortinet-forticloud-sso-admin-config-download.yml` |

## What's Inside

- Ready-to-use Sigma rules in YAML format
- MITRE ATT&CK mappings through `attack.*` tags
- CVE tags for vulnerability-focused detections
- False-positive guidance in every rule
- References to vendor advisories, vulnerability databases, or threat research
- A reusable rule template under `rules/_templates/`

## How To Use

Clone the repository:

```bash
git clone https://github.com/WojciechCiemski/Detections-Sigma.git
cd Detections-Sigma
```

Browse rules by detection area:

```bash
ls rules/windows
ls rules/linux
ls rules/cve/2025
```

Convert a rule with your Sigma toolchain. Backend names and command syntax may vary depending on whether you use `sigma-cli`, `sigmac`, or a SIEM-native integration.

Example with Sigma CLI:

```bash
sigma convert -t splunk rules/windows/lsass-access.yml
sigma convert -t splunk rules/cve/2025/cve-2025-53770-sharepoint-toolshell-toolpane-request.yml
```

Example with legacy sigmac:

```bash
sigmac -t splunk rules/windows/lsass-access.yml
```

## Rule Status

| Status | Meaning |
|--------|---------|
| `experimental` | New or draft detection logic that should be tuned and validated before production use |
| `testing` | Works in lab or controlled testing, but still needs broader environment validation |
| `stable` | Confirmed and suitable for production use with normal tuning |
| `deprecated` | Replaced, obsolete, or no longer recommended |

## Rule Quality Expectations

Each rule should include:

- `title`
- `id`
- `status`
- `description`
- `author`
- `date`
- `license`
- `logsource`
- `detection` with `condition`
- `falsepositives`
- `level`
- `tags`
- `references`

For CVE-focused rules, include at least one `cve.YEAR.ID` tag and one relevant MITRE ATT&CK technique tag.

## Tuning Notes

Sigma rules are intentionally portable, but real environments differ. Before enabling alerts in production:

- Map Sigma fields to your SIEM or data model
- Validate log source availability and field names
- Test against representative benign and malicious samples
- Review false-positive notes
- Adjust severity and filtering to match your environment

## Contributing

Pull requests are welcome.

Please follow the existing style and include:

- Clean YAML formatting
- A unique UUID in `id`
- MITRE ATT&CK tags
- CVE tags where applicable
- Useful references
- Practical false-positive guidance
- Status set to `experimental`, `testing`, `stable`, or `deprecated`

Start from:

```text
rules/_templates/template_rule.yml
```

## License

This repository is licensed under the MIT License. See `LICENSE` for details.

## Author

Created and maintained by [Wojciech Ciemski](https://www.linkedin.com/in/wojciech-ciemski) - [SecurityBezTabu.pl](https://securitybeztabu.pl)
