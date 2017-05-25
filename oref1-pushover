**How to update to oref1 with pushover**

The current version of oref1 in the dev branch does not offer prompts for microbolus or pushover options.  It also doesn't save the pushover information for your runagain file.  I have edited a version of oref1 dev branch so that it offers prompts on the setup script and saves them to the runagain file.  I currently have a PR in for that...but it's not approved yet.  If you want to use my version...here's the directions:

1. First let's remove the oref0 source code and your existing loop directories

```
cd
rm -rf src
rm -rf myopenaps
```

2. Next let's install dependencies again for good measure

`curl -s https://raw.githubusercontent.com/openaps/docs/master/scripts/quick-packages.sh | bash -`

3. Then pull oref1 code and install

`mkdir -p ~/src; cd ~/src && git clone -b patch-7 git://github.com/Kdisimone/oref0.git || (cd oref0 && git checkout patch-7 && git pull)`
`cd ~/src/oref0 && npm run global-install`

4. Then run the setup script

`cd && ~/src/oref0/bin/oref0-setup.sh`

5. Once everything gets installed and you answer YES to both of the cron questions, then we will edit your preferences.json

`edit-pref`

SMBs and UAM are the last lines in your new preferences.


Congrats, your loop is updated to oref1 and your runagain has saved the information for all those.
