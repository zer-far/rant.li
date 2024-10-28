
# rant.li
Configuration files for the [rant.li](https://rant.li) WriteFreely instance.

This set up uses the [Caddy](https://caddyserver.com/) web server and [WriteFreely](https://writefreely.org/).


## Caddyfile features
The Caddyfile includes:
- Security headers.
- Caching headers.
- Web Application Firewall: [Coraza WAF](https://coraza.io/) with [OWASP Core Ruleset](https://coreruleset.org/).
- Analytics snippet: A custom HTML snippet is added on every page to connect to analytics software.

## Set up

### Prerequisites
- Ensure you have Docker installed (in rootless mode).
- Familiarity with basic command-line operations.
- Ports 80 and 443 open in your firewall.
- Enough resources to compile WriteFreely and Caddy.

### Configuration steps
1. Follow the [WriteFreely set up instructions](https://writefreely.org/start) to generate the required configuration files.
2. Edit the necessary environment variables.
3. Modify the Caddy configuration file as needed to make sure it works with your domain and requirements.
4. (Optional) To set up Tor, point it to port 8080:
   - Edit your `torrc` file to include:
     ```plaintext
     HiddenServiceDir /var/lib/tor/onion_service/
     HiddenServicePort 80 127.0.0.1:8080
     ```
   - Get the hostname from `/var/lib/tor/onion_service/hostname` and replace the `Onion-Location` header in the Caddyfile.
5. Install Docker in rootless mode: [Docker documentation](https://docs.docker.com/engine/security/rootless/).
6. Run `docker compose -f compose.yml up -d --build`.

## Notes
- Ensure your database container is backed up regularly; [restic](https://restic.net/) can be used for this.
- Adjust configuration files based on your setup requirements.
- The environment variables file is specific to Docker; additional changes will be needed in both the Caddyfile and WriteFreely configuration to align with your environment.
