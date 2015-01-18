---
layout: post
category: 
tags: []
---

## Managing virtual machines with Vagrant

1. Install vagrant (using homebrew tap)
2. Install virtual box (again using homebrew tap)
3. `vagrant init`
4. Edit the `Vagrantfile` to specify the type of server to provision, can use Bento Box machine from <https://github.com/opscode/bento>
5. Additionally instruct Vagrant to install the chef client
6. `vagrant up`
7. `vagrant ssh`
8. Node will have been added to chef server nodes

To delete the box
1. `vagrant destroy`
2. `knife node delete <NODE-NAME> -y && knife client delete <NODE-NAME> -y`
3. Alternatively the knife butcher plugin can clean up everything about the node from the chef server automatically

## Cookbooks

Cookbooks can be created and managed using `knife`.

The knife command supports a host of commands structured like the following: 
`knife <subject> <command>`

Cooksbooks can be inspected on the server using the `show` command.
* `knife cookbook show iptables 0.12.0 definitions`
* `knife cookbook show iptables 0.12.0 definitions iptables_rule.rb`

Add any dependencies for a cookbook to the metadata.rb in the cookbook's directory.


