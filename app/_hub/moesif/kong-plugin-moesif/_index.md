---
name: Moesif API Analytics
publisher: Moesif
version: 1.x.x

categories: 
  - analytics-monitoring
  - logging

type: plugin

desc: Powerful API analytics and tools to activate, understand, and monetize customers.

description: |
  This plugin logs API traffic to [Moesif API Analytics](https://www.moesif.com?language=kong-api-gateway&utm_medium=docs&utm_campaign=partners&utm_source=kong), which enables you to:

  * [Understand customer API usage](https://www.moesif.com/features/api-analytics?utm_medium=docs&utm_campaign=partners&utm_source=kong)
  * [Debug issues quickly](https://www.moesif.com/features/api-logs?utm_medium=docs&utm_campaign=partners&utm_source=kong)
  * [Monetize your APIs](https://www.moesif.com/solutions/metered-api-billing?utm_medium=docs&utm_campaign=partners&utm_source=kong)
  * [Get alerted of API issues](https://www.moesif.com/features/api-monitoring?utm_medium=docs&utm_campaign=partners&utm_source=kong)
  * [Guide customers at scale](https://www.moesif.com/features/user-behavioral-emails?utm_medium=docs&utm_campaign=partners&utm_source=kong)
  * [Protect and govern your API](https://www.moesif.com/features/api-governance-rules?utm_medium=docs&utm_campaign=partners&utm_source=kong)

  This plugin supports automatic analysis of high-volume REST, GraphQL, and other APIs without adding latency.

support_url: https://www.moesif.com/implementation/log-http-calls-from-kong-api-gateway?utm_medium=docs&utm_campaign=partners&utm_source=kong

source_code: https://github.com/Moesif/kong-plugin-moesif

license_url: https://raw.githubusercontent.com/Moesif/kong-plugin-moesif/master/LICENSE

privacy_policy_url: https://www.moesif.com/privacy?utm_medium=docs&utm_campaign=partners&utm_source=kong

terms_of_service_url: https://www.moesif.com/terms?utm_medium=docs&utm_campaign=partners&utm_source=kong

kong_version_compatibility: # required
  community_edition: # optional
    compatible:
      - 2.8.x
      - 2.7.x
      - 2.6.x
      - 2.5.x
      - 2.4.x
      - 2.3.x
      - 2.2.x
      - 2.1.x
      - 2.0.x
      - 1.5.x
      - 1.4.x
      - 1.3.x
      - 1.2.x
      - 1.1.x
      - 1.0.x
      - 0.15.x
      - 0.14.x
      - 0.13.x
      - 0.12.x
      - 0.11.x
      - 0.10.x
    #incompatible:
  enterprise_edition: # optional
    compatible:
      - 2.8.x
      - 2.7.x
      - 2.6.x
      - 2.5.x
      - 2.4.x
      - 2.3.x
      - 2.2.x
      - 2.1.x
      - 1.5.x
      - 1.3-x
      - 0.36-x
      - 0.35-x
      - 0.34-x
      - 0.33-x
      - 0.32-x
      - 0.31-x
      - 0.30-x
    #incompatible:

params:
  name: moesif
  api_id: true
  service_id: true
  consumer_id: true
  route_id: true
  protocols:
    - name: http
    - name: https
    - name: tcp
    - name: tls
    - name: tls_passthrough
    - name: udp
    - name: grpc
    - name: grpcs
  dbless_compatible: 'yes'
  dbless_explanation: The plugin is compatible with any with DB-less mode including `local`, `cluster`, and `redis`
  config:
    - name: application_id
      required: true
      default:
      value_in_examples: MY_MOESIF_APPLICATION_ID
      description: Your Moesif Application Id from your [Moesif](http://www.moesif.com) dashboard. Go to Top Right Menu -> Installation.
    - name: api_endpoint
      required: false
      default: "`https://api.moesif.net`"
      description: URL for the Moesif Collection API (Change to your secure proxy hostname if client-side encryption is used).
    - name: connect_timeout
      required: false
      default: "`1000`"
      description: Timeout in milliseconds when connecting to Moesif.
    - name: send_timeout
      required: false
      default: "`2000`"
      description: Timeout in milliseconds when sending data to Moesif.
    - name: timeout
      required: false
      default: "`1000`"
      description: (Deprecated) timeout in milliseconds when connecting/sending to Moesif.
    - name: keepalive
      required: false
      default: "`5000`"
      description: Value in milliseconds that defines for how long an idle connection will live before being closed.
    - name: api_version
      required: false
      default: "`1.0`"
      description: API Version you want to tag this request with in Moesif.
    - name: disable_capture_request_body
      required: false
      default: "`false`"
      description: Disable logging of request body.
    - name: disable_capture_response_body
      required: false
      default: "`false`"
      description: Disable logging of response body.
    - name: request_header_masks
      required: false
      default: "`{}`"
      description: An array of request header fields to mask.
    - name: request_query_masks
      required: false
      default: "`{}`"
      description: An array of query string parameter fields to mask.
    - name: request_body_masks
      required: false
      default: "`{}`"
      description: An array of request body fields to mask.
    - name: response_header_masks
      required: false
      default: "`{}`"
      description: An array of response header fields to mask.
    - name: response_body_masks
      required: false
      default: "`{}`"
      description: An array of response body fields to mask.
    - name: batch_size
      required: false
      default: "`200`"
      description: Maximum batch size when sending to Moesif.
    - name: user_id_header
      required: false
      default: "`X-Consumer-Custom-Id`"
      description: Request or response header used to identify the User in Moesif.
    - name: company_id_header
      required: false
      default: ""
      description: Request or response header used to identify the Company (Account) in Moesif.
    - name: authorization_header_name
      required: false
      default: "`authorization`"
      description: Request header containing a Bearer or basic token to extract user id. See identifying users. Also, supports a comma-separated string. The plugin will check headers in order "X-Api-Key, Authorization".
    - name: authorization_user_id_field
      required: false
      default: "`sub`"
      description: Field name in JWT/OpenId token’s payload for identifying users. Only applicable if authorization_header_name is set and is a Bearer token.   
    - name: event_queue_size
      required: false
      default: "`5000`"
      description: Maximum number of events to hold in the queue before sending to Moesif. In case of network issues where the plugin is unable to connect or send an event to Moesif, skips adding new events to the queue to prevent memory overflow.
    - name: disable_gzip_payload_decompression
      required: false
      default: "`false`"
      description: If set to `true`, disables decompressing body in Kong.
    - name: max_callback_time_spent
      required: false
      default: "`2000`"
      description: Limits the amount of time in milliseconds to send events to Moesif per worker cycle.
    - name: request_max_body_size_limit
      required: false
      default: "`100000`"
      description: Maximum request body size in bytes to log in Moesif.
    - name: response_max_body_size_limit
      required: false
      default: "`100000`"
      description: Maximum response body size in bytes to log in Moesif.
    - name: debug
      required: false
      default: false
      description: An option if set to true, prints internal log messages for debugging integration issues.
  extra:
    # This is for additional remarks about your configuration.
###############################################################################
# END YAML DATA
# Beneath the next --- use Markdown (redcarpet flavor) and HTML formatting only.
#
# The remainder of this file is for free-form description, instruction, and
# reference matter.
# Your headers must be Level 3 or 4 (parsing to h3 or h4 tags in HTML).
# This is represented by ### or #### notation preceding the header text.
###############################################################################
# BEGIN MARKDOWN CONTENT
---

### How it works

When enabled, this plugin captures API traffic and logs it to
[Moesif API Analytics](https://www.moesif.com/?language=kong-api-gateway&utm_medium=docs&utm_campaign=partners&utm_source=kong). 
This plugin logs to Moesif with an [asynchronous design](https://www.moesif.com/enterprise/api-analytics-infrastructure?language=kong-api-gateway&utm_medium=docs&utm_campaign=partners&utm_source=kong) and doesn't add any latency to your API calls.

[Package on Luarocks](http://luarocks.org/modules/moesif/kong-plugin-moesif)

Moesif natively supports REST, GraphQL, Web3, SOAP, JSON-RPC, and more.

## How to install

> If you are using Kong's [Kubernetes Ingress Controller](https://github.com/Kong/kubernetes-ingress-controller), the installation is slightly different. Review the [docs for Kubernetes Ingress](https://www.moesif.com/docs/server-integration/kong-ingress-controller/).

The `.rock` file is a self-contained package that can be installed locally or from a remote server.

If the LuaRocks utility is installed in your system (this is likely the case if you used one of the official installation packages), you can install the 'rock' in your LuaRocks tree (a directory in which LuaRocks installs Lua modules).

### Install the Moesif plugin

```shell
luarocks install --server=http://luarocks.org/manifests/moesif kong-plugin-moesif
```

### Update your loaded plugins list
In your `kong.conf`, append `moesif` to the `plugins` field (or `custom_plugins` if old version of Kong). Make sure the field is not commented out.

```yaml
plugins = bundled,moesif         # Comma-separated list of plugins this node
                                 # should load. By default, only plugins
                                 # bundled in official distributions are
                                 # loaded via the `bundled` keyword.
```

If you don't have a `kong.conf`, create one from the default using the following command: 
`cp /etc/kong/kong.conf.default /etc/kong/kong.conf`

### Restart Kong

After LuaRocks is installed, restart Kong before enabling the plugin

```shell
kong restart
```

### Enable the Moesif plugin

```shell
curl -i -X POST --url http://localhost:8001/plugins/ --data "name=moesif" --data "config.application_id=YOUR_APPLICATION_ID";
```

### Restart Kong again

If you don't see any logs in Moesif, you may need to restart Kong again. 

```shell
kong restart
```