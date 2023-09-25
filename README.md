<div align="center">

# 15 Bit Position Rotation Networking

[![Generic badge](https://img.shields.io/github/downloads/VRLabs/15-Bits-Position-Rotation-Networking/total?label=Downloads)](https://github.com/VRLabs/15-Bits-Position-Rotation-Networking/releases/latest)
[![Generic badge](https://img.shields.io/badge/License-MIT-informational.svg)](https://github.com/VRLabs/15-Bits-Position-Rotation-Networking/blob/main/LICENSE)
[![Generic badge](https://img.shields.io/badge/Unity-2019.4.31f1-lightblue.svg)](https://unity3d.com/unity/whats-new/2019.4.31)
[![Generic badge](https://img.shields.io/badge/SDK-AvatarSDK3-lightblue.svg)](https://vrchat.com/home/download)

[![Generic badge](https://img.shields.io/discord/706913824607043605?color=%237289da&label=DISCORD&logo=Discord&style=for-the-badge)](https://discord.vrlabs.dev/)
[![Generic badge](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Fshieldsio-patreon.vercel.app%2Fapi%3Fusername%3Dvrlabs%26type%3Dpatrons&style=for-the-badge)](https://patreon.vrlabs.dev/)

This prefab will allow you to network the position and rotation of a world-fixed object. Supports world sizes up to 10,000 meters

![Alt text]()

### ⬇️ [Download latest Unitypackage](https://github.com/VRLabs/15-Bits-Position-Rotation-Networking/releases/latest)

<!-- 
### 📦 [Add to VRChat Creator Companion]() -->

</div>

---

## How it works

* Contact Receivers are used to turn the position of an object into bits, and physbones are used to turn the rotation of an object into bits.
* This data is transmitted over 6-13 seconds, and when received, turned back into a position and a rotation for the object.

## Install guide

* Merge the Animator Controller ``15 Bits Position Rotation Networking FX`` to your own FX Controller, using the [Avatars 3.0 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) tool.
  * If you want to try one of the examples, you can merge one of the ``FX`` controllers under ``Resources/Examples``.
  * These are more complete versions of the System, but they require a World Constraint with the ``15 Bits Position Rotation Networking Target`` under the ``World Constraint/Container`` object.
* Merge the Expression Parameters ``15 Bits Position Rotation Networking Parameters`` to your own Expression Parameters, using the [Avatars 3.0 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) tool.
* Drag & drop the ``15 Bits Position Rotation Networking`` prefab into the base of your Hierarchy.
* Right click and unpack the prefab, then drag & drop it onto your avatar.

## How to use

* The ``15BitsPositionRotationNetworking/Control`` parameter controls whether or not the System is syncing.
* Use a World Constraint to place the ``15 Bits Position Rottation Netorking Target`` in world space, and enable the ``15BitsPositionRotationNetworking/Control`` parameter.
* After the 6-13 seconds, the ``Result`` object will be placed at the ``15 Bits Position Rotation Netorking Target`` location in world space.
* You can use the following parameters to decide when to show the object and when to constrain the object to the Result target:
  * ``15BitsPositionRotationNetworking/Finished`` will be True when a player has finished networking.
  * ``15BitsPositionRotationNetworking/Interrupted`` will be True if a player has distance hidden you during networking, and didn't finish (and the Result transform is in the wrong place).

## Additional Notes

* If a remote user has _**both**_ self-interaction *and* avatar interaction permission with your avatar blocked, the world prop will never be shown to them.
* There is an object at "15 Bits Position Rotation Networking/World/Culling". You can enable the scale constraint on this object to be unculled as soon as your avatar loads.

## Performance stats

```c++
Material Slots:     1
Constraints:        19
Contact Receivers:  3
Contact Senders:    2
Parameter Memory:   15
PhysBone Collider:  1
PhysBones:          2
FX Animator Layers: 1
```

## Hierarchy layout

```html
15 Bits Position Rotation Networking
|-Copy Angle
|  |-Plane
|-Measure Angle
|  |-Next
|  |-Polar
|-World
|  |-Culling
|  |-Very Coarse
|  |-Coarse
|  |-Fine
|  |-Very Fine
|  |  |-Proximity
|  |  |-Next
|  |-Position
|  |-Rotation
|  |-Result
|-Cube
```

## Contributors

* [lin](https://github.com/oofdesu)

## Credits

Thanks to [Razgriz](https://github.com/rrazgriz) for her ideas on syncing rotation. Thanks to [Juzo](https://github.com/JuzoVR) and [ThatFatKidsMom](https://github.com/ThatFatKidsMom) for testing and encouragement.

## License

15 Bits Position Rotation Networking is available as-is under MIT. For more information see [LICENSE](https://github.com/VRLabs/15-Bits-Position-Rotation-Networking/blob/main/LICENSE).

​

<div align="center">

[<img src="https://github.com/VRLabs/Resources/raw/main/Icons/VRLabs.png" width="50" height="50">](https://vrlabs.dev "VRLabs")
<img src="https://github.com/VRLabs/Resources/raw/main/Icons/Empty.png" width="10">
[<img src="https://github.com/VRLabs/Resources/raw/main/Icons/Discord.png" width="50" height="50">](https://discord.vrlabs.dev/ "VRLabs")
<img src="https://github.com/VRLabs/Resources/raw/main/Icons/Empty.png" width="10">
[<img src="https://github.com/VRLabs/Resources/raw/main/Icons/Patreon.png" width="50" height="50">](https://patreon.vrlabs.dev/ "VRLabs")
<img src="https://github.com/VRLabs/Resources/raw/main/Icons/Empty.png" width="10">
[<img src="https://github.com/VRLabs/Resources/raw/main/Icons/Twitter.png" width="50" height="50">](https://twitter.com/vrlabsdev "VRLabs")

</div>

---
