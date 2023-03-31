Ansible Role: VMware CSI Deploy
=========

Deploy the VMware CSI driver on a VM based K8s cluster. This role is still very much a work in progress and needs improvement in terms of flow, fragility and idempotency.

Requirements
------------

None.

Role Variables
--------------

The following are default variables:
    # Storage Class name to use for CSI driver
    storage_class: "vmw-block-sc"

    # 2.7.0 is compatible with K8s 1.23 1.25
    # https://docs.vmware.com/en/VMware-vSphere-Container-Storage-Plug-in/2.0/vmware-vsphere-csp-getting-started/GUID-D4AAD99E-9128-40CE-B89C-AD451DA8379D.html
    csi_version: "v2.7.0"

    # vCenter information
    vcenter_ip: 10.100.24.31
    vcenter_hostname: devvcsa.tme.nebulon.com
    vcenter_username: "{{ vault_vcenter_username }}"
    vcenter_password: "{{ vault_vcenter_password }}"
    vcenter_datacenter: "SC0"

Additionally there are two URL prefix variables defined in the vars/main.yml file.

Dependencies
------------

None.

Example Playbook
----------------

    # ===========================================================================
    # Install the VMware CSI driver
    # ===========================================================================
    - name: VMware CSI driver install
      hosts: k8s_master
      become: true
      gather_facts: false
      tags: play_vmware_csi

      vars_files:
        # Ansible vault with all required passwords
        - "../../credentials.yml"

      roles:
        - { role: ansible-role-vmware-csi-deploy,
            vcenter_ip: "10.100.24.31",
            vcenter_hostname: "devvcsa.tme.nebulon.com",
            vcenter_datacenter: "SC0"
        }

License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
