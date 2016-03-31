# Setting up Tmux for Remote Pairing

## Install Tmux
Linux: sudo apt-get update && sudo apt-get install tmux
OSX: brew update && brew install tmux

## Start a session
tmux new-session -s {sessionName}

## Basic Pairing on a Single Account
1. on your machine, bring up tmux session using a shared account
2. Have your partner log into the shared account and attach
	tmux attach-session -t {sessionName}


## Pairing using two accounts
In order to use two different accounts you need two users that are in the same group. Add both users to the same group

groupadd {groupname}
usermod -a -G {groupname} {username}
groups {username}

### Start tmux on a shared socket

tmux -S {socketName} new -s {sessionName}
chgrp {group} {socketName}
Note: {socketName} contains a path like /tmp/myFancySocket

in the second terminal
tmux -S {socketName} attach -t {sessionName}

Example:
groupadd pairing
usermod -a -G pairing User1
usermod -a -G pairing User2
tmux -S /tmp/remotepairing new -s pairingSession 		#User1
tmux -S /tmp/remotepairing attach -t pairingSession 	#User2
