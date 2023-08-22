# chromecast-tool

This script allows basic configuration of a Chromecast device without
having to use Google Home or any other app.

This has been tested with a 1st generation Chromecast (2013).

## How to use it

This is a single shell script that can be run directly. The available
commands are:

* `connect-wifi`: Connect the Chromecast to a Wi-Fi network.
* `get-config`: Show the current Chromecast settings.
* `set-config`: Change some of the Chromecast settings.
* `get-locales`: Get a list of the supported locales.
* `get-timezones`: Get a list of the supported timezones.

Run `chromecast-tool` without options for more details.

## Dependencies

The following external tools are needed:

* [curl](https://github.com/curl/curl)
* [jq](https://github.com/stedolan/jq)
* [openssl](https://github.com/openssl/openssl) (for the `connect-wifi` command).

## Use case: changing a Chromecast's Wi-Fi settings

A Chromecast needs to be connected to the user's Wi-Fi network. If the
Wi-Fi settings change or the device is physically moved to a different
location then it needs to be reconfigured. This typically requires the
Google Home app and it doesn't always work correctly.

This is how to reset a Chromecast using `chromecast-tool`:

1. Press the button on the Chromecast for about 10 seconds to do a
   factory reset.
2. Wait for the Chromecast to reboot. It will create a private Wi-Fi
   network called `ChromecastXXXX` (where XXXX are 4 random digits).
3. Connect your computer to that Wi-Fi network.
4. Optional: Change the visible name and other options (see also the
`get-locales` and `get-timezones` commands):
```
$ chromecast-tool set-config --name MyChromecast \
                             --locale es \
                             --timezone Europe/Madrid \
                             --timeformat 2
```
5. Connect the Chromecast to your home Wi-Fi network:
```
$ chromecast-tool connect-wifi --ssid MyNetwork --pass MyPassword
```
6. The Chromecast's private network disappears and the device is ready
   to use.
