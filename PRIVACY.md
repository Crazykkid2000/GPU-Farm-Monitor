# GPU FARM MONITOR PRIVACY POLICY

**Free Beta Version 0.1**  
Effective Date: 3 October 2026  
Operator: Vincent Fries  
Developer/Project Name: crazykkid2000productions  
Privacy Contact: crazykkid2000productions@gmail.com

GPU Farm Monitor ("GFM," "the Software," "we," "us," or "our") is designed as a local-first application.

This Privacy Policy explains what information GFM stores locally, what information may be visible to a GFM Host Administrator, what information may be transmitted to third-party services, and what information the developer of GFM actually receives.

## 1. Scope

This Privacy Policy applies to the GPU Farm Monitor software, including its:

- Windows host application;
- Windows and Linux client components;
- local or remotely accessible web interface;
- Android application;
- GFM Stream (GFM's streaming app for Android, based on Moonlight). It connects only to the streaming software on the user's own computers;
- scheduler and worker components;
- AI-management features;
- and related GFM software components.

This Policy does not control the independent privacy practices of third-party software, websites, AI-model providers, driver vendors, download providers, or other external services.

## 2. Local-First Design

GFM is designed to operate primarily on computers and networks controlled by the person or organization running the GFM Host.

During ordinary use, GFM does not intentionally send routine farm-management or AI-usage information to servers operated by the GFM developer.

The current release does not include developer-operated advertising tracking or routine usage analytics.

We do not currently operate a centralized GFM cloud service that receives users' routine:

- GPU statistics;
- CPU statistics;
- temperatures;
- fan speeds;
- power readings;
- rig configurations;
- AI prompts;
- chat histories;
- uploaded files;
- AI-generated responses;
- per-user memories;
- AI job queues;
- model activity;
- SSH credentials;
- API keys;
- local filenames;
- or local network topology.

If future versions introduce centralized telemetry, cloud storage, licensing communications, or other new data processing, this Privacy Policy should be updated to describe those changes.

## 3. Information Stored Locally by GFM

Although the developer generally does not receive this information, GFM stores information on the Host system so that its features can operate.

Depending on which features are used, this may include:

- user accounts;
- usernames or display names;
- account permissions and roles;
- chat histories;
- AI prompts;
- AI-generated responses;
- uploaded files;
- per-user memory created from previous chats;
- AI job queues;
- information identifying which user submitted a job;
- rig and machine configuration;
- application settings;
- model configuration;
- tool configuration;
- scheduler information;
- sign-in session records, including device network addresses and times;
- locally generated logs;
- a diagnostic log, in which GFM hides passwords, keys and tokens;
- and related application data.

This information is normally stored within the user-controlled GFM environment rather than in a centralized database operated by the GFM developer.

## 4. Host Administrator Access

GFM supports multiple users.

If you access GFM through a Host operated by someone else, you should understand that the Host Administrator has elevated access.

Through GFM's administration pages, a Host Administrator can see user accounts and roles, sign-in sessions (including each device's network address and times), the administrative audit log, and the farm's job queues with the user who submitted each job.

All information GFM stores, including chats, prompts, uploaded files and per-user memory, is kept in files on the Host computer, so anyone with access to that computer's account and files can read it.

Ordinary users may have more limited visibility into other users' activity.

Do not assume that information submitted through another person's or organization's GFM Host is private from that Host Administrator.

The Host Administrator controls that GFM installation, not the GFM developer.

## 5. Responsibilities of Host Administrators

A person who operates a GFM Host and allows other people to use it is responsible for managing those users appropriately.

Host Administrators are responsible for:

- deciding who may access the Host;
- configuring permissions;
- protecting administrator credentials;
- informing users about administrator visibility;
- securing locally stored information;
- complying with any applicable privacy, employment, monitoring, consent, or recordkeeping requirements;
- and removing user access when it is no longer authorized.

Because the GFM developer normally does not possess information stored only on a privately operated GFM Host, the developer generally cannot access, correct, export, or delete that information.

Users seeking access to or deletion of information stored on a particular GFM Host should contact that Host Administrator.

