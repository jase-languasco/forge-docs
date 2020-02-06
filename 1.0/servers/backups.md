# Backups

[[toc]]

## Overview

Forge provides automatic database backups which you can schedule directly within the dashboard. You can choose to backup one or more databases at a custom frequency and restore to a point of time. The backup script is open source and can be [found on GitHub](https://github.com/laravel/forge-database-backups).

:::warning Business Plan Only
Backups are only available on the Business plan.
:::

## Creating Backup Configurations

### Storage Providers

You can choose to backup your databases to:

1. Amazon S3
2. DigitalOcean Spaces

For both storage providers you need to provide Forge with:

- Region (`eu-west-2`, `nyc3` etc..)
- Bucket
- Access Key
- Secret Key

You can also choose to provide a storage directory, for example `backups/server-name`. If left empty, backups will be made to the root of your bucket.

### Frequency Options

Within the Forge UI, you can select one frequency:

- Hourly
- Daily (at a given time)
- Weekly (on a given weekday and time)

If you're using the API to create a **Daily** or **Weekly** backup, you may provide any valid time (e.g. `13:37`) to your schedule however, for the sake of simplicity, the Forge UI allows you to select a time in 30 minute intervals. The time you select is in local time and will be converted to UTC on the server.

:::tip Bespoke Frequencies

If you need to use a more bespoke frequency for your backups then you should manually modify the `/etc/crontab` entry generated by Forge once your backup is created.
:::

### Backup Retention

Forge can automatically trim old backups for you. If you have a retention rate of five, then only the five latest backups will exist at any one time. Forge will remove older backups once the latest backup process has completed.

### Notifications For Failed Backups

You may provide an email address to be notified when a backup fails. If you need to notify multiple people, you should create a distribution list such as `team@example.com`.

Forge will also display failed backups within the **Backups** panel of the dashboard.

## Managing Backups

### Deleting Backup Configurations

You can delete a backup configuration by clicking the Delete button next to your chosen backup under the **Active Backups** section.

:::tip Backup Archives

When deleting a backup, your backup archives **will not be removed**. You must remove these manually.

:::

### Backup Immediately

If you need to take a backup immediately, you can use the **Backup Now** button.

### Restoring Backups

You can restore backups from the **Recent Backups** section. Click the **Restore** button next to your chosen backup.

### Deleting Backups

If you need to delete an individual backup, you can do this by clicking the View button on a backup and then clicking the Delete button on the chosen backup.

:::danger Deleting Backup Logs

When deleting a backup log, your backup archives **will be removed**. Please be careful when removing backup logs.

:::

### Backup Output

Each backup process will create its own log so that you can inspect the output in the event of a failure. You can view the output of a backup by clicking the Eye icon next to your backup.