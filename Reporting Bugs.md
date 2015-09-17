# Reporting Bugs or Issues with mbed OS

Please report bugs in the individual github repositories. If you're uncertain where the bug needs to be filed, please seek for help in the [mbed forums](http://forums.mbed.com/c/mbed-os).

## Writing good bug reports

* Please ensure explain the setup your running, where your power comes from in much detail as possible
* Don't hesitate to attach schematics of complicated setups
* Sending photos of your setup explaining where peripherals are attached helps us to reproduce the bugs you submit
* Please attach the output of ```yotta list``` to your bug report for identifying packages and versions
* Also attach the version of yotta itself using ```yotta version```
* We are particularly interested in your toolchain versions and the specific versions of the development boards used
* A good practice is to build a debug version of the software and attach the console output of the affected module to your bug report. Selected modules support multiple levels of verbosity that might require configuration changes to generate output on the debug console. We are happy to help you identifying the right settings.
* Try to iteratively boild down bugs to the smallest possible setup that reproduces the bug - ideally without depending on specialized hardware. It that's not possible we need to know what other software is running in the background as detailed as possible.
* We will might request a compiled firmware and the sources that allow us to reproduce the bug on one of our development boards.


