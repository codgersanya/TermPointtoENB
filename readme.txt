#*************************************#
#                                     #
#            TermPointToENB           #
#                readme               #
#                                     #
#*************************************#

termpointtoenb_main.mos adds X2-interfaces to nodes.
The script checks the existence of all relevant MOs, adds them on one side and checks the autocreation on the other-side.
The only input needed is the list of the wanted X2NR-relation(s), like:

69012BB2-69014BB2
69011BB2-69014BB2
69010BB2-69011BB2

Prerequisites:
The script may be started from offline moshell on ENM, as it logins to each node automatically -using the "monode command".
Note that since the cmd "monode" is not supported by Amos, this script doesn't run on Amos either.
Ensure that ~/moshell/sitefiles/ipdatabase is up to date and includes the addresses of all the affected nodes.
Also, always ensure that variables are set correctly in your ~/.moshellrc so that login to nodes can work -based on nodenames only.

Usage:
Upload termpointtoenb.mos together with all the subs anywhere under your ~/ on ENM!
Run termpointtoenb_main.mos from moshell!
Doesn't matter whether you are logged in to a node or you just run moshell in offline mode.
After running the script (run termpointtoenb.mos) it asks whether you have a file with the list of X2s.

	a) If the answer is yes, then the expected format is displayed.
	Then it asks the (path/filename)

	b) If the answer is no, then a manual input dialogue opens.
	The expected input format is: nodename (source-target) uppercase letters + numbers, separated by dash (e.g: 69012BB2-69014BB2).
	Having a list of nodes, you need to enter each relation line-by-line then hit "f" when finished.

The script works on Ipsec X2s (Direct IpSec via X2-feature)

Structure of the script:
termpointtoenb.mos					#The main script to run
termpointtoenb_sourcesub
termpointtoenb_targetsub
termpointtognb_xtworesulttargetsub
readme.txt

This script doesn't add ExternalEutranCellFDDs, neither they will be added by X2.
ExternalEutranCellFDDs may be added by ANR later.
If you want to add not just X2s, but ExternalEutranCellFDDs also, then check the repo: externaleutrancellfdd on: https://github.com/codgersanya/externaleutrancellfdd
Externaleutrancellfdd_main.mos adds not just X2s, but externaleutrancellfdds as well.
This script doesn't add eventual missing Eutran-frequencies, Eutran frequency relations and Eutran cell relations.
Separate scripts are available for that purpose (See: https://github.com/codgersanya/Relations).
Note that only one set of this scripts can be stored under your home -otherwise the program won't be able to find the subs and will be malfunctioning!
