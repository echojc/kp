## DEPRECATED

**Recommended replacement:** https://github.com/fgeller/kt

This tool was thrown together back when [kt](https://github.com/fgeller/kt) only had the ability to consume messages from a topic. kt's features have now grown to so much more that there really isn't any reason for this tool to exist. I highly recommend using kt for all your Kafka needs instead.

Cheers!

----

# kp - a Kafka tool

A straightforward CLI tool to produce data into Kafka. Intended as a counterpart
to [fgeller/kt](https://github.com/fgeller/kt).

## Installation

The only dependency is
[dpkp/kafka-python](https://github.com/dpkp/kafka-python), which you can install
using `pip`:

```
$ sudo apt-get install python-pip
$ sudo pip install kafka-python
```

With that installed, `kp` will just run.  I recommend putting `kp` somewhere on
your `PATH` to make it easily accessible.

## Usage

```
$ kp -h
usage: kp [-h] [--brokers BROKERS] [--json] topic

Produce messages to Kafka. Supports a JSON input format for complex messages.

positional arguments:
  topic              topic to produce to.

optional arguments:
  -h, --help         show this help message and exit
  --brokers BROKERS  comma separated list of brokers.
  --json             parses input as JSON expecting {"partition":<int>,"key":<key>,"message":<message>}, all optional.
```

## Examples

Produce a message to topic `my-topic` partition 0 with an empty key:

```
$ kp my-topic
this is a message
```

Produce a message with a specific partition, key, and message:

```
$ kp my-topic --json
{"partition":1,"key":"my-key","message":"this is a message"}
```

Produce a JSON formatted message and key:

```
$ kp my-topic --json
{"partition":3,"key":{"complex":"key"},"message":[42,"bits",{"of":"data"}]}
```

Bulk load messages into a topic:

```
$ cat messages | kp my-topic --json
```

