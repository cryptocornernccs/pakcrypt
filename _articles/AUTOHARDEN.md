---
layout: post
title: "AUTOHARDEN: A Comprehensive Hardening Framework for Connected Vehicle Cybersecurity"
subtitle: "From Attack Surface Taxonomy to Implementable Hardening Controls"
date: 2026-03-29
authors:
  - name: Ji Won
    affiliation: PakCrypt NPO, Islamabad, Pakistan
    email: won@pakcrypt.org
  - name: Naveed A. A.
    affiliation: PakCrypt NPO, Islamabad, Pakistan
categories: [automotive-security, cybersecurity, research]
tags: [vehicle-hardening, CAN-bus, attack-surface, nation-state-threat, ISO-21434, UNECE-WP29, defense-in-depth, hardening-benchmark, connected-vehicle, AUTOHARDEN]
toc: true
---

## Abstract

The hardening of information and communications technology (ICT) assets---servers, workstations, network devices---against known attack vectors is a mature discipline with well-established benchmarks (CIS Benchmarks, DISA STIGs, NIST SP 800-123). No comparable, actionable hardening regime exists for connected vehicles, despite a decade of research demonstrating that modern automobiles are susceptible to remote compromise, safety-critical system manipulation, persistent surveillance, and supply chain subversion. This paper bridges that gap. We first formalize a comprehensive *Attack Surface Taxonomy (AST)* for connected vehicles, organized across seven architectural layers: Physical Bus, Electronic Control Unit (ECU), Wireless Interface, Diagnostic Protocol, External Connectivity, Application/Cloud Backend, and Aftermarket/Third-Party Device. Drawing on 158 documented vulnerabilities and attack demonstrations from 2010--2026---including the Miller--Valasek Jeep Cherokee remote exploit, Keen Security Lab's multi-year Tesla campaign, CAN injection car theft epidemics, and 76 zero-days from Pwn2Own Automotive 2026---we derive a systematic *Vehicle Hardening Framework (VHF)* comprising 94 implementable controls mapped to the UNECE WP.29 R155 threat catalogue and ISO/SAE 21434 risk assessment methodology. Each control specifies applicability (OEM, fleet operator, or end-user), implementation tier (Essential, Enhanced, Maximum), verification method, and mapping to demonstrated attack vectors. We instantiate the framework as AUTOHARDEN, a prescriptive hardening benchmark for passenger vehicles analogous to a CIS Benchmark for Ubuntu Linux. We further present a dedicated threat model for *nation-state adversaries targeting high-value individuals* through vehicular attack surfaces, analyzing supply chain infiltration, cellular network exploitation, backend server compromise, and physical implant scenarios. We argue that connected vehicles now constitute the least-hardened node in the personal digital ecosystem of any individual under state-level surveillance, and that systematic hardening is both technically feasible and operationally urgent.

**Keywords:** Automotive cybersecurity , Vehicle hardening , CAN bus security , Attack surface taxonomy , Connected vehicle , Nation-state threat , ISO/SAE 21434 , UNECE WP.29 , Defense-in-depth , Hardening benchmark

## 1. Introduction

The practice of hardening ICT assets---systematically reducing the attack surface of a computing system by disabling unnecessary services, enforcing least-privilege access, applying cryptographic controls, and validating configurations against known vulnerability databases---is a cornerstone of defensive cybersecurity. Organizations harden Ubuntu servers against CIS Benchmark 1.0.0 (446 controls), Windows endpoints against DISA STIGs, and network appliances against vendor-specific security configuration guides. The methodology is well understood: enumerate the attack surface, catalogue known exploitation techniques, derive defensive controls that eliminate or mitigate each vector, prioritize controls by risk and implementation cost, and provide machine-auditable verification procedures.

No equivalent methodology exists for the connected vehicle. This is a remarkable omission. Modern passenger vehicles contain 70--150+ Electronic Control Units (ECUs) interconnected by Controller Area Network (CAN) buses designed without authentication, encryption, or source addressing. They maintain persistent cellular connections through Telematics Control Units (TCUs), expose Bluetooth, Wi-Fi, USB, and RF interfaces through infotainment and keyless entry systems, and increasingly communicate with infrastructure and other vehicles via V2X protocols. The OBD-II diagnostic port provides direct electrical access to the CAN bus, and a thriving aftermarket ecosystem connects third-party devices---insurance dongles, GPS trackers, fleet management units---with minimal or no security validation.

The consequences of this architectural insecurity have been demonstrated repeatedly. In 2015, Miller and Valasek remotely compromised a Jeep Cherokee via its cellular-connected head unit, achieving full control of brakes, steering, transmission, and engine from across the internet---triggering the first cybersecurity-driven automotive recall of 1.4 million vehicles [1]. Tencent Keen Security Lab conducted a four-year campaign (2016--2019) against Tesla vehicles, achieving remote brake control from 12 miles, Autopilot manipulation via adversarial road markings, and bypass of firmware code signing [2, 3]. CAN injection car theft---where attackers access CAN bus wiring through headlight connectors and inject frames impersonating the key fob ECU---accounted for 58% of UK vehicle thefts in 2023--2024 [4]. Pwn2Own Automotive 2026 yielded 76 unique zero-day vulnerabilities across vehicle infotainment systems, EV chargers, and operating systems [5].

For high-value individuals under nation-state surveillance---diplomats, intelligence officers, military commanders, political leaders, journalists, and dissidents---the connected vehicle represents perhaps the least-hardened node in their personal digital ecosystem. While such individuals may use encrypted communications, hardened mobile devices, and secured workstations, their vehicles maintain persistent cellular connections, contain always-on microphones and cameras, broadcast continuous GPS telemetry, and store paired phone data---all accessible through demonstrated remote exploitation chains or physical access during routine servicing.

This paper makes the following contributions:

**1. Attack Surface Taxonomy (AST).** We formalize a seven-layer taxonomy of the connected vehicle attack surface, cataloguing 94 distinct attack vectors with demonstrated proof-of-concept references, organized by architectural layer and access modality (remote, proximity, physical).

**2. Vehicle Hardening Framework (VHF).** We derive a systematic set of 94 hardening controls---each mapped one-to-one to a catalogued attack vector---with implementation tiers (Essential, Enhanced, Maximum), responsible parties (OEM, fleet operator, end-user), and verification methods.

**3. AUTOHARDEN Benchmark.** We instantiate the VHF as a prescriptive, auditable benchmark analogous to CIS Benchmarks for operating systems, providing specific configuration directives and pass/fail criteria.

**4. Nation-State Threat Model.** We present a dedicated adversary model for state-level actors targeting vehicles of high-value individuals, analyzing attack feasibility across supply chain, cellular network, cloud backend, and physical access vectors.

The remainder of this paper is organized as follows. Section 2 surveys related work. Section 3 describes the generic vehicle electronic architecture from a security perspective. Section 4 presents the Attack Surface Taxonomy. Section 5 introduces the Vehicle Hardening Framework methodology. Section 6 details hardening controls across all seven layers. Section 7 addresses third-party device hardening. Section 8 develops the nation-state threat model. Section 9 proposes a maturity model and implementation roadmap. Section 10 discusses limitations, and Section 11 concludes.

## 2. Related Work

The foundational vehicle security research was conducted by Koscher, Checkoway, et al. in two seminal papers: "Experimental Security Analysis of a Modern Automobile" (IEEE S&P 2010) [6] demonstrated that infiltrating any single ECU enables complete circumvention of safety-critical vehicle systems through CAN bus message injection, while "Comprehensive Experimental Analyses of Automotive Attack Surfaces" (USENIX Security 2011) [7] proved remote exploitation feasible via cellular radio, Bluetooth, and CD-based media, enabling long-distance vehicle tracking and in-cabin audio exfiltration. These papers established that vehicle security is an architectural problem---not merely a peripheral concern.

