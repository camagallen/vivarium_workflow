[Back to Model Development](Model_Development.md)

#Concept Model
The Concept Model is the currently planned method for model implementation, formalized in the <em>Concept Model Document</em> (see below). It is intended first as an agreement between the Software Engineer and Researcher that defines the requirement of the model. Over the course of the research process, the Concept Model (and Document) may evolve as troubleshooting is required, but any changes should be immediately discussed and agreed upon by the interested parties.

## Concept Model Templates
[Researcher Template](docs_andTemplates/concept_model_researcher_template.docx)
[Engineer Template](docs_andTemplates/concept_model_software_dev_template.docx)
[Concept Model Example (Researcher)](docs_andTemplates/BFP_concept_model_example_Researcher.pdf)


# Concept Model Documentation: More Information about the Template
The following information supplements the templates above.

## Intervention Definition<
Provide a high level description of the intervention and what it targets.
This definition should include the case definition(s) for the intervention and its targets here.&nbsp; These definitions will drive the rest of the modeling process. It should include final outcomes (mortality/disability), diseases, risks, important covariates, and interventions.&nbsp; When thinking about the rest of the model, one&nbsp;should try to keep it as simple as possible while still capturing all the effects of interest.

## Concept Model Diagram&nbsp;<
This diagram serves as a graphical representation of the&nbsp;model at a high level.&nbsp; Its purpose is as a discussion aid and communication tool.&nbsp; It helps separate the model into pieces that we can talk about concretely and drives the final implementation of the model.

## Example Concept Diagram
Download and open&nbsp;<ac:link><ri:attachment ri:filename="BreastfeedingPromotion_example.html" /></ac:link>&nbsp;(it should automatically open in&nbsp;<a style="letter-spacing: 0.0px;" href="http://draw.io/">draw.io</a>)

Most of the fields included in this section are exposed parameters in the simulation, meaning they&nbsp;can be changed at will once the model is implemented.&nbsp; Filling them prior to the build facilitates conversations about model run time and outstanding data considerations.&nbsp;

### Setting Time Scale and Step Size
he decision here is driven by the time scale the&nbsp;intervention takes effect over and the results desired for reporting.

This is frequently a tricky decision to make.&nbsp; Along with the model's&nbsp;time span, it determines the number of calculation steps in the simulation and therefore has a large impact on the run time of the&nbsp;model.&nbsp; The primary determining factor, however, is model accuracy.&nbsp; When&nbsp;modeling populations that are binned very finely (e.g. the early neonatal groups), we need to take small time steps to resolve events that occur during those periods.&nbsp; Additionally, if the&nbsp;model contains events with large rates (e.g. remission of infectious diseases), take time steps that are too large will massively skew disease prevalence (and therefore cause specific mortality) in the model.&nbsp; In initial model development it is better to be conservative and select a small step size relative to the&nbsp;model.&nbsp; Once initial model development and validation is complete, we can do sensitivity analysis to determine a step size that balances run time with plans for model scale up.

## Locations
Include a list of 1-5 locations for the initial model.&nbsp; Additional locations can be added if we decide to scale up the model due to interest from internal clients (e.g. our brain trust, or Abie, or other internal modelers we consult with) or external funders.<br /> <br /> There are two good ways to decide what locations to pick.&nbsp; The first is if the grant funders have a particular interest in certain locations.&nbsp; The second is to use GBD compare to get a good idea of where the&nbsp;intervention might have the largest impact. If the&nbsp;intervention targets a disease directly, look for places with a large proportion of DALYs/Deaths attributable to that disease.&nbsp; If the&nbsp;intervention targets a GBD risk, look for places where the burden of the risk-affected diseases is high and the PAF associated with the cause risk pair is also large.&nbsp; Existing coverage (existing/current use of the intervention) should be taken into account as well, since it reduces the potential impact of the intervention.
Initial Population: size, age range, other considerations
his has a large impact on the run time of the model.&nbsp; You should select a population size that is large enough so that uncertainty does not dominate the effect size of your intervention, but no larger.&nbsp; &nbsp;&nbsp;

You should inform this decision by considering the ages affected by the risks, diseases, and interventions in the model as well as the time horizon you want to report results for.
his decision is mostly driven by the results you want to report. It also has implications for how the fertility model, if present, will function.

