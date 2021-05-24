---
title: "Adding the Repository"
description: "This page describes how to add my APT repository."
lead: "This page describes how to add my APT repository."
date: 2021-05-19T09:41:42+10:00
lastmod: 2021-05-19T09:41:42+10:00
draft: false
images: []
menu:
  docs:
    parent: "apt-repository"
weight: 210
toc: true
---

### Manual Installation

1. Update the APT cache and install the prerequisite packages:

{{< btn-copy text="sudo apt-get update && apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common" >}}

```console
sudo apt-get update && apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

2. Add the repository GPG signing key to the APT trust:

{{< btn-copy text="sudo curl -fsSL https://apt.jameselliott.dev/keyring.gpg -o /etc/apt/trusted.gpg.d/jameselliottdev.gpg" >}}

```console
sudo curl -fsSL https://apt.jameselliott.dev/keyring.gpg -o /etc/apt/trusted.gpg.d/jameselliottdev.gpg
```

3. Verify the GPG signing key you added is correct:

{{< btn-copy text="sudo gpg --keyring /etc/apt/trusted.gpg.d/jameselliottdev.gpg --fingerprint 23139287" >}}

```console
sudo gpg --keyring /etc/apt/trusted.gpg.d/jameselliottdev.gpg --fingerprint 23139287
```

```text
pub   rsa4096 2021-01-06 [C]
      3011 AD01 ACED 219F 5319  12D0 F901 891F 2313 9287
uid           [ unknown] James Elliott 
sub   rsa4096 2021-01-06 [S] [expires: 2024-01-06]
sub   rsa4096 2021-01-06 [E] [expires: 2024-01-06]
sub   rsa4096 2021-01-06 [A] [expires: 2024-01-06]
```

4. Add the repository to APT's sources.list.d:

{{< btn-copy text="echo \"deb https://apt.jameselliott.dev/archive $(lsb_release -cs) main\" | sudo tee /etc/apt/sources.list.d/jameselliott.dev.list" >}}

```console
echo "deb https://apt.jameselliott.dev/archive $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/jameselliott.dev.list
```

### Ansible Playbook

The following Ansible Playbook will setup the repository.

```yaml
- name: Setup James Elliott's APT Repository (apt.jameselliott.dev)
  hosts: localhost
  become: yes
  tasks:
  - name: Ensure the Required Dependencies are Installed
    ansible.builtin.apt:
      cache_valid_time: 600
      name:
        - apt-transport-https
        - ca-certificates
        - gnupg-agent
        - software-properties-common
      state: present
  - name: Ensure James Elliott's GPG Signing Keyring is Present
    ansible.builtin.apt_key:
      id: 3011AD01ACED219F531912D0F901891F23139287
      url: https://apt.jameselliott.dev/gpg
      keyring: /etc/apt/trusted.gpg.d/jameselliott.dev.gpg
      state: present
  - name: Ensure James Elliott's Repository is Present
    ansible.builtin.apt_repository:
      repo: "deb https://apt.jameselliott.dev/archive {{ ansible_distribution_release }} main"
      filename: /etc/apt/sources.list.d/jameselliott.dev
      state: present
      update_cache: yes
```