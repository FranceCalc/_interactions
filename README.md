# The EU Calculator project

The [EUCalc project](http://www.european-calculator.eu/) has the goal of delineating emission and sustainable transformation pathways at a European and member state levels. The project develops an open source model combined with a “Transition Pathways Explorer” as well as learning tools designed to engage and be used by European and national policy makers, businesses, NGOs and other actors of society.

- The main website for the EUCalc project is [www.european-calculator.eu](http://www.european-calculator.eu)
- More info about the model can be found [here](https://docs.google.com/document/d/1gz0VumBof2SjBwrroOWMGVmWhOmiYjtbOKeL70BGlD8/edit#).
- More info about the usage of Knime in this modeling effort can be found [here](https://docs.google.com/document/d/1eVJZtXkyQrCoUH3Uc68HBoLQRKQJqCYNQKBpddyVCqM/edit#).

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

# Prerequisites

## Hardware and OS
The project has been tested with computers running Windows 10, with 8-16 GB of RAM.

## Software
Before being able to run the project on your local machine you need to install the following software.

1. **KNIME Anatytics Platform 3.7.2**: the software we use to develop the code. To install this open source software, please visit the following url: [KNIME 3.7.2 download](https://www.knime.com/download-previous-versions).
2. **Python 3.6**: some of the EUCalc code uses Python in the background. Installing the [Anaconda](https://www.anaconda.com) distribution is typically the easiest (Miniconda being the most lightweight). A virtual environment can be setup, but it is not mandatory. The following packages need to be installed:
   - lxml
   - xlrd
   - openpyxl
   - numpy
   - pandas
  
3. (optional) **Git** : To install Git on Windows you will need to download the installer from the [Git](https://git-scm.com/downloads) website. Please refer to an online Git tutorial if you are not familiar with this versionning control software (Atlassian tutorial: [Setting up Git on Windows](https://www.youtube.com/watch?v=eo00v2aw92Y)). Note that Git is not mandatory to download the model repository (see bellow).

# Setting up the model

## Installing the EUCalc code
Prior to anything you need to have a local version of the code. Do that by cloning the Git repository or by downloading a Zip archive. Whatever the selected solution, you first need to create a directory that will hold the "workspace" for KNIME, for instance `C:\EUCalc\`.

>### Git option
> To [clone the Git repository](https://confluence.atlassian.com/bitbucket/clone-a-repository-223217891.html) on your computer, open a Command Prompt, navigate to the 'workspace' folder and clone the repository using the following command line (replacing 'username' by your bitbucket username):
>
>```
>$ git clone https://username@bitbucket.org/eucalcmodel/_interactions.git
>```
> After cloning, navigate to the cloned repository and use the following command line:
>
>```
>$ git checkout tags/v2.2.1
>```
>
>### Zip option
> [Download Zip archive](https://bitbucket.org/eucalcmodel/_interactions/get/v2.2.1.zip) and unzip the content in the 'workspace' folder.

This repository contains multiple folders:

- **configuration**: configuration files to set up the position of the levers and manage the interface between the modules
- **data**: input of the model
- **workflows**: KNIME workflows

# Using the EUCalc model

## Preparation

The main workflow that you need to open in order to run the model on your local machine is called `data-processing`.

Launch KNIME, select the folder where you cloned the Git repository as workspace and open this worfklow by double clicking on it (path: `_interaction/workflows/data-processing`). If you need more explanation on how to get starting with KNIME, please visit this [url](https://www.knime.com/getting-started). 

Knime will ask what the workspace directory should be. This should be the directory you created when cloning the repo (i.e. one level up from the `_interactions` directory).

If this is the first time, after opening the workflow KNIME will ask you to install a series of extensions. Accept and restart KNIME when asked to. To set up the KNIME Python extension, please visit this [page](https://www.knime.com/blog/setting-up-the-knime-python-extension-revisited-for-python-30-and-20).

## Running the model

You are now ready to run the tests. Press `Execute all executable nodes` (`Shift + F7`) to run the model. It takes approximately 30 minutes to run (depending on your machine). 

## Visualising the outputs

A few green boxes contain nodes that allow to visualise the output of the different modules. To use them, right-click the nodes and select Wrapped Metanode > Individual Views > Generic Javascript View.

## Exploring data outputs 

The outputs of all modules can be explored in Knime by right-clicking the module and selecting the desired output.

## Changing the position of the levers

To change the position of the levers you need to go to the `configuration` folder and open the `lever_position` JSON file. Update the file and then re-run the workflow.

---
# Going deeper into individual sector models

The `_interaction` folder is only the main workflow consolidating all the sectors of the model. To go deeper in a specific sector you need to clone the Git repository of this sector on your local machine. Find the list of the repos [here](https://bitbucket.org/repo/all?name=eucalcmodel):

- Buildings
- Lifestyle
- Climate
- Agriculture
- Employment
- Industry
- Transport
- Electricity Supply
- Water
- Biodiversity
- Minerals
- Employment
- Air Quality

Once the repo is cloned, open the workflow of the sector (in the workflows folder) and run it. You don't need to connect to the MySQL server, every input in the sector repo is Excel based.

More than the workflows, you'll find in those repos the raw input (folder `data`) of the model as well as the assumptions and sources of those data.

---
## Authors

* **Vincent Matton** - *Initial work* - [Climact](http://www.climact.com/)
* **Amaury Anciaux** - *Initial work* - [Data@Work](http://www.data-at-work.ch)

See also the list of [contributors](http://www.european-calculator.eu/about/eucalc-partners/) who participated in this project.

## License

This project is licensed under the *** License - see the [LICENSE.md](LICENSE.md) file for details.

## Known issues

### Main issues

* **FATAL Java Snippet** - *There is missing value(s) in the "Country" column: "[Switzerland]"* - data-preprocessing-database - Lifestyle module
* **FATAL Java Snippet** - *There is missing value(s) in the "Years" column: "[1990, 1991, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 1992, 2010, 2011, 2012, 2013, 2014, 2015, 1993, 1994, 1995, 1996, 1997, 1998, 1999]"* - data-processing - output of *5.1 Electricity*
* **ERROR Java Snippet**  - *There is extra value(s) in the "Country" column: "[Europe]"* - data-processing - output of *5.2 Oil Refinery*



### Secondary issues

* **ERRORS** while opening the workflow
* **ERROR Excel Reader (XLS)** - *DataSpec generated by configure does not match spec after execution.* - data-preprocessing-database - Lifestyle module
* **FATAL Java Snippet** - *There is missing value(s) in the "Years" column: "[2015]"* - data-preprocessing-database - Lifestyle, Electricity Supply and Buildings modules
* **FATAL Java Snippet** - *There is missing value(s) in the "lever_decom_**" column: "[2, 3, 4]"* - data-preprocessing-database - Electricity Supply module
* **ERROR Java Snippet**  - *There is extra value(s) in the "Country" column: "[Norway]"* - data-preprocessing-database - Transport and Technology modules
* **ERROR Java Snippet** - *There is extra value(s) in the "Years" column: "[1970, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029, 2030, 2031, 2032, 2033, 2034, 2035, 2036, 2037, 2038, 2039, 2040, 2041, 2042, 2043, 2044, 2045, 2046, 2047, 2048, 2049, 2050, 1980, 2016, 2017, 2018, 2019, 2020, 2021]"* - data-preprocessing-database - Technology and Tranport modules
* **ERROR Java Snippet** - *There is extra value(s) in the "Years" column: "[1970, 1980]"* - data-preprocessing-database - Transport module
* **ERROR Java Snippet** - *There is extra value(s) in the "Country" column: "[Iceland, Norway]"* - data-preprocessing-database - Buildings module
* **ERROR Java Snippet** - *There is extra value(s) in the "Years" column: "[2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029, 2030, 2031, 2032, 2033, 2034, 2035, 2036, 2037, 2038, 2039, 2040, 2041, 2042, 2043, 2044, 2045, 2046, 2047, 2048, 2049, 2050]"* - data-preprocessing-database - Buildings module


