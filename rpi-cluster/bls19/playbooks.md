# playbooks

## how to execute playbook

`ansible-playbook -i inventory.yaml play01.yaml`

Execute the playbook `play01.yaml` with inventory `inventory.yaml` aus.

To execute playbook with root righty add `-b`.

`ansible-playbook -b -i inventory.yaml play01.yaml`

Or you can add to playbook the line `become: true`.

Use `-v` to get more output ...

`ansible-playbook -i inventory.yaml -v play01.yaml`

## handlers

You can make some 