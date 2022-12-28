# Overview
`cluster-load` is a basic, lightweight yet usable tool for reporting compute node load status across a small (Linux) multiuser cluster. It addresses the user question "Where can I best run my jobs?" especially when a job manager is not in use. In the example below, users would look to run their jobs manually on nodes where CPULOAD is low and MEMAVAIL is large.
```
HOST           CPU_LOAD  CPU_AVAIL  CPU_AVAIL     MEM_AVAIL    SWAP_AVAIL  USERS        LOAD(1/5/15m)
node01             7.1%      92.9%   52.0 /56   158G / 502G     0B /   0B     10    4.0 /  4.0 /  4.1
node02            13.1%      86.5%   83.0 /96   482G / 503G     0B /   0B      3   12.6 /  5.5 /  2.1
node03             0.3%      98.2%   55.0 /56   390G / 502G     0B /   0B      8    0.2 /  0.1 /  0.1
node04           297.7%       0.0%      0 /96    17G / 1.0T     0B /   0B     23  285.8 /290.2 /283.3
```

# Installation
* Install the script `get_node_status` to run as a cron job and send its output to a shared, readable directory, e.g., `/home/cluster_status`. Output filenames such as  `status.$(hostname)` are suggested.
* Install the script `get_cluster_status` in a local directory such as `/usr/local/bin` for running by all users. Note that in its current form, it reads files in alphabetical order, staring with a header file, followed by a series of status.* files.
* Bootstrap: Running `get_node_status 1` on a single node will include a header line in the output. Save just the header line to a separate file, e.g. `header` in the shared directory.

# Comments
* This tool can also be used to reveal nodes with low activity but with high memory in used, suggesting the presence of idle process(es) that could prohibit large memory allocation requests by new jobs.
* Very dissimilar time stamps among the output status.* files may suggest inaccessible or even crashed nodes.
