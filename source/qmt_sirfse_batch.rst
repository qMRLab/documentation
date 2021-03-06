qmt_sirfse:  qMT using Inversion Recovery Fast Spin Echo acquisition
====================================================================

.. image:: https://mybinder.org/badge_logo.svg
 :target: https://mybinder.org/v2/gh/qMRLab/doc_notebooks/master?filepath=qmt_sirfse_notebook.ipynb
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
	</style><div class="content"><h2 >Contents</h2><div ><ul ><li ><a href="#2">1. Print <tt >qmt_sirfse</tt> information</a></li><li ><a href="#3">2. Setting model parameters</a></li><li ><a href="#4">2.a. Create <tt >qmt_sirfse</tt> object</a></li><li ><a href="#5">2.b. Set <tt >protocol</tt> and <tt >options</tt></a></li><li ><a href="#8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></a></li><li ><a href="#12">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></a></li><li ><a href="#16">3. Fit MRI data</a></li><li ><a href="#17">3.a. <b >Load</b> input data</a></li><li ><a href="#19">3.b. Execute fitting process</a></li><li ><a href="#22">3.c. Display <tt >FitResults</tt></a></li><li ><a href="#23">3.d. Save fit results</a></li><li ><a href="#25">3.e. Re-use or share fit configuration files</a></li><li ><a href="#26">4. Simulations</a></li><li ><a href="#27">4.a. <tt >Single Voxel Curve</tt></a></li><li ><a href="#29">4.b. <tt >Sensitivity Analysis</tt></a></li><li ><a href="#31">5. Notes</a></li><li ><a href="#32">5.a. Notes specific to <tt >qmt_sirfse</tt></a></li><li ><a href="#33">5.b. Generic notes</a></li><li ><a href="#34">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</a></li><li ><a href="#38">5.b.2 Parallelization</a></li><li ><a href="#40">6. Citations</a></li></ul></div><pre class="codeinput"><span class="comment">% This m-file has been automatically generated using qMRgenBatch(qmt_sirfse)</span>
	<span class="comment">% for publishing documentation.</span>
	<span class="comment">% Command Line Interface (CLI) is well-suited for automatization</span>
	<span class="comment">% purposes and Octave.</span>
	<span class="comment">%</span>
	<span class="comment">% Please execute this m-file section by section to get familiar with batch</span>
	<span class="comment">% processing for qmt_sirfse on CLI.</span>
	<span class="comment">%</span>
	<span class="comment">% Demo files are downloaded into qmt_sirfse_data folder.</span>
	<span class="comment">%</span>
	<span class="comment">% Written by: Agah Karakuzu, 2017</span>
	<span class="comment">% ==============================================================================</span>
	</pre><h2 id="2">1. Print <tt >qmt_sirfse</tt> information</h2><pre class="codeinput">qMRinfo(<span class="string">'qmt_sirfse'</span>);
	</pre><pre class="codeoutput">  qmt_sirfse:  qMT using Inversion Recovery Fast Spin Echo acquisition
	<a href="matlab: figure, imshow qmt_sirfse.png ;">Pulse Sequence Diagram</a>
	
	ASSUMPTIONS:
	(1) FILL
	(2)
	(3)
	(4)
	
	Inputs:
	MTdata              Magnetization Transfert data
	(R1map)             1/T1map (OPTIONAL but recommended)
	(Mask)              Binary mask to accelerate the fitting (OPTIONAL)
	
	Outputs:
	F                   Ratio of number of restricted pool to free pool, defined
	as F = M0r/M0f = kf/kr.
	kr                  Exchange rate from the free to the restricted pool
	(note that kf and kr are related to one another via the
	definition of F. Changing the value of kf will change kr
	accordingly, and vice versa).
	R1f                 Longitudinal relaxation rate of the free pool
	(R1f = 1/T1f).
	R1r                 Longitudinal relaxation rate of the restricted pool
	(R1r = 1/T1r).
	Sf                  Instantaneous fraction of magnetization after vs. before
	the pulse in the free pool. Starting point is computed using Block
	simulation.
	Sr                  Instantaneous fraction of magnetization after vs. before
	the pulse in the restricted pool. Starting point is computed using block
	simulation.
	M0f                 Equilibrium value of the free pool longitudinal
	magnetization.
	(M0r)               Equilibrium value of the restricted pool longitudinal
	magnetization. Computed using M0f = M0r * F.
	(kf)                Exchange rate from the restricted to the free pool.
	Computed using kf = kr * F.
	(resnorm)           Fitting residual.
	
	Protocol:
	MTdata
	Ti                Inversion times (s)
	Td                Delay times (s)
	
	FSEsequence
	Trf               Duration of the pulses in the FSE sequence (s)
	Tr                Delay between the pulses in the FSE sequnece (s)
	Npulse            Number of refocusing pulses in the FSE sequence
	
	Options:
	Inversion Pulse
	Shape             Shape of the inversion pulse.
	Available shapes are:
	- hard
	- gaussian
	- gausshann (gaussian pulse with Hanning window)
	- sinc
	- sinchann (sinc pulse with Hanning window)
	- singauss (sinc pulse with gaussian window)
	- fermi
	Duration          Duration of the inversion pulse (s)
	
	Fitting
	Use R1map to      By checking this box, you tell the fitting
	constrain R1f       algorithm to check for an observed R1map and use
	its value to constrain R1f. Checking this box
	will automatically set the R1f fix box to true in
	the Fit parameters table.
	Fix R1r = R1f     By checking this box, you tell the fitting
	algorithm to fix R1r equal to R1f. Checking this
	box will automatically set the R1r fix box to
	true in the Fit parameters table.
	
	Sr Calculation
	Lineshape         The absorption lineshape of the restricted pool. Available lineshapes are: Gaussian, Lorentzian and SuperLorentzian.
	T2r               Transverse relaxation time of the restricted pool (T2r = 1/R2r)
	
	Example of command line usage:
	For more examples: <a href="matlab: qMRusage(qmt_sirfse);">qMRusage(qmt_sirfse)</a>
	
	Author: Ian Gagnon, 2017
	
	Reference page in Doc Center
	doc qmt_sirfse
	
	
	</pre><h2 id="3">2. Setting model parameters</h2><h2 id="4">2.a. Create <tt >qmt_sirfse</tt> object</h2><pre class="codeinput">Model = qmt_sirfse;
	</pre><h2 id="5">2.b. Set <tt >protocol</tt> and <tt >options</tt></h2><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Protocol:</u></b> <i >MRI acquisition parameters that are accounted for by the respective model.</i></p>
	</div>
	</p><p >For example: <tt >TE</tt>, <tt >TR</tt>, <tt >FA</tt> <tt >FieldStrength</tt>. The assigned <tt >protocol</tt> values are subjected to a sanity check to ensure that they are in agreement with the <tt >data</tt> attributes.</p><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Options:</u></b> <i >Fitting preferences that are left at user's discretion.</i></p>
	</div>
	</p><p >For example: <tt >linear fit</tt>, <tt >exponential fit</tt>, <tt >drop first echo</tt>.</p><h2 id="8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></h2><p >If you are using Octave, or would like to serialize your operations any without <tt >GUI</tt> involvement, you can assign <tt >protocol</tt> directly in CLI:</p><pre class="codeinput">Ti = [0.0030; 0.0037; 0.0047; 0.0058; 0.0072; 0.0090; 0.0112; 0.0139; 0.0173; 0.0216; 0.0269; 0.0335; 0.0417; 0.0519; 0.0646; 0.0805; 0.1002; 0.1248; 0.1554; 0.1935; 0.2409; 0.3000; 1.0000; 2.0000; 10.0000];
	<span class="comment">% Ti is a vector of [25X1]</span>
	Td = [3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000; 3.5000];
	<span class="comment">% Td is a vector of [25X1]</span>
	Model.Prot.MTdata.Mat = [ Ti Td];
	</pre><pre class="codeinput">Trf  = 0.001;
	Tr  = 0.01;
	Npulse = 16;
	Model.Prot.FSEsequence.Mat = [ Trf  Tr  Npulse];
	</pre><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for further information. </p>
	</div>
	</p><h2 id="12">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></h2><p >The following command opens a panel to set <tt >protocol</tt> and <tt >options</tt> (if <tt >GUI</tt> is available to the user):</p><pre class="language-matlab">Model = Custom_OptionsGUI(Model);
	</pre><p ><img vspace="5" hspace="5" src="https://github.com/qMRLab/doc_images/blob/main/usr/protPanels/qmt_sirfse.png?raw=true" alt=""> </p><p ><i >If available, you need to close this panel for the remaining of the script to proceed.</i></p><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Using this panel, you can save qMRLab protocol files that can be used in both interfaces. See the <a href="#36">generic notes</a> section below for details. </p>
	</div>
	</p><h2 id="16">3. Fit MRI data</h2><h2 id="17">3.a. <b >Load</b> input data</h2><p >This section shows how you can load data into a(n) <tt >qmt_sirfse</tt> object.</p><div ><ul ><li >At the CLI level, qMRLab accepts structs containing (<tt >double</tt>) data in the fields named in accordance with a qMRLab model.</li></ul></div><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-umbrella" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for BIDS compatible wrappers and scalable <br >        qMRLab workflows. </p>
	</div>
	</p><pre class="codeinput"><span class="comment">%          |- qmt_sirfse object needs 3 data input(s) to be assigned:</span>
	<span class="comment">%          |-   MTdata</span>
	<span class="comment">%          |-   R1map</span>
	<span class="comment">%          |-   Mask</span>
	
	data = struct();
	<span class="comment">% MTdata.nii.gz contains [128  128    1   25] data.</span>
	data.MTdata=double(load_nii_data(<span class="string">'qmt_sirfse_data/MTdata.nii.gz'</span>));
	<span class="comment">% Mask.nii.gz contains [128  128] data.</span>
	data.Mask=double(load_nii_data(<span class="string">'qmt_sirfse_data/Mask.nii.gz'</span>));
	</pre><h2 id="19">3.b. Execute fitting process</h2><p >This section will fit the loaded data.</p><pre class="language-matlab">FitResults = FitData(data,Model,0);
	</pre><p >
	<div class="danger">
	<p style="margin:0px!important;"><strong ><i class="fa fa-umbrella" style="color:red;margin-left:5px;"></i></strong> Visit the <a href="#36">generic notes</a> section below for instructions to accelerate fitting by <br >       parallelization using <code >ParFitData</code>. </p>
	</div>
	</p><h2 id="22">3.c. Display <tt >FitResults</tt></h2><p >You can display the current outputs by:</p><pre class="language-matlab">qMRshowOutput(FitResults,data,Model);
	</pre><p ><i >A representative fit curve will be plotted if available.</i></p><p >To render images in this page, we will load the fit results that had been saved before. You can skip the following code block;</p><pre class="codeinput"><span class="comment">% Load FitResults that comes with the example dataset.</span>
	FitResults_old = load(<span class="string">'FitResults/FitResults.mat'</span>);
	qMRshowOutput(FitResults_old,data,Model);
	</pre><img vspace="5" hspace="5" src="_static/qmt_sirfse_batch_01.png" alt=""> <img vspace="5" hspace="5" src="_static/qmt_sirfse_batch_02.png" alt=""> <h2 id="23">3.d. Save fit results</h2><p >Outputs can be saved as <tt >*.nii.(gz)</tt> if <tt >NIfTI</tt> inputs are available:</p><pre class="language-matlab"><span class="comment">% Generic function call to save nifti outputs</span>
	FitResultsSave_nii(FitResults, <span class="string">'reference/nifti/file.nii.(gz)'</span>);
	</pre><p >If not, <tt >FitResults.mat</tt> file can be saved. This file contains all the outputs as workspace variables:</p><pre class="language-matlab"><span class="comment">% Generic function call to save FitResults.mat</span>
	FitResultsSave_mat(FitResults);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-clone" style="color:navy;margin-left:5px;"></i></strong> <code >FitResults.mat</code> files can be loaded to qMRLab <code >GUI</code> for <a href="l#data-viewer" target="_blank">visualization and ROI <br >        analyses</a>. </p>
	</div>
	</p><p >The section below will be dynamically generated in accordance with the example data format (<tt >mat</tt> or <tt >nii</tt>). You can substitute <tt >FitResults_old</tt> with <tt >FitResults</tt> if you executed the fitting using example dataset for this model in section <b >3.b.</b>.</p><pre class="codeinput">FitResultsSave_nii(FitResults_old, <span class="string">'qmt_sirfse_data/MTdata.nii.gz'</span>);
	</pre><h2 id="25">3.e. Re-use or share fit configuration files</h2><p >qMRLab's fit configuration files (<tt >qmt_sirfse_Demo.qmrlab.mat</tt>) store all the <tt >options</tt> and <tt >protocol</tt> in relation to the used model and the release version.</p><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-retweet" style="color:navy;margin-left:5px;"></i></strong> <code >*.qmrlab.mat</code> files can be easily shared with collaborators to allow them fit their own <br >       data or run simulations using identical <code >option</code> and <code >protocol</code> configurations. </p>
	</div>
	</p><pre class="codeinput">Model.saveObj(<span class="string">'my_qmt_sirfse_config.qmrlab.mat'</span>);
	</pre><h2 id="26">4. Simulations</h2><h2 id="27">4.a. <tt >Single Voxel Curve</tt></h2><p >
	<details >
	<summary >Simulates single voxel curves</summary>
	<ol >
	<li >Analytically generate synthetic MRI data</li>
	<li >Add <i >rician</i> noise</li>
	<li ><tt >Fit</tt> and <tt >plot</tt> the respective curve</li>
	</ol>
	</details>
	</p><pre class="codeinput">      x = struct;
	x.F = 0.1;
	x.kr = 30;
	x.R1f = 1;
	x.R1r = 1;
	x.Sf = -0.98419;
	x.Sr = 0.65638;
	x.M0f = 1;
	<span class="comment">% Set simulation options</span>
	Opt.SNR = 50;
	Opt.Method = <span class="string">'Analytical equation'</span>;
	Opt.T2fUsedinBlockequation = 0.04;
	<span class="comment">% run simulation</span>
	figure(<span class="string">'Name'</span>,<span class="string">'Single Voxel Curve Simulation'</span>);
	FitResult = Model.Sim_Single_Voxel_Curve(x,Opt);
	</pre><img vspace="5" hspace="5" src="_static/qmt_sirfse_batch_03.png" alt=""> <h2 id="29">4.b. <tt >Sensitivity Analysis</tt></h2><p >
	<details >
	<summary >Simulates sensitivity to fitted parameters</summary>
	<ol >
	<li >Iterate fitting parameters from lower (<tt >lb</tt>) to upper (<tt >ub</tt>) bound</li>
	<li >Run <tt >Sim_Single_Voxel_Curve</tt> for <tt >Nofruns</tt> times</li>
	<li >Compute the <tt >mean</tt> and <tt >std</tt> across runs</li>
	</ol>
	</details>
	</p><pre >            F             kr            R1f           R1r           Sf            Sr            M0f</pre><pre class="codeinput">      OptTable.st = [0.1           30            1             1             -0.98         0.66          1]; <span class="comment">% nominal values</span>
	OptTable.fx = [0             1             1             1             1             1             1]; <span class="comment">%vary F...</span>
	OptTable.lb = [0.0001        0.0001        0.05          0.05          -1            0.0001        0.0001]; <span class="comment">%...from 0.0001</span>
	OptTable.ub = [1             1e+02         10            10            0             1             2]; <span class="comment">%...to 1</span>
	<span class="comment">% Set simulation options</span>
	Opt.SNR = 50;
	Opt.Method = <span class="string">'Analytical equation'</span>;
	Opt.T2fUsedinBlockequation = 0.04;
	Opt.Nofrun = 5;
	<span class="comment">% run simulation</span>
	SimResults = Model.Sim_Sensitivity_Analysis(OptTable,Opt);
	figure(<span class="string">'Name'</span>,<span class="string">'Sensitivity Analysis'</span>);
	SimVaryPlot(SimResults, <span class="string">'F'</span> ,<span class="string">'F'</span> );
	</pre><img vspace="5" hspace="5" src="_static/qmt_sirfse_batch_04.png" alt=""> <h2 id="31">5. Notes</h2><h2 id="32">5.a. Notes specific to <tt >qmt_sirfse</tt></h2><p >
	<div class="warning" style="text-align:justify;">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Not provided.</p>
	</div>
	</p><h2 id="33">5.b. Generic notes</h2><h2 id="34">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</h2><p >If you would like to load a desired set of <tt >options</tt> / <tt >protocols</tt> programatically, you can use <tt >*.qmrlab.mat</tt> files. To save a configuration from the <tt >protocol</tt> panel of <tt >qmt_sirfse</tt>, first open the respective panel by running the following command in your MATLAB command window (MATLAB only):</p><pre class="language-matlab">Custom_OptionsGUI(qmt_sirfse);
	</pre><p >In this panel, you can arrange available <tt >options</tt> and <tt >protocols</tt> according to your needs, then click the <tt >save</tt> button to save <tt >my_qmt_sirfse.qmrlab.mat</tt> file. This file can be later loaded into a <tt >qmt_sirfse</tt> object in batch by:</p><pre class="language-matlab">Model = qmt_sirfse;
	Model = Model.loadObj(<span class="string">'my_qmt_sirfse.qmrlab.mat'</span>);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >Model.loadObj('my_qmt_sirfse.qmrlab.mat')</code> call won't update the fields in the <code >Model</code> object, unless the output is assigned to the object as shown above. This compromise on convenience is to retain Octave CLI compatibility. </p>
	</div>
	</p><p ><b >If you don't have MATLAB, hence cannot access the <tt >GUI</tt>, two alternatives are available to populate <tt >options</tt>:</b></p><div ><ol ><li >Use <tt >qmrlab/mcrgui:latest</tt> Docker image to access <tt >GUI</tt>. The instructions are available <a href="https://hub.docker.com/r/qmrlab/mcrgui">here</a>.</li><li >Set <tt >options</tt> and <tt >protocols</tt> in <tt >CLI</tt>:</li></ol></div><div ><ul ><li >List available option fields using tab completion in Octave's command prompt (or window)</li></ul></div><pre class="language-matlab">Model = qmt_sirfse;
	Model.option. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><div ><ul ><li >Assign the desired field. <b >For example</b>, for a <tt >mono_t2</tt> object:</li></ul></div><pre class="language-matlab">Model = mono_t2;
	Model.options.DropFirstEcho = true;
	Model.options.OffsetTerm = false;
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Some option fields may be mutually exclusive or interdependent. Such cases are handled  by the <code >GUI</code> options panel; however, not exposed to the <code >CLI</code>. Therefore, manual <code >CLI</code> <code >options</code> assignments may be challenging for some involved methods such as <code >qmt_spgr</code> or <code >qsm_sb</code>. If above options are not working for you and you cannot infer how to set options solely in batch, please feel free to <a href="https://github.com/qmrlab/qmrlab" target="_blank">open an issue in qMRLab</a> and request the protocol file you need. </p>
	</div>
	</p><p ><b >Similarly, in CLI, you can inspect and assign the <tt >protocols</tt>:</b></p><pre class="language-matlab">Model = qmt_sirfse;
	Model.Prot. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><p >Each protocol field has two subfields of <tt >Format</tt> and <tt >Mat</tt>. The first one is a <tt >cell</tt> indicating the name of the protocol parameter (such as <tt >EchoTime (ms)</tt>) and the latter one contains the respective values (such as <tt >30 x 1 double</tt> array containing <tt >EchoTimes</tt>).</p><p >
	<div class="warning">
	<p style="margin:0px!important;"> The default <code >Mat</code> protocol values are set according to the example datasets served via <a href="https://osf.io/tmdfu" target="_blank">OSF</a>.</p>
	</div>
	</p><h2 id="38">5.b.2 Parallelization</h2><p >Beginning from release <tt >2.5.0</tt>, you can accelerate fitting for the <tt >voxelwise</tt> models using parallelization.</p><p >
	<div class="danger">
	<p style="margin:0px!important;"> <strong >Available in MATLAB only. Requires <code >parallel processing toolbox</code>.</strong></p>
	</div>
	</p><p >In <tt >CLI</tt>, you can perform parallel fitting by:</p><pre class="language-matlab">parpool();
	FitResults = ParFitData(data,Model);
	</pre><p >If a <tt >parpool</tt> exists, the <tt >ParFitData</tt> will use it. If not, a new pool will be created using the local profile. By default, <tt >ParFitData</tt> saves outputs automatically every 5 minutes. You can disable this feature by:</p><pre class="language-matlab">FitResults = ParFitData(data, Model, <span class="string">'AutosaveEnabled'</span>, false);
	</pre><p >Alternatively, you can change the autosave interval (min 1 min) by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'AutoSaveInterval'</span>,10);
	</pre><p >If something went wrong during the fitting (e.g. your computer had to be restarted), you can recover the autosaved data by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'RecoverDirectory'</span>,<span class="string">'/ParFitTempResults_*/folder/from/the/previous/session'</span>);
	</pre><p ><tt >GUI</tt> users will be prompted a question about whether they would like to use parallelization after clicking the <tt >Fit Data</tt> button, if the conditions are met. When called from <tt >GUI</tt>, <tt >ParFitData</tt> will be run with default options:</p><div ><ul ><li >Save temporary results every <tt >5</tt> minutes or whenever a chunk has finished processing</li><li >Split data into chunks with a <tt >granularity</tt> factor of <tt >3</tt></li><li >Do not remove temporary fit results upon completion</li></ul></div><p >For further information:</p><pre class="language-matlab">help <span class="string">ParFitData</span>
	</pre><p >The default <tt >parallelization</tt> options can be changed in the <tt >preferences.json</tt> file located at the root qMRLab directory.</p><h2 id="40">6. Citations</h2><p ><b >qMRLab JOSS article</b></p><p >
	<div class="success" style="text-align:justify;">
	<p > Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: Quantitative MRI analysis, under one umbrella <a href="https://doi.org/10.21105/joss.02343" target="_blank">10.21105/joss.02343</a></p>
	</div>
	</p><p ><b >Reference article for <tt >qmt_sirfse</tt></b></p><p >
	<div class="success" style="text-align:justify;">
	Li, K., et al. (2010). Optimized inversion recovery sequences for quantitative T1 and magnetization transfer imaging. Magnetic Resonance in Medicine, 64(2), 491-500. 10.1002/mrm.22440
	</div>
	</p><p >
	<hr >
	<center ><i class="fa fa-umbrella" style="color:black;font-size:2em;"></i></center>
	<center ><p >Quantitative MRI, under one umbrella.</p></center>
	<center >| <a href="https://github.com/qmrlab/pulse_sequences" target="_blank">qMRPullseq</a> | <a href="https://github.com/qmrlab/qmrflow" target="_blank">qMRFlow</a> | <a href="https://qmrlab.org/blog.html" target="_blank">Interactive Tutorials</a> | </p></center>
	<center ><p ><a href="https://www.neuro.polymtl.ca/doku.php" target="_blank">NeuroPoly Lab</a>, Montreal, Canada</p></center>
	<hr >
	</p><p class="footer"><br ><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB® R2018b</a><br ></p></div>
