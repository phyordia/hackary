## Parallelize bash script using xargs
```bash
cpus=$( ls -d /sys/devices/system/cpu/cpu[[:digit:]]* | wc -w )
find . -name \*.pdf | xargs -d "\n" --max-procs=$cpus  pdf2ps
```

## Compress zip with password
```
zip -er [archive.zip] [folder]
```

## Check individual CPU usage

1- use htop

2- top and then press “1”


## Cron:Restart job if it dies

Add something like this to crontab:

```bash
* * * * * /restart_process.sh
```
where restart_process.sh has:

```bash
pgrep -f process_name >/dev/null || process_name
```

There’s also a unix tool call (run-one)[Ubuntu Manpage: run-one - run just one instance at a time of some command and unique set of arguments](http://manpages.ubuntu.com/manpages/bionic/man1/run-one.1.html)
that has some cool features


## Get inside Docker image
```bash
docker exec -it `docker ps  | grep kpmg-updf | awk '{print $1}'` bash`
```

## MySQL on mac
From brew:
we’ve installed your MySQL database without a root password. To secure it run:
	mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run `mysql -uroot`

To have launchd start mysql now and restart at login:
```
brew services start mysql
```
Or, if you don’t want/need a background service you can just run:
```
mysql.server start
```

## Tesseract multiple page pdf:
1. convert to TIFF

`gs -sDEVICE=tiff24nc -r200 -o sample.tiff -dUseBigTIFF sample.pdf`

2. Tesseract to hOCR

`tesseract sample.tiff sample -l eng hocr`
