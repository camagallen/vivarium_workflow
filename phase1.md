[Back to Model Development](Model_Development.md)

# Background Research
The longest and most critical stage in the modeling process is the background research.&nbsp;The goal of this phase is to gather a thorough understanding of the health intervention&nbsp;literature and to connect it with outcomes produced in the Global Burden of Disease. That means researching the health&nbsp;intervention itself and linking it to GBD causes &amp; risk factors. The most important question to answer is this:&nbsp;<em>is there enough evidence to develop a defensible model for this intervention?</em>

## Searching For Background Information 
### Systematic Search 
Systematic Searches are intended as a rapid method for determining the viability of an approach (i.e. &quot;is there enough reliable evidence to build a model using this method?&quot;). Unlike a Systematic Review, the goal of the systematic search is not to track details. Rather, the goal is to track what <strong>type</strong> of information is available and where. Often this search will reveal that not enough research has been done. However, if enough information can be found, it will already contain a number of references that can be included in the systematic review.

### Systematic Search Template
[Systematic Search](docs_andTemplates/Systematic_Search.pdf)

## GBD Causes and Risk Factors
For intervention modeling in Vivarium, each intervention must be tied to at least one GBD cause and/or risk factor. You should review how GBD handles the outcomes of the intervention.

Risk exposure (e.g. an increase in breastfeeding promotion reduces exposure to non-exclusive&nbsp; and discontinued breastfeeding).
Disease incidence (e.g. a vaccine for a diarrheal disease pathogen will decrease the incidence of diarrheal diseases)
Excess Mortality (e.g. thermal care for infants will reduce the excess mortality rate for neonatal&nbsp; causes)
You should try to gain an understanding of the full pathway from your intervention to childhood mortality. For example, the breastfeeding promotion intervention reduces exposure to non-exclusive and&nbsp; discontinued breastfeeding which reduces the incidence rates of diarrheal diseases and lower&nbsp;respiratory infections which reduces the overall mortality rate which reduces the number of deaths.
It is important to target the earliest point in the pathway. Using the breastfeeding promotion example, we want to target the suboptimal breastfeeding risks, not the diarrhea/LRI causes.&nbsp;
Below are the best resources to explore GBD risks and causes. Note that some of this information is being aggregated on the&nbsp;<ac:link><ri:page ri:content-title="GBD Data Availability" /></ac:link>&nbsp;page
<p style="margin-left: 90.0px;">1) GBD compare (<a href="https://vizhub.healthdata.org/gbd-compare">https://vizhub.healthdata.org/gbd-compare</a>). Good first place to review cause and risk list. Looking at PAFs are particularly helpful, if your intervention targets risks.&nbsp;&nbsp;&nbsp;
<p style="margin-left: 90.0px;">2) GBD capstone appendices. Once you know what causes and/or risks are important to your intervention, you need to dig into how GBD treats them. The GBD 2017 appendices are saved as PDFs in the following folders. If you're researching a cause, I'd almost always start with the nonfatal appendix, then read the Cause of Death (CoD) one as necessary.&nbsp;

Once you know generally how the causes/risks are modeled, it's sometimes helpful to dig into the weeds and use GBD's internal model vetting tools. 

For example, looking at a model in epi viz 

GBD modelers - Once you have reviewed the methods appendices, you may have followup questions to ask the modelers themselves.&nbsp;They are literally the world's&nbsp;leading experts in how GBD thinks about particular risks and causes, and are probably just a couple offices away.&nbsp;

# Useful Resources 

<p>WHO manuals - Most important child health interventions are the subject of WHO guidelines/recommendations. Skimming the executive summary of the most recent/relevant report should be sufficient.&nbsp;
Cochrane Database - Important interventions generally have helpful Cochrane Reviews. If you're lucky, the WHO manual may already listed the most useful ones. If you don't find useful reviews here, try a general Google search (e.g. &quot;Vitamin A Supplementation Systematic Review&quot;)
Lives Saved Tool (LiST) For most child health interventions, the best place to start is to review how the Lives Saved Tool (LiST) models it. Their technical manual used to be at&nbsp;<a href="http://livessavedtool.org/images/documents/manuals/LiSTHelpEnglish_September2018.pdf">http://livessavedtool.org/images/documents/manuals/LiSTHelpEnglish_September2018.pdf</a>
## Goals of Background Research Process 
<strong>The primary goal of the background research is to determine a viable method for demonstrating how a given health intervention will change the health status of some location by linking that intervention to a change in some GBD metric.</strong>
For all GBD causes and risks that are involved in the intervention, you should understand the following:

<li style="list-style-type: none;background-image: none;">

Determine to what ages and sexes those causes and risks apply.&nbsp; Sometimes this will not line up with the way GBD bins ages for reporting.
Determine which measures are available for the causes and risks.  NOTE: The cause-risk pair measures might exist for morbidity, where the risk targets the incidence rate of the cause, or mortality, where the risk targets the excess mortality rate of the cause, or there might be effects for both.  
Determine how the causes and risks are related to each other.&nbsp;

Are there mediation pathways in the modeled risks (GBD currently only has mediation for adult metabolic risks, so shouldn't be a concern for CoNIC)
Are there PAF of 1 relationships between any of the cause risk pairs.&nbsp; A PAF of 1 can mean:
The cause and the risk are alternative definitions of the same thing. For example, the low birth rate and short gestation risk is an alternative definition of the neonatal preterm cause.
Exposure to the risk is a sufficient explanation for a prevalent case of the cause. The relationship between child wasting and protein energy malnutrition is probably an example of this.&nbsp;&nbsp;
Exposure to the risk is a necessary precondition for a prevalent case of the cause. An example would be the risk high systolic blood pressure and the cause chronic kidney disease due to hypertension  
Determine any discrepancies in the way GBD models the causes and/or risks targeted by an intervention and the way the literature reports the effect size of the intervention.&nbsp; For example the literature for the effect size of breastfeeding promotion might report that it reduces sub-optimal breastfeeding by X%.&nbsp; GBD reports discontinued breastfeeding as dichotomous (breastfeeding was continued or not) but reports non-exclusive breastfeeding as a 4 category risk with different levels of harm for each category.&nbsp;&nbsp;  You should have some idea of how to rectify these discrepancies.&nbsp; The GBD modeler(s) responsible for the cause or risk of interest are a great resource.

