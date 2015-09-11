# Jeap 2.0 Development Record

### Core Scripts:

- jeap.py
- lease_listen.py
  - sample.leases
  - known_host.txt

### Development Thoughts:
 > thinking about do it in multithread
 1. Initialization phase:
   * Web scraping with help of BeautifulSoup
   * Get key info from JTAC Recommended Version webpage
   * Store info into a local dictionary, periodically refresh
   * Key attributes are **model**, **Junos version**

 2. Start listening(_always running_):
   * Check _dhcp.lease_ frequently, compare(hash function or so) with known ips stored locally(private list)
   * found new ip(s), put into a private list(arraylist, stack, queue etc.)

 3. jeap.py phase:
   * Get private dictionary
   * Read new hosts from ips in queue, open connection to get their current configuration, and store into a dictionary
   * Compare current software version with recommended ones
     * If need updates, delete this address from known_host list,reach out to download latest version and autoinstall `lots of work`, and start all over again 
     * If not, continue
   * Based on known info, gather config files based on some customer policy(e.g. MAC, #sn, ip, subnet etc.)
   * `Policy` `File Assembly Module`
