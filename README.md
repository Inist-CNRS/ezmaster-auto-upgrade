# ezmaster-auto-upgrade
[ezmaster](https://github.com/Inist-CNRS/ezmaster) app used to auto upgrade an ezmaster application/instance.

## Usage

- Add the application in your [ezmaster](https://github.com/Inist-CNRS/ezmaster) ([inistcnrs/ezmaster-auto-upgrade:1.0.0](https://hub.docker.com/r/inistcnrs/ezmaster-auto-upgrade/tags/)) then create a new instance on this application

- Then, open the configuration of the created instance in your ezmaster and insert your wanted parameters:

  ```json
  {
    "env": {
      "APPLICATION_BASENAME": "istex/istex-dl",
      "INSTANCE_BASENAME": "istex-dl",
      "CONFIG_FROM_INSTANCE": "istex-dl-2",
      "EZMASTER_BASEURL": "http://ezmaster:35267"
    },
    "crontab" : {
      "when": "* * * * *",
      "commands" : [
        "test -f /tmp/ezmaster.lock || (touch /tmp/ezmaster.lock && ezmaster-auto-upgrade-application && rm -f /tmp/ezmaster.lock)"
      ],
      "options": {
        "silent": false
      }
    }
  }
  ```

  ​