Miller and Valasek's multi-year program on Jeep Cherokee (2013--2016) [1, 8] translated these findings into public consciousness and regulatory action, demonstrating full remote vehicle control via the Sprint cellular network and directly catalyzing NHTSA's 2016 Cybersecurity Best Practices for Modern Vehicles [9] and the SPY Car Act. Their 2016 follow-up demonstrated steering wheel turns of 90 degree at highway speed, unintended acceleration, and complete brake disablement [10].

On the standards front, ISO/SAE 21434:2021 [11] provides a process framework for cybersecurity engineering across the vehicle lifecycle, mandating Threat Analysis and Risk Assessment (TARA), supply chain cybersecurity requirements, and incident response. UNECE WP.29 R155 [12] provides regulatory enforcement, requiring a certified Cybersecurity Management System (CSMS) for vehicle type approval in 54+ markets as of July 2024. R155 Annex 5 catalogues 69 threat types and 29 mitigation categories. However, neither standard provides implementation-level hardening directives---they specify what must be addressed, not how to configure specific vehicle subsystems.

The CIS (Center for Internet Security) Benchmarks [13] provide the closest ICT analogy to our work. A CIS Benchmark for Ubuntu Linux 24.04 contains 446 scored and unscored recommendations, each specifying a configuration directive, rationale, audit procedure, and remediation command. DISA STIGs (Security Technical Implementation Guides) serve a comparable function for U.S. Department of Defense systems [14]. NIST SP 800-123 [15] provides general server hardening guidance. No equivalent benchmark exists for vehicles. The SAE J3061 Cybersecurity Guidebook (2016) [16], while valuable, predates ISO/SAE 21434 and focuses on process rather than implementable controls. Upstream Security's annual reports [17] provide threat intelligence and incident tracking but not hardening prescriptions. The I Am The Cavalry "Five Star Automotive Cyber Safety Framework" (2015) [18] offered high-level recommendations but without the technical depth required for implementation.

Our contribution differs from prior work in three respects: (a) we derive hardening controls directly from a systematic enumeration of demonstrated attack vectors rather than abstract threat categories; (b) we provide implementation-level specificity comparable to CIS Benchmarks; and (c) we explicitly model the nation-state adversary targeting high-value individuals---a threat class largely absent from existing automotive cybersecurity literature, which focuses predominantly on criminal theft, ransomware, and safety-motivated attacks.

## 3. Generic Vehicle Electronic Architecture

To derive a universal hardening framework, we first establish a generic reference architecture that captures the common security-relevant structure across manufacturers. While OEM implementations vary in detail, the fundamental topology is remarkably consistent across the global vehicle fleet.

### 3.1. In-Vehicle Network Topology

The canonical architecture comprises multiple CAN bus segments organized by functional domain, interconnected through a Central Gateway ECU. We identify six primary network domains relevant to security analysis:

***Powertrain Domain (CAN-P).*** High-speed CAN (500 kbps) connecting the Engine Control Module (ECM), Transmission Control Module (TCM), and---in hybrid/electric vehicles---the Battery Management System (BMS) and Motor Control Unit (MCU). This domain controls vehicle propulsion and is the primary target for sabotage attacks.

***Chassis Domain (CAN-C).*** High-speed CAN connecting the Anti-lock Braking System / Electronic Stability Control (ABS/ESC), Electronic Power Steering (EPS), active suspension, and airbag Supplemental Restraint System (SRS). Direct control of braking and steering makes this the highest-consequence domain for safety attacks.

***Body Domain (CAN-B).*** Lower-speed CAN (125--250 kbps) with the Body Control Module (BCM) managing door locks, windows, exterior lighting, HVAC, wipers, and horn. Compromise enables physical access (door unlock) and distraction attacks.

***Infotainment Domain (CAN-I / Automotive Ethernet).*** The In-Vehicle Infotainment (IVI) head unit, instrument cluster, telematics control unit (TCU), and connectivity modules (Bluetooth, Wi-Fi, cellular). Increasingly migrating to Automotive Ethernet (100BASE-T1 / 1000BASE-T1) with IP-based protocols (DoIP, SOME/IP). This domain concentrates the majority of external-facing interfaces and is the primary entry point for remote attacks.

***ADAS Domain.*** Forward-facing camera, radar modules, LiDAR (where equipped), ultrasonic sensors, and the ADAS ECU performing sensor fusion and automated driving functions. Dedicated high-bandwidth Automotive Ethernet is common for camera data. Sensor spoofing attacks target this domain to manipulate autonomous driving decisions.

***Auxiliary Bus Systems.*** LIN (Local Interconnect Network, <=20 kbps) for low-priority peripherals (seat motors, mirror adjustment, rain sensors); MOST (Media Oriented Systems Transport, up to 150 Mbps) for legacy multimedia; FlexRay (up to 10 Mbps, deterministic) for steer-by-wire in select vehicles.

### 3.2. External Interface Enumeration

We enumerate the complete set of externally accessible interfaces present in the generic architecture, each representing a potential entry point for attack:

| Interface | Protocol/Frequency | Range | CAN Path |
| --- | --- | --- | --- |
| TCU Cellular Modem | 4G LTE / 5G NR | Global (IP) | Gateway -> CAN-P/C/B |
| IVI Bluetooth | BT Classic / BLE 5.x | ~100 m | IVI -> Gateway |
| IVI Wi-Fi | 802.11 a/b/g/n/ac | ~50 m | IVI -> Gateway |
| IVI USB | USB 2.0/3.0 | Physical | IVI -> Gateway |
| OBD-II Port | CAN 2.0 (Pins 6,14) | Physical | Direct bus access |
| PKES Key Fob | 125 kHz LF / 315--433 MHz UHF | ~5--100 m | BCM -> CAN-B |
| TPMS Sensors | 315/433 MHz ASK/FSK | ~40 m | TPMS ECU -> CAN-B |
| V2X Module | DSRC 5.9 GHz / C-V2X | ~300--1000 m | V2X ECU -> Gateway |
| GPS/GNSS Receiver | L1/L2/L5 bands | Satellite | TCU/IVI internal |
| EV Charge Port | ISO 15118 PLC | Physical | Charge ECU -> CAN |
| eCall Module | Cellular (mandated EU) | Global | Independent ECU |
| UWB Anchors | 802.15.4z | ~10 m | BCM -> CAN-B |

**Table 1.** Complete external interface enumeration for the generic vehicle architecture. CAN Path indicates the route from the external interface to the internal CAN bus network.*

### 3.3. The Central Gateway: Security-Critical Chokepoint

The Central Gateway ECU serves as the architectural firewall between untrusted domains (infotainment, external interfaces) and trusted domains (powertrain, chassis). It performs CAN-to-CAN routing, protocol translation (CAN <-> Ethernet <-> LIN), message filtering, and rate limiting. Ideally, the gateway enforces a strict security policy: infotainment CAN frames must never propagate to powertrain or chassis CAN buses. In practice, research has revealed critical weaknesses. NDSS VehicleSec 2024 demonstrated that gateways universally whitelist all UDS (Unified Diagnostic Services) diagnostic messages, creating a protocol-level bypass of network segmentation [19]. The 2015 Jeep Cherokee exploit leveraged the head unit's SPI connection to the gateway's V850 microcontroller to achieve CAN bus access [1]. BMW's Central Gateway Module was compromised through a logic flaw that permitted arbitrary UDS diagnostic messages to powertrain and body CAN buses via a compromised TCU [20].

## 4. Attack Surface Taxonomy

We organize the connected vehicle attack surface into seven architectural layers, inspired by the OSI model's layered abstraction but adapted to vehicular systems. For each layer, we enumerate specific attack vectors, cite demonstrated proof-of-concept implementations, and assign a composite risk score based on exploitability (access complexity, skill required) and impact (confidentiality, integrity, availability, safety). This taxonomy serves as the systematic foundation from which hardening controls are derived in Section 6.

