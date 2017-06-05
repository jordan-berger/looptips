**How to update to oref1 dev branch**

1. First let's remove the oref0 source code and crontab (skip this step if you have a brand new rig and this is the first loop you're installing on it)

```
cd
rm -rf src
crontab -r
```

2. Then pull oref1 code and install

`mkdir -p ~/src; cd ~/src && git clone -b dev git://github.com/openaps/oref0.git || (cd oref0 && git checkout dev && git pull)`


`cd ~/src/oref0 && npm run global-install`

3. Then use your runagain setup script...

`bash ~/myopenaps/oref0-runagain.sh`

4. Once everything gets installed and you answer YES to both of the cron questions (it may have you reboot), then we edit your preferences.json

`edit-pref`

