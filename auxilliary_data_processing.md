## Auxiliary Data Processing Tutorial

For all foreseeable tasks for the CoNIC process, external data comes from the following primary sources:

- ubCov extraction
- Expert opinion (no primary data source.)
- Literature (e.g. systematic review)
- Other

This tutorial will show you how to process these external data sources so that they are properly stored and uploaded for
use in a `vivarium` simulations. This involves preparing your data, initializing a processing task, transforming your 
data into the appropriate format, validating the processing code you've written to ensure it works, and finally uploading 
your data so it can be used in a simulation.

### 1. Prepare your raw data.
Before you can begin processing your data, you first must prepare it. 

#### a. ubCov data

Because ubCov is such a complicated and unstable tool, we have a separate library 
used to extract and prepare UbCov data. Use the [conic_ubcov_extraction library](https://stash.ihme.washington.edu/projects/CSTE/repos/conic_ubcov_extraction/browse)
to prepare your ubCov data.

As of 9/6/2018, the `DATA_DIRECTORY` is `J:/Project/Cost_Effectiveness/CoNIC/Data` for ubCov extractions
 
 #### b. Expert opinion

You have no data, so no need to prep it :-).

#### c. Literature

Literature data does not necessarily have to be a systematic review, it simply refers to any data source 
extracted using the literature template. 

As of 9/6/2018, the `DATA_DIRECTORY` is `J:\Project\Cost_Effectiveness\CoNIC\Literature\Intervention_reviews`
for literature reviews. See the below example for what should be in your data directory.   

**Example** 
```
<DATA_DIRECTORY>/
    breastfeeding_promotion/
        2018_07_26_breastfeeding_promotion_extraction_yaqi.csv
        version.yaml
```

Note that data must be in **.csv format.**

More on `version.yaml` in a minute.

#### d. Other
**Note:** as of 8/27/2018, we have not had a use case for custom data, but below are instructions for future use.  

Some data (e.g. facility records) will not neatly fit the literature extraction template.
Custom data should be as close as possible to the raw data extracted. If you perform
an aggregation or tabulation of your raw data, include both the original data and the
aggregated data as well as the script or notebook you used to perform the aggregation
in your data directory. 

Data should be saved in the directory 
`<DATA_DIRECTORY>/<DATA_NAME>`,  where `DATA_NAME` refers to what the data represents (e.g. breastfeeding_promotion). A 
note for clarity: the `DATA_NAME` used here is distinct from the `ENTITY_NAME` you will see used below. `ENTITY_NAME` 
refers to the entity used within Vivarium (e.g. lack_of_breastfeeding_promotion).  

We'll walk through two examples using data about coverage of in-facility births. Our directory is thus
 `<DATA_DIRECTORY>/breastfeeding_promotion`.
  
**Example 1. No aggregation:**
 
For this example, let's assume we have a series of nice studies conducted at the country 
level describing in facility birth coverage.  In that case, our data directory would
look like:
```
<DATA_DIRECTORY>/
    breastfeeding_promotion/
        country_1.csv
        country_2.csv
        ...
        country_N.csv
        version.yaml
```

`version.yaml` will be described in detail below. For now, just note it's presence in the directory.

**Example 2. With aggregation.**

Now let's assume we are instead dealing with a series of surveys that collected data at the facility level instead of the
country level. As is, this data is inconvenient to build country-level models with, so we've written a jupyter 
notebook that aggregates it into country level data. Our data directory in this case would look like:

```
<DATA_DIRECTORY>/
    in_facility_birth_coverage/
        microdata/
            country_1_facility_1.csv
            country_1_facility_2.csv
            ...
            country_1_facility_i.csv
            country_2_facility_1.csv
            ...
            country_N_facility_k.csv
         country_1.csv
         country_2.csv
         ...
         country_N.csv
         aggregation.ipynb
         version.yaml            
```
Notice that the difference here as compared to the previous example is the presence of the original microdata and 
aggregation notebook.

**Note:** The names of the individual `.csv` files here are not important for processing, as long 
as you understand how they relate to each other.

**The `version.yaml` file**

Hopefully you've noticed that every example data directory we've shown has an included a `version.yaml` file. The purpose
of this file is to serve as a chain of custody for the data. This allows anyone with questions to find out when the data 
was generated and who generated the data. This is vital if we need to debug any issues we find in the data.

