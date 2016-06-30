# pfs_backup
Perform backups of all pfSense firewalls in pfs_backup.conf.  Works with all 2.x pfSense releases.
On first run, it will output a sample config file for you to build on.

Simply requires:

  - requests (python-requests pkg on Fedora)
  - BeautifulSoup4 (python-beautifulsoup4 on Fedora)
  - ConfigParser (python-configparser on Fedora)
