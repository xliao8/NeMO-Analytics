# NeMO-Analytics
This document introduces the NeMO (Neuroscience Multi-Omic Archive) environment workflow and highlights the main features of the NeMO Analytics platform, providing a quick overview for new users. NeMO Analytics is closely related to the Gene Expression Analysis Resource (gEAR), as both platforms are built on the same back-end data infrastructure. The key distinction lies under the scope of the study, where NeMO is designed specifically for neuroscience study, and gEAR is primarily tailored to hearing-related study. Because they share the same infrastructure, many of the features and workflows are common across both platforms.

> *This tutorial is adapted from the official gEAR wiki page (which can be accessed through this [link](https://github.com/IGS/gEAR/blob/main/docs/Documentation/gEARWiki.md)), with modifications to highlight the NeMO-specific environment and workflows.*

---

## Table of Contents
1. [Overview](#overview)
2. [Key Features](#key-features)
3. [Getting Started](#getting-started)
4. [Typical Workflow](#typical-workflow)
5. [Examples](#examples)
6. [FAQ](#faq)
7. [Support](#support)

---

## Overview of typical NeMO workflow 
<img width="715" height="627" alt="image" src="https://github.com/user-attachments/assets/422d7fdc-26b5-4536-98c6-d461316302fb" />

---

### 1. Getting started with NeMO platform 

#### 1.1 Set up NeMO accounts
- Go to the homepage → click Log In (top right) → select Sign Up.
- Enter your basic details and email address.
- Verify your email to activate the account.
- Once logged in, you will have access to all the NeMO analytic tools and be able to make private/public dataset collections.
- Manage your profile anytime by clicking your username (top right).
- Enable colorblind-friendly mode for plots if needed.

<img width="1388" height="654" alt="image" src="https://github.com/user-attachments/assets/0deee0e6-fdc4-4c0a-a5f3-43b01d4d2fb7" />

---

#### 1.2 Layout of the NeMO platform 
    
*1.2.1 Home page* 

The homepage of the NeMO platform is the "My Workspace" Dashboard. At any time on the site, you can return to the homepage by clicking the NeMO icon in the top left corner. 

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/1695c719-5d58-41c7-8a4c-ca0a28a5e7a9" />

*1.2.2 Navigation panel*

The sidebar on the left-hand side of the page is the navigation panel. This panel will stay on the side as the users move between pages, allowing quick access to the various modules within NeMO. As the users become more familiar with the layout of the panel, they can choose to minimize it so that only the symbols are displayed (without text labels). To do this, simply click the arrow located in the upper-right corner of the navigation panel.

---

#### 1.3 Explore and exploit the available datasets

As a comprehensive data compendium, the NeMO platform allows users not only to upload their own datasets for customized analysis but also to explore a wide range of publicly available datasets. In fact, one of the best ways to become familiar with NeMO environment is to dive into the extensive collection of datasets already hosted on the platform. This section introduces the core functions and steps for data exploration, helping new users build an understanding of the platform and practice analyzing datasets of interest without uploading their own data.

*1.3.1 Finding datasets*

To view results from a specific dataset or browse available datasets, you can click the “Datasets” option or "Dataset collections" from the navigation panel. Within the Dataset Explorer, you can refine searches using the filter controls on the left side of the page. Filters include options such as data type, keywords from the study title, or organism. The explorer supports four different views of datasets, including "Table View", "List View-Compact", "List View (Expanded), and "Collection View". Each view presents a different level of detail about the datasets. 

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/ab54a4eb-9831-4baf-a83f-e859e65c01f5" />

To search for specific genes within a dataset,
  - click the small arrow in front of the dataset title to expand the entry.
  - In the expanded entry, you will see a default display created by the dataset owner.
  - Click the test tube icon to open the Expression Viewer, which allows you to explore gene expression using the default display.

If you prefer to create your own visualization:
  - Use the single-gene curator option from the drop-down menu under the analysis tools.
  - Detailed instructions on building custom visualizations will be provided in a later section.

When you first open the Expression Viewer, a default gene will appear, but you can replace it by typing any other gene name into the search box. By default, the viewer shows one gene at a time with the "single-gene display" mode. However, after saving your own gene list in NeMO (covered in a later section), you will be able to view multiple genes using the "multi-gene display" mode and toggle between them.

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/357a677a-d075-4052-8b01-2a927b33a5ac" />

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/c2931cc9-002c-460a-ae84-c1c193a6fc1c" />

On the right side of the Expression Viewer display, there are two buttons:
  - The left button lets you zoom in on the visualization.
  - The right button opens additional tools, including the option to view or switch to other displays created by the dataset owner.
    - Click on "Choose display" button allows you to select the new display you wish to view your gene of interest
      
<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/258530f3-2ef6-46c6-8979-f0f99aaff1ef" />

---

### 2. Retrieve datasets and metadata
The next few sections will begin introducing how to upload your own multi-omics datasets. 

---

### 3. Format standardizing and NeMO output packaging 
`Counts.IN.SeuratDimRedNeMO.OUT.TRIM.R` and `Counts.IN.SeuratDimRedNeMO.OUT.R` are two functions we have implemented in the NeMO workflow to standardize the multi-omics datasets format and package them into `NeMOanalytics.org` compatible outputs for uploading. Details about how to use the functions can be found in `Counts.IN.SeuratDimRedNeMO.OUT.TRIM.md` and `Counts.IN.SeuratDimRedNeMO.OUT.md`. 

---

### 4. Upload output to NeMO analytics platform
4.1 Output from the NeMO function 

Running the NeMO function will generate four outputs in the designated directory. Download the .tar.gz file and the .xlsx for uploading it onto NEMO

<img width="450" height="122" alt="image" src="https://github.com/user-attachments/assets/5380585e-f975-4cc4-a0a6-92bc3b4ca119" />

---

4.2 Uploading Data to NeMO

The dataset upload process in NeMO consists of two main parts: uploading the metadata file and uploading the expression data file.

*4.2.1. Upload Metadata*
 - In the left navigation panel, click Dataset Uploader.
 - On the Dataset Upload page, click “Choose” and select the metadata .xlsx file generated by the NeMO function.
 - Confirm your selection by clicking Upload.
 - The metadata fields will automatically populate, except for the Dataset type.
 - Manually select the correct dataset type from the dropdown menu.
 - Click Submit to proceed.
   <img width="852" height="400" alt="image" src="https://github.com/user-attachments/assets/632d158e-7670-45d0-9258-f747e97c7d4a" />
---

*4.2.2 Upload Expression Data*
    - On the next page, under Step – Upload dataset, select MEX / 3-tab format.
    - Click “Choose” and upload the .tar.gz file generated by the NeMO function.
    - Click Upload dataset to begin.
    - The upload time will depend on file size. Do not close your browser until the upload finishes, as this will interrupt the process.

*4.2.3. Background Processing*
   - Once the dataset file is successfully uploaded, NeMO will automatically extract and process the dataset in the background.At this stage, you no longer need to keep your browser open.
   - When processing is complete, the system will confirm that your dataset is available.

*4.2.4 Finalize and Curate*
After processing is complete, click Done. You can then begin curating dataset visualizations and adding the dataset to your collections.

*4.2.5 Troubleshooting*
If you encounter errors during the upload process, please submit a ticket on [the gEAR GitHub site]
(https://github.com/IGS/gEAR/issues). Be sure to include your dataset ID when reporting the issue.


### 5. Curate Visualization 
### 6. Create dataset collections 
### 7. Further analysis using additional NeMO analytic features
