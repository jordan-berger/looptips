**How to update your loop**

This will preserve all BT pairing and functions.

1. Delete your exsiting cron (this helps prevent those annoying rebooting to fix radio error messages after a rebuild)

`crtontab -r`

2.  Then let's grab updated oref0 code

For Master branch users:  `cd ~/src/oref0 && git checkout master && git pull && sudo npm install -g oref0`

For Dev branch users: `cd ~/src/oref0 && git checkout dev && git pull` and then `npm run global-install`

3.  Edit your runagain file to change anything that you'd like by using either of these commands

If you have aliases installed `edit-runagain`
If you don't have aliases `cd ~/myopenaps && nano oref0-runagain.sh`

If you want to add or remove features, those are in the `enable` part of the script...

autotune is `autotune`
AMA is `meal`
autosens is `autosens`
SMB is `microbolus` (only on dev branch currently)

If you changed phones, changed NS sites, changed pumps, or such...make those changes here too.

4. Then run the runagain setup script

`bash ~/myopenaps/oref0-runagain.sh`

answer yes to all the questions

5. Once everything gets installed and you answer YES to both of the cron questions, then we will edit your preferences.json

`edit-pref`


Congrats, your loop is updated to oref1 and your runagain has saved the information for all those.