You are responsible for writing this file, containing the below required fields and adding it to your data directory.

It should always include the same four fields:
 
 - `timestamp`: The time the data was extracted. Can be any human readable date format. I used
 `python`'s `datetime` library to generate the one above, but you could have just written `"7/15/2018"`
 and that would be fine.
 - `owner`: This is you. Your full name please.
 - `owner_email`: Your work email.
 - `notes`: A single string (though maybe multiple sentences) describing any important information
 about the data. Relevant things to include here are the date and name of the studies/surveys/etc.
 you extracted. You might also include other information you think is relevant (e.g. "Only
 includes hospitals with more than 10000 patients a year").


The `version.yaml` file for our facility coverage data examples would look like:

```yaml
timestamp: "2018-07-15 16:41:11.945793"
owner: "James Collins"
owner_email: "collijk@uw.edu"
note: "Data was extracted from the 2007 International Hospital Outcomes Study" 
```
**Note the quotation marks around each value.** 


### 2. Make a separate environment 
You'll need a dedicated environment for auxiliary data processing. This environment will have only the `conic_ubcov_extraction` 
and `auxiliary_data_processing` repositories. Depending on your needs, you may also need to install `R` or `stata`. If 
you've previously made this environment for another entity, you only need to activate the environment and you can move to
step 3. 

First, create a new environment:
``` 
conda create -n aux-data python=3.6
```
Once you have your environment, you'll need to install the necessary repositories as shown here:
``` 
source activate aux-data
pip install gbd_mapping vivarium_gbd_access
git clone ssh://git@stash.ihme.washington.edu:7999/cste/conic_ubcov_extraction.git
cd conic_ubcov_extraction
python setup.py develop
cd ..
git clone ssh://git@stash.ihme.washington.edu:7999/cste/auxiliary_data_processing.git
cd auxiliary_data_processing
python setup.py develop 
```
You're now ready to proceed with processing in your new environment!

### 3. Initialize your processing task

Now that you have an environment to work in, let's walk through how to initialize the processing task. We'll use an 
example of our `breastfeeding_promotion` systematic review used to model `lack_of_breastfeeding_promotion`.

With your environment activated, make a new git branch for your new data.  To do this: `cd` into the `auxiliary_data_processing` 
directory (the one that contains this file `TUTORIAL.md`) and type `git checkout -b new_data/<ENTITY_NAME>_<MEASURE>`. 
In our breastfeeding_promotion example, we're modeling the exposure of the lack_of_breastfeeding_promotion coverage gap, 
so we would run:

```
git checkout -b new_data/lack_of_breastfeeding_promotion_exposure
```

Having made your git branch, you'll now want to initialize exposure and relative risk. You should process exposure first.
If you want to have an intervention that affects some entity, you'll need to have a relative risk between your risk and 
that entity. 

We'll walk through how to handle both measures.

####`Exposure`
How you initialize exposure depends on whether or not you have data. By data, we mean a data directory like we walked 
through in step 1. 

To initialize the auxiliary data processing task, run 
```
adp initialize <ENTITY_NAME> <ENTITY_TYPE> <MEASURE>
```

**If you have data**, you'll need to specify where the tool can find your data. You'll use the `-i` or 
`--input-data-path` flag to do this:
```
adp initialize <ENTITY_NAME> <ENTITY_TYPE> <MEASURE> -i <DATA_DIRECTORY>/<DATA_NAME>
```

In our example, we're modeling the `exposure` (the MEASURE) of the `coverage_gap` (the ENTITY_TYPE) named 
`lack_of_breastfeeding_promotion` (the ENTITY_NAME), so if we did NOT have data we would run

```
adp initialize lack_of_breastfeeding_promotion coverage_gap exposure
```
 **If we have data,** we would run, 

```
adp initialize lack_of_breastfeeding_promotion coverage_gap exposure -i <DATA_DIRECTORY>/breastfeeding_promotion
```
or equivalently,
```
adp initialize lack_of_breastfeeding_promotion coverage_gap exposure --input-data-path=<DATA_DIRECTORY>/breastfeeding_promotion
```

###`Relative risk`
Having initialized exposure, you can now add relative risk. 

Again you may or may not have data. 

The important difference in working with `relative_risk` instead of `exposure` is that **you should provide an affected 
entity with the -e flag for all adp commands**. Because of this, we require that you process relative risk for a single 
affected cause or risk at a time. Don't try to provide multiple affected entities or no affected entities at once - this 
program will not be happy about your work. 


To initialize the auxiliary data processing task, run 
```
adp initialize <ENTITY_NAME> <ENTITY_TYPE> <MEASURE> -e <AFFECTED_ENTITY
```

**If you have data**, you'll need to specify where the tool can find your data. You'll use the `-i` or 
`--input-data-path` flag to do this:

```
adp initialize <ENTITY_NAME> <ENTITY_TYPE> <MEASURE> -i <DATA_DIRECTORY>/<DATA_NAME> -e <AFFECTED_ENTITY
```

For our breastfeeding example, let's assume we're processing the relative risk of 
`lack_of_breast_feeding_promotion` on the affected entity `non_exclusive_breastfeeding`. We're modelling the 
`relative_risk` (the MEASURE) of the `coverage_gap` (the ENTITY_TYPE) named `lack_of_breastfeeding_promotion` (the 
ENTITY_NAME) with the `non_exclusive_breastfeeding` (the AFFECTED_ENTITY) so if we did NOT have data we would run:

```
adp initialize lack_of_breastfeeding_promotion coverage_gap relative_risk -e non_exclusive_breastfeeding
```

**If we have data,** we would run, 

```
adp initialize lack_of_breastfeeding_promotion coverage_gap relative_risk -i <DATA_DIRECTORY>/breastfeeding_promotion -e non_exclusive_breastfeeding
```
or, equivalently
```
adp initialize lack_of_breastfeeding_promotion coverage_gap relative_risk --input-data-path=<DATA_DIRECTORY>/breastfeeding_promotion --affected_entity non_exclusive_breastfeeding
```

#### Okay, so what happened when we ran initialize?
For the sake of this tutorial, let's assume that you have initialized both `exposure` and `relative_risk`. 

**For your actual work, please finish the whole process of `initialize`, `validate`, and `upload` for `exposure` first 
and then do the same for `relative_risk`.**

Let's look at the directory containing the `auxiliary_data_processing` package (again, the one containing this tutorial). 

The Auxiliary Data Processing tool has done a few things. 

If you provided data, it has verified that all your data files are in order and that your `version.yaml` is properly 
formatted. It has then copied all that data from your <DATA_DIRECTORY> into `auxiliary_data_processing/entities/<ENTITY_NAME>/exposure/data/` 
or, `auxiliary_data_processing/entities/<ENTITY_NAME>/relative_risk/<AFFECTED_ENTITY>/data`. You should be able to `cd` 
into those directories and see the copied files.

In both cases, it has also created a `processing.py` file in the same directory. This file is a template that you will 
need to fill out in order to continue processing your data. The file contains some fields specific to the `entity_type` 
and `measure` you provided that you need to fill out and a `process_data` function that you need to write.

Going back to our breastfeeding promotion example for exposure, we should see the following if we provided data:
```
auxiliary_data_processing/
    auxiliary_data_processing/
        app/
            ...stuff you don't care about
        entities/
            lack_of_breast_feeding_promotion/
                exposure/
                    data/
                        ...the data you provided
                    processing.py
                relative_risk/
                    non_exclusive_breastfeeding/
                        data/
                            ...the data you provided
                        processing.py
                    ...maybe other affected entity/
                        data/
                            ...some data
                        processing.py
            ...maybe other entities
    .gitignore
    README.md
    setup.py
    TUTORIAL.md
```
and this if we did not provide data:
```
auxiliary_data_processing/
    auxiliary_data_processing/
        app/
            ...stuff you don't care about
        entities/
            lack_of_coverage_of_calcium_supplementation/
                exposure/                    
                    processing.py
                relative_risk/
                    non_exclusive_breastfeeding/
                        processing.py
                    ..maybe other affected entity/
                        processing.py
            ...maybe other entities
    .gitignore
    README.md
    setup.py
    TUTORIAL.md
```

If you provided data, `processing.py` will already contain your name and email. If not, the initialize process will ask 
your name and email. 


**Note:** Since the initialize requires copying data and creating directories, re-initializing data that already exists will
be rejected to avoid accidentally overwriting files or leaving directories in a dirty state. If a replacement is
explicitly desired, `adp` should be called with a `--replace` option as in `adp initialize --replace`. This will result
in all current data being deleted and the process then proceeding normally. This ensures the process begins from a clean
state.


### 3. Filling out the `processing.py` file.

Now that we've initialized things and gotten our template `processing.py`, we'll need to fill it out. 

We are iteratively building modeling tools within `auxiliary_data_processing/models` that can be used in your `processing.py`. 
Please see the breastfeeding_promotion `processing.py` module for examples of how to incorporate these tools. 
Additionally, there is a `TUTORIAL` within the `models` directory showing how to make model diagnostics. 

Let's continue with our example of `lack_of_breastfeeding_promotion` exposure example. At this point, our `processing.py` 
file generated by `intialize` will look like this:

```python
"""File for processing raw data for test.exposure."""
import os

from gbd_mapping import causes, risk_factors

OWNER = ''  # Your full name.
OWNER_EMAIL = ''  # Your UW email

# Include metadata about the entity you're modelling here
ENTITY_NAME = '<ENTITY_NAME>'
ENTITY_TYPE = '<ENTITY_TYPE>'
MEASURE = 'exposure'
GBD_ID_TYPE = 'rei_id'
GBD_ID = ''  # Replace this with the GBD risk id if one exists. 

DISTRIBUTION = None  # One of {"dichotomous", "polytomous"}
# Replace the following with names of the actual categories for polytomous coverage gaps
LEVELS = {"cat1": "exposed",
          "cat2": "unexposed", }
RESTRICTIONS = {"male_only": False,
                "female_only": False,
                "yll_only": False,
                "yld_only": False, }

# Expected Columns
# ----------------
#
# age_group_id : Should contain the values
#                [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 30, 31, 32, 235]
#                or the id 22, representing all ages.
#
# sex_id : Should contain the values [1, 2] representing men and women respectively
#          or the value 3, representing both.
#
# location_id : Should contain the GBD location ids representing your data, or 1, the global location
#               id indicating that the data does not vary by location.
#
# year_id : Should contain the years represented by the data or 1, indicating the data does
#           not vary by year.
#
# rei_id : Probably `np.NaN`. However, if this data corresponds to something in the risk hierarchy,
#          include the corresponding rei_id here.
#
# coverage_gap : A column containing the name of the coverage gap you're modelling.
#
# measure : Column containing the string 'exposure'
#
# parameter : Column containing the names 'cat1', 'cat2', ..., 'catN' where 'N' is the 
#             number of exposure categories in the data.
#
# draw_0, draw_1, ..., draw_999 : One column for each draw represented by the data.


def process_data():
    """Code for transforming raw data into processed outputs"""
    processed_data = None  # Write your data processing code here

    return processed_data


if __name__ == "__main__":
    process_data()

```

There are two main parts to this file. 
1. The first is a section with variables that need to be
assigned values. These describe metadata associated with the entity you're modelling. You can see above that we have:

    - `DATA_DIR`: the path to the raw data directory. It will only show up in the `processing.py` file if you
    provided raw data. You should load your data using this variable.
    - `ENTITY_NAME`: the name of the entity you provided. It will be automatically filled for you.
    If you made a mistake, delete the entire entity directory and rerun `adp initialize`.
    - `ENTITY_TYPE`: the type of entity you provided. It will be automatically filled for you.
    - `MEASURE`: the name of the measure you're modelling. It will be automatically filled for you.
    - `GBD_ID_TYPE`: e.g., `rei_id` if there is any matching GBD_ID, otherwise empty
    - `GBD_ID`: likely to be empty, but if there's any, please specify it here. 

2. The remainder of the variables are specific to the `entity_type` and `measure` we're modeling. For the 
`exposure` of a `coverage_gap` we have:

    - `DISTRIBUTION`: either dichotomous (two categories, exposed and not exposed), or polytomous (multiple categories).
    - `LEVELS`: if the coverage gap is dichotomous, the default will do.  If polytomous, `LEVELS` should be a dictionary
    of category number, category name pairs.  
    Suppose, for instance, we had three supplementation categories for 
    our `lack_of_coverage_of_calcium_supplementation` coverage gap: `no_supplementation`, `cheap_calcium_tablets`, 
    and `calcium_supervitamins`, then we would have 
        ```
        LEVELS = {"cat1": "no_supplementation",
                  "cat2": "cheap_calcium_tablets",
                  "cat3": "calcium_supervitamins", }
        ```
        *Note: `LEVELS` should be ordered from worst to best.  If no ordering is clear, `vivarium` is probably not
        equipped to handle the coverage gap* 
    
    - `RESTRICTIONS`: whether this coverage gap targets particular sexes or kinds of burden. Ask someone if you 
    think you need to modify this.
    
    The following are only provided for relative risk and not for exposure: 
    - `AFFECTED_CAUSES`: The causes impacted by this coverage gap, if any.  
    - `AFFECTED_RISKS`: The risk factors impacted by this coverage gap, if any.
    - `AFFECTED_ENTITY_GBD_ID_TYPE`: For the relative risk, you need to specify either affected cause or risk, and fill up here with either `rei_id` or `cause_id`
    - `AFFECTED_ENTITY_GBD_ID`: Fill it up here with the matching GBD ID.
 
    As we mentioned earlier, you should process only one pair of (entity_name, affected_entity) for the relative risk 
    each time. i.e., we expect you fill out **only one** of `AFFECTED_CAUSES` or `AFFECTED_RISKS` and leave the other as it is.

With our updated metadata this looks like:

```python
"""File for processing raw data for lack_of_iron_supplementation_during_pregnancy.exposure."""
"""File for processing raw data for lack_of_breastfeeding_promotion.exposure."""
import os
import pandas as pd
import numpy as np

from db_queries import get_location_metadata
from gbd_mapping import causes, risk_factors, covariates
from auxiliary_data_processing.models.least_squares import OLS_model

DATA_DIR = os.path.join(os.path.dirname(os.path.abspath(__file__)), "data")


OWNER = YOUR NAME'  # Your full name.
OWNER_EMAIL = 'YOUR EMAIL'  # Your UW email

# Include metadata about the entity you're modelling here
ENTITY_NAME = 'lack_of_breastfeeding_promotion'
ENTITY_TYPE = 'coverage_gap'
MEASURE = 'exposure'
GBD_ID_TYPE = 'rei_id'
GBD_ID = ''  # Replace this with the GBD risk id if one exists. 

DISTRIBUTION = "dichotomous"  # One of {"dichotomous", "polytomous"}
# Replace the following with names of the actual categories for polytomous coverage gaps
LEVELS = {"cat1": "exposed",
          "cat2": "unexposed", }
RESTRICTIONS = {"male_only": False,
                "female_only": False,
                "yll_only": False,
                "yld_only": False, }

# Expected Columns
# ----------------
#
# age_group_id : Should contain the values
#                [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 30, 31, 32, 235]
#                or the id 22, representing all ages.
#
# sex_id : Should contain the values [1, 2] representing men and women respectively
#          or the value 3, representing both.
#
# location_id : Should contain the GBD location ids representing your data, or 1, the global location
#               id indicating that the data does not vary by location.
#
# year_id : Should contain the years represented by the data or 1, indicating the data does
#           not vary by year.
#
# rei_id : Probably `np.NaN`. However, if this data corresponds to something in the risk hierarchy,
#          include the corresponding rei_id here.
#
# coverage_gap : A column containing the name of the coverage gap you're modelling.
#
# measure : Column containing the string 'exposure'
#
# parameter : Column containing the names 'cat1', 'cat2', ..., 'catN' where 'N' is the 
#             number of exposure categories in the data.
#
# draw_0, draw_1, ..., draw_999 : One column for each draw represented by the data.

def process_data():
    """Code for transforming raw data into processed outputs"""
    raw_data = # Load data here

    processed data = # Write your data processing code here

    return processed_data


if __name__ == "__main__":
    process_data()
```
##### some important notes :

1. On naming:

    The tool will yell at you if you get the `<ENTITY_TYPE>` and/or `<MEASURE>` wrong, but it can't predict
    what the names of things should be. Names are very important! Some guidelines on entity names:
    
    - **NO ACRONYMS**. There are a couple reasons for this. The first is that acronyms are confusing jargon. Most 
     of us are not experts in even one of the diseases we're modelling and acronyms serve as a big barrier to entry
     in understanding what's going on. Second, we're going to be producing dozens or hundreds of models for the 
     CoNIC project across many different health domains and acronyms often collide. For example, NTDs are both
     Neglected Tropical Diseases and Neural Tube Defects, both of which we might deal with in CoNIC models.  
    - The name should be all lowercase.
    - The name should contain no special characters and be separated by underscores rather than spaces.
    
    The latter will *probably* be enforced by the tool by the time you're reading this.

2. Debugging 

    If you're having trouble and you want to investigate, you can run `adp` under the python debugger with
    ```
    adp --pdb <SUBCOMMAND> <SUBCOMMAND_ARGS>
    ```
    In our example, this would be 
    ```
    adp --pdb initialize lack_of_breastfeeding_promotion coverage_gap exposure -i <DATA_DIRECTORY>/breastfeeding_promotion
    ```
    This works for the `validate` and `upload` subcommands detailed in the rest of this document as well. 

### 4. Validate your work
Validation is to ensure your processed data has all the expected columns and format in order to be processed as if it 
were pulled from GBD. 

For this step, you will run 
```
adp validate <ENTITY_NAME> <MEASURE>` (with `-e <AFFECTED_ENTITY>` for relative_risk)
```
Using our breastfeeding promotion example, this would be the following for `exposure`:
```
adp validate lack_of_breastfeeding_promotion exposure 
```
 and for `relative_risk`:
```
adp validate lack_of_breastfeeding_promotion relative_risk -e non_exclusive_breastfeeding
```

Once validation is done, it will tell you that you can move on to `upload` if everything checks out. 

### 5. Upload your work
The final step to ensure your auxiliary data can actually be used in a simulation is to upload it. This is an involved step
with a lot of things going on behind the scenes, so `upload` may take some time to finish. Just be patient :) 

The following is brief description of what happens in this process. 

First, it will check that you're on cluster and raise an error if not. Then it will perform a series of additional checks,
 e.g., did you do everything correctly and in the proper order (`exposure` -> `relative_risk`), are you trying to override 
existing data that has already been uploaded to the auxiliary data folder, etc. 

Once these checks are done, it will copy all the original data in your `auxiliary_data_processing/entities/<ENTITY_NAME>/<MEASURE>` 
folder to our `auxiliary data folder/01_original_data` folder with relevant information in a `README.rst`. Then it will 
run `processing.py` to generate your data as an hdf file, which will be stored in `auxiliary data folder/02_processded_data`,
also with a `README.rst` containing relevant information.

Because you've added new data, we also need to update our `gbd_mapping`. This is all done in a temporary conda environment 
in a temporary folder. Once your updated `gbd_mapping` is pushed to github, this temporary environment and folder will be 
 cleaned up. You will need to provide your password to stash and to github during the process. 
 
Now that you have an overview of what `upload` will do, let's see how to run it. Again, you should upload exposure before
relative risk. 

Simply run
```
adp upload <ENTITY_NAME> <MEASURE>` (with `-e <AFFECTED_ENTITY>` for relative_risk).
``` 

Using our breastfeeding promotion example, this would be the following for `exposure`:
```
adp upload lack_of_breastfeeding_promotion exposure
```
and for `relative_risk`:
```
adp upload lack_of_breastfeeding_promotion relative_risk -e non_exclusive_breastfeeding
```

When everything is done, you will see a message at the end like the following
```
Data uploaded! Don't forget to submit a PR
```

This is a reminder that there is one more step before you're done. Once you've successfully uploaded your data, we want 
to make sure your branch of auxiliary data processing is properly stored. Go to the [auxiliary_data_processing repository](https://stash.ihme.washington.edu/projects/CSTE/repos/auxiliary_data_processing/browse)
and submit a pull request from your branch to master. Add the entire engineering team as reviewers to your pull request. 
One or more will review and once approved, will merge it to the master branch. **DO NOT FORGET TO DO THIS!** We need a 
central record of all the work you've just done to upload this data. 

**Note:** As with initialize, since upload requires copying data and creating directories, re-uploading data that
already exists will be rejected to avoid accidentally overwriting files or leaving directories in a dirty state. If a
replacement is explicitly desired, `adp` should be called with a `--replace` option as in `adp upload --replace`. This
will result in all current data being deleted and the process then proceeding normally. This ensures the process begins
from a clean state.

