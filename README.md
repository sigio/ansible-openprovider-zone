Openprovider Zone Update
========================

An Ansible role to update OpenProvider hosted DNS zones.

Note that OpenProvider only allows you to update/publish the following record-types via
this api: A, AAAA, CNAME, MX, SPF, SRV, TXT, TLSA, SSHFP, CAA.
In the documentation it states that 'NS' records can be used if contacting support first.

Requirements
------------

Openprovider.eu API account, username and password or password-hash.

Role Variables
--------------

openprovider_username: "your_openprovider_username"
openprovider_password: "your_password, but not needed if you use the hash"
openprovider_pwhash: "your password hash for the webapi"
openprovider_api: https://api.openprovider.eu
openprovider_default_ttl: "3600"

openprovider_zones: The zones (split out into zonename and tld, and the dict of records.

Example:

testingzone_tld_records:
  - { name: "www", type: "A", value: "192.0.2.80" }
  - { name: "www", type: "AAAA", value: "2001:DB8::80" }
  - { name: "", type: "A", value: "192.0.2.100" }

otherzone_com_records:
  - { name: "www", type: "A", value: "192.0.2.80" }
  - { name: "www", type: "AAAA", value: "2001:DB8::80" }

openprovider_zones:
  - { zonename: "testingzone", zoneext: "tld", records: "{{testingzone_tld_records}}" }
  - { zonename: "otherzone", zoneext: "com", records: "{{otherzone_com_records}}" }


Dependencies
------------

None

Example Playbook
----------------

    - hosts: localhost
      roles:
         - { role: sigio.openprovider-zone }

License
-------

BSD

Author Information
------------------

Mark Janssen <info@sig-io.nl>
Sig-I/O Automatisering
