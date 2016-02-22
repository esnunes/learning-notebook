---
date: 2016-02-18
title: "MongoDB: Backup and Restore"
is: Guide
categories:
  - MongoDB
---

```bash
# backup a specific database
mongodump --host 192.168.1.2 --port 27017 --db database_name --username mongodevdb --password YourSecretPwd
# the backup will generated in the current folder + dump

# restore a specific database
mongorestore --host 192.168.1.2 --port 27017 --db database_name --username mongodevdb --password YourSecretPwd --drop /backup/dump
# the --drop argument drops the database before restore - be careful
```
