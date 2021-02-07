noddi:   Neurite Orientation Dispersion and Density Imaging
===========================================================

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
   </style><div class="content"><h2 >Contents</h2><div ><ul ><li ><a href="#2">1. Print <tt >noddi</tt> information</a></li><li ><a href="#3">2. Setting model parameters</a></li><li ><a href="#4">2.a. Create <tt >noddi</tt> object</a></li><li ><a href="#5">2.b. Modify the options</a></li><li ><a href="#7">3. Fit MRI data</a></li><li ><a href="#8">3.a. Load input data</a></li><li ><a href="#10">3.b. Execute fitting process</a></li><li ><a href="#13">3.c. Display <tt >FitResults</tt></a></li><li ><a href="#14">3.d. Saving fit results</a></li><li ><a href="#16">4. Simulations</a></li><li ><a href="#17">4.a. <tt >Single Voxel Curve</tt></a></li><li ><a href="#18">4.b. <tt >Sensitivity Analysis</tt></a></li><li ><a href="#19">5. Notes</a></li><li ><a href="#20">5.1. Notes specific to <tt >noddi</tt></a></li><li ><a href="#21">5.2. Generic notes</a></li><li ><a href="#22">6. Citations</a></li></ul></div><pre class="codeinput"><span class="comment">% This m-file has been automatically generated using qMRgenBatch(noddi)</span>
   <span class="comment">% for publishing documentation.</span>
   <span class="comment">% Command Line Interface (CLI) is well-suited for automatization</span>
   <span class="comment">% purposes and Octave.</span>
   <span class="comment">%</span>
   <span class="comment">% Please execute this m-file section by section to get familiar with batch</span>
   <span class="comment">% processing for noddi on CLI.</span>
   <span class="comment">%</span>
   <span class="comment">% Demo files are downloaded into noddi_data folder.</span>
   <span class="comment">%</span>
   <span class="comment">% Written by: Agah Karakuzu, 2017</span>
   <span class="comment">% ==============================================================================</span>
   </pre><h2 id="2">1. Print <tt >noddi</tt> information</h2><pre class="codeinput">qMRinfo(<span class="string">'noddi'</span>);
   </pre><pre class="codeoutput">  noddi:   Neurite Orientation Dispersion and Density Imaging
              Three-compartment model for fitting multi-shell DWI
    a href="matlab: figure, imshow Diffusion.png ;"Pulse Sequence Diagram/a
    
     ASSUMPTIONS:
       Neuronal fibers model:
         geometry                          sticks (Dperp = 0)
         Orientation dispersion            YES (Watson distribution). Note that NODDI is more robust to
                                                                       crossing fibers that DTI  (Campbell, NIMG 2017)
    
         Permeability                      NO
       Diffusion properties:
         intra-axonal                      totally restricted
           diffusion coefficient (Dr)      fixed by default.
         extra-axonal                      Tortuosity model. Parallel diffusivity is equal to
                                             intra-diffusivity.Perpendicular diffusivity is
                                             proportional to fiber density
           diffusion coefficient (Dh)      Constant
    
     Inputs:
       DiffusionData        4D diffusion weighted dataset
       (Mask)               Binary mask to accelerate the fitting (OPTIONAL)
    
     Outputs:
       di                  Diffusion coefficient in the restricted compartment.
       ficvf               Fraction of water in the restricted compartment.
       fiso                Fraction of water in the isotropic compartment (e.g. CSF/Veins)
       fr                  Fraction of restricted water in the entire voxel (e.g. intra-cellular volume fraction)
                            fr = ficvf*(1-fiso)
       diso (fixed)        diffusion coefficient of the isotropic compartment (CSF)
       kappa               Orientation dispersion index
       b0                  Signal at b=0
       theta               angle of the fibers
       phi                 angle of the fibers
    
     Protocol:
       Multi-shell diffusion-weighted acquisition
        at least 2 non-zeros bvalues
        at least 5 b=0 (used to compute noise standard deviation
    
       DiffusionData       Array [NbVol x 7]
         Gx                Diffusion Gradient x
         Gy                Diffusion Gradient y
         Gz                Diffusion Gradient z
         Gnorm (T/m)         Diffusion gradient magnitude
         Delta (s)         Diffusion separation
         delta (s)         Diffusion duration
         TE (s)            Echo time
    
     Options:
       Model               Model part of NODDI.
                             Available models are:
                               -WatsonSHStickTortIsoVIsoDot_B0 is a four model compartment used for ex-vivo datasets
    
     Example of command line usage
       For more examples: a href="matlab: qMRusage(noddi);"qMRusage(noddi)/a
    
     Author: Tanguy Duval
    
     References:
       Please cite the following if you use this module:
         Zhang, H., Schneider, T., Wheeler-Kingshott, C.A., Alexander, D.C., 2012. NODDI: practical in vivo neurite orientation dispersion and density imaging of the human brain. Neuroimage 61, 1000?1016.
       In addition to citing the package:
         Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., 
         Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: 
         Quantitative MRI analysis, under one umbrella doi: 10.21105/joss.02343
   
       Documentation for noddi
          doc noddi
   
   
   </pre><h2 id="3">2. Setting model parameters</h2><h2 id="4">2.a. Create <tt >noddi</tt> object</h2><pre class="codeinput">Model = noddi;
   </pre><h2 id="5">2.b. Modify the options</h2><p >This section will pop-up the <tt >options</tt> GUI for demonstration purposes.</p><p ><i >You need to close this window to proceed.</i></p><div ><ul ><li >If you are using Octave, or would like to serialize your operations without GUI involvement, you can assign method options directly in CLI.</li></ul></div><p >
   <div class="info">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#17">generic notes</a> section below for further details. </p>
   </div>
   </p><pre class="codeinput">Model = Custom_OptionsGUI(Model); <span class="comment">% You need to close GUI to move on.</span>
   </pre><img src="_static/noddi_batch_01.png" vspace="5" hspace="5" alt=""> <h2 id="7">3. Fit MRI data</h2><h2 id="8">3.a. Load input data</h2><p >This section shows how you can load data into a(n) <tt >noddi</tt> object.</p><div ><ul ><li >At the CLI level, qMRLab accepts structs containing (<tt >double</tt>) data in the fields named in accordance with a qMRLab model.</li></ul></div><p >
   <div class="info">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> See the <a href="#17">generic notes</a> section below for BIDS compatible wrappers and scalable qMRLab workflows. </p>
   </div>
   </p><pre class="codeinput"><span class="comment">%          |- noddi object needs 2 data input(s) to be assigned:</span>
   <span class="comment">%          |-   DiffusionData</span>
   <span class="comment">%          |-   Mask</span>
   
   data = struct();
   <span class="comment">% DiffusionData.nii.gz contains [74   87   50  109] data.</span>
   data.DiffusionData=double(load_nii_data(<span class="string">'noddi_data/DiffusionData.nii.gz'</span>));
   <span class="comment">% Mask.nii.gz contains [74  87  50] data.</span>
   data.Mask=double(load_nii_data(<span class="string">'noddi_data/Mask.nii.gz'</span>));
   </pre><h2 id="10">3.b. Execute fitting process</h2><p >This section will fit the loaded data.</p><p >
   <div class="info">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> Visit the <a href="#17">generic notes</a> section below for instructions to accelerate fitting by parallelization using <code >ParFitData</code>. </p>
   </div>
   </p><pre class="language-matlab">FitResults = FitData(data,Model,0);
   </pre><h2 id="13">3.c. Display <tt >FitResults</tt></h2><p >You can display the current outputs by:</p><pre class="language-matlab">qMRshowOutput(FitResults,data,Model);
   </pre><p ><i >A representative fit curve will be plotted if available.</i></p><p >To render images in this page, we will load the fit results that had been saved before. You can skip the following code block;</p><pre class="codeinput"><span class="comment">% Load FitResults that comes with the example dataset.</span>
   FitResults_old = load(<span class="string">'FitResults/FitResults.mat'</span>);
   qMRshowOutput(FitResults_old,data,Model);
   </pre><img src="_static/noddi_batch_02.png" vspace="5" hspace="5" alt=""> <img src="_static/noddi_batch_03.png" vspace="5" hspace="5" alt=""> <h2 id="14">3.d. Saving fit results</h2><p >Outputs can be saved as <tt >*.nii.(gz)</tt> if <tt >NIfTI</tt> inputs are available:</p><pre class="language-matlab"><span class="comment">% Generic function call to save nifti outputs</span>
   FitResultsSave_nii(FitResults, <span class="string">'reference/nifti/file.nii.(gz)'</span>);
   </pre><p >If not, <tt >FitResults.mat</tt> file can be saved. This file contains all the outputs as workspace variables:</p><pre class="language-matlab"><span class="comment">% Generic function call to save FitResults.mat</span>
   FitResultsSave_mat(FitResults);
   </pre><p >
   <div class="info">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >FitResults.mat</code> files can be loaded to qMRLab GUI for <a href="l#data-viewer" target="_blank">visualization and ROI analyses</a>. </p>
   </div>
   </p><p >Model object (<tt >noddi_Demo.qmrlab.mat</tt>) stores all the options and protocol.</p><p >
   <div class="info">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:navy;margin-left:5px;"></i></strong> <code >*.qmrlab.mat</code> files can be easily shared with collaborators to allow them fit their own data or run simulations using identical <code >option</code> and <code >protocol</code> configurations. </p>
   </div>
   </p><p >The section below will be dynamically generated in accordance with the example data format (<tt >mat</tt> or <tt >nii</tt>). You can substitute <tt >FitResults_old</tt> with <tt >FitResults</tt> if you executed the fitting using example dataset for this model in section <b >3.b.</b>.</p><pre class="codeinput">FitResultsSave_nii(FitResults_old, <span class="string">'noddi_data/DiffusionData.nii.gz'</span>);
   Model.saveObj(<span class="string">'noddi_Demo.qmrlab.mat'</span>);
   </pre><pre class="codeoutput">Warning: Directory already exists. 
   </pre><h2 id="16">4. Simulations</h2><h2 id="17">4.a. <tt >Single Voxel Curve</tt></h2><p >Simulates single voxel curves:</p><div ><ol ><li >Analytically generate synthetic MRI data</li><li >Add <i >rician</i> noise</li><li ><tt >Fit</tt> and <tt >plot</tt> the respective curve</li></ol></div><pre class="codeinput">      x = struct;
         x.ficvf = 0.5;
         x.di = 1.7;
         x.kappa = 0.05;
         x.fiso = 0;
         x.diso = 3;
         x.b0 = 1;
         x.theta = 0.2;
         x.phi = 0;
          Opt.SNR = 50;
         <span class="comment">% run simulation</span>
         figure(<span class="string">'Name'</span>,<span class="string">'Single Voxel Curve Simulation'</span>);
         FitResult = Model.Sim_Single_Voxel_Curve(x,Opt);
   </pre><img src="_static/noddi_batch_04.png" vspace="5" hspace="5" alt=""> <h2 id="18">4.b. <tt >Sensitivity Analysis</tt></h2><p >Simulates sensitivity to fitted parameters:</p><div ><ol ><li >Iterate fitting parameters from lower (<tt >lb</tt>) to upper (<tt >ub</tt>) bound</li><li >Run <tt >Sim_Single_Voxel_Curve</tt> for <tt >Nofruns</tt> times</li><li >Compute the <tt >mean</tt> and <tt >std</tt> across runs</li></ol></div><pre >            ficvf         di            kappa         fiso          diso          b0            theta         phi</pre><pre class="codeinput">      OptTable.st = [0.5           1.7           0.05          0             3             1             0.2           0]; <span class="comment">% nominal values</span>
         OptTable.fx = [0             1             1             1             1             1             1             1]; <span class="comment">%vary ficvf...</span>
         OptTable.lb = [0             1.3           0.05          0             1             0             0             0]; <span class="comment">%...from 0</span>
         OptTable.ub = [1             2.1           0.8           1             5             1e+03         3.1           3.1]; <span class="comment">%...to 1</span>
          Opt.SNR = 50;
          Opt.Nofrun = 5;
         <span class="comment">% run simulation</span>
         SimResults = Model.Sim_Sensitivity_Analysis(OptTable,Opt);
         figure(<span class="string">'Name'</span>,<span class="string">'Sensitivity Analysis'</span>);
         SimVaryPlot(SimResults, <span class="string">'ficvf'</span> ,<span class="string">'ficvf'</span> );
   </pre><img src="_static/noddi_batch_05.png" vspace="5" hspace="5" alt=""> <h2 id="19">5. Notes</h2><h2 id="20">5.1. Notes specific to <tt >noddi</tt></h2><p >
   <div class="warning" style="text-align:justify;">
   <p style="margin:0px!important;"><strong ><i class="fa fa-info-circle" style="color:black;margin-left:5px;"></i></strong> Not provided.</p>
   </div>
   </p><h2 id="21">5.2. Generic notes</h2><p >To be edited</p><h2 id="22">6. Citations</h2><p ><b >qMRLab JOSS article</b></p><p >
   <div class="success" style="text-align:justify;">
   <p > Karakuzu A., Boudreau M., Duval T.,Boshkovski T., Leppert I.R., Cabana J.F., Gagnon I., Beliveau P., Pike G.B., Cohen-Adad J., Stikov N. (2020), qMRLab: Quantitative MRI analysis, under one umbrella <a href="https://doi.org/10.21105/joss.02343" target="_blank">10.21105/joss.02343</a></p>
   </div>
   </p><p ><b >Reference article for <tt >noddi</tt></b></p><p >
   <div class="success" style="text-align:justify;">
   <p >|noddi|</p>
   </div>
   </p><p >
   <hr >
   <center ><i class="fa fa-umbrella" style="color:black;font-size:2em;"></i></center>
   <center ><p >Quantitative MRI, under one umbrella.</p></center>
   <center >| <a href="https://github.com/qmrlab/pulse_sequences" target="_blank">qMRPullseq</a> | <a href="https://github.com/qmrlab/qmrflow" target="_blank">qMRFlow</a> | <a href="https://qmrlab.org/blog.html" target="_blank">Interactive Tutorials</a> | </p></center>
   <center ><p ><a href="https://www.neuro.polymtl.ca/doku.php" target="_blank">NeuroPoly Lab</a>, Montreal, Canada</p></center>
   <hr >
   </p><p class="footer"><br ><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB R2019b</a><br ></p></div>