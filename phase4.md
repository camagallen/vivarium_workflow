[Back to Model Development](Model_Development.md)

# Minimal Model Implementation
Minimal model implementation largely the responsibility of the Software Engineer assigned to the model.&nbsp;<

## Software Engineer Tasks
<ol>
<li>Construct a minimal model based on the concept model with data-free test components
<ol>
<li>Optional: do this as a paired-programming exercise with interested research staff</li></ol></li>
<li>Construct non-standard components necessary for minimal model</li>
<li><strong>Identify any infrastructure gaps preventing minimal model implementation and notify relevant staff.</strong></li>
<li>Develop and run validation for minimal model (unit and integration testing)</li></ol>

## Creating an Artifact
Artifacts are hdf files containing GBD data subsets (location(s), years, ages, sexes, etc.) specific to an intervention model. It's inputs are Auxilliary Data (finds it automatically based on the tag) and GBD Data (uses shared GBD functions). The output is a single HDF file that will be used by the model.

## Example
For examples, see individual model repos.
