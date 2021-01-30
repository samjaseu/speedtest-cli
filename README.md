# check-speedtest

This is a fork of sivel's speedtest-cli with Icinga2 support.
Original repo found under: https://github.com/sivel/speedtest-cli


## Installation
```
cd /usr/lib/nagios/plugins
wget -O check_speedtest https://raw.githubusercontent.com/samjaseu/check-speedtest/master/check_speedtest
chmod +x check_speedtest
```


## Usage
**Only showing Icinga2 support here.**


### command line
```
$ check_speedtest --icinga2
Ping: 5.108 ms
Download: 321.87 Mbit/s
Upload: 644.90 Mbit/s
|ping=5.108ms
|download=321.87
|upload=644.90
```


### Icinga2

#### CheckCommand
```
object CheckCommand "check_speedtest" {
    command = [ PluginDir + "/check_speedtest" ]
    arguments += {
        "--icinga2" = {
            required = true
        }
        "--server" = {
            value = "$speedtest_servers$"
            repeat_key = true
        }
    }
}
```

#### Service template
```
template Service "Check Speedtest Template" {
    check_command = "check_speedtest"
    notes_url = "https://github.com/samjaseu/check-speedtest"
}
```

#### Service check output
![Speedtest service check output](speedtest-service-check-output.png)

#### Grafana speedtest graph
![Grafana speedtest graph](grafana-speedtest-graph.png)
