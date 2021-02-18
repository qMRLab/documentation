qmt_bssfp : qMT using Balanced Steady State Free Precession acquisition
=======================================================================

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
   </style><div class="content"><h2 >Contents</h2><div ><ul ><li ><a href="#2">1. Print <tt >qmt_bssfp</tt> information</a></li><li ><a href="#3">2. Setting model parameters</a></li><li ><a href="#4">2.a. Create <tt >qmt_bssfp</tt> object</a></li><li ><a href="#5">2.b. Modify the options</a></li><li ><a href="#7">3. Fit MRI data</a></li><li ><a href="#8">3.a. Load input data</a></li><li ><a href="#10">3.b. Execute fitting process</a></li><li ><a href="#13">3.c. Display <tt >FitResults</tt></a></li><li ><a href="#14">3.d. Saving fit results</a></li><li ><a href="#16">4. Simulations</a></li><li ><a href="#17">4.a. <tt >Single Voxel Curve</tt></a></li><li ><a href="#18">4.b. <tt >Sensitivity Analysis</tt></a></li><li ><a href="#19">5. Notes</a></li><li ><a href="#20">5.a. Notes specific to <tt >qmt_bssfp</tt></a></li><li ><a href="#21">5.b. Generic notes</a></li><li ><a href="#22">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</a></li><li ><a href="#26">5.b.2 Parallelization</a></li><li ><a href="#28">6. Citations</a></li></ul></div><pre class="codeinput"><span class="comment">% This m-file has been automatically generated using qMRgenBatch(qmt_bssfp)</span>
   <span class="comment">% for publishing documentation.</span>
   <span class="comment">% Command Line Interface (CLI) is well-suited for automatization</span>
   <span class="comment">% purposes and Octave.</span>
   <span class="comment">%</span>
   <span class="comment">% Please execute this m-file section by section to get familiar with batch</span>
   <span class="comment">% processing for qmt_bssfp on CLI.</span>
   <span class="comment">%</span>
   <span class="comment">% Demo files are downloaded into qmt_bssfp_data folder.</span>
   <span class="comment">%</span>
   <span class="comment">% Written by: Agah Karakuzu, 2017</span>
   <span class="comment">% ==============================================================================</span>
   </pre><h2 id="2">1. Print <tt >qmt_bssfp</tt> information</h2><pre class="codeinput">qMRinfo(<span class="string">'qmt_bssfp'</span>);
   </pre><pre class="codeoutput">  qmt_bssfp : qMT using Balanced Steady State Free Precession acquisition
    -----------------------------------------------------------------------------------------------------
     Assumptions:
    
     Inputs:
       MTdata        4D Magnetization Transfer data
       (R1map)       1/T1map (OPTIONAL)
       (Mask)        Binary mask to accelerate the fitting (OPTIONAL)
    
     Outputs:
         F         Ratio of number of restricted pool to free pool, defined
                   as F = M0r/M0f = kf/kr.
         kr        Exchange rate from the free to the restricted pool
                   (note that kf and kr are related to one another via the
                   definition of F. Changing the value of kf will change kr
                   accordingly, and vice versa).
         R1f       Longitudinal relaxation rate of the free pool
                   (R1f = 1/T1f).
         R1r       Longitudinal relaxation rate of the restricted pool
                   (R1r = 1/T1r).
         T2f       Tranverse relaxation time of the free pool (T2f = 1/R2f).
         M0f       Equilibrium value of the free pool longitudinal
                   magnetization.
    
       Additional Outputs
         M0r       Equilibrium value of the restricted pool longitudinal
                      magnetization.
         kf        Exchange rate from the restricted to the free pool.
         resnorm   Fitting residual.
    
     Protocol:
       MTdata      Array [nbVols x 2]:
           Alpha   Flip angle of the RF pulses (degrees)
           Trf     Duration of the RF pulses (s)
    
     Options:
       RF Pulse
           Shape           Shape of the RF pulses.
                              Available shapes are:
                              - hard
                              - gaussian
                              - gausshann (gaussian pulse with Hanning window)
                              - sinc
                              - sinchann (sinc pulse with Hanning window)
                              - singauss (sinc pulse with gaussian window)
                              - fermi
           Nb of RF pulses Number of RF pulses applied before readout.
    
       Protocol Timing
           Fix TR          Select this option and enter a value in the text
                             box below to set a fixed repetition time.
           Fix TR - Trf	Select this option and enter a value in the text
                             box below to set a fixed free precession time
                             (TR - Trf).
           Prepulse      Perform an Alpha/2 - TR/2 prepulse before each
                             series of RF pulses.
    
       R1
           Use R1map to      By checking this box, you tell the fitting
             constrain R1f   algorithm to check for an observed R1map and use
                             its value to constrain R1f. Checking this box
                             will automatically set the R1f fix box to true in
                             the Fit parameters table.
           Fix R1r = R1f     By checking this box, you tell the fitting
                             algorithm to fix R1r equal to R1f. Checking this
                             box will automatically set the R1r fix box to
                             true in the Fit parameters table.
    
       Global
           G(0)              The assumed value of the absorption lineshape of
                             the restricted pool.
    
     References:
       Please cite the following if you use this module:
    
       In addition to citing the package:
         Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., 
         Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: 
         Quantitative MRI analysis, under one umbrella doi: 10.21105/joss.02343
   
       Documentation for qmt_bssfp
          doc qmt_bssfp
   
   
   </pre><h2 id="3">2. Setting model parameters</h2><h2 id="4">2.a. Create <tt >qmt_bssfp</tt> object</h2><pre class="codeinput">Model = qmt_bssfp;
   </pre><h2 id="5">2.b. Modify the options</h2><p >This section will pop-up the <tt >options GUI</tt> for demonstration purposes.</p><p ><i >You need to close this window to proceed.</i></p><div ><ul ><li >If you are using Octave, or would like to serialize your operations without <tt >GUI</tt> involvement, you can assign method options directly in CLI.</li></ul></div><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#21">generic notes</a> section below for further details. </p>
   </div>
   </p><pre class="codeinput">Model = Custom_OptionsGUI(Model); <span class="comment">% You need to close GUI to move on.</span>
   </pre><img vspace="5" hspace="5" src="_static/qmt_bssfp_batch_01.png" alt=""> <h2 id="7">3. Fit MRI data</h2><h2 id="8">3.a. Load input data</h2><p >This section shows how you can load data into a(n) <tt >qmt_bssfp</tt> object.</p><div ><ul ><li >At the CLI level, qMRLab accepts structs containing (<tt >double</tt>) data in the fields named in accordance with a qMRLab model.</li></ul></div><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#21">generic notes</a> section below for BIDS compatible wrappers and scalable qMRLab workflows. </p>
   </div>
   </p><pre class="codeinput"><span class="comment">%          |- qmt_bssfp object needs 3 data input(s) to be assigned:</span>
   <span class="comment">%          |-   MTdata</span>
   <span class="comment">%          |-   R1map</span>
   <span class="comment">%          |-   Mask</span>
   
   data = struct();
   <span class="comment">% MTdata.nii.gz contains [128  128    1   16] data.</span>
   data.MTdata=double(load_nii_data(<span class="string">'qmt_bssfp_data/MTdata.nii.gz'</span>));
   <span class="comment">% R1map.nii.gz contains [128  128] data.</span>
   data.R1map=double(load_nii_data(<span class="string">'qmt_bssfp_data/R1map.nii.gz'</span>));
   <span class="comment">% Mask.nii.gz contains [128  128] data.</span>
   data.Mask=double(load_nii_data(<span class="string">'qmt_bssfp_data/Mask.nii.gz'</span>));
   </pre><h2 id="10">3.b. Execute fitting process</h2><p >This section will fit the loaded data.</p><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Visit the <a href="#21">generic notes</a> section below for instructions to accelerate fitting by parallelization using <code >ParFitData</code>. </p>
   </div>
   </p><pre class="language-matlab">FitResults = FitData(data,Model,0);
   </pre><h2 id="13">3.c. Display <tt >FitResults</tt></h2><p >You can display the current outputs by:</p><pre class="language-matlab">qMRshowOutput(FitResults,data,Model);
   </pre><p ><i >A representative fit curve will be plotted if available.</i></p><p >To render images in this page, we will load the fit results that had been saved before. You can skip the following code block;</p><pre class="codeinput"><span class="comment">% Load FitResults that comes with the example dataset.</span>
   FitResults_old = load(<span class="string">'FitResults/FitResults.mat'</span>);
   qMRshowOutput(FitResults_old,data,Model);
   </pre><img vspace="5" hspace="5" src="_static/qmt_bssfp_batch_02.png" alt=""> <img vspace="5" hspace="5" src="_static/qmt_bssfp_batch_03.png" alt=""> <h2 id="14">3.d. Saving fit results</h2><p >Outputs can be saved as <tt >*.nii.(gz)</tt> if <tt >NIfTI</tt> inputs are available:</p><pre class="language-matlab"><span class="comment">% Generic function call to save nifti outputs</span>
   FitResultsSave_nii(FitResults, <span class="string">'reference/nifti/file.nii.(gz)'</span>);
   </pre><p >If not, <tt >FitResults.mat</tt> file can be saved. This file contains all the outputs as workspace variables:</p><pre class="language-matlab"><span class="comment">% Generic function call to save FitResults.mat</span>
   FitResultsSave_mat(FitResults);
   </pre><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >FitResults.mat</code> files can be loaded to qMRLab <code >GUI</code> for <a href="l#data-viewer" target="_blank">visualization and ROI analyses</a>. </p>
   </div>
   </p><p >Model object (<tt >qmt_bssfp_Demo.qmrlab.mat</tt>) stores all the options and protocol.</p><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >*.qmrlab.mat</code> files can be easily shared with collaborators to allow them fit their own data or run simulations using identical <code >option</code> and <code >protocol</code> configurations. </p>
   </div>
   </p><p >The section below will be dynamically generated in accordance with the example data format (<tt >mat</tt> or <tt >nii</tt>). You can substitute <tt >FitResults_old</tt> with <tt >FitResults</tt> if you executed the fitting using example dataset for this model in section <b >3.b.</b>.</p><pre class="codeinput">FitResultsSave_nii(FitResults_old, <span class="string">'qmt_bssfp_data/MTdata.nii.gz'</span>);
   Model.saveObj(<span class="string">'qmt_bssfp_Demo.qmrlab.mat'</span>);
   </pre><pre class="codeoutput">Warning: Directory already exists. 
   </pre><h2 id="16">4. Simulations</h2><h2 id="17">4.a. <tt >Single Voxel Curve</tt></h2><p >Simulates single voxel curves:</p><div ><ol ><li >Analytically generate synthetic MRI data</li><li >Add <i >rician</i> noise</li><li ><tt >Fit</tt> and <tt >plot</tt> the respective curve</li></ol></div><pre class="codeinput">      x = struct;
         x.F = 0.1;
         x.kr = 30;
         x.R1f = 1;
         x.R1r = 1;
         x.T2f = 0.04;
         x.M0f = 1;
         <span class="comment">% Set simulation options</span>
         Opt.SNR = 50;
         Opt.Method = <span class="string">'Analytical equation'</span>;
         Opt.ResetMz = false;
         <span class="comment">% run simulation</span>
         figure(<span class="string">'Name'</span>,<span class="string">'Single Voxel Curve Simulation'</span>);
         FitResult = Model.Sim_Single_Voxel_Curve(x,Opt);
   </pre><img vspace="5" hspace="5" src="_static/qmt_bssfp_batch_04.png" alt=""> <h2 id="18">4.b. <tt >Sensitivity Analysis</tt></h2><p >Simulates sensitivity to fitted parameters:</p><div ><ol ><li >Iterate fitting parameters from lower (<tt >lb</tt>) to upper (<tt >ub</tt>) bound</li><li >Run <tt >Sim_Single_Voxel_Curve</tt> for <tt >Nofruns</tt> times</li><li >Compute the <tt >mean</tt> and <tt >std</tt> across runs</li></ol></div><pre >            F             kr            R1f           R1r           T2f           M0f</pre><pre class="codeinput">      OptTable.st = [0.1           30            1             1             0.04          1]; <span class="comment">% nominal values</span>
         OptTable.fx = [0             1             1             1             1             1]; <span class="comment">%vary F...</span>
         OptTable.lb = [0.0001        0.0001        0.2           0.2           0.01          0.0001]; <span class="comment">%...from 0.0001</span>
         OptTable.ub = [0.3           1e+02         3             3             0.2           2]; <span class="comment">%...to 0.3</span>
         <span class="comment">% Set simulation options</span>
         Opt.SNR = 50;
         Opt.Method = <span class="string">'Analytical equation'</span>;
         Opt.ResetMz = false;
         Opt.Nofrun = 5;
         <span class="comment">% run simulation</span>
         SimResults = Model.Sim_Sensitivity_Analysis(OptTable,Opt);
         figure(<span class="string">'Name'</span>,<span class="string">'Sensitivity Analysis'</span>);
         SimVaryPlot(SimResults, <span class="string">'F'</span> ,<span class="string">'F'</span> );
   </pre><img vspace="5" hspace="5" src="_static/qmt_bssfp_batch_05.png" alt=""> <h2 id="19">5. Notes</h2><h2 id="20">5.a. Notes specific to <tt >qmt_bssfp</tt></h2><p >
   <div class="warning" style="text-align:justify;">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Not provided.</p>
   </div>
   </p><h2 id="21">5.b. Generic notes</h2><h2 id="22">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</h2><p >If you would like to load a desired set of <tt >options</tt>/|protocols| programatically, you can use <tt >*.qmrlab.mat</tt> files. To save a configuration from the <tt >protocol</tt> panel of <tt >qmt_bssfp</tt>, first open the respective panel by running the following command in your MATLAB command window (MATLAB only):</p><pre class="language-matlab">Custom_OptionsGUI(qmt_bssfp);
   </pre><p >In this panel, you can arrange available <tt >options</tt> and <tt >protocols</tt> according to your needs, then click the <tt >save</tt> button to save <tt >my_qmt_bssfp.qmrlab.mat</tt> file. This file can be later loaded into a <tt >qmt_bssfp</tt> object in batch by:</p><pre class="language-matlab">Model = qmt_bssfp;
   Model = Model.loadObj(<span class="string">'my_qmt_bssfp.qmrlab.mat'</span>);
   </pre><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >Model.loadObj('my_qmt_bssfp.qmrlab.mat')</code> call won't update the fields in the <code >Model</code> object, unless the output is assigned to the object as shown above. This compromise on convenience is to retain Octave CLI compatibility. </p>
   </div>
   </p><p ><b >If you don't have MATLAB, hence cannot access the <tt >GUI</tt>, two alternatives are available to populate <tt >options</tt>:</b></p><div ><ol ><li >Use <tt >qmrlab/mcrgui:latest</tt> Docker image to access <tt >GUI</tt>. The instructions are available <a href="https://hub.docker.com/r/qmrlab/mcrgui">here</a>.</li><li >Set <tt >options</tt> and <tt >protocols</tt> in <tt >CLI</tt>:</li></ol></div><div ><ul ><li >List available option fields using tab completion in Octave's command prompt (or window)</li></ul></div><pre class="language-matlab">Model = qmt_bssfp;
   Model.option. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
   </pre><div ><ul ><li >Assign the desired field. <b >For example</b>, for a <tt >mono_t2</tt> object:</li></ul></div><pre class="language-matlab">Model = mono_t2;
   Model.options.DropFirstEcho = true;
   Model.options.OffsetTerm = false;
   </pre><p >
   <div class="info">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Some option fields may be mutually exclusive or interdependent. Such cases are handled  by the <code >GUI</code> options panel; however, not exposed to the <code >CLI</code>. Therefore, manual <code >CLI</code> <code >options</code> assignments may be challenging for some involved methods such as <code >qmt_spgr</code> or <code >qsm_sb</code>. If above options are not working for you and you cannot infer how to set options solely in batch, please feel free to <a href="https://github.com/qmrlab/qmrlab" target="_blank">open an issue in qMRLab</a> and request the protocol file you need. </p>
   </div>
   </p><p ><b >Similarly, in CLI, you can inspect and assign the <tt >protocols</tt>:</b></p><pre class="language-matlab">Model = qmt_bssfp;
   Model.Prot. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
   </pre><p >Each protocol field has two subfields of <tt >Format</tt> and <tt >Mat</tt>. The first one is a <tt >cell</tt> indicating the name of the protocol parameter (such as <tt >EchoTime (ms)</tt>) and the latter one contains the respective values (such as <tt >30 x 1 double</tt> array containing <tt >EchoTimes</tt>).</p><p >
   <div class="warning">
   <p style="margin:0px!important;"> The default <code >Mat</code> protocol values are set according to the example datasets served via <a href="https://osf.io/tmdfu" target="_blank">OSF</a>.</p>
   </div>
   </p><h2 id="26">5.b.2 Parallelization</h2><p >Beginning from release <tt >2.5.0</tt>, you can accelerate fitting for the <tt >voxelwise</tt> models using parallelization.</p><p >
   <div class="danger">
   <p style="margin:0px!important;"> <strong >Available in MATLAB only. Requires <code >parallel processing toolbox</code>.</strong></p>
   </div>
   </p><p >In <tt >CLI</tt>, you can perform parallel fitting by:</p><pre class="language-matlab">parpool();
   FitResults = ParFitData(data,Model);
   </pre><p >If a <tt >parpool</tt> exists, the <tt >ParFitData</tt> will use it. If not, a new pool will be created using the local profile. By default, <tt >ParFitData</tt> saves outputs automatically every 5 minutes. You can disable this feature by:</p><pre class="language-matlab">FitResults = ParFitData(data, Model, <span class="string">'AutosaveEnabled'</span>, false);
   </pre><p >Alternatively, you can change the autosave interval (min 1 min) by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'AutoSaveInterval'</span>,10);
   </pre><p >If something went wrong during the fitting (e.g. your computer had to be restarted), you can recover the autosaved data by:</p><pre class="language-matlab">FitResults = ParFitData(data,Model,<span class="string">'RecoverDirectory'</span>,<span class="string">'/ParFitTempResults_*/folder/from/the/previous/session'</span>);
   </pre><p ><tt >GUI</tt> users will be prompted a question about whether they would like to use parallelization after clicking the <tt >Fit Data</tt> button, if the conditions are met. When called from <tt >GUI</tt>, <tt >ParFitData</tt> will be run with default options:</p><div ><ul ><li >Save temporary results every <tt >5</tt> minutes or whenever a chunk has finished processing</li><li >Split data into chunks with a <tt >granularity</tt> factor of <tt >3</tt></li><li >Do not remove temporary fit results upon completion</li></ul></div><p >For further information:</p><pre class="language-matlab">help <span class="string">ParFitData</span>
   </pre><p >The default <tt >parallelization</tt> options can be changed in the <tt >preferences.json</tt> file located at the root qMRLab directory.</p><h2 id="28">6. Citations</h2><p ><b >qMRLab JOSS article</b></p><p >
   <div class="success" style="text-align:justify;">
   <p > Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: Quantitative MRI analysis, under one umbrella <a href="https://doi.org/10.21105/joss.02343" target="_blank">10.21105/joss.02343</a></p>
   </div>
   </p><p ><b >Reference article for <tt >qmt_bssfp</tt></b></p><p >
   <div class="success" style="text-align:justify;">
   _Reference article is not defined for this model._
   </div>
   </p><p >
   <hr >
   <center ><i class="fa fa-umbrella" style="color:black;font-size:2em;"></i></center>
   <center ><p >Quantitative MRI, under one umbrella.</p></center>
   <center >| <a href="https://github.com/qmrlab/pulse_sequences" target="_blank">qMRPullseq</a> | <a href="https://github.com/qmrlab/qmrflow" target="_blank">qMRFlow</a> | <a href="https://qmrlab.org/blog.html" target="_blank">Interactive Tutorials</a> | </p></center>
   <center ><p ><a href="https://www.neuro.polymtl.ca/doku.php" target="_blank">NeuroPoly Lab</a>, Montreal, Canada</p></center>
   <hr >
   </p><p class="footer"><br ><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB® R2019b</a><br ></p></div>
