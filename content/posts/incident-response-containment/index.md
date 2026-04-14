+++
title = "The Containment Stage: Strategy, Process, and Standards"
subtitle = "How effective containment bridges detection and recovery in incident response"
authors = ['Daniel']
date = 2026-04-13
publishedDate = 2026-04-13
draft = false
featured = false
cover = 'iso-27035-diagram.png'
tags = ['incident response', 'cybersecurity', 'networks']
toc = false
+++

When a security incident is detected, the clock starts ticking. Every second of delay can mean additional compromised systems, exfiltrated data, or expanded attacker access. The containment stage exists to stop this progression — to halt the bleeding before the organization moves into eradication and recovery. Yet containment is often the most poorly planned phase of incident response. Without a clear strategy, well-defined processes, and an understanding of how containment connects to the broader incident management lifecycle, response teams risk making the situation worse instead of better.

## The Importance of a Good Containment Strategy

Containment is not simply about unplugging machines or blocking IP addresses. It is a deliberate set of actions designed to limit the scope and impact of an incident while preserving evidence and maintaining business continuity. A good containment strategy answers three critical questions before an incident ever occurs:

- **What assets are most critical?** Not all systems are equal. A domain controller, a customer database, and a public marketing website carry vastly different risk profiles. Containment priorities must align with business impact.
- **What is the acceptable trade-off between speed and evidence preservation?** Aggressive containment — such as immediately powering down a compromised server — may destroy volatile memory artifacts that forensic analysts need. A nuanced strategy defines when to isolate, when to snapshot, and when to observe.
- **Who has the authority to make containment decisions?** During a crisis, unclear chains of command lead to hesitation or conflicting actions. The strategy must designate decision-makers and escalation paths in advance.

Organizations that fail to develop this strategy in peacetime often find themselves improvising during an incident, which leads to inconsistent results and prolonged damage.

## Well-Defined Processes in Case of an Incident

Processes turn strategy into repeatable action. At minimum, an incident response playbook should define the following containment procedures:

1. **Initial Triage:** Confirm the incident, assess its severity, and identify affected systems. This step prevents panic-driven overreaction to false positives.
2. **Network Segmentation:** Isolate affected segments using VLANs, firewall rules, or access control lists. The goal is to prevent lateral movement without cutting off legitimate operations.
3. **Credential Rotation:** Force password resets and revoke session tokens for compromised accounts. Attackers often maintain persistence through valid credentials.
4. **Evidence Preservation:** Capture memory dumps, disk images, and log exports before containment actions alter the system state.
5. **Communication Protocols:** Notify stakeholders according to a pre-defined matrix. Legal, public relations, and executive leadership may all need timely updates.

These processes should be documented, tested in tabletop exercises, and updated regularly. A playbook that sits unread in a SharePoint folder provides no value when ransomware is encrypting files at 2:00 AM.

## How Containment Relates to Eradication

Containment and eradication are distinct phases, but they are deeply interdependent. **Containment stops the attack from spreading.** **Eradication removes the attacker's presence from the environment.** You cannot safely eradicate a threat across a wide, uncontrolled attack surface. Containment shrinks that surface to a manageable scope.

Conversely, containment without eradication is a temporary fix. An isolated compromised endpoint that remains infected is still a liability. It may re-infect the network the moment isolation is lifted. Effective incident response treats containment as the bridge that allows the team to move systematically into eradication — removing malware, closing vulnerabilities, and rebuilding trust in the affected systems.

## ISO/IEC 27035 and the Incident Management Cycle

The international standard **ISO/IEC 27035** provides a structured framework for information security incident management. It divides the lifecycle into five continuous stages that form a closed loop of improvement. Containment sits at the heart of the **Response** stage, but its effectiveness depends on the maturity of all preceding stages.

{{< figure src="iso-27035-diagram.png" caption="ISO/IEC 27035 Incident Management Cycle" width="500" >}}

The five stages are:

- **Plan & Prepare:** Establish policies, playbooks, and communication channels before an incident occurs.
- **Identify, Detect, & Report:** Recognize anomalies through monitoring and reporting mechanisms.
- **Assessment & Decision:** Evaluate the incident's scope, impact, and required response level.
- **Response:** Execute containment, eradication, and recovery actions.
- **Lesson Learnt:** Review what happened, update processes, and feed improvements back into the planning stage.

ISO/IEC 27035 emphasizes that incident management is not a linear checklist but an iterative discipline. Every incident is an opportunity to refine containment strategies and strengthen organizational resilience.

## A Practical Containment Decision Tree

Theory is essential, but containment often happens under pressure. The following decision tree provides a practical workflow for responding to a potentially infected endpoint. It guides the responder through physical access constraints, network disconnection options, and fallback actions when standard isolation is not possible.


The logic can be represented as a structured flowchart:

{{< mermaid >}}
flowchart TD
    A{Is the equipment infected?} -->|Yes| B[Remove USB drives or external hard drives]
    B --> C{Do I have physical access to the device?}
    C -->|No| D[Block the device on the router/firewall or revoke its IP address]
    C -->|Yes| E{Is the keyboard not working, or is it preventing me from using the graphical interface or opening applications?}
    E -->|Yes| F[1. WiFi hardware switch: Many laptops have a physical switch or Fn+F2/F3/F12 key]
    F --> G{Did you successfully disconnect it from the network?}
    G -->|No| H{Do you have a Faraday bag/box?}
    H -->|No| I[Shut down immediately, disconnect from power, remove battery]
    H -->|Yes| J[Place the device in a Faraday bag/box to block RF and Wi-Fi signals]
    E -->|No| K[1. Remove Ethernet cable, disconnect from Wi-Fi, or disable network adapters]
{{< /mermaid >}}

This decision tree illustrates a key principle: **containment must be adaptive.** The responder's available tools, physical proximity, and the nature of the compromise all shape the correct action. A remote cloud instance requires a different approach than a compromised laptop on a corporate network. Flexibility within a structured framework is the hallmark of a mature incident response program.

## Conclusion

Containment is the pivot point of incident response. Done well, it limits damage, preserves evidence, and creates the conditions for clean eradication and swift recovery. Done poorly, it allows threats to metastasize across the environment. Organizations that invest in containment strategy, document clear processes, align with standards like ISO/IEC 27035, and train their responders with practical decision frameworks will always be better prepared when the inevitable incident occurs.
