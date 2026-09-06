# Blue Team Command Reference

A practical defensive quick reference for cybersecurity engineers, SOC analysts, and IT administrators.

> Use only on systems you own or are authorized to administer.

## Quick Start

```bash
git clone https://github.com/BlackPanda999/blue-team-command-cheatsheet.git
cd blue-team-command-cheatsheet
```

## Linux Triage

```bash
id
whoami
cat /etc/os-release
uname -a
who
last -n 20
ss -tulpn
ps aux --sort=-%cpu | head -20
df -h
free -h
uptime
```

## Linux Logs and Authentication

```bash
journalctl -p err -b --no-pager
sudo grep -E "Failed password|Accepted|Invalid user" /var/log/auth.log | tail -50
sudo journalctl _COMM=sudo --since "24 hours ago" --no-pager
```

## Linux Permissions and Persistence

```bash
find /var/www -xdev -type f -perm -0002 -print
find /var/log -type f -mtime -1 -print
crontab -l
sudo ls -la /etc/cron.*
systemctl --type=service --state=running
```

## Windows PowerShell Triage

```powershell
whoami
Get-ComputerInfo | Select-Object WindowsProductName, OsVersion, CsName
Get-Process | Sort-Object CPU -Descending | Select-Object -First 20
Get-NetTCPConnection -State Listen | Sort-Object LocalPort
Get-WinEvent -FilterHashtable @{LogName="System"; Level=2} -MaxEvents 50
Get-WinEvent -FilterHashtable @{LogName="Security"; Id=4625} -MaxEvents 50
Get-MpComputerStatus | Select-Object AMRunningMode, AntivirusEnabled, RealTimeProtectionEnabled
```

## Network Investigation

```bash
nslookup example.com
traceroute example.com
nc -vz example.com 443
ip route
```

```powershell
Resolve-DnsName example.com
Test-NetConnection example.com -Port 443
Get-NetRoute
```

## Incident Response Checklist

1. Confirm the alert and record the time in UTC.
2. Preserve relevant logs before rotation.
3. Identify affected hosts, accounts, and services.
4. Contain only with authorization and document changes.
5. Rotate compromised credentials through the approved process.
6. Check persistence and lateral movement.
7. Restore from a known-good state and monitor.
8. Write a timeline, root cause, and prevention actions.

## Free Official References

- [NIST Incident Handling](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final)
- [CIS Controls](https://www.cisecurity.org/controls/v8)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [MITRE D3FEND](https://d3fend.mitre.org/)
- [OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/)
- [Microsoft Security](https://learn.microsoft.com/en-us/security/)
- [Wireshark Guide](https://www.wireshark.org/docs/wsug_html_chunked/)

## Why This Matters

Fast, careful triage is a daily skill in security engineering and IT administration. This reference favors evidence collection and least-impact checks before remediation.

## Contributing

Suggest tested, defensive commands or official free references. Never include secrets, private customer data, or unapproved scanning instructions.

## License

MIT. See [LICENSE](LICENSE).
