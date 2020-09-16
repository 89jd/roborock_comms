# roborock_comms

This github is for my findings of using the roborock app in parallel with local communication.

To communicate locally with the device, it uses the Tuya protocol. It sends a DPS of 101, and a Base64 encoding of the the vacuum protocol (above). It does this using the device ID and the key (the same one that is used).

Furthermore, I have worked out how to get the map using Tuya mqtt server. I managed to get the details to log in to your account, but they seem to match this persons finding here in terms of how they are created (Link in second post). The mqtt command I am using to get the map is: -

mosquitto_sub -v -h m1.tuyaeu.com -u p******* -P ************ -t m/m/i/<roborock_device_id>

It is possible to subscribe, and by sending the get_map_v1 request (see first link) locally, it will make the mqtt spit out the encrypted map. It needs to be request with a new JSON object though: -

"security":{"endpoint":"****","nonce":"\<AES generated key\>"}

It is possible to retrieve the “endpoint” from SharedPreferences.

See the script above from how to decrypt what is returned from mqtt into the gzip format map file
