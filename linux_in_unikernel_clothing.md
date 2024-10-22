# Unikernels

Often single process, single application libOS which combines the kernel and the application into
one thing. 

## Advantages

    - Small image size
    - Fast boot time
    - Low memory footprint
    - Better application performance

## Disadvantages

    - Software compatibility is difficult
    - Turns out there are many powerful pieces of software that rely on multiple processes
        communicating with each other 

## Motivation

Cloud workflow is generally based off of micro-services which only run one specific thing. Generally
having either a full VM or container for each server, database, caching thing etc. Having all of a
Linux kernel for this makes little sense as they are full of extra features to enable a more
generalized experience


## Types

There are two main types, ground up language based and POSIX-Like.

### Ground-up

These have the advantage of being able to start from scratch, and implement the API in such a way
that suits a more modern workflow, performance gains or suits the language of choice better.
Disadvantage of this is that there is such a weight of previously made excellent software that is
now unavailable 

### POSIX-LIKE

Means you need a rigid structure, a lot of functionality to implement in order to be POSIX
compliant, generally the kernels are not fully compatible but have enough functionality for running
most well used apps. These are often unstable and do not handle calls to FORK for example


# New approach, POSIX built from stripped back Linux

What if we take Linux and specialise it to only need specifically what we need. Massively reduces
the size, down to 4mb, try KML, sort of better, sort of worse.

