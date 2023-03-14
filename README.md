# TV1_ODIR19-
<i>Ophthalmic diseases classification</i>
## Ocular Disease Intelligent Recognition (ODIR-2019)

### Introduction

The growing development and advancement of Artificial Intelligence (AI) techniques in healthcare along with AI-powered tools has significantly improved over the years, whether in image analysis, robotics-assisted surgery, patient monitoring, medical device automation, personalized-medicine and drug identification ... (see references 1 & 2)

During my 9-months training in data science I worked on a project for the development of an AI for image-based disease classification made based on a structured ophthalmic database of "real-life" patients.  

### Source

The dataset was provided for the "Peking University International Competition on Ocular Disease Intelligent Recognition (ODIR-2019)" (Source : https://odir2019.grand-challenge.org/) and is based on fundoscopy images of 5,000 patients from different hospitals and medical centers across China. 

### Background 

Fundoscopy is a cost-effective examination of the inner anatomical details of the eyeball allowing for the diagnosis of eye diseases and the identification of vision-loss associated risk factors 

Indeed, through the image-based analysis of the retina, it is possible to detect a broad range of alterations of the eye anatomy (see https://www.exetereye.co.uk/the-eye/eye-anatomy/ for further info). 

As the light enters the eye, it passes through the crystalline lens that refracts it. With age, this lens can opacify in a condition named, <b>cataract</b>, where patients experience a blurry vision and eventually blindness.

Once refracted, the light is focused onto the macula, a specific spot of the retina. This spot can also be altered with age, causing a disease with vision loss or impairment named <b>Age-related Macular Degeneration (AMD).</b>

Then, as it hits the retina, the light is converted into information transmitted to the brain through the optic nerve which can be damaged in some diseases such as <b>glaucoma</b>.

The retina is also home to the cilioretinal arteries that supply it with blood. Diseases affecting the morphology, shape or diameter of the blood vessels, such as <b>hypertension</b> or <b>diabetes</b>, will affect cilioretinal arteries and eventually lead to blindness.

Moreover, any modifications in the shape of the eyeball can prevent the light from being focused onto the retina causing a blurry vision. This happens in <b>myopia</b> which is marked by choroidal thinning and morphologic changes in the retina.

### Data info

The dataset provided in this ODIR-19 challenge contains information regarding 5000 patients and info related to their sex, age, and <i>diagnositc keywords</i> made by medical doctors for each of the left and right eye-fundus. 

Based on these <i>diagnositc keywords</i>, <i>labels</i> are assigned to each patient. 

### Aim

The aim here is to develop an AI-based classification of the diseases based on the dataset provided using the patient's <i>labels</i> and color eye-fundi.

### Identifying primary flaws and weakness: 

<b>1. Data organization </b>
<br>The dataset is a patient-based dataset, meaning each row contains all data for each individual patient, and thus includes both eye-fundi and each of their related information.
<br>However, one disease may not affect each eye at the same time, the same intensity, if at all. 
<br>Moreover, pooling both patient's eye fundi increases the combination of <i>diagnositc keywords</i>, thus <i>labels</i>, possible, which may in return affect the efficiency of our classification model. 

<i>--> As we seek to classify the eye-fundi based on specific diseases, we will need a fundi-based dataset to allow our model to train on each fundus individually</i>

<b>2. Data labeling </b>
<br>Within the dataset are 8 columns related to <i>labels</i> : N, D, G, C, A, H, M and O, corresponding to the terms Normal, Diabetes, Glaucoma, Cataract, AMD, Hypertension, Myopia and Other diseases/abnormalities, respectively.

In the current dataset, the annotated <i>labels</i> are assigned to each patient based on the following rules:
<br>(1) <i>labels</i> are determined based on <i>diagnosis keywords</i> given by medical doctors,
<br>(2) the Normal <i>label</i> is assigned to a given patient if and only if <u>both</u> or his/her left and right diagnosis keywords are "normal fundus";
<br>(3) disease-related <i>labels</i> are assigned whenever at least one of both fundi is not diagnosed as "normal fundus";
<br>(4) all suspected diseases or abnormalities as considered as fully diagnosed diseases or abnormalities.
<br>(5) one patient may be assigned one or multiple <i>labels</i>.

<i>--> 1) It seems important to have a look at the correspondance between the labels and their corresponding diagnotic keywords to assess the homogeneity of the terms and their assignation to a given label (especially with the different hospitals and medical centers being involved).
<br>--> 2/3) Since disease-related labels are assigned even if one of the two fundus' diagnostic keywords is 'normal fundus', it seems important to treat each fundus separetely. 
<br>--> 4) Finally, given that a disease-related label can be assigned even when the diseases is only 'suspected', it might indicate that the dataset contains images of different stage of the disease. Such disparity could create a biais when running our classification model.</i>

<b>3. Image quality </b> 
<br> Finally, because the images come from different medical centers and hospitals, there are differences in their quality and size.
<br>However, the organizers of the challence indicates that the following ones present background issues. 

<i>--> Decision was made to discard them from the dataset (2174_right.jpg 2175_left.jpg 2176_left.jpg 2177_left.jpg 2177_right.jpg 2178_right.jpg 2179_left.jpg 2179_right.jpg 2180_left.jpg 2180_right.jpg 2181_left.jpg 2181_right.jpg 2182_left.jpg 2182_right.jpg 2957_left.jpg 2957_right.jpg)

<b>4. Image analysis </b> 
<br>Given the broad range of diseases fundoscopy can detect, and knowing their identification might rely on the analysis of different key structural details of the retina, there might be a limitation with using a "simple" non-segmented image analysis of the fundi. 

<i>--> To potentialize the classification by our future model, image segmentation may be required.</i>

### References

1. Bajwa J. et al. Artificial intelligence in healthcare: transforming the practice of medicine. Future Healthcare Journal, 2021 Vol 8, No 2: e188–94.
2. Bohr A & Memarzadeh K. The rise of artificial intelligence in healthcare applications. Artificial Intelligence in Healthcare, 2020, Pages 25-60 Chapter 