### 4.1. Layer 1: Physical Bus Layer

This layer encompasses attacks that exploit the electrical and protocol characteristics of in-vehicle communication buses, principally CAN 2.0A/B, CAN FD, LIN, and FlexRay. The CAN protocol's architectural deficiencies---no authentication, no encryption, broadcast topology, priority-based arbitration without source addressing---render it fundamentally vulnerable to any attacker with bus access.

**V-1.1: CAN Message Injection/Spoofing.** Transmission of crafted CAN frames with target function IDs to actuate safety-critical systems. Demonstrated: Miller--Valasek (brakes, steering, engine) [1]; Koscher et al. (all subsystems) [6]; CAN injection car theft via headlight wiring (Toyota RAV4, Lexus, Land Rover, Hyundai) [4, 21].

**V-1.2: CAN Bus Denial-of-Service.** Flooding the bus with highest-priority frames (ID 0x000), winning all arbitration contests and starving legitimate ECU communication. Demonstrated: multiple academic implementations using Arduino + MCP2515 CAN shield [6, 22].

**V-1.3: CAN Bus-Off Attack.** Manipulating CAN error handling to force a target ECU's Transmit Error Counter above 255, triggering permanent Bus-Off state (IEEE 802.3 analogue: network partitioning). CISA ICS-ALERT-17-209-01 [23]. Selective ECU silencing enables replacement of legitimate messages with attacker-controlled alternatives.

**V-1.4: CAN Traffic Eavesdropping.** Passive monitoring of all CAN bus traffic, which is transmitted in cleartext broadcast. Enables reverse engineering of proprietary CAN databases (DBC files), extraction of vehicle state data (speed, RPM, steering angle, GPS coordinates), and reconnaissance for targeted injection attacks.

**V-1.5: CAN Frame Replay.** Capture and retransmission of legitimate CAN frames at a later time. Trivially feasible because CAN lacks sequence numbers, timestamps, or freshness values. canplayer from Linux can-utils provides turnkey replay capability [22].

### 4.2. Layer 2: ECU Layer

This layer addresses vulnerabilities in the ECUs themselves---their firmware, boot processes, debug interfaces, and update mechanisms.

**V-2.1: ECU Firmware Extraction.** Extracting firmware via JTAG/SWD debug interfaces, UART consoles, or SPI flash chip reading (using tools such as Bus Pirate, J-Link, or ChipWhisperer). Enables reverse engineering of proprietary protocols, cryptographic key extraction, and vulnerability discovery. The I-CAN-hack team extracted SecOC keys from a Toyota RAV4 Prime's EPS ECU in seconds via an unprotected bootloader [24].

**V-2.2: Unsigned/Weakly-Signed Firmware Updates.** Installation of malicious firmware on ECUs that do not cryptographically verify update authenticity. Tesla Model X key fob BLE firmware updates lacked code signing (CVE-2020-29438) [25]. The Zubie fleet management dongle accepted firmware via rogue cellular tower without validation [26].

**V-2.3: UDS Security Access Bypass.** Circumventing the UDS SecurityAccess (0x27) challenge--response mechanism through hardcoded secrets, predictable seed generation, brute-forceable key spaces, or XOR-based algorithms with recoverable keys. Enables entry to programming sessions, arbitrary ECU reprogramming, and direct I/O control via InputOutputControlByIdentifier (0x2F) [19, 27].

**V-2.4: Bootloader Exploitation.** Compromise of the secure boot chain through unsigned first-stage bootloaders, RSA verification bypass (fault injection, Bellcore attack), or fallback to recovery modes that disable security. Once the bootloader is compromised, all subsequent firmware validation is meaningless.

**V-2.5: Side-Channel Attacks on Automotive HSMs.** Differential Power Analysis (DPA), electromagnetic emanation analysis, and timing attacks against Hardware Security Modules used for key storage and cryptographic operations. Demonstrated against KeeLoq cipher (EUROCRYPT 2008), Hitag2 (USENIX Security 2012), and AES implementations in SHE-compliant modules.

### 4.3. Layer 3: Wireless Interface Layer

This layer encompasses all radio-frequency attack vectors accessible without physical vehicle contact.

**V-3.1: PKES Relay Attack.** Real-time relay of the 125 kHz LF challenge and UHF response between car and key fob using two accomplices with relay equipment ($10--30). Demonstrated against virtually all PKES-equipped vehicles (BMW, Mercedes, Audi, Toyota, Tesla) [28, 29].

**V-3.2: Rolling Code Replay (RollJam/RollBack).** Simultaneous jamming and capture of RKE signals to steal valid rolling codes. RollJam (DEF CON 23, 2015) provides single-use access; RollBack (2022) exploits resynchronization windows for permanent access. Honda CVE-2022-27254 revealed complete absence of rolling codes in 2016--2020 Civic [30, 31].

**V-3.3: BLE Relay/Proximity Attack.** Link-layer relay of BLE phone-as-a-key communication, bypassing encryption and application-level protections. NCC Group demonstrated on Tesla Model 3 (May 2022), unlocking and starting the vehicle with the owner's phone 25 meters away [32].

**V-3.4: TPMS Eavesdropping and Spoofing.** Interception of unencrypted, unauthenticated TPMS transmissions (315/433 MHz) for vehicle tracking (unique 32-bit sensor IDs) or injection of false pressure readings to trigger driver distraction. Rouf et al. (USENIX Security 2010) demonstrated at 40+ meters [33]. Synacktiv (Pwn2Own 2024) achieved RCE via TPMS->VCSEC integer overflow (CVE-2025-2082) [5].

**V-3.5: GPS/GNSS Spoofing.** Overriding legitimate satellite navigation signals with stronger spoofed signals from SDR-based transmitters, causing route deviation, incorrect position reporting, and potential lane departure in vehicles relying on GPS for navigation-assisted ADAS functions [34].

**V-3.6: Cellular Network Exploitation.** Attacking the TCU's cellular connection via rogue base stations (IMSI catchers), SS7/Diameter signaling protocol exploitation (interception, location tracking, traffic redirection), or exploitation of the TCU's embedded web server/IP services. BMW's TCU was remotely compromised via a fake GSM base station delivering HTTP payloads [20]; Jeep's head unit exposed open port 6667 on the Sprint cellular network [1].

### 4.4. Layer 4: Diagnostic Protocol Layer

**V-4.1: OBD-II Direct Bus Access.** The OBD-II connector provides direct electrical access to CAN bus via pins 6 (CAN_H) and 14 (CAN_L) with +12V power (pin 16). Any device connected to the port can read all CAN traffic and inject arbitrary frames. Physical access to the port (typically beneath the dashboard) requires only seconds [22, 35].

**V-4.2: UDS Diagnostic Abuse.** Exploitation of legitimate diagnostic services for malicious purposes: RoutineControl (0x31) to invoke arbitrary ECU routines, WriteDataByIdentifier (0x2E) to modify calibration data, RequestDownload (0x34) / TransferData (0x36) to flash malicious firmware. NDSS VehicleSec 2024 demonstrated that gateway ECUs whitelist all UDS traffic [19].

**V-4.3: DoIP (Diagnostics over IP) Remote Access.** As vehicles migrate to Automotive Ethernet, diagnostic access via DoIP (ISO 13400) over TCP/IP introduces network-reachable diagnostic capabilities. Misconfigured DoIP servers or weak authentication expose UDS services to IP-based attackers.

### 4.5. Layer 5: External Connectivity Layer

**V-5.1: IVI Head Unit Compromise.** Exploitation of the Linux/QNX/Android-based infotainment system through browser vulnerabilities (WebKit CVEs), media codec flaws (malicious MP3/MP4/USB media), Bluetooth stack vulnerabilities, or USB-based attacks. The Jeep Cherokee's head unit ran D-Bus IPC as root without authentication [1]. Harman's QNX-based units have been compromised through multiple vectors across BMW, FCA, and other OEMs.

