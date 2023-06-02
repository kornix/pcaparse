# pcaparse
### NAME
**pcaparse** - simple PCAP file parser.

### SYNOPSIS
**pcaparse** [ options ] [ -f ] <filename.pcap> [ -h | --help | -H ]

This tool is used in conjunction with either **tcpdump** of **wireshark**, e. g.:

Dump 1000 packets on interface eno1 and write capture to STDOUT, pipe it
to pcaparse' STDIN, sort results by destination:
```
tcpdump -i eno1 -c 1000 -w - | pcaparse -f - -d
```
Check for main sources of NTP amplification DDoS attack to *IP_ADDRESS*:
```
tcpdump -c 1000 -w - dst IP_ADDRESS and proto 17 and port 123 | pcaparse -f - -s
```
### PREREQUISITES
This tool depends on:
- Net::Pcap
- Data::Validate::IP
- NetPacket::Ethernet
- NetPacket::IP
- NetPacket::UDP
- NetPacket::TCP
- NetPacket::ICMP

### OPTIONS
**-f** <filename.pcap | ->

            PCAP file to parse (for example, you can write the file using
            tcpdump -w). If no filename was provided or this option is set
            to '-', STDIN is used. Useful for almost real time traffic
            analyse (tcpdump -w - | pcaparse).

**-q**

            Be quiet - do not print filename.pcap general information
            (quantity and size of records, parse time etc).

**-n N**

            Print top N results (default is 10);

**-N X**

            Parse X samples and exit. Program parses all available data by
            default.

**-d** [ ip [ /prefix ] ]

            Group data by destination IP address (default). Skip all
            samples, that does not match specified ip/prefix. Causes to show
            per-port statistics if single address or /32 network was
            provided.

**-s** [ ip [ /prefix ] ]

            Group data by source IP address. Skip all samples, that does not
            match specified ip/prefix. Causes to show per-port statistics if
            single address or /32 network was provided.

**-S**

            Sort by summary samples size instead of samples count.

**-v**

            Print verbose statistics for all addresses.

**-p**

            Be parser-friendly (print easy to parse output) - '-q' switch is
            employed and all values are not converted to human-readable
            format.

**--version**

            Print script version and exit.

**-h | --help**

            Print short help message and exit.

**-H**

            Print extended help message and exit.

### TODO
- Rewrite IP address matching code using pack().
- IPv6 support.

### HISTORY
**0.0.7** - added parser-friendly output;

**0.0.6** - fixed a bug with older Net::Pcap versions;
          
          - initial public release;
          
**0.0.5** - added STDIN data source support.

**0.0.4** - fixed error with run time calculation;

**0.0.3** - output code rewrite;

**0.0.2** - added per-port stats for /32 networks;

**0.0.1** - initial release;

### AUTHOR
Volodymyr Pidgornyi <vp@dtel-ix.net>
