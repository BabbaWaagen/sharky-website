---
title: Multiplayer Autocomponents
description: A reference for defining Open 3D Engine multiplayer state through autocomponents.
linktitle: Autocomponents
---

*Autocomponents* provide a convenient way to define states of a multiplayer component relevant to network synchronization. Using the [AzAutoGen](/docs/user-guide/engine/autogen) system, autocomponent files found inside of your project are processed during builds to create C++ classes for components and controllers that provide network replication and remote function calls. Autocomponents also take care of Editor and behavior context bindings so that the bound component shows in the Editor and works with O3DE scripting.

In order to enable autocomponent builds for your project, follow the instructions in [Multiplayer Project Configuration](./configuration).

## Autocomponent file structure

Autocomponents are defined in XML files, placed in the `Code\Source\Autogen` directory of the Multiplayer Gem.

### Component attributes

The `Component` tag defines the name, namespace, include path, and override behavior for the multiplayer component being described.

| Property | Description | Type |
|---|---|---|---|
| Name | The class name of the generated autocomponent. | `string`: Must be a valid C++ class name. |
| Namespace | The namespace the generated autocomponent will be placed within. For a given Gem, all defined autocomponents must be defined within the same namespace. Mixing namespaces inside a Gem will result in compiler errors. | `string`: Must be a valid C++ namespace name. |
| OverrideComponent | If `true`, the generated component will be a base class and the developer implementing the multiplayer component will be responsible for supplying the final derived component used in the editor and at runtime. | `bool` |
| OverrideController | If `true`, the generated controller will be a base class, and the developer implementing the multiplayer component will be responsible for supplying the final derived controller used in the runtime. | `bool` |
| OverrideInclude | If either `OverrideComponent` or `OverrideController` are `true`, this value is **required** and must be the path (relative to the Gem root) of the header containing the concrete implementations. | the developer implementing the final component or controller classes must provide the class header the final classes are declared within. | `string` |

### ComponentRelation

A component relation (the `ComponentRelation` tag) describes how various components may be related to the component being described. 

| Property | Description | Type |
|---|---|---|---|
| Name | The name of the related component. | `string`: Must be a valid C++ class name. |
| Namespace | The namespace the related component is declared within. | `string`: Must be a valid C++ namespace. |
| Include | The include path of the related component. | `string` |
| Constraint | The type of relation this entry has with the component being described. The allowed values are: | `Required`, `Weak`, `Incompatible` |
| | **Required**: The related component must be present on the entity. These components are displayed in the Editor as a hard requirement for adding this autocomponent. |
| | **Weak**: The related component isn't required, but will be activated on the entity (if present) before this autocomponent. | |
| | **Incompatible**: The related component isn't compatible with this autocomponent. Attempting to place both components on an entity will result in an error. | |
| HasController | If `true`, the related component must have a multiplayer controller associated with it. Setting this value to true will cause controller accessors to be generated on the controller being described. | `bool` |

For components which have a relation constraint of `Required` or `Weak`, accessors are generated on the autocomponent with the name `Get<ComponentName>()`. These accessors return a cached pointer to the related component, created on entity activation.

### Include

The `Include` tag is used to generate the `#includes` of the C++ code. Use an `Include` tag for each header that your generated classes will use.

| Property | Description | Type |
| File | The path to a header to add as an `#include` of the generated source. | `string` |

{{< todo issue="https://github.com/o3de/o3de.org/issues/678" >}}
Document the following parts of autocomponents:
* NetworkInput
* NetworkProperty
* ArchetypeProperty
* RemoteProcedure
{{< /todo >}}

### Example

The following is an example of an autocomponent which synchronizes a component representing weapon state across a multiplayer session.

```xml
<?xml version="1.0"?>
 
<Component
    Name="NetworkWeaponsComponent"
    Namespace="MultiplayerSample"
    OverrideComponent="true"
    OverrideController="true"
    OverrideInclude="Source/Components/NetworkWeaponsComponent.h"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <ComponentRelation Constraint="Required" HasController="true" Name="NetworkAnimationComponent" Namespace="MultiplayerSample" Include="Source/Components/NetworkAnimationComponent.h" />
 
    <Include File="Source/Weapons/WeaponTypes.h" />
 
    <NetworkInput Type="bool" Name="Draw" Init="false" />
    <NetworkInput Type="WeaponActivationBitset" Name="Firing"  Init="" />
 
    <NetworkProperty Type="AZ::Vector3"  Name="TargetPosition"   Init="AZ::Vector3::CreateZero()" Container="Object"       ReplicateFrom="Authority" ReplicateTo="Client"     IsPublic="false" IsRewindable="false" IsPredictable="false" ExposeToEditor="false" GenerateEventBindings="false" Description="Target position the weapons component is currently aiming at" />
    <NetworkProperty Type="FireParams"   Name="ActivationParams" Init=""  Container="Array" Count="MaxWeaponsPerComponent" ReplicateFrom="Authority" ReplicateTo="Client"     IsPublic="false" IsRewindable="false" IsPredictable="false" ExposeToEditor="false" GenerateEventBindings="false" Description="Parameters for the current weapon activation" />
    <NetworkProperty Type="uint8_t"      Name="ActivationCounts" Init="0" Container="Array" Count="MaxWeaponsPerComponent" ReplicateFrom="Authority" ReplicateTo="Client"     IsPublic="false" IsRewindable="false" IsPredictable="false" ExposeToEditor="false" GenerateEventBindings="false" Description="The number of activations" />
    <NetworkProperty Type="WeaponState"  Name="WeaponStates"     Init=""  Container="Array" Count="MaxWeaponsPerComponent" ReplicateFrom="Authority" ReplicateTo="Autonomous" IsPublic="false" IsRewindable="false" IsPredictable="true"  ExposeToEditor="false" GenerateEventBindings="false" Description="The predictable states of the weapons" />
 
    <ArchetypeProperty Type="WeaponParams" Name="WeaponParams"  Init=""           Container="Array" Count="MaxWeaponsPerComponent" ExposeToEditor="true" Description="Parameters for the weapons attached to this NetworkWeaponsComponent" />
    <ArchetypeProperty Type="AZ::Name"     Name="FireBoneNames" Init="AZ::Name()" Container="Array" Count="MaxWeaponsPerComponent" ExposeToEditor="true" Description="Name of the bone to attach to for fire events" />
 
    <RemoteProcedure Name="SendConfirmHit" InvokeFrom="Authority" HandleOn="Client" IsPublic="false" IsReliable="false" GenerateEventBindings="false" Description="Single hit event confirmed by the server" >
        <Param Type="WeaponIndex" Name="WeaponIndex" />
        <Param Type="HitEvent"    Name="HitEvent" />
    </RemoteProcedure>
 
    <RemoteProcedure Name="SendConfirmProjectileHit" InvokeFrom="Authority" HandleOn="Client" IsPublic="false" IsReliable="false" GenerateEventBindings="false" Description="Fired by projectile entities on confirmed hit" >
        <Param Type="WeaponIndex" Name="WeaponIndex" />
        <Param Type="HitEvent"    Name="HitEvent" />
    </RemoteProcedure>
</Component>
```
