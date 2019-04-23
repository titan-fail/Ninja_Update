Invoice Ninja Self-Hosted Update v4.7.1
==
 
USE AT YOUR OWN RISK
--
 
This script will automatically update your Invoice Ninja install to the latest version.
It does this by checking https://invoiceninja.org for the latest version string, and then
comparing it to the string in your local version.txt file (/ninja/storage/version.txt). You
have two different options for using this script: it can be run it manually any time you
want to check for an update, or you can place it in a crontab to have it run on a set
schedule. The important commands all output to stdout, so you can direct to a logfile if
you so choose.
 
If you are updating from a version prior to 4.3.0, it will attempt to manually delete the
compiled.php located in /bootstrap/cache/ under your Invoice Ninja directory. If the file is
not there, it will move on.
 
Please note that this DOES NOT backup the MySQL database. If you would like to backup the
database, consider running mysqldump on a similar schedule.
 
This script makes a couple assumptions in order to be completely hands-off.
 
1. You have locate installed.
 
2. You have ONLY ONE copy Invoice Ninja installed on your system (see below).
 
3. You have sudo access, either to run manually or to place the script in the root's crontab.
   This access is required by the rsync, chown, and chmod commands. It's also required to
   remove the downloaded files, which are put in /usr/local/download.
 
4. The partition containing /usr/local has enough space to store the downloaded ZIP file
   along with the extracted files that will be synced to your Invoice Ninja install
   location.
 
CAVEATS
--
 
While the script will detect whether or not you are using UPDATE_SECRET in your .env file,
running the update migration commands may not work if UPDATE_SECRET is present, and will
cause wget to return file not found errors.
Re-running wget --spider 'yourninjaurl/update?secret=yoursecret' again or simply
pointing your browser to that URL will successfully complete the migration commands. This
is a known issue, and I'm still trying to figure out what exactly is going on.
 
If you have more than one copy of Invoice Ninja extracted on your system, the script will
cause problems. This is due to using locate to determine where Invoice Ninja is installed.
Make sure that the only copy of the Invoice Ninja directory structure present on your system
is the one the app is actually running from, to prevent locate from setting multiple values
in the $ninja_home variable and causing problems.
