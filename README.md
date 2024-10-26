# ABOUT

Tutorial - run a ddclient service in a docker swarm to update a cloudflare DNS record.

## DISCLAIMER

see [DISCLAIMER.md](DISCLAIMER.md)

## USAGE

### EXAMPLE

1. I am using docker in swarm mode. To create a master node, I run the following command:
    ```bash
   docker swarm init
   ```

2. I am using docker secrets for my API Key.
    - To create a key in cloudflare, go to your profile, click on API Tokens, and create a new token.
        * The token should have the following permissions:
            - Zone.Zone:Read.
            - Zone.DNS:Edit.
            - Zone.DNS:Read (might not be needed).

      Note - I found this information in the default ddclient.conf of the linuxserver/ddclient image.
    - To create a secret, run the following command:
    ```bash
    sudo apt install ddclient
    ```

3. Update your ddclient.conf file and update the docker-compose.yml volume to point to your ddclient.conf file (see
   comments in the file).

4. To run the service in your swarm, run the following command:
    ```bash
    docker stack deploy -c docker-compose.yml ddclient_ddns
    ```
    - This will create a service called `ddclient_ddns` (you can change this name) in your swarm.

## KNOWN ISSUES

1. (MINOR) Use of uninitialized value $type in string eq at /usr/bin/ddclient line ...
    - https://github.com/ddclient/ddclient/issues/643
    - Fix in place but not yet released (as of 26/10/24)

## SUPPORT

This is a personal project. I am not providing support for this project.
