# Python-with-Google-Colab
This repo contains information on how to use Python in Google Colab.




 

### What is Colab
It’s a Jupyter notebook environment that requires no setup to use.
Moreover it gives you **free GPU** access to run your code. 
In simple words Colab is a free hosted Jupyter notebook with access to GPU.
 
* Colab Runtime - Instance of Jupyter notebook.  

* Colab stores the notebooks in your Google Drive.  

* All the files uploaded to Colab are **ephemeral**, they are **gone** after reloading Colab Runtime. 
    The recommended way is to upload your data to Google Drive then mount the drive in the Runtime  
    
* Colab provides integration with Github. It's possible to load notebooks directly from repositories 
and commit changes made in Colab. However, there are some limitations  

##  Quick Start

1. Create Github repository and push Jupyter Notebook (can be empty) into it 
(if you already have a notebook that you want to run in colab in some other repository you can skip this step.)

2. Go to <https://colab.research.google.com/>, pick *GITHUB* source and put the repository details

    ![colab start](pictures/colab_github_load.png)

3. Click on **NEW PYTHON 3 NOTEBOOK** and that's (almost) it! Now you can write and run your code in Colab using Google GPUs

### Bonus
#### Accessing data on Google Drive
Code below mounts your Google Drive to 
`/content/drive/My Drive` directory.

In case `google.cloab` is not found it assumes that the notebook runs somewhere else and it doesn't mount the drive.
```python
try:
    from google.colab import drive
    drive.mount("/content/drive/", force_remount=True)
    google_drive_prefix = "/content/drive/My Drive"
    data_prefix = "{}/mnist/".format(google_drive_prefix)
except ModuleNotFoundError: 
    data_prefix = "data/"
```

After that your data are available locally:
`f = gzip.open("{}/train-images-idx3-ubyte.gz".format(data_prefix), 'r')`

#### Integration with Github

It is more convenient to work on your code locally (e.g. Using JupyterLab or Pycharm) and use Colab only to
execute the code on GPU and do some small changes (e.g. Hyper parameters tuning).

Unfortunately there is no `git pull` functionality in Colab, so once you push a new changes into the Repository
you have to reopen your notebook (File -> Open notebook -> GITHUB -> Open notebook in new tab (Square with arrow next to the notebook name)).
The downside is that the runtime has to be reloaded.



##### Warning This might create conflicts! 
 
However, it's possible to push changes made in colab to the Repo (File -> Save a copy in Github):
![colab push](pictures/colab_push.png)
This will make a commit to the Repository.

#### Using GPUs
**Warning** This will reload your runtime!

Navigate to: Runtime -> Change runtime type -> Hardware accelerator -> pick GPU (or TPU) 

