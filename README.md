# Top  Docker Security Best Practices: Ultimate Guide for Deamon, Image & Container

## Introduction
Docker has become synonymous with containers, and while various tools and platforms exist, Docker security remains crucial. This guide compiles the most essential best practices to help you build more secure containers.

### A Brief Introduction to Docker Security
Docker security involves protecting containers, the Docker daemon, host OS, and underlying hardware. While containers provide isolation, vulnerabilities in one container can impact others or the host system.

### Common Security Risks in Docker
1. **Unrestricted Traffic and Unsafe Communication**
   - Docker allows all network traffic between containers by default, posing a security risk.
   - Communication between the Docker client and daemon lacks encryption, risking data interception.

2. **Vulnerable and Malicious Container Images**
   - Use of unverified Docker Hub images without scanning can lead to deploying compromised containers.

3. **Root Access for Containers**
   - Containers run as root by default, posing a security risk if compromised, enabling attackers to escalate privileges.

4. **Host Kernel Vulnerabilities**
   - Containers share the host system's kernel, and vulnerabilities in the kernel can lead to system-wide breaches.

## 22 Key Docker Security Best Practices

### Docker and Host Configuration
1. **Keep Host and Docker Up to Date**
   - Patch Docker Engine and host OS regularly to prevent known vulnerabilities.

2. **Do Not Expose the Docker Daemon Socket**
   - Avoid exposing the Docker daemon socket, especially in production containers.

3. **Run Docker in Rootless Mode**
   - Utilize Docker's rootless mode to mitigate vulnerabilities in daemons and container runtimes.

4. **Avoid Privileged Containers**
   - Refrain from using privileged containers in any environment due to the elevated security risks.

5. **Limit Container Resources**
   - Set memory and CPU limits to minimize the impact of resource-intensive containers in case of compromise.

6. **Segregate Container Networks**
   - Use custom bridge networks to control container communication and avoid connecting sensitive containers to public-facing networks.

7. **Improve Container Isolation**
   - Leverage Linux security capabilities, including namespaces, SELinux, AppArmor, cgroups, capabilities, and seccomp for enhanced isolation.

8. **Set Filesystem and Volumes to Read-only**
   - Run containers with a read-only filesystem to prevent unauthorized modifications.

9. **Complete Lifecycle Management**
   - Implement vulnerability scanning, use a sandbox environment, ensure container immutability, and establish an incident response process.

10. **Restrict System Calls from Within Containers**
   - Monitor and control system calls based on container runtime observations to enhance security.

### Securing Images
11. **Scan and Verify Container Images**
    - Test container images for vulnerabilities before use, especially those pulled from public repositories.

12. **Use Minimal Base Images**
    - Choose minimal base images to reduce the attack surface and build more secure containers.

13. **Don’t Leak Sensitive Info to Docker Images**
    - Avoid hardcoding sensitive information in Dockerfiles; use container orchestrators' secrets management.

14. **Use Multi Stage Builds**
    - Employ multi-stage builds to create smaller, more secure final images without unnecessary dependencies.

15. **Secure Container Registries**
    - Use private registries behind firewalls, apply Role Based Access Control (RBAC), and restrict registry access.

16. **Use Fixed Tags for Immutability**
    - Ensure tag immutability by preferring specific tags, maintaining local image copies, or using Docker Content Trust.

17. **Add the HEALTHCHECK Instruction to the Container Image**
    - Continuously test and automatically restart containers based on health checks for improved availability.

18. **Use COPY Instead of ADD When Writing Dockerfiles**
    - Favor COPY over ADD to reduce security vulnerabilities related to additional features in the ADD command.

### Monitoring Containers
19. **Monitor Container Activity**
    - Implement tools for visibility and monitoring of Docker hosts, container engines, middleware, networking, and workloads.

20. **Secure Containers at Runtime**
    - Implement runtime security measures, including drift prevention, vulnerability patching, and automated response.

21. **Save Troubleshooting Data Separately from Containers**
    - Design a way to troubleshoot containers without direct SSH access by making logs available outside the container.

22. **Use Metadata Labels for Images**
    - Automate labeling processes and use metadata labels to organize containers, ensuring accuracy and compliance.

## Bonus Section: Docker CIS Security Benchmark: Safe Docker Configuration

### Host Configuration
- Create a separate partition for containers
- Harden the container host
- Update Docker software regularly
- Manage Docker daemon access authorization
- Configure Docker files directories
- Audit Docker daemon activity

### Docker Daemon Configuration
- Restrict network traffic between default bridge containers
- Enable user namespace support
- Disable legacy registry operations and Userland Proxy
- Avoid networking misconfiguration
- Configure TLS authentication for Docker daemon
- Set appropriate logging levels and ulimit
- Avoid insecure registries and use fixed tags for containers

### Container Images and Build File
- Create a user for the container
- Ensure containers use trusted images
- Avoid unnecessary packages in containers
- Include security patches during scans and rebuilding processes
- Enable content trust for Docker
- Add HEALTHCHECK instructions to the container image
- Remove setuid and setgid permissions from images
- Use COPY instead of ADD in Dockerfiles
- Install only verified packages
- Avoid update instructions alone in Dockerfiles
- Don’t store secrets in Dockerfiles

### Container Runtime
- Restrict containers from acquiring additional privileges
- Enable AppArmor Profile
- Avoid privileged containers and certain runtime configurations
- Ensure sensitive host system directories aren’t mounted
- Set appropriate CPU priority, restart policy, and open only necessary ports
- Apply SELinux security options and overwrite ulimit
- Avoid sharing host namespaces and devices with containers
- Limit memory usage, bind incoming traffic, and avoid exposing host devices directly
- Confirm cgroup usage, use PIDs cgroup limit, check container health, and update Docker commands

### Docker Security Operations
- Avoid image sprawl and container sprawl

### Docker Swarm Configuration
- Enable swarm mode only if needed
- Create a minimum number of manager nodes
- Bind swarm services to specific host interfaces
- Encrypt containers data exchange
- Manage secrets in a Swarm cluster
- Run swarm manager in auto-lock mode
- Rotate swarm manager auto-lock key periodically
- Rotate node and CA certificates as needed
- Separate management plane traffic from data plane traffic

## Holistic Docker Security with Aqua
Aqua provides an end-to-end security platform for Docker, offering continuous image assurance, runtime security, a container firewall, and secrets management. It supports cloud-native, serverless, and container technologies, securing applications throughout the continuous delivery and DevOps pipeline.

### Continuous Image Assurance
- Scan images for malware, vulnerabilities, secrets, configuration issues, and OSS licensing using Aqua’s vulnerabilities database and Trivy tool.

### Runtime Security for Docker
- Ensure container immutability and prohibit changes to running containers with custom SECCOMP profiles, least privilege enforcement, and network controls.

### Container Firewall for Docker
- Visualize network connections, develop rules based on application services, and whitelist connections within and between clusters.

### Secrets Management
- Securely transfer secrets to containers at runtime, encrypt them at rest and in transit, and integrate with enterprise vaults for secure secret management.

### Compliance Enforcement
- Implement granular audit trails, perform CIS certified benchmark checks
