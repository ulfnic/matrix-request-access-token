# matrix-request-access-token

`curl` wrapper for requesting an access token from a matrix homeserver.

```bash
# Request an access token
matrix-request-access-token -u 'myuser' -P <(printf '%s' 'mypass') 'https://myhomeserver.org'
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

curl wrapper for requesting an access token from a matrix homeserver.

DEPENDENCIES
	curl

ARGUEMENT
	-u|--user USER
	-I|--device-id ID                       Optional ID of known device
	-r|--refresh-token true || false		Optional client support for refresh tokens
	-n|--initial-device-display-name NAME   Optional display NAME for new device
	-P|--password-file PASSWORD_FILE		See: PASSWORD_FILE
	-U|--user-file USER_FILE                See: USER_FILE
	--dry-run                               Do everything except send the request
	--debug                                 Output debugging information
	-h|--help                               Print help doc
	HOMESERVER                              Homeserver base url

PASSWORD_FILE
	Path to a file containing a password on the first line. Additional lines are ignored.
	If the path is a hyphen (-), path becomes stdin.

USER_FILE
	Path to a file containing VALUE_PAIRs as an alternative to using ARGUEMENTs, ex:
		VAR_NAME=VALUE
		
	If the path is a hyphen (-), path becomes stdin.

	ACCEPTED VAR_NAMEs:
		homeserver, user, password, device_id, refresh_token, initial_device_display_name

	- Lines not containing a VALUE_PAIR with an ACCEPTED VAR_NAME are ignored as comments.
	- Lines beginning with equals (=) after removing tab/space indenting are comments.
	- Each VALUE_PAIR must be on its own line ending in a newline.
	- VAR_NAME is every character after tab/space indenting until the first equals (=).
	- VALUE is every character after the first equals (=) until the first newline (\n).
	- VAR_NAME and VALUE are read as raw text with no escaping or special rules.

ENVIRONMENT
	MATRIX__HOMESERVER                    Matrix homeserver url, ex: https://myhomeserver.org
	MATRIX__USER                          Account username, not including @...
	MATRIX__DEVICE_ID                     Optional ID of known device
	MATRIX__REFRESH_TOKEN                 true || false, optional client support for refresh tokens
	MATRIX__INITIAL_DEVICE_DISPLAY_NAME   Optional display name for new device

VALUE PRIORITY
	ARGUEMENT value > PASSWORD_FILE value > USER_FILE value > ENVIRONMENT value

EXAMPLES
	# User interactive prompts to enter missing information that's required
	matrix-request-access-token

	# Headless request using ARGUEMENTs
	matrix-request-access-token -u myuser -P <(printf '%s' 'mypass') 'https://myhomeserver.org'

	# Create a USER_FILE
	>'/path/to/myuser'
	chmod 600 -- '/path/to/myuser'
	cat <<-'EOF' > '/path/to/myuser'
		homeserver=https://myhomeserver.org
		user=myuser
		password=m\y pa#ss
		device_id=12345
		refresh_token=true
		initial_device_display_name=My Device
	EOF

	# Headless request using a USER_FILE
 	matrix-request-access-token -U '/path/to/myuser'
```
