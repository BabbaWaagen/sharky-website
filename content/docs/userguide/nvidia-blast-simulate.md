# Simulate destruction with NVIDIA Blast<a name="nvidia-blast-simulate"></a>


****  

|  | 
| --- |
| This feature is an [experimental](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#experimental) release and is subject to change\.  | 

To use NVIDIA Blast assets in Lumberyard, create an entity, add a **Blast Family** component, add a **Blast Family Mesh Data** component, and then assign the blast assets to the components\. 

**Note**  
To quickly test NIVIDIA Blast simulation, the following steps assume that the assets have been exported from Houdini with **Static root** disabled in the **Blast Export** SOP\. With **Static root** disabled, the NVIDIA Blast asset is dynamic, and destruction can be triggered by dropping the entity on a PhysX collision surface such as **PhysX Terrain**\. If **Static root** is enabled, the root asset is static, and destruction must be triggered by an external force, such as a projectile impact\.   
For more information, see [Create assets for NVIDIA Blast](nvidia-blast-create-blast-asset.md)\. 

**Contents**
+ [Create an entity for NVIDIA Blast](#nvidia-blast-create-entity)
+ [Add automatically processed mesh assets to a NVIDIA Blast entity](#nvidia-blast-entity-automatic-assets)
+ [Add manually created mesh assets to a NVIDIA Blast entity](#nvidia-blast-entity-manual-assets)
+ [Test NVIDIA Blast destruction simulation](#nvidia-blast-simulate-destruction)

## Create an entity for NVIDIA Blast<a name="nvidia-blast-create-entity"></a>

When you create an entity, you add the NVIDIA Blast functionality and define how the asset destructs\.

**To create an entity for NVIDIA Blast**

1. Ensure that the terrain has a **PhysX Terrain** level component\. In **Level inspector**, choose **Add Component** and select **PhysX Terrain** from the component list\. 

1. Create a new entity\. Right\-click in **Perspective** and choose **Create entity** from the context menu\. 

1. Add a **Blast Family** component to the entity\. In **Entity Inspector**, choose **Add Component** and select **Blast Family** from the component list\. The **Blast Family** component adds NVIDIA Blast functionality to the entity\. For more information, see [Blast Family component](component-blast-family.md)\. 

1. Set the **Blast asset** for the **Blast Family** component\. Click the **Folder** button to the right of the **Blast asset** property and choose the `.blast` asset in the Blast Asset selection window\.   
![\[Add the .blast asset to the Blast Family component.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/blast/ui-blast-add-blast-asset-1.27.png)

1. Set the **Blast Material** for the **Blast Family** component\. Blast materials define how much damage various forces cause to the bonds holding the fractured asset together, and how much damage is required to cause destruction\. For more information see [Specify destruction properties with Blast materials](nvidia-blast-materials.md)\. 

1. Add a **Blast Family Mesh Data** component to the entity\. In **Entity Inspector**, Choose **Add Component** and select **Blast Family Mesh Data** from the component list\. The **Blast Family Mesh Data** component adds NVIDIA Blast meshes to the entity\. For more information, see [Blast Family Mesh Data component](component-blast-family-mesh-data.md)\. 

If you have processed your mesh assets with **Python Asset Builder**, follow the steps in the section: [Add automatically processed mesh assets to a NVIDIA Blast entity](#nvidia-blast-entity-automatic-assets)\. 

If you have manually edited your mesh assets with **FBX Settings**, follow the steps in the section: [Add manually created mesh assets to a NVIDIA Blast entity](#nvidia-blast-entity-manual-assets)\. 

## Add automatically processed mesh assets to a NVIDIA Blast entity<a name="nvidia-blast-entity-automatic-assets"></a>

**Python Asset Builder** creates a `blast_slice` asset when it processes your NVIDIA Blast assets\. The blast slice automatically adds the mesh assets and material to the **Blast Family Mesh Data **component\.

**To add automatically processed mesh assets**

1. In the **Blast Family Mesh Data** component, set a material for the Blast mesh\. Click the **Folder** button to the right of the **Material** property and select a material from the material selection window\. 

1. In the **Blast Family Mesh Data** component, set the **Blast Slice** property\. Click the **Folder** button to the right of the **Blast Slice** property and select the asset from the Blast Slice selection window\. 

   Enable the **Show mesh assets** property if you would like to view the mesh list\.   
![\[Add the blast slice asset to the Blast Family Mesh Data component.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/blast/ui-blast-add-blast-mesh-data-1.27.png)

1. The entity is now set up to simulate destruction\. Continue to the section: [Test NVIDIA Blast destruction simulation](#nvidia-blast-simulate-destruction)\. 

## Add manually created mesh assets to a NVIDIA Blast entity<a name="nvidia-blast-entity-manual-assets"></a>

If your NVIDIA Blast mesh assets have been manually edited in **FBX Settings**, use the following steps to add the mesh assets to the entity\. 

**To add manually processed assets**

1. In the **Blast Family Mesh Data** component, set a material for the Blast mesh\. Click the **Folder** button to the right of the **Material** property and select a material from the material selection window\. 

1. In the **Blast family mesh data** component, enable the **Show mesh assets** property to show the mesh asset list\. 

1. Add a mesh slot to the list\. Choose the **\+** button to the right of **Mesh assets** to add a mesh slot to the **Mesh assets** list\. 

1. Add a mesh to the list\. Click the **Folder** button to the right of the numbered mesh slot property and select a mesh asset from the **Static Mesh** selection window\. 

1. Repeat steps **3** and **4** until all of the meshes for the blast asset have been added to the **Blast family mesh data** component\.   
![\[Add mesh assets manually to the Blast Family Mesh Data component.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/blast/ui-blast-family-mesh-data-add-mesh-1.27.png)

1. The entity is now set up to simulate destruction\. Continue to the section: [Test NVIDIA Blast destruction simulation](#nvidia-blast-simulate-destruction)\. 

## Test NVIDIA Blast destruction simulation<a name="nvidia-blast-simulate-destruction"></a>

Because the blast asset has been exported from Houdini with **Static root** disabled, and a **PhysX Terrain** level component has been added to the level, destruction can be tested by dropping the object on the terrain\. 

**To test the destruction simulation**

1. With the entity selected, press the **2** key to enable the move tool\. 

1. Click and drag on the **Z** axis of the move gizmo to move the entity several units above the terrain\. 

1.  Press **Control \+ P** to view simulation\. The entity drops and shatters when it collides with the terrain\. 

1.  Press **Control \+ P** to end the simulation\. 

![\[Add the blast slice asset to the Blast Family Mesh Data component.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/blast/anim-nvidia-blast-view-simulation.gif)