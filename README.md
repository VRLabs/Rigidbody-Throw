<div align="center">

# Rigidbody Throw

[![Generic badge](https://img.shields.io/github/downloads/VRLabs/Rigidbody-Throw/total?label=Downloads)](https://github.com/VRLabs/Rigidbody-Throw/releases/latest)
[![Generic badge](https://img.shields.io/badge/License-MIT-informational.svg)](https://github.com/VRLabs/Rigidbody-Throw/blob/main/LICENSE)
[![Generic badge](https://img.shields.io/badge/Unity-2019.4.31f1-lightblue.svg)](https://unity3d.com/unity/whats-new/2019.4.31)
[![Generic badge](https://img.shields.io/badge/SDK-AvatarSDK3-lightblue.svg)](https://vrchat.com/home/download)

[![Generic badge](https://img.shields.io/discord/706913824607043605?color=%237289da&label=DISCORD&logo=Discord&style=for-the-badge)](https://discord.vrlabs.dev/)
[![Generic badge](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Fshieldsio-patreon.vercel.app%2Fapi%3Fusername%3Dvrlabs%26type%3Dpatrons&style=for-the-badge)](https://patreon.vrlabs.dev/)

Throw an object with collision against the world

![Rigidbody Throw](https://github.com/VRLabs/Rigidbody-Throw/assets/76777936/b4915105-3d27-4095-b162-435a2a981b89)


### ⬇️ [Download Latest Version](https://github.com/VRLabs/Rigidbody-Throw/releases/latest)


### 📦 [Add to VRChat Creator Companion](https://vrlabs.dev/packages?package=dev.vrlabs.rigidbody-throw)

</div>

---

## How it works

* A particle system is parented to the reset target, which emits particles as it moves.
* When the system is enabled, these particles hit the Force Collider, which adds force to the Rigidbody.
* This Rigidbody then flies forward as if thrown, and collides with the world using the Collision Collider.
* Meanwhile, Contact Senders and Receivers, in combination with Constraints, are used to figure out the position of the thrown object, and this is synced to the remote client (since parameter force is local only).
  * This remote sync is not incredibly accurate to not spend too many bits on it: 25m from where you throw, with 0.2m precision, so landing location might differ slightly between local and remote.
  * If you want rotation sync, install the components from the Rotation-Synced directory.

## Install guide

https://github.com/VRLabs/Rigidbody-Throw/assets/76777936/57fbfe66-ddfd-4b0c-b168-e739ffc0a1ef

* Merge the Animator Controller ``Rigidbody Throw FX`` to your own FX Controller, using the [Avatars 3.0 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) tool.
* Merge the Expression Parameter List ``Rigidbody Throw Parameters`` to your own Expression Parameter List, using the [Avatars 3.0 Manager](https://github.com/VRLabs/Avatars-3.0-Manager) tool.
* Drag & drop the ``Rigidbody Throw`` prefab into the base of your Hierarchy.
* Right click and unpack the prefab, then drag & drop it onto your avatar.
* Move ``Reset Target`` outside of ``Rigidbody Throw`` and place it anywhere in your avatar's hierarchy. Adjust the transforms as needed.

## How to use

* Place the objects you want to to use inside ``Rigidbody Throw`` -> ``Container``.
    * Alternatively you can constrain the objects to ``Container``.
* Your right hand gesture must be 2 (HandOpen) for the system to release, and 1 (Fist) to reset.
* To change the friction and the bounciness, change the parameters on the ``Resources/Physics Material`` Physics Material and apply that Physics Material to your Collision Collider.
* To have a custom throwing/reset condition, change the ``GestureRight Equals 1 or 2`` conditions in the ``Rigidbody Throw Main`` layer.  
* To change world collision, only use Colliders on the `Collision Collider` object. This can be a Box Collider, Sphere Collider, Capsule Collider, but it has to be on the `Collision Collider` object.

## Performance stats

Default version:
```c++
Colliders:              2
Constraints:            10
Contact Receivers:      4
Contact Senders:        2
FX Animator Layers:     4
Particle Systems:       2
Rigidbodies:            2
Joints:                 1
Expression Parameters:  27
```

Rotation synced version:
```c++
Colliders:              2
Constraints:            14
Contact Receivers:      4
Contact Senders:        2
FX Animator Layers:     4
Particle Systems:       2
PhysBones:              6
PhysBone Colliders:     3
Rigidbodies:            2
Joints:                 1
Expression Parameters:  51
```

## Hierarchy layout

Default version:
```html
Rigidbody Throw
|-Reset Target
|-Force Particle
|-Container
|  |-Colliders
|  |  |-Force Collider
|  |  |-Colission Collider
|  |  |-Collision Detection
|  |-Example Sphere
|-Quick Position Sync
|  |-Position Sync
|  |  |-Contacts
|  |  |  |-Sender
|  |  |  |-Receiver X
|  |  |  |-Receiver Y
|  |  |  |-Receiver Z
|  |  |-Local Target
|  |  |-Remote Target
```

Rotation synced version:
```html
Rigidbody Throw
|-Reset Target
|-Force Particle
|-Container
|  |-Colliders
|  |  |-Force Collider
|  |  |-Colission Collider
|  |  |-Collision Detection
|  |-Example Cube
|-Quick Position Sync
|  |-Position Sync
|  |  |-Contacts
|  |  |  |-Sender
|  |  |  |-Receiver X
|  |  |  |-Receiver Y
|  |  |  |-Receiver Z
|  |  |-Local Target
|  |  |-Remote Target
|  |-Rotation Sync
|  |  |-Measure Bones
|  |  |  |-Measure X Magnitude
|  |  |  |-Measure X Sign
|  |  |  |-Measure Y Magnitude
|  |  |  |-Measure Y Sign
|  |  |  |-Measure Z Magnitude
|  |  |  |-Measure Z Sign
|  |  |-Measure Planes
|  |  |  |-X Angle Plane
|  |  |  |-Y Angle Plane
|  |  |  |-Z Angle Plane
```

## Contributors

* [hfcred](https://github.com/hfcred)
* [jellejurre](https://github.com/jellejurre)
* [jetees](https://github.com/jetees)
* [JustSleightly](https://links.sleightly.dev)

## License

Rigidbody Throw is available as-is under MIT. For more information see [LICENSE](https://github.com/VRLabs/Rigidbody-Throw/blob/main/LICENSE).

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

