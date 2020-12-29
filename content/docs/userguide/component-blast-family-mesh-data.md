# Blast Family Mesh Data component<a name="component-blast-family-mesh-data"></a>


****  

|  | 
| --- |
| This feature is an [experimental](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#experimental) release and is subject to change\.  | 

With the **Blast Family Mesh Data** component, you can set the mesh and material assets for NVIDIA Blast entities\. The **Blast Family Mesh Data** component is used with the **Blast Family** component\. This topic describes the properties of the **Blast Family Mesh Data** component\. 

The **Blast Family Mesh Data** component is provided by the [NVIDIA Blast gem](nvidia-blast.md)\. 

For information on using the **Blast Family Mesh Data** component see [Simulated destruction with NVIDIA Blast](nvidia-blast-intro.md)\. 

## Blast Family Mesh Data component properties<a name="component-blast-family-mesh-data-properties"></a>

![\[Properties of the Blast Family Mesh Data component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx/blast/ui-blast-family-mesh-data-component-1.27.png)

**Show mesh assets**  
When enabled, you can manually add mesh assets to this **Blast Family Mesh Data** component\.  
The **Show mesh assets** property exposes the **Mesh assets** list\. Choose the **\+** button to the right of **Mesh assets** to add a list entry\. Choose the **Folder** button to select a mesh for the list entry\. 

**Material**  
The material that supplies the visual appearance for the meshes in this **Blast Family Mesh Data** component\. 

**Blast Slice**  
A blast slice for this **Blast Family Mesh Data** component\. Blast slices are generated when blast assets are processed by the Python asset builder for NVIDIA Blast\. A blast slice will automatically add the mesh assets and material to the **Blast Family Mesh Data** component\. 