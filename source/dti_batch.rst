dti: Compute a tensor from diffusion data
=========================================

.. image:: https://mybinder.org/badge_logo.svg
 :target: https://mybinder.org/v2/gh/qMRLab/doc_notebooks/master?filepath=dti_notebook.ipynb
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
	</style><div class="content"><h2 >Contents</h2><div ><ul ><li ><a href="#2">1. Print <tt >dti</tt> information</a></li><li ><a href="#3">2. Setting model parameters</a></li><li ><a href="#4">2.a. Create <tt >dti</tt> object</a></li><li ><a href="#5">2.b. Set <tt >protocol</tt> and <tt >options</tt></a></li><li ><a href="#8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></a></li><li ><a href="#11">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></a></li><li ><a href="#15">3. Fit MRI data</a></li><li ><a href="#16">3.a. <b >Load</b> input data</a></li><li ><a href="#18">3.b. Execute fitting process</a></li><li ><a href="#21">3.c. Display <tt >FitResults</tt></a></li><li ><a href="#22">3.d. Save fit results</a></li><li ><a href="#24">3.e. Re-use or share fit configuration files</a></li><li ><a href="#25">4. Simulations</a></li><li ><a href="#26">4.a. <tt >Single Voxel Curve</tt></a></li><li ><a href="#28">4.b. <tt >Sensitivity Analysis</tt></a></li><li ><a href="#30">5. Notes</a></li><li ><a href="#31">5.a. Notes specific to <tt >dti</tt></a></li><li ><a href="#32">5.b. Generic notes</a></li><li ><a href="#33">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</a></li><li ><a href="#37">5.b.2 Parallelization</a></li><li ><a href="#39">6. Citations</a></li></ul></div><pre class="codeinput"><span class="comment">% This m-file has been automatically generated using qMRgenBatch(dti)</span>
	<span class="comment">% for publishing documentation.</span>
	<span class="comment">% Command Line Interface (CLI) is well-suited for automatization</span>
	<span class="comment">% purposes and Octave.</span>
	<span class="comment">%</span>
	<span class="comment">% Please execute this m-file section by section to get familiar with batch</span>
	<span class="comment">% processing for dti on CLI.</span>
	<span class="comment">%</span>
	<span class="comment">% Demo files are downloaded into dti_data folder.</span>
	<span class="comment">%</span>
	<span class="comment">% Written by: Agah Karakuzu, 2017</span>
	<span class="comment">% ==============================================================================</span>
	</pre><h2 id="2">1. Print <tt >dti</tt> information</h2><pre class="codeinput">qMRinfo(<span class="string">'dti'</span>);
	</pre><pre class="codeoutput"> dti: Compute a tensor from diffusion data
	
	Assumptions:
	Anisotropic Gaussian diffusion tensor
	Valid at relatively low b-value (i.e. ~< 2000 s/mm2)
	
	Inputs:
	DiffusionData       4D DWI
	(SigmaNoise)        map of the standard deviation of the noise per voxel. (OPTIONAL)
	(Mask)              Binary mask to accelerate the fitting. (OPTIONAL)
	
	Outputs:
	D                   [Dxx Dxy Dxz Dxy Dyy Dyz Dxz Dyz Dzz] Diffusion Tensor
	L1                  1rst eigenvalue of D
	L2                  2nd eigenvalue of D
	L3                  3rd eigenvalue of D
	FA                  Fractional Anisotropy: FA = sqrt(3/2)*sqrt(sum((L-L_mean).^2))/sqrt(sum(L.^2));
	S0_TEXX             Signal at b=0 at TE=XX
	(residue)           Fitting residuals
	
	Protocol:
	At least 2 shells (e.g. b=1000 and b=0 s/mm2)
	diffusion gradient direction in 3D
	
	DiffusionData       Array [NbVol x 7]
	Gx                Diffusion Gradient x
	Gy                Diffusion Gradient y
	Gz                Diffusion Gradient z
	Gnorm (T/m)         Diffusion gradient magnitude
	Delta (s)         Diffusion separation
	delta (s)         Diffusion duration
	TE (s)            Echo time
	
	Options:
	fitting type
	'linear'                              Solves the linear problem (ln(S/S0) = -bD)
	'non-linear (Rician Likelihood)'      Add an additional fitting step,
	using the Rician Likelihood.
	Rician noise bias                       only for non-linear fitting
	SigmaNoise map is prioritary.
	'Compute Sigma per voxel'             Sigma is estimated by computing the STD across repeated scans.
	'fix sigma'                           Use scd_noise_std_estimation to measure noise level. Use 'value' to fix Sigma.
	
	
	Example of command line usage (see <a href="matlab: web(which('dti_batch.html'))"> dti_batch.html</a>):
	Model = dti
	%% LOAD DATA
	data.DiffusionData = load_nii_data('DiffusionData.nii.gz');
	data.SigmaNoise = load_nii_data('SigmaNoise.nii.gz');
	data.Mask = load_nii_data('Mask.nii.gz');
	%% FIT A SINGLE VOXEL
	% Specific voxel:         datavox = extractvoxel(data,voxel);
	% Interactive selection:  datavox = extractvoxel(data);
	voxel       = round(size(data.DiffusionData(:,:,:,1))/2); % pick FOV center
	datavox     = extractvoxel(data,voxel);
	FitResults  = Model.fit(datavox);
	Model.plotModel(FitResults, datavox); % plot fit results
	%% FIT all voxels
	FitResults = FitData(data,Model);
	% SAVE results to NIFTI
	FitResultsSave_nii(FitResults,'DiffusionData.nii.gz'); % use header from 'DiffusionData.nii.gz'
	
	For more examples: <a href="matlab: qMRusage(dti);">qMRusage(dti)</a>
	
	Author: Tanguy Duval, 2016
	
	References:
	Please cite the following if you use this module:
	Basser, P.J., Mattiello, J., LeBihan, D., 1994. MR diffusion tensor spectroscopy and imaging. Biophys. J. 66, 259?267.
	In addition to citing the package:
	Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., 
	Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: 
	Quantitative MRI analysis, under one umbrella doi: 10.21105/joss.02343
	
	Reference page in Doc Center
	doc dti
	
	
	</pre><h2 id="3">2. Setting model parameters</h2><h2 id="4">2.a. Create <tt >dti</tt> object</h2><pre class="codeinput">Model = dti;
	</pre><h2 id="5">2.b. Set <tt >protocol</tt> and <tt >options</tt></h2><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Protocol:</u></b> <i >MRI acquisition parameters that are accounted for by the respective model.</i></p>
	</div>
	</p><p >For example: <tt >TE</tt>, <tt >TR</tt>, <tt >FA</tt> <tt >FieldStrength</tt>. The assigned <tt >protocol</tt> values are subjected to a sanity check to ensure that they are in agreement with the <tt >data</tt> attributes.</p><p >
	<div class="info">
	<p style="margin:0px!important;"> <b ><u >Options:</u></b> <i >Fitting preferences that are left at user's discretion.</i></p>
	</div>
	</p><p >For example: <tt >linear fit</tt>, <tt >exponential fit</tt>, <tt >drop first echo</tt>.</p><h2 id="8">2.b.1 Set <tt >protocol</tt> <i >the CLI way</i></h2><p >If you are using Octave, or would like to serialize your operations any without <tt >GUI</tt> involvement, you can assign <tt >protocol</tt> directly in CLI:</p><pre class="codeinput">Gx = [0.0000; 0.0000; 0.6528; -0.3734; 0.6595; 0.4251; 0.9307; 0.2346; -0.5629; -0.1656; -0.9726; -0.0150; 0.1463; -0.2313; 0.7377; -0.7661; -0.1051; 0.0000; 0.3909; 0.1496; -0.9334; 0.1903; -0.7039; -0.5217; 0.9662; -0.3714; -0.7828; 0.8305; -0.3302; -0.2348; 0.0253; -0.5469; 0.7053; 0.0000; 0.3198; 0.7962; 0.8699; 0.6890; -0.9299; 0.0387; 0.3218; 0.3582; 0.8944; 0.4384; -0.3516; -0.1507; -0.5361; 0.5114; -0.0808; 0.0000; -0.0261; -0.4804; -0.8220; -0.3674; -0.8059; 0.9937; -0.9844; -0.4309; 0.1316; -0.0096; 0.6996; -0.6609; 0.8179; -0.7977; 0.4352; 0.0000; 0.3330; 0.5147; -0.8173; -0.5177; -0.0540; 0.0108; -0.0691; 0.8929; 0.6656; 0.3998; 0.2992; -0.6774; -0.3221; 0.5112; -0.1681; 0.0000; 0.8415; 0.2496; 0.6320; 0.1861; 0.4758; 0.7481; 0.9338; 0.6610; 0.6125; 0.6137; 0.6817; 0.0996; -0.9739; 0.8386; 0.2920; 0.0000; -0.7056; -0.2181; -0.6203; 0.0020; -0.1074; 0.2822; 0.4012; 0.5307; 0.5323; 0.9651; 0.0000];
	<span class="comment">% Gx is a vector of [109X1]</span>
	Gy = [0.0000; 0.0000; -0.6550; 0.1688; 0.7394; 0.0347; 0.0616; -0.8169; -0.0797; -0.8647; 0.0079; 0.9886; 0.7658; -0.5711; 0.5254; 0.5946; -0.9930; 0.0000; -0.4079; -0.3372; -0.2009; 0.7622; -0.4547; 0.4241; -0.2577; 0.9198; 0.6149; -0.2333; -0.8437; -0.5578; 0.1522; -0.7771; 0.6419; 0.0000; -0.6674; -0.0672; -0.1770; 0.4593; 0.3590; 0.4492; 0.4365; 0.2082; 0.4341; -0.8638; 0.8508; 0.5115; 0.3158; -0.7514; 0.9207; 0.0000; -0.9526; -0.8692; 0.3566; -0.3033; -0.5619; -0.0273; -0.1502; -0.9023; 0.1687; -0.1114; -0.7110; -0.2140; -0.3778; -0.1210; 0.6742; 0.0000; -0.5741; -0.6575; -0.5127; 0.4818; 0.5946; -0.8315; -0.7675; 0.2597; 0.3549; -0.8171; -0.0563; -0.1344; 0.2540; 0.6731; -0.9515; 0.0000; -0.4352; 0.9109; -0.0796; -0.9773; -0.8795; 0.6348; -0.2954; -0.0966; -0.4925; -0.1628; -0.4899; 0.3862; -0.2261; 0.5426; 0.9388; 0.0000; 0.1116; 0.9406; 0.7701; 0.3742; -0.4286; -0.6551; 0.7562; 0.4305; 0.4358; -0.2538; 0.0000];
	<span class="comment">% Gy is a vector of [109X1]</span>
	Gz = [0.0000; 0.0000; 0.3807; 0.9122; 0.1356; -0.9045; 0.3607; -0.5270; -0.8227; 0.4743; 0.2325; -0.1496; -0.6262; -0.7876; -0.4240; 0.2441; 0.0536; 0.0000; 0.8251; 0.9295; -0.2972; 0.6187; 0.5456; 0.7403; -0.0065; -0.1266; 0.0958; 0.5057; -0.4233; 0.7961; 0.9880; 0.3116; 0.3009; 0.0000; 0.6726; -0.6012; -0.4604; 0.5607; -0.0796; 0.8926; -0.8402; 0.9101; -0.1075; -0.2483; 0.3905; 0.8460; -0.7829; 0.4170; -0.3819; 0.0000; -0.3031; 0.1170; 0.4439; -0.8792; -0.1865; 0.1090; 0.0921; 0.0165; -0.9768; 0.9937; 0.0714; 0.7193; 0.4339; -0.5907; -0.5967; 0.0000; -0.7480; -0.5502; -0.2629; -0.7070; -0.8022; 0.5555; -0.6373; -0.3679; 0.6565; 0.4153; 0.9525; 0.7233; 0.9120; 0.5345; -0.2576; 0.0000; 0.3202; -0.3285; -0.7708; -0.1011; 0.0065; -0.1930; -0.2018; 0.7442; 0.6183; -0.7725; -0.5434; 0.9170; -0.0219; -0.0485; 0.1827; 0.0000; -0.6998; 0.2600; 0.1488; 0.9274; 0.8971; -0.7009; -0.5169; 0.7301; -0.7258; 0.0647; 0.0000];
	<span class="comment">% Gz is a vector of [109X1]</span>
	Gnorm = [0.0000; 0.0000; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0310; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0000; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0310; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0000; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0310; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0000; 0.0800; 0.0566; 0.0800; 0.0800; 0.0310; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0000; 0.0566; 0.0800; 0.0800; 0.0310; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0000; 0.0800; 0.0800; 0.0310; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0000; 0.0800; 0.0310; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0800; 0.0800; 0.0566; 0.0000];
	<span class="comment">% Gnorm is a vector of [109X1]</span>
	Delta = [0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308; 0.0308];
	<span class="comment">% Delta is a vector of [109X1]</span>
	delta = [0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128; 0.0128];
	<span class="comment">% delta is a vector of [109X1]</span>
	TE = [0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636; 0.0636];
	<span class="comment">% TE is a vector of [109X1]</span>
	Model.Prot.DiffusionData.Mat = [ Gx Gy Gz Gnorm Delta delta TE];
	</pre><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for further information. </p>
	</div>
	</p><h2 id="11">2.b.2 Set <tt >protocol</tt> and <tt >options</tt> <i >the GUI way</i></h2><p >The following command opens a panel to set <tt >protocol</tt> and <tt >options</tt> (if <tt >GUI</tt> is available to the user):</p><pre class="language-matlab">Model = Custom_OptionsGUI(Model);
	</pre><p ><img vspace="5" hspace="5" src="https://github.com/qMRLab/doc_images/blob/main/usr/protPanels/dti.png?raw=true" alt=""> </p><p ><i >If available, you need to close this panel for the remaining of the script to proceed.</i></p><p >
	<div class="warning">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Using this panel, you can save qMRLab protocol files that can be used in both interfaces. See the <a href="#36">generic notes</a> section below for details. </p>
	</div>
	</p><h2 id="15">3. Fit MRI data</h2><h2 id="16">3.a. <b >Load</b> input data</h2><p >This section shows how you can load data into a(n) <tt >dti</tt> object.</p><div ><ul ><li >At the CLI level, qMRLab accepts structs containing (<tt >double</tt>) data in the fields named in accordance with a qMRLab model.</li></ul></div><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-umbrella" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#36">generic notes</a> section below for BIDS compatible wrappers and scalable <br >        qMRLab workflows. </p>
	</div>
	</p><pre class="codeinput"><span class="comment">%          |- dti object needs 3 data input(s) to be assigned:</span>
	<span class="comment">%          |-   DiffusionData</span>
	<span class="comment">%          |-   SigmaNoise</span>
	<span class="comment">%          |-   Mask</span>
	
	data = struct();
	<span class="comment">% DiffusionData.nii.gz contains [74   87   50  109] data.</span>
	data.DiffusionData=double(load_nii_data(<span class="string">'dti_data/DiffusionData.nii.gz'</span>));
	<span class="comment">% Mask.nii.gz contains [74  87  50] data.</span>
	data.Mask=double(load_nii_data(<span class="string">'dti_data/Mask.nii.gz'</span>));
	</pre><h2 id="18">3.b. Execute fitting process</h2><p >This section will fit the loaded data.</p><pre class="language-matlab">FitResults = FitData(data,Model,0);
	</pre><p >
	<div class="danger">
	<p style="margin:0px!important;"><strong ><i class="fa fa-umbrella" style="color:red;margin-left:5px;"></i></strong> Visit the <a href="#36">generic notes</a> section below for instructions to accelerate fitting by <br >       parallelization using <code >ParFitData</code>. </p>
	</div>
	</p><h2 id="21">3.c. Display <tt >FitResults</tt></h2><p >You can display the current outputs by:</p><pre class="language-matlab">qMRshowOutput(FitResults,data,Model);
	</pre><p ><i >A representative fit curve will be plotted if available.</i></p><p >To render images in this page, we will load the fit results that had been saved before. You can skip the following code block;</p><pre class="codeinput"><span class="comment">% Load FitResults that comes with the example dataset.</span>
	FitResults_old = load(<span class="string">'FitResults/FitResults.mat'</span>);
	qMRshowOutput(FitResults_old,data,Model);
	</pre><img vspace="5" hspace="5" src="_static/dti_batch_01.png" alt=""> <img vspace="5" hspace="5" src="_static/dti_batch_02.png" alt=""> <h2 id="22">3.d. Save fit results</h2><p >Outputs can be saved as <tt >*.nii.(gz)</tt> if <tt >NIfTI</tt> inputs are available:</p><pre class="language-matlab"><span class="comment">% Generic function call to save nifti outputs</span>
	FitResultsSave_nii(FitResults, <span class="string">'reference/nifti/file.nii.(gz)'</span>);
	</pre><p >If not, <tt >FitResults.mat</tt> file can be saved. This file contains all the outputs as workspace variables:</p><pre class="language-matlab"><span class="comment">% Generic function call to save FitResults.mat</span>
	FitResultsSave_mat(FitResults);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-clone" style="color:navy;margin-left:5px;"></i></strong> <code >FitResults.mat</code> files can be loaded to qMRLab <code >GUI</code> for <a href="l#data-viewer" target="_blank">visualization and ROI <br >        analyses</a>. </p>
	</div>
	</p><p >The section below will be dynamically generated in accordance with the example data format (<tt >mat</tt> or <tt >nii</tt>). You can substitute <tt >FitResults_old</tt> with <tt >FitResults</tt> if you executed the fitting using example dataset for this model in section <b >3.b.</b>.</p><pre class="codeinput">FitResultsSave_nii(FitResults_old, <span class="string">'dti_data/DiffusionData.nii.gz'</span>);
	</pre><h2 id="24">3.e. Re-use or share fit configuration files</h2><p >qMRLab's fit configuration files (<tt >dti_Demo.qmrlab.mat</tt>) store all the <tt >options</tt> and <tt >protocol</tt> in relation to the used model and the release version.</p><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-retweet" style="color:navy;margin-left:5px;"></i></strong> <code >*.qmrlab.mat</code> files can be easily shared with collaborators to allow them fit their own <br >       data or run simulations using identical <code >option</code> and <code >protocol</code> configurations. </p>
	</div>
	</p><pre class="codeinput">Model.saveObj(<span class="string">'my_dti_config.qmrlab.mat'</span>);
	</pre><h2 id="25">4. Simulations</h2><h2 id="26">4.a. <tt >Single Voxel Curve</tt></h2><p >
	<details >
	<summary >Simulates single voxel curves</summary>
	<ol >
	<li >Analytically generate synthetic MRI data</li>
	<li >Add <i >rician</i> noise</li>
	<li ><tt >Fit</tt> and <tt >plot</tt> the respective curve</li>
	</ol>
	</details>
	</p><pre class="codeinput">      x = struct;
	x.L1 = 2;
	x.L2 = 0.7;
	x.L3 = 0.7;
	Opt.SNR = 50;
	<span class="comment">% run simulation</span>
	figure(<span class="string">'Name'</span>,<span class="string">'Single Voxel Curve Simulation'</span>);
	FitResult = Model.Sim_Single_Voxel_Curve(x,Opt);
	</pre><img vspace="5" hspace="5" src="_static/dti_batch_03.png" alt=""> <h2 id="28">4.b. <tt >Sensitivity Analysis</tt></h2><p >
	<details >
	<summary >Simulates sensitivity to fitted parameters</summary>
	<ol >
	<li >Iterate fitting parameters from lower (<tt >lb</tt>) to upper (<tt >ub</tt>) bound</li>
	<li >Run <tt >Sim_Single_Voxel_Curve</tt> for <tt >Nofruns</tt> times</li>
	<li >Compute the <tt >mean</tt> and <tt >std</tt> across runs</li>
	</ol>
	</details>
	</p><pre >            L1            L2            L3</pre><pre class="codeinput">      OptTable.st = [2             0.7           0.7]; <span class="comment">% nominal values</span>
	OptTable.fx = [0             1             1]; <span class="comment">%vary L1...</span>
	OptTable.lb = [0             0             0]; <span class="comment">%...from 0</span>
	OptTable.ub = [5             5             5]; <span class="comment">%...to 5</span>
	Opt.SNR = 50;
	Opt.Nofrun = 5;
	<span class="comment">% run simulation</span>
	SimResults = Model.Sim_Sensitivity_Analysis(OptTable,Opt);
	figure(<span class="string">'Name'</span>,<span class="string">'Sensitivity Analysis'</span>);
	SimVaryPlot(SimResults, <span class="string">'L1'</span> ,<span class="string">'L1'</span> );
	</pre><img vspace="5" hspace="5" src="_static/dti_batch_04.png" alt=""> <h2 id="30">5. Notes</h2><h2 id="31">5.a. Notes specific to <tt >dti</tt></h2><p >
	<div class="warning" style="text-align:justify;">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Not provided.</p>
	</div>
	</p><h2 id="32">5.b. Generic notes</h2><h2 id="33">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</h2><p >If you would like to load a desired set of <tt >options</tt> / <tt >protocols</tt> programatically, you can use <tt >*.qmrlab.mat</tt> files. To save a configuration from the <tt >protocol</tt> panel of <tt >dti</tt>, first open the respective panel by running the following command in your MATLAB command window (MATLAB only):</p><pre class="language-matlab">Custom_OptionsGUI(dti);
	</pre><p >In this panel, you can arrange available <tt >options</tt> and <tt >protocols</tt> according to your needs, then click the <tt >save</tt> button to save <tt >my_dti.qmrlab.mat</tt> file. This file can be later loaded into a <tt >dti</tt> object in batch by:</p><pre class="language-matlab">Model = dti;
	Model = Model.loadObj(<span class="string">'my_dti.qmrlab.mat'</span>);
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >Model.loadObj('my_dti.qmrlab.mat')</code> call won't update the fields in the <code >Model</code> object, unless the output is assigned to the object as shown above. This compromise on convenience is to retain Octave CLI compatibility. </p>
	</div>
	</p><p ><b >If you don't have MATLAB, hence cannot access the <tt >GUI</tt>, two alternatives are available to populate <tt >options</tt>:</b></p><div ><ol ><li >Use <tt >qmrlab/mcrgui:latest</tt> Docker image to access <tt >GUI</tt>. The instructions are available <a href="https://hub.docker.com/r/qmrlab/mcrgui">here</a>.</li><li >Set <tt >options</tt> and <tt >protocols</tt> in <tt >CLI</tt>:</li></ol></div><div ><ul ><li >List available option fields using tab completion in Octave's command prompt (or window)</li></ul></div><pre class="language-matlab">Model = dti;
	Model.option. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><div ><ul ><li >Assign the desired field. <b >For example</b>, for a <tt >mono_t2</tt> object:</li></ul></div><pre class="language-matlab">Model = mono_t2;
	Model.options.DropFirstEcho = true;
	Model.options.OffsetTerm = false;
	</pre><p >
	<div class="info">
	<p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Some option fields may be mutually exclusive or interdependent. Such cases are handled  by the <code >GUI</code> options panel; however, not exposed to the <code >CLI</code>. Therefore, manual <code >CLI</code> <code >options</code> assignments may be challenging for some involved methods such as <code >qmt_spgr</code> or <code >qsm_sb</code>. If above options are not working for you and you cannot infer how to set options solely in batch, please feel free to <a href="https://github.com/qmrlab/qmrlab" target="_blank">open an issue in qMRLab</a> and request the protocol file you need. </p>
	</div>
	</p><p ><b >Similarly, in CLI, you can inspect and assign the <tt >protocols</tt>:</b></p><pre class="language-matlab">Model = dti;
	Model.Prot. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
	</pre><p >Each protocol field has two subfields of <tt >Format</tt> and <tt >Mat</tt>. The first one is a <tt >cell</tt> indicating the name of the protocol parameter (such as <tt >EchoTime (ms)</tt>) and the latter one contains the respective values (such as <tt >30 x 1 double</tt> array containing <tt >EchoTimes</tt>).</p><p >
	<div class="warning">
	<p style="margin:0px!important;"> The default <code >Mat</code> protocol values are set according to the example datasets served via <a href="https://osf.io/tmdfu" target="_blank">OSF</a>.</p>
	</div>
	</p><h2 id="37">5.b.2 Parallelization</h2><p >Beginning from release <tt >2.5.0</tt>, you can accelerate fitting for the <tt >voxelwise</tt> models using parallelization.</p><p >
	<div class="danger">
	<p style="margin:0px!important;"> <strong >Available in MATLAB only. Requires <code >parallel processing toolbox</code>.</strong></p>
	</div>
	</p><p >In <tt >CLI</tt>, you can perform parallel fitting by:</p><pre class="language-matlab">parpool();
	FitResults = ParFitData(data,Model);
	</pre><p >If a <tt >parpool</tt> exists, the <tt >ParFitData</tt> will use it. If not, a new pool will be created using the local profile. By default, <tt >ParFitData</tt> saves outputs automatically every 5 minutes. You can disable this feature by:</p><pre class="language-matlab">FitResults = ParFitData(data, Model, <span class="string">'AutosaveEnabled'</span>, false);
	</pre><p >Alternatively, you can change the autosave interval (min 1 min) by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'AutoSaveInterval'</span>,10);
	</pre><p >If something went wrong during the fitting (e.g. your computer had to be restarted), you can recover the autosaved data by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'RecoverDirectory'</span>,<span class="string">'/ParFitTempResults_*/folder/from/the/previous/session'</span>);
	</pre><p ><tt >GUI</tt> users will be prompted a question about whether they would like to use parallelization after clicking the <tt >Fit Data</tt> button, if the conditions are met. When called from <tt >GUI</tt>, <tt >ParFitData</tt> will be run with default options:</p><div ><ul ><li >Save temporary results every <tt >5</tt> minutes or whenever a chunk has finished processing</li><li >Split data into chunks with a <tt >granularity</tt> factor of <tt >3</tt></li><li >Do not remove temporary fit results upon completion</li></ul></div><p >For further information:</p><pre class="language-matlab">help <span class="string">ParFitData</span>
	</pre><p >The default <tt >parallelization</tt> options can be changed in the <tt >preferences.json</tt> file located at the root qMRLab directory.</p><h2 id="39">6. Citations</h2><p ><b >qMRLab JOSS article</b></p><p >
	<div class="success" style="text-align:justify;">
	<p > Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: Quantitative MRI analysis, under one umbrella <a href="https://doi.org/10.21105/joss.02343" target="_blank">10.21105/joss.02343</a></p>
	</div>
	</p><p ><b >Reference article for <tt >dti</tt></b></p><p >
	<div class="success" style="text-align:justify;">
	Basser, P.J., et al. (1994). MR diffusion tensor spectroscopy and imaging. Biophysical Journal, 66(1), 259-267. 10.1016/S0006-3495(94)80775-1
	</div>
	</p><p >
	<hr >
	<center ><i class="fa fa-umbrella" style="color:black;font-size:2em;"></i></center>
	<center ><p >Quantitative MRI, under one umbrella.</p></center>
	<center >| <a href="https://github.com/qmrlab/pulse_sequences" target="_blank">qMRPullseq</a> | <a href="https://github.com/qmrlab/qmrflow" target="_blank">qMRFlow</a> | <a href="https://qmrlab.org/blog.html" target="_blank">Interactive Tutorials</a> | </p></center>
	<center ><p ><a href="https://www.neuro.polymtl.ca/doku.php" target="_blank">NeuroPoly Lab</a>, Montreal, Canada</p></center>
	<hr >
	</p><p class="footer"><br ><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB® R2018b</a><br ></p></div>
