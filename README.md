# ezmaster-automaton

[![Docker Pulls](https://img.shields.io/docker/pulls/inistcnrs/ezmaster-automaton.svg)](https://registry.hub.docker.com/u/inistcnrs/ezmaster-automaton/)

[ezmaster](https://github.com/Inist-CNRS/ezmaster) app used to auto upgrade an ezmaster application/instance just when a new version of the application is released (npm version, then git push, then dockerhub autobuild).

## Prerequisites

- [ezmaster](https://github.com/Inist-CNRS/ezmaster) >= 3.7.3

## Usage

- Add the application in your [ezmaster](https://github.com/Inist-CNRS/ezmaster) ([inistcnrs/ezmaster-automaton:1.0.0](https://hub.docker.com/r/inistcnrs/ezmaster-automaton/tags/)) then create a new instance on this application

- Then, open the configuration of the created instance in your ezmaster and insert your wanted parameters:

  ```json
  {
    "env": {
      "APPLICATION_BASENAME": "istex/istex-dl",
      "INSTANCE_BASENAME": "istex-dl",
      "CONFIG_FROM_INSTANCE": "",
      "EZMASTER_BASEURL": "http://ezmaster:35267"
    },
    "crontab" : {
      "when": "* * * * *",
      "commands" : [
        "test -f /tmp/ezmaster.lock || (touch /tmp/ezmaster.lock ; ezmaster-automaton-instance ; rm -f /tmp/ezmaster.lock)"
      ],
      "options": {
        "silent": false
      }
    }
  }
  ```

  The `"env"` parameters are explained in the [ezmaster-cli documentation](https://github.com/Inist-CNRS/ezmaster-cli#ezmaster-automaton-instance), this is the most important part of the config.

  To stop docker logging, you can set the ``crontab.options.silent`` to `true`. Having log is usefull at the begining to setup the stuff.

  You can also change ``crontab.when`` (crontabl syntax) if you do not want the  `ezmaster-automaton-instance` command to be run too often. Ex: `"5 * * * *"` will run the command each 5 minutes instead of each minutes by default. 
