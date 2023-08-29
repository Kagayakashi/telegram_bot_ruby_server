# BOTServer 
[Telegram](http://Telegram.org) Bot API Webhooks Framework, for Rubyists.<br>
_BOTServer_ configures, tests and deploys bots, running a fast rack server for webhooks routing.

![](https://github.com/solyaris/BOTServer/blob/master/wiki/BOTServer.png)

## Architecture:

* [Telegram Bot Architecture(s)](https://github.com/solyaris/BOTServer/blob/master/wiki/architectures.md)
```
  TELEGRAM Bot API Server                         
 --------------------------------------------------------------------
   v v v                                                       ^ ^ ^
   | | |                                                       | | |
   | | |    SSL/HTTPS                                          | | | 
   | | |    front-end       BOTServer                          | | |
   | | |    +-------+       Rack router                        | | |
   | | |    |       |       +------+                           | | |
   | | |    |       |       |      |     +-------+ HTTPS send  | | |
   | | |    |       |       |      |---->| App 1 |-------------+ | |
   | | |    |       | HTTP  |      |     +-------+               | |
   | | |    |       | POST  |      |                             | |
   | | +--->|       |------>|      |     +-------+ HTTPS send    | |
   | +----->|       |------>|      |---->| App 2 |---------------+ |
   +------->|       |------>|      |     +-------+                 |
   webhooks |       |       |      |                               |
 HTTPS POST |       |       |      |     +-------+  HTTPS send     |
            |       |       |      |---->| App   |-----------------+
            |       |       | Thin |     +-------+
            | NGINX |       +------+
            +-------+       
```

### [Instructions in 7 steps](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md)

_BOTServer_ is a devops utility to: 

* set-up and test tokens/webhooks
* generate a template app for each bot
* run a webhooks router/server. 

Here assembly instruction steps: 

1. [Installation (web/proxy server, Ruby project code)](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md#step-1-installation)
2. [Get Telegram Bot token(s)](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md#step-2-get-your-telegram-bot-tokens)
3. [Update configuration files](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md#step-3-set-up-configuration-files)
4. [Create (self-signed) Certificate](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md#step-4-create-self-signed-certificate)
5. [Configure "Webhooks mode" for each token](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md#step-5-set-webhooks)
6. [Generate template for each bot](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md#step-6-generate-template-for-each-of-your-application-bots)
7. [Deploy and run _BOTServer](https://github.com/solyaris/BOTServer/blob/master/wiki/usage.md#step-7-deploy-and-run)
 

```
$ rake
rake app:new[token]        # Create bot app template for given token
rake certificate:new       # Create SSL certificate
rake certificate:show      # Show public certificate
rake proxy:config:new      # Generate nginx proxy SSL configuration from server.yml data
rake proxy:restart         # Restart proxy server
rake proxy:start           # Start proxy server
rake proxy:stop            # Stop proxy server
rake server:config:show    # Show server configuration: /home/solyaris/BOTServer/config/server.yml
rake server:config:test    # Check server configuration: /home/solyaris/BOTServer/config/server.yml
rake server:log            # Tail -f rack sever logfile: /home/solyaris/BOTServer/log/thin.log
rake server:pid            # Show rack server pid
rake server:restart        # Restart rack server
rake server:start          # Start rack server
rake server:stop           # Stop rack server
rake tokens:show           # Show tokens configuration file: /home/solyaris/BOTServer/config/tokens.yml
rake tokens:test           # Verify if tokens are valid, online querying Telegram Server
rake webhook:reset[token]  # Reset webhook for a given token
rake webhook:set[token]    # Set webhook for a given token
```

## [License](http://www.opensource.org/licenses/mit-license)

## Credits/Contributing/Contact
* [Telegram BOT webhook rake server](https://github.com/solyaris/BOTServer)
* [Telegram BOT wrapper] (https://github.com/atipugin/telegram-bot-ruby)
