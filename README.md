![Sin titulo](http://atvs.ii.uam.es/atvs/github/mEBAL/mEBAL_ICONO1.jpg)
***
# About
We present mEBAL, a multimodal database for eye blink detection and attention level estimation. mEBAL is a database which is initially introduced in [arXiv technical report](https://arxiv.org/abs/2006.05327) and then accepted by the [22nd ACM International Conference on Multimodal Interaction](http://icmi.acm.org/2020/). 

The eye blink frequency is related to the cognitive activity and automatic detectors of eye blinks have been proposed for many tasks including attention level estimation, analysis of neuro-degenerative diseases, deception recognition, drive fatigue detection, or face anti-spoofing. However, most existing databases and algorithms in this area are limited to experiments involving only a few hundred samples and individual sensors like face cameras. 

The proposed mEBAL improves previous databases in terms of numbers samples in eye blink and cognitive information available.  In particular, **three different sensors** are simultaneously considered: **Near Infrared (NIR)** and **RGB cameras** to capture the face gestures and an **Electroencephalography (EEG) band** to capture the cognitive activity of the user and blinking events.

Regarding the size of mEBAL, it comprises **3,000 blink samples** and the corresponding **attention level** from **38 different students** while conducting a number of e-learning tasks of varying difficulty.**This information is avalible on this web [[Download Database](#instructions-for-downloading-mEBAL)].**

The following table shows the sensors and the information captured:

![Sin titulo](http://atvs.ii.uam.es/atvs/github/mEBAL/Table1.jpg)
<br/>The following sections describe the motivation, the activities designed, the sensors, the public database and share mEBAL database with the community to advance in this area:

# Motivation

The main motivation  of this work is  **the improvement of the virtual education** using e-learnig platforms. Virtual education technologies are growing up, with a market reaching a turnover around 240.000 million dollars. 
**E-learning platforms** are important tools to get high quality online education. They allow to capture student information to better understand the student behavior and conditions and this information can be used to create personalized environments. Information such as the heart rate [1], the emotional state, or the **cognitive activity** can be used to improve e-learning platforms.
Undoubtedly, e-learning platforms will benefit significantly by exploiting the **attention level** of the student. This could be used to: **i)** adapt dynamically the environment and content  based on the attention level, and **ii)** improve the educational materials and resources with a posterior analysis of the e-learning sessions (e.g. detecting the type of contents more appropriate for a specific student).

**Since the 70s there are studies relating the eye blink rate with cognitive activity like attention**. The studies suggest that **lower eye blink rates** can be associated to **high attention** periods while **higher eye blink rates** are related to **low attention levels**. Therefore, in this context, automatic eye blink detection can be a tool for estimating the attention level of the students and improving e-learning platforms.

For this reasons, we hope that mEBAL will be valuable to the scientific community thanks to the multimodal nature: **Cognitive Activity and Eye Blink detection**.


# Tasks


The activities designed to conform the database consist of 8 different tasks that can be categorized in the following three groups:
 
 - **Enrollment form:** name and surname, ID number, nationality, e-mail address, etc. (low level of attention is expected);
 
 - **Writing questions:** these questions are oriented to measure the students’ cognitive abilities under different situations such as solving logical problems, describing images, crosswords, finding differences, etc. (increasing level of attention is expected)
 
 - **Multiple choice questions:** aimed to detect the students’ attention and focus levels (high level of attention is expected).

The questions are selected from popular riddles and they present different levels of difficulty. The interface is designed to ensure data from different nature: free text typing (writing questions), fixed text typing (enrollment form), mouse movement (multiple choice questions), visual attention (describing images and finding differences), etc.



# Sensors

   We designed a multimodal acquisition framework to monitor cognitive and eye blink activity during the execution of online tasks based on the edBB platform [2] for remote education assessment:
   
![Sin titulo](http://atvs.ii.uam.es/atvs/github/mEBAL/Framework_mEBAL2.jpg)

   The acquisition setup consisted of the next components: 

   - An **EEG headset** by NeuroSky that captures 5 channels of electroencephalographic information **(𝛼, 𝛽,𝛾, 𝛿, 𝜃)**. These signals provide temporal information related to the cognitive activity of the student. The sensor also provides a temporal sequence with the eye blink strength. The sampling rate of the band is 1 Hz. The EEG band is used to capture the **cognitive activity of the student** and **the eye blink candidates**. **We have made a manual refinement of these eye blink candidates detected by the band to eliminate false positives**. These refined eye blinks will be used as eye blink groundtruth.
  
   - An **Intel RealSense** (model D435i), which comprises **1 RGB** and **2 NIR cameras**. It is  configured to 30 Hz, one frame every 33ms. It's known that an average blink takes 100ms to 400ms, therefore, an eye blink can take between 3 to 13 frames.
  
We used facial landmark detection to track the eyes position and classify the images as blink or no-blink based on the eye blink groundtruth.



# Database

mEBAL comprises a total of 3,000 blink samples from both eyes acquired with 1 RGB and 2 NIR cameras. Each sample comprises 19 frames (around 600 ms.) for a total number of images of **342,000** (3,000 × 19 × 2 × 3). Aspects such as the user position and changes in the illumination were considered during the acquisition in order to simulate realistic e-learning scenarios. 11 out of the 38 students used glasses.

mEBAL was collected in a constrained environment, but it is rich in pose, illumination changes, and other naturally-occurring factors. It can be seen in the next figure:
![Sin titulo](http://atvs.ii.uam.es/atvs/github/mEBAL/Examples_Blink3.jpg)


The mEBAL dataset was obtained from the **raw data provided in the edBBdb** [2]. The eye blink and attention level information was labelled following a semi-supervised method. First, eye blink candidates were selected using the EEG band signals (eye blink strength is an attribute provided by the EEG band SDK). Second, we made a manual refinement of the eye blink samples detected by the band to eliminate false positives. Once the eye blink samples were validated, we stored the 9 frames previous and posterior to the eye blink event (19 frames in total for each eye blink). These frames can be used to exploit the temporal information proposed in some approaches of the literature. Finally, we used facial landmark detection [3] to track the eye position.

**The video recorded during the session, eye bounding boxes, and the cropped eyes are provided in our contributed mEBAL database**. Additionally, we include **the cognitive temporal signals α, β,γ , δ, θ** provided by the EEG band. Also, we include only a one folder with **all closed eyes** obtaining a sample of both eyes for each eye blink  (the 9 frame is eyes closed in each eye blink) and only a one folder with **eyes open** too (the 18 frame usually is  eyes open in each eye blink).  These frames can be used to an eye blink detector based on  Convolutional Neural Networks (CNN), for example, the proposed  in the paper mEBAL, where  the network is trained as a binary classifier, eyes open or closed, using the mEBAL database.

The next table shows the most popular eye blink detection databases. As can be seen, all available databases comprise only a few hundred samples, however mEBAL **includes 3000 blink samples**:

![Sin titulo](http://atvs.ii.uam.es/atvs/github/mEBAL/Table_eye_blink_detection_databases3.jpg)

This means that is **8 times** larger than HUST-LEBW database, the existing database with largest number of eye blinks. Data is critical to train end-to-end approaches such as those based on neural networks. Furthermore, **mEBAL is unique in to use 3 sensors and to include the attention level**.



# Instructions for Downloading mEBAL

1) [Download license agreement](), send by email one signed and scanned copy to **atvs@uam.es** according to the instructions given in point 2.

2) Send an email to **atvs@uam.es**, as follows:

   *Subject:* **[DATABASE: mEBAL]**

   Body: Your name, e-mail, telephone number, organization, postal mail, purpose for which you will use the database, time and date at which you sent the email with the signed      license agreement.

3) Once the email copy of the license agreement has been received at ATVS, you will receive an email with a username, a password, and a time slot to download the database.

4) [Download the database](http://atvs.ii.uam.es/atvs/intranet/free_DB/edBB/), for which you will need to provide the authentication information given in step 4. After you finish the download, please notify by email to **atvs@uam.es** that you have successfully completed the transaction.

5) For more information, please contact: **atvs@uam.es**


# License

Any entity using this dataset agrees to the following conditions:

THIS DATASET IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.



# References

+ [1] Hernandez-Ortega, J.; Daza, R.; Morales, A.; Fierrez, J.; and Tolosana, R. 2020. Heart Rate Estimation from Face Videos for Student Assessment: Experiments on edBB. In *IEEE Computers, Software, and Applications Conference*. [[pdf](https://arxiv.org/pdf/2006.00825.pdf)]


[2] Zhang, K.; Zhang, Z.; Li, Z.; and Qiao, Y. 2016. Joint face detection and alignment using multi-task cascaded convolutional networks. *IEEE Signal Processing Letters* 23(10):1499–1503.

[3] Cao, Q., et al. 2018. VGGFace2: A dataset for recognising faces across pose and age.


# Contact:

For more information contact Aythami Morales, associate professor UAM at aythami.morales@uam.es

