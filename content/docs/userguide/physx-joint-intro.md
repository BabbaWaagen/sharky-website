# Dynamic joints with PhysX<a name="physx-joint-intro"></a>

PhysX joint components constrain the position and orientation of one PhysX rigid body called the *follower*, relative to another PhysX rigid body, called the *leader*\. The leader rigid body will have rotational freedom in zero, one, or two axes around the joint, depending on the type of PhysX joint\. 

The example image below is a simple demonstration of the three joint types\. In each example, the blue sphere is the follower rigid body\. The joints are centered on their respective follower rigid bodies\. The red sphere is the leader rigid body\. For clarity, the ball joint and hinge joint follower rigid bodies are set to fixed positions, but they can be dynamic rigid bodies like the fixed joint example\. Also note that the joints can be offset from the follower rigid body using the **Local Position** and **Local Rotation** properties of the joint component\. 

![\[PhysX Joints example\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/anim-joints-example.gif)

**Contents**
+ [PhysX joint types](#physx-joint-types)
+ [PhysX joint setup](#physx-joint-setup)
+ [PhysX Joint configuration](#physx-joint-config)
  + [Position mode](#joint-position)
  + [Rotation mode](#joint-rotation)
  + [Snap position mode](#joint-snap-position)
  + [Snap rotation mode](#joint-snap-rotation)
  + [Maximum Force and Maximum Torque modes](#joint-breakable-properties)
  + [Swing limits mode](#joint-swing-limit)
  + [Twist limits mode](#joint-twist-limit)
  + [Stiffness and Damping modes](#joint-soft-limit-properties)
+ [Notes on stability](#joint-stability)

## PhysX joint types<a name="physx-joint-types"></a>

See the linked component reference below for information on the three PhysX joint types:
+ [ PhysX Ball Joint component reference ](component-physx-ball-joint.md) \- The **PhysX Ball Joint** component allows freedom of rotation of the leader rigid body in two axes\. 
+ [ PhysX Fixed Joint component reference ](component-physx-fixed-joint.md) \- The **PhysX Fixed Joint** component does not allow freedom of rotation of the leader rigid body in any axis\. 
+ [ PhysX Hinge Joint component reference ](component-physx-hinge-joint.md) \- The **PhysX Hinge Joint** component allows freedom of rotation of the leader rigid body in one axis\. 

## PhysX joint setup<a name="physx-joint-setup"></a>

The setup for each joint type is the same\. 

**To set up a PhysX joint**

1. Create an entity for the joint and the follower rigid body\. 

   1. Create a new entity\. Right click in **Perspective** and choose **Create enity** from the context menu\.

   1. Add a **PhysX Rigid Body** component to the entity\. 

   1. Add a **PhysX Collider** component to the entity\. This is required for angle limits to work correctly\. Joints still work without a PhysX Collider component but angle limits and might not be enforced\. This is also true when using trigger colliders\. 

   1.  Add one of the PhysX joint components: 
      + **PhysX Ball Joint** 
      + **PhysX Fixed Joint** 
      + **PhysX Hinge Joint** 

   1. The joint's position and orientation are expressed as an offset from the follower\. Adjust the position and orientation of the joint by changing the **Local Position** and **Local Rotation** fields in the PhysX joint component\. 

1. Create an entity for the leader rigid body\. 

   1. Create a new entity\. 

   1. Add a **PhysX Rigid Body** component to the entity\. 

   1. Add a **PhysX Collider** component to the entity\. 

1. Assign the leader entity to the **Lead Entity** property of the PhysX joint\. 

   1. In the Joint component, click the **Target** button to the right of the **Lead Entity** property to start entity selection\. 

   1. In **Perspective**, click on the leader entity to select it and assign it to the **Lead Entity** property\. 

## PhysX Joint configuration<a name="physx-joint-config"></a>

Joint components have an **Edit** button that enables component edit mode\. In component edit mode, you can edit the properties of the joint in **Perspective**\. You can use one of several edit contexts in component edit mode\. Press the **Tab** key to cycle through the edit mode contexts\. The current context is displayed at the bottom of the **Perspective** pane\. 

### Position mode<a name="joint-position"></a>

**Applies to:** All Joints 

![\[PhysX joint position mode\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-position-mode-1.27.png)

Position mode displays a translate gizmo that you can click and drag to adjust the **Local Position** of the joint relative to the entity transform\. 

### Rotation mode<a name="joint-rotation"></a>

**Applies to:** All Joints 

![\[PhysX joint rotation mode\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-rotation-mode-1.27.png)

Rotation mode displays a rotation gizmo that you can click and drag on any axis to adjust the **Local Rotation** of the joint relative to the entity transform\. 

### Snap position mode<a name="joint-snap-position"></a>

**Applies to:** Ball Joint and Hinge Joint 

![\[PhysX joint snap position mode\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-snap-position-mode-1.27.png)

Snap position mode displays a highlight bounding box and target when you hover over an entity\. Click the entity to snap the joint **Local Position** to the highlighted entity's position\. If **Select Lead on Snap** is enabled in the joint properties, the entity will be assigned to the joint's **Lead Entity** property\. Any entity can be selected except the follower entity\. 

### Snap rotation mode<a name="joint-snap-rotation"></a>

**Applies to:** Ball Joint 

![\[PhysX joint snap rotation mode\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-snap-rotation-mode-1.27.png)

Snap rotation mode displays a highlight bounding box and target when you hover over an entity\. Click the entity to snap the joint **Local Rotation** to the highlighted entity's rotation\. Any entity can be selected except the leader entity\. 

### Maximum Force and Maximum Torque modes<a name="joint-breakable-properties"></a>

**Applies to:** All Joints 

![\[PhysX joint maximum force and maximum torque modes\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-breakable-properties-mode-1.27.png)

Maximum force and maximum torque modes display a gray box that you can click and drag to adjust the **Maximum Force** and **Maximum Torque** properties\. The maximum force and maximum torque modes and properties are available only when the **Breakable** property is enabled for the joint\. 

### Swing limits mode<a name="joint-swing-limit"></a>

**Applies to:** Ball Joint 

![\[PhysX joint swing limits mode\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-swing-limit-mode-1.27.png)

Swing limits mode displays a ring gizmo at the local root of the joint that you can use to rotate the swing limits on the joint's x\-axis, and a scale gizmo that you can use to scale the swing limits uniformly or non\-uniformly on the joint's y\- and z\-axes\. Swing limits mode is available only when the **Limits** property is enabled for the ball joint component\. 

### Twist limits mode<a name="joint-twist-limit"></a>

**Applies to:** Hinge Joint 

![\[PhysX joint twist limits mode\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-twist-limit-mode-1.27.png)

Twist limits mode displays two ring gizmos that you can click and drag to adjust the **Positive angular limit** and **Negative angular limit** properties\. The red ring adjusts the positive limit and the green ring adjusts the negative limit\. Twist limits mode is available only when the **Limits** property is enabled for the hinge joint component\. 

### Stiffness and Damping modes<a name="joint-soft-limit-properties"></a>

**Applies to:** Ball Joint and Hinge Joint 

![\[PhysX joint stiffness and damping modes\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/physx/ui-physx-joint-soft-limit-properties-mode-1.27.png)

Stiffness and damping modes display a gray box that you can click and drag to adjust the **Stiffness** and **Damping** properties\. The stiffness and damping modes and properties are available only when the **Soft limit** property is enabled for the joint\. 

## Notes on stability<a name="joint-stability"></a>

The iterative solver used by PhysX joints may not be able to maintain constraints in some configurations\. For example, the solver might fail to converge\. The result is unstable or unexpected motion during simulation\. The PhysX documentation describes configurations that could help avoid such occurrences\. Please see [Configuring Joints for Best Behavior](https://docs.nvidia.com/gameworks/content/gameworkslibrary/physx/guide/Manual/Joints.html) in NVIDIA's PhysX Joint documentation\. 