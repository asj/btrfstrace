# btrfstrace
Run time tracing of btrfs internals

## ftracegraph
A wrapper script for ftrace graph functionality, making it easy and quick to use. Runs a given command and writes the function graphs trace into /tmp/ftracegraph.out.

  Usage:

      ftracegraph <function-to-graph> <depth> <filter|noop> <cmd-to-run>

  Examples:

      ftracegraph btrfs_file_write_iter 2 noop "fs_mark -d /btrfs -D 2 -N 1 -L 1 -S 1 -s 65536"
      ftracegraph btrfs_buffered_write 2 "*:mod:btrfs" "fs_mark -d /btrfs -D 2 -N 1 -L 1 -S 1 -s 65536"

  
  
## btrfstrace_write_hist
  Show write performance distribution per block size.

  Example:

     bpftrace_timespent_btrfs_write
      Attaching 2 probes...
      ^C
      @file_write_in_usecs[16384]:
      [64, 128)          11731 |@@@@@@@@@@@@@@@@                                    |
      [128, 256)         36371 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@|
      [256, 512)          5352 |@@@@@@@                                             |
      [512, 1K)           9439 |@@@@@@@@@@@@@                                       |
      [1K, 2K)            1986 |@@                                                  |
      [2K, 4K)             399 |                                                    |
      [4K, 8K)             174 |                                                    |
      [8K, 16K)             61 |                                                    |
      [16K, 32K)            15 |                                                    |
      [32K, 64K)             8 |                                                    |

## btrfstrace_write_sync_hist:
  Show sync performance distribution and write performance distribution per block size.

  Example:
 

     btrfstrace_write_sync_hist
      Attaching 4 probes...
      ^C
      @file_write_in_usecs[16384]:
      [64, 128)           2498 |@@@@@@@@@@@@@@                                      |
      [128, 256)          9081 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@|
      [256, 512)          1084 |@@@@@@                                              |
      [512, 1K)           3034 |@@@@@@@@@@@@@@@@@                                   |
      [1K, 2K)             463 |@@                                                  |
      [2K, 4K)              84 |                                                    |
      [4K, 8K)              59 |                                                    |
      [8K, 16K)             19 |                                                    |
      [16K, 32K)             5 |                                                    |
      [32K, 64K)             1 |                                                    |
      [64K, 128K)            1 |                                                    |
    
      @sync_file_in_usecs:
      [512K, 1M)             1 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@|
