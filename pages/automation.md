# Infrastructure Automation: Terraform & Ansible

As a Cloud/DevOps Engineer, I follow the "Infrastructure as Code" (IaC) philosophy to ensure environments are reproducible, scalable, and version-controlled.

## The Toolset Strategy
I utilize a "Best of Breed" approach by combining Terraform and Ansible:
* **Terraform:** Best for **Provisioning**. It manages the lifecycle of infrastructure (VPCs, VMs, Databases) using a *declarative* approach.
* **Ansible:** Best for **Configuration Management**. It handles software installation, security patching, and OS hardening using an *agentless* approach via SSH.

---

## 1. Terraform: Infrastructure Provisioning
Terraform allows us to define our desired state. If a VM is manually deleted, Terraform will detect the "drift" and recreate it.

### Best Practices
* **Remote State:** Always store `.tfstate` files in a remote backend (like AWS S3 or Azure Blob) with state locking (DynamoDB) to prevent corruption during team collaboration.
* **Modularization:** Break code into reusable modules (e.g., `modules/compute`, `modules/network`) to keep code DRY (Don't Repeat Yourself).
* **Plan Before Apply:** Always run `terraform plan` to preview changes before they affect production.

### Example: Provisioning a Linux VM (AWS)
```hcl
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0" # Ubuntu 20.04 LTS
  instance_type = "t2.micro"

  tags = {
    Name = "DevOps-Project-VM"
    Env  = "Development"
  }
}

2. Ansible: Configuration & PatchingAnsible excels at executing tasks across hundreds of servers simultaneously without needing any software installed on the "target" machines.Best PracticesIdempotency: Ensure playbooks can be run multiple times without changing the result if the system is already in the desired state.Use Roles: Organize tasks, variables, and handlers into Roles to make automation scripts portable.Vault for Secrets: Use ansible-vault to encrypt sensitive data like API keys or passwords within your playbooks.Example: Applying Security Patches to LinuxThis playbook updates all packages to their latest security versions and reboots the server if necessary.YAML---

Example:
---
- name: Security Patching Playbook
  hosts: all
  become: yes
  tasks:
    - name: Update all packages (Ubuntu/Debian)
      apt:
        update_cache: yes
        upgrade: dist
      when: ansible_os_family == "Debian"

    - name: Update all packages (RHEL/CentOS)
      yum:
        name: "*"
        state: latest
      when: ansible_os_family == "RedHat"

    - name: Check if a reboot is required
      stat:
        path: /var/run/reboot-required
      register: reboot_required_file

    - name: Reboot server if patches require it
      reboot:
        msg: "Rebooting to apply security patches"
      when: reboot_required_file.stat.exists

3. Use Cases for AutomationUse CaseRecommended ToolWhy?Creating a VPC & SubnetsTerraformHandles complex cloud resource dependencies.Installing Nginx & PHPAnsibleBetter at file manipulation and service management.Scaling Cluster sizeTerraformBuilt to manage resource counts and state.User ManagementAnsibleSimplifies adding/removing SSH keys across many nodes.
