# Gauge with Selenium Grid
[![Build Status](https://snap-ci.com/apoorvam/gaugeGrid/branch/master/build_image)](https://snap-ci.com/apoorvam/gaugeGrid/branch/master)

This is a sample [Gauge](http://getgauge.io/) project that uses Selenium as the driver to interact with a web browser. It uses Selenium Grid to run tests on multiple browsers.
This can also be used to run tests remotely, in different browsers, different platforms or even different versions of browsers.

## Prerequisites

This example requires the following softwares to run.
  * [Java 1.7](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) or above
  * [Gauge](http://getgauge.io/get-started/index.html)
  * Gauge Java plugin
    * can be installed using `gauge --install java`
  * Firefox(>= v46)/Chromedriver in PATH


## Setting the Selenium Grid

* Download the latest version of Selenium Server [here](http://docs.seleniumhq.org/download/). Or, you can use the selenium server jar v2.53.1 present in `resources` directory of this repository.

To set up the Hub, run
```
java -jar <path_to_selenium_server_jar> -role hub
```
This uses port 4444 by default for its web interface.

To set up a node, run
```
java -jar <path_to_selenium_server_jar> -role webdriver -hub http://localhost:4444/grid/register/ -port 5566
```
You can use the free port of choice.

To check web console, go to [http://localhost:4444/grid/console](http://localhost:4444/grid/console)

If you are running hub and nodes in different machines, `localhost` should be replaced with IP address of hub. This should also be updated in `project_dir/env/user.properties`.

## Run specs

* Clone repository and run

```
mvn test
```
This runs the sample specs using the firefox driver by default. To run tests in Chrome browser, pass the `-Dwebdriver.chrome.driver="<path_to_chrome_driver>"` flag to selenium node.
Then run specs using `mvn test -Denv="chrome"`

To run the specs in android Web view of a physical android device, follow steps as [here](http://selendroid.io/setup.html#launchingSelendroid).
Launch selendroid-standalone as below, the jar is included in `resources` directory of this repository(if needed).

```
java -jar <path_to_selenroid_standalone_jar> -host <IP_of_selenium_hub> -hub <path_to_node_register> -port <port_for_selendroid>
```

Example:

```
java -jar selendroid-standalone-0.17.0-with-dependencies.jar -host localhost -hub http://localhost:4444/grid/register -port 4445
```

Run specs

```
mvn gauge:execute -Denv=android
```






