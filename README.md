# Secure Smart Home Management Enterprise Lab

A cyber-physical engineering laboratory built around an **IBM Power S922**, using a real smart-home environment as the physical workload and an enterprise-style software platform as the management layer.

The initial physical deployment may consist of a single smart home, but the software is intentionally designed as a **multi-tenant SaaS platform** capable of managing multiple organizations, properties, users, and IoT devices.

The purpose of this project is not simply to build a smart home.

The purpose is to create a realistic environment where **Software Engineering and Electrical Engineering meet**, while providing a platform for experimenting with:

- Cybersecurity
- DevSecOps
- Enterprise infrastructure
- IoT
- Networking
- Distributed systems
- Observability
- AI-assisted software engineering

The IBM S922 provides the central infrastructure on which the platform can be developed, deployed, secured, monitored, and tested.

---

## Project Status

**Status:** Proposal / Awaiting Approval

This repository currently describes the proposed architecture, objectives, scope, and development roadmap.

Implementation will begin after the project concept and infrastructure plan are approved.

---

# 1. Project Concept

The project combines two primary engineering domains.

## Software Engineering

Responsible for the digital platform:

- SaaS architecture
- Backend
- Frontend
- APIs
- Database
- Authentication
- Authorization
- Multi-tenancy
- Device management
- Automation
- Logging
- Monitoring
- DevSecOps
- Infrastructure
- Cybersecurity
- AI-assisted development

## Electrical Engineering

Responsible for the physical system:

- Sensors
- Actuators
- Microcontrollers
- Embedded systems
- Electrical measurements
- Device communication
- Physical automation
- Control systems
- IoT hardware

The IBM Power S922 acts as the central infrastructure platform connecting these domains.

---

# 2. High-Level Architecture

```text
                              ┌───────────────┐
                              │     Users     │
                              └───────┬───────┘
                                      │
                                      ▼
                              Web / Mobile UI
                                      │
                                      ▼
                         ┌────────────────────────┐
                         │   Security Boundary    │
                         │                        │
                         │ Firewall / Network     │
                         │ Security / Monitoring  │
                         └───────────┬────────────┘
                                     │
                                     ▼
                         ┌────────────────────────┐
                         │      IBM Power S922    │
                         │         POWER9         │
                         │                        │
                         │  Smart Home SaaS       │
                         │  Authentication        │
                         │  API                   │
                         │  Database              │
                         │  Device Management     │
                         │  Automation            │
                         │  Monitoring            │
                         └───────────┬────────────┘
                                     │
                            MQTT / API / Network
                                     │
                                     ▼
                         ┌────────────────────────┐
                         │      IoT Environment   │
                         │                        │
                         │ Sensors                │
                         │ Actuators              │
                         │ ESP32 / MCU            │
                         │ Energy Monitoring      │
                         │ Lighting               │
                         │ Environmental Devices  │
                         └────────────────────────┘
```

---

# 3. Why a Smart Home?

The physical smart home provides a **real cyber-physical environment** for the software platform.

Instead of generating artificial data, the system can continuously receive real data from:

- Temperature sensors
- Humidity sensors
- Motion sensors
- Light sensors
- Energy meters
- Current/voltage sensors
- Smart lights
- Fans
- Relays
- Motors
- Other IoT devices

This creates a realistic workload for the software infrastructure.

For example:

```text
Temperature Sensor
        │
        ▼
      ESP32
        │
       MQTT
        │
        ▼
      S922
        │
        ├── Database
        ├── API
        ├── Automation
        ├── Monitoring
        └── Dashboard
```

The physical environment can also intentionally generate real-world conditions:

- Devices disconnect
- Sensors produce unexpected values
- Networks become unavailable
- Devices restart
- Firmware changes
- Software deployments introduce bugs
- Security events occur
- Hardware fails

These situations provide opportunities to study:

- Reliability
- Fault tolerance
- Observability
- Incident response
- Security
- Recovery

---

# 4. Why Design It as SaaS?

