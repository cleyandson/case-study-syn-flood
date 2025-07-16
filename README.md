# Security Incident Analysis: Denial of Service (SYN Flood) Attack

<div align="right">
<a href="./README-PT.md">Ver em Português 🇧🇷</a>
</div>

*A practical case study developed during the <a href="https://www.coursera.org/google-certificates/cybersecurity-certificate">Google Cybersecurity Professional Certificate</a>, focused on network log analysis for threat identification and response.*

---

### ⚠️ Important Note on Ethics and Data Security

This project was developed within a 100% controlled and simulated laboratory environment as part of the **Google Cybersecurity Professional Certificate** curriculum.

All data, including logs and packet captures, is entirely fictional. The IP addresses used, such as `192.0.2.1`, `198.51.100.14`, and `203.0.113.0`, are **TEST-NET** blocks, reserved by the IETF (Internet Engineering Task Force) in RFC 5737 specifically for use in documentation and examples.

**No information from real systems, production networks, or confidential user data is exposed in this repository.** The presentation of this data adheres to the best ethical practices of the cybersecurity industry.

---

### Scenario Context

As a security analyst, I was tasked with investigating the cause of a service disruption on a company's web server. Users reported "connection timeout" errors, preventing access to critical business functionalities.

The objective of this project was to use packet analysis techniques to diagnose the issue, document the findings in a technical report, and propose a mitigation plan.

---

### Analysis and Incident Report

The investigation of the network logs revealed that the server was under a **Denial of Service (DoS) attack, specifically a SYN Flood**. The initial packet analysis in Wireshark already indicated a suspicious communication pattern, as seen in the evidence below.

![Evidence from TCP/HTTP Traffic Log](https://github.com/cleyandson/case-study-syn-flood/blob/8fcc6e1ba7d5cbd87151e172fbbf82d8715f9b8f/Documents/log-wireshark.png)

Further analysis confirmed that a single malicious IP address (`203.0.113.0`) was flooding the server with TCP connection requests (`SYN`) without ever completing the handshake.

This tactic exhausted the server's resources, rendering it unable to respond to legitimate user connections. The key evidence confirming the attack included `Connection Timeout` errors and `TCP [RST, ACK]` packets sent to valid clients.

---

### Mitigation and Recommendation Plan

Based on the analysis, an action plan was structured to contain the threat and enhance the infrastructure's resilience:

**Immediate Containment:** Block the source IP address (`203.0.113.0`) at the network firewall to stop the attack immediately.
**Mitigation 1:** Enable **SYN Cookies** on the server's operating system to validate connections before allocating resources.
**Mitigation 2:** Implement **Rate Limiting** policies to limit the number of new connections per second from a single IP address.

---

### Full Report in PDF
* [**Cybersecurity Incident Report**](https://github.com/cleyandson/case-study-syn-flood/blob/2dc1f7343f7beb00c6b281634c6a081930fc81cd/Documents/Cybersecurity%20incident%20report.pdf)

---

### Conclusion

In conclusion, the root cause analysis determined that the incident was a Denial of Service (SYN Flood) attack. The situation was resolved through an immediate containment plan and the recommendation of strategic mitigations.

---
*Conducting this case study reinforces the importance of translating technical evidence into business-oriented actions, demonstrating practical skills in network analysis, incident response, and security planning to protect critical assets.*
