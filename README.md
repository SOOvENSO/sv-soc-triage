# SV SOC Triage

**Khalid Aslaoui (SOOVENSO) · SV**

A browser-only analyst dashboard for a Wazuh and pfSense home lab. Open
`index.html` directly. The sample is loaded automatically. No Python,
dependencies, or network requests are required.

## Triage workflow

1. Paste one JSON record per line in each input and select **Analyser**.
2. Review the alert and blocked-event timestamps and their source line numbers.
3. Export the report as JSON for incident notes.

Wazuh input expects `timestamp`, `data.srcip`, `rule.level` and optionally
`rule.description`. The pfSense input expects already-normalized JSONL
with `timestamp`, `src_ip`, and `action` (`block` or `pass`).
Example pfSense row:

```json
{"timestamp":"2026-11-20T20:01:00Z","src_ip":"192.0.2.20","action":"block"}
```

Use IPv4 addresses and timestamps with timezone offsets. Alerts at level 7
and above are shown. Each alert is matched to the first firewall block for
that source IP within five minutes either side. A match is a lead for manual
review. Separate events may share an IP, and clock skew can affect results.
Native pfSense syslog/CSV parsing and IPv6 are outside this version.
