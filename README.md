Description
===========

`certificates` is an ansible role which was built to help you with:

 * coping of certficates
 * coping of private keys
 * storing encrypted private keys

I use the role as part of my common setup.

I hope it helps!

Requirements
===========

This role requires Ansible 1.4 or higher.

Tested and supported:
* Ubuntu saucy

Optional Variables
===========

These are the turning knobs and their default values, if you like to change em, just go ahead.

```lang
# group_vars/all.yml

ssl_certificates:
    - keys/www.example.com.cert # copy from ansible project folder
    - /Users/user/.certs/keys/mail.example.com.cert # copy from absolute path
ssl_private_keys:
    - keys/www.example.com.key # copy from ansible project folder
    - /Users/user/.certs/keys/mail.example.com.key # copy from absolute path

# Or define content, so you can encrypt this var file with ansible-vault
ssl_private_key_contents:
    - name: mykey.key
      content: |
        -----BEGIN RSA PRIVATE KEY-----
        MIIJKAIBAAKCAgEA25qk2rd29s4Z6vTBs1gHznsNS9e3J/C87H5pX0zm0UJtyUfm
        +3hrX5Ag+U368OFO7XeR09iuWhae5FYe5GGFz7CRcIo29hLroXXQgh5cFfrmOdJw
        GCvASbVJhIES0Q/XifS2KNU72fTge7teCsqXo9RgNzNqGK7pgXutPQ8e9NF3NfZj
        XKJhzThde75Ih2Or36R7JKfNfq+jv9t8ulbSrlDltCXafo5+k/RdYtG8QhGKHTHW
        ...
        ...
        ...
        -----END RSA PRIVATE KEY-----  

```

Examples
===========

Like so you can include the role in your setup:

```lang
# playbook.yml

- { role: lxhunter.certficates }
```

Example with encrypted settings
===========

1. First, create a file with your private keys like ```mykeys.yml``` and enter the
settings ```ssl_private_key_contents``` variable
2. Encrypt the file using ansible-vault ```ansible-vault encrypt mykeys.yml```
3. Load the file before you use the role: ```
pre_tasks:
  - name: Load certificates
    include_vars: "certificates/mykeys.yml"
    no_log: true
roles:
  - storeman.certificates
```
4. Run your playbook, don't forget to pass the ```--ask-vault-pass``` parameter

Quote
==========

"Never, never, never give up."
- Winston Churchill

Contribute
==========

[Tutorial](http://kbroman.github.io/github_tutorial/pages/fork.html)

License and Author
==================

Author:: [Alexander Jäger](https://github.com/lxhunter)

Copyright 2014

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
