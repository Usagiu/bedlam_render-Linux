# Unreal Import Scripts
The various scripts in this folder help with automating BEDLAM related data import into Unreal.

# Requirements
+ Unreal Engine 5.0.3 with active [Python Editor Script Plugin](https://docs.unrealengine.com/5.0/en-US/scripting-the-unreal-editor-using-python/)
+ Python for Linux (3.10.2 or later)
+ Blank Unreal project with active Python Editor Script Plugin (Sandbox5) <-- In UE5 project create interface. You can click (FILM/ VIDEO & LIVE EVENTS) to create this.
+ In the following "/Engine" mean UE5 File(Linux_Unreal...../Engine) not your project "/Engine","/Game" mean your project path(/data/demoProject === /Game in UE5)
# Scripts

## Animated SMPL-X bodies
+ [import_abc_smplx.py](import_abc_smplx.py) <-- If don't download all animation. use this one.
+ [import_abc_smplx_batch.py](import_abc_smplx_batch.py) <-- This's for batch processing data
+ Use this script to import SMPL-X Alembic ABC files as `GeometryCache`
+ Usage
    + Adjust data paths at top of `import_abc_smplx.py` and `import_abc_smplx.py` scripts(YourABCFilePath, Example: /data/rp_aaron_posed_002)
    + Then copy `import_abc_smplx.py` path, Click the CMD button at the UE5 bottom to switch to Python. Paste the path to Run Script.
    + ↓↓↓↓↓↓↓↓ The following is batch processing, if you are just doing a demo, please ignore it.
    + Adjust data paths at top of `import_abc_smplx_batch.py` and `import_abc_smplx.py` scripts  <-- This's for batch processing data
    + Run multiprocess batch import from Windows command prompt. The example below uses 10 simultaneous Unreal Engine instances for data import of 1000 data batches. Depending on your available CPU core count and available main memory (128GB+ recommended) you can increase or need to decrease the amount of processes. For fastest processing of BEDLAM release data make sure that you have a fast SSD with large enough space (700GB).
        + `py -3 import_abc_smplx_batch.py 1000 10`

## Simulated animated clothing
+ [import_abc_clothing.py](import_abc_clothing.py) <-- If don't download all clothing. use this one.
+ [import_abc_clothing_batch.py](import_abc_clothing_batch.py) <-- This's for batch processing data
+ Use this script to import simulated 3D clothing files in Alembic ABC format as `Geometry Cache`
+ Usage
    + Adjust data paths at top of `import_abc_clothing.py` and `import_abc_clothing.py` scripts(YourABCFilePath, Example: /data/rp_aaron_posed_002)
    + Make sure your .abc asset and clothing asset from the folder of the same name. because abc and clothing have a one-to-one correspondence.(example: The abc generated with "rp_aaron_posed_002" under folder animationFolder must import the clothes of "rp_aaron_posed_002" under folder clothingFolder)
    + Then copy `import_abc_clothing.py` path, Click the "CMD" button at the UE5 bottom to switch to "Python". Paste the path to Run Script.
    + ↓↓↓↓↓↓↓↓ The following is batch processing, if you are just doing a demo, please ignore it.
    + Adjust data paths at top of `import_abc_clothing_batch.py` and `import_abc_clothing.py` scripts
    + Run multiprocess batch import from Windows command prompt. The example below uses 10 simultaneous Unreal Engine instances for data import of 1000 data batches. Depending on your available CPU core count and available main memory (128GB+ recommended) you can increase or need to decrease the amount of processes. For fastest processing of BEDLAM release data make sure that you have a fast SSD with large enough space (1.4TB).
        + `py -3 import_abc_clothing_batch.py 1000 10`

## Body textures
+ [create_body_materials.py](create_body_materials.py)
+ Use this script to generate required `MaterialInstance` materials for imported BEDLAM body textures
+ Requirements
    + BEDLAM Unreal Core assets installed under your UE5 install directory. See [Unreal render README](../render/README.md) for instructions.(It'e mean Copy Core file to "/Engine/PS/Bedlam")
    + Imported BEDLAM body textures
        + Download `bedlam_body_textures_meshcapade.zip` from BEDLAM website and extract to local folder and remove `previews` subfolders
        + Load Unreal Editor project(It'e mean enter your project)
        + Make sure that "Show Engine Content" is activated in Content Browser settings so that you see the `Engine` folder hierarchy(It's mean click the "Content Drawer" button at the UE5 bottom, then click the pop up page top right setting button,check the "Show Engine Content")
        + Create `Engine/Content/PS/Meshcapade/SMPL` folder via Content Browser
        + Import local `MC_textures_skintones` body texture folder via Content Browser to `Engine/Content/PS/Meshcapade/SMPL`(If you can, you can drag the `MC_textures_skintones` folder to here)
        + Content Browser>Save All

+ Usage
    + Select all imported body textures under `Engine/Content/PS/Meshcapade/SMPL` in Content Browser (Filter:Texture, CTRL-A)
    + Run script via Execute Python Script
    + Content Browser>Save All

## Clothing textures
+ [import_clothing_textures.py](import_clothing_textures.py)
+ Use this script to import downloaded BEDLAM 3D clothing textures and generate required `MaterialInstance` materials for them
+ Requirements:
    + BEDLAM Unreal Core assets installed under your UE5 install directory
        + Example: `C:\UE_5.0\Engine\Content\PS\Bedlam\Core`
+ Usage
    + Adjust data paths at top of script
    + Run script via Execute Python Script

## HDR images
+ [import_hdr.py](import_hdr.py)
+ Use this script to import panoramic high-dynamic range images in HDR format for image-based lighting
    + Not needed for existing 3D environments from Unreal Marketplace
+ [List of used BEDLAM HDR images](../../config/whitelist_hdri.txt)
    + HDR Source: https://polyhaven.com/hdris
    + 4K HDR version (4096x2048)
+ Usage
    + Download desired 4K HDRI images in HDR format
    + Remove file resolution suffix from the filenames (`abandoned_church_4k.hdr` => `abandoned_church.hdr`)
        + `rename` is your friend and helper here.
    + Adjust data paths at top of script
    + Run script via Execute Python Script
    + After import disable Mipmaps for all imported HDR images
        + Bulk Edit via Property Matrix
            + LevelOfDetail>Mip Gen Settings>NoMipmaps
