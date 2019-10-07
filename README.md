# XMC API Clients - Go - GenericNbiClient

Sends a query to the XMC API and prints the raw JSON response to stdout.

## Compiling

`go build GenericNbiClient.go`

Tested with go1.13.

## Usage

`GenericNbiClient -h`:

<pre>
This tool queries the XMC API and prints the raw reply (JSON) to stdout.

Usage: GenericNbiClient [options]

Available options:
  -host string
        XMC Hostname / IP
  -httptimeout uint
        Timeout for HTTP(S) connections (default 5)
  -insecurehttps
        Do not validate HTTPS certificates
  -password string
        Password for HTTP auth
  -query string
        GraphQL query to send to XMC (default "query { network { devices { up ip sysName } } }")
  -username string
        Username for HTTP auth (default "admin")
</pre>
