# pod

Fake pod implementation

The "scripts" folder contains bits and small pieces that I used trying to figure out the protocol with data from logs.

## How to build

```
go build
```

building for Raspberry Pi:
```
GOARCH=arm go build`
```

## How to run

This was tested so far only on Linux.
Before running, bring the BLE device down and stop bluetooth daemon
```
sudo hciconfig
sudo hciconfig hci0 down

sudo service bluetooth stop
sudo  systemctl  disable bluetooth
```

Before running, the executable must be granted capabilities(or run as root):
```
sudo setcap 'cap_net_raw,cap_net_admin=eip' ./pod
```
And then run

```
./pod -fresh
```

## Flags

```
$ ./pod  --help
Usage of ./pod:
  -fresh
        start fresh. not activated, empty state
  -state string
        pod state (default "state.toml")

```

When running with `-fresh`, the state will be saved, so running it twice(first with `-fresh`, then without) should work.

## How to build & run for Raspberry pi
Tested on `Raspberry Pi 3B+` running `Raspbian 10`

```
GOARCH=arm go build; 
ssh pi 'killall pod'; 
scp pod pi:~/  
ssh pi " sudo setcap 'cap_net_raw,cap_net_admin=eip' ./pod; ./pod"
```
