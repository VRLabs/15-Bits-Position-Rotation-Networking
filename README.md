# 15 Bits Position Rotation Networking
  
[![Generic badge](https://img.shields.io/badge/Unity-2019.4.31f1-informational.svg)](https://unity3d.com/unity/whats-new/2019.4.31)
[![Generic badge](https://img.shields.io/badge/SDK-AvatarSDK3-informational.svg)](https://vrchat.com/home/download)
[![Generic badge](https://img.shields.io/github/downloads/VRLabs/15-Bits-Position-Rotation-Networking/total?label=Downloads)](https://github.com/VRLabs/15-Bits-Position-Rotation-Networking-Private/releases/latest)

This prefab will allow you to network the position and rotation of a world-fixed object. Supports world sizes up to 10,000 meters.

## How it works

Proximity receivers find what constraint adjustments need to be made to reach a target position, and physbone angle parameters are used to reach a target rotation. Data is sent over the network in 18 steps. Sync time depends on the FPS of the host and when a remote viewer has loaded your avatar, relative to the state machine networking cycle. Average times are 6 to 13 seconds.

- 1 Material (For anti-culling)
- 18 Objects
- 19 Constraints
- 3 Contact Receivers
- 2 Contact Senders
- 2 PhysBones
- 1 PhysBone Collider
- 1 Animator Layer
- 1 Synced Float, 7 Synced Booleans
- 15 Bits
 
## Install guide

Merge the FX controller to your own FX controller, using the [Avatars 3.0 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) tool.

If you are testing an example controller, merge the example FX instead.

"15BitsPositionRotationNetworking/Control" is a synced parameter, so click the checkbox within the tool to add it to your avatar's parameter asset.

Everything under "15BitsPositionRotationNetworking/Send/" is also a synced parameter. There are 7 Booleans and 1 Float that should be synced in total.

"15 Bits Position Rotation Networking.prefab" should go to the base of your Unity scene, which will give it base Unity scaling.

Unpack the prefab by right-clicking it and move the prefab to base of your avatar.

## How to use

The "15BitsPositionRotationNetworking/Control" parameter must be True to start the system. Changing it to False will stop and reset the system.

Locate "15 Bits Position Rotation Networking/15 Bits Position Rotation Networking Target" and take it out of the prefab hierarchy. Place it somewhere that will be in world space by the time you set 15BitsPositionRotationNetworking/Control as True, as you should be trying to sync a world object.

Constrain your world prop to the "15 Bits Position Rotation Networking/World/Result" transform. By default, 15 Bits Position Rotation Networking/Cube is constrained to it. 15 Bits Position Rotation Networking/World/Result will start at world 0,0,0 and when networking is finished, it will move to the synced transforms. I recommend testing the prefab like this until you know what to expect.

## Visibility

"Active" players will have loaded your avatar before setting 15BitsPositionRotationNetworking/Control to True. "Late" players loaded your avatar after 15BitsPositionRotationNetworking/Control is True. There is another kind of player that uses the Avatar Distance Hider and did not finish networking before your avatar was hidden. They should be treated as late. Try to show the most appropriate effect to the player.

"15BitsPositionRotationNetworking/Finished" will be True when a player has finished networking.

"15BitsPositionRotationNetworking/Interrupted" will be True if a player has distance hidden you during networking, and didn't finish.

There are example FX controllers in the Resources folder. You do not have to follow the examples to the letter, but try to understand the logic and use of parameters to show the player the correct effect.

The examples use a [World Constraint](https://github.com/VRLabs/World-Constraint) and expects the 15 Bits Position Rotation Networking Target to be in World Constraint/Container.

## Notes

Having a controller reference in your avatar's main animator before you upload can actually cause errors.

Don't try using a clone in the emulator to test. Test with only the original avatar in the scene. Do remote testing in-game.

If a remote user has _**both**_ self-interaction *and* avatar interaction permission with your avatar blocked, the world prop will never be shown to them. This is because recovering from the Avatar Distance Hiding feature requires a self-interaction. Without the ability to recover properly from distance hiding, it's more likely that a user will see incorrect results. Mitigations for this seem make the system worse for everyone else. Since it's exceedingly rare to have both of these options disabled, and users that do have both of these options disabled are probably very careful with what they allow to be shown, I've opted to require these users to enable at least self-interaction permission.

There is an object at "15 Bits Position Rotation Networking/World/Culling". For situations where avatar performance rank does not matter, you may want to enable the scale constraint on this object by default, so that you will be unculled as soon as your avatar loads. Ideally you would only do this on a private avatar. This will not circumvent Avatar Distance Hiding.

## Credits

Thanks to [Razgriz](https://github.com/rrazgriz) for her ideas on syncing rotation. Thanks to [Juzo](https://github.com/JuzoVR) and [ThatFatKidsMom](https://github.com/ThatFatKidsMom) for testing and encouragement.
