Sparkngin Config
================

Links
- [Main](https://github.com/DemandCube/Sparkngin)
- [Doc Index](https://github.com/DemandCube/Sparkngin/tree/master/docs/README.md)

Sparkngin Nginx module allows for logging Nginx activity to a zeromq server.

Configuration of this module includes:
- zeromq server properties
- output properties

Example Configuration
=====================

TODO

Directives
==========

sparkngin_zeromq_server
-----------------------

**syntax:**	`sparkngin_zeromq_server hostname[:port];`

**default:**	`no default hostname, default port is 7000`  
**context:**	`http`

Sets the network information to connect to zeromq server. Port can be left unspecified and will default to 7000.

sparkngin_buffer_size
---------------------

syntax:	    sparkngin_buffer_size size;

default:    4M
context:    http

Sets log data buffer size. Buffer will be used when no zeromz listener are available. Module will write logs to this buffer and will delete older entries when full, until a listener becomes available.

sparkngin_gzip
--------------

syntax:	    sparkngin_gzip on/off;

default:    off
context:    http

Indicates if module has to gzip logs before sending.

sparkngin_gzip_buffer_size
--------------------------

syntax:	    sparkngin_gzip_buffer_size size;

default:    1M
context:    http

Sets the size of the gzip buffer. Module will wait until sparkngin_gzip_buffer_size is reached before actually sending data.

sparkngin_format
----------------

syntax:	    sparkngin_format (json|plain) ['delimiter'];

default:    plain ' '
context:    http

Sets module outpout format:
- json will log data in json format
- plain will log data as plaintext, fields being separated by delimiter

sparkngin_root_loc
------------------

syntax:	    sparkngin_root_loc;

default:    none
context:    location

Sets Sparkngin root location.

sparkngin_log_format
--------------------

FIXME


