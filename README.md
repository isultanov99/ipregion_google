# IPRegion for Google and YouTube

A fork of [Davoyan/ipregion](https://github.com/Davoyan/ipregion) that checks which region Google and YouTube see for your connection.

| Check | Result |
| --- | --- |
| Google | Region code from Google, with Google Play as a fallback |
| Google Search Captcha | Whether Google Search returned a CAPTCHA or abuse warning |
| YouTube | Region code from YouTube, with the Google result as a fallback |
| YouTube Premium and Music | Whether each service reports a regional restriction |
| YouTube CDN | Three-letter edge location code from Google Video |

## Usage

Download the script and run it with Bash.

~~~bash
curl -fsSLo ipregion.sh https://raw.githubusercontent.com/isultanov99/ipregion_google/main/ipregion.sh
bash ipregion.sh
~~~

By default, the script runs all checks over IPv4 and includes IPv6 when it detects a global IPv6 address.

~~~bash
bash ipregion.sh --group custom           # Google and YouTube, excluding CDN
bash ipregion.sh --group cdn              # YouTube CDN only
bash ipregion.sh --ipv4 --json            # IPv4 only, JSON output
bash ipregion.sh --ipv6                   # IPv6 only
bash ipregion.sh --proxy 127.0.0.1:1080   # SOCKS5 proxy
bash ipregion.sh --interface eth1         # Bind to a network interface
bash ipregion.sh --timeout 15 --verbose
bash ipregion.sh --help
~~~

The script uses system DNS and sends its checks to Google, YouTube and Google Video endpoints. The JSON output retains the upstream fields for compatibility. The top-level external IP fields are null and the primary GeoIP group is empty.

Requires Bash 4 or newer, curl, jq and column. Automatic IPv6 detection uses the ip command on Linux.

Licensed under the [MIT License](LICENSE).
