# Ad-Hoc commands

## examples shell

* `ansible all -i inventory.yaml -m shell -a 'uptime'`
* `ansible all -i inventory.yaml -m shell -a 'sudo apt-get -y install ansible'`

## examples RAW

* `ansible all -i inventory.yaml -m raw -a 'uptime >> test.txt'`
  anschauen mit:
  `ansible all -i inventory.yaml -m raw -a 'cat test.txt'`

## examples file

* `ansible all -i inventory.yaml -m file -a '/home/pi/test.txt state=absent'` 
  oder mit Module file
  `ansible all -i inventory.yaml -m file -a 'path=/home/pi/test.txt state=absent'`

## module copy

* `ansible server -b -m copy -a "src=/home/pi/bla_v1.txt dest="/home/pi/bla_v2.txt"`
* 

## examples package

posisble values: present, absent, latest

* `-b` give the command root rights
  `ansible all -i inventory.yaml -b -m package -a "name=ansible state=present"`
* to make shure the latest package is installed
  `ansible all -i inventory.yaml -b -m package -a "name=ansible state=latest"`

## examples apt

* make a complete distribution update
  `ansible all -i inventory.yaml -b -m apt -a "upgrade=dist"`

## service

* `ansible all -i inventory.yaml -b -m service -a "name=docker enabled=true state=started"`