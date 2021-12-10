# What is this?

This is a recipe that stands up a VirtualBox VM based on a Pop!_OS distribution, along with things to connect to GlobalProtect. This is built off of [ahplummer/PopOS_21.10](https://app.vagrantup.com/ahplummer/boxes/PopOS_21.10) base box. The Ansible playbook in this repo provisions things to get GlobalProtect working with OpenConnect.

This also works with MFA via Yubikey.

KUDOS to Dr_J! (John Woodward). His runbook made this possible. [Original Source](https://doctorjw.wordpress.com/2021/11/30/globalprotect-vpn-with-openconnect/)

## Limitations
* Copy/Paste does not work when starting via `vagrant up`. Once you've provisioned things, use the VirtualBox GUI to start the VM; the copy/paste works this way. 

## Requirements

* VirtualBox
* Vagrant
* Ansible

## Get it working
* Clone the repo to a clean directory; then cd into it.
* Stand up the VM in the cloned directory:
```
vagrant up
```
Note: You may get a GuestAdditions error, that dumps to the screen. This is due to VirtualBox, GuestAdditions, and an incompatibility with PopOS. You ought to be able to simply do another `vagrant up`, and provisioning will continue where it left off.

* Log into the server with VirtualBox (the GUI). Use `vagrant` as both the user and password.
* Open a terminal window on the guest.
* Execute `GATEWAY=gp.yourcompany.com ./login.sh` and follow the prompts. Note, you'll need to know the correct gateway address for this to work.
* Follow normal GUI login for SAML via GlobalProtect.

## Cleanup
* Turn it off 
```
vagrant halt
```
* Re-provision
```
vagrant provision
```
* Destroy things with fire
```
vagrant destroy
rm -rf .vagrant
```