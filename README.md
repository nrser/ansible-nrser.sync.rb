nrser.sync.rb
=============

tiny little module (67 lines!) that lets you provide the body of two Ruby
functions, `in_sync?` and `sync`, to manage something.

first, `in_sync?` is called. if it returns `false` (or `nil`), then `sync` is
called and a change is reported.

simple real world example (OSX):

```yaml
- name: Show the ~/Library folder
  sync.rb:
    in_sync?: |
      ! `ls -aOl ~/Library`.lines[1].include? 'hidden'    
    sync: |
      `chflags nohidden ~/Library`
```

this makes it really quick and easy to sync things that are much easier to
express in a little blocks of code than ansible YAML structures.

you can also provide a `pre` argument that will get inserted before both the
`in_sync?` and `sync` function bodies. nice for doing requires and 
assigning variables and such. not super thought-out at this point but 
immediately useful. may change.

Version
-------

0.0.1

Requirements
------------

Ruby.

Role Variables
--------------

none.

Dependencies
------------

none.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers

  roles:
  - role: nrser.sync.rb
  
  tasks:
  - name: Show the ~/Library folder
    sync.rb:
      in_sync?: |
        ! `ls -aOl ~/Library`.lines[1].include? 'hidden'    
      sync: |
        `chflags nohidden ~/Library`
```

License
-------

BSD

Author Information
------------------

<https://github.com/nrser>
