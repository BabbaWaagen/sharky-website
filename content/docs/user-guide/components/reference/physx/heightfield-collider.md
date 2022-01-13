---
linkTitle: PhysX Heightfield Collider
title: PhysX Heightfield Collider Component
description: Use the PhysX Heightfield Collider component to create collision for heightfields such as terrain in Open 3D Engine (O3DE).
toc: true
---

The **PhysX Heightfield Collider** component creates NVIDIA PhysX simulation collider geometry based on the shape definition supplied by an [Axis-Aligned Box Shape](/docs/user-guide/components/reference/shape/axis-aligned-box-shape/) component.

{{< note >}}
The PhysX Heightfield Collider component attached to an entity with an **Axis-Aligned Box Shape component** and a **Terrain Physics Collider** creates a static (non-moving) entity.
{{< /note >}}

## Provider

[PhysX](/docs/user-guide/gems/reference/physics/nvidia/physx/)

## Dependencies

[Axis-Aligned Box Shape](/docs/user-guide/components/reference/shape/axis-aligned-box-shape)

## PhysX Heightfield Collider properties 

![\[PhysX Heightfield Collider component interface.\]](/images/user-guide/component/physx/physx/ui-physx-heightfield-collider-A.png)

| Property | Description | Values | Default |
| - | - | - | - |
| Collision Layer | The collision layer that's assigned to this collider. For more information, see [Collision Layers](/docs/user-guide/interactivity/physics/nvidia-physx/configuring/configuration-collision-layers/). | Collision layer | `Default` |
| Collides With | The collision group containing the layers that this collider collides with. For more information, see [Collision Groups](/docs/user-guide/interactivity/physics/nvidia-physx/configuring/configuration-collision-groups/). | Collision group | `All` |
| Trigger | When enabled, this heightfield collider functions as a trigger. A trigger performs a quick overlap test and does not apply forces or return contact point information. Use this to speed up PhysX computations where a simple overlap between colliders is sufficient. | Boolean | `Disabled` |
| Simulated |  When enabled, this heightfield collider will be part of the physics simulation. | Boolean | `Enabled` |
| In Scene Queries |  When enabled, this heightfield collider can be queried for raycasts, shapecasts and overlap. | Boolean | `Enabled` |
| Tag |  Set a tag for this heightfield collider. Tags can be used to quickly identify components in script or code. | String |  |
| Rest offset |  PhysX bodies come to rest separated by the sum of their rest offset values. The **Rest offset** value must be less than the **Contact offset** value. | -Infinity to `50.0` | `0.0` |
| Contact offset | PhysX bodies generate contacts when they are within the sum of their contact offset values. The **Contact offset** value must be greater than the **Rest offset** value. | `0.0` to `50.0` | `0.02` |
| Draw collider |  Render this heightfield collider in the viewport. Enabled by default. | Boolean | `Enabled` |

## Colliders as triggers 

Triggers allow colliders to perform efficient overlap tests. Colliders marked as triggers won't have forces applied when they intersect with another collider. This is useful for detecting when something enters a certain area or when two objects overlap. Use Lua or Script Canvas to detect overlap.

{{< note >}}
Because triggers don't perform contact resolution, the contact points between a trigger and another collider aren't available.
{{< /note >}}
