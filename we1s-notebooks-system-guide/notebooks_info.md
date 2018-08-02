<div style="float: right; font-size: 80%;">(Document author: Lindsay Thomas; document created Aug. 1, 2018; last revised Aug. 1 2018)</div>

# WE1S Jupyter notebook system
harbor.english.ucsb.edu:9999

Password: This is the password we will give you.

## General warning
Our notebook system is rough right now. It works, but there's a lot of junk in there that is a holdover from previous workflows, and there's some weird hacky stuff we had to do at various points to make everything work and to make using the notebooks slightly easier until our Workspace Management System (WMS) is up and running. We are in the process of streamlining and revising the entire workflow for JupyterLab, and for hooking it up with our WMS, but we aren't done with that yet. Additionally, the notebook workflow only allows for topic modeling at this stage; we have plans to incorporate more methods of analysis later.

In other words, we are definitely not ready for public release, and the system is not exactly user friendly if you're not already familiar with it. Our apologies.

## Our data
Please note that none of our data is publicly shareable right now. Our contract with LexisNexis for use of their Web Services Kit allows us to store plain text from LexisNexis for a preliminary period of time for development, which we are still within. After this development period ends, we will be storing data in bagified form.

All of the data we have collected for the project so far is available on our server in zip folders that contain json files. The majority of this data is collected from LexisNexis, but we have also scraped some data from various news websites.

If you go to [harbor.english.ucsb:9999](http://harbor.english.ucsb:9999), and enter in the password we have given you, you will see a directory tree with 4 folders: 
* `data`
* `read`
* `view`
* `write` 

All of our data is in the `data` folder. If you click on that, you will see a folder named `data-new`, and a folder named `data-old`. Both directories are a mess in their own ways. The `data-old` folder contains a lot of messy subdirectories that made sense at various points in time throughout our camp, but likely just to us. The `data-new` folder contains everything we have downloaded from LexisNexis since about July 26, 2018. We recently completed the process of re-collecting everything with our improved collection script that people have requested from LexisNexis throughout our five weeks of camp, so data-new contains the best data we have thus far. However, we don't necessarily recommend browsing `data-new`, as it contains a lot of files, takes a long time to load, and is difficult to browse anyway because of the verbose filenames. Notebook 1 (see below) gives you a way to "browse" this folder for the data you want before import.

The zip files from LexisNexis are organized by query, and the filenames include the source, keyword searched, and the year requested. Usually, people have requested data in 1-year increments. For each query, there are 2 zip files: one including the phrase `no-exact-match` and one without it. This is related to how we collect data from LexisNexis; most of the time, you will want to only use the exact match zip files in your modeling (so, those zip files WITHOUT the phrase `no-exact-match` in their filenames).

We also have some data that has been scraped from various online news websites on our server. This data is located in `data` > `data-old` >`am-team-5-webscraped-data`. It is also stored as a series of zipped folders containing json files.

## Take the notebooks for a spin
### A. Generate a new project
1. Go to [harbor.english.ucsb:9999](http://harbor.english.ucsb:9999) and enter in the password we have given you.
2. To spin up a new project, go to `write` and select `new_topic_json_browser`. This is our project generator notebook. It will create the notebooks you need for your project. It is a read-only notebook, meaning you can't save anything to it.
3. A Jupyter notebook will open. You need to specify the template you want to work with, your project name, and the directory where you want to store your project. 
    * The default template path is `templates/topic_browser_json_template`. This is what you want; leave it alone. 
    * Under NAME PROJECT, give your project a name. No spaces, please, and keep the single quotes around the name; it should look like this `'your-project-name'`. When your project is created, a timedate stamp will automatically be added to the beginning of your project name.
    * Under CHOOSE WHERE PROJECT IS STORED, select the directory where you want to store your project. The default project path is simply `'projects'`. We have created a folder for your projects on our system, which is called `advisory-board`. The cell with the directory should look like this: `project_directory = 'projects/advisory-board'`.
4. Now this notebook is ready to run. The cells of the notebook need to be run in the order in which they appear in the notebook. You can run one individually by clicking in the cell, and then clicking on the play button up under the file menu, or, once you've filled out all of the names and paths you need, you can go to `Cell > Run all.` The notebook cells will run, and a link to your new project will appear at the bottom (`Next: Import Data`). You can click that link to go to your first project notebook.
5. Go to `File > Close and Halt` and then close the project generator notebook (it will tell you changes can't be saved; this is to be expected).
6. You can find your project in the directory tree by going to `home > write > projects > advisory-board.` You should see your project folder listed there. If you click on it, you will see all of the folders and notebooks you need to run your project.

### B. What your project folder contains
There are currently 7 notebooks in our workflow:
* Notebook 1: Import Data
* Notebook 2: Clean Data
* Notebook 3: Make Topic Model
* Notebook 4: Make Topic Browser
* Notebook 5: Customize Topic Browser
* Notebook 6: PyLDAvis Browser
* Notebook 7: Topic Bubbles Browser

To create a topic model, you will need to run notebooks 1-3 in series (1, then 2, then 3). Notebooks 4-7 offer different ways of visualizing your model. Each of those visualizations is briefly explained below. 

Each notebook contains comments that explain what's happening at each stage, but we haven't yet had time to make these legible to a wider audience. As with the project generator notebook, each cell in each notebook needs to be run in the order in which it appears. You can run cells individually by clicking in them and pressing the play button; or you can run all of the cells in a notebook (once you've customized how you like) by clicking `Cell > Run all`. 

Slightly more extensive (though outdated) directions can be found in our GitHub repo: https://github.com/whatevery1says/we1s-notebook.

### C. Change the number of topics
The default number of topics that each project is set to create is `50`. If you want to change this, head to your project folder (`write > projects > advisory-board`), and click on the file named `settings.py`. You'll see a bunch of settings there; the one you want to change is `model_num_topics`. You need to change this setting _before_ running Notebook 3.

### D. Import data
1. After generating a new project, a link will automatically appear at the bottom of the project generator notebook to Notebook 1 of your project. Click on that link.
2. Under "Preview Available Data," you will see a series of 3 steps that allow you to browse the `data` folders and select files to import.
3. Step 1 asks you to choose a search term (perhaps the name of the source you want data from). Step 2 runs that search, which you can then review. Select the filenames that you want to import, and, in Step 3, copy and paste the entire cell output into the `datafile_list` array.
4. You can then run the notebook cells. 

### E. Browser notebooks
* Notebook 4: Make Topic Browser
    * This notebook uses Andrew Goldstone's `dfrtopics` package to create a topic model browser (Goldstone's `dfrtopics` GitHub repo: https://github.com/agoldst/dfrtopics; Goldstone's `dfr-browser` Github repo: https://github.com/agoldst/dfr-browser). 
* Notebook 5: Customize Topic Browser: 
    * This notebook allows you to customize topic labels and some other settings for `dfr-browser.`
* Notebook 6: PyLDAvis Browser: 
    * This notebook uses Carson Sievert and Kenny Shirley's port of the R LDAVis package to create a topic model visualization (GitHub repo: https://github.com/bmabey/pyLDAvis).
* Notebook 7: Topic Bubbles Browser: 
    * This notebook deploys WE1S RA Sihwa Park's custom Topic Bubbles script to create a topic model visualization (GitHub repo: https://github.com/sihwapark/topic-bubbles).
