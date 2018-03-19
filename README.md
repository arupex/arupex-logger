# arupex-logger
Generic logger that operates in both a JSON format and a Easy to read Dev format but is also extendable

![Logo](http://arupex.com/img/logo.png)

[![npm version](https://badge.fury.io/js/arupex-logger.svg)](https://badge.fury.io/js/arupex-logger)
[![dependencies](https://david-dm.org/arupex/arupex-logger.svg)](http://github.com/arupex/arupex-logger)
![Build Status](https://api.travis-ci.org/arupex/arupex-logger.svg?branch=master) 
![Donate]("https://www.patreon.com/bePatron?u=5407448)
![lifetimeDownloadCount](https://img.shields.io/npm/dt/arupex-logger.svg?maxAge=25920000)

#### Description:
    This is the logging framework that npm arupex uses
    
#### Main feature
    process.NODE_ENV === 'production' || 'prod'
Uses a prod formatter which formats logs in JSON so splunk and other aggregators can read your logs easily

 - IE: 

        {
            "timestamp":"2018-03-19T21:18:54.023+00:00",
            "logger_name":"Prod Logger",
            "level":"info",
            "log_line":"    at traceRoute (/Users/daniel.irwin/git/arupex-logger/Logger.js:21:20)",
            "message":"quick test"
        }
    
Otherwise a dev formatter is used to keep your console clean, but also give you timestamps, and tracing information
    
  - IE: 
  
        19:37:21 Dev Logger info     at traceRoute  | Logger.js:21:20 quick test
    
#### LOG Factory
    
    let LoggerFactory = require('arupex-logger').LoggerFactory;
    let factory = new LoggerFactory(opts);
    let console = factory.getLogger('my-logger', overridingOpts);
    
#### Logger

    let Logger = require('arupex-logger').Logger;
    
    let console = new Logger('my-logger', opts);
    default opts = { 
       level      : 'info',
       outStream  : process.stdout,
       errStream  : process.stdError,
       messageKey : 'message',
       slicer     : DEFAULT_SLICER_FUNCTION,
       devFormat  : DEFAULT_DEV_FORMAT,
       prodFormat : DEFAULT_PROD_FORMAT
    }; // optional
    
#### Log Types:

DEBUG:    

    console.debug();//debug level log 

INFO: 

    console.log();//info level log
    console.info();//info level log
    console.pretty();//info level log that pretties json
    console.box();//info level log that boxes data

ERROR:
    
    console.error();//error level log
    
VERBOSE:
    
    console.verbose();//verbose level log

SILLY:
    
    console.silly();//silly level log

CRITICAL:

    console.critical();//critical level log

CRUCIAL:

    console.crucial();//crucial level log that ends the current process! process.exit(1)
