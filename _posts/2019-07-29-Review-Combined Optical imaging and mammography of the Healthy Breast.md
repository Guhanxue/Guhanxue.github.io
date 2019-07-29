

# Paper Review

## 1.Combined Optical Imaging and Mammography of the Healthy Breast: Optical Contrast Derived From Breast Structure and Compression

IEEE Trans Med Imaging. 2009 January ; 28(1): 30–42. doi:10.1109/TMI.2008.925082

key words: Breast imaging; multimodality imaging; tomography

### Abstract 

1. the instrument and software platform of a combined X-ray mammography/diffuse optical breast imaging system
2. focus on system validation 
3. finite-element method for forward modeling and **regularized Gauss-Newton method** for parameter reconstruction
4. enhanced coupling coefficient estimation scheme ->improve accuracy and robustness
5. recovered average total HbT and $SO_2 $  :16.2um and 71%. HbT present a linear trend with breast density. Low HbT value may due to mammographic compression

### Advancements

1. a combined X-ray and optical breast imaging system
2. The blood-pressure coupling effect

### Methods

A block diagram of the tomographic optical imaging system(TOBI)

RF modulated imaging system and the CW system

![1563503336102](C:\Users\ghx\AppData\Roaming\Typora\typora-user-images\1563503336102.png)

TOBI  optical probes (provide the capability of co-registration with 2-D mammography or tomosynthesis)

##### Two protocols

###### similarity:

a solid calibration phantom measurement is required

repeated measurements

###### difference:

temporal duration between the initial breast compression and the optical data acquisition

duration in protocol 2 is roughly 1 or 2 min longer than in protocol 1

expect more hemodynamic change during the measurement period in protocol 1 than in protocol 2. **(why?)**

##### Data Analysis procedure



![1563505644412](../AppData/Roaming/Typora/typora-user-images/1563505644412.png)

image reconstruction steps:

1. estimate the bulk optical properties of the patient's breast and the mean source/detector coupling coefficients
2.  perform a full image reconstruction starting with the homogeneous initial guess from the output of the previous step

##### image reconstruction algorithm

iterative Gauss-Newton reconstruction approach

###### Forward Model

diffusion equation
$$
-\bigtriangledown \cdot D(r) \bigtriangledown \Phi(r,t)+\mu_a(r)\Phi(r,t)+\frac{1}{c}\frac{\partial\Phi(r,t)}{\partial t}=S_0(r,t)
$$
$\mu_a$ :absorption coefficient

$D(r)=\frac{1}{3}(\mu^{’}_a(r)+\mu_s(r)) \approx \frac{1}{3} \mu^{’}_s(r)$  :diffusion coefficient

$\mu^{’}_s$ :reduced scattering coefficient

$c=c_0/n $ :speed of light in the medium

$S_0(r,t)$ :light source

frequency-domain diffusion equation
$$
-\nabla \cdot D(r) \nabla \Phi(r)+\left(\mu_{a}(r)+\frac{j \omega}{c}\right) \Phi(r)=S_{0}(r)
$$
discretization:
$$

\sum_{i} \Phi_{i} \sum_{k}\left(D_{k}\left\langle\phi_{k}, \nabla \varphi_{i} \cdot \nabla \varphi_{j}\right\rangle- D_{k}\left\langle\phi_{k} \nabla \varphi_{i}, \varphi_{j}\right\rangle_{\partial \Omega}+\left(\mu_{a}^{k}+\frac{j \omega}{c}\right)\left\langle\phi_{k} \varphi_{i}, \varphi_{j}\right\rangle\right)=\left\langle S_{0}, \varphi_{j}\right\rangle
$$
$\phi_k$ :basis on the reconstruction mesh

$\varphi_i$ and  $\varphi_j$ ：basis and weight functions on the forward mesh

$\langle f,g \rangle$ : intergration  $\int_{\Omega} fg dr$  over volume $\Omega$

$\langle\vec{f}, g\rangle_{\partial \Omega}$ : surface integration $\int_{\partial \Omega} \vec{g} \vec{f} \cdot d \vec{S}$  on the boundaries $\partial \Omega$ 

->final form for the forward quation（6）:
$$
\sum_{i} \Phi_{i}\left(\sum_{k} D_{k}\left\langle\phi_{k}, \nabla \varphi_{i} \cdot \nabla \varphi_{j}\right\rangle+\frac{1}{2 \alpha}\left\langle\varphi_{i}, \varphi_{j}\right\rangle_{\partial \Omega}+\sum_{k}\left(\mu_{a}^{k}+\frac{j \omega}{c}\right)\left\langle\phi_{k} \varphi_{i}, \varphi_{j}\right\rangle\right)=\left\langle S_{0}, \varphi_{j}\right\rangle 
$$
**linear equation** in form of $A \mathbf{x}=\mathbf{b}$ 

###### Mesh Generation

1. create a uniform 3-D grid
2. split each cube based on a T5 rule

dual-mesh scheme: a forward mesh for diffusion modeling and a separate reconstruction mesh to represent the optical properties

different mesh densities, the higher one for the forward mesh, the lower one for the reconstruction mesh

###### Inverse Problem

