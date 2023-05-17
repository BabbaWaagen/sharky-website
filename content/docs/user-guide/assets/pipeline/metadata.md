---
linkTitle: Moving/Renaming Assets
title: Moving/Renaming Assets
description: In Open 3D Engine (O3DE), files can be moved and renamed freely without breaking existing references by storing a UUID in a side-car file (.meta).
weight: 600
toc: true
---

Moving/renaming files freely without breaking existing references is possible through the experimental metadata feature which stores a UUID in a side-car file (.meta).  See the [Asset Metadata Relocation RFC](https://github.com/o3de/sig-content/blob/main/rfcs/rfc-77-metadata-asset-relocation.md) for technical details on how the system works

By default, the metadata system is disabled because not all file types can be relocated without issue currently.  Each asset file type must be enabled individually in the settings.  Once an asset file type is enabled, the Asset Processor will generate a metadata file for every file of the given type on startup.  Any file which has a metadata associated with it can then be moved or renamed.  The Asset Processor does not need to be running when moving or renaming files and there are no special tools required to do so.

Example metadata file:
```json
{
    "FileVersion": 1,
    "UUID": {
        "uuid": "{931ADFA6-0578-4932-9C39-EA4A921A30DE}",
        "legacyUuids": [
            "{2336F175-E6FD-5A11-87B4-04B00088CADD}",
            "{45F2B574-8C8B-5D2B-8833-E99CEBD18F14}"
        ],
        "originalPath": "ScriptCanvas/ForceDebug.scriptcanvas",
        "creationUnixEpochMS": 1679507888552,
        "__version": 0
    }
}
```
Example of metadata files in a source directory:

![Metadata files in directory](/images/user-guide/assets/pipeline/metadata.png)

## How to Enable
To enable metadata generation for a set of file types, create a .setreg file (`<project or gem directory>/Registry` is suggested) with the following settings:
```json
{
    "O3DE":
    {
        "AssetProcessor":
        {
            "Settings":
            {
                "Metadata":
                {
                    "EnabledTypes": [
                    ]
                }
            }
        }
    }
}
```
EnabledTypes is simply an array of strings of file extension to enable.  For example, `".txt", ".png"`

It is highly recommended that this setreg file be placed in a central location, which is shared with other users of the project, to ensure everyone is generating the same metadata files.  For a game project, it should be placed in the project directory; for gem development, it should be placed in the gem directory.  Keep in mind this is an Asset Processor (AP) wide setting, it will apply to all files the AP processes, not just the ones in the project or gem where the setting exists.

Once a metadata file is generated for an asset and the asset is relocated or any references are saved using the newly generated UUID, the metadata file must be kept alongside the asset.  Not doing so could break references to the file.

> AssetProcessor will continue to use existing metadata files for assets which have them, regardless of the above settings.

## How to use
Moving or renaming assets can be done either in the editor via the asset browser or using any file management tool of your choosing, such as the File Explorer in Windows.

There is only one requirement when moving or renaming an asset, which is **the metadata file must be moved or renamed as well**.

Folders can be moved or renamed without having to touch metadata files, but all files within a folder **must have a metadata file** to ensure existing references do not break.

Examples:

* If blue.png is renamed to red.png, the metadata file blue.png.meta must be renamed to red.png.meta.
* If textures/hat.png is moved to character/hat.png, the metadata file must be moved to character/hat.png.meta.

If using source control, metadata files **must be checked in** along with the source asset and updated to match any move or rename changes to those assets.

There is one exception to the above, which is Intermediate Asset metadata files.  These metadata files follow the same rules as Intermediate Assets: they should not be modified or checked into source control.

When relocating an asset, the asset's ID will remain stable, so existing references will continue to work.  Assets are typically referenced using the `Asset<T>` type which includes an asset hint, which is a human readable string containing the last known location of the referenced file.  If a file is moved or renamed, the next time a file referencing it is saved, this may show up as a change which wasn't expected.  For example: File1.ext references File2.ext, and stores the asset reference to File2.ext. This contains both the asset ID, and the human readable asset hint that contains the file name File2.ext. When File2.ext is renamed to FileB.ext, the asset ID will remain the same. The next time File1.ext is saved, the data will change because the asset hint has changed.

## Renaming while Asset Processor is running

By default, renaming assets manually while Asset Processor is running can prove difficult as AP will try to immediately create a new metadata file for the renamed asset.  To prevent this, AP can be configured to wait for a specified time before it attempts to process a "new" asset, which avoids the automatic creation of an unwanted, new metadata file.  

> This delay will affect all newly created assets for metadata-enabled types and is off by default.  The longer the delay time, the longer it will take AP to start processing any newly created metadata-enabled file type.

In a .setreg file, add the following setting:

```json
{
    "O3DE":
    {
        "AssetProcessor":
        {
            "Settings":
            {
                "Metadata":
                {
                    "MetaCreationDelayMs": 5000
                }
            }
        }
    }
}
```
The value specified is the milliseconds to wait.  The above example config will wait 5 seconds before processing an asset.  

>  This setting can be user-specific and does not need to be shared across users if not desired.

This setting is mainly useful to help allow manual renaming of assets, but can help in some situations of slow file updates on disk, such as copying a large number of files or fetching latest from source control.  These operations can sometimes be ordered in a way that requires a very high delay setting, such as a Git LFS fetch, which may fetch files in groups by type, possibly resulting in metadata files being created on disk long after the source asset was created.  In these situations, it is recommended to close AP first to avoid conflicts caused by AP creating metadata files which already exist in source control.

## Asset Processor Batch
Since Asset Processor Batch is intended for use with automated processes, it will not create metadata files and will not use the meta creation delay, regardless of what settings are configured.  It will make use of any existing metadata files however.

## Limitations
Metadata relocation currently only supports UUID-based references.  That means references from code (C++, Lua, AZSL, etc) which typically reference files by path will break when a file is moved or renamed and will need to be updated through some other means.  This also applies in the case of a file type being enabled when there are still other files which may reference it by path.

As this feature is still experimental, see the [engine contributors documentation](../../../../engine-dev/assets/metadata) for more information on the current state of file type support.