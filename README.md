# rant.li
Configuration files for the [rant.li](https://rant.li) WriteFreely instance.

## Set up

### Prerequisites
- Ensure you have Docker installed (in rootless mode).
- Familiarity with basic command-line operations.
- Ports 80 and 443 open in your firewall.

### Configuration Steps
1. Follow the [WriteFreely set up instructions](https://writefreely.org/start) to generate the required configuration files.
2. Edit the necessary environment variables.
3. Modify the Caddy configuration file as needed to make sure it works with your domain and requirements.
4. If you want to set up Tor, point it to port 8080 (or any port specified in the Caddy configuration):
   - Edit your `torrc` file to include:
     ```plaintext
     HiddenServiceDir /var/lib/tor/onion_service/
     HiddenServicePort 80 127.0.0.1:8080
     ```
5. Install Docker in rootless mode: https://docs.docker.com/engine/security/rootless/.
6. Run `docker compose -f compose.yml up -d --build`.
