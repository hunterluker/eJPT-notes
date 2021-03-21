# Vulnerability Assesment

A vulnerability assessment is a review of security weaknesses in an information system. It evaluates if the system is susceptible to any known vulnerabilities, assigns severity levels to those vulnerabilities, and recommends remediation or mitigation, if and whenever needed. 

### Nessus

Nessus is a popular and powerful vulnerability scanner.

Examples of vulnerabilities and exposures Nessus can scan for include:

- Vulnerabilities that could allow unauthorized control or access to sensitive data on a system.
- Misconfiguration of software suites, files on the operating system, network devices...
- Default passwords, a few common passwords, and blank/absent passwords on some system accounts. Nessus can also call Hydra (an external tool) to launch a dictionary attack.
- Denial of service vulnerabilities


Running Kali you should be able to start Nessus with the command below and visiting https://kali:8834 to configure the scan
```
service nessud start
```


