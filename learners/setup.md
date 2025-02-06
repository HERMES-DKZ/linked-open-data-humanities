---
title: Setup
---

FIXME: Setup instructions live in this document. Please specify the tools and
the data sets the Learner needs to have installed.

## Data Sets

The Dataset we will use in this lesson is a subset from the Collection of the [Metropolitan Museum of Art](https://www.metmuseum.org/de). If you are interested in the whole data you can find and use it in their database [here](https://www.metmuseum.org/de/art/collection). The subset we are using can be downloaded [here]()

## Software Setup

::::::::::::::::::::::::::::::::::::::: discussion

### Details

The only software you need for doing this workshop is Open Refine with the extension rdf-transform. OpenRefine is actually a tool for data cleaning. However, with various extensions, the tool can be customised and extended to convert data into other formats just as easily. If you are interested in the other functionalities of Open Refine, we are developing a lesson to this aswell, where you learn more of the fundamental functionalities of OpenRefine. 

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: spoiler

### Windows

1. Click this [link](https://openrefine.org/post_download?version=3.9-beta1&platform=linux) to download OpenRefine. 
2. Unzip the folder to a place of your choice (such as D:\Program Files\OpenRefine).
3. In the unzipped folder doubeclick "openrefine.exe" to install and start OpenRefine. 
4. Download the extension [rdf-transform](https://github.com/AtesComp/rdf-transform/releases/download/v2.2.4/rdf-transform-2.2.4.zip).
5. In the next step you need to unzip this folder into your OpenRefine Workspace. Depending on your Windows version the path for this can be different. You can find your path by:
5.     launchING OpenRefine and click Open Project in the sidebar
5.     At the bottom of the screen, click Browse workspace directory
5.     A file-explorer or finder window will open in your workspace. Note that path
6. In the workspace folder, if not already there, create a new folder called "extensions" Unzip rdf-transform into that folder
7. Close OpenRefine and reopen it.




::::::::::::::::::::::::

:::::::::::::::: spoiler

### MacOS

Use Terminal.app

::::::::::::::::::::::::


:::::::::::::::: spoiler

### Linux

1. Click this [link](https://openrefine.org/post_download?version=3.9-beta1&platform=linux) to download OpenRefine. 
2. Unzip the folder to a place of your choice. We recommend using your personal space.
3. Open your terminal and navigate into the new OpenRefine folder.
4. Write "./refine" into your terminal to install OpenRefine. This should start the program in your browser. Close the browser and close OpenRefine in your terminaml with "Strg+C".
5. Download the extension [rdf-transform](https://github.com/AtesComp/rdf-transform/releases/download/v2.2.4/rdf-transform-2.2.4.zip).
6. Unzip the folder into your OpenRefine workspace. The workspace is not the folder you downloaded and unzipped in step 2. By default your workspace is located here: "~/.local/share/openrefine/". In this workspace, if not already there, create a folder "extensions". Unzip the folder into this new folder.
7. Open your terminal again, navigate again into your OpenRefine folder and start it with "./refine".

::::::::::::::::::::::::
