# What are we dealing with ?

The motion-blinds library defines objects

+ class ParseException(Exception):
+ class GatewayStatus(IntEnum):
+ class BlindType(IntEnum):
+ class BlindStatus(IntEnum):
+ class LimitStatus(IntEnum):
+ class VoltageMode(IntEnum):
+ class WirelessMode(IntEnum):
+ class MotionCommunication: Communication class for Motion Gateways.
+ class MotionDiscovery(MotionCommunication):
+ class MotionMulticast(MotionCommunication): Multicast UDP communication class for a MotionGateway.
+ class MotionGateway(MotionCommunication): 
    Main class representing the Motion Gateway. 
    "Key not specified, specify a key when creating the gateway class like MotionGateway(ip = '192.168.1.100', key = 'abcd1234-56ef-78') when using _get_access_token."
    "Key not specified, specify a key when creating the gateway class like MotionGateway(ip = '192.168.1.100', key = 'abcd1234-56ef-78') when using the access_token."
+ class MotionBlind: Sub class representing a blind connected to the Motion Gateway.
+ class MotionTopDownBottomUp(MotionBlind): Sub class representing a Top Down Bottom Up blind connected to the Motion Gateway.


## Connecting the gateway

    from motionblinds import MotionGateway
    m = MotionGateway(ip = "192.168.1.100", key = "12ab345c-d67e-8f")

Is to be followed by

    m.device_list

In order to get the devices defined on the gateway (populate the m.device_list dict with devices).

 for blind in m.device_list.values():
    blind.Update()
    print(blind)
will provide this data

<MotionBlind mac: abcdefghujkl0001, type: RollerBlind, status: Stopped, position: 0 %, angle: 0, limit: Limits, battery: 1195, RSSI: -82 dBm>

Which is a representation of the Blind Object's variables, this is something tha we can use to extract data for fhem the representation.

Although it lokks like a dict, it is not directly usable in python and needs to be converted.