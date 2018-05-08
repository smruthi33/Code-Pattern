# Image Recognition and Information Extraction from Image Documents using Keras and Watson NLU  

Application of loans, rental agreement and many such legal processes are extremely cumbersome and require high manual intervention. These processes usually, require the applicant to submit a few original documents along with the application form. An official is required to check these documents and identify one from the other. Furthermore he is required to extract information such as the Landlord or Tenant of the agreement if in case of a Rental agreement. So, the question is how can such processes leverage from the recent technological advancements such as Machine Learning, Natural Language Processing and Natural Language Understanding.

This code pattern aims to provide an end to end solution which will help improve legal application by automating certain processes and thereby reducing the need for manual intervention. 

The first module will identify the legal documents submitted such as, passport, cheque or a legal form. Once the images have been identified, the second module converts the images to text format. Finally, the third module extracts useful information required for the legal application by leveraging rule based techniques and results from Watson Natural Language Understanding.


This code pattern focuses on classifying an image document and extract the required information using Image Recognition techniques, Optical Character Recognition and Natural Language Processing.

After completing this pattern, you will learn how to:

* Perform Image Recognition using python libraries such as scikit-learn and keras(deep learning libraries)
* Extract information using Optical Character Recognition
* Use the IBM Watson NLU API to extract metadata from documents in Jupyter notebooks.
* Use a configuration file to build configurable and layered classification grammar.
* Use the combination of grammatical classification and regex patterns from a configuration file to extract information.


## Included components

