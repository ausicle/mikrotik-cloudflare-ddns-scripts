# mikrotik-cloudflare-ddns-scripts

This simple scripts are designed to implement `DDNS` feature using the service [Cloudflare](https://www.cloudflare.com/).

### Requirements and dependences

Scripts work only on `RouterOS` version 6.44 and above.

Depends on [Mikrotik JSON Parser](https://github.com/Winand/mikrotik-json-parser) project installed as system script with name `JParseFunctions`.

### Configure

Each script (IPv4 and IPv6) has a configuration area. Just insert your values.

First of all you need your `Cloudflare API` key. Just go to the `Cloudflare` [site](https://www.cloudflare.com/) `My Profile -> API Keys section -> Global API Key -> View`. Follow the instructions. Now you have your `API` key. Keep it safe.

The service does not allow easy retrieval of required Zone and DNS record identifiers. This is only possible through a REST API methods [List Zones](https://developers.cloudflare.com/api/operations/zones-get) and [List DNS Records](https://developers.cloudflare.com/api/operations/dns-records-for-a-zone-list-dns-records). Using any REST client (I use [Advanced REST client](https://chrome.google.com/webstore/detail/advanced-rest-client/hgmloofddffdnphfgcellkdfbfbjeloo) for `Chrome Browser`, [HTTPie](https://httpie.io/app) also works, or [curl](https://curl.se)), sending a request, you will receive the `JSON` answer with necessary Zone and DNS Record IDs.

Insert all variables in scripts and install in your `Mikrotik` device.

#### Get zone id with cURL
Replace `$api_token` with your [api token](https://dash.cloudflare.com/profile/api-tokens).
```shell
curl --request GET \
  --url https://api.cloudflare.com/client/v4/zones \
  --header "Authorization: Bearer $api_token" \
  --header "Content-Type: application/json"
```

#### Get record id with cURL
Get dns record id. Replace `$api_token` with your [api token](https://dash.cloudflare.com/profile/api-tokens). And `$zone_id` with zone id from [above](#Get-zone-id-with-cURL)
```shell
curl --request GET \
    --url https://api.cloudflare.com/client/v4/zones/$zone_id/dns_records \
    --header "Authorization: Bearer $api_token" \
    --header "Content-Type: application/json"
```
> [!TIP]
> You can use jq to prettify json output
### Running

You may add this script to system scheduler as periodically task.

#### Thanks for using.
