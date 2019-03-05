test-duplicates
===============

This role will print out a simple message, and test a passed in list of items
for duplicates, failing if there are duplicates.

This is from a Question in Redit. (https://www.reddit.com/r/ansible/comments/awuux5/lookup_specific_list_in_vars_file_and_assert_for/)

While it was originally presented as a series of tasks, I placed the decision in
a role, that would most likely be expanded ( do tasks after the assertion ). The
seperation between the role and the variables, make it more flexible and you need
to know less about the internals of the role.

Requirements
------------

None. Thought Molecule is being used for testing.

Role Variables
--------------

There are two role variables :

| Variable Name | Description |
| list | A simple list to be verified |
| msg | A message to be printed out |

Example Playbook
----------------

You would use this as follows:

```
---
- name: Converge
  hosts: all
  vars:
    my_list:
       - value1
       - value2
  roles:
    - role: test-duplicates
      msg: "Do some work if no duplicate"
      list: "{{ my_list }}"
```

Development and Testing
-------

I have been iterating on this role using Molecule ( https://molecule.readthedocs.io/en/latest/ )
but do not have any tests in place, as there is not much to test. I am also using
the Molecule container and docker to test.

```
docker run --rm -it -v "$(pwd)":/root -v /var/run/docker.sock:/var/run/docker.sock -w /root quay.io/ansible/molecule:2.19 sudo molecule test
```

Testing dependencies
---------

Docker is required for testing in its current form.

License
-------

BSD

Author Information
------------------

Alain Chiasson
