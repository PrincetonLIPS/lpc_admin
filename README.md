![Kamaji GPU](https://healthchecks.io/b/2/8ec56db3-8ed9-451d-8ef4-41cbd684a33f.svg)
![Kamaji Uptime](https://healthchecks.io/b/2/8fd677f1-727d-44ce-bbfb-5bc1e523b56a.svg)
![Yubaba GPU](https://healthchecks.io/b/2/5732116b-b11b-4aad-a3bb-d62686bdacf0.svg)
![Yubaba Uptime](https://healthchecks.io/b/2/098e2288-4279-4953-a981-dd0ef760bbc2.svg)
![Zeneba GPU](https://healthchecks.io/b/2/aae54f51-80dd-459b-bd83-bd62700254d0.svg)
![Zeneba Uptime](https://healthchecks.io/b/2/084e72ba-11b8-4011-af32-7bcb5dc53e35.svg)

# LIPS Private Compute Configuration Management

## Background
This repository contains a collection of configuration management and system administration tools for the LIPS Private Compute (LPC) systems. Primarily, configuration management rose in popularity with the increasing need for automation and repeatability associated with operations. In our case, I manage only four servers, but because a new administrator (or multiple administrators) will need to be brought up to speed when I leave the lab, configuration management serves a dual role as both an administration convenience, but also as a form of automatic documentation for new administrators. In some sense the administration policies (backups, logging, software/package management, network file system, user management) are concretized in the configuration management code. 

Of course there will always be ad-hoc administration duties that require real-time attention and may not be built into the configuration management system, but I aim to capture as much as I can in this repository. 

## Playbook Descriptions

### Administration Tools 
- Link: [admin_tools.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/admin_tools.yml)

Installs several administrative monitoring tools and configures them. [Logwatch](https://sourceforge.net/projects/logwatch/) is configured to flag logs of interest, and sends me a daily status email for each of our hosts, as well as a more detailed system report on a weekly and monthly basis. [Cockpit](https://cockpit-project.org/) integrates with Ansible and enables a sleu of administrative tasks through a simple API: configuring firewalls, managing virtual machines, inspecting hardware and managing software updates, as well as user accounts and systemd services. 

### Automated Backups 
- Link: [backups.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/backups.yml)

Installs and configures [rsnapshot](https://rsnapshot.org/) a filesystem snapshot utility based on [rsync](https://linux.die.net/man/1/rsync). Copies a configuration file (also under version control [here](https://github.com/PrincetonLIPS/lpc_admin/blob/master/templates/rsnapshot.j2)) to the hosts to configure daily, weekly, and monthly log rotations onto an external 5TB SSD. 

### Container Management 
- Link: [containers.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/containers.yml)

Configures Docker, Docker GPG security and maintains a collection of default container images for use across each host: 
  - Alpine Linux
  - Ubuntu Linux
  - Nvidia CUDA 12 Development Image (with CUDNN 8)
  - PyTorch 2.0 (CUDA 11.7/CUDNN 8.1) Development Image
  - Tensorflow (CUDA 12.2) Development Image

### Nvidia GPU Configuration 
- Link: [cuda.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/cuda.yml)

Installs linux kernel headers, configures GPG security, and installs CUDA and the CUDA toolkit across each host. 

### Developer Tools 
- Link: [development_tools.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/development_tools.yml)

Updates core development tools and ensures they are at the latest version. See the list of maintained tools [here](https://github.com/PrincetonLIPS/lpc_admin/blob/master/variables/development_tools.yml). 

### OpenLDAP Client Configuration 
- Link: [ldap_client.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/ldap_client.yml)

Manages [OpenLDAP](https://www.openldap.org/) client configuration. Includes templated configurations for [SSSD](https://github.com/PrincetonLIPS/lpc_admin/blob/master/templates/sssd.j2), [PAM](https://github.com/PrincetonLIPS/lpc_admin/blob/master/templates/pam_common_session.j2), [NSLCD](https://github.com/PrincetonLIPS/lpc_admin/blob/master/templates/nslcd.j2), and of course [LDAP](https://github.com/PrincetonLIPS/lpc_admin/blob/master/templates/ldap.j2) itself. 

### Network File System Client Configuration 
- Link: [nfs_client.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/nfs_client.yml)

Configures the NFS clients (Kamaji and Zeneba). Installs [nfs-common](https://packages.debian.org/sid/nfs-common), creates mount points, mounts the remote backup volume (and soft links it). 

### Network File System Server Configuration 
- Link: [nfs_server.yml](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/nfs_server.yml)

Configures NFS server (Yubaba). Templates the server configuration and configures the firewall. 
