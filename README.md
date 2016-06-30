# pfs_backup
Perform backups of all pfSense firewalls in pfs_backup.conf.  Works with all 2.x pfSense releases.
On first run, it will output a sample config file for you to build on.

Here is a short sample pfs_backup.conf:
```
# Empty lines and lines starting with # are ignored.
#
# Options in [defaults] are used for all entries unless
# overridden in a firewall-specific entry.
#
# For each [firewall] entry, a single 'host' option
# is required. You only need to specify the others if
# you want to override defaults for that firewall.
#
# You _must_ have 'username', 'password', 'skiprrd',
# 'verify_ssl', and 'directory' in [defaults], even 
# if intending to redefine them per-firewall and thus
# no defaults are actually used.

[defaults]
# Highly recommended to create a backup-only user and
# _not_ store admin or even r/w credentials here.
username  = backup-user
password  = your-backup-pass
#   Location where configs are written (no trailing /).
directory = /path/to/backups
#   Skip backup of RRD data? Much smaller backups if
#   you don't mind losing graph data on a restore.
skiprrd = yes 
#   Verify the SSL certificate on connection?
verify_ssl = no

[firewall01]
# Uses all default options
host = 172.19.231.254

[firewall02]
# Overrides all the default options
host = firewall02.example.com
skiprrd = no
directory = /alt/backup/path
username = different-user
password = some-different-pass
verify_ssl = yes

[firewall03]
# Overrides only 'skiprrd'
host = fw03.example.com
skiprrd = no
```


Simply requires:

  - requests (python-requests pkg on Fedora)
  - BeautifulSoup4 (python-beautifulsoup4 on Fedora)
  - ConfigParser (python-configparser on Fedora)

As you're storing credentials in a .conf file, you should both limit permissions on the file itself
and use a separate user for backups.  You can create a backup-only user from pfSense's User Manager with
only two permissions set in the "Effective Privileges" section:
  - WebCfg - Diagnostics: Backup/restore page
  - User - Config - Deny Config Write

Bugfixes/improvements welcome, I'm still learning.
