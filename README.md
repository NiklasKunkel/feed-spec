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

`String` - <CLIENT_NAME>/v\<VERSION>/\<OS>

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

#### terra_join

Returns an API key to join the oracle network

##### Parameters
`String` ETH_ADDRESS - address of oracle to join    
`String` ETH_PASSWORD - absolute path to ethereum passphrase file associated with ETH_ADDRESS    

##### Implementation
```bash
Get Timestamp   
now=$(date +%s)
hash=$(seth keccak "$now")

Create Signature    
sig = $(ethsign msg --from "$ETH_ADDRESS --data "$hash" --passphrase-file "$ETH_PASSWORD")
key=$(curl -sS -d "address=$ETH_ADDRESS&now=$now&sig=$sig" -X POST "https://dai-service.makerdao.com/token")

echo $key
```
##### Returns

Success   
`String` - <API_KEY>

Failure    
`String` - "Something went wrong. Could not get API key."


##### Example
```bash
// Request
terra join 0xEA674fdDe714fd979de3EdF0F56AA9716B898ec8 /path/to/passphrase/file

// Result
$key

```

***

#### terra_pack

Returns keccak-256 hash of price (wei) and timestamp (seconds)

##### Parameters
`String` PRICE - price of the asset denominated in wei   
`String` TIMESTAMP - timestamp denominated in seconds

##### Returns

`String` - <SHA3_HASH>

##### Example
```bash
// Request
terra pack 1200000000000000000 1528410938

// Result
e070a03f47773b961c60f5370e53dcad9e74ab57b6a90dac2adc50fed4613e0d
```

***

#### terra_send

Sends data to the oracle network

##### Parameters
`String` APIKEY - API key returned by `join`   
`String` ADDRESS - ethereum address of oracle    
`String` SIG -     
`String` PRICE - price of the asset denominated in wei     
`String` TIMESTAMP - timestamp denominated in seconds    
`String` PAIR - token pair corresponding to price data    

##### Returns

`String` - "Sent!"

##### Example
```bash
// Request
terra send 1200000000000000000 1528410938

// Result
Sent!
```

***

#### terra_verify

***

#### terra_bot
