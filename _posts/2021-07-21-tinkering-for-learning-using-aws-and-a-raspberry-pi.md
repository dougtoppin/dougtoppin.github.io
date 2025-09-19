---
title: "Tinkering for Learning using AWS and a Raspberry Pi"
date: 2021-07-21
---

I have always found tinkering to be the best way to learn about software. It is also a very good means of determining interest in the subject. While following tutorials can be beneficial, experimenting and learning by trial and error can provide a deeper learning experience because tutorials always work and do not necessarily teach debug and problem solving techniques.

A modern way to tinker for learning and just plain fun is to use a Raspberry Pi in conjunction with AWS. The Raspberry Pi is a very cheap device that has built-in capabilities and a large range of low cost add-ons to provide a variety of uses.

To start with, install the AWS Systems Manager (SSM) Agent on your device and then do things like use RunCommand to execute shell commands and scripts on your device.

Notice the differences between EC2 instances and your device. This will help with learning how to manage a hybrid configuration for your AWS account where you are including your own devices in addition to AWS compute resources. For example, the Raspberry Pi will appear in the SSM Fleet Manager console as opposed to the EC2 console.

While some SSM services such as RunCommand executions can be performed on a Raspberry Pi, to open an SSM Session to it the Systems Manager advanced-instances tier, which has a cost, must be enabled for your account.

Since SSM Command documents can include Python, create a Command document and do something like get and report the cpu temperature on a Raspberry Pi. The script could be installed on your device and then run but by including it in the Command document it should work as is without having to install and manage it on your device.

The following is a simple example of a Command document that will run a Python script on the Pi and output the cpu temperature in both Celsius and Fahrenheit. In it note some of the nuances such as how to format and include the Python script lines and dealing with double quotes where they are needed. There are probably better or more efficient ways to implement this but it is for learning and a reasonable example to work through.

```yaml
---
schemaVersion: "2.2"
description: "Command Document to get cpu temperature"
mainSteps:
- action: "aws:runShellScript"
  name: "pythonTemperature"
  precondition:
    StringEquals:
    - platformType
    - Linux
  inputs:
    runCommand:
    - "#!/usr/bin/python3"
    - "import os"
    - "from gpiozero import CPUTemperature"
    -
    - "# cursory check to avoid execution on unexpected instances"
    - "result=os.uname()"
    - "if result.machine != 'armv7l':"
    - "    print('not raspberrypi')"
    - "    exit(1)"
    -
    - "# get cpu temperature (in Celsius)"
    - "cpu = CPUTemperature()"
    - "temperatureC = cpu.temperature"
    -
    - "# get Fahrenheit value"
    - "temperatureF = (temperatureC * 1.8) + 32"
    -
    - "# round to a single decimal place"
    - "temperatureCr = \"{:.1f}\".format(temperatureC)"
    - "temperatureFr = \"{:.1f}\".format(temperatureF)"
    -
    - "# report both values"
    - "print(\"temperature=\", temperatureCr, \"C\", temperatureFr, \"F\")"
    -
    - "exit(0)"
```

SSM Command executions can be initiated using a specific instance in the Fleet Manager or specifying a tag can be used to have commands be sent only to the Raspberry Pis in your “home fleet”. This will begin to give some practical experience in how to manage compute resources. Note that using the Command document platformType pre-condition does not include support for Raspberry Pi instances specifically which means a check should be performed within the script itself to prevent accidental execution and the resulting errors that might occur on another platform type.

This exercise is a good way to experience a variety of things including a bit of Python, Raspberry Pi, and AWS SSM.

Links:

- [Manage Raspberry Pi devices using AWS Systems Manager](https://aws.amazon.com/blogs/mt/manage-raspberry-pi-devices-using-aws-systems-manager/)
- [Document schemas and features](https://docs.aws.amazon.com/systems-manager/latest/userguide/document-schemas-features.html)
- [Systems Manager managed instances (advanced tier)](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-managedinstances-advanced.html)
