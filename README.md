```bash
matrix-request-access-token [ARGUEMENT...] [--] [BASE_URL]

A curl wrapper for requesting an access token from a matrix server.

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
  Newline deliminated file containing values described in ARGUEMENT above in the
  order of their description. Lines in excess of those values are treated as comments.

ENVIRONMENT
  MATRIX__BASE_URL   Base url of the Matrix server
  MATRIX__USER       Account username, not including @...

VALUE PRIORITY
   ARGUEMENT value > AUTH_FILE value > ENVIRONMENT value

EXAMPLES
  # Enter information interactively
  matrix-request-access-token

  matrix-request-access-token --auth-user-pass /path/to/auth 'https://matrix-client.matrix.org'

  MATRIX__BASE_URL='https://matrix-client.matrix.org' \
  matrix-request-access-token -u myuser --auth-pass <( printf '%s\n' 'mypass' )
```
