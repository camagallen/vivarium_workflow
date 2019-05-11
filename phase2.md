
<h1>Table of Contents</h1>
<p><ac:structured-macro ac:name="toc" ac:schema-version="1" ac:macro-id="179d822a-b3c1-4509-987f-f8c9b20a28ad"><ac:parameter ac:name="maxLevel">3</ac:parameter></ac:structured-macro></p>
<h1>Overview</h1>
<p style="margin-left: 30.0px;">The Concept Model is the currently planned method for model implementation, formalized in the <em>Concept Model Document</em> (see below). It is intended first as an agreement between the Software Engineer and Researcher that defines the requirement of the model. Over the course of the research process, the Concept Model (and Document) may evolve as troubleshooting is required, but any changes should be immediately discussed and agreed upon by the interested parties.</p>
<h1>See Also</h1>
<p style="margin-left: 30.0px;"><ac:link><ri:page ri:content-title="Effect Size Meta-analysis" /></ac:link></p>
<p style="margin-left: 30.0px;"><ac:link><ri:page ri:content-title="Costing" /></ac:link></p>
<p style="margin-left: 30.0px;"><ac:link><ri:page ri:content-title="Coverage Gaps" /></ac:link></p>
<h1>Concept Model Templates</h1>
<p style="margin-left: 30.0px;"><span style="font-size: 20.0px;letter-spacing: 0.0px;">Templates&nbsp;</span><ac:structured-macro ac:name="anchor" ac:schema-version="1" ac:macro-id="0e63c43c-b745-4bd8-9b17-a0a4156daa4f"><ac:parameter ac:name="">ConceptModelTemplate</ac:parameter></ac:structured-macro></p>
<table style="margin-left: 30.0px;"><colgroup><col style="width: 220.0px;" /><col style="width: 220.0px;" /></colgroup>
<tbody>
<tr>
<th>For Researchers</th>
<th>For Software Engineers</th></tr>
<tr>
<td>
<div class="content-wrapper">
<p><ac:structured-macro ac:name="view-file" ac:schema-version="1" ac:macro-id="6310c57b-51cc-402e-a857-182ae87251a3"><ac:parameter ac:name="name"><ri:attachment ri:filename="concept_model_researcher_template.docx" /></ac:parameter><ac:parameter ac:name="height">250</ac:parameter></ac:structured-macro></p>
<p><br /></p></div></td>
<td>
<div class="content-wrapper">
<p><ac:structured-macro ac:name="view-file" ac:schema-version="1" ac:macro-id="d7de1498-2585-4033-8d94-26f0efafa296"><ac:parameter ac:name="name"><ri:attachment ri:filename="concept_model_software_dev_template.docx" /></ac:parameter><ac:parameter ac:name="height">250</ac:parameter></ac:structured-macro></p></div></td></tr></tbody></table>
<h2 style="margin-left: 30.0px;">Examples</h2>
<p style="margin-left: 30.0px;"><ac:structured-macro ac:name="view-file" ac:schema-version="1" ac:macro-id="8fe2e0a9-29be-4781-b123-276786684da1"><ac:parameter ac:name="name"><ri:attachment ri:filename="BFP_concept_model_example_Researcher.pdf" /></ac:parameter><ac:parameter ac:name="height">250</ac:parameter></ac:structured-macro></p>
<h1>Concept Model Documentation</h1>
<p style="margin-left: 30.0px;">The following information supplements the templates above.</p>
<h2 style="margin-left: 30.0px;">Intervention Definition</h2>
<p style="margin-left: 30.0px;">Provide a high level description of the intervention and what it targets.</p>
<p style="margin-left: 30.0px;">This definition should include the case definition(s) for the intervention and its targets here.&nbsp; These definitions will drive the rest of the modeling process. It should include final outcomes (mortality/disability), diseases, risks, important covariates, and interventions.&nbsp; When thinking about the rest of the model, one&nbsp;should try to keep it as simple as possible while still capturing all the effects of interest.</p>
<h2 style="margin-left: 30.0px;">Concept Model Diagram&nbsp;<ac:structured-macro ac:name="anchor" ac:schema-version="1" ac:macro-id="f5b81467-63c1-413f-b1ed-b5442b9c0c36"><ac:parameter ac:name="">ConceptModelDiagram</ac:parameter></ac:structured-macro></h2>
<p style="margin-left: 60.0px;">This diagram serves as a graphical representation of the&nbsp;model at a high level.&nbsp; Its purpose is as a discussion aid and communication tool.&nbsp; It helps separate the model into pieces that we can talk about concretely and drives the final implementation of the model.</p>
<h3 style="margin-left: 60.0px;">Example Concept Diagram</h3>
<p style="margin-left: 60.0px;">Download and open&nbsp;<ac:link><ri:attachment ri:filename="BreastfeedingPromotion_example.html" /></ac:link>&nbsp;(it should automatically open in&nbsp;<a style="letter-spacing: 0.0px;" href="http://draw.io/">draw.io</a>)</p>
<h2 style="margin-left: 30.0px;">Fields and Definitions</h2>
<h3 style="margin-left: 60.0px;">Population Model</h3>
<p style="margin-left: 90.0px;">Most of the fields included in this section are exposed parameters in the simulation, meaning they&nbsp;can be changed at will once the model is implemented.&nbsp; Filling them prior to the build facilitates conversations about model run time and outstanding data considerations.&nbsp;</p>
<h4 style="margin-left: 90.0px;">Setting Time Scale and Step Size</h4>
<p style="margin-left: 120.0px;">The decision here is driven by the time scale the&nbsp;intervention takes effect over and the results desired for reporting.</p>
<p style="margin-left: 120.0px;">This is frequently a tricky decision to make.&nbsp; Along with the model's&nbsp;time span, it determines the number of calculation steps in the simulation and therefore has a large impact on the run time of the&nbsp;model.&nbsp; The primary determining factor, however, is model accuracy.&nbsp; When&nbsp;modeling populations that are binned very finely (e.g. the early neonatal groups), we need to take small time steps to resolve events that occur during those periods.&nbsp; Additionally, if the&nbsp;model contains events with large rates (e.g. remission of infectious diseases), take time steps that are too large will massively skew disease prevalence (and therefore cause specific mortality) in the model.&nbsp; In initial model development it is better to be conservative and select a small step size relative to the&nbsp;model.&nbsp; Once initial model development and validation is complete, we can do sensitivity analysis to determine a step size that balances run time with plans for model scale up.</p>
<h4 style="margin-left: 90.0px;">Locations</h4>
<p style="margin-left: 120.0px;">Include a list of 1-5 locations for the initial model.&nbsp; Additional locations can be added if we decide to scale up the model due to interest from internal clients (e.g. our brain trust, or Abie, or other internal modelers we consult with) or external funders.<br /> <br /> There are two good ways to decide what locations to pick.&nbsp; The first is if the grant funders have a particular interest in certain locations.&nbsp; The second is to use GBD compare to get a good idea of where the&nbsp;intervention might have the largest impact. If the&nbsp;intervention targets a disease directly, look for places with a large proportion of DALYs/Deaths attributable to that disease.&nbsp; If the&nbsp;intervention targets a GBD risk, look for places where the burden of the risk-affected diseases is high and the PAF associated with the cause risk pair is also large.&nbsp; Existing coverage (existing/current use of the intervention) should be taken into account as well, since it reduces the potential impact of the intervention.</p>
<h4 style="margin-left: 90.0px;">Initial Population: size, age range, other considerations</h4>
<p style="margin-left: 120.0px;">This has a large impact on the run time of the model.&nbsp; You should select a population size that is large enough so that uncertainty does not dominate the effect size of your intervention, but no larger.&nbsp; &nbsp;&nbsp;</p>
<p style="margin-left: 120.0px;">You should inform this decision by considering the ages affected by the risks, diseases, and interventions in the model as well as the time horizon you want to report results for.</p>
<p style="margin-left: 120.0px;">This decision is mostly driven by the results you want to report. It also has implications for how the fertility model, if present, will function.</p>
<h4 style="margin-left: 90.0px;">Fertility Model</h4>
<p style="margin-left: 120.0px;">One of:</p>
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
<p style="margin-left: 120.0px;">The decision here is determined by the structure of your intervention, your reporting needs, and the need for accuracy and model speed. Age specific fertility is the truest model of population dynamics but may require simulating large numbers of individuals that are unimportant to the intervention effects.&nbsp; Crude birth rate is a good trade off, but has issues when simulating small age subsets of the population.&nbsp; Any model that uses a fertility component must have 0 specified as the population age start.</p>
<h3 style="margin-left: 60.0px;">Intervention Model</h3>
<p style="margin-left: 90.0px;">The purpose of this section is to lay out the model for the intervention in detail.&nbsp; There are a few high level pieces that will always need to be included, but much of this section can vary widely between interventions.<br /> <br /> Based on deadline considerations, you should generally split this into two sections.&nbsp; One for a minimal model implementation (think: what if we magically shifted intervention coverage from 10% to 60% over 3 years with a linear ramp), and one for a detailed implementation strategy (e.g. when someone comes in for a doctor&rsquo;s visit, we perform a measurement of their risk exposure.&nbsp; Based on the outcome of that measurement, and perhaps other criteria, we enroll them in a clinical trial of a new drug.&nbsp; They fill their prescriptions every once in a while and generally take their medications.&nbsp; Sometimes there are adverse events that cause them to stop though).</p>
<p style="margin-left: 90.0px;">In both the minimal model and the detailed model, you must address all of the following:</p>
<h4 style="margin-left: 90.0px;">Intervention Effect</h4>
<p style="margin-left: 90.0px;">How does your intervention effect its targets? Is the effect additive, multiplicative, etc.?&nbsp; Does the size of the effect depend on the quality of treatment? On how long someone has been receiving the intervention?&nbsp; If so, how?&nbsp; Include equations and graphs where possible.</p>
<p style="margin-left: 90.0px;">Are the intervention targets specified in terms of something GBD models directly? If not, you should include a brief description of the targets and reference the relevant disease or risk section where you lay out the alternative modeling strategy for the intervention targets.</p>
<h4 style="margin-left: 90.0px;">Existing Coverage</h4>
<p style="margin-left: 90.0px;">Is there already coverage of the intervention in your target populations?&nbsp; How should we account for it?</p>
<h4 style="margin-left: 90.0px;">Treatment Algorithm</h4>
<p style="margin-left: 90.0px;">How do we alter the coverage of the intervention in the target population?&nbsp; When does your change go into effect? Is it rolled out over time? Is it given to people during particular events (the onset of a particular disease, or a visit to a health care facility? For complex treatment algorithms, think from the perspective of what can happen to an individual. Equations, graphs, and diagrams are often useful here.</p>
<p>&nbsp;</p>
<p style="margin-left: 90.0px;">We have already implemented a common intervention strategy called the coverage gap that is useful for particular kinds of interventions.&nbsp; The criteria for using this strategy are:</p>
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li style="list-style-type: none;background-image: none;">
<ul>
<li>There is existing coverage of your intervention in the population.&nbsp; (We can use this strategy without existing coverage, but it is often unnecessary).</li>
<li>The intervention target is a rate (e.g. disease incidence, mortality, healthcare utilization) or the intervention target is dichotomous (e.g. a risk where you&rsquo;re either exposed or unexposed).</li></ul></li></ul></li></ul></li></ul>
<h4 style="margin-left: 90.0px;">Scenarios</h4>
<p style="margin-left: 90.0px;">What intervention scenarios do you want to explore? What parameters would be useful for that exploration/sensitivity analysis?</p>
<h4 style="margin-left: 90.0px;">Components</h4>
<p style="margin-left: 90.0px;">What components are used to implement the intervention?&nbsp;</p>
<p style="margin-left: 90.0px;">How do you include them in the simulation?</p>
<p style="margin-left: 90.0px;">What columns do they create in the population table?&nbsp; What do the columns mean?</p>
<p style="margin-left: 90.0px;">What value pipelines do they create? What do the values coming out of the pipelines mean?</p>
<h4 style="margin-left: 90.0px;">Parameters</h4>
<p style="margin-left: 90.0px;">List all available parameters in the format:</p>
<p style="margin-left: 90.0px;"><em>parameter_name</em> &ndash; default parameter value [parameter range either as minimum and maximum or as a list of values]</p>
<p style="margin-left: 90.0px;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; parameter description</p>
<h3 style="margin-left: 60.0px;">Risk Entities</h3>
<p style="margin-left: 60.0px;">Vivarium has the infrastructure to model using any risks in the GBD hierarchy.&nbsp;</p>
<h4 style="margin-left: 90.0px;">Data Sources</h4>
<p style="margin-left: 90.0px;">What data sources are used to inform your risk model?</p>
<p style="margin-left: 90.0px;">This section is only important to fill out if you deviate from our standard data sources (which will be returned from vivarium_inputs tools):</p>
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
<h4 style="margin-left: 90.0px;">Components</h4>
<p style="margin-left: 90.0px;">What components are used to implement the risk and risk effects?&nbsp;</p>
<p style="margin-left: 90.0px;">How do you include them in the simulation?</p>
<p style="margin-left: 90.0px;">What columns do they create in the population table?&nbsp; What do the columns mean?</p>
<p style="margin-left: 90.0px;">What value pipelines do they create? What do the values coming out of the pipelines mean?</p>
<p style="margin-left: 90.0px;">This section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation.</p>
<h4 style="margin-left: 90.0px;">Parameters</h4>
<p style="margin-left: 90.0px;">List all available parameters in the format:</p>
<p style="margin-left: 90.0px;"><em>parameter_name</em> &ndash; default parameter value [parameter range either as minimum and maximum or as a list of values]</p>
<p style="margin-left: 90.0px;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; parameter description</p>
<p style="margin-left: 90.0px;">This section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation or state that no parameters are available.</p>
<h3 style="margin-left: 60.0px;">Cause Entities</h3>
<p style="margin-left: 60.0px;">Vivarium has the infrastructure to model using causes at any level in the GBD hierarchy. However, it is recommended to model GBD causes at the most detailed level to avoid problems with&nbsp;missingness in the GBD cause hierarchy.</p>
<p style="margin-left: 60.0px;">Like risks, tools from vivarium_inputs can be used to pull and inspect the data for the models.&nbsp; You should document your findings in the following format:</p>
<h4 style="margin-left: 90.0px;">Modeling Strategy</h4>
<p style="margin-left: 90.0px;">This decision will be driven by data availability, and disease epidemiology.&nbsp;There are many causes that this list will be unable to handle.&nbsp; In such a situation, you should detail an appropriate strategy.&nbsp; Causes with PAF of one relationships with modeled risks are the most frequent example. There are also situations where you might have multiple causes in the model with overlapping definitions.&nbsp; For example, diabetes and chronic kidney disease due to diabetes.</p>
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
<h4 style="margin-left: 90.0px;">Data Sources</h4>
<p style="margin-left: 120.0px;">What data sources are used to inform your cause model?</p>
<p style="margin-left: 120.0px;">This section is only important to fill out if you deviate from our standard data sources (which will be returned from vivarium_inputs tools).&nbsp;</p>
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
<h4 style="margin-left: 90.0px;">Components</h4>
<p style="margin-left: 120.0px;">What components are used to implement the cause model?&nbsp;</p>
<p style="margin-left: 120.0px;">How do you include them in the simulation?</p>
<p style="margin-left: 120.0px;">What columns do they create in the population table?&nbsp; What do the columns mean?</p>
<p style="margin-left: 120.0px;">What value pipelines do they create? What do the values coming out of the pipelines mean?</p>
<p style="margin-left: 120.0px;">This section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation.</p>
<h4 style="margin-left: 90.0px;">Parameters</h4>
<p style="margin-left: 120.0px;">List all available parameters in the format:</p>
<p style="margin-left: 120.0px;"><em>parameter_name</em> &ndash; default parameter value [parameter range either as minimum and maximum or as a list of values]</p>
<p style="margin-left: 120.0px;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; parameter description</p>
<p style="margin-left: 120.0px;">This section is primarily necessary for non standard components.&nbsp; It should otherwise point to standard documentation or state that no parameters are available.</p>
<h3 style="margin-left: 60.0px;">Model Outputs</h3>
<p style="margin-left: 90.0px;">There are two kinds of outputs to consider here: outputs used for model validation/sensitivity analysis and outputs used to produce final results.&nbsp; You should label what they&rsquo;ll be used for.&nbsp; Recording some kinds of data in the simulation is sometimes quite costly in terms of computation time and memory usage.&nbsp; We can afford the extra resources when doing small scale runs for validation, but need to be careful when running models at scale.</p>
<h4 style="margin-left: 90.0px;">Stratification</h4>
<p style="margin-left: 120.0px;">How should this output be stratified? By age?&nbsp; By sex? By risk exposure level or treatment category?</p>
<p style="margin-left: 120.0px;">You should think fairly carefully about this.&nbsp; We will typically construct observers that report numerators and denominators separately in entirely stratified bins. If you want to observe very finely stratified outcomes, you may end up in situations where your denominator (e.g. your sample size) is too small to be representative.</p>
<h4 style="margin-left: 90.0px;">Observer Component</h4>
<p style="margin-left: 120.0px;">What component produces the appropriate outputs?</p>
<p style="margin-left: 120.0px;">How do you include it in the simulation?</p>
<p style="margin-left: 120.0px;">(For interactive observers) What columns do they create in the population table?&nbsp; What do the columns mean?</p>
<p style="margin-left: 120.0px;">(For interactive observers) What value pipelines do they create? What do the values coming out of the pipelines mean?</p>
<p style="margin-left: 120.0px;">Is this observer parameterized?&nbsp; If so, what parameters are available.</p>
<h1 style="margin-left: 30.0px;">Model Development Meeting(s)</h1>
<p style="margin-left: 60.0px;">Once the researcher completes a draft of the <ac:link ac:anchor="ConceptModelTemplate"><ac:plain-text-link-body><![CDATA[Concept Model Document]]></ac:plain-text-link-body></ac:link>&nbsp;the intervention literature and GBD models involved,&nbsp;reach out to the team's Project Officer (<ac:link><ri:user ri:userkey="8a1b98ce62944f110163082ebd9d0010" /></ac:link>&nbsp;) to schedule a Concept Model Development Meeting.&nbsp;<br /><br />This is a formal design meeting with the following goals:</p>
<ol>
<li style="list-style-type: none;background-image: none;">
<ol>
<li style="list-style-type: none;background-image: none;">
<ol>
<li>Explain the intervention and GBD models involved to the engineer responsible for the model.&nbsp;If at all possible, the researcher should send a summary ahead of time so that this part can proceed mostly as a Q&amp;A.</li>
<li>Collaboratively develop a detailed <ac:link ac:anchor="ConceptModelDiagram"><ac:plain-text-link-body><![CDATA[concept model diagram]]></ac:plain-text-link-body></ac:link> annotated with all necessary data sources.&nbsp;&nbsp;</li>
<li>Identify any gaps in data, understanding, or simulation infrastructure that need to be addressed before proceeding.</li></ol></li></ol></li></ol>
<p style="margin-left: 60.0px;">The concept model we produce from this meeting essentially creates a&nbsp;<strong>contract</strong>&nbsp;between the research staff and the engineering staff.&nbsp; It represents a shared understanding of the model to be built.&nbsp;</p>
<p style="margin-left: 60.0px;">Models will inevitably change as we do more research, gather more data, or our clients ask for more&nbsp;things.&nbsp;<strong>The first step in addressing a change to the model is to update the concept model diagram in consultation with all research and engineering stakeholders.&nbsp;</strong>In order for us to be responsive to change, the change must be highly visible and make sense to everyone involved.</p>
<h1>Template Revision History&nbsp;<ac:structured-macro ac:name="anchor" ac:schema-version="1" ac:macro-id="b59d62a1-1c22-4dc3-94eb-b77f81f6fc1e"><ac:parameter ac:name="">concept_model_revision_hisotry</ac:parameter></ac:structured-macro></h1>
<table><colgroup><col /><col /><col /></colgroup>
<tbody>
<tr>
<td>
<p align="center"><strong>Name</strong></p></td>
<td>
<p align="center"><strong>Date</strong></p></td>
<td>
<p align="center"><strong>Notes</strong></p></td></tr>
<tr>
<td>
<p>James Collins</p></td>
<td>
<p>01/30/19</p></td>
<td>
<p>Initial draft of concept model template</p></td></tr>
<tr>
<td>
<p>Christine Allen</p></td>
<td>
<p>2/5/19</p></td>
<td>
<p>Extracted bullet points, added tabular formatting</p></td></tr>
<tr>
<td>
<p>Zane Rankin</p></td>
<td>
<p>2/6/2019</p></td>
<td>
<p>Add revision history, model development narrative section</p></td></tr>
<tr>
<td colspan="1">Christine Allen</td>
<td colspan="1">2/7/2019</td>
<td colspan="1">Split into two templates. Updated formatting.</td></tr></tbody></table>
<p class="auto-cursor-target" style="margin-left: 30.0px;"><br /></p>