**V-5.2: TCU Remote Exploitation.** Direct compromise of the Telematics Control Unit via its cellular interface, targeting the embedded Linux/RTOS, AT command interface, or exposed IP services. The TCU is the most consequential remote attack vector because it is always online and connects to the CAN bus via the gateway [1, 20].

**V-5.3: OTA Update Mechanism Compromise.** Man-in-the-middle attacks on over-the-air firmware updates, exploitation of update server infrastructure, or rollback attacks installing older vulnerable firmware. Formal verification of the Uptane framework (RAID 2024) revealed 6 previously unknown specification vulnerabilities [36].

**V-5.4: Connected Car Mobile App API Exploitation.** Compromise of OEM mobile applications and their backend APIs. Sam Curry (2022--2023) demonstrated that API vulnerabilities in 16 major manufacturers (including Hyundai, Kia, BMW, Mercedes, Ferrari, Porsche) allowed full remote vehicle control, account takeover, and fleet-wide data access using only VIN numbers [37].

**V-5.5: EV Charging Communication Attacks.** The Brokenwire attack (2022) demonstrated wireless disruption of CCS DC fast charging at 47 meters with <1W using SDR [38]. Baker and Martinovic (2019) achieved 91.8% message recovery from unencrypted HomePlug Green PHY PLC [39]. Pwn2Own Automotive 2024 yielded 29 zero-days in EV chargers [5].

### 4.6. Layer 6: Application and Cloud Backend Layer

**V-6.1: Telematics Backend Server Compromise.** Exploitation of OEM cloud infrastructure that communicates with vehicle TCUs, providing fleet-wide command-and-control capability. Spireon (15.5 million vehicles) was vulnerable to SQL injection granting full administrative access [37].

**V-6.2: Vehicle Data Exfiltration.** Extraction of sensitive telemetry, location history, paired phone data (contacts, call logs, SMS), voice command recordings, and cabin camera footage from OEM cloud services or compromised vehicles. Mozilla Foundation (2023) rated cars as the worst product category for privacy [40].

**V-6.3: V2X Infrastructure Attacks.** Sybil attacks (fake vehicle identities), ghost vehicle injection via spoofed Basic Safety Messages (BSMs), and PKI infrastructure compromise. C-V2X's Semi-Persistent Scheduling algorithm enables predictable jamming of target vehicles [41].

### 4.7. Layer 7: Aftermarket/Third-Party Device Layer

**V-7.1: OBD-II Dongle Exploitation.** "Plug-N-Pwned" (USENIX Security 2020) tested all 77 Amazon US OBD-II dongles: 100% had >=2 vulnerabilities, 85% lacked authentication, 67.53% failed to filter dangerous CAN messages [35]. Bosch Drivelog Connector---Bluetooth brute-force -> CAN injection -> engine stop [42].

**V-7.2: GPS Tracker Compromise.** MiCODUS MV720: hardcoded API key (CVE-2022-2107), default password "123456" in 94.5% of devices, MITM redirect command (CVE-2022-2141)---1.5 million devices in 169 countries [43].

**V-7.3: Aftermarket Head Unit Exploitation.** Android-based aftermarket units running outdated kernels (Dirty COW exploitable), forcing USB debugging, side-loading exfiltration APKs onto paired phones. CarlinKit and 70mai dashcams with hardcoded credentials and RCE (CVE-2025-2763/2764/2765) [44].

## 5. The Vehicle Hardening Framework (VHF)

### 5.1. Design Principles

The VHF is designed around five principles drawn from established ICT hardening practice, adapted to the constraints of vehicular systems:

**P1: Attack-Vector-Driven Derivation.** Every hardening control is derived from, and traceable to, a specific demonstrated attack vector in the AST. Controls without a corresponding demonstrated vulnerability are excluded to maintain empirical grounding.

**P2: Defense in Depth.** No single control is assumed sufficient. Each attack vector is addressed by controls at multiple architectural layers (analogous to network segmentation + host-based firewall + application-level authentication in ICT).

**P3: Implementability.** Controls specify concrete technical actions (e.g., "Disable JTAG fuses on all production ECUs") rather than abstract objectives (e.g., "ensure adequate protection of debug interfaces").

**P4: Tiered Implementation.** Recognizing that implementation cost and feasibility vary, each control is assigned to one of three tiers: Essential (minimum baseline, all vehicles), Enhanced (recommended for connected/autonomous vehicles), and Maximum (required for vehicles of high-value individuals under nation-state threat).

**P5: Responsible Party Assignment.** Each control designates the party responsible for implementation: OEM (vehicle manufacturer, at design/production), Fleet Operator (fleet management, at deployment), or End-User (vehicle owner/driver, at operation). This recognizes that vehicle security is a shared responsibility model, analogous to cloud security's shared responsibility between provider and customer.

### 5.2. Control Structure

Each AUTOHARDEN control is specified using the following structure, modeled on CIS Benchmark recommendation format:

| Field | Description |
| --- | --- |
| Control ID | Hierarchical identifier: AH-{Layer}.{Sequence} (e.g., AH-1.01) |
| Title | Concise imperative statement of the required action |
| Addresses | AST vector(s) mitigated (e.g., V-1.1, V-1.5) |
| Tier | Essential (E) / Enhanced (N) / Maximum (M) |
| Responsible Party | OEM / Fleet Operator / End-User |
| Rationale | Technical justification referencing demonstrated attacks |
| Implementation | Specific technical actions required |
| Verification | Audit procedure to confirm control implementation |
| WP.29 Mapping | Corresponding UNECE R155 Annex 5 threat/mitigation ID |

**Table 2.** AUTOHARDEN control specification structure.*

## 6. Hardening Controls by Architectural Layer

We present representative controls for each layer. The complete benchmark contains 94 controls; due to space constraints, we detail the highest-priority controls and summarize the remainder.

### 6.1. Layer 1 Controls: Physical Bus Hardening

**AH-1.01: Deploy Authenticated CAN Communication (SecOC).** *[Addresses V-1.1, V-1.5] [Tier: Essential] [OEM]*

Implement AUTOSAR Secure Onboard Communication (SecOC) with AES-128-CMAC message authentication codes and monotonic freshness counters on all safety-critical CAN messages (powertrain and chassis domains at minimum). Keys must be stored in hardware security modules (HSMs), not in firmware flash. Toyota's initial SecOC deployment on the RAV4 Prime was compromised because keys were stored in the EPS ECU's firmware rather than an HSM [24]; this control mandates HSM-backed key storage.

***Verification:*** Capture CAN bus traffic using oscilloscope or CAN analyzer (e.g., Vector CANalyzer); verify that all safety-critical message IDs include MAC fields and incrementing freshness values. Attempt injection of unauthenticated frames on safety-critical IDs and confirm rejection by receiving ECUs.

**AH-1.02: Implement CAN Bus Intrusion Detection System.** *[Addresses V-1.1, V-1.2, V-1.3] [Tier: Essential] [OEM]*

Deploy an anomaly-based CAN IDS on each bus segment, monitoring for: (a) unexpected CAN IDs not in the authorized whitelist; (b) abnormal message frequencies (injection attacks increase message rates); (c) timing deviations from known ECU transmission patterns (clock-skew fingerprinting); (d) bus error rate anomalies indicative of bus-off attacks. Detection events must generate alerts to the vehicle SOC via the TCU and log to tamper-resistant storage.

***Verification:*** Inject anomalous CAN frames via a test harness on each bus segment and confirm IDS detection, alerting, and logging within specified latency bounds.

**AH-1.03: Enforce Network Segmentation with Strict Gateway Filtering.** *[Addresses V-1.1, V-1.4] [Tier: Essential] [OEM]*

