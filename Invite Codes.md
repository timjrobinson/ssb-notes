An Invite code makes it so the creator of the code automatically adds the redeemer as a friend when the code is redeemed. 

Invite codes can be created with:

`ssb-server invite.create <n>` where n is an integer of how many uses this code should have. 

For invites to be reedeemable your server needs a publicly available IP address or URL. As when the invite is redeemed the redeemer basically connects to your server via that IP/URL and tells it the code, to get added as a friend. 

## Public Invite Codes

Can get a list of public pub servers and their invite codes at: https://github.com/ssbc/ssb-server/wiki/pub-servers