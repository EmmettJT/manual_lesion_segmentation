# Manual Segmentation of Lesions Using Slice Histology

This repository provides guidance for performing **manual segmentation of lesions** using slice histology.

## Installation

First, install [BrainGlobe-Segment](https://github.com/brainglobe/brainglobe-segmentation), the tool used for manual segmentation

Next clone this repo (or at least download the reference allen atlas data) 

## Manual Segmentation

The goal is to manually draw the extent of the lesion.  
You will work with 2D histology slices, projecting them onto a 3D brain stack. It is important to ensure that your drawing accurately captures both:

- The **Z-position** of the slice within the 3D stack.
- The **extent** of the lesion.

This process can be challenging because slices are sometimes cut at a slightly different angle compared to the Allen atlas 3D reference stack.  
With this simple pipeline, there is no automatic correction for such discrepancies — you must manually account for them when tracing the lesions.

> **Note:**  
> This workflow assumes you have already mounted, stained, and imaged your brain slices.


## First Steps: Creating a Reference Volume

Before beginning lesion tracing, it is helpful to create a **reference volume** of the full region. (eg.DMS).  
This allows you to:

- Compare your lesion to the original structure.
- Calculate the overall percentage of the region that was lesioned.
- Understand lesion positioning across the full 3D extent of the brain.

To create a reference volume:

1. Follow the same segmentation steps described later, but instead of tracing lesions, **trace the full extent of the DMS**.
2. Work in 2D slices, sampling regularly — for example, trace every 2nd or 3rd slice through the brain region.
3. During analysis, these traced slices will be combined to estimate the full 3D volume of the brain region.

You can also load these reference volumes (e.g., DMS, tail of the striatum, etc.) into **napari** while tracing lesions.  
This helps by showing key boundary regions during your lesion drawing (see tracing steps below).

## Pipeline

1. **Open Napari** and launch the BrainGlobe-Segment tool.  
   For help, refer to the [BrainGlobe-Segment User Guide](https://brainglobe.info/documentation/brainglobe-segmentation/index.html).

2. **Load the example Allen atlas-registered brain** (in atlas space).  
   This gives you a 3D stack of a real brain warped to Allen atlas coordinates.

3. **For each histology slice**, find the corresponding position within the 3D stack.

4. **Click "Region Segmentation"** and add a new region.

5. **Create different regions** for different structures you trace, and **name them appropriately**.  
   For example:
   - `Left_DMS_Lesion`
   - `Right_DMS_Lesion`
   - `Left_Striatum_NonDMS`
   - `Right_Cortical_Leak`

   Each region can be plotted later, so think ahead about what plots you might need.  
   Consider whether you care about hemisphere differences, cortex damage, or striatal spillover — the labels you use here define what you can analyze later.

   > **Important:**  
   > Always include the slice name (standard space coordinate) in your region name.  
   > Best practice is a standardized naming scheme, e.g., `240_LDMS` for slice 240, left DMS lesion.  
   > Consistent naming across samples and animals makes analysis much easier.

6. **Trace all regions** you care about across all relevant slices.

   > **Important:**  
   > Make sure that **'n edit dim'** is set to **2** in BrainGlobe-Segment.  
   > This ensures you are drawing a flat 2D plane, not a 3D blob.  
   > If you accidentally create 3D blobs, the estimated lesion volumes will be significantly overestimated.

   **Tip:**  
   You can overlay your histology slice on your screen using a transparent image tool, which helps trace accurately:

   - **Windows:**
     - [Screendragon](https://www.majorgeeks.com/files/details/screen_dragons.html)
     - [Microsoft PowerToys: Always on Top](https://learn.microsoft.com/en-us/windows/powertoys/)

   (For help using these tools, ask ChatGPT!)

7. **Save your data** by clicking "Save".  
   This exports each traced region as a `.csv` file.

   > **Important:**  
   > The saved files go into a folder called 'segmentation/' inside the example allen atlas registered folder.  
   > **You must immediately copy them into a new folder named after your animal.**  
   > Otherwise, if you save new regions later, they could overwrite your previous work.









