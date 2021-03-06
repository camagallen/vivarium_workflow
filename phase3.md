[Back to Model Development](Model_Development.md)

# Data Processing
Based on concept model, corresponding data (baseline coverage/efficacy/cost etc.) will be collected. LiST is a good reference of detailed intervention definition and data source guidance, it's good to stick with LiST. 
<ol>
<li style="list-style-type: none;background-image: none;">
<ol>
For baseline coverage data, it's suggested to look up UbCov database first. If GBD already have intervention data we are interested in, directly extract them; otherwise, please check Macro_DHS/UNICEF_MICS surveys/WHO to see if their questionnaire or database contain information we want. The least way of collecting data is to do systematic review.
For systematic review, please use the following extraction and screening spreadsheets: <project_folder>/Literature/Intervention_reviews<br />This extraction pattern is helpful for future ST-GPR step which will be talked later. Meanwhile, don't forget to make PRISMA flow chart for recording review procedures.&nbsp;
When you are done with systematic review/data extraction, it can be helpful to write a  gap report
[Example Gap Report pending]

## Running Models to Expand Input Data
After data extraction, the next step is to process these external data sources so that they are properly stored and uploaded for use in vivarium simulations. This procedure is called auxiliary data processing which has a detailed tutorial:&nbsp;<a rel="nofollow" href="<repo_loc>/auxiliary_data_processing/browse/TUTORIAL.md" class="external-link"><repo_loc>/auxiliary_data_processing/browse/TUTORIAL.md</a>
Follow the tutorial instructions and choose proper methods based on your data source. If the extracted data is not sufficient or representative (usually from systematic review), it&rsquo;s necessary to do prediction for other country/year using extracted data as training data. Please select proper predictive model by comparing predicted values with true values. Commonly used predictive models in our team are but not limited to simple/multiple linear regression model, logistic regression model, generalized linear model, linear mixed effects model, ST-GPR etc. These models are just for you reference. If you could find more appropriate model to describe your data set, don&rsquo;t hesitate to discuss and use it.

## Auxilliary Data Processing
Before modeling can begin, the data must first be validated and cataloged by Vivarium's auxiliary data processing. Auxilliary Data inputs are data from external sources with info about shape of data, etcetera. The output is&nbsp;standardized, tagged data stored in /share/costeffectiveness/auxiliary_data. This process automatically updates Vivarium GBD mapping.
<h3 style="margin-left: 30.0px;">Notes</h3>
<p style="margin-left: 60.0px;">If you have never done this before, install auxiliary_data_processing though the instructions found at the following link. Then&nbsp;<strong>follow the tutorial</strong>&nbsp;(<a href="http://TUTORIAL.md">TUTORIAL.md</a> file in the repo):&nbsp;&nbsp;<a href="<repo_loc>/auxiliary_data_processing/browse"><repo_loc>/auxiliary_data_processing/browse</a>
<p style="margin-left: 60.0px;">NOTE - if you want to use Zane's old mixed effects regression tools for baseline coverage modelling (eventually, we'd use stGPR), see&nbsp;<a href="<repo_loc>/auxiliary_data_processing/browse/auxiliary_data_processing/models/MODEL_TUTORIAL.ipynb"><repo_loc>/auxiliary_data_processing/browse/auxiliary_data_processing/models/MODEL_TUTORIAL.ipynb</a>
[More on Auxilliary Data Processing Here](auxilliary_data_processing.md)

## Validation of Inputs
<ol>
Do the data have the expected characteristics?
Do the data target the correct age/sex groups?
etc...<br /><br /></ol>
