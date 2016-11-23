

Many products from Victron Energy (www.victronenergy.com) seem to
implement their "VE.Direct" protocol, which allows remote monitoring
(and some control) of those devices.  At its simplest (monitoring
only), VE.Direct is a 19200 baud ASCII stream of keyword/value pairs,
reporting various parameters (voltage, current, battery capacity, etc)
from the device.  The monitoring protocol is specified here:
    https://www.victronenergy.com/support-and-downloads/whitepapers
    (search for "VE.Direct Protocol")
with a little more information here:
    https://www.victronenergy.com/live/vedirect_protocol:faq

This script (called, imaginatively, "ve.direct") captures that stream
of data, implements a (relatively primitive) display of the important
parts, allows logging to a CSV file for later plotting, and, most
importantly for me, allows remote access by acting both as a network
server for the data and as a client that can receive the data either
directly or remotely.  There's also a facility for keeping a backup
copy of the data, in case you want to reprocess it.

The "primitive" display simply takes over your terminal window and
presents this simple display (from my BMV702 battery monitor):

    Voltage           12.358 Volts
    Current           0.259 Amps
    Power             -3.20 Watts
    Charge consumed   -17.867 Ah
    Capacity left     93.9 %
    Time left         10d 0h 00m
    Time since full   2d 6h 54m 03s
    Battery temp.     51 degF

The CSV file contains lines like this:

    # date/time, mV, mA, W, %charge (x10), time-left (sec), degrees C, alarm-reason
    2016-11-17-17:20:04, 12359, -258, -318, 939, 14400, 11, 0
    2016-11-17-17:20:06, 12358, -254, -313, 939, 14400, 11, 0
    2016-11-17-17:20:08, 12359, -260, -321, 939, 14400, 11, 0
    2016-11-17-17:20:10, 12357, -276, -341, 939, 14400, 11, 0
    2016-11-17-17:20:12, 12358, -252, -311, 939, 14400, 11, 0
    2016-11-17-17:20:14, 12358, -262, -323, 939, 14400, 11, 0

The specific contents of both of the above are trivially changed in
the code.

(Victron also has an interactive command/response protocol, described
in other papers at the above link.  This script doesn't do anything
with that.  See the "HEX Protocol" documents at the above link.)

The client/server aspects are based on ssh, so the security
implications of connecting to a remote host to get battery data are
minimal.

And, just because I enjoy it, and usually learn something new when I
push the boundaries of the language, it's all implemented in bash.

paul fox, autumn 2016
