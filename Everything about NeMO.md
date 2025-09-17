# NeMO-Analytics
This document introduces the NeMO (Neuroscience Multi-Omic Archive) environment workflow and highlights the main features of the NeMO Analytics platform, providing a quick overview for new users. NeMO Analytics is closely related to the Gene Expression Analysis Resource (gEAR), as both platforms are built on the same back-end data infrastructure. The key distinction lies under the scope of the study, where NeMO is designed specifically for neuroscience study, and gEAR is primarily tailored to hearing-related study. Because they share the same infrastructure, many of the features and workflows are common across both platforms.

> *This tutorial is adapted from the official gEAR wiki page (which can be accessed through this [link](https://github.com/IGS/gEAR/blob/main/docs/Documentation/gEARWiki.md)), with modifications to highlight the NeMO-specific environment and workflows.*

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
      
<img width="961" height="452" alt="image" src="https://github.com/user-attachments/assets/f6da7f8a-1591-4c29-af8a-ca43204261af" />


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
   <img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/632d158e-7670-45d0-9258-f747e97c7d4a" />
---

*4.2.2 Upload Expression Data*

- On the next page, under Step – Upload dataset, select MEX / 3-tab format.
- Click “Choose” and upload the .tar.gz file generated by the NeMO function.
- Click Upload dataset to begin.
- The upload time will depend on file size. Do not close your browser until the upload finishes, as this will interrupt the process.
<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/b97826cb-c4a3-4047-853e-f569721ab9e0" />

*4.2.3. Background Processing*
   - Once the dataset file is successfully uploaded, NeMO will automatically prompt you to the next step, "processing", where all the extraction and processing of the dataset happens in the background. At this stage, you no longer need to keep your browser open.
   - When processing is complete, click continue to move on to the next setp.
<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/a2e290c9-5c0e-41f6-a0db-44ce97df46ec" />

*4.2.4 Finalize and Curate*

- After processing is complete, follow the prompt on NeMO to change the data visibility and finalize the uploading. 
- You can then begin curating dataset visualizations and adding the dataset to your collections.

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/25ba3da4-6804-4369-9788-bd0588cfc242" />
<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/287b9247-43df-4d3a-ba19-f7810e6dc525" />


*4.2.5 Troubleshooting*

If you encounter errors during the upload process, please submit a ticket on [the gEAR GitHub site]
(https://github.com/IGS/gEAR/issues). Be sure to include your dataset ID when reporting the issue.

---

### 5. Curate Visualization 

One of the major strengths of the NeMO Analytics platform is the ability to create multiple visualizations for the same dataset. In addition to the default displays generated by the original dataset owner (as shown in 1.3 Explore and exploit the available datasets), you can create custom displays that are better suited to your own research questions for the datasets that are available on NeMO or your own uploaded datasets. 

5.1 Launch the visualization tools 

There are three ways you could start curating your own visualization, depending on the usage scenario
 1. After uploading your own datasets

Clicking on the "Curate" button will bring you to the "single-gene display" page, where your uploaded dataset will automatically populate in the "1. select a dataset" slot

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/674640b7-b337-40cd-aa49-4b0d91090f99" />

 2. Customize visualization for existing datasets

- You may also access the "single-gene display" page through the navigation panel and manually search for the dataset of interest.
<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/25ea897d-f1a9-4735-97dd-f4a8f6bf2ed5" />

- Alternatively, in the Data management page, select the "single-gene display in the expanded entry from the "analysis tool" dropdown menu. 

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/1fdd31af-844f-4cfb-a69c-c8fe10cfceca" />

---

5.2 Create new visualization 
After navigating to the "single-gene display" page, you can start creating a new visualization for the dataset by clicking "Curate new display".  

<img width="1378" height="443" alt="image" src="https://github.com/user-attachments/assets/8dc5542a-4b6a-408f-a91f-57257bc50e6e" />


Multiple plot types and analysis types are available through NeMO, including line plot, bar plot, scatter plot, violin plot, t-SNE, UMAP, and PCA. NeMO also offers the option to make the plot interactive or static. All these features for the plot can be changed in step three, "Select dataset plot type and analysis type". 


<img width="1378" height="184" alt="image" src="https://github.com/user-attachments/assets/355b4d98-8f5a-4ec9-be14-a07abee9fd8d" />

Choose a gene for your analysis in Step 4. Note that this gene could be arbitrary for the purpose of creating displays. Saving the visualization would allow you to look up a different gene/list of genes in the "Gene Expression Search" page (see 1.3 Explore and exploit the available datasets for details). 

The plot setting could be further customized by specifying the axes of the plots. The axis and color options available in the dropdown menu are related to the column names/variables in the cellMETA when running the `Counts.IN.SeuratDimRedNeMO.OUT.R function". Therefore, we recommend concatenating the complete metadata information to the cellMETA when first running the `Counts.IN.SeuratDimRedNeMO.OUT.R function` to avoid going back and forth with the uploading process.  

<img width="1378" height="298" alt="image" src="https://github.com/user-attachments/assets/13d86a28-bd6f-411e-bfcf-5ee95a8ec9ea" />

Confirm the setting by clicking "Plot", which will bring you to the preview of the display, where you have more options to refine and make minor adjustments on the plot using "Dataset filters", "Plot configuration", and "Change color". Check the "Make this my default display box" if you wish it to appear as a preview on the expanded dataset list view. Confirm the change by clicking the "Save as new display" button. 

<img width="1378" height="452" alt="image" src="https://github.com/user-attachments/assets/e599ea89-d5c7-41ea-9514-39b59bbe8f52" />

Once the display is saved, it will appear in the "single-gene display" page. To make changes to this existing display, select "Clone" under the display. After the necessary changes on the plot, confirm by selecting the "Update plot" button and choosing "Overwrite existing display instead". 

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/941942e0-f96c-452e-95ca-d900402fa25a" />


### 6. Create dataset collections
Dataset collection is one of the unique NeMO features of grouping different datasets around a shared theme. The NeMO community has been curating dataset collections that are available to the public domain, but any user can create their own dataset collection of datasets to explore.

6.1 Exploring site curated collections

In the Gene Expression Viewer, you can search within specific dataset collections by using the dropdown menu. The menu provides several options, including: site-curated collection, collections you own, collections you’ve recently accessed, collections from groups you belong to, and collections shared with you by other users. 

Type in your gene of interest and simply select the desired collection from the dropdown to focus your search within that set of datasets.

<img width="1378" height="648" alt="image" src="https://github.com/user-attachments/assets/98c5f9b5-a53d-4a92-8ef0-ad6574f29c75" />

To generate a shareable link for this particular collection page, select Datasets or "Dataset collections" from the navigation panel. Use the dropdown menu from the Collection management to choose the desired curated collection. Move the cursor on the middle icon to get the shareable link. 
<img width="1374" height="648" alt="image" src="https://github.com/user-attachments/assets/78922e20-1999-4899-8afd-a3669dc0d869" />

---
6.2  Create a new collection

In the "Dataset Explorer" page, locate the "Collection Management" and click the plus (+) icon to create a new dataset collection. Enter a name for your collection and click "Add". The new collection will then appear in the dropdown menu.

<img width="1374" height="648" alt="image" src="https://github.com/user-attachments/assets/d5baed23-a9cb-4d56-96f0-0b8de6615fd7" />

---

6.3 Add datasets to your collection

In the same "Dataset Explorer" page, make sure you are in the collection you just created. Find the dataset you want to add to the collection and expand its dataset entry. Clicking the plus (+) icon next to a dataset entry adds it to the collection. To remove a dataset, click the minus (–) icon. 
<img width="1374" height="648" alt="image" src="https://github.com/user-attachments/assets/86fa18c3-a950-4306-b9a3-2c230bb064b8" />

Clicking the plus (+) icon will prompt you to view all the displays created by you or the dataset owner. To select/remove a specific display from this dataset, click the plus (+)/minus(-) button again. 

<img width="1374" height="648" alt="image" src="https://github.com/user-attachments/assets/e64e0bbb-118d-4d93-bacf-3008116b723e" />

---

6.4 View and arrange the collection

The layout of dataset collections (how they appear when viewed in the "Gene Expression Viewer") can be customized in the Dataset Explorer under "Collection arrangement view".

- In the "Dataset Explorer, select a collection: use the "Collection Management" dropdown to choose the dataset collection you want to edit. (Note: You can only modify collections you own. However, you may duplicate shared collections and then customize them as you wish). 
- Go to the "Collection arrangement view" by clicking the last icon among the view selection. If you do not have editing permissions for the collection, this button will not appear.
- Rearrange datasets by following the instructions. 
    - Drag and drop panels to change their order and position.
    - Resize panels by adjusting their width and height to make them larger, smaller, wider, or narrower.
    - When you are satisfied with the layout, click Save to apply your changes.

<img width="1374" height="648" alt="image" src="https://github.com/user-attachments/assets/8395bcc0-72e1-44b2-b113-e60471efbf5e" />

---

### 7. Further analysis using additional NeMO analytic features

7.1 Gene List 
