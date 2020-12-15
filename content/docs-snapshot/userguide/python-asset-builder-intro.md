# Process custom assets with Python Asset Builder<a name="python-asset-builder-intro"></a>

 With Python Asset Builder, you can create Python scripts that process custom assets produced from content creation tools such as Maya and Houdini, or any content tool with a known file format\. 

To use Python Asset Builder you must enable the [Python Asset Builder gem](python-asset-builder.md)\. 

## Python Asset Builder terms<a name="python-asset-builder-terms"></a>

The input and output files for a Python Asset Builder are both assets of some type\. This documentation uses the following terms to distinguish between the input and output of **Python Asset Builder**\. 

**Source asset file**  
An input asset file, such as an asset produced by a content creation tool, that will be processed by **Asset Processor** to generate a *product asset file*, source dependencies, and build dependencies\. 

**Product asset file**  
An output asset file produced by Python Asset Builder that can be consumed by a game launcher or Lumberyard Editor\. 

## Writing a Python Asset Builder<a name="python-asset-builder-overview"></a>

There are four steps to create a Python Asset Builder: 
+ [Create or modify a bootstrap script](python-asset-builder-bootstrap.md) \- Add a new Python Asset Builder script to a bootstrap location\. 
+ [Register a Python Asset Builder](python-asset-builder-register.md) \- Add logic to the Python Asset Builder that registers an asset builder pattern and handlers for job creation and processing\. 
+ [Create jobs with Python Asset Builder](python-asset-builder-create-job.md) \- Define logic in the callback method for `CreateJobs` that responds with the job description to process source asset files\. 
+ [Process job with Python Asset Builder](python-asset-builder-process-job.md) \- Define logic for `ProcessJob` to generate product asset files and dependencies\. 