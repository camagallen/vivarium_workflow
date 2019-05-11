
<p><ac:structured-macro ac:name="toc" ac:schema-version="1" ac:macro-id="89f6f4b3-03b2-44c1-9f32-72ed4246b45f"><ac:parameter ac:name="maxLevel">2</ac:parameter></ac:structured-macro></p>
<h1>Overview</h1>
<p style="margin-left: 30.0px;">Minimal model implementation largely the responsibility of the Software Engineer assigned to the model.&nbsp;</p>
<h1>Software Engineer Tasks</h1>
<ol>
<li>Construct a minimal model based on the concept model with data-free test components
<ol>
<li>Optional: do this as a paired-programming exercise with interested research staff</li></ol></li>
<li>Construct non-standard components necessary for minimal model</li>
<li><strong>Identify any infrastructure gaps preventing minimal model implementation and notify relevant staff.</strong></li>
<li>Develop and run validation for minimal model (unit and integration testing)</li></ol>
<h1>Creating an Artifact</h1>
<p style="margin-left: 30.0px;">Artifacts are hdf files containing GBD data subsets (location(s), years, ages, sexes, etc.) specific to an intervention model. It's inputs are Auxilliary Data (finds it automatically based on the tag) and GBD Data (uses shared GBD functions). The output is a single HDF file that will be used by the model.</p>