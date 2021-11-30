This script adds X2s between ENBs via a user-friendly dialouge format.
The only input needed is the name of X2-relation(s).

Prerequisites:
The script may be started from offline amos/moshell on ENM
If it is run from moshell, ensure that ~/moshell/sitefiles/ipdatabase is up to date and includes the addresses of all the affected nodes.
Also, always ensure that variables are set correctly in your ~/.moshellrc so that login to nodes can work -based on nodenames only.

Usage:
After running the script (amos termpointtoenb_main.mos) it asks whether you have a file with the list of X2s.
a) If the answer is yes, then the expected format is displayed.
Then it asks the (path/filename)
b) If the answer is no, then a manual input dialogue opens.
The expected input format is: nodename (source-target) uppercase letters + numbers, separated by dash (e.g: 69012BB2-69014BB2).
Having the list of wanted X2s, the script logins to each affected target node automatically.
Checks the enbid, the transport config (especially internal IP-address).
Logs in to the source eNB, checks whether the wanted X2 already exists, creates it if not and then checks the op-status.
Logs in to the target enb and checks whether the termpoint has been autocreated by X2 from the source node and whether it's operational.
For autocreation of X2 on the target, X2IpAddress via S1 feature needs to be operational on the source and target enodeBs and MME needs to support it too.
Writes the reult in a table.
This loop is iterated over all relations.
If the user doesn't want to let X2 to create the termpoint on target nodes, or if X2IpAddress via S1 feature is disabled,
then the same relations need to be included on the X2-list -with inversed direction -to create the termpoints on the target too.
The script checks and displays if there's no contact to the nodes.
It checks whether LRAT is defined.

The script works on Ipsec X2s -if Direct IpSec via X2-feature is operational.

Results (example):

SOURCE-TARGET X2_LDN_source X2_operstate_source target_name X2_LDN_target X2_operstate_target
69014BB2-69013BB2: ENodeBFunction=1,EUtraNetwork=1,ExternalENodeBFunction=23430-69013,TermPointToENB=23430-69013 1 (ENABLED) ENodeBFunction=1,EUtraNetwork=1,ExternalENodeBFunction=23430-69014,TermPointToENB=23430-69014 1 (ENABLED)
69014BB2-69012BB2: ENodeBFunction=1,EUtraNetwork=1,ExternalENodeBFunction=23430-69012,TermPointToENB=23430-69012 0 (DISABLED) Warning: X2 CRE-FAIL on target!
69013BB2-69012BB2: ENodeBFunction=1,EUtraNetwork=1,ExternalENodeBFunction=23430-69012,TermPointToENB=23430-69012 1 (ENABLED) ENodeBFunction=1,EUtraNetwork=1,ExternalENodeBFunction=23430-69013,TermPointToENB=23430-69013 1 (ENABLED)
69013BB2-69011BB2: ENodeBFunction=1,EUtraNetwork=1,ExternalENodeBFunction=23430-69011,TermPointToENB=23430-69011 0 (DISABLED) Warning: X2 CRE-FAIL on target!

Structure:
The main script (termpointtoenb_main.mos) has 3-additional subs, which need to be placed to the same folder.
termpointtoenb_sourcesub
termpointtoenb_targetsub
termpointtoenb_xtworesulttargetsub
