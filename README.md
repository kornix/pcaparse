# pcaparse
### NAME
**pcaparse** - simple PCAP file parser.

### SYNOPSIS
**pcaparse** [ options ] [ -f ] <filename.pcap> [ -h | --help | -H ]

This tool is used in conjunction with **tcpdump**, **wireshark** or **sflow-tools**, see **EXAMPLES** section for explanation.
### EXAMPLES
* tcpdump -c 10 -w - proto 17 and dst port 53 | ./pcaparse -d -f -
```
Filename:                   -
File size:                  -
Parsed:                     10 samples in 28.62 seconds
Matched:                    10 samples / 761B
  tcp:                      0 samples / 0B
  udp:                      10 samples / 761B
  icmp:                     0 samples / 0B
  other:                    0 samples / 0B

                            Samples    Summary    Average
Destination                   count       size       size
8.8.8.8                          10       761B        76B
  tcp:                            0         0B         0B
  udp:                           10       761B        76B
  icmp:                           0         0B         0B
  other:                          0         0B         0B
```
* tcpdump -c 10 -w - proto 6 and dst net not 192.168.0.0/16 | ./pcaparse -d -v -f -
```
Filename:                   -
File size:                  -
Parsed:                     10 samples in 0.99 seconds
Matched:                    10 samples / 1.48kB
  tcp:                      10 samples / 1.48kB
  udp:                      0 samples / 0B
  icmp:                     0 samples / 0B
  other:                    0 samples / 0B

                            Samples    Summary    Average
Destination                   count       size       size
142.251.36.46                     5       869B       174B
  tcp:                            5       869B       174B
    443 (https)                   5       869B       174B
  udp:                            0         0B         0B
  icmp:                           0         0B         0B
  other:                          0         0B         0B
149.154.167.99                    2       315B       158B
  tcp:                            2       315B       158B
    443 (https)                   2       315B       158B
  udp:                            0         0B         0B
  icmp:                           0         0B         0B
  other:                          0         0B         0B
142.251.39.99                     2       262B       131B
  tcp:                            2       262B       131B
    443 (https)                   2       262B       131B
  udp:                            0         0B         0B
  icmp:                           0         0B         0B
  other:                          0         0B         0B
157.240.224.12                    1        66B        66B
  tcp:                            1        66B        66B
    443 (https)                   1        66B        66B
  udp:                            0         0B         0B
  icmp:                           0         0B         0B
  other:                          0         0B         0B
```
### PREREQUISITES
This tool is written in **perl** and depends on the next modules:

- Net::Pcap
- Data::Validate::IP
- NetPacket

All other dependencies seems to be standard and installed with perl interpreter by default.

### OPTIONS
**-f** <filename.pcap | ->

            PCAP file to parse (for example, you can write the file using
            tcpdump -w). If no filename was provided or this option is set
            to '-', STDIN is used. Useful for almost real time traffic
            analyse (tcpdump -w - | pcaparse);

**-q**

            Be quiet - do not print filename.pcap general information
            (quantity and size of records, parse time etc);

**-n N**

            Print top N results (default is 10);

**-N X**

            Parse X samples and exit. Program parses all available data by
            default;

**-d** [ ip [ /prefix ] ]

            Group data by destination IP address (default). Skip all
            samples, that does not match specified ip/prefix. Causes to show
            per-port statistics if single address or /32 network was
            provided;

**-s** [ ip [ /prefix ] ]

            Group data by source IP address. Skip all samples, that does not
            match specified ip/prefix. Causes to show per-port statistics if
            single address or /32 network was provided;

**-S**

            Sort by summary samples size instead of samples count;

**-v**

            Print verbose statistics for all addresses;

**-p**

            Be parser-friendly (print easy to parse output) - '-q' switch is
            employed and all values are not converted to human-readable
            format;

**--version**

            Print script version and exit;

**-h | --help**

            Print short help message and exit;

**-H**

            Print extended help message and exit.

### TODO
- Rewrite IP address matching code using pack();
- IPv6 support.

### HISTORY
**0.0.7** - added parser-friendly output;

**0.0.6** - fixed a bug with older Net::Pcap versions, initial public release;
          
**0.0.5** - added STDIN data source support.

**0.0.4** - fixed error with run time calculation;

**0.0.3** - output code rewrite;

**0.0.2** - added per-port stats for /32 networks;

**0.0.1** - initial release;

### AUTHOR
Volodymyr Pidgornyi <vp@dtel-ix.net>
