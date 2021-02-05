---
layout: default
title:  "Postgresql backup all databases seperate files"
date:   2021-02-05 15:30:46 +0700
categories: devops
---

Situtation: We need backup all postgresql database local before moving to other computer

Solution:
- Create bash file

``` {r, engine='bash', count_lines}
#!/bin/sh
DBLIST=`/usr/local/bin/psql -U acvq -d postgres -q -t -c 'SELECT
datname from pg_database order by datname'`
for d in $DBLIST
do
     echo "db = $d";
     pg_dump -U acvq $d > ./$d.sql
done

```

---
References:
- [https://www.postgresql.org/message-id/47D64FBF.4090703@archonet.com](https://www.postgresql.org/message-id/47D64FBF.4090703@archonet.com)
