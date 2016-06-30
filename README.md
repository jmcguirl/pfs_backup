# pfs_backup
Perform backups of all pfSense firewalls in pfs_backup.conf.  Works with all 2.x pfSense releases.
On first run, it will output a sample config file for you to build on.

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