The physical deployment may initially contain only one smart home.

However, the software will be designed as if it were a commercial IoT SaaS platform.

For example:

```text
Organization A
├── House A1
│   ├── Living Room
│   ├── Bedroom
│   └── Kitchen
│
└── House A2
    └── ...

Organization B
├── House B1
└── House B2

Organization C
└── House C1
```

The initial installation may only contain:

```text
Organization A
└── House A1
```

The difference is that the **software architecture supports the larger model**.

This allows the project to investigate real enterprise software problems without requiring an actual commercial deployment.

Potential areas include:

- Multi-tenancy
- Tenant isolation
- Authentication
- Authorization
- Device management
- Scalability
- Reliability
- Security
- Auditing
- Monitoring

---

# 5. Software Platform

The management platform will provide functionality such as:

## Identity

- User registration
- Authentication
- Session management
- MFA
- Role-based access control

## Organization Management

- Organizations
- Users
- Roles
- Permissions
- Houses/properties

## Smart Home Management

- Rooms
- Devices
- Sensors
- Actuators
- Device status
- Device configuration

## Automation

Example:

```text
IF
    temperature > 30°C

AND
    someone is home

THEN
    turn_on(fan)
```

Other possible functionality:

- Scheduled actions
- Event-based automation
- Device groups
- Scenes
- Notifications

---

# 6. Device Management

The platform should treat IoT devices as managed resources.

Example:

```text
House: Main House

Living Room
├── Light-01         ONLINE
├── Temperature-01   ONLINE
└── Motion-01        OFFLINE

Bedroom
├── Light-02         ONLINE
└── Temperature-02   ONLINE

Kitchen
└── Energy-01        ONLINE
```

A possible device lifecycle:

```text
Manufactured
     ↓
Registered
     ↓
Provisioned
     ↓
Authenticated
     ↓
Connected
     ↓
Managed
     ↓
Updated
     ↓
Decommissioned
```

This creates opportunities to study:

- Device identity
- Device provisioning
- Device authentication
- Firmware management
- Device lifecycle management
- Device revocation

---

# 7. Multi-Tenant Security

One of the major Software Engineering and Cybersecurity problems is **tenant isolation**.

For example:

```text
Tenant A
└── House A
    └── Light A

Tenant B
└── House B
    └── Light B
```

A user belonging to Tenant A must not be able to access or control resources belonging to Tenant B.

This applies to:

- API requests
- Database queries
- Device commands
- MQTT topics
- Files
- Logs
- Dashboards
- Automation rules

A request such as:

```http
POST /api/devices/123/command
```

must not be authorized solely because the user knows `device_id=123`.

The platform must verify that the authenticated identity is actually permitted to operate that device.

This provides a practical environment for studying:

- Authentication
- Authorization
- RBAC
- Object-level authorization
- Tenant isolation
- Session security
- Audit logging
- Access control

---

# 8. Cybersecurity Architecture

The project will apply **enterprise-style cybersecurity principles** to the environment.

The goal is not to reproduce proprietary technology from any particular security vendor.

Instead, the project will study and implement general security concepts such as:

- Network segmentation
- Zero-trust principles
- Least privilege
- Identity-based access
- Firewalling
- IDS/IPS
- Secure APIs
- Device identity
- Secrets management
- Security logging
- Vulnerability management
- Security monitoring
- Incident response

A conceptual architecture:

```text
                         Internet
                            │
                            ▼
                    ┌───────────────┐
                    │ Network Edge  │
                    │ Security      │
                    └───────┬───────┘
                            │
                    ┌───────▼───────┐
                    │ Application   │
                    │ Network       │
                    └───────┬───────┘
                            │
                  ┌─────────┼─────────┐
                  │         │         │
                  ▼         ▼         ▼
                API      Database    Auth
                  │
                  ▼
             IoT Gateway
                  │
                  ▼
              IoT Network
                  │
          ┌───────┼────────┐
          ▼       ▼        ▼
       Sensor   Sensor   Actuator
```

