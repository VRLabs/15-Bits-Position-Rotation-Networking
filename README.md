# Synced Object
  
[![Generic badge](https://img.shields.io/badge/Unity-2019.4.31f1-informational.svg)](https://unity3d.com/unity/whats-new/2019.4.31)
[![Generic badge](https://img.shields.io/badge/SDK-AvatarSDK3-informational.svg)](https://vrchat.com/home/download)
[![Generic badge](https://img.shields.io/github/downloads/VRLabs/Synced-Object/total?label=Downloads)](https://github.com/VRLabs/Synced-Object/releases/latest)

This prefab will allow you to network sync a world-fixed object for late joiners. Supports worlds up to 3000 units.

## How it works

Proximity receivers find what constraint adjustments need to be made to reach a target position, and physbone angle parameters are used to reach a target rotation. Data is sent over the network in 18 steps. Sync time depends on the FPS of the host and when a remote viewer has joined the instance, relative to the state machine networking cycle. Average times are 6 to 13 seconds.

- 1 Material (For anti-culling)
- 20 Objects
- 20 Constraints
- 4 Contact Receivers
- 2 Contact Sender
- 2 Physbones
- 1 Physbone colliders
- 1 Animator Layer
- 1 Float, 7 Booleans
- 15 Bits
 
## Install guide

Merge the FX controller to your own FX controller, using the [Avatars 3.0 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) tool.

"SyncedObject/Control" is a synced parameter, so click the checkbox within the tool to add it to your avatar's parameter asset.

Everything under "SyncedObject/Send/" is also a synced parameter. There are 7 Booleans and 1 Float parameter.

"Synced Object.prefab" should go to the base of your Unity scene, which will give it base Unity scaling.

Unpack the prefab by right-clicking it and move the prefab to base of your avatar.

## How to use

Locate "Synced Object/Sync Target" and take it out of the prefab hierarchy. Place it somewhere in a world space hierarchy, as you should be trying to sync a world object. I recommend putting the Sync Target inside of a [World Constraint]([https://github.com/VRLabs/Avatars-3.0-Manager](https://github.com/VRLabs/World-Constraint)) and using the "SyncedObject/Control" parameter for transitions.

Place your world object props into the "Synced Object/Container" hierarchy.

The "SyncedObject/Control" parameter must be true to start syncing. The "SyncedObject/Show" parameter will indicate when you can show your world prop. Always hide when SyncedObject/Control is False.

## Option details
There are two ways the world prop can start for viewers, fast and late.

Fast appearance can occur when a viewer has your avatar loaded and not culled before you enable the SyncedObject/Control parameter. The object will appear quickly without any network sync and behave like a regular world drop. Later, remote viewers will switch to the synced transform after the state machine networking has cycled one time. This switch may become noticeable if your world drop is signficantly desynced by quick movement. Slow and deliberate drops will likely be unnoticeable when the switch happens.

Because it can be visually imperfect, fast starting is disabled for remote viewers by default. To enable fast starting remotely, unmute the transition to "Fast Start" in your merged "Sync XYZ" layer. 

Late appearance occurs for viewers that do not have your avatar loaded, or are culling your avatar when the SyncedObject/Control parameter is enabled. They will only see the synced transform after the networking has cycled once.

For the host, network sync is disabled by default, and you will always see a fast start. For debugging purposes, you can view the late start by inspecting the "Start" state in your merged "Sync XYZ" layer and using the parameter driver on that state to set the "SyncedObject/Debug" parameter as True.

There is an object called "SyncedObject/Solving/World/Culling". For situations where avatar performance rank does not matter, you may want to enable the scale constraint on this object by default, so that you will be unculled as soon as your avatar loads. Ideally you would only do this on a private avatar. This will not circumvent Avatar Distance Hiding.

## Notes

If a remote user has _**both**_ self-interaction *and* avatar interaction permission with your avatar blocked, the world prop will never be shown to them. This is because recovering from the Avatar Distance Hiding feature requires a self interaction. Without the ability to recover properly from distance hiding, it's more likely that a user will see incorrect results. Mitigations for this seem make the system worse for everyone else. Since it's exceedingly rare to have both of these options disabled, and users that do have both of these options disabled are probably very careful with what they allow to be shown, I've opted to require these users to enable at least interaction permission for your avatar.

## Credits

Thanks to [Razgriz](https://github.com/rrazgriz) for her ideas on syncing rotation. Thanks to [Juzo](https://github.com/JuzoVR) and [ThatFatKidsMom](https://github.com/ThatFatKidsMom) for testing and encouragement.
