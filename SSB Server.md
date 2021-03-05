Category:: [[SSB]]

when you install ssb-server globally (`npm i -g ssb-server`) it adds ssb-server executable to your system where you can run publish etc commands against it. 

You can also just use it in a script by requiring 'ssb-server' and 'ssb-config' then doing server = Server(config) and running server.publish or server.createHistoryStream etc. 

Can get the entire manifest of available commands with server.getManifest()

[[SSB Server Minimal Manifest]]

## Structure

The server itself contains as little code as possible, most ssb functionality is added via modules. 

## Commands

- `ssb-server whoami` - Easiest way to check if the server is running. Returns your SSB user id. 
- [[Invite Codes]]