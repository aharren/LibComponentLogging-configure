

# LibComponentLogging-configure

[http://0xc0.de/LibComponentLogging](http://0xc0.de/LibComponentLogging)    
[http://github.com/aharren/LibComponentLogging-configure](http://github.com/aharren/LibComponentLogging-configure)


## Overview

(Auto-)configuration for [http://0xc0.de/LibComponentLogging](http://0xc0.de/LibComponentLogging).

Note: `lcl_configure` is still under construction.


## Example

Take the new LibComponentLogging CocoaPods pod specs from https://github.com/aharren/LibComponentLogging-CocoaPods-NewSpecs.

Create a `Podfile`, e.g.

    platform :ios, 7
    pod 'LibComponentLogging-Core'
    pod 'LibComponentLogging-LogFile'
    pod 'LibComponentLogging-qlog'

Then, run `pod install` which will download and install the pods:

    $ pod install
    Analyzing dependencies
    Downloading dependencies
    Installing LibComponentLogging-Core (1.3.3)
    Installing LibComponentLogging-LogFile (1.2.2)
    Installing LibComponentLogging-qlog (1.1.1)
    Generating Pods project
    Integrating client project

Then, run `lcl_configure pod` to create the `lcl_config*` files:

    $ lcl_configure pod
    Creating configuration file 'lcl_config_components.h'
    Creating configuration file 'lcl_config_logger.h'
    Creating configuration file 'lcl_config_extensions.h'
    Using LibComponentLogging-Core (core)
    Using LibComponentLogging-LogFile (LogFile logger)
    Creating configuration file 'LCLLogFileConfig.h' from template 'Pods/LibComponentLogging-LogFile/LCLLogFileConfig.template.h'
    [!] Configuration file 'LCLLogFileConfig.h' needs to be adapted before compiling your project, e.g. adapt '<UniquePrefix>'
    Using LibComponentLogging-qlog (qlog extension)

`lcl_configure` analyzes the `Pods` folder and the `Podfile.lock` file and creates the required `lcl_config*` files based on the configured pods.

Based on the `Podfile` above, the following files are created:

_lcl_config_components.h:_

    /*::lcl_configure:begin::*/
    /*::lcl_configure:end::*/

_lcl_config_logger.h:_

    /*::lcl_configure:begin::*/
    #include "LCLLogFile.h"
    /*::lcl_configure:end::*/

_lcl_config_extensions.h:_

    /*::lcl_configure:begin::*/
    #include "qlog.h"
    /*::lcl_configure:end::*/

Whenever you change the `Podfile` and that change is related to LibComponentLogging, you can run `lcl_configure pod` again and `lcl_configure` will update the `lcl_config*` files. `lcl_configure` will only touch the managed `/*::lcl_configure:begin::*/`...`/*::lcl_configure:end::*/` sections inside the `lcl_config*` files.


## Copyright and License

Copyright (c) 2014 Arne Harren <ah@0xc0.de>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
