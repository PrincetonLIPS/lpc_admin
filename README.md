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

Further documentation can be found in the [Playbooks README](https://github.com/PrincetonLIPS/lpc_admin/blob/master/playbooks/README.md)

