DaemonController
================

This is an adaptation of the DaemonController class from Max Howell. The idea is to create a simple controller,
that can wach, start and stop any daemon, just passing the launchPath of the daemon. It will execute several
optional callbacks to give feedback about the status of the daemon.

Installation
------------

Just add the FFYDaemonController header and implementation files. Then, be sure to add the FFYDaemonController.m
file to your desired target.

Usage
-----

Just include the FFYDaemonController.h file in your Class:

    include "FFYDaemonController.h";

Then, create an instance of it

    FFYDaemonController *daemonController = [[FFYDaemonController alloc]
      init];

Set the launch path for the Daemon to watch:

    daemonController.launchPath =
      @"/usr/local/Cellar/mysql/5.1.56/libexec/mysqld";

Set the initialization arguments, if any:

    daemonController.startArguments = [NSArray arrayWithObjects:
      @"--basedir=/usr/local/Cellar/mysql/5.1.56",
      @"--datadir=/usr/local/var/mysql",
      @"--log-error=/usr/local/var/mysql/localjost.local.err",
      @"--pid-file=/usr/local/var/mysql/localjost.local.pid", nil];

Finally,  there's an especial list of arguments in order to stop the daemon:

    daemonController.stopArguments = [NSArrary arrayWithObjects:
      @"stop", nil];

### Start/Stop

To start and stop the daemon just call:

    [daemonController start];
    [daemonController stop];

### Callbacks

There are several callbacks, here are described the ones used. All of them are optional.

#### Start callback

Whenever the daemon is started this notification is called. The block receives an NSNumber,
this is the PID of the started daemon.

    typedef void (^DaemonStarted)(NSNumber *);

#### Stop callback

When the daemon is stopped, this callback is called.

    typedef void (^DaemonStopped)();

#### Starting/Stopping callbacks

When the daemon is going to be started or stopped, these callbacks are called.

    typedef void (^DaemonIsStarting)();
    typedef void (^DaemonIsStopping)();

#### Failure callbacks

When the daemon failes to start or stop, these callbacks are called, passing an NSString,
that contains the reason of the failure.

    typedef void (^DaemonFailedToStart)(NSString *);
    typedef void (^DaemonFailedToStop)(NSString *);

More information
----------------

See the commented source at http://ivanvc.github.com/DaemonController

Credits
-------

Based in [DaemonController](https://github.com/mxcl/playdar.prefpane/blob/master/DaemonController.h),
by [Max Howell](http://methylblue.com/).

License
-------

Released under MIT License.

