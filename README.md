# shodanXtract

is a command-line tool written in Go that fetches IP addresses from Shodan based on various inputs such as IP ranges, domains, and custom query strings. The tool allows users to pipe input from text files and retrieve relevant IP addresses from Shodan's search results.

## Features

- Fetch IP addresses from IP ranges
- Fetch IP addresses associated with domains
- Fetch IP addresses based on custom query strings
- Fetch IP addresses from favicon hashes with HTTP status codes.

## Install

`go install -v github.com/Vulnpire/sXtract@latest`

## Usage

The tool supports three main flags to specify the type of input:

    -ir : Fetch IP addresses from IP ranges.
    -ip : Fetch IP addresses associated with domains.
    -hs : Fetch IP addresses based on favicon hashes.
    -q : Fetch IP addresses based on custom query strings (can be used with -hs and -ir).

## Fetching IPs from IP ranges

Provide a text file with IP ranges, one per line, and use the -ir flag:

`cat ipranges.txt | sXtract -ir -q "port:(21 OR 1337 OR 10001)`

## Fetching IPs from domains

Provide a text file with domain names, one per line, and use the -ip flag:

`cat domains.txt | sXtract -ip`

## Fetching IPs from favicon hashes

Provide a text file with favicon hashes, one per line, and use the -hs flag. You can also specify an HTTP status code using the -q flag:

`cat hashes.txt | sXtract -hs -q "200 OK"`

## Fetching IPs from a CVE query strings

Provide a text file with custom query strings, one per line, and use the -q flag:

`cat queries.txt | sXtract -ip -q <input>`

## Port scan using Shodan

```
cat << EOF > wildcards.txt
> spotify.com
> EOF
```

`cat wildcards.txt | sXtract -ip | anew ips.txt && for i in $(cat ips.txt);do shodan host $i;done`

![image](https://github.com/user-attachments/assets/5e574a3f-17fd-4dc6-bbb0-8edbc71c1199)
