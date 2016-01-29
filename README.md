# kp - a Kafka tool

A straightforward CLI tool to produce data into Kafka. Intended as a counterpart
to [fgeller/kt](https://github.com/fgeller/kt).

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

## Dependencies

This depends on bleeding edge
[dpkp/kafka-python](https://github.com/dpkp/kafka-python):

```
$ sudo apt-get install python-pip
$ git clone https://github.com/dpkp/kafka-python
$ pip install ./kafka-python
```

See http://kafka-python.readthedocs.org/en/master/install.html for further
documentation.
