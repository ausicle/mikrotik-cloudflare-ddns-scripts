# mikrotik-cloudflare-ddns-scripts

This simple scripts are designed to implement DDNS feature using the [Cloudflare API](https://developers.cloudflare.com/api).

### Requirements and dependences

Scripts work only on `RouterOS` version 6.44 and above.

Depends on [Mikrotik JSON Parser](https://github.com/Winand/mikrotik-json-parser) project installed as system script with name `JParseFunctions`.

### Configure

Each script (IPv4 and IPv6) has a configuration area. Just insert your values.

First of all you need your Cloudflare API Token. Create the [Cloudflare API Token](https://dash.cloudflare.com/profile/api-tokens), with DNS edit permission for your zone. Then grab your token, and follow the instructions. Keep the API Token safe.

You can go to your site's [cloudflare dashboard](https://dash.cloudflare.com) to retrieve zone id, on the URL it is `https://dash.cloudflare.com/$zone_id/$domain_name`, but DNS Record ID is only possible through REST API.

REST API methods [List Zones](https://developers.cloudflare.com/api/operations/zones-get) and [List DNS Records](https://developers.cloudflare.com/api/operations/dns-records-for-a-zone-list-dns-records). Using any REST client (e.g. [HTTPie](https://httpie.io/app), or [curl](https://curl.se)), sending a request, you will receive the JSON answer with necessary Zone and DNS Record IDs.

Insert all variables in scripts and install in your RouterOS device.

#### Get zone id with cURL
Replace `$api_token` with your [api token](https://dash.cloudflare.com/profile/api-tokens).
```shell
curl --request GET \
  --url https://api.cloudflare.com/client/v4/zones \
  --header "Authorization: Bearer $api_token" \
  --header "Content-Type: application/json"
```

#### Get record id with cURL
Get dns record id. Replace `$api_token` with your [api token](https://dash.cloudflare.com/profile/api-tokens). And `$zone_id` with zone id from [above](#Get-zone-id-with-cURL).
```shell
curl --request GET \
    --url https://api.cloudflare.com/client/v4/zones/$zone_id/dns_records \
    --header "Authorization: Bearer $api_token" \
    --header "Content-Type: application/json"
```
> [!TIP]
> You can use jq to prettify json output.
### Running

You may add this script to system scheduler as periodically task.

#### Thanks for using.
