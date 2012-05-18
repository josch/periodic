Overview
========

Count or execute a program with an overall precise interval. Counting or
execution does not "fall behind" over time. The overall frequency will stay the
same and there will be no cumulative timing error.

This script is just a convenience wrapper around the sleepenh program.

Requirements
============

POSIX shell and sleepenh

Features
========

 * interval will stay the same on average and the counter will not "fall behind"
 * count upward or downward
 * specify interval length as a floating point number of seconds including fractions of one second
 * begin to count at given integer and count for a specific number of times or until infinity
 * print nothing at all
 * execute a program at every step, optionally by forking it from the script for programs possibly running longer than the given interval

Usage
=====

Usage: periodic [ARGS] [COMMAND]

It counts upward (incrementing by 1, default) or downward (decrementing by 1,
-d) starting at integer BEGIN (-b, default: 0) with a configurable floating
point interval of SECS seconds (-n, default 1.0) until infinity (default) or up
to a maximum number of COUNT intervals (-c). It can operate silently and not
print this counter (-s). It optionally executes a COMMAND per interval which it
can also fork (-f) in case the command is expected to take longer than SECS
seconds.

  -f       fork COMMAND
  -s       silent, do not print counter
  -d       count downward (default: upward)
  -n SECS  interval of SECS in floating point (default: 1.0)
  -c COUNT only run for COUNT interval(s) (default: -1 = infinity)
  -b BEGIN start counting at BEGIN (default: 0)
  -h       print this help message

History
=======

I just wanted a program that reliably counted with a given frequency without
suffering from cumulative timing errors. I did not want to accept the small
delays that are adding up each time in a "while sleep(1)" loop. Being
instructed to count up to a million with a frequency of 1 Hz, the total
execution time should equal exactly one million seconds.

Apparently such a trivial program didnt exist, but there is the sleepenh
program which is able to sleep for just the amount of time that the execution
is done in with an overall precise interval. Therefor I built a script around
that utility.

watch(1) comes very close to what I do but it can only run in fullscreen,
doesnt go faster than 10Hz and doesnt allow the programs it executes to take
longer than its interval.
