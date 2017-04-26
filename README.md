# ssh-mole
SSH Agent Back Channel Tools

## Installation

This tool does not require additional Python libraries and can be run as a single executable.

## Demo

If you currently have SSH_AUTH_SOCK set as an environment variable and a typical ssh-agent listening on the UNIX domain socket you can run a few tests.

  - ```ssh-mole bash``` for a local shell
  - ```ssh-mole ssh -A username@servername``` for a remote shell

If you chose to run bash you should see that SSH_AUTH_SOCK has changed and SSH_ORIG_AUTH_SOCK has been declared.

Test this by listing or adding your ssh keys to the agent.

  - ```ssh-add -l``` to list existing keys assigned to this agent connection
  - ```ssh-add``` to add keys

The ssh-mole script can send itself to a remote host by intercepting any requests on the UNIX domain socket smaller than 4 chars.

  - ```echo sup | nc -U $SSH_AUTH_SOCK```

## The 'Chain'

Using ssh-mole on different machines throughout a series of SSH connections will eventually allow ssh-mole commands to interface with specific hosts.  For instance running ```ssh-mole copy``` once implemented could contain source file, destination file, and destination system parameters.

## Todo

  - Implement ```SSH_MOLEC_PUT``` and ```SSH_MOLEC_GET``` commands for sending files up the chain
