**How to update to oref1**

1. First let's remove the oref0 source code, your existing loop directories, and crontab (skip this step if you have a brand new rig and this is the first loop you're installing on it)

```
cd
rm -rf src
rm -rf myopenaps
crontab -r
```

2. Next let's install dependencies 

`curl -s https://raw.githubusercontent.com/openaps/docs/master/scripts/quick-packages.sh | bash -`

3. Then pull oref1 code (remainingCarbsFraction branch) and install

`mkdir -p ~/src; cd ~/src && git clone -b smb-bolus-snooze git://github.com/openaps/oref0.git || (cd oref0 && git checkout smb-bolus-snooze && git pull)`


`cd ~/src/oref0 && npm run global-install`

4. Then run the setup script...but **read the note below before finishing the script**


`cd && ~/src/oref0/bin/oref0-setup.sh --btmac=AA:BB:CC:DD:EE:FF`  (replacing the btmac address with your phone's BT MAC)


**NOTE:**  Answer all the setup script questions like normal...but DO NOT say yes to actually install it.  When it spits out the "To run again with these same options, use:"...simply answer NO, and instead **copy and paste that line into the terminal prompt so you can edit it**

*If you want to add SMB and UAM: you're going to edit it to add word `microbolus` to the "enable" area of that string.

For example:  Your edited script line may look like this if you have the option added:

`oref0-setup --dir=/root/myopenaps --serial=123456 --cgm=g4-upload --ns-host=https://samplesite.herokuapp.com --api-secret=TOPSECRETapi12 --tty=/dev/spidev5.1 --enable=' autosens  meal  microbolus ' --radio_locale='US' --btmac='11:AD:31:23:FR:12' 

After you add the `microbolus` to the enable line, press enter to run the script once you've edited it for the above items

5. Once everything gets installed and you answer YES to both of the cron questions (it may have you reboot), then we will edit your preferences.json

`edit-pref`

SMBs and UAM are the last lines in your new preferences.

Congrats, your loop is updated to oref1.


**NOTE**

A word of caution about using SMBs.  When the rig is actively trying to send an SMB command to the pump and it is bolusing that SMB, if you try to deliver a bolus using the pump's bolus wizard during that time (or vice versa)...you may cause the pump to have an error and it will need to restart itself and you will have to set the pump time/rewind.  Pump doesn't like getting two bolus commands at once.

A couple of ideas on this...check to see if you are actively getting SMBs before you bolus, and wait for a time right after an SMB has been given so that you don't cross-bolus (SMBs only go every 5 minutes).  OR use the easy bolus feature in your pump so that you can bolus a little quicker and lessen your likelihood of causing that pump error.
