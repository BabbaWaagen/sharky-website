# Cloth component<a name="component-cloth"></a>


****  

|  | 
| --- |
| This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 

The **Cloth** component treats the vertices of any mesh that it references as cloth particles and applies physical properties, forces, and constraints to simulate the behavior of cloth\. You can add this component to any entity that has **Mesh** or **Actor** components\. You can add multiple cloth components to an entity\. 

The **Cloth** component is provided by the [NVIDIA Cloth gem](nvidia-cloth.md)\. 

For information on using the **Cloth** component see [Simulate cloth with NVIDIA Cloth](nvidia-cloth-intro.md)\. 

**Contents**
+ [Base properties](#component-cloth-base-properties)
+ [Motion constraints properties](#component-cloth-motion-constraints-properties)
+ [Backstop properties](#component-cloth-backstop-properties)
+ [Damping properties](#component-cloth-damping-properties)
+ [Inertia properties](#component-cloth-inertia-properties)
+ [Wind properties](#component-cloth-wind-properties)
+ [Collision properties](#component-cloth-collision-properties)
+ [Self Collision properties](#component-cloth-self-collision-properties)
+ [Fabric stiffness properties](#component-cloth-fabric-stiffness-properties)
+ [Fabric compression properties](#component-cloth-fabric-compression-properties)
+ [Fabric stretch properties](#component-cloth-fabric-stretch-properties)
+ [Tether constraints properties](#component-cloth-tether-constraints-properties)
+ [Quality properties](#component-cloth-quality-properties)

## Base properties<a name="component-cloth-base-properties"></a>

![\[Base properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-A-1.27.png)

**Simulate in editor**  
Enable to simulate cloth in editor\. 

**Mesh node**  
The mesh node to simulate as cloth\. The meshes available in the list have **Cloth** modifiers applied in **FBX Settings**\. 

**Mass**  
Scale multiplier applied to the mass of all cloth particles\. A value of **0\.0** in this property makes all cloth particles static\. 

**Custom Gravity**  
Enable to override global gravity and set a custom gravity value for this cloth\. 

**Gravity**  
Set gravity for this cloth\. The default, **\-9\.81** on the **Z** axis, is standard gravity\.   
The **Gravity** property is enabled by the **Custom Gravity** property\. 

**Gravity Scale**  
Scale multiplier applied to the gravity of cloth particles\.

**Stiffness frequency**  
Stiffness exponent that adjusts the overall stiffness of the cloth simulation\. This exponent is applied per second to these properties:   
+ **Damping**
+ **Damping \- Linear drag**
+ **Damping \- Angular drag**
+ **Wind \- Air drag coefficient**
+ **Wind \- Air lift coefficient**
+ **Self collision \- Stiffness**
+ **Fabric stiffness**
+ **Fabric compression**
+ **Fabric stretch**
+ **Tether \- Stretch**

## Motion constraints properties<a name="component-cloth-motion-constraints-properties"></a>

![\[Motion constraints properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-B-1.27.png)

**Max distance**  
Maximum distance limit in meters for cloth particle movement\. 

**Scale**  
Scale value applied to all motion constraints\.   
**0\.0**: Motion constraints have no effect\.   
**1\.0**: Motion constraints are fully applied\. 

**Bias**  
Bias value in meters added to all motion constraints\. Valid values range from **\-Infinity** to **Infinity**\. 

**Stiffness**  
Stiffness for motion constraints\.   
**0\.0**: Stiffness is not applied to motion constraints\.   
**1\.0**: Stiffness is fully applied to motion constraints\. 

## Backstop properties<a name="component-cloth-backstop-properties"></a>

![\[Backstop properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-C-1.27.png)

**Note**  
Backstop properties are only available when a **Backstop** vertex color stream is specified in the **Cloth** modifier for the selected **Mesh node** in **FBX Settings**\. 

**Radius**  
The radius in meters of the backstop sphere\. 

**Back offset**  
The offset in meters for backstop spheres behind the cloth\. 

**Front offset**  
The offset in meters for backstop spheres in front of the cloth\. 

## Damping properties<a name="component-cloth-damping-properties"></a>

![\[Damping properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-D-1.27.png)

**Damping**  
Damping of cloth particle velocity\.   
**0\.0**: Velocity is unaffected\.   
**1\.0**: Velocity is zeroed\. 

**Linear Drag**  
Portion of velocity applied to cloth particles\.   
**0\.0**: Cloth particles are unaffected\.   
**1\.0**: Damped global cloth particle velocity\. 

**Angular Drag**  
Portion of angular velocity applied to turning cloth particles\.   
**0\.0**: Cloth particles are unaffected\.   
**1\.0**: Damped global cloth particle angular velocity\. 

## Inertia properties<a name="component-cloth-inertia-properties"></a>

![\[Inertia properties of the NVIDIA Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-E-1.27.png)

**Linear**  
Portion of linear acceleration applied to cloth particles\.   
**0\.0**: Cloth particles are unaffected\.   
**1\.0**: Physically correct linear acceleration\. 

**Angular**  
Portion of angular acceleration applied to turning cloth particles\.   
**0\.0**: Cloth particles are unaffected\.   
**1\.0**: Physically correct angular acceleration\. 

**Centrifugal**  
Portion of angular velocity applied to turning cloth particles\.   
**0\.0**: Cloth particles are unaffected\.   
**1\.0**: Physically correct angular velocity\. 

## Wind properties<a name="component-cloth-wind-properties"></a>

**Note**  
The component wind properties create wind that effects only the cloth referenced by the component\. To create wind that can effect multiple components across multiple entities, see [Create global or localized wind forces with PhysX](wind-provider.md)\. 

![\[Wind properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-F-1.27.png)

**Note**  
Wind is disabled when both the below **Air drag** and **Air lift** coefficients are **0\.0**\. 

**Enable local wind velocity**  
Enable to set a wind **Local velocity** for this cloth\. When disabled, the velocity from Physics::WindBus will be used\. 

**Local velocity**  
Wind vector \(direction and magnitude\) in world coordinates\. A greater magnitude applies a stronger wind force\.   
The wind **Local velocity** property is enabled by the **Enable local wind velocity** property\. 

**Air drag coefficient**  
Specifies how much drag air applies to the cloth particles\.

**Air lift coefficient**  
Specifies how much lift air applies to the cloth particles\.

**Air density**  
The density of air used for drag and lift calculations\.

## Collision properties<a name="component-cloth-collision-properties"></a>

![\[Collision properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-G-1.27.png)

**Friction**  
Controls the amount of friction between cloth particles and colliders\.   
**0\.0**: **Friction** disabled\. 

**Mass scale**  
Controls how quickly cloth particle mass is increased during collisions\.   
**0\.0**: **Mass scale** disabled\. 

**Continuous detection**  
Continuous collision detection improves collision by computing the time of impact between cloth particles and colliders\.   
The increase in quality can impact performance\. We recommend that you use **Continuous detection** only when necessary\. 

**Affects static cloth particles**  
Enable to allow colliders to move static cloth particles\. Static cloth particles have a **0\.0** inverse mass\. 

## Self Collision properties<a name="component-cloth-self-collision-properties"></a>

![\[Self collision properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-H-1.27.png)

**Distance**  
The minimum distance that the colliding cloth particles must maintain from each other in meters\.  
**0\.0**: **Self collision** disabled\. 

**Stiffness**  
Stiffness for the self collision constraints\.   
**0\.0**: **Self collision** disabled\. 

## Fabric stiffness properties<a name="component-cloth-fabric-stiffness-properties"></a>

![\[Fabric stiffness properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-I-1.27.png)

**Horizontal**  
Stiffness value for horizontal stretch and compression constraints\.   
**0\.0**: No horizontal stretch and compression constraints\. 

**Horizontal multiplier**  
Scale value for horizontal stretch and compression constraints\.   
**0\.0**: No horizontal stretch and compression constraints applied\.   
**1\.0**: Fully apply horizontal stretch and compression constraints\. 

**Vertical**  
Stiffness value for vertical stretch and compression constraints\.   
**0\.0**: No vertical stretch and compression constraints\. 

**Vertical multiplier**  
Scale value for vertical stretch and compression constraints\.   
**0\.0**: No horizontal stretch and compression constraints applied\.   
**1\.0**: Fully apply horizontal stretch and compression constraints\. 

**Bending**  
Stiffness value for bending constraints\. This value defines how easily a cloth folds on itself\.   
**0\.0**: No bending constraints\. 

**Bending multiplier**  
Scale value for bending constraints\.   
**0\.0**: No bending constraints applied\.   
**1\.0**: Fully apply bending constraints\. 

**Shearing**  
Stiffness value for shearing constraints\. This value defines how easily a cloth twists\.   
**0\.0**: No shearing constraints\. 

**Shearing multiplier**  
Scale value for shearing constraints\.   
**0\.0**: No shearing constraints applied\.   
**1\.0**: Fully apply shearing constraints\. 

## Fabric compression properties<a name="component-cloth-fabric-compression-properties"></a>

![\[Fabric Compression properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-J-1.27.png)

**Horizontal limit**  
Compression limit for horizontal constraints\. This property is affected by **Horizontal multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Horizontal compression disabled\. 

**Vertical limit**  
Compression limit for vertical constraints\. This property is affected by **Vertical multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Vertical compression disabled\. 

**Bending limit**  
Compression limit for bending constraints\. This property is affected by **Bending multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Bending compression disabled\. 

**Shearing limit**  
Compression limit for shearing constraints\. This property is affected by **Shearing multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Shearing compression disabled\. 

## Fabric stretch properties<a name="component-cloth-fabric-stretch-properties"></a>

**Note**  
For **Fabric stretch** properties, reduce **Stiffness** of **Tether constraints** or increase its **Scale** to allow cloth to stretch\. 

![\[Fabric stretch properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-K-1.27.png)

**Horizontal limit**  
Stretch limit for horizontal constraints\. This property is affected by **Horizontal multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Horizontal stretch disabled\. 

**Vertical limit**  
Stretch limit for vertical constraints\. This property is affected by **Vertical multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Vertical stretch disabled\. 

**Bending limit**  
Stretch limit for bending constraints\. This property is affected by **Bending multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Bending stretch disabled\. 

**Shearing limit**  
Stretch limit for shearing constraints\. This property is affected by **Shearing multiplier** in the **Fabric stiffness** property group\.   
**0\.0**: Shearing stretch disabled\. 

## Tether constraints properties<a name="component-cloth-tether-constraints-properties"></a>

![\[Tether constraints properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-L-1.27.png)

**Stiffness**  
Stiffness for tether constraints\.   
**0\.0**: Tether constraints disabled\.   
**1\.0**: Tether constraints behave like springs\. 

**Scale**  
Scale factor for tether constraint **Stiffness** 

## Quality properties<a name="component-cloth-quality-properties"></a>

![\[Quality properties of the Cloth component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/cloth/ui-cloth-component-M-1.27.png)

**Solver frequency**  
Target solver iterations per second\. The executed number of iterations per second may vary dependent on many performance factors\. However, at least one iteration per frame is solved regardless of the value set\. 

**Acceleration filter iterations**  
Number of iterations to average the delta time factor used for gravity and external acceleration\. 

**Remove static triangles**  
Enable to remove triangles composed of static cloth particles\. Enabling this property improves performance, however the removed static cloth particles will not be present for collision and self collision calculations\. 