The security architecture should evolve together with the application rather than being added after the application is completed.

---

# 9. Cybersecurity Laboratory

The platform can also become a controlled cybersecurity laboratory.

Security testing will only be performed against systems and devices owned or explicitly authorized for testing.

A separate testing environment can be maintained:

```text
                    IBM S922
                        │
          ┌─────────────┼─────────────┐
          │             │             │
          ▼             ▼             ▼
     Production       IoT Lab     Security Lab
                                      │
                                      ▼
                               Security Testing
```

The testing cycle:

```text
Attack
  │
  ▼
Detect
  │
  ▼
Investigate
  │
  ▼
Respond
  │
  ▼
Fix
  │
  ▼
Verify
  │
  └──────────────► Repeat
```

Potential areas of study:

- Authentication security
- Authorization security
- API security
- MQTT security
- Network segmentation
- Vulnerability assessment
- Configuration security
- IoT device security
- Security logging
- Incident investigation

The objective is to understand the complete security lifecycle rather than simply finding vulnerabilities.

---

# 10. Observability

The system will treat observability as part of the platform rather than an afterthought.

## Metrics

Examples:

```text
IoT devices online:       18
API requests/sec:          4.2
MQTT messages/sec:        12
CPU usage:                23%
Memory usage:             41%
Database connections:     17
```

## Logs

Examples:

```text
USER_LOGIN
DEVICE_CONNECTED
DEVICE_DISCONNECTED
DEVICE_COMMAND
AUTOMATION_TRIGGERED
AUTHORIZATION_DENIED
MQTT_CONNECTION
SECURITY_EVENT
```

## Monitoring

Monitoring can combine:

- Application health
- Infrastructure metrics
- Device status
- Network health
- Database health
- Security events

## Alerting

Examples:

```text
⚠ Multiple failed login attempts

⚠ IoT device unexpectedly disconnected

⚠ Unauthorized device command attempted

⚠ Unusual API traffic detected

⚠ Database resource usage abnormal
```

Observability data should also support security investigation and incident response.

---

# 11. DevSecOps

The platform will serve as a **DevSecOps laboratory**, integrating security throughout the software development and operational lifecycle rather than treating security as a final-stage activity.

The intended lifecycle is:

```text
Developer
    │
    ▼
Git Repository
    │
    ▼
PLAN
    │
    ├── Security Requirements
    ├── Threat Modeling
    └── Architecture Review
    │
    ▼
DEVELOP
    │
    ├── Secure Coding
    ├── Code Review
    ├── Secrets Detection
    └── Dependency Management
    │
    ▼
BUILD
    │
    ├── Unit Tests
    ├── Integration Tests
    ├── SAST
    ├── SCA
    ├── SBOM Generation
    ├── Container Scanning
    └── Build Verification
    │
    ▼
TEST
    │
    ├── Functional Tests
    ├── Security Tests
    ├── DAST
    ├── API Security Tests
    └── IoT Integration Tests
    │
    ▼
SECURITY GATE
    │
    ├── Vulnerabilities?
    ├── Policy Violations?
    └── Failed Security Tests?
    │
    ├────────────── YES ──────────────┐
    │                                  │
    │                                  ▼
    │                              Remediate
    │                                  │
    │                                  └──► Re-test
    │
    ▼ NO
RELEASE
    │
    ▼
DEPLOY
    │
    ├── Infrastructure as Code
    ├── Configuration Validation
    ├── Deployment Verification
    └── Runtime Security Checks
    │
    ▼
OPERATE
    │
    ├── Metrics
    ├── Logs
    ├── Security Monitoring
    ├── Vulnerability Monitoring
    └── Alerting
    │
    ▼
CONTINUOUS FEEDBACK
    │
    └──────────────────────────────► PLAN
```

---

## 11.1 DevSecOps Practices

Potential practices include:

