# Backup server

## Create remote backup

* Start server on rescue mode
* Copy all the disk:
```
ssh user@remote "dd if=/dev/sda1 | gzip -1 -" | dd of=image.gz status=progress 
```

Source: https://vander.host/knowledgebase/operating-systems/how-do-dd-from-one-server-to-another/ 