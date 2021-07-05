---
title : "About"
description: "About me"
lead: "I am an experienced developer who practices development for a profession and a hobby. I regularly contribute to open source projects, and am one of the maintainers of the Authelia open source project."
date: 2021-05-19T09:41:42+10:00
lastmod: 2021-05-19T09:41:42+10:00
draft: false
weight: 50
images: []
type: myabout
---

I am an experienced developer who practices development for a profession and a
hobby. I regularly contribute to open source projects, and am one of the
maintainers of the [Authelia](https://github.com/authelia/authelia) open source
project.

My day job is relatively broad but mostly revolves around data analysis; but
also has a healthy level of devops type workloads, systems integration, and
general automation.

## Kubernetes

I love Kubernetes. I run a fairly nice highly available home cluster
specifically for experimenting and general hobbying.

My cluster consists of haproxy servers (currently two) with floating IP
addresses controlled by keepalived. Each proxy has an IP address it has
priority for making the setup active-active.

My haproxy load balances both the Kubernetes API Server and my chosen
Ingress provider (currently traefik) which runs as a DaemonSet with a NodePort
service. This means that any single node can fail and a majority of all
services remain fully functional provided they can be deployed into the cluster
as a highly available Pod.

## Languages

The languages I use on a daily basis are:

- go
- C#
- Python

The other languages I occasioanlly use are:

- C
- C++
- JavaScript/TypeScript (nodejs)

The other languages I've dabbled in are:

- Java/Kotlin
- PHP
- Rust
- Julia
- F#

# Tools

Some of the tools I use to accomplish both my day job and my hobbies include:

- [Ansible](https://www.ansible.com/) for configuration management

- [ArgoCD](https://argoproj.github.io/argo-cd/) for Kubernetes continuous
  deployment

- [HashiCorp Vault](https://www.vaultproject.io/) for secrets storage

- [Jaeger](https://www.jaegertracing.io/) for tracing in Kubernetes

- [Sealed Secrets](https://github.com/bitnami-labs/sealed-secrets) for basic
  secret storage in code

- [JetBrains](https://www.jetbrains.com/) for developing in go/python and
  drafting database schemas

- [Visual Studio](https://visualstudio.microsoft.com/) for developing in C#

- [VS Codium](https://vscodium.com/) as an editor for anything I don't use a
  specific IDE for

- [Buildkite](https://buildkite.com/) for continuous integration
