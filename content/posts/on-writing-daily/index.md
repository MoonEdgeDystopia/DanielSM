+++
title = "The Discipline of Log Analysis"
subtitle = "Turning noise into signal during incident response"
authors = ['Daniel']
date = 2026-02-14
publishedDate = 2026-02-14
draft = false
featured = false
cover = 'https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Computer_code_screen.jpg/1200px-Computer_code_screen.jpg'
tags = ['digital forensics', 'incident response', 'operating systems']
toc = false
+++

In the aftermath of a security incident, logs are often the only witness. They record who accessed a system, what commands were executed, which files were touched, and where data traveled. But logs are also noisy, incomplete, and frequently overwhelming. The ability to analyze them effectively is one of the most valuable skills in cybersecurity.

## The Foundation: Know Your Data Sources

Before an incident occurs, a mature security team has already mapped its data sources. Windows Event Logs, Sysmon, Linux auditd, web server access logs, firewall logs, DNS queries, and endpoint detection telemetry each tell part of the story. The analyst's job is to weave these fragments into a coherent narrative.

Different operating systems produce different log formats and store them in different locations. On Linux, `/var/log/` is the traditional home for system logs, but modern distributions may also use systemd-journald. On Windows, the Event Log service records application, security, and system events. Understanding these native formats is essential before you can parse, filter, or correlate them.

## Baselining: Understanding Normal

The single most common mistake in log analysis is looking for malicious activity without first understanding what normal looks like. Every environment has its own rhythms: scheduled backup jobs, automated patching windows, legitimate administrative scripts. Without a baseline, these benign patterns look like threats, while actual attacker behavior blends into the noise.

Baselining is not a one-time project. It is an ongoing process of observing, documenting, and refining. Start with the high-volume event types. When do they typically occur? Which accounts generate them? What does the payload usually contain? Over time, this contextual knowledge allows you to spot deviations instantly.

## Correlation and Pattern Recognition

Isolated events are rarely meaningful. A single failed login is probably noise. A series of failed logins followed by a successful one from an unusual location is a different story. This is where correlation becomes critical.

Time-based correlation is the most intuitive approach: group events that occur close together and look for sequences that match known attack patterns. But correlation can also be geographic (unusual source IP), behavioral (an account accessing resources it never touches), or statistical (a spike in outbound traffic).

Modern SIEM platforms automate much of this work, but the analyst must still understand the logic behind the alerts. A poorly tuned correlation rule generates false positives that erode trust and waste time. A well-tuned rule surfaces genuine anomalies that demand investigation.

## Hunting for Indicators of Compromise

During active incident response, analysts often work from Indicators of Compromise (IOCs): IP addresses, domain names, file hashes, or command-line strings associated with known malware or threat actors. IOCs are useful but limited. They are static signatures that attackers can easily change.

More powerful are Indicators of Attack (IOAs): behavioral patterns that reveal intent regardless of the specific tools used. Lateral movement, credential dumping, privilege escalation, and data staging all produce distinctive behavioral signatures. Hunting for IOAs requires deeper log analysis but yields more durable detections.

## Tools of the Trade

While enterprise SIEMs are common, many powerful log analysis tools are freely available:

- **jq** for parsing JSON logs at the command line.
- **grep, awk, and sed** for rapid filtering and transformation.
- **Sigma** for writing generic detection rules portable across SIEM platforms.
- **Velociraptor** for endpoint visibility and artifact collection.
- **Eric Zimmerman's tools** for Windows forensic artifact parsing.

The best analysts are comfortable moving between these tools depending on the task at hand. There is no single platform that solves every problem.

## Conclusion

Log analysis is painstaking work. It demands patience, attention to detail, and a tolerance for ambiguity. But it is also deeply rewarding. In a field where attackers hide in shadows, logs are the light that reveals their movements. Mastering log analysis means mastering the art of detection itself.
