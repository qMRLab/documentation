inversion_recovery: Compute a T1 map using Inversion Recovery data
==================================================================

.. image:: https://mybinder.org/badge_logo.svg
 :target: https://mybinder.org/v2/gh/qMRLab/doc_notebooks/master?filepath=inversion_recovery_notebook.ipynb
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
	</style><div class="content"><h2 >Contents</h2><div ><ul ><li ><a href="#2">1. Print <tt >inversion_recovery</tt> information</a></li><li ><a href="#3">2. Setting model parameters</a></li><li ><a href="#4">2.a. Create <tt >inversion_recovery</tt> object</a></li><li ><a href="#5">2.b. Set <tt >protocol</tt> and <tt >options</tt></a></li><li ><a href="#8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></a></li><li ><a href="#13">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></a></li><li ><a href="#17">3. Fit MRI data</a></li><li ><a href="#18">3.a. <b >Load</b> input data</a></li><li ><a href="#20">3.b. Execute fitting process</a></li><li ><a href="#23">3.c. Display <tt >FitResults</tt></a></li><li ><a href="#25">3.d. Save fit results</a></li><li ><a href="#27">3.e. Re-use or share fit configuration files</a></li><li ><a href="#28">4. Simulations</a></li><li ><a href="#29">4.a. <tt >Single Voxel Curve</tt></a></li><li ><a href="#31">4.b. <tt >Sensitivity Analysis</tt></a></li><li ><a href="#33">5. Notes</a></li><li ><a href="#34">5.a. Notes specific to <tt >inversion_recovery</tt></a></li><li ><a href="#35">5.a.1 BIDS (official)</a></li><li ><a href="#37">5.b. Generic notes</a></li><li ><a href="#38">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</a></li><li ><a href="#42">5.b.2 Parallelization</a></li><li ><a href="#44">6. Citations</a></li></ul></div><pre class="codeinput"><span class="comment">%                   This page has been automatically generated.</span>
	<span class="comment">%</span>
	<span class="comment">%                              https://qmrlab.org</span>
	<span class="comment">%           _______________________________________________________</span>
	<span class="comment">%          |           _.._                                        |</span>
	<span class="comment">%          |       .-""    ""-.                                    |</span>
	<span class="comment">%          |      :---.-__-.---;                                   |</span>
	<span class="comment">%          |            || Quantitative MRI. Under one umbrella.   |</span>
	<span class="comment">%          |          ,.|| Karakuzu et al. (2020), JOSS            |</span>
	<span class="comment">%          |           `-' https://doi.org/10.21105/joss.02343     |</span>
	<span class="comment">%          |_______________________________________________________|</span>
	</pre><h2 id="2">1. Print <tt >inversion_recovery</tt> information</h2><pre class="codeinput">qMRinfo(<span class="string">'inversion_recovery'</span>);
	</pre><pre class="codeoutput"> inversion_recovery: Compute a T1 map using Inversion Recovery data
	
	Assumptions:
	(1) Gold standard for T1 mapping
	(2) Infinite TR
	
	Inputs:
	IRData      Inversion Recovery data (4D)
	(Mask)      Binary mask to accelerate the fitting (OPTIONAL)
	
	Outputs:
	T1          transverse relaxation time [ms]
	b           arbitrary fit parameter (S=a + b*exp(-TI/T1))
	a           arbitrary fit parameter (S=a + b*exp(-TI/T1))
	idx         index of last polarity restored datapoint (only used for magnitude data)
	res         Fitting residual
	
	
	Protocol:
	IRData  [TI1 TI2...TIn] inversion times [ms]
	TimingTable   [TR] repetition time [ms]
	
	Options:
	method          Method to use in order to fit the data, based on whether complex or only magnitude data acquired.
	'complex'     Complex dataset.
	'magnitude'   Magnitude dataset.
	
	
	fitModel        T1 fitting moddel.
	'Barral'      Fitting equation: a+bexp(-TI/T1)
	'General'     Fitting equation: c(1-2exp(-TI/T1)+exp(-TR/T1))
	
	Example of command line usage (see also <a href="matlab: showdemo inversion_recovery_batch">showdemo inversion_recovery_batch</a>):
	Model = inversion_recovery;  % Create class from model
	Model.Prot.IRData.Mat=[350.0000; 500.0000; 650.0000; 800.0000; 950.0000; 1100.0000; 1250.0000; 1400.0000; 1700.0000];
	data = struct;  % Create data structure
	data.MET2data ='IRData.mat';  % Load data
	data.Mask = 'Mask.mat';
	FitResults = FitData(data,Model); %fit data
	FitResultsSave_mat(FitResults);
	
	For more examples: <a href="matlab: qMRusage(minversion_recovery);">qMRusage(inversion_recovery)</a>
	
	Author: Ilana Leppert, 2017
	
	References:
	Please cite the following if you use this module:
	A robust methodology for in vivo T1 mapping. Barral JK, Gudmundson E, Stikov N, Etezadi-Amoli M, Stoica P, Nishimura DG. Magn Reson Med. 2010 Oct;64(4):1057-67. doi: 10.1002/mrm.22497.
	In addition to citing the package:
	Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., 
	Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: 
	Quantitative MRI analysis, under one umbrella doi: 10.21105/joss.02343
	
	Documentation for inversion_recovery
	doc inversion_recovery
	
	
	</pre><h2 id="3">2. Setting model parameters</h2><h2 id="4">2.a. Create <tt >inversion_recovery</tt> object</h2><pre class="codeinput">Model = inversion_recovery;
	</pre><h2 id="5">2.b. Set <tt >protocol</tt> and <tt >options</tt></h2><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Protocol:</u></b> <i >MRI acquisition parameters that are accounted for by the respective model.</i></p>
	</div>
	</p><p >For example: <tt >TE</tt>, <tt >TR</tt>, <tt >FA</tt> <tt >FieldStrength</tt>. The assigned <tt >protocol</tt> values are subjected to a sanity check to ensure that they are in agreement with the <tt >data</tt> attributes.</p><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Options:</u></b> <i >Fitting preferences that are left at user's discretion.</i></p>
	</div>
	</p><p >For example: <tt >linear fit</tt>, <tt >exponential fit</tt>, <tt >drop first echo</tt>.</p><h2 id="8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></h2><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> The units below are displayed according to the original implementation contributed to qMRLab. To learn how to manage input protocol units, please visit the documentation on <a href="#36">|/usr/preferences.json|</a>.</p>
	</div>
	</p><p >If you are using Octave, or would like to serialize your operations any without <tt >GUI</tt> involvement, you can assign <tt >protocol</tt> directly in CLI:</p><pre class="codeinput">TI = [350.0000; 500.0000; 650.0000; 800.0000; 950.0000; 1100.0000; 1250.0000; 1400.0000; 1700.0000];
	<span class="comment">% TI(ms) is a vector of [9X1]</span>
	Model.Prot.IRData.Mat = [ TI];
	</pre><pre class="codeinput">TR = 2500;
	Model.Prot.TimingTable.Mat = [ TR];
	</pre><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for further information. </p>
	</div>
	</p><h2 id="13">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></h2><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> The units below are displayed according to the original implementation contributed to qMRLab. To learn how to manage input protocol units, please visit the documentation on <a href="#36">|/usr/preferences.json|</a>.</p>
	</div>
	</p><p >The following command opens a panel to set <tt >protocol</tt> and <tt >options</tt> (if <tt >GUI</tt> is available to the user):</p><pre class="language-matlab">Model = Custom_OptionsGUI(Model);
	</pre><p ><img vspace="5" hspace="5" src="https://github.com/qMRLab/doc_images/blob/main/usr/protPanels/inversion_recovery.png?raw=true" alt=""> </p><p ><i >If available, you need to close this panel for the remaining of the script to proceed.</i></p><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Using this panel, you can save qMRLab protocol files that can be used in both interfaces. See the <a href="#36">generic notes</a> section below for details. </p>
	</div>
	</p><h2 id="17">3. Fit MRI data</h2><h2 id="18">3.a. <b >Load</b> input data</h2><p >This section shows how you can load data into a(n) <tt >inversion_recovery</tt> object.</p><div ><ul ><li >At the CLI level, qMRLab accepts structs containing (<tt >double</tt>) data in the fields named in accordance with a qMRLab model.</li></ul></div><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-umbrella" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for BIDS compatible wrappers and scalable <br >        qMRLab workflows. </p>
	</div>
	</p><pre class="codeinput"><span class="comment">%          |- inversion_recovery object needs 2 data input(s) to be assigned:</span>
	<span class="comment">%          |-   IRData</span>
	<span class="comment">%          |-   Mask</span>
	
	data = struct();
	
	<span class="comment">% IRData.mat contains [128  128    1    9] data.</span>
	load(<span class="string">'inversion_recovery_data/IRData.mat'</span>);
	<span class="comment">% Mask.mat contains [128  128] data.</span>
	load(<span class="string">'inversion_recovery_data/Mask.mat'</span>);
	data.IRData= double(IRData);
	data.Mask= double(Mask);
	</pre><h2 id="20">3.b. Execute fitting process</h2><p >This section will fit the loaded data.</p><pre class="language-matlab">FitResults = FitData(data,Model,0);
	</pre><p >
	<div class="danger">
	<p style="margin:0px!important;"><strong ><i class="fa fa-umbrella" style="color:red;margin-left:5px;"></i></strong> Visit the <a href="#36">generic notes</a> section below for instructions to accelerate fitting by <br >       parallelization using <code >ParFitData</code>. </p>
	</div>
	</p><h2 id="23">3.c. Display <tt >FitResults</tt></h2><p >You can display the current outputs by:</p><pre class="language-matlab">qMRshowOutput(FitResults,data,Model);
	</pre><p ><i >A representative fit curve will be plotted if available.</i></p><p >To render images in this page, we will load the fit results that had been saved before. You can skip the following code block;</p><pre class="codeinput"><span class="comment">% Load FitResults that comes with the example dataset.</span>
	FitResults_old = load(<span class="string">'FitResults/FitResults.mat'</span>);
	qMRshowOutput(FitResults_old,data,Model);
	</pre><img vspace="5" hspace="5" src="_static/inversion_recovery_batch_01.png" alt=""> <img vspace="5" hspace="5" src="_static/inversion_recovery_batch_02.png" alt=""> <p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> The unit of the quantitative map displayed above is set according to the original implementation contributed to qMRLab. To learn how to manage output map units, please visit the documentation on <a href="#36">|/usr/preferences.json|</a>.</p>
	</div>
	</p><h2 id="25">3.d. Save fit results</h2><p >Outputs can be saved as <tt >*.nii.(gz)</tt> if <tt >NIfTI</tt> inputs are available:</p><pre class="language-matlab"><span class="comment">% Generic function call to save nifti outputs</span>
	FitResultsSave_nii(FitResults, <span class="string">'reference/nifti/file.nii.(gz)'</span>);
	</pre><p >If not, <tt >FitResults.mat</tt> file can be saved. This file contains all the outputs as workspace variables:</p><pre class="language-matlab"><span class="comment">% Generic function call to save FitResults.mat</span>
	FitResultsSave_mat(FitResults);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-clone" style="color:navy;margin-left:5px;"></i></strong> <code >FitResults.mat</code> files can be loaded to qMRLab <code >GUI</code> for <a href="l#data-viewer" target="_blank">visualization and ROI <br >        analyses</a>. </p>
	</div>
	</p><p >The section below will be dynamically generated in accordance with the example data format (<tt >mat</tt> or <tt >nii</tt>). You can substitute <tt >FitResults_old</tt> with <tt >FitResults</tt> if you executed the fitting using example dataset for this model in section <b >3.b.</b>.</p><pre class="codeinput">FitResultsSave_mat(FitResults_old);
	</pre><h2 id="27">3.e. Re-use or share fit configuration files</h2><p >qMRLab's fit configuration files (<tt >inversion_recovery_Demo.qmrlab.mat</tt>) store all the <tt >options</tt> and <tt >protocol</tt> in relation to the used model and the release version.</p><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-retweet" style="color:navy;margin-left:5px;"></i></strong> <code >*.qmrlab.mat</code> files can be easily shared with collaborators to allow them fit their own <br >       data or run simulations using identical <code >option</code> and <code >protocol</code> configurations. </p>
	</div>
	</p><pre class="codeinput">Model.saveObj(<span class="string">'my_inversion_recovery_config.qmrlab.mat'</span>);
	</pre><h2 id="28">4. Simulations</h2><h2 id="29">4.a. <tt >Single Voxel Curve</tt></h2><p >
	<details >
	<summary >Simulates single voxel curves</summary>
	<ol >
	<li >Analytically generate synthetic MRI data</li>
	<li >Add <i >rician</i> noise</li>
	<li ><tt >Fit</tt> and <tt >plot</tt> the respective curve</li>
	</ol>
	</details>
	</p><pre class="codeinput">      x = struct;
	x.T1 = 600;
	x.rb = -1000;
	x.ra = 500;
	<span class="comment">% Set simulation options</span>
	Opt.SNR = 50;
	Opt.T1 = 600;
	Opt.M0 = 1000;
	Opt.TR = 3000;
	Opt.FAinv = 180;
	Opt.FAexcite = 90;
	Opt.Updateinputvariables = false;
	<span class="comment">% run simulation</span>
	figure(<span class="string">'Name'</span>,<span class="string">'Single Voxel Curve Simulation'</span>);
	FitResult = Model.Sim_Single_Voxel_Curve(x,Opt);
	</pre><img vspace="5" hspace="5" src="_static/inversion_recovery_batch_03.png" alt=""> <h2 id="31">4.b. <tt >Sensitivity Analysis</tt></h2><p >
	<details >
	<summary >Simulates sensitivity to fitted parameters</summary>
	<ol >
	<li >Iterate fitting parameters from lower (<tt >lb</tt>) to upper (<tt >ub</tt>) bound</li>
	<li >Run <tt >Sim_Single_Voxel_Curve</tt> for <tt >Nofruns</tt> times</li>
	<li >Compute the <tt >mean</tt> and <tt >std</tt> across runs</li>
	</ol>
	</details>
	</p><pre >            T1            rb            ra</pre><pre class="codeinput">      OptTable.st = [6e+02         -1e+03        5e+02]; <span class="comment">% nominal values</span>
	OptTable.fx = [0             1             1]; <span class="comment">%vary T1...</span>
	OptTable.lb = [0.0001        -1e+04        0.0001]; <span class="comment">%...from 0.0001</span>
	OptTable.ub = [5e+03         0             1e+04]; <span class="comment">%...to 5000</span>
	Opt.SNR = 50;
	Opt.Nofrun = 5;
	<span class="comment">% run simulation</span>
	SimResults = Model.Sim_Sensitivity_Analysis(OptTable,Opt);
	figure(<span class="string">'Name'</span>,<span class="string">'Sensitivity Analysis'</span>);
	SimVaryPlot(SimResults, <span class="string">'T1'</span> ,<span class="string">'T1'</span> );
	</pre><img vspace="5" hspace="5" src="_static/inversion_recovery_batch_04.png" alt=""> <h2 id="33">5. Notes</h2><h2 id="34">5.a. Notes specific to <tt >inversion_recovery</tt></h2><h2 id="35">5.a.1 BIDS (official)</h2><p >
	<img src="https://github.com/qMRLab/doc_images/blob/main/usr/BIDS_Logo.png?raw=true" style="height:100px!important;">
	</p><pre class="language-matlab">|== sub-01/
	|~~~~~~ anat/
	|---------- sub-01_inv-1_IRT1.json
	|---------- sub-01_inv-1_IRT1.nii.gz
	|---------- sub-01_inv-2_IRT1.json
	|---------- sub-01_inv-2_IRT1.nii.gz
	|---------- .
	|---------- .
	|---------- sub-01_inv-N_IRT1.json
	|---------- sub-01_inv-N_IRT1.nii.gz
	|
	|== derivatives/
	|~~~~~~ qMRLab/
	|---------- dataset_description.json
	|~~~~~~~~~~ sub-01/anat/
	|-------------- sub-01_T1map.nii.gz
	|-------------- sub-01_T1map.json
	|-------------- sub-01_R1map.nii.gz
	|-------------- sub-01_R1map.json
	|-------------- sub-01_M0map.nii.gz
	|-------------- sub-01_M0map.json
	</pre><p ><a href="https://osf.io/92kwv/download">Download</a> our example <tt >IRT1</tt> BIDS dataset and process:</p><pre class="language-matlab">dataDir = <span class="string">'set/your/directory/ds-IRT1/sub-01/anat'</span>
	maskFile = <span class="string">'set/your/directory/ds-IRT1/sub-01/anat/sub-01_label-brain.nii.gz'</span>
	niiList = {dir(fullfile(dataDir,<span class="string">'*IRT1.nii*'</span>)).name};
	FitBIDS(niiList,<span class="string">'Mask'</span>,maskFile);
	</pre><p >For further information, please visit <a href="https://bids-specification.readthedocs.io/en/stable/99-appendices/11-qmri.html">BIDS qMRI Appendix</a>.</p><h2 id="37">5.b. Generic notes</h2><h2 id="38">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</h2><p >If you would like to load a desired set of <tt >options</tt> / <tt >protocols</tt> programatically, you can use <tt >*.qmrlab.mat</tt> files. To save a configuration from the <tt >protocol</tt> panel of <tt >inversion_recovery</tt>, first open the respective panel by running the following command in your MATLAB command window (MATLAB only):</p><pre class="language-matlab">Custom_OptionsGUI(inversion_recovery);
	</pre><p >In this panel, you can arrange available <tt >options</tt> and <tt >protocols</tt> according to your needs, then click the <tt >save</tt> button to save <tt >my_inversion_recovery.qmrlab.mat</tt> file. This file can be later loaded into a <tt >inversion_recovery</tt> object in batch by:</p><pre class="language-matlab">Model = inversion_recovery;
	Model = Model.loadObj(<span class="string">'my_inversion_recovery.qmrlab.mat'</span>);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >Model.loadObj('my_inversion_recovery.qmrlab.mat')</code> call won't update the fields in the <code >Model</code> object, unless the output is assigned to the object as shown above. This compromise on convenience is to retain Octave CLI compatibility. </p>
	</div>
	</p><p ><b >If you don't have MATLAB, hence cannot access the <tt >GUI</tt>, two alternatives are available to populate <tt >options</tt>:</b></p><div ><ol ><li >Use <tt >qmrlab/mcrgui:latest</tt> Docker image to access <tt >GUI</tt>. The instructions are available <a href="https://hub.docker.com/r/qmrlab/mcrgui">here</a>.</li><li >Set <tt >options</tt> and <tt >protocols</tt> in <tt >CLI</tt>:</li></ol></div><div ><ul ><li >List available option fields using tab completion in Octave's command prompt (or window)</li></ul></div><pre class="language-matlab">Model = inversion_recovery;
	Model.option. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><div ><ul ><li >Assign the desired field. <b >For example</b>, for a <tt >mono_t2</tt> object:</li></ul></div><pre class="language-matlab">Model = mono_t2;
	Model.options.DropFirstEcho = true;
	Model.options.OffsetTerm = false;
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Some option fields may be mutually exclusive or interdependent. Such cases are handled  by the <code >GUI</code> options panel; however, not exposed to the <code >CLI</code>. Therefore, manual <code >CLI</code> <code >options</code> assignments may be challenging for some involved methods such as <code >qmt_spgr</code> or <code >qsm_sb</code>. If above options are not working for you and you cannot infer how to set options solely in batch, please feel free to <a href="https://github.com/qmrlab/qmrlab" target="_blank">open an issue in qMRLab</a> and request the protocol file you need. </p>
	</div>
	</p><p ><b >Similarly, in CLI, you can inspect and assign the <tt >protocols</tt>:</b></p><pre class="language-matlab">Model = inversion_recovery;
	Model.Prot. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><p >Each protocol field has two subfields of <tt >Format</tt> and <tt >Mat</tt>. The first one is a <tt >cell</tt> indicating the name of the protocol parameter (such as <tt >EchoTime (ms)</tt>) and the latter one contains the respective values (such as <tt >30 x 1 double</tt> array containing <tt >EchoTimes</tt>).</p><p >
	<div class="warning">
	<p style="margin:0px!important;"> The default <code >Mat</code> protocol values are set according to the example datasets served via <a href="https://osf.io/tmdfu" target="_blank">OSF</a>.</p>
	</div>
	</p><h2 id="42">5.b.2 Parallelization</h2><p >Beginning from release <tt >2.5.0</tt>, you can accelerate fitting for the <tt >voxelwise</tt> models using parallelization.</p><p >
	<div class="danger">
	<p style="margin:0px!important;"> <strong >Available in MATLAB only. Requires <code >parallel processing toolbox</code>.</strong></p>
	</div>
	</p><p >In <tt >CLI</tt>, you can perform parallel fitting by:</p><pre class="language-matlab">parpool();
	FitResults = ParFitData(data,Model);
	</pre><p >If a <tt >parpool</tt> exists, the <tt >ParFitData</tt> will use it. If not, a new pool will be created using the local profile. By default, <tt >ParFitData</tt> saves outputs automatically every 5 minutes. You can disable this feature by:</p><pre class="language-matlab">FitResults = ParFitData(data, Model, <span class="string">'AutosaveEnabled'</span>, false);
	</pre><p >Alternatively, you can change the autosave interval (min 1 min) by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'AutoSaveInterval'</span>,10);
	</pre><p >If something went wrong during the fitting (e.g. your computer had to be restarted), you can recover the autosaved data by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'RecoverDirectory'</span>,<span class="string">'/ParFitTempResults_*/folder/from/the/previous/session'</span>);
	</pre><p ><tt >GUI</tt> users will be prompted a question about whether they would like to use parallelization after clicking the <tt >Fit Data</tt> button, if the conditions are met. When called from <tt >GUI</tt>, <tt >ParFitData</tt> will be run with default options:</p><div ><ul ><li >Save temporary results every <tt >5</tt> minutes or whenever a chunk has finished processing</li><li >Split data into chunks with a <tt >granularity</tt> factor of <tt >3</tt></li><li >Do not remove temporary fit results upon completion</li></ul></div><p >For further information:</p><pre class="language-matlab">help <span class="string">ParFitData</span>
	</pre><p >The default <tt >parallelization</tt> options can be changed in the <tt >preferences.json</tt> file located at the root qMRLab directory.</p><h2 id="44">6. Citations</h2><p ><b >qMRLab JOSS article</b></p><p >
	<div class="success" style="text-align:justify;">
	<p > Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: Quantitative MRI analysis, under one umbrella <a href="https://doi.org/10.21105/joss.02343" target="_blank">10.21105/joss.02343</a></p>
	</div>
	</p><p ><b >Reference article for <tt >inversion_recovery</tt></b></p><p >
	<div class="success" style="text-align:justify;">
	Barral, J.K., et al. (2010). A robust methodology for in vivo T1 mapping. Magnetic Resonance in Medicine, 64(4), 1057-1067. 10.1002/mrm.22497
	</div>
	</p><p >
	<hr >
	<center ><i class="fa fa-umbrella" style="color:black;font-size:2em;"></i></center>
	<center ><p >Quantitative MRI, under one umbrella.</p></center>
	<center >| <a href="https://github.com/qmrlab/pulse_sequences" target="_blank">qMRPullseq</a> | <a href="https://github.com/qmrlab/qmrflow" target="_blank">qMRFlow</a> | <a href="https://qmrlab.org/blog.html" target="_blank">Interactive Tutorials</a> | </p></center>
	<center ><p ><a href="https://www.neuro.polymtl.ca/doku.php" target="_blank">NeuroPoly Lab</a>, Montreal, Canada</p></center>
	<hr >
	</p><p class="footer"><br ><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB® R2019b</a><br ></p></div>
