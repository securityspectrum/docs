# Welcome to the Security Spectrum Docs

The Security Spectrum platform is a cybersecurity SIEM solution that facilitates the detection and protection of customers' networks against malicious attacks, all while safeguarding the confidentiality of sensitive information contained within event logs.

## Description of the problem

As many cybersecurity SIEM platforms, we rely on many open-source projects to generate cybersecurity event logs such as:

- **Zeek**: Is a free and open-source software network analysis framework
- **OSSEC**: OSSEC is a multiplatform, open source and free Host Intrusion Detection System (HIDS)
- **Suricata**: Suricata is an open-source based intrusion detection system (IDS) and intrusion prevention system (IPS)
- **OpenVAS**: The Open Vulnerability Assessment System, OpenVAS is a comprehensive open-source vulnerability scanning tool and vulnerability management system.
and others. Naturally, these event logs will contain sensitive information such as IP addresses, emails, usernames, hostnames, and more which are visible in clear.

Processing and storing sensitive information in clear is a **security risk**.


## How does it work?

Before going any further, let's describe shortly the terminology we will use.

#### Terminology description

- **Event logs**: The event logs are structured files containing records of event data. They originate from the customer's network which are processed and analyzed to detect any attacks or threats. Please note that our focus is mostly security event logs.
- **Organization**: The organization, the client or the customer are identical in our context.
- **Managed Security Service Provider (MSSP)**: Organization specialized in cybersecurity and which offers cybersecurity  protection services to other organizations.
- **Security Information and Event Management (SIEM)**: A SIEM platform that helps organizations detect and protect against cyber-attacks.

To protect sensitive information, we rely on **encryption mechanisms**. When sensitive data is collected and processed, we believe that it needs to be encrypted as early as possible, before the events leave the customers network. In other words, we are talking about end-to-end encryption (E2EE).

When discussing encryption, a critical question that arises is the following: **Who** possesses to the **decryption key***?

In our threat model, it is only **the customer or the organization** who has access to the secret keys. It is then up to them to decide to whom he wants to provide the decryption keys which will give access to data in clear.


## End-to-end encryption (E2EE)

The privacy protection of sensitive information is achieved using the E2EE. To achieve high processing throughput of the event logs, we use symmetric encryption.

The principal benefits of using E2EE is that our platforms assures that it is **only** the **customer** with the decryption **keys** that is able to decrypt encrypted sensitive information (PIIs).
The owner of the organization can decide to whom he wants to grant access to sensitive information in cleartext by sharing the Data Decryption Key (DEK) to the desired user. This provides an extra layer of protection and gives customers full control over their sensitive data, improving their privacy and security.

## Why privacy?

Why do we care about privacy? We believe that the customer should have control of governance of personal data. As the time goes on, we believe that the importance of **privacy** will only increase as access to information gets easier.


## Why are we doing this?

1. Privacy is important.
2. We believe that a SOC analyst does not need to know all information in cleartext at all times during his investigation time.
3. At the moment of writing, we were unable to find any single SIEM solution on the market which is protecting collected sensitive information with E2EE in the field of cybersecurity.
4. Some organizations are hesitant to move to the cloud infrastructure because they could lose control of their own data.
5. We believe that privacy and protecting sensitive information will make our civilization better.

At Security Spectrum, we have implemented a solution that we believe is challenging, but important, and we are proud to offer a cybersecurity SIEM platform that prioritizes privacy and protecting sensitive information.