## 6. Credentials and API Keys

GFM may store sensitive credentials needed to communicate with Managed Systems or external services.

These may include:

- SSH passwords;
- SSH keys;
- API keys;
- authentication tokens;
- or similar credentials.

Where supported, GFM uses operating-system credential-storage or keyring facilities rather than intentionally storing secrets in ordinary plaintext configuration files.

Host Administrators remain responsible for:

- securing the Host operating system;
- restricting account access;
- protecting credentials;
- rotating compromised credentials;
- configuring network security;
- and removing credentials when they are no longer needed.

The GFM developer does not receive SSH credentials or API keys merely because they are stored in a local GFM installation.

## 7. Web and Android Access

GFM may allow authorized users to access a GFM Host through web or Android interfaces.

Information necessary to provide that access may travel between the user's device and the GFM Host.

Under the current architecture, that information is not intentionally routed through a centralized cloud service operated by the GFM developer.

GFM's built-in server uses plain HTTP, which is not encrypted. Use it only on a trusted local network, or place your own HTTPS reverse proxy or VPN in front of it.

Desktop streaming (Sunshine, Moonlight and GFM Stream) goes directly between the user's computers and devices and is not routed through the GFM developer.

If a Host Administrator uses VPN services, reverse proxies, remote-access services, streaming services, or other third-party network infrastructure, those services may process connection or usage information according to their own terms and privacy policies.

## 8. Third-Party Downloads and Internet Connections

GFM can connect to third-party internet services when a user or administrator requests installation, downloading, updating, or related functionality.

Depending on the feature being used, GFM may connect to providers or projects including:

- GitHub;
- Hugging Face;
- NVIDIA;
- AMD;
- Intel;
- PyTorch;
- Node.js;
- Microsoft .NET;
- Microsoft (OpenSSH for Windows, Visual C++ runtime);
- Eclipse Adoptium Java;
- Google Android development resources;
- Parsec;
- public PCI hardware-identification databases;
- Docker Hub (container images for the Python sandbox and SearXNG);
- Linux distribution package repositories;
- public web search engines (through SearXNG);
- and other upstream software or model providers.

When GFM Chat's web search tool is used, search queries, which may be based on your prompts, are sent through the SearXNG service on your own computer to public search engines, and pages it opens are retrieved from their websites.

These connections may disclose information normally associated with an internet request, such as:

- public IP address;
- request time;
- requested file or resource;
- browser, application, or network information;
- and other technical connection details.

These third parties operate independently of GFM and are governed by their own privacy policies and terms.

The GFM developer does not control their privacy practices.

## 9. AI Models

GFM may allow a Host Administrator to download and use third-party AI models.

GFM does not generally distribute those model weights as part of the base GFM application.

AI models may have their own:

- licenses;
- privacy terms;
- acceptable-use requirements;
- commercial restrictions;
- geographic restrictions;
- registration requirements;
- or other conditions.

The Host Administrator is responsible for reviewing applicable model terms before downloading or using a model.

If a user or administrator configures GFM to communicate with an external AI service rather than a locally operated model, information sent to that service may be processed by that provider under its own privacy policy.

## 10. Local Chats, Prompts, Files and Memory

When GFM uses locally operated AI models, chats, prompts, uploaded files, generated responses, per-user memory, and job information remain within the Host environment under the current architecture unless the web search tool is used or the user or administrator configures an external service.

The GFM developer does not routinely receive this information.

Host Administrators may nevertheless have access to information stored on their own GFM installation as described in this Policy.

## 11. Software Downloads and Updates

GFM releases may be distributed through GitHub or another official software-distribution location designated by the developer.

When downloading GFM or updates from a third-party distribution platform, that platform may collect technical information such as IP addresses, request information, account information where applicable, and download activity according to its own privacy policy.

## 12. Support Communications

If you contact the GFM developer for support, bug reporting, questions, or other assistance, we receive whatever information you choose to provide.

This may include:

- your name;
- email address;
- message;
- screenshots;
- logs;
- hardware or software information;
- or files you intentionally submit.

