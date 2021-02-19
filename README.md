# ansible-rclone-jobber
An ansible role that configures rclone_jobber for backups.
https://github.com/wolfv6/rclone_jobber

# Requirements
Requires a valid rclone configuration on target host. https://github.com/stefangweichinger/ansible-rclone is recommended.

# Example configuration
```
rclone_jobber_config:
  - file_name: home_backup
    src: "$HOME"
    dst: "google_drive:"
    opts: "--dry-run"
    move_old_files: "dated_directory"
    monitor_url: "https://hc-ping.com/1234-5678-abcde"
    job_name: "$(basename $0)"
    filter: yes # everything except for explicit items below will be filtered
    include_files:
      - ".bashrc" # config file
      - "direc1/.thingrc" # file within directory
      - ".git/**" # entire git folder
    exclude_patterns:
      - "*_exc/**" # directory names ending in _exc
      - ".*/**" # hidden directories
      - "*.bak" # file names with extension
    include_folders:
      - "direc_empty/**"
      - "direc0/**"
    cron: yes
    # https://docs.ansible.com/ansible/latest/collections/ansible/builtin/cron_module.html
    weekday: "5"
    minute: "00"
    hour: "02"
    dom: "5"
```