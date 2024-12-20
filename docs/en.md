[简体中文](../README.md) | English  

Please help me improve this document.  

This script is used for deploying vless-xhttp proxy on Cloudflare workers.  

#### Usage
 1. Pre-requirment: have a domain managed by Cloudflare.
 1. Enable `gRPC` feature in `network` settings in Cloudflare dashboard.
 1. Create a DNS `A record` for a new sub-domain with a random IPv4 address. Enable `proxy` option.
 1. Create a worker and copy-and-paste the source code from [src/index.js](../src/index.js).
 1. Goto worker's config panel, add a routing rule to your new sub-domain. e.g. `sub.your-website.com/*`.

There are some configurations at the top of the source code.  
`UUID` need no explains  
`PROXY` (optional) reverse proxy for websites using Cloudflare CDN. Format: `example.com`  
`LOG_LEVEL` debug, info, error, none  
`TIME_ZONE` timestamp time zone of logs. e.g. Argentina is `-3`  
`DOH_QUERY_PATH` URL path for DNS over HTTP(S) feature, leave it empty means disable this feature. e.g. `/doh-query`  
`UPSTREAM_DOH` e.g. `https://dns.google/dns-query`, do not use Cloudflare DNS  


You can setup those configurations in worker's eviroment variables config panel too. Env-vars have higher priority.  

If every thing goes right, you would see a `Hello world!` when accessing `https://sub.your-website.com/`.  
Viste `https://sub.your-website.com/xhttp/?uuid=YOUR-UUID` for `client-config.json`.  

#### Notice
 * This script is slow, do not expect too much.
 * Can only deploy on Cloudflare workers. [issue #2](https://github.com/vrnobody/cfxhttp/issues/2)
 * DoH feature is no for xray-core, use DoT in `config.json` instead. e.g. `tcp://8.8.8.8:53`
 * The more people knows of this script, the sooner this script got banned.

#### Credits
[tina-hello/doh-cf-workers](https://github.com/tina-hello/doh-cf-workers/) DoH feature  