- Secure coding standards
- Code review
- Threat modeling
- Secret scanning
- Dependency management
- Software Composition Analysis (SCA)
- Static Application Security Testing (SAST)
- Dynamic Application Security Testing (DAST)
- Container image scanning
- Infrastructure as Code security scanning
- Software Bill of Materials (SBOM)
- Automated security testing
- Vulnerability assessment
- Security policy enforcement
- Security gates in CI/CD
- Artifact integrity verification
- Secure deployment
- Runtime security monitoring
- Vulnerability management
- Incident response

The objective is not simply to scan the application for vulnerabilities.

The objective is to create a development and operations process in which **security continuously influences how software is designed, developed, tested, released, deployed, and operated**.

---

## 11.2 DevSecOps Security Pipeline

```text
                    Git Push / Pull Request
                              │
                              ▼
                    ┌──────────────────┐
                    │     CI Pipeline  │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
          Unit Tests        SAST           SCA
              │              │              │
              └──────────────┼──────────────┘
                             │
                             ▼
                       Secret Scan
                             │
                             ▼
                     Build Application
                             │
                             ▼
                    Generate SBOM
                             │
                             ▼
                    Build Container
                             │
                             ▼
                   Container Scan
                             │
                             ▼
                       DAST / API
                       Security Tests
                             │
                             ▼
                    ┌─────────────────┐
                    │  Security Gate  │
                    └────────┬────────┘
                             │
                   ┌─────────┴─────────┐
                   │                   │
                 FAIL                 PASS
                   │                   │
                   ▼                   ▼
              Remediation          Release
                                       │
                                       ▼
                                  Deployment
                                       │
                                       ▼
                                  Production
                                       │
                         ┌─────────────┴─────────────┐
                         ▼                           ▼
                    Monitoring                  Security
                         │                       Monitoring
                         │                           │
                         └─────────────┬─────────────┘
                                       ▼
                                  Alert / Feedback
                                       │
                                       └──► Development
```

---

# 12. Infrastructure Security

DevSecOps also applies to the infrastructure running the platform.

Infrastructure should be managed and validated through code where practical.

Potential areas include:

- Infrastructure as Code
- Configuration management
- Network security policies
- Least-privilege access
- Secrets management
- Secure container configuration
- Image provenance
- Host hardening
- Configuration scanning
- Backup verification
- Disaster recovery testing

The goal is to ensure that security is applied not only to the application but also to the infrastructure on which the application operates.

---

# 13. Security Feedback Loop

Security findings should become engineering work rather than simply appearing as reports.

```text
Vulnerability Detected
        │
        ▼
Security Finding
        │
        ▼
Prioritize / Investigate
        │
        ▼
Remediation
        │
        ▼
Security Test
        │
        ▼
Verification
        │
        ▼
Deploy
        │
        ▼
Monitor
        │
        └──────────────► New Findings
```

This creates a continuous security feedback loop between development, security, and operations.

---

# 14. AI-Assisted Engineering

AI coding tools such as **Cursor** can be incorporated into the development workflow.

Possible uses:

- Code generation
- Refactoring
- Documentation
- Test generation
- Code review
- Security review
- Log analysis
- Debugging
- Incident investigation

However, AI agents should operate within controlled environments with appropriate permissions.

A possible development architecture:

```text
                    AI Coding Agent
                          │
                          ▼
                  Development VM
                          │
                  ┌───────┴───────┐
                  │               │
                Source          Tests
                  │               │
                  └───────┬───────┘
                          ▼
                         CI
                          │
                          ▼
                       Staging
                          │
                          ▼
                      Production
```

This creates an opportunity to study the security implications of AI agents with access to:

- Source code
- Files
- Terminals
- Development environments
- Build systems
- Infrastructure tooling

Potential research areas include:

- AI-generated code security
- AI-assisted vulnerability detection
- AI-generated tests
- AI-assisted code review
- AI-assisted incident investigation
- AI agent permissions
- Prompt injection against development agents
- Protection of secrets and credentials
- Human review of AI-generated changes

---

# 15. IBM Power S922

The IBM Power S922 is the central infrastructure component.

Potential uses include:

