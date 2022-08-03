[![PyPI license](https://img.shields.io/pypi/l/ansicolortags.svg)](https://pypi.python.org/pypi/ansicolortags/)
[![Python application](https://github.com/renaner123/siptools/actions/workflows/python-app.yml/badge.svg)](https://github.com/renaner123/siptools/actions/workflows/python-app.yml)

# SipTools

SipTools is a lightweight tool for sending a SIP message of test. You can send a message `Register` for example, or send a notify for test a `BLF` and check the response, if exists...

Clone from https://github.com/martincyoung/SIPRig and added new features for testing VoIP equipments. 

## Features

- Send any SIP message anywhere

  SIPRig allows you to send a SIP message to a destination of your choice.  Construct (or copy) your SIP message in an input file and use the `-f` command line option to specify the location.  Your input does not have to be valid SIP (discussed later).  You have complete control over the headers and content of your message.

  Use the `-d` flag to specify a destination as an IP or a FQDN.

  You can also specify the destination port, src address and port, and several other options.  SIPRig will use sensible defaults if these are not provided.  See the usage below.

- Guard against malformed SIP

  SIPRig automatically ensures your input file ends in two blank lines to guard against malformed SIP. This can be disabled using the `--no-validation` option.

- Protocol detection

  SIPRig automatically detects the protocol based on the input file.  You can override this by explicitly specifying the protcol with the `--tcp` and `--udp` options.

- SIPRig works under both python 2.7 and python 3

### New Features
  - Can edit others [options](#new-arguments) you need to send on methods sip. 
  - New files for testing on folder [examples](/examples/)

## Full Usage

```
    $ python siprig.py -h
    usage: siprig.py [-h] [-f INPUT_FILE] [-d DEST_ADDR] [-p DEST_PORT]
                     [-S SRC_IP] [-P SRC_PORT] [-q] [-v] [--tcp] [--udp]
                     [--timeout TIMEOUT] [--no-validation]

    optional arguments:
      -h, --help            show this help message and exit
      -f INPUT_FILE, --input_file INPUT_FILE
                            *Required - Input file
      -d DEST_ADDR, --dest-addr DEST_ADDR
                            *Required - Destination address. IP or FQDN.
      -p DEST_PORT, --dest-port DEST_PORT
                            Destination port. Default 5060.
      -S SRC_IP, --src-ip SRC_IP
                            Source IP address.
      -P SRC_PORT, --src-port SRC_PORT
                            Source port.
      -q, --quiet           Suppress all output.
      -v, --verbose         Show request and response in stdout.
      --tcp                 Force TCP protocol.
      --udp                 Force UDP protocol.
      --timeout TIMEOUT     Seconds to wait for a response. Default 1s.
      --no-validation       Disable input file blank line validation.
```
### New arguments

      -user                 User to send on Invite and Register
                            User for Register method
      -callid               Number for the Call-ID
       
                            Unique session identifier 
      -seq                  Identify and order transactions
      -mac                  The address MAC
      -model                The source equipment model
      -sip_from             From user on INVITE methods
      -sip_to               To user on INVITE methods
      -rtp_port             Port for connect the media.
      -a                    Define a surname for the user from
      -e, --expire          Time for expires

## Installation

```
git clone https://github.com/renaner123/Siptools.git
cd Siptools/
```

## Examples Usages

- Sending a `Register`
```shell
python3 siprig.py -f examples/register.txt -S <use your IP Address here> -d <use destination IP Address here> -p 5060 -P 55220 -v -sip_from 300 -sip_to 500 -callid 10 -user 300

```

- Sending a `Subscribe`

```shell
python3 siprig.py -f examples/subscribe.txt -S <use your IP Address here> -d <use destination IP Address here> -p 5060 -P 55220 -v -a surname -mac 123B3C1YHC12 -callid 1010 -model VOIP 

```

- Sending a `Notify`

```shell
python3 siprig.py -f examples/notify.txt -S <use your IP Address here> -d <use destination IP Address here> -p 5060 -P 55220 -v -callid 1010 --expire 1500 -user test
```

***OBs.:*** You can also use `tcpdump` or some software like Wireshark to monitor the sending and response of these messages.

## Libraries

`re` `socket` `sys` `ArgumentParser` 
