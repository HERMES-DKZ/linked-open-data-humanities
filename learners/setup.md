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
2. Unzip the folder to a place of your choice (such as D:/Program Files/OpenRefine).
3. In the unzipped folder doubeclick "openrefine.exe" to install and start OpenRefine. 
4. Download the extension [rdf-transform](https://github.com/AtesComp/rdf-transform/releases/download/v2.2.4/rdf-transform-2.2.4.zip).
5. In the next step you need to unzip this folder into your OpenRefine Workspace. Depending on your Windows version the path for this can be different. You can find your path by: 
launchING OpenRefine and click Open Project in the sidebar
At the bottom of the screen, click Browse workspace directory
A file-explorer or finder window will open in your workspace. Note that path
6. In the workspace folder, if not already there, create a new folder called "extensions". Unzip rdf-transform into that folder.
7. Close OpenRefine and reopen it.




::::::::::::::::::::::::

:::::::::::::::: spoiler

### MacOS

 1. Check that you have Firefox, Edge, Opera or Chrome browsers installed and set as your
   default browser. OpenRefine runs in your default browser. It will not run
   correctly in Internet Explorer.
 2. Download the software from [openrefine.org](https://openrefine.org).
 3. Unzip the downloaded file into a directory by double-clicking it. Name
   that directory something like OpenRefine. / Double click the dmg file. A window opens an now drag and drop the OpenRefine.app into your Applications
 4. Go to your newly created OpenRefine directory.
 5. Drag the OpenRefine app into the Applications folder.
 6. Launch OpenRefine: Control-click the app icon, then
   choose "Open" from the shortcut menu. For Troubleshooting help, see
   [the Apple support page](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac).
 7. If you are using a different browser than listed above, or if OpenRefine does not automatically
   open for you, point your browser at [http://127.0.0.1:3333/](https://127.0.0.1:3333/) or
   [http://localhost:3333](https://localhost:3333) to launch the program.
 8. Download the extension [rdf-transform](https://github.com/AtesComp/rdf-transform/releases/download/v2.2.4/rdf-transform-2.2.4.zip).
 9. Unzip the folder and move it into your OpenRefine workspace. 
        1. You can find the path to your OpenRefine Workspace by launching OpenRefine and click Open Project in the sidebar. Then at the bottom of the screen, click "Browse workspace directory". A Finder window with the path `~/Library/Application Support/OpenRefine` opens.
        2. Unzip the downloaded folder by double clicking on it.
        3. Move the folder `rdf-transform` into the folder `extension` in your OpenRefine workspace.
10. Close OpenRefine and reopen it.

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
