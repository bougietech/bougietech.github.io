---
title: Integrating CardDAV server with FreePBX for Caller ID
published: false
---

When helping a client migrate from a cell phone to a FreePBX VOIP phone system, I was looking for a good contact management system. The main requirement was a way to display the names of saved contacts on the IP phones for incoming calls.

Many VOIP handsets have an LDAP phonebook feature. When a call comes in, they can query an LDAP server with the phone number and display the name if a contact with a matching number is found.

Most contact management systems I am aware of support the CardDAV protocol but not LDAP. So I was happy to discover [this project](https://projects.shbe.net/projects/l2cpbg). L2CPBG = LDAP-to-CardDAV Phone Book Gateway. This lightweight utility acts as a bridge between LDAP-capable phones and a CardDAV server such as Synology Contacts or Nextcloud Contacts.

The project isn't opensource, but the developer is responsive helpful. There is a free version with limitations, and the dev is happy to provide a license key for testing.

I installed the `.deb` package on a Ubuntu machine and edited `/etc/l2cpbg.conf` with my settings, most of which are self-explanatory.

Here is where the LDAP server and CardDAV sources are configured:
```
[ldap]
  host      = "0.0.0.0"
  port      = 1389
  base      = "dc=l2cpbg, dc=com"

[ldap.bind]
  dn   = "cn=phone"
  pass = "my_secure_password"

[dav]
  server       = "http://url-to-shared-addressbook-in-synology-contacts"
  user         = "synology_username"
  pass         = "secure_synology_password"

addressbooks = "My Contacts"
```