Configure the Central Gateway ECU with a default-deny routing policy. Only explicitly whitelisted CAN message IDs may traverse domain boundaries. The gateway must block all CAN frames originating from the infotainment domain from reaching powertrain or chassis domains, with no blanket exceptions for diagnostic protocols. UDS diagnostic routing must require authenticated session establishment (see AH-4.01).

***Verification:*** Transmit non-whitelisted CAN frames from the infotainment bus segment toward powertrain/chassis segments and confirm gateway drops. Enumerate all gateway routing rules and verify against authorized whitelist.

**AH-1.04: Disable Unused Bus Segments and Terminate CAN Lines.** *[Addresses V-1.1, V-1.4] [Tier: Enhanced] [OEM]*

Remove or electrically isolate unused CAN bus stubs, development test points, and diagnostic connectors accessible from the vehicle exterior (e.g., headlight, taillight, and bumper-area wiring harnesses). Apply tamper-evident seals on all accessible CAN bus junction points. For the headlight CAN injection vector specifically: implement a dedicated headlight sub-bus with a microcontroller gateway that only passes legitimate lighting commands [21].

### 6.2. Layer 2 Controls: ECU Hardening

**AH-2.01: Enforce Secure Boot with HSM-Rooted Chain of Trust.** *[Addresses V-2.2, V-2.4] [Tier: Essential] [OEM]*

All ECUs must implement a hardware-rooted secure boot chain: immutable first-stage bootloader in ROM verifies the second-stage bootloader's RSA-2048/ECDSA-P256 signature against a public key stored in OTP (one-time programmable) fuses; each subsequent stage verifies the next. Boot must halt on any signature verification failure. Rollback protection via monotonic version counters in OTP prevents installation of older, vulnerable firmware versions.

**AH-2.02: Disable Production Debug Interfaces.** *[Addresses V-2.1] [Tier: Essential] [OEM]*

Permanently disable JTAG, SWD, UART, and SPI debug interfaces on all production ECUs by blowing silicon-level lock fuses (e.g., Renesas RH850 OPBT security fuse, NXP S32K secure JTAG lock, Infineon AURIX debug port protection). Debug access for authorized service must use authenticated challenge--response via HSM (not static passwords or bypass sequences).

**AH-2.03: Implement Runtime Integrity Monitoring.** *[Addresses V-2.2, V-2.4] [Tier: Enhanced] [OEM]*

Deploy Trusted Execution Environment (TEE) or ARM TrustZone-based runtime integrity verification on safety-critical ECUs. Periodically hash firmware memory regions and compare against reference values stored in HSM-protected secure storage. Deviation triggers alert and controlled safe-state transition.

**AH-2.04: Enforce Cryptographic Key Management via HSM.** *[Addresses V-2.5] [Tier: Essential] [OEM]*

All cryptographic keys (SecOC CMAC keys, TLS private keys, firmware signing keys, UDS SecurityAccess secrets) must be generated, stored, and used exclusively within automotive-grade HSMs (SHE, EVITA Full, or SAE J3101 compliant). Keys must never exist in plaintext outside the HSM boundary. Key provisioning must occur during secure manufacturing with per-vehicle unique key material derived from OEM root keys.

### 6.3. Layer 3 Controls: Wireless Interface Hardening

**AH-3.01: Deploy UWB Distance-Bounding for Keyless Entry.** *[Addresses V-3.1, V-3.3] [Tier: Essential] [OEM]*

Replace or supplement LF/UHF PKES and BLE phone-as-a-key systems with Ultra-Wideband (IEEE 802.15.4z) distance-bounding. UWB's time-of-flight measurement with ~10 cm accuracy is resistant to relay attacks because the speed-of-light propagation delay cannot be reduced by a relay. The CCC (Car Connectivity Consortium) Digital Key 3.0 specification provides the interoperability framework. Apple, Samsung, BMW, and Tesla have begun deployment.

***Verification:*** Attempt relay attack using LF/UHF relay equipment and confirm vehicle rejects authentication when the key is outside UWB distance-bounding threshold (typically <2 meters).

**AH-3.02: Encrypt and Authenticate TPMS Communication.** *[Addresses V-3.4] [Tier: Enhanced] [OEM]*

Implement AES-128-CCM authenticated encryption on TPMS sensor transmissions with per-sensor unique keys provisioned during tire mounting. Replace static 32-bit sensor IDs with rotating pseudonymous identifiers that change on a configurable interval to prevent vehicle tracking. Note: this requires replacement of legacy TPMS sensors and receiver ECU firmware updates.

**AH-3.03: Implement GNSS Anti-Spoofing.** *[Addresses V-3.5] [Tier: Enhanced] [OEM]*

Deploy multi-constellation GNSS receivers (GPS + Galileo + GLONASS) with receiver autonomous integrity monitoring (RAIM), signal consistency checking (cross-validation between constellations), inertial navigation system (INS) fusion for dead-reckoning verification, and---where available---Galileo Open Service Navigation Message Authentication (OSNMA). Alert the driver and ADAS systems when spoofing indicators are detected.

**AH-3.04: Harden Cellular Modem Configuration.** *[Addresses V-3.6] [Tier: Essential] [OEM]*

Configure the TCU's cellular modem to: (a) reject 2G (GSM) connections entirely (eliminating A5/1 cipher downgrade attacks); (b) enforce mutual authentication (EPS-AKA for LTE, 5G-AKA for 5G); (c) close all inbound IP ports except those required for OEM telematics (minimum: TLS-authenticated MQTT or proprietary protocol); (d) use a dedicated APN with VPN tunnel to OEM backend; (e) disable AT command interface accessibility from the application processor.

### 6.4. Layer 4 Controls: Diagnostic Protocol Hardening

**AH-4.01: Enforce Certificate-Based UDS Authentication.** *[Addresses V-4.1, V-4.2] [Tier: Essential] [OEM]*

Replace legacy SecurityAccess (0x27) seed-key mechanisms with certificate-based authentication per ISO 14229-1:2020 Authentication service (0x29). Diagnostic tool certificates must be issued by the OEM's PKI with short-lived validity periods (e.g., 24 hours), per-technician identity binding, and OEM-controlled revocation. HSMs on ECUs must validate the certificate chain before granting any elevated diagnostic session.

**AH-4.02: Implement OBD-II Port Access Control.** *[Addresses V-4.1, V-7.1] [Tier: Enhanced] [OEM / End-User]*

Deploy a hardware gateway module between the OBD-II connector and the internal CAN bus that: (a) authenticates connected devices via cryptographic challenge--response before granting bus access; (b) maintains a whitelist of permitted CAN message IDs for each authenticated device class; (c) rate-limits CAN frame transmission from the OBD-II port; (d) logs all OBD-II activity to tamper-resistant storage. For end-users and fleet operators: install an OBD-II port lock (physical tamper deterrent) when the port is not in authorized use.

### 6.5. Layer 5 Controls: External Connectivity Hardening

**AH-5.01: Harden IVI Head Unit Operating System.** *[Addresses V-5.1] [Tier: Essential] [OEM]*

