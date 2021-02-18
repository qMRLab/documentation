qsm_sb: Fast quantitative susceptibility mapping
================================================

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
   </style><div class="content"><h2 >Contents</h2><div ><ul ><li ><a href="#2">1. Print <tt >qsm_sb</tt> information</a></li><li ><a href="#3">2. Setting model parameters</a></li><li ><a href="#4">2.a. Create <tt >qsm_sb</tt> object</a></li><li ><a href="#5">2.b. Modify the options</a></li><li ><a href="#7">3. Fit MRI data</a></li><li ><a href="#8">3.a. Load input data</a></li><li ><a href="#10">3.b. Execute fitting process</a></li><li ><a href="#13">3.c. Display <tt >FitResults</tt></a></li><li ><a href="#14">3.d. Saving fit results</a></li><li ><a href="#16">4. Simulations</a></li><li ><a href="#17">4.a. <tt >Single Voxel Curve</tt></a></li><li ><a href="#18">4.b. <tt >Sensitivity Analysis</tt></a></li><li ><a href="#19">5. Notes</a></li><li ><a href="#20">5.a. Notes specific to <tt >qsm_sb</tt></a></li><li ><a href="#21">5.b. Generic notes</a></li><li ><a href="#22">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</a></li><li ><a href="#26">5.b.2 Parallelization:</a></li><li ><a href="#28">6. Citations</a></li></ul></div><pre class="codeinput"><span class="comment">% This m-file has been automatically generated using qMRgenBatch(qsm_sb)</span>
   <span class="comment">% for publishing documentation.</span>
   <span class="comment">% Command Line Interface (CLI) is well-suited for automatization</span>
   <span class="comment">% purposes and Octave.</span>
   <span class="comment">%</span>
   <span class="comment">% Please execute this m-file section by section to get familiar with batch</span>
   <span class="comment">% processing for qsm_sb on CLI.</span>
   <span class="comment">%</span>
   <span class="comment">% Demo files are downloaded into qsm_sb_data folder.</span>
   <span class="comment">%</span>
   <span class="comment">% Written by: Agah Karakuzu, 2017</span>
   <span class="comment">% ==============================================================================</span>
   </pre><h2 id="2">1. Print <tt >qsm_sb</tt> information</h2><pre class="codeinput">qMRinfo(<span class="string">'qsm_sb'</span>);
   </pre><pre class="codeoutput">  qsm_sb: Fast quantitative susceptibility mapping
    
     Assumptions:
     Type/number of outputs will depend on the selected options. 
     (1) Case - Split-Bregman:
           i)  W/ magnitude weighting:  chiSBM, chiL2M, chiL2, unwrappedPhase, maskOut
           ii) W/O magnitude weighting: chiSM, chiL2, unwrappedPhase, maskOut
     (2) Case - L2 Regularization:
           i)  W/ magnitude weighting:  chiL2M, chiL2, unwrappedPhase, maskOut
           ii) W/O magnitude weighting: chiL2, unwrappedPhase, maskOut
     (3) Case - No Regularization: 
           i) Magnitude weighting is not enabled: nfm, unwrappedPhase, maskOut
     Inputs:
       PhaseGRE      3D GRE acquisition. <<Wrapped phase image>>
       (MagnGRE)     3D GRE acquisition. <<Magnitude part of the image>> (OPTIONAL)
       Mask          Brain extraction mask.
    
     Outputs:
       chiSBM          Susceptibility map created using Split-Bregman method with magnitude weighting 
       chiSB           Susceptibility map created using Split-Bregman method without magnitude weighting.
       chiL2M          Susceptibility map created using L2 regularization with magnitude weighting
       chiL2           Susceptibility map created using L2 regularization without magnitude weighting
       nfm             Susceptibility map created without regularization
       unwrappedPhase  Unwrapped phase image using Laplacian-based method
       maskOut         Binary mask (maskSharp, gradientMask or same as the input)
    
     Options:
       Derivative direction               Direction of the derivation 
                                            - forward 
                                            - backward
       SHARP Filtering                    Sophisticated harmonic artifact reduction for phase data
                                            - State: true/false
                                            - Mode: once/iterative 
                                            - Padding Size: [1X3 array]
                                            - Magnitude Weighting: on/off
       L1-Regularization                  Apply L1-regularization 
                                            - State: true/false
                                            - Reoptimize parameters:
                                            true/false
                                            - Lambda-L1: [double]
                                            - L1-Range:  [1X2 array]
       L2-Regularization                  Apply L2-regularization 
                                            - State: true/false
                                            - Reoptimize parameters:
                                            true/false
                                            - Lambda-L2: [double]
                                            - L2-Range:  [1X2 array]
       Split-Bregman                       Apply Split-Bregman method 
                                            - State: true/false
                                            - Reoptimize parameters:
    
     Authors: Agah Karakuzu, 2018
    
     References:
       Please cite the following if you use this module:
         Bilgic et al. (2014), Fast quantitative susceptibility mapping with
         L1-regularization and automatic parameter selection. Magn. Reson. Med.,
         72: 1444-1459. doi:10.1002/mrm.25029
       In addition to citing the package:
         Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., 
         Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: 
         Quantitative MRI analysis, under one umbrella doi: 10.21105/joss.02343
   
       Documentation for qsm_sb
          doc qsm_sb
   
   
   </pre><h2 id="3">2. Setting model parameters</h2><h2 id="4">2.a. Create <tt >qsm_sb</tt> object</h2><pre class="codeinput">Model = qsm_sb;
   </pre><h2 id="5">2.b. Modify the options</h2><p >This section will pop-up the <tt >options GUI</tt> for demonstration purposes.</p><p ><i >You need to close this window to proceed.</i></p><div ><ul ><li >If you are using Octave, or would like to serialize your operations without <tt >GUI</tt> involvement, you can assign method options directly in CLI.</li></ul></div><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#21">generic notes</a> section below for further details. </p>
   </div>
   </p><pre class="codeinput">Model = Custom_OptionsGUI(Model); <span class="comment">% You need to close GUI to move on.</span>
   </pre><img vspace="5" hspace="5" src="_static/qsm_sb_batch_01.png" alt=""> <h2 id="7">3. Fit MRI data</h2><h2 id="8">3.a. Load input data</h2><p >This section shows how you can load data into a(n) <tt >qsm_sb</tt> object.</p><div ><ul ><li >At the CLI level, qMRLab accepts structs containing (<tt >double</tt>) data in the fields named in accordance with a qMRLab model.</li></ul></div><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#21">generic notes</a> section below for BIDS compatible wrappers and scalable qMRLab workflows. </p>
   </div>
   </p><pre class="codeinput"><span class="comment">%          |- qsm_sb object needs 3 data input(s) to be assigned:</span>
   <span class="comment">%          |-   PhaseGRE</span>
   <span class="comment">%          |-   MagnGRE</span>
   <span class="comment">%          |-   Mask</span>
   
   data = struct();
   
   <span class="comment">% PhaseGRE.mat contains [40  40  40] data.</span>
    load(<span class="string">'qsm_sb_data/PhaseGRE.mat'</span>);
   <span class="comment">% MagnGRE.mat contains [40  40  40] data.</span>
    load(<span class="string">'qsm_sb_data/MagnGRE.mat'</span>);
   <span class="comment">% Mask.mat contains [40  40  40] data.</span>
    load(<span class="string">'qsm_sb_data/Mask.mat'</span>);
    data.PhaseGRE= double(PhaseGRE);
    data.MagnGRE= double(MagnGRE);
    data.Mask= double(Mask);
   </pre><h2 id="10">3.b. Execute fitting process</h2><p >This section will fit the loaded data.</p><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Visit the <a href="#21">generic notes</a> section below for instructions to accelerate fitting by parallelization using <code >ParFitData</code>. </p>
   </div>
   </p><pre class="language-matlab">FitResults = FitData(data,Model,0);
   </pre><h2 id="13">3.c. Display <tt >FitResults</tt></h2><p >You can display the current outputs by:</p><pre class="language-matlab">qMRshowOutput(FitResults,data,Model);
   </pre><p ><i >A representative fit curve will be plotted if available.</i></p><p >To render images in this page, we will load the fit results that had been saved before. You can skip the following code block;</p><pre class="codeinput"><span class="comment">% Load FitResults that comes with the example dataset.</span>
   FitResults_old = load(<span class="string">'FitResults/FitResults.mat'</span>);
   qMRshowOutput(FitResults_old,data,Model);
   </pre><img vspace="5" hspace="5" src="_static/qsm_sb_batch_02.png" alt=""> <h2 id="14">3.d. Saving fit results</h2><p >Outputs can be saved as <tt >*.nii.(gz)</tt> if <tt >NIfTI</tt> inputs are available:</p><pre class="language-matlab"><span class="comment">% Generic function call to save nifti outputs</span>
   FitResultsSave_nii(FitResults, <span class="string">'reference/nifti/file.nii.(gz)'</span>);
   </pre><p >If not, <tt >FitResults.mat</tt> file can be saved. This file contains all the outputs as workspace variables:</p><pre class="language-matlab"><span class="comment">% Generic function call to save FitResults.mat</span>
   FitResultsSave_mat(FitResults);
   </pre><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >FitResults.mat</code> files can be loaded to qMRLab <code >GUI</code> for <a href="l#data-viewer" target="_blank">visualization and ROI analyses</a>. </p>
   </div>
   </p><p >Model object (<tt >qsm_sb_Demo.qmrlab.mat</tt>) stores all the options and protocol.</p><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >*.qmrlab.mat</code> files can be easily shared with collaborators to allow them fit their own data or run simulations using identical <code >option</code> and <code >protocol</code> configurations. </p>
   </div>
   </p><p >The section below will be dynamically generated in accordance with the example data format (<tt >mat</tt> or <tt >nii</tt>). You can substitute <tt >FitResults_old</tt> with <tt >FitResults</tt> if you executed the fitting using example dataset for this model in section <b >3.b.</b>.</p><pre class="codeinput">FitResultsSave_mat(FitResults_old);
   Model.saveObj(<span class="string">'qsm_sb_Demo.qmrlab.mat'</span>);
   </pre><pre class="codeoutput">Warning: Directory already exists. 
   </pre><h2 id="16">4. Simulations</h2><h2 id="17">4.a. <tt >Single Voxel Curve</tt></h2><p >Simulates single voxel curves:</p><div ><ol ><li >Analytically generate synthetic MRI data</li><li >Add <i >rician</i> noise</li><li ><tt >Fit</tt> and <tt >plot</tt> the respective curve</li></ol></div><p >
   <div class="danger" style="text-align:justify;">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:red;margin-left:5px;"></i></strong> Not available for the current model.</p>
   </div>
   </p><h2 id="18">4.b. <tt >Sensitivity Analysis</tt></h2><p >Simulates sensitivity to fitted parameters:</p><div ><ol ><li >Iterate fitting parameters from lower (<tt >lb</tt>) to upper (<tt >ub</tt>) bound</li><li >Run <tt >Sim_Single_Voxel_Curve</tt> for <tt >Nofruns</tt> times</li><li >Compute the <tt >mean</tt> and <tt >std</tt> across runs</li></ol></div><p >
   <div class="danger" style="text-align:justify;">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:red;margin-left:5px;"></i></strong> Not available for the current model.</p>
   </div>
   </p><h2 id="19">5. Notes</h2><h2 id="20">5.a. Notes specific to <tt >qsm_sb</tt></h2><p ><b >Note 1:</b></p><p >To make documentation generation and our CI tests faster for this model, we used a subportion of the data <tt >40x40x40</tt> in our testing environment.</p><p >Therefore , the dimensions displayed in the section <i >3.a</i> of this automatically generated documentation is different than those provided to the user.</p><pre class="language-matlab">qMRgenBatch(qsm_sb)
   </pre><p >When the command above is called from MATLAB/Octave by the user, the complete high resolution (<tt >0.6mm iso</tt> resolution) dataset (<tt >384x336x224</tt> dimensions) will be downloaded.</p><p ><b >Note 2:</b></p><div ><ul ><li ><tt >L1 regularization</tt> is performed as a sub-process to <tt >Split-Bregman</tt> regularization. Therefore, L1 (lambda) reoptimization panel is enabled only when <tt >Split-Bregman</tt> is activated. The <tt >Chimap</tt> (inn ppm) calculated upon this selection are <tt >chiSB</tt> and <tt >chiL2</tt>.</li><li >Unlike <tt >L1</tt>, <tt >L2 regularization</tt> can be run independently. The <tt >Chimap</tt> (in ppm) calculated upon this selection is <tt >chiL2</tt>.</li><li >When the <tt >magnitude weighting</tt> optio`n is enbled, associated the output maps attains an <tt >M</tt> suffix: <tt >chiL2M</tt> or <tt >chiSBM</tt>.</li><li >A susceptibility map can be also generated without regularization. For this selection, the output <tt >Chimap</tt> is <tt >nfm</tt>, which is displayed as an example in this page.</li><li >Unwrapped phase images are provided in the output: <tt >unwrappedPhase</tt>.</li></ul></div><h2 id="21">5.b. Generic notes</h2><h2 id="22">5.b.1. Batch friendly <tt >option</tt> and <tt >protocol</tt> conventions</h2><p >If you would like to load a desired set of <tt >options</tt>/|protocols| programatically, you can use <tt >*.qmrlab.mat</tt> files. To save a configuration from the <tt >protocol</tt> panel of <tt >qsm_sb</tt>, first open the respective panel by running the following command in your MATLAB command window (MATLAB only):</p><pre class="language-matlab">Custom_OptionsGUI(qsm_sb);
   </pre><p >In this panel, you can arrange available <tt >options</tt> and <tt >protocols</tt> according to your needs, then click the <tt >save</tt> button to save <tt >my_qsm_sb.qmrlab.mat</tt> file. This file can be later loaded into a <tt >qsm_sb</tt> object in batch by:</p><pre class="language-matlab">Model = qsm_sb;
   Model = Model.loadObj(<span class="string">'my_qsm_sb.qmrlab.mat'</span>);
   </pre><p >
   <div class="info">
   <p style="margin:0px!important;"><strong > <i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >Model.loadObj('my_qsm_sb.qmrlab.mat')</code> call won't update the fields in the <code >Model</code> object, unless the output is assigned to the object as shown above. This compromise on convenience is to retain Octave CLI compatibility. </p>
   </div>
   </p><p ><b >If you don't have MATLAB, hence cannot access the <tt >GUI</tt>, two alternatives are available to populate <tt >options</tt>:</b></p><div ><ol ><li >Use <tt >qmrlab/mcrgui:latest</tt> Docker image to access <tt >GUI</tt>. The instructions are available <a href="https://hub.docker.com/r/qmrlab/mcrgui">here</a>.</li><li >Set <tt >options</tt> and <tt >protocols</tt> in <tt >CLI</tt>:</li></ol></div><div ><ul ><li >List available option fields using tab completion in Octave's command prompt (or window)</li></ul></div><pre class="language-matlab">Model = qsm_sb;
   Model.option. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
   </pre><div ><ul ><li >Assign the desired field. <b >For example</b>, for a <tt >mono_t2</tt> object:</li></ul></div><pre class="language-matlab">Model = mono_t2;
   Model.options.DropFirstEcho = true;
   Model.options.OffsetTerm = false;
   </pre><p >
   <div class="info">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Some option fields may be mutually exclusive or interdependent. Such cases are handled  by the <code >GUI</code> options panel; however, not exposed to the <code >CLI</code>. Therefore, manual <code >CLI</code> <code >options</code> assignments may be challenging for some involved methods such as <code >qmt_spgr</code> or <code >qsm_sb</code>. If above options are not working for you and you cannot infer how to set options solely in batch, please feel free to <a href="https://github.com/qmrlab/qmrlab" target="_blank">open an issue in qMRLab</a> and request the protocol file you need. </p>
   </div>
   </p><p ><b >Similarly, in CLI, you can inspect and assign the <tt >protocols</tt>:</b></p><pre class="language-matlab">Model = qsm_sb;
   Model.Prot. <span class="comment">% click the tab button on your keyboard and list the available fields.</span>
   </pre><p >Each protocol field has two subfields of <tt >Format</tt> and <tt >Mat</tt>. The first one is a <tt >cell</tt> indicating the name of the protocol parameter (such as <tt >EchoTime (ms)</tt>) and the latter one contains the respective values (such as <tt >30 x 1 double</tt> array containing <tt >EchoTimes</tt>).</p><p >
   <div class="warning">
   <p style="margin:0px!important;"> The default <code >Mat</code> protocol values are set according to the example datasets served via <a href="https://osf.io/tmdfu" target="_blank">OSF</a>.</p>
   </div>
   </p><h2 id="26">5.b.2 Parallelization:</h2><p >
   <div class="danger">
   <p style="margin:0px!important;"> The current model does not perform voxelwise fitting. Therefore, parallelization is not enabled.</p>
   </div>
   </p><h2 id="28">6. Citations</h2><p ><b >qMRLab JOSS article</b></p><p >
   <div class="success" style="text-align:justify;">
   <p > Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: Quantitative MRI analysis, under one umbrella <a href="https://doi.org/10.21105/joss.02343" target="_blank">10.21105/joss.02343</a></p>
   </div>
   </p><p ><b >Reference article for <tt >qsm_sb</tt></b></p><p >
   <div class="success" style="text-align:justify;">
   Bilgic, B., et al. (2014). Fast quantitative susceptibility mapping with L1-regularization and automatic parameter selection. Magnetic Resonance in Medicine, 72(5), 1444-1459. 10.1002/mrm.25029
   </div>
   </p><p >
   <hr >
   <center ><i class="fa fa-umbrella" style="color:black;font-size:2em;"></i></center>
   <center ><p >Quantitative MRI, under one umbrella.</p></center>
   <center >| <a href="https://github.com/qmrlab/pulse_sequences" target="_blank">qMRPullseq</a> | <a href="https://github.com/qmrlab/qmrflow" target="_blank">qMRFlow</a> | <a href="https://qmrlab.org/blog.html" target="_blank">Interactive Tutorials</a> | </p></center>
   <center ><p ><a href="https://www.neuro.polymtl.ca/doku.php" target="_blank">NeuroPoly Lab</a>, Montreal, Canada</p></center>
   <hr >
   </p><p class="footer"><br ><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB® R2019b</a><br ></p></div>
