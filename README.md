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
# Please read README.txt for instructions how to configure your distributions.
# This distribution is a minimum configuration that distributes all except 100 LSK,
# and sends 1% of that amount as a donation to cc001 :)
# If you don't want to make that donation, just remove/change it and define your own distributions
# Please make sure that the spacing and intents are correct, they are important in .yml-files.

default:
    Sender:
        # Add here a host where you want to send the api commands to. I recommend to use your own node.
        # I strongly recommend to use only nodes that are pretected with SSL (https://....)
        # because your secret passphrase needs to be submitted to this node to be able to execute transactions.
        # Make sure to not put a '/' at the end of it
        # Example:
        # Host: "https://wallet.shiftnrg.nl"
        Host: "https://wallet.shiftnrg.nl"

        # Add here the address of the account from where you want to send the transactions
        # Example:
        # Address: "12312352346456L"
        Address: "2325153273098531263S"

        # Add here the PublicKey of your account
        # Example:
        # PublicKey: "234234645jfweijf9384rz76gr39ehg938th283th398gh94ghb832gb9238gbwiegb83f"
        PublicKey: "412406d5b2b4a9a0e59fdf0dc991877ac7bdaaadb37712a505e1c513aa37e2dc"

        # Add here your secret passphrase of the account you want to send the transactions from
        # The passphrase is needed to be able to send transactions
        # If you leave it empty like this: Secret: "", the script will ask you on the prompt to enter it during runtime.
        # Of course this can not be used when run by cron
        # Secret: "word1 word2 word3 word4 word5 word6 word7 word8 word9 word10 word11 word12"
        Secret: "yourword1 word2 word3 word4 word5 word6 word7 word8 word9 word10 word11 word12"

        # Add here your second passphrase if you configured it.
        # If no second passphrase is configured, remove it completely.
        # If you leave it empty like this: SecondSecret: "", the script will ask you on the prompt to enter it during runtime.
        # Of course this can not be used when run by cron
        # Example:
        # mySecondSecret: "other1 other2 other3 other4 other5 other6 other7 other8 other9 other10 other11 other12"
        SecondSecret: "yourother1 other2 other3 other4 other5 other6 other7 other8 other9 other10 other11 other12"

    Distribution:
        Style: "AllExcept"
        Amount: 0.5

    Distribution_Main:
        - type: "file_fixed"
          value: "donations_seatrips.csv"
          
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
