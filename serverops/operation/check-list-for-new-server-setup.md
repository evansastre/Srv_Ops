# Check list for new server setup

1. Change Administrator password
2. Add Company/Dev account
3. Windows firewall setup 
   * Drop TCP/UDP 445,135-139 port
   * Disable all default firewall settings for both inbound and outbound
   * Make sure firewall state is on for Domain/Private/Public Profile
4. Change remote port number
5. Change computer name/hostname/Net bios computer name
6. Set DNS server
7. WSUS client config, let it connect to WSUS server
8. Windows is update to date
9. Install salt-minion
10. Install zabbix-agent
11. Update server hardware list
12. Date format/Location/System locale: English\(United States\)
13. Time Sync - set NTP server
14. Hard disk partition, format and allocation unit size
15. Power Options: High performance
16. DB server: Install .Net Framework 3.5.1 \(Server manager → Features\)



