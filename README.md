YasuhiroABE.homegw-network
==========================

This role initializes /etc/network/interfaces and /etc/resolv.conf files on debian and ubuntu for my gateway router, APU2C.

                   +----------+---+---------+
           <isp>---|  ens33   |   |         |
                   +--+-------+ A |         |
                   |  | ens34 | P | dnsmasq |
       <switch A>--|  ---+    | U | pppoe   |
                   | br0 |----| 2 | ...     |
       <switch B>--|  +--+    | C |         |
                   |  | ens35 |   |         |
                   +--+-------+---+---------+

Requirements
------------

This role is tested on the following platforms.

### Ansible
- Version 2.4

### Distributions
- Ubuntu 16.04
- Debian 9

Role Variables
--------------

### Default

    # DNS server list in /etc/resolv.conf (example: [192.168.0.1])
    homegw_network_setup_nameservers: []
    
    # Domain list in /etc/resolv.conf (example: [8.8.8.8]
    homegw_network_resolv_search: []
    
    # Internal ip address (example: 192.168.0.1/24)
    homegw_network_setup_br0_hostprefix: ''
    
    # List of the eth device name for br0 bridge-ports
    homegw_network_setup_br0_devices: []
    
    # External eth device name (example: ens33)
    homegw_network_setup_external_device: ''
    
    # External ip address (example: 172.16.10.1/24)
    homegw_network_setup_external_hostprefix: ''
    
    # [Optional] If you have a gateway at your external network, please set the ip address. (example: 172.16.0.1)
    homegw_network_setup_external_gateway: ''

    # Labels for the ansible blockinfile module 
    # Each line shuould be unique.
    homegw_network_setup_lo_label: 'ANSIBLE LO CONFIG'
    homegw_network_setup_br0_label: 'ANSIBLE BR0 CONFIG'
    homegw_network_setup_br0_manual_label: 'ANSIBLE ETHDEV MANUAL CONFIG'
    homegw_network_setup_external_label: 'ANSIBLE EXTERNAL CONFIG'

Dependencies
------------

N/A

Example Playbook
----------------

    - hosts: servers
      vars:
        homegw_network_setup_br0_hostprefix: 192.168.39.1/24
        homegw_network_setup_br0_devices:
          - ens34
          - ens38
        homegw_network_setup_external_device: ens33
        homegw_network_setup_external_hostprefix: 10.1.1.88/24
        homegw_network_resolv_nameservers:
          - 8.8.8.8
        homegw_network_resolv_search:
          - example.org.
      roles:
        - YasuhiroABE.homegw-network

License
-------

Apache License 2.0

Author Information
------------------

[Yasuhiro ABE](http://www.yasundial.org/foaf.xml)

