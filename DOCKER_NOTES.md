# Docker and DevOps Notes

## DevOps

DevOps is a combination of:

- **Dev** → Development team
- **Ops** → Operations team

It is a culture/practice where developers and operations teams work together to build, test, deploy, and maintain software faster and more efficiently.

### Main Goals of DevOps

- Faster software delivery
- Continuous testing and deployment
- Better collaboration between teams
- Automation of repetitive tasks
- High-quality software

### DevOps Lifecycle

1. **Plan** → Requirement gathering and planning
2. **Develop** → Writing code
3. **Build** → Compile/package application
4. **Test** → Automated/manual testing
5. **Release** → Prepare for deployment
6. **Deploy** → Deploy application to server/cloud
7. **Operate** → Run and manage application
8. **Monitor** → Check logs, performance, issues

### Popular DevOps Tools

| Purpose | Tools |
|---------|-------|
| CI/CD | Jenkins, GitHub Actions |
| Containerization | Docker |
| Orchestration | Kubernetes |
| Configuration Management | Ansible |
| Infrastructure as Code | Terraform |
| Monitoring | Prometheus, Grafana |
| Version Control | Git, GitHub |

---

## Container

A container is a lightweight isolated environment that contains:

- Application code
- Libraries
- Dependencies
- Runtime

It allows the application to run the same everywhere.

### Simple Definition

A container packages an application with everything needed to run it.

### Example of Container

Suppose you created a Python app.

**Normally another system may not have:**

- Python installed
- Required libraries
- Correct environment

**With Docker container:**

- Everything is packed together
- App runs the same on all systems

---

## Containerization

Containerization is the process of packaging an application and its dependencies into containers.

### Features

- Lightweight
- Fast startup
- Portable
- Efficient
- Isolated environment

### Popular Containerization Tool

- **Docker**

---

## Virtualization

Virtualization means creating multiple virtual machines (VMs) on one physical machine using a hypervisor.

Each VM has:

- Full operating system
- Virtual hardware
- Separate kernel

### Popular Virtualization Tools

- VMware
- VirtualBox
- Hyper-V

---

## Containerization vs Virtualization

| Feature | Containerization | Virtualization |
|---------|------------------|-----------------|
| Uses | Containers | Virtual Machines |
| OS | Shares host OS kernel | Each VM has separate OS |
| Size | Lightweight | Heavy |
| Startup Time | Seconds | Minutes |
| Performance | Faster | Slower than containers |
| Resource Usage | Less | More |
| Isolation | Process level | Full OS level |
| Portability | Very high | Moderate |
| Example Tools | Docker, Podman | VMware, VirtualBox |

### Architecture Difference

**Virtualization:**
```
Hardware
   ↓
Hypervisor
   ↓
VM1 (OS + App)
VM2 (OS + App)
VM3 (OS + App)
```
Each VM contains a complete operating system.

**Containerization:**
```
Hardware
   ↓
Host Operating System
   ↓
Docker Engine
   ↓
Container1 (App)
Container2 (App)
Container3 (App)
```
Containers share the host OS kernel.

### Why Containers are Faster

Containers do not install a full operating system.

They share the host system kernel, so:

- Less memory used
- Faster startup
- Better performance

---

## Real Life Example

### Virtual Machine

Like renting a complete separate house.

### Container

Like different rooms inside the same house sharing electricity and water.

---

## Short Interview/Viva Answers

### What is DevOps?

DevOps is a practice that combines development and operations to automate and speed up software delivery.

### What is a Container?

A container is an isolated environment that packages an application with all dependencies.

### What is Containerization?

Containerization is the process of packaging applications into containers for portability and consistency.

### Difference Between VM and Container?

VM uses separate OS for each machine while containers share the host OS kernel and are lightweight.
