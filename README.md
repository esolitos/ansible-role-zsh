# Ansible Role: ZSH

[![Build Status](https://travis-ci.org/esolitos/ansible-role-zsh.svg?branch=master)](https://travis-ci.org/esolitos/ansible-role-zsh)

Install and set up [ZSH](http://www.zsh.org/).  
This role can also configure `~./zshrc` file, upload functions files or download and set up a nice standalone `prompt`.

## Requirements

- RedHat family
- Debian + Ubuntu family
- Darwin (OSX) with [homebrew](http://brew.sh/) package manager installed. (test are missing)

## Role Variables

### `__users__`

Unset by default, dictionary should defined like this:

```yaml
__users__:
  [username]:
    [option]: [value]
```
**Options**

| Option                    | Type     | Comments                                                      |
|---------------------------|----------|---------------------------------------------------------------|
| zsh_default_shell         | bool     | Configure as default shell. Create `.zshrc`and `.zfunctions`. |
| zsh_prompt_install        | bool     | Install prompt ?, default value is `No`                       |
| zsh_prompt_name           | string   | Prompt name to load in `.zshrc`.                              |
| zsh_prompt_download_url   | string   | Prompt download url, e.g [mlpure](https://github.com/loliee/mlpure) |
| zsh_prompt_additional_url | string   | Prompt additional download url to put in `.zfunctions`.       |
| zsh_zfunctions_directory  | string   | Directory of files to upload on remote `.zfunctions`.         |
| zsh_zshrc_content         | text     | Lines to append in `~/.zshrc`.                                |


### Defaults

Check [defaults/main.yml](defaults/main.yml) for default values.

| Variable                          | Type     | Comments                                            |
|-----------------------------------|----------|-----------------------------------------------------|
| zsh_default_prompt_name           | string   | Default prompt_name, `pure`.                        |
| zsh_default_prompt_download_url   | string   | Prompt download url, [pure](https://github.com/sindresorhus/pure) |
| zsh_default_prompt_download_md5   | string   | md5 sum of `zsh_default_prompt_download_url`        |
| zsh_default_prompt_additional_url | string   | `pure` async lib.                                   |
| zsh_default_prompt_additional_md5 | string   | md5 sum of `zsh_default_prompt_additional_url`      |

## Example Playbook

The following playbook will ensure zsh is present for root user and will setup `dailyherold/pure-time` as prompt. This playbook will also append an alias in zshrc file.

```yaml
# ./test/playbooks/configuration.yml
- hosts: localhost
  remote_user: root
  vars:
    __users__:
      root:
        zsh_prompt_install: Yes
        zsh_prompt_name: pure-time
        zsh_prompt_download_url: https://raw.githubusercontent.com/dailyherold/pure-time/master/pure.zsh
        zsh_prompt_download_md5: /*TODO*/
        zsh_prompt_additional_url: https://raw.githubusercontent.com/dailyherold/pure-time/master/async.zsh
        zsh_prompt_additional_md5: /*TODO*/
        zfunctions_directory: ./files/zfunctions
        zshrc_content: |
          alias ls='ls -lah'

  # Run
  roles:
    - zsh
```

## Licence

MIT © [Esolitos](https://github.com/esolitos/)
Based on: [loliee/ansible-zsh](https://github.com/loliee/ansible-zsh) MIT © [Maxime Loliée](https://github.com/loliee/)
