---
layout: post
category: shell
title: "backup files"
tags: [shell,diff,date]
description: "backup"

---
{% include JB/setup %}

**File
<pre>
#! /bin/bash
cd /var/backups
backuptoday=etc.$(date +%Y%m%d)
backupyesterday=etc.$(date -d yesterday +%Y%m%d)

sudo mkdir $backuptoday
sudo cp /etc/*  $backuptoday
a=(diff $backuptoday  $backupyesterday|wc -l  )
if [ $a -eq 0 ];then
  rm -rf $backupyesterday
fi
</pre>