Apply operating system hardening analogous to CIS Benchmark controls for Linux/QNX: (a) run all application processes as non-root with mandatory access control (SELinux/SMACK policies); (b) disable unnecessary services, daemons, and IPC mechanisms (the Jeep Cherokee's D-Bus ran as root without authentication); (c) enable ASLR, DEP/NX, stack canaries, and RELRO on all compiled binaries; (d) sandbox the web browser in a separate container/namespace with no CAN bus access; (e) disable USB autorun and auto-mount of removable media; (f) maintain a Software Bill of Materials (SBOM) and patch all third-party components (WebKit, OpenSSL, etc.) within OEM-defined SLA timelines.

**AH-5.02: Secure Over-the-Air Update Infrastructure.** *[Addresses V-5.3] [Tier: Essential] [OEM]*

Implement the Uptane framework (IEEE-ISTO 6100.1.0.0) with: (a) dual-repository architecture (Director + Image repositories with independent key management); (b) threshold signing (n-of-m) for production firmware images; (c) per-vehicle Director metadata; (d) TUF-compliant metadata expiry; (e) rollback protection via monotonic version counters verified by ECU HSMs; (f) delta update support to minimize cellular bandwidth; (g) independent integrity verification at each ECU before installation. Address the six specification vulnerabilities identified in RAID 2024 formal verification [36].

**AH-5.03: Implement API Security for Connected Car Services.** *[Addresses V-5.4, V-6.1] [Tier: Essential] [OEM]*

Apply OWASP API Security Top 10 controls to all vehicle-facing APIs: (a) enforce OAuth 2.0 with PKCE for mobile app authentication; (b) implement per-user API rate limiting; (c) validate all input parameters (preventing injection attacks that compromised Spireon); (d) enforce object-level authorization (preventing IDOR vulnerabilities that allowed Hyundai/Kia VIN-based access); (e) implement certificate pinning in mobile apps; (f) conduct regular penetration testing by third-party security firms; (g) deploy web application firewall (WAF) with automotive-specific rulesets.

### 6.6. Layer 6 Controls: Backend and Cloud Hardening

**AH-6.01: Harden Telematics Backend Infrastructure.** *[Addresses V-6.1, V-6.2] [Tier: Essential] [OEM]*

Apply standard ICT server hardening (CIS Benchmark for the relevant OS) to all telematics backend servers. Additionally: (a) encrypt all vehicle telemetry data at rest (AES-256) and in transit (TLS 1.3); (b) implement network segmentation between vehicle-facing, internet-facing, and internal services; (c) deploy fleet-level anomaly detection (unexpected command patterns, geographic impossibilities, temporal anomalies); (d) implement multi-factor authentication for all administrative access; (e) conduct supply chain security assessment for all cloud service providers.

**AH-6.02: Implement Data Minimization and Privacy Controls.** *[Addresses V-6.2] [Tier: Enhanced] [OEM]*

Minimize the collection, transmission, and retention of privacy-sensitive vehicle data: (a) offer user-accessible controls to disable cabin camera, microphone, and location sharing; (b) implement automatic deletion of paired phone data (contacts, call logs, SMS, navigation history) upon device disconnection or user request; (c) anonymize or pseudonymize telemetry data at the earliest possible processing stage; (d) restrict data sharing with third parties (insurance telematics providers, data brokers) to explicit, revocable user consent; (e) publish a machine-readable data inventory documenting all collected data categories, retention periods, and recipients.

### 6.7. Layer 7 Controls: Aftermarket Device Hardening

**AH-7.01: Validate Third-Party OBD-II Devices Before Installation.** *[Addresses V-7.1] [Tier: Essential] [Fleet Operator / End-User]*

Before connecting any third-party device to the OBD-II port: (a) verify the device has been evaluated against a recognized automotive cybersecurity certification (e.g., ISO/SAE 21434 compliance attestation, Common Criteria for automotive); (b) confirm the device implements CAN message filtering (blocking transmission of safety-critical IDs unless explicitly authorized); (c) verify the device uses encrypted, authenticated wireless communication (no open Bluetooth pairing, no default passwords); (d) confirm firmware update mechanism includes code signing with vendor-controlled PKI. In the absence of verifiable security claims, the device should not be installed.

**AH-7.02: Change Default Credentials on All Aftermarket Devices.** *[Addresses V-7.2, V-7.3] [Tier: Essential] [End-User]*

Immediately upon installation, change all default passwords, PINs, and API keys on GPS trackers, dashcams, aftermarket head units, and fleet management devices. MiCODUS MV720's default password of "123456" remained unchanged on 94.5% of deployed devices [43]. Use unique, high-entropy credentials for each device. Disable remote management interfaces (web UI, telnet, SSH) when not required.

## 7. Consolidated Control Summary

Table 3 summarizes the complete AUTOHARDEN control catalogue by layer, tier, and responsible party. The full benchmark contains 94 controls; this summary presents counts and representative examples per layer.

| Layer | Controls | E / N / M | Representative Controls |
| --- | --- | --- | --- |
| L1: Physical Bus | 14 | 6 / 5 / 3 | SecOC, CAN IDS, Gateway filtering, Bus isolation, CAN FD migration, CAN XL adoption |
| L2: ECU | 16 | 7 / 6 / 3 | Secure boot, Debug lockout, HSM key management, Runtime integrity, Firmware signing |
| L3: Wireless | 18 | 8 / 7 / 3 | UWB distance-bounding, TPMS encryption, GNSS anti-spoof, Cellular hardening, BLE mitigation |
| L4: Diagnostic | 8 | 4 / 3 / 1 | Certificate-based UDS auth, OBD port access control, DoIP hardening, Session logging |
| L5: Ext. Connectivity | 16 | 8 / 5 / 3 | IVI OS hardening, OTA (Uptane), API security, EV charging auth, V2X PKI |
| L6: Backend/Cloud | 10 | 5 / 3 / 2 | Server hardening, Data minimization, Fleet anomaly detection, SOC integration |
| L7: Third-Party | 12 | 6 / 4 / 2 | OBD-II device validation, Credential hygiene, GPS tracker audit, Dashcam isolation |

**Table 3.** AUTOHARDEN control catalogue summary. E = Essential, N = Enhanced, M = Maximum tier. Total: 94 controls (44 Essential, 33 Enhanced, 17 Maximum).*

## 8. Nation-State Threat Model for Vehicle-Targeted Operations

### 8.1. Adversary Characterization

We define the adversary as a state-level Advanced Persistent Threat (APT) with the following capabilities: dedicated offensive cyber units with automotive domain expertise (reverse engineering of ECU firmware, CAN protocol analysis, RF signal interception); signals intelligence (SIGINT) infrastructure including SS7/Diameter access, IMSI catchers, and lawful intercept capabilities in allied telecommunications networks; supply chain infiltration capability including front companies, compromised component suppliers, and customs interdiction of shipments; physical access teams capable of covert vehicle entry during servicing, border crossing, valet, or overnight parking; and financial resources to acquire zero-day vulnerabilities through broker markets ($100K--$2M per automotive zero-day) or develop them internally.

The adversary's objectives are twofold: (a) espionage---persistent, covert surveillance of the target individual including real-time location tracking, in-cabin audio/video recording, extraction of paired device data, and communication metadata analysis; and (b) sabotage---the capability to remotely disable, damage, or cause a crash of the target's vehicle at a time of the adversary's choosing. We note that the 2024 Hezbollah pager attack demonstrated state-level willingness and capability to execute supply chain hardware sabotage at scale [45].

### 8.2. Attack Scenarios and Required Hardening Tier

**Scenario A: Cellular Network Exploitation.** The adversary deploys an IMSI catcher near the target's known routes or residence to force the vehicle's TCU to connect, then exploits TCU firmware vulnerabilities or delivers malicious payloads via the cellular interface. SS7 signaling exploitation provides location tracking without IMSI catcher proximity. *Required controls: AH-3.04 (cellular hardening, 2G rejection, dedicated APN), AH-5.02 (authenticated OTA), AH-6.01 (backend segmentation to prevent lateral movement from TCU compromise). Tier: Maximum.*

**Scenario B: Supply Chain Compromise.** The adversary inserts a covert hardware implant---a secondary microcontroller with cellular modem, integrated into the wiring harness or hidden within an existing ECU enclosure---during vehicle manufacturing, shipping, or authorized servicing. The implant provides persistent remote access to the CAN bus, bypassing all software-level controls. *Required controls: AH-2.01 (secure boot, which does not protect against hardware implants), AH-1.02 (CAN IDS to detect anomalous traffic from the implant), AH-1.01 (SecOC, which forces the implant to possess valid CMAC keys), plus supply chain integrity verification (physical inspection, component provenance tracking, X-ray inspection of critical modules). Tier: Maximum.*

**Scenario C: Backend Server Exploitation.** The adversary compromises the OEM's connected car cloud platform through web application vulnerabilities (SQL injection, IDOR, SSRF) or supply chain compromise of cloud service providers. This provides fleet-scale command-and-control capability---the adversary can send commands to the target's vehicle through legitimate OEM infrastructure, making detection extremely difficult. *Required controls: AH-6.01 (backend hardening), AH-5.03 (API security), AH-5.02 (mutual TLS between vehicle and backend), AH-1.02 (CAN IDS as last line of defense against commands from a compromised backend). Tier: Maximum.*

**Scenario D: Physical Access Exploitation.** The adversary gains physical access to the target's vehicle during diplomatic servicing, customs/border inspection, hotel valet, or covert nighttime entry. Physical access enables: OBD-II port reprogramming of ECUs, installation of cellular-connected CAN bus implants, firmware extraction from ECU debug ports, or installation of tracking/surveillance devices disguised as legitimate components. *Required controls: AH-4.01 (certificate-based UDS auth preventing unauthorized reprogramming), AH-2.02 (debug interface lockout), AH-4.02 (OBD-II port access control), AH-7.01 (detection of unauthorized devices). Tier: Maximum. Additionally: post-servicing vehicle cybersecurity inspection protocol, including CAN bus traffic baseline comparison, OBD-II device enumeration, and RF spectrum analysis for unauthorized transmitters.*

**Scenario E: Vehicle as Surveillance Platform.** The adversary exploits any of the preceding vectors to silently activate the vehicle's built-in sensors: cabin-facing camera (driver monitoring system, standard in Tesla Model 3/Y and EU-mandated for driver drowsiness detection), hands-free microphones (2--8 per vehicle), eCall module's independent cellular modem, and GPS receiver. Data is exfiltrated via the compromised TCU or an implanted cellular device. *Required controls: All Maximum-tier controls plus AH-6.02 (privacy controls including user-accessible sensor disable), physical inspection for unauthorized antenna installations, and---for the highest threat levels---consideration of RF-shielded vehicle storage and electromagnetic emission testing.*

### 8.3. High-Value Individual Protection Protocol

Based on the threat model analysis, we recommend the following operational protocol for vehicles of individuals under assessed nation-state threat:

**(1) Vehicle procurement:** Source vehicles through vetted supply chains with chain-of-custody documentation from factory to delivery. Consider specification of vehicles without TCU cellular connectivity (rare in modern vehicles, but possible in some base-trim configurations) or with TCU physically disconnected post-delivery.

**(2) Baseline establishment:** Upon delivery, establish a complete CAN bus traffic baseline (all message IDs, frequencies, and payload patterns across all bus segments) and a physical wiring harness survey (component inventory, weight measurement, X-ray of critical junction boxes).

**(3) Connectivity minimization:** Disable all non-essential external interfaces. Physically disconnect the TCU cellular antenna (or the entire TCU module) if telematics services are not required. Disable Bluetooth and Wi-Fi on the IVI. Remove the SIM card from the eCall module if permitted by local regulation. Use wired (USB) connections for media rather than Bluetooth audio.

**(4) Aftermarket device prohibition:** Do not install any third-party device (OBD-II dongle, GPS tracker, dashcam with cellular connectivity, aftermarket head unit) without security vetting by qualified automotive cybersecurity assessors.

**(5) Servicing protocol:** All vehicle servicing must occur at security-cleared facilities with continuous vehicle monitoring (CCTV, access logs). Post-servicing, perform CAN bus baseline comparison, OBD-II device enumeration (can-utils cansniffer), and RF spectrum sweep (1 MHz--6 GHz) to detect unauthorized transmitters.

**(6) Continuous monitoring:** Deploy a dedicated, trusted CAN bus monitoring device (e.g., CSS Electronics CANedge2 with encrypted cellular reporting to the protective organization's SOC) that provides real-time anomaly detection independent of the vehicle's own systems.

## 9. Maturity Model and Implementation Roadmap

We propose a four-level maturity model for organizational adoption of AUTOHARDEN, recognizing that comprehensive vehicle hardening is a multi-year journey requiring investment across engineering, procurement, and operations:

| Level | Name | Controls | Scope | Timeline |
| --- | --- | --- | --- | --- |
| Level 1 | Foundational | 44 Essential-tier controls | All new model-year vehicles | 0--18 months |
| Level 2 | Comprehensive | Essential + 33 Enhanced controls | All connected vehicles | 18--36 months |
| Level 3 | Resilient | All 94 controls including Maximum | High-value fleets, gov/mil | 36--60 months |
| Level 4 | Adaptive | Full controls + threat intelligence integration + continuous red-teaming | Nation-state threat targets | Ongoing |

**Table 4.** AUTOHARDEN maturity model for organizational adoption.*

Level 1 prioritizes controls with the highest risk-reduction-to-cost ratio: SecOC deployment on safety-critical buses, secure boot, debug interface lockout, cellular modem hardening, IVI OS hardening, and OBD-II device validation. These controls address the most commonly exploited vectors (CAN injection, firmware tampering, remote TCU access) and are implementable with current technology and reasonable engineering effort.

Level 4 represents the state required for vehicles of individuals under active nation-state surveillance. It requires not only full control implementation but also continuous adversary simulation (red-teaming by automotive-specialized offensive security teams), threat intelligence integration (monitoring dark web markets for vehicle-specific zero-days, tracking APT group automotive capabilities), and incident response exercises specific to vehicular compromise scenarios.

## 10. Discussion

### 10.1. Limitations

Several limitations of this work merit acknowledgment. First, our attack surface taxonomy, while comprehensive, is necessarily incomplete---the automotive threat landscape evolves continuously, and proprietary OEM architectures may present attack vectors not represented in the publicly available research literature. Second, verification procedures for certain controls (particularly supply chain integrity controls at Maximum tier) require capabilities---such as X-ray inspection of ECU modules and silicon-level analysis---that may exceed the resources of many organizations. Third, the framework does not address legacy vehicles already deployed without the architectural features (HSMs, gateway ECUs with filtering capability) required by many controls; retrofit hardening of in-fleet vehicles is a distinct and more constrained problem. Fourth, we note a tension between hardening controls that restrict external connectivity and legitimate user expectations of connected car functionality---full TCU disconnection, while maximally secure, eliminates telematics, OTA updates, and emergency services.

### 10.2. Comparison with Existing Standards

AUTOHARDEN is complementary to, not a replacement for, ISO/SAE 21434 and UNECE WP.29 R155. ISO/SAE 21434 provides the process framework (TARA methodology, organizational cybersecurity management, supplier requirements) within which AUTOHARDEN controls are implemented. WP.29 R155 provides the regulatory mandate that creates organizational incentive for implementation. AUTOHARDEN's contribution is at the implementation level: where R155 Annex 5 states that the OEM must mitigate "unauthorized manipulation of vehicle communication buses" (threat category 4.3.5), AUTOHARDEN specifies the concrete controls (AH-1.01 through AH-1.04) and verification procedures to achieve that mitigation. This relationship is analogous to the relationship between PCI DSS (process/requirement framework) and CIS Benchmarks (implementation-level configuration guides) in payment card security.

### 10.3. Emerging Technologies

Several emerging technologies may fundamentally alter the vehicle hardening landscape. CAN XL, with its built-in CANsec authentication and encryption layer, could address Layer 1 vulnerabilities at the protocol level if adopted at scale---but widespread deployment is unlikely before 2030. Software-Defined Vehicles (SDVs) with centralized compute architectures (collapsing 100+ ECUs into 2--4 high-performance domain controllers) will reduce the attack surface breadth but concentrate risk in fewer, more complex targets. Vehicle-to-Cloud (V2C) architectures where critical functions are controlled from cloud-based digital twins introduce new categories of availability and integrity risk. Post-quantum cryptographic algorithms will need deployment in vehicular HSMs before large-scale quantum computing threatens current asymmetric cryptography---a migration that must begin in the current design cycle given vehicle lifespans of 10--15 years.

## 11. Conclusion

This paper has presented AUTOHARDEN, the first comprehensive, implementation-level hardening framework for connected vehicles, addressing a critical gap between high-level regulatory requirements (ISO/SAE 21434, UNECE WP.29 R155) and the practical security configurations needed to defend against demonstrated attack vectors. Our seven-layer Attack Surface Taxonomy systematically catalogues the connected vehicle's exposure, and the 94-control Vehicle Hardening Framework provides actionable, verifiable security directives analogous to CIS Benchmarks for enterprise ICT assets.

The nation-state threat model presented in Section 8 underscores the urgency of this work. Connected vehicles now constitute rich surveillance and sabotage platforms---containing always-on microphones, cameras, GPS receivers, and persistent cellular connectivity---accessible through attack chains demonstrated by academic researchers using modest resources. A well-resourced state adversary can combine supply chain infiltration, cellular network exploitation, backend server compromise, and physical access to achieve persistent, covert control of a target's vehicle. The operational protection protocol we prescribe for high-value individuals represents the minimum defensive posture against this threat class.

The fundamental insight underlying this framework is that vehicle cybersecurity is an operational discipline, not merely a design-time activity. Just as ICT organizations continuously harden, monitor, and patch their server infrastructure against evolving threats, vehicle operators---whether OEMs, fleet managers, or individual owners---must adopt a continuous hardening posture. The AUTOHARDEN maturity model provides a structured path from foundational baseline controls to the adaptive, intelligence-driven security posture required in the most demanding threat environments. We call on the automotive cybersecurity community to develop AUTOHARDEN into a maintained, consensus-driven benchmark---updated annually against the latest threat intelligence---that becomes as foundational to vehicle security as CIS Benchmarks are to server security.

## References

[1] Miller, C., Valasek, C.: Remote exploitation of an unaltered passenger vehicle. Black Hat USA (2015)

[2] Nie, S., Liu, L., Du, Y.: Free-fall: hacking Tesla from wireless to CAN bus. Black Hat USA (2017)

[3] Tencent Keen Security Lab: Experimental security research of Tesla Autopilot. Technical Report (2019)

[4] Tindell, K.: CAN injection: keyless car theft. Canis Automotive Labs Technical Report (2023)

[5] Zero Day Initiative: Pwn2Own Automotive results 2024--2026. Trend Micro (2024--2026)

[6] Koscher, K., Checkoway, S., et al.: Experimental security analysis of a modern automobile. In: IEEE Symposium on Security and Privacy, pp. 447--462 (2010)

[7] Checkoway, S., McCoy, D., et al.: Comprehensive experimental analyses of automotive attack surfaces. In: USENIX Security Symposium (2011)

[8] Valasek, C., Miller, C.: Adventures in automotive networks and control units. Technical Report (2013)

[9] NHTSA: Cybersecurity best practices for modern vehicles. Report No. DOT HS 812 333 (2016)

[10] Miller, C., Valasek, C.: CAN message injection: OG car hacking. Black Hat USA (2016)

[11] ISO/SAE 21434:2021: Road vehicles --- Cybersecurity engineering. International Organization for Standardization (2021)

[12] UNECE: UN Regulation No. 155 --- Cyber security and cyber security management system. WP.29 (2021)

[13] Center for Internet Security: CIS Benchmarks. https://www.cisecurity.org/cis-benchmarks (2024)

[14] DISA: Security Technical Implementation Guides (STIGs). https://public.cyber.mil/stigs/ (2024)

[15] Scarfone, K., Souppaya, M., Hoffman, P.: Guide to general server security. NIST SP 800-123 (2008)

[16] SAE International: J3061 --- Cybersecurity guidebook for cyber-physical vehicle systems (2016)

[17] Upstream Security: Global automotive cybersecurity report. Annual Reports 2020--2025 (2020--2025)

[18] I Am The Cavalry: Five star automotive cyber safety framework (2015)

[19] VehicleSec 2024: Exploiting diagnostic protocol vulnerabilities. In: NDSS Workshop on Vehicle Security (2024)

[20] Tencent Keen Security Lab: Experimental security assessment of BMW cars. Black Hat USA (2019)

[21] VicOne: How to get away with car theft: unveiling the dark side of the CAN bus. Technical Blog (2023)

[22] Hoppe, T., Kiltz, S., Dittmann, J.: Security threats to automotive CAN networks. In: ARES, pp. 1232--1237 (2008)

[23] CISA: ICS-ALERT-17-209-01 --- CAN bus standard vulnerability. Cybersecurity Advisory (2017)

[24] I-CAN-hack: Breaking Toyota SecOC on RAV4 Prime. DEF CON 32 Car Hacking Village (2024)

[25] Wouters, L., et al.: My other car is your car: compromising the Tesla Model X keyless entry system. In: USENIX Security Symposium (2021)

[26] UCSD SCCS: Comprehensive vulnerability analysis of OBD-II dongles. In: USENIX Security Symposium (2020)

[27] Cydrill: The ECU killer: broken authentication in automotive security. Technical Report (2024)

[28] Francillon, A., Danev, B., Capkun, S.: Relay attacks on passive keyless entry and start systems in modern cars. In: NDSS (2011)

[29] ADAC: Keyless entry relay attack test results across 600+ vehicle models. German Automobile Club (2016--2024)

[30] Kamkar, S.: Drive it like you hacked it: new attacks and tools to wirelessly steal cars. DEF CON 23 (2015)

[31] Rollback: RollBack breaks into your car. Hackaday (2022)

[32] Khan, S.Q.: Bluetooth Low Energy link-layer relay attacks on passive entry systems. NCC Group Research (2022)

[33] Rouf, I., et al.: Security and privacy vulnerabilities of in-car wireless networks: a tire pressure monitoring system case study. In: USENIX Security Symposium (2010)

[34] Southwest Research Institute: GPS spoofing test system for automated vehicles (2019)

[35] Wen, H., et al.: Plug-N-Pwned: comprehensive vulnerability analysis of OBD-II dongles. In: USENIX Security Symposium (2020)

[36] RAID 2024: Formal verification of Uptane framework reveals six new vulnerabilities (2024)

[37] Curry, S.: Web hackers vs. the auto industry: critical vulnerabilities in Ferrari, BMW, Rolls Royce, Porsche, and more. Technical Blog (2023)

[38] Kohler, S., et al.: Brokenwire: wireless disruption of CCS electric vehicle charging. In: NDSS (2023)

[39] Baker, R., Martinovic, I.: Losing the car keys: wireless PHY-layer insecurity in EV charging. In: USENIX Security Symposium (2019)

[40] Mozilla Foundation: Privacy not included: cars review (2023)

[41] Twardokus, K., et al.: Targeted sidelink jamming of C-V2X semi-persistent scheduling. RIT Technical Report (2024)

[42] Argus Cyber Security: Bosch Drivelog Connect OBD-II dongle vulnerability disclosure (2017)

[43] BitSight: Critical vulnerabilities in MiCODUS MV720 GPS tracker (CVE-2022-2107, CVE-2022-2141). CISA Advisory (2022)

[44] VicOne: Thousands of vehicles at risk: zero-day vulnerabilities in aftermarket devices. Technical Report (2025)

[45] Various: Analysis of Hezbollah pager supply chain attack. Multiple sources (2024)
