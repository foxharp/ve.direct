

Many products from Victron Energy (www.victronenergy.com) seem to
implement their VE.Direct protocol, which allows remote monitoring
(and some control) of the devices.  At it's simplest (monitoring
only), it's a 19200 baud stream of keyword/value pairs, reporting
various parameters (voltage, current, battery capacity, etc) from
their devices.  The monitoring protocol is specified here:
    https://www.victronenergy.com/support-and-downloads/whitepapers
    (search for "VE.Direct Protocol")
with a little more information here:
    https://www.victronenergy.com/live/vedirect_protocol:faq

This script (called, imaginatively, "ve.direct") captures that stream
of data, implements a (relatively primitive) display of the important
parts, allows logging to a CSV file for later plotting, and, most
importantly for me, allows remote access by acting both as a network
server for the data and as a client that can receive the data either
directly or remotely.

(Victron also has an interactive command/response protocol, described
in other papers at the above link.  This script doesn't do anything
with that.  See the "HEX Protocol" documents at the above link.)

And, just because I enjoy it, and usually learn something new when I
push the boundaries of the language, it's all implemented in bash.

paul fox, autumn 2016
