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
matrix-request-access-token [ARGUEMENT...] [--] [HOMESERVER]

A curl wrapper for requesting an access token from a matrix homeserver.

DEPENDENCIES
	curl

ARGUEMENT
	-u|--user USER
	-I|--device-id ID                       Optional ID of known device
	-n|--initial-device-display-name NAME   Optional display NAME for new device
	-U|--user-file USER_FILE                See: USER_FILE
	--dry-run                               Do everything except send the request
	--debug                                 Output debugging information
	-h|--help                               Print help doc
	HOMESERVER                              Homeserver base url

USER_FILE
	Path to a file containing VALUE_PAIRs as an alternative to using ARGUEMENTs, ex:
		VAR_NAME=VALUE
		
	If the path is a hyphen (-), file is stdin.

	ACCEPTED VAR_NAMEs:
		homeserver, user, password, device_id, initial_device_display_name

	- Lines not containing a VALUE_PAIR with an ACCEPTED VAR_NAME are ignored as comments.
	- Each VALUE_PAIR must be on its own line ending in a newline.
	- VAR_NAME is every character after tab/space indenting until the first equals (=).
	- VALUE is every character after the first equals (=) until the first newline (\n).
	- VAR_NAME and VALUE are read as raw text with no escaping or special rules.

ENVIRONMENT
	MATRIX__HOMESERVER                    Matrix homeserver url, ex: https://myhomeserver.org
	MATRIX__USER                          Account username, not including @...
	MATRIX__DEVICE_ID                     Optional ID of known device
	MATRIX__INITIAL_DEVICE_DISPLAY_NAME   Optional display name for new device

VALUE PRIORITY
	ARGUEMENT value > USER_FILE value > ENVIRONMENT value

EXAMPLES
	# Enter missing information interactively
	matrix-request-access-token 'https://myhomeserver.org'

	# Create a USER_FILE
	>'/path/to/myuser'
	chmod 600 -- '/path/to/myuser'
	cat <<-'EOF' > '/path/to/myuser'
		initial_device_display_name=My Device
		device_id=12345
		user=myuser
		password=m\y pa#ss
		homeserver=https://myhomeserver.org
	EOF

	# Headless request
 	matrix-request-access-token -U '/path/to/myuser'
```
