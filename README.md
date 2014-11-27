# TuioTouch plugin for Qt 5

## Introduction

This is a QPA-using plugin (meaning, it uses Qt internals) that provides touch
events from TUIO-based sources (such as [TUIOPad](https://code.google.com/p/tuiopad/)).

[TUIO](http://www.tuio.org/) is a framework for providing touch events over the
network (implemented here using a UDP transport).

This repository also includes a simple [OSC](http://opensoundcontrol.org/spec-1_0)
parser. OSC is the binary format that TUIO uses for over-the-wire communication.

## Building

Make sure you have Qt available (I'd hope this is obvious, but...)

After that, it should be a case of doing `qmake`, `make`, `make install`.

## Use

Run your application with -plugin TuioTouch, e.g.

`qmlscene foo.qml -plugin TuioTouch`

Or make sure the plugin is loaded using the QT_QPA_GENERIC_PLUGINS environment
variable.

By default, you must direct TUIO packets to the IP of the machine the application
is running on, protocol UDP, port 3333. If you want to customise the port, you
may provide a port number like this:

`qmlscene foo.qml -plugin TuioTouch:udp=3333`

At present, UDP is the only supported transport mechanism.

## Advanced use

If you have the need to invert the X/Y axis, you can do so, by adding an
additional option when loading the plugin.

For example:

`qmlscene foo.qml -plugin TuioTouch:udp=4000:invertx:inverty`

Would invert the X and Y coordinates of all input coming in on port 4000.

## Further work

* Support other profiles (we implement 2Dcur, we want 2Dobj, 2Dblb?)
* Support multiple simultaneous sources, generating distinct QTouchEvents
    * We'd need to somehow not rely on FSEQ for removing touchpoints, else our
      currently minor memory exhaustion problem could become a real issue
* Support TCP transports?
* Submit for merge in 5.5 :)