## Fertility Model
One of:
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li>None &ndash; A closed cohort model</li>
<li>Deterministic &ndash; A set number of individuals will be added to the simulation every time step.&nbsp; If you select this option, you should specify the number of people to be added per year.</li>
<li>Crude Birth Rate &ndash; This uses a population level fertility rate from GBD to determine the number of individuals to add each time step.&nbsp; If you select this model, your initial population end age and the population exit age must be the same.</li>
<li>Age specific fertility &ndash; This model determines the number of individuals to add each time step based on the number of women of child bearing age in the simulation.&nbsp; It requires modeling the full population age range in order to work correctly.</li></ul></li></ul></li></ul></li></ul></li></ul>
he decision here is determined by the structure of your intervention, your reporting needs, and the need for accuracy and model speed. Age specific fertility is the truest model of population dynamics but may require simulating large numbers of individuals that are unimportant to the intervention effects.&nbsp; Crude birth rate is a good trade off, but has issues when simulating small age subsets of the population.&nbsp; Any model that uses a fertility component must have 0 specified as the population age start.
Intervention Model
The purpose of this section is to lay out the model for the intervention in detail.&nbsp; There are a few high level pieces that will always need to be included, but much of this section can vary widely between interventions.<br /> <br /> Based on deadline considerations, you should generally split this into two sections.&nbsp; One for a minimal model implementation (think: what if we magically shifted intervention coverage from 10% to 60% over 3 years with a linear ramp), and one for a detailed implementation strategy (e.g. when someone comes in for a doctor&rsquo;s visit, we perform a measurement of their risk exposure.&nbsp; Based on the outcome of that measurement, and perhaps other criteria, we enroll them in a clinical trial of a new drug.&nbsp; They fill their prescriptions every once in a while and generally take their medications.&nbsp; Sometimes there are adverse events that cause them to stop though).
In both the minimal model and the detailed model, you must address all of the following:
Intervention Effect
How does your intervention effect its targets? Is the effect additive, multiplicative, etc.?&nbsp; Does the size of the effect depend on the quality of treatment? On how long someone has been receiving the intervention?&nbsp; If so, how?&nbsp; Include equations and graphs where possible.
Are the intervention targets specified in terms of something GBD models directly? If not, you should include a brief description of the targets and reference the relevant disease or risk section where you lay out the alternative modeling strategy for the intervention targets.
Existing Coverage
Is there already coverage of the intervention in your target populations?&nbsp; How should we account for it?
Treatment Algorithm
How do we alter the coverage of the intervention in the target population?&nbsp; When does your change go into effect? Is it rolled out over time? Is it given to people during particular events (the onset of a particular disease, or a visit to a health care facility? For complex treatment algorithms, think from the perspective of what can happen to an individual. Equations, graphs, and diagrams are often useful here.
<p>&nbsp;
We have already implemented a common intervention strategy called the coverage gap that is useful for particular kinds of interventions.&nbsp; The criteria for using this strategy are:
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li>There is existing coverage of your intervention in the population.&nbsp; (We can use this strategy without existing coverage, but it is often unnecessary).</li>
<li>The intervention target is a rate (e.g. disease incidence, mortality, healthcare utilization) or the intervention target is dichotomous (e.g. a risk where you&rsquo;re either exposed or unexposed).</li></ul></li></ul></li></ul></li></ul>
## Scenarios
What intervention scenarios do you want to explore? What parameters would be useful for that exploration/sensitivity analysis?

### Components
What components are used to implement the intervention?&nbsp;
How do you include them in the simulation?
What columns do they create in the population table?&nbsp; What do the columns mean?
What value pipelines do they create? What do the values coming out of the pipelines mean?

### Parameters
List all available parameters in the format:
<em>parameter_name</em> &ndash; default parameter value [parameter range either as minimum and maximum or as a list of values]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; parameter description

## Risk Entities
Vivarium has the infrastructure to model using any risks in the GBD hierarchy.&nbsp;
Data Sources
What data sources are used to inform your risk model?
This section is only important to fill out if you deviate from our standard data sources (which will be returned from vivarium_inputs tools):
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li>exposure &ndash; get_draws(source=&rsquo;exposure&rsquo;)</li>
<li>exposure standard deviation [only relevant for continuously modeled risks] &ndash; get_draws(source='exposure_sd')</li>
<li>relative risk &ndash; get_draws(source='rr')</li>
<li>population attributable fraction &ndash; get_draws(source='burdenator')</li></ul></li></ul></li></ul></li></ul>

### Components
What components are used to implement the risk and risk effects?&nbsp;
How do you include them in the simulation?
What columns do they create in the population table?&nbsp; What do the columns mean?
What value pipelines do they create? What do the values coming out of the pipelines mean?
This section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation.

### Parameters
List all available parameters in the format:
<em>parameter_name</em> &ndash; default parameter value [parameter range either as minimum and maximum or as a list of values]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; parameter description
This section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation or state that no parameters are available.
Cause Entities
Vivarium has the infrastructure to model using causes at any level in the GBD hierarchy. However, it is recommended to model GBD causes at the most detailed level to avoid problems with&nbsp;missingness in the GBD cause hierarchy.
Like risks, tools from vivarium_inputs can be used to pull and inspect the data for the models.&nbsp; You should document your findings in the following format:
Modeling Strategy
This decision will be driven by data availability, and disease epidemiology.&nbsp;There are many causes that this list will be unable to handle.&nbsp; In such a situation, you should detail an appropriate strategy.&nbsp; Causes with PAF of one relationships with modeled risks are the most frequent example. There are also situations where you might have multiple causes in the model with overlapping definitions.&nbsp; For example, diabetes and chronic kidney disease due to diabetes.
<h5 style="margin-left: 120.0px;">Standard Options</h5>
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li>SI &ndash; Short for susceptible-infected.&nbsp; This modeling strategy is appropriate for causes where people never recover once they enter into a with condition state.&nbsp; Example: Ischemic Heart Disease</li>
<li>SIS &ndash; Short for susceptible-infected-susceptible.&nbsp; This modeling strategy is appropriate for causes where individuals can have multiple cases over the course of their lives.&nbsp; Example: Diarrheal Diseases</li>
<li>SIR &ndash; Short for susceptible-infected-recovered.&nbsp; This modeling strategy is appropriate for causes where individuals can only have a single case, but do not stay in the with condition state forever.&nbsp; Example: Measles</li>
<li>Neonatal &ndash; This modeling strategy is appropriate for causes that an individual is born into the with condition state with and never recovers from.&nbsp; Example: Preterm birth</li></ul></li></ul></li></ul></li></ul>

## Data Sources
What data sources are used to inform your cause model?
his section is only important to fill out if you deviate from our standard data sources (which will be returned from vivarium_inputs tools).&nbsp;
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li><strong>incidence</strong> : calculated as raw incidence / (1 &ndash; prevalence)
<ul>
<li>&nbsp;raw_incidence : get_draws(source=&rsquo;como&rsquo;)</li></ul></li>
<li><strong>prevalence</strong> : get_draws(source=&rsquo;como&rsquo;)</li>
<li><strong>birth prevalence</strong> : get_draws(source=&rsquo;como&rsquo;)</li>
<li><strong>cause specific mortality</strong> : calculated as deaths due to cause / population size
<ul>
<li>deaths due to cause : get_draws(source=&rsquo;codcorrect&rsquo;)</li>
<li>&nbsp;population size : db_queries.get_population()</li></ul></li>
<li><strong>excess mortality</strong> : calculated as cause specific mortality / prevalence</li>
<li><strong>disability weight</strong> : aggregated from seqeulae according by sum_over_sequelae(sequela prevalence * sequela disability weight)
<ul>
<li>sequela prevalence &ndash; get_draws(source=&rsquo;como&rsquo;)</li>
<li>seqeula disability weight &ndash; flat file in auxiliary data sourced from GBD</li></ul></li></ul></li></ul></li></ul></li></ul>

### Components
What components are used to implement the cause model?&nbsp;
How do you include them in the simulation?
What columns do they create in the population table?&nbsp; What do the columns mean?
What value pipelines do they create? What do the values coming out of the pipelines mean?
his section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation.

### Parameters
List all available parameters in the format:
<em>parameter_name</em> &ndash; default parameter value [parameter range either as minimum and maximum or as a list of values]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; parameter description
his section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation or state that no parameters are available.

### Model Outputs
There are two kinds of outputs to consider here: outputs used for model validation/sensitivity analysis and outputs used to produce final results.&nbsp; You should label what they&rsquo;ll be used for.&nbsp; Recording some kinds of data in the simulation is sometimes quite costly in terms of computation time and memory usage.&nbsp; We can afford the extra resources when doing small scale runs for validation, but need to be careful when running models at scale.

### Stratification
How should this output be stratified? By age?&nbsp; By sex? By risk exposure level or treatment category?
You should think fairly carefully about this.&nbsp; We will typically construct observers that report numerators and denominators separately in entirely stratified bins. If you want to observe very finely stratified outcomes, you may end up in situations where your denominator (e.g. your sample size) is too small to be representative.
Observer Component
What component produces the appropriate outputs?
How do you include it in the simulation?
(For interactive observers) What columns do they create in the population table?&nbsp; What do the columns mean?
(For interactive observers) What value pipelines do they create? What do the values coming out of the pipelines mean?
Is this observer parameterized?&nbsp; If so, what parameters are available.
<h1 style="margin-left: 30.0px;">Model Development Meeting(s)
Once the researcher completes a draft of the Concept Model &nbsp;the intervention literature and GBD models involved,&nbsp;reach out to the team's Project Officer to schedule a Concept Model Development Meeting.&nbsp;<br /><br />This is a formal design meeting with the following goals:
<ol>
<li style="list-style-type: none;background-image: none;">
<ol>
<li style="list-style-type: none;background-image: none;">
<ol>
<li>Explain the intervention and GBD models involved to the engineer responsible for the model.&nbsp;If at all possible, the researcher should send a summary ahead of time so that this part can proceed mostly as a Q&amp;A.</li>
<li>Collaboratively develop a detailed <ac:link ac:anchor="ConceptModelDiagram"><ac:plain-text-link-body><![CDATA[concept model diagram]]></ac:plain-text-link-body></ac:link> annotated with all necessary data sources.&nbsp;&nbsp;</li>
<li>Identify any gaps in data, understanding, or simulation infrastructure that need to be addressed before proceeding.</li></ol></li></ol></li></ol>
The concept model we produce from this meeting essentially creates a&nbsp;<strong>contract</strong>&nbsp;between the research staff and the engineering staff.&nbsp; It represents a shared understanding of the model to be built.&nbsp;
Models will inevitably change as we do more research, gather more data, or our clients ask for more&nbsp;things.&nbsp;<strong>The first step in addressing a change to the model is to update the concept model diagram in consultation with all research and engineering stakeholders.&nbsp;</strong>In order for us to be responsive to change, the change must be highly visible and make sense to everyone involved.
