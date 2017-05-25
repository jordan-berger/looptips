How to update to oref1

// First let's remove the oref0 source code and your existing loop directories

cd
rm -rf src
rm -rf myopenaps

// Next let's install dependencies again for good measure

curl -s https://raw.githubusercontent.com/openaps/docs/master/scripts/quick-packages.sh | bash -

// Then pull oref1 code and install

mkdir -p ~/src; cd ~/src && git clone -b dev git://github.com/openaps/oref0.git || (cd oref0 && git checkout dev && git pull)
cd ~/src/oref0 && npm run global-install

// Then run the setup script

cd && ~/src/oref0/bin/oref0-setup.sh

// NOTE:  Answer all the setup script questions like normal...but DO NOT say yes to actually install it.  When it spits out the "To run again with these same options, use:"...simply say No to the continue question, and instead copy and paste that line in to the terminal prompt...you're going to edit it to add word microbolus to the "enable" area of that string....and THEN press enter to run the setup script.

// Once everything gets installed and you answer yes to both of the cron questions, then we will edit your preferences.json

edit-pref

Congrats, your loop is updated to oref1.
