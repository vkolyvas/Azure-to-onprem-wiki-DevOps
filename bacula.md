# Bacula – Installation & Configuration
Bacula is an enterprise-grade backup solution.

Installation (Ubuntu)
bash
sudo apt update
sudo apt install -y bacula-server bacula-client bacula-console
Configuration
Configure Bacula Director, Storage Daemon, and File Daemon in their respective config files.

Define backup jobs, file sets, and schedules.

Configure storage devices, volumes, and retention policies.

Reload/restart Bacula services and run test jobs to verify backups and restores.
