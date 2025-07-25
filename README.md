<span align="center">

# Homebridge Shark Clean Vacuum Plugin

[![verified-by-homebridge](https://badgen.net/badge/homebridge/verified/purple)](https://github.com/homebridge/homebridge/wiki/Verified-Plugins)
[![npm](https://badgen.net/npm/dt/@homebridge-plugins/homebridge-sharkiq?color=purple)](https://www.npmjs.com/package/@homebridge-plugins/homebridge-sharkiq)
[![npm](https://badgen.net/npm/v/@homebridge-plugins/homebridge-sharkiq?color=purple)](https://www.npmjs.com/package/@homebridge-plugins/homebridge-sharkiq)

</span>

A new homebridge plugin for SharkIQ Vacuums.

Contributions are always welcome. I used the [sharkiq](https://github.com/JeffResc/sharkiq/) python module as a reference for creating the javascript wrapper to control SharkIQ Vacuums.

This plguin has only been tested on the `UR250BEXUS` model.

The fastest way to get community support (not for bugs) is to join the [Homebridge Discord server](https://discord.gg/kqNCe2D) and chat in the #sharkiq channel.

## Install and Setup

### Step 1.

Run `npm install -g homebridge-sharkiq`

### Step 2.

Configure Homebridge. The config file for SharkIQ should include:

```json
{
  "platforms": [
    {
      "name": "SharkIQ",
      "platform": "SharkIQ",
      "email": "[Shark Clean Account Email]",
      "password": "[Shark Clean Account Password]",
      "oAuthCode": "[Optional. Use for manually obtaining credentials]",
      "vacuums": [
        "[Shark Vacuum DSN]",
        "..."
      ],
      "europe": false,
      "invertDockedStatus": false,
      "dockedUpdateInterval": 30000
    }
  ]
}
```

# Important

You may be prompted to use the manual OAuth login method. In order to use the manual OAuth login method, you must remove the email and password values in your configuration first.

#

The email and password is your Shark Clean account you used to setup the vacuum. The Vacuums array is a list of your vacuum's device serial numbers (DSN). If you only have one vacuum, just include the one's DSN. The DSN(s) can be found in the SharkClean mobile app.

If you would like to manually obtain your Shark Clean credentials without using your email and password, you can obtain a OAuth code instead. Refer to the `OAuth Code Login Method` section.

The Vacuums array is a list of your vacuum's device serial numbers (DSN). If you only have one vacuum, just include the one's DSN. The DSN(s) can be found in the SharkClean mobile app.

If you are in Europe, set the `europe` config value to `true`. SharkClean has separate servers for the U.S. and Europe. The default value is `false`, which connects to the U.S. server.

The default interval between updating the docked status is 30 seconds (30000 ms). To change the docked status interval, add `dockedUpdateInterval` to your config. Value is in milliseconds. If the interval is too low, you have the risk of your account being rate limited.

## Features

- Be able to turn on and off the vacuum
- Set the power mode of the vacuum and change it while running
- Sensor for if the vacuum is docked or not
  - The sensor will display as "opened" when the vacuum is docked and "closed" when the vacuum is not docked
  - Set `invertDockedStatus` to `true` to display as "closed" when the vacuum is docked and "opened" when the vacuum is not docked
- Pause switch for pausing the vacuum while it's running

### OAuth Code Login Method

The OAuth Code value is for creating and storing the login for the plugin. Here is how to sign in with this method.

1. Run Homebridge with the latest plugin version.
2. Open the Homebridge logs
3. Open the URL in the console printed by homebridge-sharkiq. Safari will not work due to the way Safari handles the results of the login
4. Before you login, open up developer tools in your browser (inspect element), and navigate to the network tab
5. Enter your login info, and press continue
6. Open the request with the uri of `/authorize/resume` that shows up and view the headers
7. Search `com.sharkninja.shark` in the headers
8. Copy the code in between `code=` and `&`. for example in `com.sharkninja.shark://login.sharkninja.com/ios/com.sharkninja.shark/callback?code=abcdefghijkl&state=`, `abcdefghijkl` is the code that needs to be copied
9. Open your Homebridge configuration, and paste the `code` value in the OAuth Code config option
10. Restart Homebridge

## Notes

Contributions would be very helpful to help this Homebridge plugin stay maintained and up to date. If you have any problems, please create an issue.

## Useful Links

- [SharkIQ Python](https://github.com/JeffResc/sharkiq/)
