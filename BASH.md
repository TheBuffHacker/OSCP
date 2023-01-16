

``` bash
#!/bin/bash
#Name: pingsweeper.sh
#Description: Pingsweep the network

if [ "$1" == "" ]; then
  echo "You forgot an IP address"
  echo "Usage: ./$(basename $0) 192.168.0" 
else
  for ip in `seq 1 254`; do
    ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
  done
fi
```

