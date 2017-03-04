# Shift-fundsDistributor
Script to distribute funds to different accounts. The amounts are fully configurable and hierarchical groupable.
Different configurations are possible and a second passphrase is supported.

## Installation
Make sure to have installed the imported python modules time, json, requests, sy, yaml.
For example in Ubuntu this is done with 'sudo apt-get install python-requests python-yaml'. If you start the script with missing modules it will tell you which modules you have to install.
Read also the header in fundsDistributor.py. Read also README.txt and the comments in config.yml.

## Configuration
You have to modify the file config.yml to adapt it for your needs. See the instructions in README.txt. The script won't run if you don't adapt the mentioned constants.
In the beginning, the script runs in the Simulation mode. This means, no real transactions are executed.
If you are sure your configuration is correct, set the SIMULATION flag in fundsDistributor.py to 'False'.
You can add multiple configuration secions, to use different distributions from different accounts.

## Donations_seatrips.csv example
amount;address;description

1;15073035977129307459S;"Donation seatrips"
1;12559640335253367172S;"Donation communitywallet2"
1;10171121796382845819S;"Donation communitywallet3"
1;14828780214380070211S;"Donation shift donations"
1;6335202970982935269S;"Donation shiftcommunitywallet"
0.5;11523444743106892567S;"Donation for the maker cc001"

## Config.yml example for csv use
see config.yml.example
          
## example crontab for every 6 hours payment
15     */6     *     *     * cd Shift-fundsDistributor && ./fundsDistributor.py -y

## Usage
Make sure this script is executable with 'chmod +x fundsDistributor.py'
If you start the script with no parameters: './fundsDistributor.py' it uses the default config section in config.yml.
If you want to run a different config secion, you can add it as an argument with the '-c <CONFIGSECTION>.
Example: './fundsDistributor.py -c cc001'
Before executing the transactions, you need to confirm it again. If you want to suppress this request, you can add the '-y'
flag, which means that the question is answered automatically with 'yes'. This is needed if you want to run the script
non-interactively, for example with 'cron'.

## Information
The default configuration sends 1% of your distributed funds to CC001 account 11523444743106892567S. :)
If you don't want to send such a donation, of course you simpley can remove or modify it!

## Screenshot
![Screenshot](screenshot.png?raw=true "Screenshot")

If you have any question or suggestion, please contact me on lisk.chat, forum.lisk.io or www.liskdelegate.io

If you like this script, please vote for my delegate 'cc001' on test- and mainnet, Thanks!
