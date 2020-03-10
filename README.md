# GCP IMAGE

## Description

A simple role to create a GCP (Google cloud platform) VM, install some stuff on it's disk
then save that disk as an image.

## How to use

I use this through flags to trigger different behaviors. 

Here's an example snipped of a playbook to do so.
```yaml
- hosts: localhost
  tasks:
  - include_role:
      name: image
    vars:
      new_image: true
      instance_name: 'jeffo-image-creation-vm'
  tags: [ 'image' ]

- hosts: gcp_working_image
  tasks:
  - include_role:
      name: image
    vars:
      modify_image: true
  tags: [ 'image' ]

- hosts: localhost
  tasks:
  - include_role:
      name: image
    vars:
      save_image: true
      instance_name: 'jeffo-image-creation-vm'
      saved_image_name: 'jeffo-compute-image'
  tags: [ 'image' ]
```

## Variables

These variables you have to define, there are no defaults for.
```yaml
# when installing things you'll need to specify the user and key
# ansible needs to ssh into it
working_vm_user: changeme
working_vm_key: changeme
```

Check the [defaults](defaults/main.yml) file for other defaults.