- Virtual machines / logical partitions
- Linux workloads
- Application hosting
- Databases
- IoT services
- Monitoring
- Security services
- Development environments
- Testing environments
- AI-assisted development environments

The exact architecture will depend on the S922's available:

- CPU resources
- Memory
- Storage
- Network interfaces
- PowerVM configuration
- HMC availability
- Existing operating systems
- Licensing

The machine should therefore be inventoried before the final infrastructure design is created.

---

# 16. Engineering Responsibilities

The project deliberately separates responsibilities by engineering domain while keeping the overall system integrated.

## Software Engineering

Focus areas:

- System architecture
- Backend
- Frontend
- APIs
- Databases
- Authentication
- Authorization
- SaaS architecture
- Multi-tenancy
- DevSecOps
- Infrastructure
- Monitoring
- Cybersecurity
- AI-assisted development

## Electrical Engineering

Focus areas:

- Sensors
- Actuators
- Microcontrollers
- Embedded systems
- Electrical measurement
- Device communication
- Control systems
- Physical automation
- Hardware reliability
- IoT device design

## Shared Engineering Areas

Both disciplines interact in:

- IoT protocols
- Networking
- System architecture
- Device provisioning
- Security
- Reliability
- Testing
- Troubleshooting
- Documentation

The objective is not to keep the disciplines isolated.

The objective is to understand the **interfaces between them**.

---

# 17. Development Roadmap

## Phase 0 — Infrastructure Discovery

- [ ] Inventory IBM S922
- [ ] Identify CPU configuration
- [ ] Identify RAM
- [ ] Identify storage
- [ ] Identify network interfaces
- [ ] Identify PowerVM configuration
- [ ] Identify HMC availability
- [ ] Identify existing operating systems
- [ ] Document current configuration

---

## Phase 1 — Basic IoT Platform

- [ ] Select initial IoT devices
- [ ] Establish IoT network
- [ ] Connect microcontroller
- [ ] Establish MQTT communication
- [ ] Build basic backend
- [ ] Store sensor data
- [ ] Build basic dashboard

Target:

```text
Sensor → MCU → MQTT → S922 → Database → Dashboard
```

---

## Phase 2 — Smart Home Management

- [ ] Users
- [ ] Houses
- [ ] Rooms
- [ ] Devices
- [ ] Sensors
- [ ] Actuators
- [ ] Device status
- [ ] Automation rules
- [ ] Scheduling
- [ ] Notifications

---

## Phase 3 — SaaS Architecture

- [ ] Organizations
- [ ] Multi-tenancy
- [ ] Tenant isolation
- [ ] RBAC
- [ ] Authentication
- [ ] Authorization
- [ ] Audit logging
- [ ] Device provisioning

---

## Phase 4 — DevSecOps Foundation

- [ ] Containerization
- [ ] CI
- [ ] Automated testing
- [ ] Linting
- [ ] Code coverage
- [ ] Secret scanning
- [ ] SAST
- [ ] SCA
- [ ] SBOM generation
- [ ] Container scanning
- [ ] DAST
- [ ] API security testing
- [ ] Security gates
- [ ] CD
- [ ] Infrastructure as Code
- [ ] IaC security scanning
- [ ] Staging environment
- [ ] Production environment
- [ ] Backup
- [ ] Recovery testing

---

## Phase 5 — Cybersecurity

- [ ] Network segmentation
- [ ] Firewall
- [ ] IDS/IPS
- [ ] Secure MQTT
- [ ] API security
- [ ] Secrets management
- [ ] Vulnerability assessment
- [ ] Security monitoring
- [ ] Security alerting
- [ ] Incident response exercises
- [ ] Security incident documentation

---

## Phase 6 — Security Testing

- [ ] Build isolated security-testing environment
- [ ] Authentication testing
- [ ] Authorization testing
- [ ] API testing
- [ ] MQTT testing
- [ ] Network testing
- [ ] Vulnerability assessment
- [ ] Log investigation
- [ ] Incident response
- [ ] Remediation
- [ ] Verification

