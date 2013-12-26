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

**FIXME: use any transport provided by zeromq library (tcp, pgm, ipc, inproc) **

**syntax:**	`sparkngin_zeromq_server hostname[:port];`

**default:**	`no default hostname, default port is 7000`  
**context:**	`http`

Sets the network information to connect to zeromq server. Port can be left unspecified and will default to 7000.

sparkngin_buffer_size
---------------------

**syntax:**	`sparkngin_buffer_size size;`

**default:**	`4M`  
**context:**	`http`

Sets log data buffer size. Buffer will be used when no zeromz listener are available. Module will write logs to this buffer and will delete older entries when full, until a listener becomes available.

sparkngin_gzip
--------------

**syntax:**	`sparkngin_gzip on/off;`

**default:**	`off`  
**context:**	`http`

Indicates if module has to gzip logs before sending.

sparkngin_gzip_buffer_size
--------------------------

**syntax:**	`sparkngin_gzip_buffer_size size;`

**default:**    `1M`  
**context:**    `http`

Sets the size of the gzip buffer. Module will wait until sparkngin_gzip_buffer_size is reached before actually sending data.

sparkngin_format
----------------

**syntax:**	`sparkngin_format (json|plain) ['delimiter'];`

**default:**    `plain ' '`  
**context:**    `http`

Sets module outpout format:
- json will log data in json format
- plain will log data as plaintext, fields being separated by delimiter

sparkngin_root_loc
------------------

**syntax:**	`sparkngin_root_loc;`

**default:**    `none`  
**context:**    `location`

Sets Sparkngin root location.

sparkngin_log_fields
--------------------

**syntax:**	`sparkngin_log_fields %field [%field%] ... [%field%];`

**default:**    `%version% %ip% %time_stamp% %level% %topic% %user-agent% %referrer% %cookie%`  
**context:**    `http`

Sets fields to be logged to zeromq server. Current list of fields is:
- version
- ip
- time_stamp
- submitted_timestamp
- level (info, warning, error, ...)
- topic
- user-agent
- referer
- cookie (whole Cookie header)
- cookie_cookiekey (e.g.: %cookie_user_id% will extract user_id value from Cookie header)
- env

ZeroMQ options
==============

sparkngin_zmq_io_threads
------------------------

**syntax:**	`sparkngin_zmq_io_threads number_of_threads;`

**default:**    `1`  
**context:**    `http`

Sets number of I/O threads. it specifies the size of the zeromq thread pool to handle I/O operations. If your application is using only the inproc transport for messaging you may set this to zero, otherwise set it to at least one.

sparkngin_zmq_max_sockets
-------------------------

**syntax:**	`sparkngin_zmq_max_sockets number_of_sockets;`

**default:**    `1`  
**context:**    `http`

Sets maximum number of sockets allowed on the context.

sparkngin_zmq_sndhwm
--------------------

**syntax:**	`sparkngin_zmq_sndhwm high_watermark;`

**default:**    `1000`  
**context:**    `http`

Sets the high water mark for outbound messages on the specified socket. The high water mark is a hard limit on the maximum number of outstanding messages zeromq shall queue in memory for any single peer that the specified socket is communicating with.

sparkngin_zmq_sndtimeo:
-----------------------

**syntax:**	`sparkngin_zmq_sndtimeo timeout_ms;`

**default:**    `-1`  
**context:**    `http`

Sets the timeout (in milliseconds) for send operation on the socket. If the value is 0, zmq_send will return immediately, with a EAGAIN error if the message cannot be sent. If the value is -1, it will block until the message is sent. For all other values, it will try to send the message for that amount of time before returning with an EAGAIN error.


