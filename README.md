# docker-jmeter

## Introduction

This is an alpine based jmeter image.

## Usage
### Install JMeter plugin
Start the container by `/bin/bash docker-jmeter-base/run.sh /bin/bash`

```bash
PluginsManagerCMD.sh install <plugin-name>
```

## To-do

- [ ] distributed testing
- [ ] startup script
- [ ] doc

## Known issues

- The host mode is not working on macOS or Windows (until 2022-03-09), which makes worker nodes unavailable when
  distributed testing. (ref: [Use host networking](https://docs.docker.com/network/host/))

## References

[](https://github.com/guitarrapc/docker-jmeter-gui)
[](https://github.com/kaarolch/kubernetes-jmeter)
[](https://jmeter.apache.org/usermanual/jmeter_distributed_testing_step_by_step.html)
[](https://jmeter-plugins.org/install/Install/)
[](https://jmeter-plugins.org/wiki/PluginsManagerAutomated/)