# Gliobastoma-Marker-Prediction


Data Collection:

    This step involved collecting data from multiple hospitals, upload them into a common cloud based storage, download them locally and analyse the original directory structure.


Preprocessing and Data Organization:

    All the data collected from the hospitals were uploaded in different formats and directory structures. Therefore it was necessary reorganizing the images in a standard way. This was done automatically using a python script. In additiona all the folders and files containing sensible data were anonymized and eliminated if not containing DICOM files. Afterwards, the image size was rescaled to be consistent with the minimum image size available, and the pixel density was readjusted as well for it to be uniform across the whole dataset. Furthermore, once the objective of restructuring the folder tree, having a uniform dataset of DICOM files and anonymizing the data was completed, it was necessary to associate the markers labels per each subject. This was done via mapping of an excel sheet to the directory tree.

Segmentation:

    Once the data were structured, it was necessary to load them sequentially and applying image segmentation to the glioblastoma area of the brian. This procedure was done using an alghoritm called GliomaSeg which leveraged Convolutional Neural Network, which are commonly used for imaging related tasks. The convolutional filters apply a series of filters to the picture which subsequently is fed into fully connected layers which have the scope of classifying the different regions of the image.


Feature Extraction:

    At this point a preliminary analysis of the dataset was done using different tools to analyse the RGB intensity distribution across the pictures, the average volume of the glioblastoma based on the previous algorithm, and the thickness of each slice. This was done as a prelimiary step to identify possible outliers present int he dataset.


Data Augumentation and Processing:
    
    At this point the images were organized into a 3D arrays of pixels so that all the cartesian axis were considered at once and the future neural network model could consider a full 3D array rather than slices of images.  Subsequently the dataset was augmented using sensible data augumentation technique which would still present plausible data to the neural network model. SOme of those techniques were: elastic deformation, mirrowing, noise injection, intensity variation. The goal was to simulate anatomical variability, making the model more robust to noise introduced by machinary errors and simulate different scanner settings or slightly different positions of the patient.

Data Splitting:

    The dataset was split as per standards, into training test and validation. This was done with the objective to plot the significant metrics throughout the whole training cycle to determine the performance of the model. At the same time it was veryfied that the stes of arrays were mutually exclusive and that there were no data overlaps between the different groups.


Model Selection and Training:

    The model will be mainly composed by Convolutional Neural Network layers, and coupled with dense layers and a potential classifier such as XGBoost that provides regularizing gradient boosting and has showewed to be applicable in the case of MRI analysis. The trained model will 'learn' to recognize and extract features from the initial 3D array representing the gliobastoma, in order to associate it with specific markers.

Model Evaluation:

    The performace of the model will be monitored constantly during the validation, test and training phase. THis will be done by looking at the mutual relationships between learning curves and other metrics like precision, accuracy, recall, F1-score and area under the ROC curve.


Model Development:

    Once the model will be built and trained variations will be made with the introduction of new datasources from different hospitals, and at the same time new neural network architectures will be introduced to improve the performance metrics of the model. Potentially a website could be created where the model will be made available for patients having a gliobastoma where the model will give feedback regarding potential markers present in the tumor. This however, will not be in anyway a medical diagnosis but could be used as pure support for doctors.
