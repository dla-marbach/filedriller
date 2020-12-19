## filedriller

[![Build status](https://ci.appveyor.com/api/projects/status/vffor64yaxd2bc3q?svg=true)](https://ci.appveyor.com/project/steffenfritz/friller)
[![Go Report Card](https://goreportcard.com/badge/codeberg.org/steffenfritz/filedriller)](https://goreportcard.com/report/codeberg.org/steffenfritz/filedriller)

filedriller walks a directory tree and inspects all regular files with [siegfried](https://www.itforarchivists.com/siegfried/). Furthermore it creates UUIDv4s, hash sums (md5, sha1, sha256, sha512 or blake2b-512) and filedriller can check if the file is in the [NSRL](https://www.nist.gov/itl/ssd/software-quality-group/national-software-reference-library-nsrl).

The NSRL check expects a Redis server that serves NSRL SHA-1 hashes. You can use [my docker image](https://hub.docker.com/r/ampoffcom/nslredis)

## Status 

v1.0-BETA

For issues see the issue tab.

## Installation

1. Binary release
    
    Download the file for your platform and execute it. The executables are named friller.
    
    Optional NSRL:

        - docker pull ampoffcom/nslredis:032020

        - docker images

        - docker run -p 6379:6379 $IMAGEID        

    When you pass the -redisserv flag, friller sends a SHA-1 hash to the specified server.

2. From source

        go get codeberg.org/steffenfritz/filedriller/cmd/friller

## Usage
0. Fetch the pronom.sig file

        friller -download

1. Without Redis / NSRL

        friller -in SOMEDIRECTORY

2. With Redis / NSRL

        friller -in SOMEDIRECTORY -redisserv localhost

3. With alternate output file

        friller -in SOMEDIRECTORY -output foo.csv

## Output

The output is written to a CSV file. Schema of the file:

    Filename, SizeInByte, Registry, PUID, Name, Version, MIME, ByteMatch, IdentificationNote, HashSum, UUID, inNSRL

## Flags

Usage of ./friller:
  
  -download
  
    	Download siegfried's signature file
  
  -hash string
  
    	The hash algorithm to use: md5, sha1, sha256, sha512, blake2b-512 (default "sha256")
  
  -in string
  
    	Root directory to work on
  
  -output string
  
    	Output file (default "info.txt")
  
  -redisport string
  
    	Redis port number for a NSRL database (default "6379")
  
  -redisserv string
  
    	Redis server address for a NSRL database
