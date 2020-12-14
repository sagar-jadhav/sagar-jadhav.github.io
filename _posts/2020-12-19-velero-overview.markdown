---
layout: post
title:  "A quick introduction to Velero"
date:   2020-12-19
categories: [kubernetes]
---

![A quick introduction to Velero](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/overview_velero.png)

# Introduction

- Formerly known as "Heptio Ark"
- It provides tools to Backup and Restore K8s cluster
- It consists of the following components:
    - **Server:** Runs on K8s cluster
    - **CLI:** Runs locally
- Current release: v1.5.x
- GitHub stars: 4.6K+ 

Checkout [here](https://velero.io/) for more details

# Architecture

![Velero Architecture](https://velero.io/docs/v1.5/img/backup-process.png)
**Source:** [https://velero.io/docs/v1.5/img/backup-process.png](https://velero.io/docs/v1.5/img/backup-process.png)

Velero supports the following operations:
- On-demand backup
- Scheduled backup
- Restore

Each operation is a custom resource defined with the custom resource definition and stored in etcd. Velero has controllers that act on these resources.

## On-demand backup
Creates a copy of k8s objects in the form of tarball and uploads that tarball to cloud object storage

**Note:** Backup operation is not atomic.

## Scheduled backup
As the name suggests you can schedule the backup at a particular time. You can also schedule recurrent backups. Provide `Cron` expression to specify a schedule. For e.g. Use the `0 0 * * *` Cron expression to take backup once a day.

## Restore
Creates k8s objects from the definition stored in cloud object storage.

**Note:** As a good practice always set the mode of backup storage location to `Read-Only` during restore to avoid update or deletion of backup.

Velero uses cloud object storage as a source of truth. It synchronizes data between cloud object storage and the K8s cluster.

# Features
- Filtering k8s objects based on type, namespace & label during backup and restore
- TTL (Time to Live) for backups. Backup resources will be deleted after TTL is reached
- Different lifecycle hooks for both backup and restore operations
- Supports namespace remapping i.e. K8s object from namespace `A` can be restored to namespace `B`