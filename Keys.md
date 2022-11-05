Node Key File
=============

<node-url>.key.json
-------------------

### filedata
  - vendor
    - Privateness

  - type
    - key

  - for
    - node

  - filename
    - <node-url>.key.json


### keys
  - private
  - public
  - verify


### url

### nonce
  - cryptographic salt


### master-user
  - master user (admin) name


### tags
  - coma,separated,tags


### tariff
  - amount of coin hours per each tick count


### worm
  - <worm>


directory
---------

### flashdrive

User Key File (flashdrive)
==========================

<username>.key.json
-------------------

### filedata
  - vendor
    - Privateness

  - type
    - key

  - for
    - user

  - filename
    - <username>.key.json


### keys
  - private
    - [array of keys]

  - public
    - [array of keys]

  - verify
    - [array of keys]

  - current
    - current key index (private, public, verify)


### nonce
  - cryptographic salt


### tags
  - coma,separated,tags


### worm
  - <worm>


directory
---------

### flashdrive

Application Key File(s) (local)
===============================

privateness-tools.json
----------------------

### filedata
  - vendor
    - Privateness

  - type
    - application

  - for
    - privateness-tools

  - filename
    - privateness-tools.json


### files
  - node URL (service node URL where file is stored)
    - filename1
      - cipher
        - 78oqf3hfyuf;ohf9qp43hgafgre (separate cipher for each file)

      - cipher-type
        - salsa20

      - shadowname
        - generated shadowname of the file (stored localy)

      - directory
        -  

    - filename2 ...


### current-node
  - node-url


### my-nodes
  - [URL1, URL2, ....]


directory
---------

### ~/.privateness-common

User Key File (local)
=====================

<username>.local.key.json
-------------------------

### filedata
  - vendor
    - Privateness

  - type
    - key

  - for
    - user-local

  - filename
    - <username>.local.key.json


### keys
  - public
  - private
  - verify


### nonce
  - cryptographic salt


directory
---------

### ~/.privateness-common

+++
===
+++
===
___
===
Password Encrypted Key File
===========================

<username>.encrypted.keys.json OR <node-url>.encrypted.key.json OR local.encrypted.keys.json
--------------------------------------------------------------------------------------------

### filedata
  - vendor
    - Privateness

  - type
    - encrypted-keys

  - for
    - user
    - node
    - local

  - cipher
    - salsa20


### keys [...]
  - Password Encrypted Key 1 gwh8gw47gh8o
  - Password Encrypted Key 2 wo3hgw78o3hgw
  - ...


directory
---------

### flashdrive


Tasks
-----

