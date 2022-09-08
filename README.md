# Synced Object
  
[![Generic badge](https://img.shields.io/badge/Unity-2019.4.31f1-informational.svg)](https://unity3d.com/unity/whats-new/2019.4.31)
[![Generic badge](https://img.shields.io/badge/SDK-AvatarSDK3-informational.svg)](https://vrchat.com/home/download)
[![Generic badge](https://img.shields.io/github/downloads/VRLabs/Synced-Object/total?label=Downloads)](https://github.com/VRLabs/Synced-Object/releases/latest)

This prefab will allow you to network sync a world-fixed object for late joiners. Supports worlds up to 3000 units.

## How it works

Proximity receivers find on each axis what constraint adjustments need to be made to reach a target position, and physbone angle parameters are used to reach a target rotation. Data is sent over the network in steps.

1 Material (For anti-culling)
19 Objects
20 Constraints
2 Contact Receivers
1 Contact Sender
2 Physbones
1 Physbone colliders
1 Animator Layer
1 Float, 7 Booleans
15 Bits
 
## Install guide

Merge the FX controller to your own FX controller, using the [Avatars 3.0 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) tool.

"Synced Object.prefab" should go to the base of your Unity scene, which will give it base Unity scaling.

Unpack the prefab by right-clicking it and move the prefab to base of your avatar.

## Credits

Thanks to Razgriz for her ideas on syncing rotation. Thanks to Juzo and ThatFatKidsMom for testing and encouragement.