nonlinear optimization problem （7）
$$
\arg \min _{\mu_{u}, D}\left\|\boldsymbol{y}-\Phi\left(\mu_{a}, \boldsymbol{D}\right)\right\|^{2}+\lambda\left\|\left(\mu_{a}, \boldsymbol{D}\right)\right\|^{2}
$$
Gauss-Newton method updates $\mu_a$ and $D$ vectors iteratively （8）
$$
\left(J_{k}^{T} J_{k}+\gamma_{k} I+\lambda I\right)\left(\Delta_{k} \mu_{a}, \Delta_{k} \boldsymbol{D}\right)^{T}=J_{k}^{T}\left(y-\Phi_{k}\left(\mu_{a}, \boldsymbol{D}\right)\right)
$$
$\triangle_{K} \mu_{a}$ and $\Delta_{k} D$ : property updates of absorption and diffusion coefficients

$\gamma_{k}$ : determined by empirical approach 

$J_k$ : Jacobian matrix defined as $J_{k}=\left(J_{\mu_{a}} \quad J_{D}\right)$  （9）
$$
\begin{array}{l}{J_{\mu_{a}}((s, r), \tau)=\frac{\partial \Phi_{s, r}}{\partial \mu_{a}^{\tau}}=\sum_{e \in \Omega_{r}}\left(M_{\tau}^{e} \Phi_{s}^{e}\right)^{T} \widehat{\Phi}_{r}^{e}} \\ {J_{D}((s, r), \tau)=\frac{\partial \Phi_{s, r}}{\partial D_{\tau}}=\sum_{e \in \Omega_{r}}\left(H_{\tau}^{e} \Phi_{s}^{e}\right)^{T} \widehat{\Phi}_{r}^{e}}\end{array}
$$
a heuristic re-weighting scheme when solving (8)：
$$
\left(J_{k}^{T} J_{k}+\gamma_{k} \Sigma_{1}+\lambda \Sigma_{2}\right)\left(\Delta_{k} \mu_{a}, \Delta_{k} \boldsymbol{D}\right)^{T}=J_{k}^{T}\left(y-\Phi_{k}\left(\mu_{a}, \boldsymbol{D}\right)\right)
$$

###### Data Calibration and Source/Detector Coupling Coefficient Estimation

(16)
$$
\Phi_{T}^{\mathrm{cal}}=\frac{\Phi_{T}^{\mathrm{meas}}}{\Phi_{p}^{\mathrm{meas}}} \Phi_{p}^{\mathrm{model}}
$$
$\Phi_{T}^{\text { meas }}, \Phi_{p}^{\text { meas }},$ and $\Phi_{p}^{\text { model }}$  : measured target data, measured and model prediction of calibration phantom data

not sufficient to remove all the systematic errors

simultaneous determination of coupling coefficients (18)
$$
\left(J_{k}^{T} J_{k}+\gamma_{k} I+\lambda I\right)\left(\Delta_{k} \mu_{a}, \Delta_{k} \boldsymbol{D}, \Delta_{k} \mathbf{s}, \Delta_{k} \mathbf{d}\right)^{T}=J_{k}^{T}\left(\mathbf{y}-\operatorname{diag}(\mathbf{s} \otimes \mathbf{d}) \Phi_{k}\left(\mu_{a}, \boldsymbol{D}\right)\right) \\
\begin{array}{l}{J_{\mathrm{s}}=\operatorname{diag}(1 \otimes \mathbf{d}) \Phi} \\ {J_{\mathrm{d}}=\operatorname{diag}(\mathbf{s} \otimes 1) \Phi}\end{array}
$$


advantages: greatly reduce the previously mentioned artifacts

side effect: reduce target contrast

(24) perform high-pass filter on SD distributions
$$
S_{i} \leftarrow S_{i}-\frac{\sum_{j=1}^{N_{i}} S_{i, j}}{N_{i}}
$$

######  Bulk Property Estimation and Image Reconstruction 

estimated optical properties were used as homogeneous initial guess for the image reconstruction 

can not be used for the second stage (SD coefficients maximum coupling to the optical images)

### Results

###### Phantom reconstruction

maximum absorption contrast are lower than expected contrast  2:1

###### Clinical Data Reconstructions

![1563589977757](../AppData/Roaming/Typora/typora-user-images/1563589977757.png)

For breasts with very little glandular content, the averaged HbT values are relatively small

For breasts with small amount of glandular tissue, a positive contrast in HbT from the bulk values at the glandular region appears in the images

###### pressure simulations

expect lower-HbT content in the region where tissue stress is stronger

breast tumors have been shown to have even higher stiffness and interstitial pressure than normal breast tissue  

The additional complexities of the tissue compression response represent an opportunity for identifying dynamic characteristics useful in cancer diagnosis.

###### Problems and further study

1. expect more hemodynamic change during the measurement period in protocol 1 than in protocol 2. **(why?)**  

   (temporal duration between the initial breast compression and the optical data acquisition duration in protocol 2 is roughly 1 or 2 min longer than in protocol 1, why more duration caused less change?)

2. tissue compression response ->dynamic characteristics for cancer diagnosis

3. only healthy breasts in this paper->further study in tumor cases

