mp2rage: Compute a T1 map using MP2RAGE
=======================================

.. image:: https://mybinder.org/badge_logo.svg
 :target: https://mybinder.org/v2/gh/qMRLab/doc_notebooks/master?filepath=mp2rage_notebook.ipynb
.. raw:: html
	
	
	<style type="text/css">
	.content { font-size:1.0em; line-height:140%; padding: 20px; }
	.content p { padding:0px; margin:0px 0px 20px; }
	.content img { padding:0px; margin:0px 0px 20px; border:none; }
	.content p img, pre img, tt img, li img, h1 img, h2 img { margin-bottom:0px; }
	.content ul { padding:0px; margin:0px 0px 20px 23px; list-style:square; }
	.content ul li { padding:0px; margin:0px 0px 7px 0px; }
	.content ul li ul { padding:5px 0px 0px; margin:0px 0px 7px 23px; }
	.content ul li ol li { list-style:decimal; }
	.content ol { padding:0px; margin:0px 0px 20px 0px; list-style:decimal; }
	.content ol li { padding:0px; margin:0px 0px 7px 23px; list-style-type:decimal; }
	.content ol li ol { padding:5px 0px 0px; margin:0px 0px 7px 0px; }
	.content ol li ol li { list-style-type:lower-alpha; }
	.content ol li ul { padding-top:7px; }
	.content ol li ul li { list-style:square; }
	.content pre, code { font-size:11px; }
	.content tt { font-size: 1.0em; }
	.content pre { margin:0px 0px 20px; }
	.content pre.codeinput { padding:10px; border:1px solid #d3d3d3; background:#f7f7f7; overflow-x:scroll}
	.content pre.codeoutput { padding:10px 11px; margin:0px 0px 20px; color:#4c4c4c; white-space: pre-wrap; white-space: -moz-pre-wrap; white-space: -pre-wrap; white-space: -o-pre-wrap; word -wrap: break-word;}
	.content pre.error { color:red; }
	.content @media print { pre.codeinput, pre.codeoutput { word-wrap:break-word; width:100%; } }
	.content span.keyword { color:#0000FF }
	.content span.comment { color:#228B22 }
	.content span.string { color:#A020F0 }
	.content span.untermstring { color:#B20000 }
	.content span.syscmd { color:#B28C00 }
	.content .footer { width:auto; padding:10px 0px; margin:25px 0px 0px; border-top:1px dotted #878787; font-size:0.8em; line-height:140%; font-style:italic; color:#878787; text-align:left; float:none; }
	.content .footer p { margin:0px; }
	.content .footer a { color:#878787; }
	.content .footer a:hover { color:#878787; text-decoration:underline; }
	.content .footer a:visited { color:#878787; }
	.content table th { padding:7px 5px; text-align:left; vertical-align:middle; border: 1px solid #d6d4d4; font-weight:bold; }
	.content table td { padding:7px 5px; text-align:left; vertical-align:top; border:1px solid #d6d4d4; }
	::-webkit-scrollbar {
	-webkit-appearance: none;
	width: 4px;
	height: 5px;
	}
	
	::-webkit-scrollbar-thumb {
	border-radius: 5px;
	background-color: rgba(0,0,0,.5);
	-webkit-box-shadow: 0 0 1px rgba(255,255,255,.5);
	}
	</style><div class="content"><h2 >Contents</h2><div ><ul ><li ><a href="#2">1. Print <tt >mp2rage</tt> information</a></li><li ><a href="#3">2. Setting model parameters</a></li><li ><a href="#4">2.a. Create <tt >mp2rage</tt> object</a></li><li ><a href="#5">2.b. Set <tt >protocol</tt> and <tt >options</tt></a></li><li ><a href="#8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></a></li><li ><a href="#15">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></a></li><li ><a href="#19">3. Fit MRI data</a></li><li ><a href="#20">3.a. <b >Load</b> input data</a></li><li ><a href="#22">3.b. Execute fitting process</a></li><li ><a href="#25">3.c. Display <tt >FitResults</tt></a></li><li ><a href="#26">3.d. Save fit results</a></li><li ><a href="#28">3.e. Re-use or share fit configuration files</a></li><li ><a href="#29">4. Simulations</a></li><li ><a href="#30">4.a. <tt >Single Voxel Curve</tt></a></li><li ><a href="#32">4.b. <tt >Sensitivity Analysis</tt></a></li><li ><a href="#34">5. Notes</a></li><li ><a href="#35">5.a. Notes specific to <tt >mp2rage</tt></a></li><li ><a href="#36">5.a.1 BIDS</a></li><li ><a href="#38">5.a.2 Note-1</a></li><li ><a href="#39">5.b. Generic notes</a></li><li ><a href="#40">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</a></li><li ><a href="#44">5.b.2 Parallelization:</a></li><li ><a href="#46">6. Citations</a></li></ul></div><pre class="codeinput"><span class="comment">% This m-file has been automatically generated using qMRgenBatch(mp2rage)</span>
	<span class="comment">% for publishing documentation.</span>
	<span class="comment">% Command Line Interface (CLI) is well-suited for automatization</span>
	<span class="comment">% purposes and Octave.</span>
	<span class="comment">%</span>
	<span class="comment">% Please execute this m-file section by section to get familiar with batch</span>
	<span class="comment">% processing for mp2rage on CLI.</span>
	<span class="comment">%</span>
	<span class="comment">% Demo files are downloaded into mp2rage_data folder.</span>
	<span class="comment">%</span>
	<span class="comment">% Written by: Agah Karakuzu, 2017</span>
	<span class="comment">% ==============================================================================</span>
	</pre><h2 id="2">1. Print <tt >mp2rage</tt> information</h2><pre class="codeinput">qMRinfo(<span class="string">'mp2rage'</span>);
	</pre><pre class="codeoutput">  mp2rage: Compute a T1 map using MP2RAGE
	
	Assumptions:
	N/A
	Inputs:
	(MP2RAGE)       MP2RAGE UNI image.
	(B1map)         Normalized transmit excitation field map (B1+). B1+ is defined 
	as a  normalized multiplicative factor such that:
	FA_actual = B1+ * FA_nominal. (OPTIONAL).
	(Mask)          Binary mask to a desired region (OPTIONAL).
	(INV1mag)       Magnitude image from the first GRE readout (OPTIONAL).
	(INV1phase)     Phase image from the first GRE readout (OPTIONAL).
	(INV2mag)       Magnitude image from the second GRE readout (OPTIONAL).
	(INV2phase)     Phase image from the second GRE readout (OPTIONAL).
	
	Outputs:
	T1              Longitudinal relaxation time [s].
	Corrected for B1+ bias IF the B1map is provided.
	R1              Longitudinal relaxation rate [1/s].
	Corrected for B1+ bias IF the B1map is provided.
	MP2RAGE         Combined MP2RAGE image if INV1mag, INV1phase, INV2mag, INV2phase
	images were provided but MP2RAGE was not.
	MP2RAGEcor      MP2RAGE image corrected for B1+ bias if B1map is provided.
	
	Options:
	Inversion efficiency               Efficiency of the inversion pulse (fraction).
	
	Authors: Agah Karakuzu, Mathieu Boudreau 2019
	
	References:
	Please cite the following if you use this module:
	Marques, José P., et al. "MP2RAGE, a self bias-field corrected sequence for
	improved segmentation and T1-mapping at high field." Neuroimage 49.2 (2010): 1271-1281.
	In addition to citing the package:
	Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., 
	Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: 
	Quantitative MRI analysis, under one umbrella doi: 10.21105/joss.02343
	
	Reference page in Doc Center
	doc mp2rage
	
	
	</pre><h2 id="3">2. Setting model parameters</h2><h2 id="4">2.a. Create <tt >mp2rage</tt> object</h2><pre class="codeinput">Model = mp2rage;
	</pre><h2 id="5">2.b. Set <tt >protocol</tt> and <tt >options</tt></h2><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Protocol:</u></b> <i >MRI acquisition parameters that are accounted for by the respective model.</i></p>
	</div>
	</p><p >For example: <tt >TE</tt>, <tt >TR</tt>, <tt >FA</tt> <tt >FieldStrength</tt>. The assigned <tt >protocol</tt> values are subjected to a sanity check to ensure that they are in agreement with the <tt >data</tt> attributes.</p><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Options:</u></b> <i >Fitting preferences that are left at user's discretion.</i></p>
	</div>
	</p><p >For example: <tt >linear fit</tt>, <tt >exponential fit</tt>, <tt >drop first echo</tt>.</p><h2 id="8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></h2><p >If you are using Octave, or would like to serialize your operations any without <tt >GUI</tt> involvement, you can assign <tt >protocol</tt> directly in CLI:</p><pre class="codeinput">B0  = 7;
	Model.Prot.Hardware.Mat = [ B0 ];
	</pre><pre class="codeinput">Inv  = 6;
	Exc  = 0.0067;
	Model.Prot.RepetitionTimes.Mat = [ Inv  Exc ];
	</pre><pre class="codeinput">InversionTimes  = [0.8000; 2.7000];
	<span class="comment">% InversionTimes (s) is a vector of [2X1]</span>
	Model.Prot.Timing.Mat = [ InversionTimes ];
	</pre><pre class="codeinput">FlipAngles = [4.0000; 5.0000];
	<span class="comment">% FlipAngles is a vector of [2X1]</span>
	Model.Prot.Sequence.Mat = [ FlipAngles];
	</pre><pre class="codeinput">Pre = 35;
	Post = 72;
	Model.Prot.NumberOfShots.Mat = [ Pre Post];
	</pre><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for further information. </p>
	</div>
	</p><h2 id="15">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></h2><p >The following command opens a panel to set <tt >protocol</tt> and <tt >options</tt> (if <tt >GUI</tt> is available to the user):</p><pre class="language-matlab">Model = Custom_OptionsGUI(Model);
	</pre><p ><img vspace="5" hspace="5" src="https://github.com/qMRLab/doc_images/blob/main/usr/protPanels/mp2rage.png?raw=true" alt=""> </p><p ><i >If available, you need to close this panel for the remaining of the script to proceed.</i></p><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Using this panel, you can save qMRLab protocol files that can be used in both interfaces. See the <a href="#36">generic notes</a> section below for details. </p>
	</div>
	</p><h2 id="19">3. Fit MRI data</h2><h2 id="20">3.a. <b >Load</b> input data</h2><p >This section shows how you can load data into a(n) <tt >mp2rage</tt> object.</p><div ><ul ><li >At the CLI level, qMRLab accepts structs containing (<tt >double</tt>) data in the fields named in accordance with a qMRLab model.</li></ul></div><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-umbrella" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for BIDS compatible wrappers and scalable <br >        qMRLab workflows. </p>
	</div>
	</p><pre class="codeinput"><span class="comment">%          |- mp2rage object needs 7 data input(s) to be assigned:</span>
	<span class="comment">%          |-   MP2RAGE</span>
	<span class="comment">%          |-   INV1mag</span>
	<span class="comment">%          |-   INV1phase</span>
	<span class="comment">%          |-   INV2mag</span>
	<span class="comment">%          |-   INV2phase</span>
	<span class="comment">%          |-   B1map</span>
	<span class="comment">%          |-   Mask</span>
	
	data = struct();
	
	<span class="comment">% MP2RAGE.mat contains [143  218    2] data.</span>
	load(<span class="string">'mp2rage_data/MP2RAGE.mat'</span>);
	<span class="comment">% B1map.mat contains [143  218    2] data.</span>
	load(<span class="string">'mp2rage_data/B1map.mat'</span>);
	data.MP2RAGE= double(MP2RAGE);
	data.B1map= double(B1map);
	</pre><h2 id="22">3.b. Execute fitting process</h2><p >This section will fit the loaded data.</p><pre class="language-matlab">FitResults = FitData(data,Model,0);
	</pre><p >
	<div class="danger">
	<p style="margin:0px!important;"><strong ><i class="fa fa-umbrella" style="color:red;margin-left:5px;"></i></strong> Visit the <a href="#36">generic notes</a> section below for instructions to accelerate fitting by <br >       parallelization using <code >ParFitData</code>. </p>
	</div>
	</p><h2 id="25">3.c. Display <tt >FitResults</tt></h2><p >You can display the current outputs by:</p><pre class="language-matlab">qMRshowOutput(FitResults,data,Model);
	</pre><p ><i >A representative fit curve will be plotted if available.</i></p><p >To render images in this page, we will load the fit results that had been saved before. You can skip the following code block;</p><pre class="codeinput"><span class="comment">% Load FitResults that comes with the example dataset.</span>
	FitResults_old = load(<span class="string">'FitResults/FitResults.mat'</span>);
	qMRshowOutput(FitResults_old,data,Model);
	</pre><img vspace="5" hspace="5" src="_static/mp2rage_batch_01.png" alt=""> <h2 id="26">3.d. Save fit results</h2><p >Outputs can be saved as <tt >*.nii.(gz)</tt> if <tt >NIfTI</tt> inputs are available:</p><pre class="language-matlab"><span class="comment">% Generic function call to save nifti outputs</span>
	FitResultsSave_nii(FitResults, <span class="string">'reference/nifti/file.nii.(gz)'</span>);
	</pre><p >If not, <tt >FitResults.mat</tt> file can be saved. This file contains all the outputs as workspace variables:</p><pre class="language-matlab"><span class="comment">% Generic function call to save FitResults.mat</span>
	FitResultsSave_mat(FitResults);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-clone" style="color:navy;margin-left:5px;"></i></strong> <code >FitResults.mat</code> files can be loaded to qMRLab <code >GUI</code> for <a href="l#data-viewer" target="_blank">visualization and ROI <br >        analyses</a>. </p>
	</div>
	</p><p >The section below will be dynamically generated in accordance with the example data format (<tt >mat</tt> or <tt >nii</tt>). You can substitute <tt >FitResults_old</tt> with <tt >FitResults</tt> if you executed the fitting using example dataset for this model in section <b >3.b.</b>.</p><pre class="codeinput">FitResultsSave_mat(FitResults_old);
	</pre><h2 id="28">3.e. Re-use or share fit configuration files</h2><p >qMRLab's fit configuration files (<tt >mp2rage_Demo.qmrlab.mat</tt>) store all the <tt >options</tt> and <tt >protocol</tt> in relation to the used model and the release version.</p><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-retweet" style="color:navy;margin-left:5px;"></i></strong> <code >*.qmrlab.mat</code> files can be easily shared with collaborators to allow them fit their own <br >       data or run simulations using identical <code >option</code> and <code >protocol</code> configurations. </p>
	</div>
	</p><pre class="codeinput">Model.saveObj(<span class="string">'my_mp2rage_config.qmrlab.mat'</span>);
	</pre><h2 id="29">4. Simulations</h2><h2 id="30">4.a. <tt >Single Voxel Curve</tt></h2><p >
	<details >
	<summary >Simulates single voxel curves</summary>
	<ol >
	<li >Analytically generate synthetic MRI data</li>
	<li >Add <i >rician</i> noise</li>
	<li ><tt >Fit</tt> and <tt >plot</tt> the respective curve</li>
	</ol>
	</details>
	</p><p >
	<div class="danger" style="text-align:justify;">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:red;margin-left:5px;"></i></strong> Not available for the current model.</p>
	</div>
	</p><h2 id="32">4.b. <tt >Sensitivity Analysis</tt></h2><p >
	<details >
	<summary >Simulates sensitivity to fitted parameters</summary>
	<ol >
	<li >Iterate fitting parameters from lower (<tt >lb</tt>) to upper (<tt >ub</tt>) bound</li>
	<li >Run <tt >Sim_Single_Voxel_Curve</tt> for <tt >Nofruns</tt> times</li>
	<li >Compute the <tt >mean</tt> and <tt >std</tt> across runs</li>
	</ol>
	</details>
	</p><p >
	<div class="danger" style="text-align:justify;">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:red;margin-left:5px;"></i></strong> Not available for the current model.</p>
	</div>
	</p><h2 id="34">5. Notes</h2><h2 id="35">5.a. Notes specific to <tt >mp2rage</tt></h2><h2 id="36">5.a.1 BIDS</h2><p >
	<img src="https://github.com/qMRLab/doc_images/blob/main/usr/BIDS_Logo.png?raw=true" style="height:100px!important;">
	</p><pre class="language-matlab">|== sub-01/
	|~~~~~~ anat/
	|---------- sub-01_inv-1_MP2RAGE.json
	|---------- sub-01_inv-1_part-mag_MP2RAGE.nii.gz
	|---------- sub-01_inv-1_part-phase_MP2RAGE.nii.gz
	|---------- sub-01_inv-2_MP2RAGE.json
	|---------- sub-01_inv-2_part-mag_MP2RAGE.nii.gz
	|---------- sub-01_inv-2_part-phase_MP2RAGE.nii.gz
	|
	|== derivatives/
	|~~~~~~ Siemens/
	|---------- dataset_description.json
	|~~~~~~~~~~ sub-01/anat/
	|-------------- sub-01_UNIT1.nii.gz (Vendor-generated UNIT1)
	|-------------- sub-01_UNIT1.json
	|~~~~~~ qMRLab/
	|---------- dataset_description.json
	|~~~~~~~~~~ sub-01/anat/
	|-------------- sub-01_T1map.nii.gz
	|-------------- sub-01_T1map.json
	|-------------- sub-01_R1map.nii.gz
	|-------------- sub-01_R1map.json
	|-------------- sub-01_UNIT1.nii.gz (If calculated by qMRLab)
	|-------------- sub-01_UNIT1.json
	</pre><p >For further information, please visit <a href="https://bids-specification.readthedocs.io/en/stable/99-appendices/11-qmri.html">BIDS qMRI Appendix</a>.</p><h2 id="38">5.a.2 Note-1</h2><p >Further details about <tt >mp2rage</tt> protocol settings are available <a href="protocols.html#mp2rage">here</a>.</p><p >Original repository: <a href="https://github.com/JosePMarques/MP2RAGE-related-scripts">https://github.com/JosePMarques/MP2RAGE-related-scripts</a></p><h2 id="39">5.b. Generic notes</h2><h2 id="40">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</h2><p >If you would like to load a desired set of <tt >options</tt> / <tt >protocols</tt> programatically, you can use <tt >*.qmrlab.mat</tt> files. To save a configuration from the <tt >protocol</tt> panel of <tt >mp2rage</tt>, first open the respective panel by running the following command in your MATLAB command window (MATLAB only):</p><pre class="language-matlab">Custom_OptionsGUI(mp2rage);
	</pre><p >In this panel, you can arrange available <tt >options</tt> and <tt >protocols</tt> according to your needs, then click the <tt >save</tt> button to save <tt >my_mp2rage.qmrlab.mat</tt> file. This file can be later loaded into a <tt >mp2rage</tt> object in batch by:</p><pre class="language-matlab">Model = mp2rage;
	Model = Model.loadObj(<span class="string">'my_mp2rage.qmrlab.mat'</span>);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >Model.loadObj('my_mp2rage.qmrlab.mat')</code> call won't update the fields in the <code >Model</code> object, unless the output is assigned to the object as shown above. This compromise on convenience is to retain Octave CLI compatibility. </p>
	</div>
	</p><p ><b >If you don't have MATLAB, hence cannot access the <tt >GUI</tt>, two alternatives are available to populate <tt >options</tt>:</b></p><div ><ol ><li >Use <tt >qmrlab/mcrgui:latest</tt> Docker image to access <tt >GUI</tt>. The instructions are available <a href="https://hub.docker.com/r/qmrlab/mcrgui">here</a>.</li><li >Set <tt >options</tt> and <tt >protocols</tt> in <tt >CLI</tt>:</li></ol></div><div ><ul ><li >List available option fields using tab completion in Octave's command prompt (or window)</li></ul></div><pre class="language-matlab">Model = mp2rage;
	Model.option. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><div ><ul ><li >Assign the desired field. <b >For example</b>, for a <tt >mono_t2</tt> object:</li></ul></div><pre class="language-matlab">Model = mono_t2;
	Model.options.DropFirstEcho = true;
	Model.options.OffsetTerm = false;
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Some option fields may be mutually exclusive or interdependent. Such cases are handled  by the <code >GUI</code> options panel; however, not exposed to the <code >CLI</code>. Therefore, manual <code >CLI</code> <code >options</code> assignments may be challenging for some involved methods such as <code >qmt_spgr</code> or <code >qsm_sb</code>. If above options are not working for you and you cannot infer how to set options solely in batch, please feel free to <a href="https://github.com/qmrlab/qmrlab" target="_blank">open an issue in qMRLab</a> and request the protocol file you need. </p>
	</div>
	</p><p ><b >Similarly, in CLI, you can inspect and assign the <tt >protocols</tt>:</b></p><pre class="language-matlab">Model = mp2rage;
	Model.Prot. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><p >Each protocol field has two subfields of <tt >Format</tt> and <tt >Mat</tt>. The first one is a <tt >cell</tt> indicating the name of the protocol parameter (such as <tt >EchoTime (ms)</tt>) and the latter one contains the respective values (such as <tt >30 x 1 double</tt> array containing <tt >EchoTimes</tt>).</p><p >
	<div class="warning">
	<p style="margin:0px!important;"> The default <code >Mat</code> protocol values are set according to the example datasets served via <a href="https://osf.io/tmdfu" target="_blank">OSF</a>.</p>
	</div>
	</p><h2 id="44">5.b.2 Parallelization:</h2><p >
	<div class="danger">
	<p style="margin:0px!important;"> The current model does not perform voxelwise fitting. Therefore, parallelization is not enabled.</p>
	</div>
	</p><h2 id="46">6. Citations</h2><p ><b >qMRLab JOSS article</b></p><p >
	<div class="success" style="text-align:justify;">
	<p > Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: Quantitative MRI analysis, under one umbrella <a href="https://doi.org/10.21105/joss.02343" target="_blank">10.21105/joss.02343</a></p>
	</div>
	</p><p ><b >Reference article for <tt >mp2rage</tt></b></p><p >
	<div class="success" style="text-align:justify;">
	Marques, José P., et al. (2010). MP2RAGE, a self bias-field corrected sequence for improved segmentation and T1-mapping at high field. Neuroimage, 49(2), 1271-1281. 10.1016/j.neuroimage.2009.10.002
	</div>
	</p><p >
	<hr >
	<center ><i class="fa fa-umbrella" style="color:black;font-size:2em;"></i></center>
	<center ><p >Quantitative MRI, under one umbrella.</p></center>
	<center >| <a href="https://github.com/qmrlab/pulse_sequences" target="_blank">qMRPullseq</a> | <a href="https://github.com/qmrlab/qmrflow" target="_blank">qMRFlow</a> | <a href="https://qmrlab.org/blog.html" target="_blank">Interactive Tutorials</a> | </p></center>
	<center ><p ><a href="https://www.neuro.polymtl.ca/doku.php" target="_blank">NeuroPoly Lab</a>, Montreal, Canada</p></center>
	<hr >
	</p><p class="footer"><br ><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB® R2018b</a><br ></p></div>
