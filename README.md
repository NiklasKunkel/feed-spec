## MakerDAO Feeds Reference Spec

* [terra_version](#terra_version)
* [terra_help](#terra_help)
* [terra_join](#terra_join)
* [terra_pack](#terra_pack)
* [terra_send](#terra_send)
* [terra_verify](#terra_verify)
* [terra_bot](#terra_bot)

***

#### terra_version

Returns the current client name, version, and operating system.

##### Parameters
none

##### Returns

`String` - "<CLIENT_NAME>/v\<VERSION>/\<OS>"

##### Example
```js
// Request
terra version

// Result
“Terra/v0.7.5/x86_64-macos”
```

***

#### terra_help

Returns a list of all client commands or in-depth information for a specific method (if provided)

##### Parameters
`String` [OPTIONAL] - name of method

##### Returns

`TEXT` - list of commands and parameters

##### Example
```js
// Request
terra help 

// Result
Usage: terra [<options>] <command> [<args>]
   or: terra <command> --help

Feedbot and tools

Bot options:

   --api-key=<key>            key needed for participating in network
   -F, --from=<address>       address used for signing
   --keystore=<dir>           local keystore directory
   -S, --password=<file>      password for non-interactive signing
   -L, --loop=<seconds>       wait time in seconds before looping

Misc options:
   --verbose                  additional verbose output

Commands:

   bot             run the price feed bot
   help            print help about terra(1) or one of its subcommands
   join            get API key to join oracle network
   pack            return hash of <price> (wei) and <timestamp> (seconds)
   send            send data to network
   verify          verify signed message

Report bugs to <https://github.com/makerdao/terra/issues>.
```

***