Do not send passwords, private keys, complete API keys, cryptocurrency wallet private keys, or other unnecessary secrets in support requests.

Support communications may be retained as reasonably necessary to:

- respond to your request;
- troubleshoot problems;
- document bugs;
- maintain business records;
- prevent abuse;
- or improve GFM.

## 13. Voluntary Support and Cryptocurrency

GFM may display an option allowing users to voluntarily support continued development.

If a Bitcoin or other cryptocurrency address is provided, transactions to that address may be publicly visible on the relevant blockchain.

Public blockchain information may include:

- wallet addresses;
- transaction identifiers;
- transaction amounts;
- and timestamps.

Blockchain transactions should not be considered private merely because a person's real-world name is not directly displayed.

If you separately provide identifying information concerning a transaction, such as an email address or transaction ID, that information may make it possible to associate you with the transaction.

Voluntary support does not automatically grant commercial-use rights or other software-license rights unless separate terms expressly state otherwise.

## 14. Information We Do Not Sell

We do not sell personal information obtained through the GFM application.

GFM is not operated as an advertising-data collection service.

Third-party software and service providers may process information independently under their own policies.

## 15. Data Retention

Information stored locally by GFM remains on the Host system according to the Host Administrator's:

- configuration;
- storage practices;
- deletion actions;
- backup practices;
- and continued use of GFM.

Because the GFM developer generally does not possess this local data, the developer does not control its retention.

When GFM is uninstalled, the uninstaller asks whether to keep (the default) or permanently remove GFM's data folder and its stored credentials.

Deleting or uninstalling GFM may not automatically delete information contained in:

- backups;
- exported files;
- third-party applications;
- model directories;
- logs stored elsewhere;
- or storage independently controlled by the Host Administrator.

Information voluntarily provided directly to the developer through support or other communications may be retained for as long as reasonably necessary for the purpose for which it was provided, legal compliance, dispute resolution, security, or legitimate recordkeeping.

## 16. Security

GFM is designed to keep routine farm and AI information under the control of the user or Host Administrator.

However, no application, network, operating system, credential-storage system, or internet transmission can be guaranteed completely secure.

Users and Host Administrators are responsible for securing:

- their computers;
- networks;
- accounts;
- passwords;
- SSH keys;
- API keys;
- remote-access configuration;
- and backups.

If you believe information that you provided directly to the GFM developer has been compromised, contact:

crazykkid2000productions@gmail.com

## 17. Children

GFM is a technical system-management and AI-compute application and is not designed or directed specifically toward children under 13.

The GFM developer does not knowingly operate GFM for the purpose of collecting personal information from children under 13.

If a Host Administrator allows a minor to use their GFM installation, that Host Administrator is responsible for complying with applicable parental-consent and privacy requirements.

## 18. Your Privacy Rights

Depending on where you live and what information the GFM developer actually possesses about you, applicable law may provide rights concerning access, correction, deletion, restriction, or other processing of personal information.

Requests concerning information held directly by the GFM developer may be sent to:

crazykkid2000productions@gmail.com

For information stored only on a privately operated GFM Host, contact that Host Administrator.

The GFM developer generally cannot retrieve or delete information that the developer does not possess.

## 19. Third-Party Services

GFM may interact with third-party software, services, repositories, model providers, driver providers, and download platforms.

Those third parties operate under their own licenses, terms, and privacy practices.

The GFM developer is not responsible for the independent privacy practices of those third parties.

## 20. Changes to This Privacy Policy

This Privacy Policy is identified by version number and effective date.

If GFM's data practices materially change, this Policy should be updated.

Examples include introduction of:

- centralized telemetry;
- developer-operated cloud storage;
- crash-report collection;
- commercial license validation;
- account synchronization;
- payment processing;
- or another new category of data processing.

Where appropriate or legally required, material changes may also be presented within GFM.

## 21. Contact

Privacy questions may be directed to:

Vincent Fries  
Developer: crazykkid2000productions  
Email: crazykkid2000productions@gmail.com

---

GPU Farm Monitor Privacy Policy  
Version 0.1 Beta
