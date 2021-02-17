# ansible-rclone-jobber
An ansible role that configures rclone_jobber for backups.
https://github.com/wolfv6/rclone_jobber

# Requirements
Requires a valid rclone configuration on target host. https://github.com/stefangweichinger/ansible-rclone is recommended.

# Example configuration
rclone_jobber_config:
  - file_name: docker_backup
    src: /mnt/storage/pictures
    dst: "google_drive:" # Name of remote rclone config
    opts: "--dry-run"
    move_old_files: "dated_directory"
    monitor_url: "https://hc-ping.com/12345-6789-abcd-efgh
    job_name: "$(basename $0)"
    filter: yes
    includes:
      - direc0/** # full directory
      - .bashrc # hidden files
      - *.jpg # all jpegs
    excludes:
      - *.tmp # temp files
      - .* # hidden files
    cron: yes
