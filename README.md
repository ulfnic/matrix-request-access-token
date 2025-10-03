# matrix-request-access-token

A curl wrapper for requesting an access token from a matrix homeserver.

```bash
# Request an access token
matrix-request-access-token --auth-url-user-pass '/path/to/auth'
```
```bash
# stdout
{"access_token":"myaccesstoken","device_id":"mydeviceid","user_id":"@myuser:myhomeserver.org"}
```
---
```bash
# Output help
matrix-request-access-token --help
```
```bash
matrix-request-access-token [ARGUEMENT...] [--] [BASE_URL]

A curl wrapper for requesting an access token from a matrix homeserver.

DEPENDENCIES
  curl

ARGUEMENT
  -u|--user USER
  --auth-url-user-pass AUTH_FILE   File containing a BASE_URL, user and password
  --auth-user-pass AUTH_FILE       File containing a user and password
  --auth-pass AUTH_FILE            File containing a password
  --dry-run                        Do everything except send the request
  --debug                          Output debugging information
  BASE_URL

AUTH_FILE
  Newline deliminated file containing values in the order specified by the ARGUEMENT.
  Lines in excess of those values are treated as comments.

ENVIRONMENT
  MATRIX__BASE_URL   Base url of the Matrix homeserver
  MATRIX__USER       Account username, not including @...

VALUE PRIORITY
   ARGUEMENT value > AUTH_FILE value > ENVIRONMENT value

EXAMPLES
  # Enter missing information interactively
  matrix-request-access-token 'https://myhomeserver.org'

  # Create an auth file
  >'/path/to/auth'
  chmod 600 -- '/path/to/auth'
  cat <<-'EOF' > '/path/to/auth'
  	https://myhomeserver.org
  	myuser
  	mypass
  EOF

  # Headless request
  matrix-request-access-token --auth-url-user-pass '/path/to/auth'

  # Headless request using a variety of inputs
  MATRIX__BASE_URL='https://matrix-client.matrix.org' \
  matrix-request-access-token -u 'myuser' --auth-pass <( printf '%s\n' 'mypass' )
```
