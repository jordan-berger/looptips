I'm not sure the cause, but some people have noticed repeated issues with the error message:
```
Could not get subg_rfspy state or version. Have you got the right port/device and radio_type?")
mmeowlink.exceptions.CommsException: Could not get subg_rfspy state or version. Have you got the right port/device and radio_type?
```

I have not been able to get the error unless I let my lipo battery die.  I think other people have gotten it sporadically.  Well, since I don't know the underlying cause...and I have a kid who just needs a rig on autopilot as much as possible.  I'm using this on my rigs now.  Basically every 10 minutes, your rig will search to see if that "Could not get subg_rfspy stator or version" message in your pump-loop.log.  If it sees the message, it will do several commands that reset the spi_serial and start a manual tune again to get your rig back on track.  It will also write a note into a file called "reset-log.txt" into your root directory, so if you want to check how many times a day your rig may be needing this fix...it will be logged.

1. Navigate to root directory and reate a new blank script file by typing:

`cd && nano fix_comms_script.sh`

2. Copy and paste the following into the blank screen:

```
radio_errors=`tail /var/log/openaps/pump-loop.log | grep "Could not get subg_rfspy state or version"`
if [ ! -z "$radio_errors" ]
then
  logfile=~/reset-log.txt
  date >> $logfile
  echo "Radio error found" | tee -a $logfile
  wall "Fixing subg_rfspy state or version error!"
  cd ~/myopenaps && /etc/init.d/cron stop && killall -g openaps ; killall -g oref0-pump-loop ; reset_spi_serial.py && openaps mmtune && /etc/init.d/cron start | tee -a $logfile
fi
```

`Control-X` to exit`
`Y` to confirm writing the changes
`Enter` to save it with the same file name

3.  Change permissions on the script so that it is executable

`chmod +x fix_comms_script.sh`

4. Add a line to crontab to schedule the script to run every 10 minutes enter the crontab editor by entering:

`crontab -e`

(If you get a message asking you to select an editor, choose the number “1”)  

copy and paste the following line onto its own line at bottom of existing crontab lines

`*/10 * * * * /root/fix_comms_script.sh`

`Control-X` to exit`
`Y` to confirm writing the changes
`Enter` to save it with the same file name

5.  Check that your crontab changes got saved

`crontab –l`
