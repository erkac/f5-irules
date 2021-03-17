# HSL Notes

## HSL Config

```
ltm pool pool-hsl-logging {
    members {
        syslog-server-01:514 {
            address 10.10.10.100
            session monitor-enabled
            state down
        }
        syslog-server-02:514 {
            address 10.10.10.200
            session monitor-enabled
            state down
        }
    }
    monitor gateway_icmp 
}
 
sys log-config destination remote-high-speed-log dest-hsl-logging {
    pool-name pool-hsl-logging
    protocol udp
}
 
sys log-config destination remote-syslog dest-syslog {
    format rfc5424
    remote-high-speed-log dest-hsl-logging
}
 
sys log-config publisher publisher-remote-syslog {
    destinations {
        dest-syslog { }
    }
}
```