---

## Phase 7 — AI-Assisted Engineering

- [ ] Introduce AI coding agent
- [ ] Establish development permissions
- [ ] Test AI-generated code
- [ ] AI-assisted code review
- [ ] AI-assisted security review
- [ ] AI-assisted test generation
- [ ] AI-assisted log analysis
- [ ] Study AI agent security
- [ ] Document AI security findings

---

# 18. Possible Future Extensions

Once the core platform works, additional areas can be explored.

## Energy Management

```text
Voltage
Current
Power
Energy
Power Factor
```

with historical analysis and visualization.

## Predictive Maintenance

Use sensor data to identify abnormal behavior in:

- Motors
- Fans
- Pumps
- Electrical equipment

## Anomaly Detection

Detect unusual:

- Network traffic
- Device behavior
- Energy consumption
- Authentication activity
- Sensor readings

## Edge Computing

Move selected processing closer to IoT devices instead of sending everything to the central server.

## High Availability

Experiment with:

- Service redundancy
- Failover
- Backups
- Recovery
- Disaster scenarios

## Fleet Management

Expand the software model from individual devices to large fleets of IoT devices.

---

# 19. Success Criteria

The project should eventually demonstrate that:

## Software Engineering

- A real IoT management platform can be developed.
- The architecture supports multiple tenants.
- Users and devices can be securely managed.
- Automated deployment and testing work reliably.
- The platform can operate as a multi-tenant SaaS architecture.

## Electrical Engineering

- Physical devices can reliably collect data.
- Actuators can be controlled through the platform.
- Embedded systems can communicate with the infrastructure.
- Electrical measurements can be integrated into the platform.
- Devices can be managed throughout their lifecycle.

## Cybersecurity

- IoT and application networks can be appropriately separated.
- Users and devices can be authenticated.
- Access can be authorized according to defined permissions.
- Security events can be detected and investigated.
- Controlled security testing can be performed.
- Security findings can be remediated and verified.

## DevSecOps

- Security is incorporated throughout the SDLC.
- Automated tests run during CI.
- Security scanning runs automatically.
- Vulnerabilities can block or influence releases according to defined policies.
- Infrastructure can be securely managed as code.
- Deployments are automated.
- Runtime security and observability are available.
- Security findings feed back into development.

## AI

- AI tools can assist development.
- AI-generated changes can be tested and reviewed.
- AI agents can be operated with controlled permissions.
- The security implications of AI-assisted development can be studied.

---

# 20. Core Idea

The project can be summarized as:

```text
          ELECTRICAL ENGINEERING
                   │
             Physical World
                   │
                   ▼
            Sensors / IoT
                   │
                   ▼
              Networking
                   │
                   ▼
          SOFTWARE ENGINEERING
                   │
            SaaS Platform
                   │
                   ▼
             IBM Power S922
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
  Cybersecurity  DevSecOps    AI
        │          │          │
        └──────────┼──────────┘
                   │
                   ▼
          Secure Smart Platform
```

The smart home is the **physical test environment**.

The SaaS platform is the **software engineering environment**.

The IBM S922 is the **enterprise infrastructure laboratory**.

Cybersecurity protects the complete system.

DevSecOps securely builds, tests, deploys, and operates the system.

AI provides another layer of modern engineering experimentation.

Together, they create a small but realistic **enterprise-style cyber-physical engineering laboratory**.

---

# Project Philosophy

> **Build the physical system.**
>
> **Build the software platform.**
>
> **Connect them.**
>
> **Secure them.**
>
> **Test them.**
>
> **Deploy them.**
>
> **Monitor them.**
>
> **Break them safely.**
>
> **Understand why they broke.**
>
> **Fix them.**
>
> **Automate the process.**

The goal is not to create a commercial smart-home product immediately.

The goal is to use a real physical environment and enterprise-class infrastructure as a laboratory for learning how modern interconnected engineering systems are **designed, developed, secured, deployed, monitored, tested, and operated**.
