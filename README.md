<h1 align="center">

<img src="https://raw.githubusercontent.com/keesschollaart81/CaseOnline.Azure.WebJobs.Extensions.Mqtt/master/readme_banner.png" width=650 alt="CaseOnline.Azure.WebJobs.Extensions.Mqtt"/>
<br/>
Mqtt Bindings for Azure Functions, with .net 6 support
</h1>

<div align="center">

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/keesschollaart81/CaseOnline.Azure.WebJobs.Extensions.Mqtt/blob/master/LICENSE)
[![BCH compliance](https://bettercodehub.com/edge/badge/keesschollaart81/CaseOnline.Azure.WebJobs.Extensions.Mqtt?branch=master)](https://bettercodehub.com/)
[![Code Coverage](https://sonarcloud.io/api/project_badges/measure?project=CaseOnline.Azure.WebJobs.Extensions.Mqtt&metric=coverage)](https://sonarcloud.io/dashboard?id=CaseOnline.Azure.WebJobs.Extensions.Mqtt)
[![Maintainability](https://sonarcloud.io/api/project_badges/measure?project=CaseOnline.Azure.WebJobs.Extensions.Mqtt&metric=sqale_rating)]()
</div>

This repository contains the code for the CaseOnline.Azure.WebJobs.Extensions.Mqtt.net6 NuGet Package. 

It has been forked from original, because the original was not updated in two years.

This package enables you to:

* Trigger an Azure Function based on a MQTT Subscription
* Publish a message to a MQTT topic as a result of an Azure Function
* With .net 6 support and Azure Functions v4

Are you curious what MQTT is? Check [this page](http://mqtt.org/faq)!

## How to use

**Important note when using MQTT triggers:** This extension only works when you use AppService Plan! Do not use this with Consumption plan. If you're only using the output binding, using consumption plan is fine!

* [Getting Started](/../../wiki/Getting-started)
* [Publish via output](/../../wiki/Publish-via-output)
* [Subscribe via trigger](/../../wiki/Subscribe-via-trigger)
* [Integrate with Azure IoT Hub](/../../wiki/Azure-IoT-Hub)
* [And more in the Wiki](/../../wiki)

## Where to get

Install stable releases via Nuget with package - CaseOnline.Azure.WebJobs.Extensions.Mqtt.net6

https://www.nuget.org/packages/CaseOnline.Azure.WebJobs.Extensions.Mqtt.net6/
## Examples

This is a simple example, receicing messages for topic ```my/topic/in``` and publishing messages on topic ```testtopic/out```.

``` csharp
public static class ExampleFunctions
{
    [FunctionName(nameof(SimpleFunction))]
    public static void SimpleFunction(
        [MqttTrigger("my/topic/in")] IMqttMessage message,
        [Mqtt] out IMqttMessage outMessage,
        ILogger logger)
    {
        var body = message.GetMessage();
        var bodyString = Encoding.UTF8.GetString(body);
        logger.LogInformation($"{DateTime.Now:g} Message for topic {message.Topic}: {bodyString}");
        outMessage = new MqttMessage("testtopic/out", new byte[] { }, MqttQualityOfServiceLevel.AtLeastOnce, true);
    }
}
```

Please find all working examples in the [sample project](./src/ExampleFunctions/). 


## References

- [Original repository](https://github.com/keesschollaart81/CaseOnline.Azure.WebJobs.Extensions.Mqtt)
- [MQTTnet](https://github.com/chkr1011/MQTTnet)

## MIT License
Copyright (c) 2020 Kees Schollaart

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
