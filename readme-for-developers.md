# Developers

When i try resolve this issue, i wanna know when my s8 restarted, so i coded a widget with uebersicht, the widget call a shell script, the shell request a api coded on nodejs running on S8

## widget | uptime.coffee
```
command: "/Users/tribeiros/Projects/scripts/s8up"
refreshFrequency: 10000

render: (output) -> """
  <h1>#{output}</h1>
"""

style: """
  color: #fff
  font-family: monospace
  font-weight: 400
  left: 1400px
  top: 925px
  width: 340px
  text-align: justify

  h1
    font-size: 15px
    font-weight: 400
    opacity: 0.3
    
"""
```

## shell scropt | s8up
```
#!/bin/bash
stdout=`curl --silent http://192.168.0.6:3000`
timedigit=`echo ${stdout} | awk '{print$4}' | sed 's/,//'`
timealpha=`echo ${stdout} | awk '{print$6}' | sed 's/,//'`
json=`echo "$stdout" | sed '1d'`
battery=`echo $json | awk '{print$5}' | sed 's/,//'`
msg=`echo "S8 $timedigit $battery%"`
echo $msg
```

## nodejs api | s8api
```
const { exec } = require("child_process");
var express = require('express');
var app = express();
var os = require('os');
var ifaces = os.networkInterfaces();

Object.keys(ifaces).forEach(function (ifname) {
  var alias = 0;

  ifaces[ifname].forEach(function (iface) {
    if ('IPv4' !== iface.family || iface.internal !== false) {
      // skip over internal (i.e. 127.0.0.1) and non-ipv4 addresses
      return;
    }

    if (alias >= 1) {
      // this single interface has multiple ipv4 addresses
      console.log(ifname + ':' + alias, iface.address);
    } else {
      // this interface has only one ipv4 adress
      console.log(ifname, iface.address);
    }
    ++alias;
  });
});

app.get('/', function (req, res) {
  exec("uptime;termux-battery-status", (error, stdout, stderr) => {
    if (error) {
        console.log(`error: ${error.message}`);
        return;
    }
    if (stderr) {
        console.log(`stderr: ${stderr}`);
        return;
    }
    res.send(`stdout: ${stdout}`);
    console.log(`stdout: ${stdout}`);
  });
});

app.listen(3000, function () {
  console.log('s8up em execução');
});

```

