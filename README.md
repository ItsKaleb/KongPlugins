# Local Setup
This project was created by following Kong's Plugin Development Guide https://docs.konghq.com/gateway/latest/plugin-development/get-started/

This project uses a docker-in-docker dev container to provide the required development environment.

To begin development, start the dev container in any appropriate IDE (eg, VSCode).

## Testing
Tests for each plugin are provided following Kong's guidelines, and use Pongo to provide a containerised testing environment. As a summary of Kong's own instructions:

1. Ensure Pongo is installed for the local environment
    ```
    curl -Ls https://get.konghq.com/pongo | bash
    pongo help
    ```
1. Initialize the test environment
    ```
    cd <plugin-name>
    pongo init
    pongo up
    pongo shell
    kms
    ```
1. Verify that the plugin you're working on is loaded
    ```
    curl -s localhost:8001 | \
    jq '.plugins.available_on_server."plugin-name"'
    ```

<br>

# Pre Canary Release Helper
## About
Provides additional functionality designed to synergise with Kong's Canary Release plugin.

Facilitates a 'canary by user' scheme that will route requests based on the end user of the request.
This is identified either by reading a specified claim from a JWT bearer token (eg, 'sub') or by integrating with Kong's OpenID Connect plugin which sets a 'credential' for the request in a similar fassion.

This plugin also allows for performing regex matching over the user identifier.
This can have the effect of controlling a specific set of users to always be routed to the canary upstream by setting the value of a header intended to match that from the Canary By Header Name https://docs.konghq.com/hub/kong-inc/canary/configuration/#config-canary_by_header_name

<br>

# Post Canary Release Helper
## About