* [IBM Watson Studio](https://www.ibm.com/bs-en/marketplace/data-science-experience): Analyze data using RStudio, Jupyter, and Python in a configured, collaborative environment that includes IBM value-adds, such as managed Spark.

* [IBM Cloud Object Storage](https://console.bluemix.net/catalog/infrastructure/cloud-object-storage): An IBM Cloud service that provides an unstructured cloud data store to build and deliver cost effective apps and services with high reliability and fast speed to market.

* [Watson Natural Language Understanding](https://console.bluemix.net/catalog/services/natural-language-understanding/?cm_sp=dw-bluemix-_-code-_-devcenter): A IBM Cloud service that can analyze text to extract meta-data from content such as concepts, entities, keywords, categories, sentiment, emotion, relations, semantic roles, using natural language understanding.


## Featured technologies

* [Jupyter Notebooks](http://jupyter.org/): An open-source web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text.
* [Artificial Intelligence](https://www.computerworld.com/article/2906336/emerging-technology/what-is-artificial-intelligence.html): Intelligence demonstrated by machines, in contrast to the natural intelligence displayed by humans and other animals
* [Machine Learning](https://searchenterpriseai.techtarget.com/definition/machine-learning-ML): Uses statistical techniques to give computer systems the ability to "learn" with data
* [Natural Language Processing](https://machinelearningmastery.com/natural-language-processing/): the ability of a computer program to understand human language as it is spoken. NLP is a component of Artificial Intelligence 
* [Python](https://www.python.org/): An interpreted high-level programming language for general-purpose programming


## 1. Sign up for IBM Watson Studio

Sign up for IBM's [Watson Studio](http://datascience.ibm.com/). 
By signing up for IBM Watson Studio, two services will be created - ``Spark`` and ``ObjectStore`` in your IBM Cloud account.

This code pattern is further divided into 3 sections-

* Image Classification of Documents
* Text Extraction Using Optical Character Recognition
* Entity Extraction and Document Classification

# Image Classification of Documents

## 1.  Prepare the Data

The input to this code are a set of images required for training and testing of the model.
To create your own Dataset, follow the following naming structure for each image-

![](images/Dir_structure-1.png)

Where, Cheque, Driving_License, None, Pancard and Passport are the classes required to classify by the model.
Or 
You may also use the sample training images provided in the git repo, in the Data folder.

## 2. Create the notebook 

A [notebook](https://datascience.ibm.com/docs/content/analyze-data/notebooks-parent.html) in Watson Studio is a web-based environment for interactive computing. You can run small pieces of code that process your data, and you can immediately view the results of your computation.

Steps:

In [Watson Studio](http://datascience.ibm.com/), click on Create notebook to create a notebook.

* In Watson Studio, click on Create notebook to create a notebook.
* Create a project if necessary, provisioning an object storage service if required.
* In the Assets tab, select the Create notebook option.
* Select the From URL tab.
* Enter a name for the notebook.
* Optionally, enter a description for the notebook.
* Enter this Notebook URL: https://github.com/smruthi33/Code-Pattern/blob/master/code/Image%20Classification%20of%20Documents.ipynb
* Select the free Anaconda runtime with 4 vCPU and 16 GB RAM .
* Click the Create button.

![](images/create_notebook_from_url_imageclassification.png)

## 3. Add the data file

* Add the all the files in your Data Folder to Object Storage- From the My Projects > Default page, Use Find and Add Data (look for the 10/01 icon) and its Files tab.
* Click browse and navigate to this repo (some name)/data and select the zip file

![](images/add_file.png)

    Note:  It is possible to use your own data files. If you use an image file from your computer, make sure to conform to the directory structure mentioned above and zip it.

Fix-up file names for your own data file

If you use your own data and configuration files, you will need to update the variables that refer to the data files in the Jupyter Notebook.

In the notebook, update the global variables in the cell following

2.2 Global Variables section.

    In the notebook, update the global variables in the cell following 2.2 Global Variables section.

Enter the desired batch_sizes for your training, validation and testing datasets

![](images/global_variables.png)


## 4. Update the notebook with service credentials

Add the Object Storage credentials to the notebook

Select the cell below  2.1 Add your service credentials for Object Storage section in the notebook to update the credentials for Object Store.

* Delete the contents of the cell
* Use Find and Add Data (look for the 10/01 icon) and its Files tab. You should see the file names uploaded earlier. Make sure your active cell is the empty one below 2.2 Add...
* Select Insert to code (below your sample_text.txt).
* Click Insert StreamingBody object from drop down menu.
* Make sure the credentials are saved as streaming_body_1.

![](images/add_file_imageclassification.png)


# Text Extraction Using Optical Character Recognition

* [Install Tesseract OCR](https://github.com/tesseract-ocr/tesseract/wiki). Follow the instructions according to you system specifications
* In the repo download the notebook Convert_Image_to_Text.ipynb 

    ### Configuration
         Fix-up file names for your filename and configuration files in the `2.1 Global Variables` section. 
         In the notebook, update the global variables in the cell following `2.1 Global Variables` section.
         
    ![](images/global_variables_OCR.png)    
         
    Replace the filename with the path of your image files and name with the desired output text file name
    or 
    Use the image files provided in the git repo /input_image/Rental_agreement and /input_image/Purcahse_agreement
    
* The output of this section will be the extracted text, saved as a text file in your current working directory. 
    
# Entity Extraction and Document Classification

## 1. Create IBM Cloud services

Create the following IBM Cloud service and give a unique name for the service instance:

* [Watson Natural Language Understanding](https://console.bluemix.net/catalog/services/natural-language-understanding)

![](images/bluemix_service_nlu.png)


## 2. Create the notebook 

In [Watson Studio](http://datascience.ibm.com/), click on Create notebook to create a notebook.

* In Watson Studio, click on Create notebook to create a notebook.
* Create a project if necessary, provisioning an object storage service if required.
* In the Assets tab, select the Create notebook option.
* Select the From URL tab.
* Enter a name for the notebook.
* Optionally, enter a description for the notebook.
* Enter this Notebook URL: https://github.com/smruthi33/Code-Pattern/blob/master/code/Entity%20Extraction%20and%20Document%20Classification.ipynb
* Select the free Anaconda runtime.
* Click the Create button.

![](images/create_notebook_from_url.png)


## 3. Add the data file

* Add the all the files in your Data Folder to Object Storage- From the My Projects > Default page, Use Find and Add Data (look for the 10/01 icon) and its Files tab.
* Upload the text files obtained as a result of 'Text Extraction Using Optical Character Recognition'
* Click browse and navigate to this repo (some name)/Confuguration and select all the files

![](images/add_file.png)

Note:  It is possible to use your own data files. If you use an image file from your computer, make sure to conform to the naming structure mentioned above.

Fix-up file names for your own data file

If you use your own data and configuration files, you will need to update the variables that refer to the data files in the Jupyter Notebook.

In the notebook, update the global variables in the cell following

2.2 Global Variables section.

In the notebook, update the global variables in the cell following 2.2 Global Variables section.

 Enter the filenames of the text file obtained as a result of 'Text Extraction Using Optical Character Recognition' as well as the configuration files uploaded into Object Storage.

![](images/global_variables_entity.png)

## 4. Update the notebook with service credentials

#### Add the Watson Natural Language Understanding credentials to the notebook
Select the cell below `2.1 Add your service credentials from IBM Cloud for the Watson services` section in the notebook to update the credentials for Watson Natural Langauage Understanding. 

Open the Watson Natural Language Understanding service in your [IBM Cloud Dashboard](https://console.bluemix.net/dashboard/services) and click on your service, which you should have named `wdc-NLU-service`.

Once the service is open click the `Service Credentials` menu on the left.

![](images/service_credentials_menu.png)

In the `Service Credentials` that opens up in the UI, select whichever `Credentials` you would like to use in the notebook from the `KEY NAME` column. Click `View credentials` and copy `username` and `password` key values that appear on the UI in JSON format.

![](images/copy_credentials.png)

Update the `username` and `password` key values in the cell below `2.1 Add your service credentials from IBM Cloud for the Watson services` section.

![](images/watson_nlu_credentials.png)

#### Add the Object Storage credentials to the notebook
* Select the cell below `2.2 Add your service credentials for Object Storage` section in the notebook to update the credentials for Object Store.
* Delete the contents of the cell
* Use `Find and Add Data` (look for the `10/01` icon) and its `Files` tab. You should see the file names uploaded earlier. Make sure your active cell is the empty one below `2.2 Add...`
* Select `Insert to code` (below your sample_text.txt).
* Click `Insert Crendentials` from drop down menu.
* Make sure the credentials are saved as `credentials_1`.

![](images/service_credentials.png)

# Run the notebooks

First run the Image Classification of Documents.ipynb. This notebook will identify a set of legal document from the rest of the input documents. The identified documents are further fed into Convert_Image_to_Text.ipynb. The resulting documents produced are fed as input to the next phase.
The notebook entity_extraction_and_document_classification.ipynb provides the required entities in the document and classify the document based on the configuration files fed as an input to the same

When a notebook is executed, what is actually happening is that each code cell in
the notebook is executed, in order, from top to bottom.

> IMPORTANT: The first time you run your notebook, you will need to install the necessary
packages in section 1.1 and then `Restart the kernel`.

Each code cell is selectable and is preceded by a tag in the left margin. The tag
format is `In [x]:`. Depending on the state of the notebook, the `x` can be:

* A blank, this indicates that the cell has never been executed.
* A number, this number represents the relative order this code step was executed.
* A `*`, this indicates that the cell is currently executing.

There are several ways to execute the code cells in your notebook:

* One cell at a time.
  * Select the cell, and then press the `Play` button in the toolbar.
* Batch mode, in sequential order.
  * From the `Cell` menu bar, there are several options available. For example, you
    can `Run All` cells in your notebook, or you can `Run All Below`, that will
    start executing from the first cell under the currently selected cell, and then
    continue executing all cells that follow.
* At a scheduled time.
  * Press the `Schedule` button located in the top right section of your notebook
    panel. Here you can schedule your notebook to be executed once at some future
    time, or repeatedly at your specified interval.




# Analyze the Results

