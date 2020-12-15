# Script Canvas nodes for NVIDIA Blast<a name="nvidia-blast-script-canvas"></a>


****  

|  | 
| --- |
| This feature is an [experimental](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#experimental) release and is subject to change\.  | 

The NVIDIA Blast gem includes several **Script Canvas** nodes to script destructible assets\. The nodes can be found in the **Blast** group in **Script Canvas**\. 

**Contents**
+ [BlastFamilyComponentNotificationBus nodes](#blast-family-notification-bus-nodes)
+ [BlastFamilyComponentNotificationBus nodes](#blast-family-request-bus-nodes)
+ [BlastFamilyDamageRequestBus nodes](#blast-family-damage-request-bus-nodes)

## BlastFamilyComponentNotificationBus nodes<a name="blast-family-notification-bus-nodes"></a>

**On Actor Created**  
Event notification that is invoked whenever an actor is created from a destroyed object used in the given entity\. 

**On Actor Destroyed**  
Notification that is invoked whenever an actor is destroyed from a destroyed object used in the given entity\. 

## BlastFamilyComponentNotificationBus nodes<a name="blast-family-request-bus-nodes"></a>

**Get Actors Data**  
Obtains the actor data, such as entity id and whether actor is static or not, from a destructible object used in the given entity\. 

## BlastFamilyDamageRequestBus nodes<a name="blast-family-damage-request-bus-nodes"></a>

**Capsule Damage**  
Full damage is dealt to all chunks and bonds that are not farther than **minRadius** from either **position0** or **position1**\. Linearly decreasing damage is applied if the distance is less than **maxRadius**\. 

**Destroy Actor**  
Destroys the actors from a destroyed object used in the given entity\. 

**Get Family Id**  
Get the entity id of the **Blast Family** in the given entity\. 

**Impact Spread Damage**  
Full damage is dealt to all chunks and bonds that are not farther than **minRadius** from **position**\. Decreasing damage is applied if the distance is less than **maxRadius**\. Decreasing damage is calculated using BFS on the support graph instead of Euclidean distances\. 

**Radial Damage**  
Full damage is dealt to all chunks and bonds that are not farther than **minRadius** from **position**\. Linearly decreasing damage is applied if the distance is less than **maxRadius**\. 

**Shear Damage**  
Deals full damage to bonds that are orthogonal to **normal**\. No damage is dealt to bonds that are parallel\. Damage to chunks is dependent on distance to **position**\. The damage falloff between **minRadius** and **maxRadius** is linear\. 

**Stress Damage**  
Stress damage is applied using **force** vector instead of a scalar value\. Damage is propagated between bonds based on the support graph\. 

**Triangle Damage**  
Full damage is dealt to all chunks and bonds that intersect with a triangle described by the given vertices defined by **position0**, **position1**, and **position2**\. 