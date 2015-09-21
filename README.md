# Jeap 2.0 Development Record

### Core Scripts:

- jeap.py
- ~~lease_listen.py~~
  - ~~sample~~  dhcpd.leases
  - ~~known_host.txt~~ ==> known_host list

### Development Thoughts:
 `thinking about do it in multithread`
 1. Initialization phase:
   - [x] Web scraping with help of BeautifulSoup
   - [x] Get key info from JTAC Recommended Version webpage
   - [x] Store info into a local dictionary, periodically refresh
   - [x] Key attributes are **model**, **Junos version**

 2. Start listening(_always running_):
   - [x] Check _dhcp.lease_ frequently
   - [ ] Compare( ~~hash function or so~~  `in` for string) with known ips stored locally(private list)
   - [ ] found new ip(s), put into a private list(~~arraylist, stack, queue etc.~~ `list`)

 3. jeap.py phase:
   * Get private dictionary
   * Read new hosts from ips in queue, open connection to get their current configuration, and store into a dictionary
   * Compare current software version with recommended ones
     * If need updates, delete this address from known_host list,reach out to download latest version and autoinstall __lots of work__, and start all over again 
     * If not, continue
   * Based on known info, gather config files based on some customer policy(e.g. MAC, #sn, ip, subnet etc.)
   * more thoughts on `Policy` and `File Assembly Module`

###  Brief History
 Weekly summary :sunny: Sep 18 2015
 - SecIntel for a whole day :pizza: :tropical_drink:
 - run another python online tutorial for 2 days :sleepy:
 - installed 'Pycharm' for python IDE environment, makes my life so much easier :kissing_smiling_eyes:
 - finished optimizing scraper_bike() inherited from Logan, use a thread to constantly refreshing it :+1:
 - finished optimizing lease_read() inherited from Logan, use another thread to periodically update. Able to automatically extract ip addresses from *dhcpd.leases* file ranging from '0.0.0.0 to 255.255.255.255' with help of __regular expresion__, a tough one, spent a lot of time. May need to change a little bit for the range in the future. :+1:

:question:Potential Questions: 
 - is there a way to change the sleep time interval for threading, e.g. stop threading -> set new time value -> restart threading :scream:

:date: Next Week:
- [ ] NYC for 3 days, potential customer meetings
- [ ] Some time for SecIntel before Shruti leave
- [ ] Start working on core part for jeap.py
