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
