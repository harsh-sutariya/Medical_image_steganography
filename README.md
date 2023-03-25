# Securing Medical Images with PVD

# Introduction

The amount of digital visual data (image, video and 3D object) has increased rapidly on the Internet. Image, video and 3D object security becomes increasingly important for many applications, e.g., confidential transmission, video surveillance, military and medical applications. For example, the necessity of fast and secure diagnosis is vital in the medical world. Nowadays, the transmission of visual data is a daily routine and it is necessary to find an efficient way to transmit them over networks.  

The works presented in this project show how encryption algorithms provide security to medical imagery. The main objective is to guarantee the protection of medical images during transmission, and also once this digital data is archived. The subsequent challenge is to ensure that such coding withstands severe treatment such as compression. When a physician receives a visit from a patient, he often requires a specialist opinion before giving a diagnosis. One possible solution is to send images of the patient, along with a specialist report, over a computer network. A region of Interest (ROI) of a medical image is an area including important information and must be stored without distortion. Nevertheless, computer networks are complex and espionage is a potential risk. We are therefore faced with a real security problem when sending data. For ethical reasons, medical imagery cannot be sent when such a risk is present, and has to be better protected. Encryption is the best form of protection in cases such as this. Many different techniques for the encryption of text already exist.

In this project, we first try to embed the patient data of a hospital by using Pixel Value Differencing and then the second part includes the encryption and decryption of data using RSA Algorithm. The accuracy of both the algorithms were measured in the working of the project and the best out of the both shall be recommended for the use in real world implementation.  

# Proposed Methodology
Along with RSA encryption, a PVD embedding method has been proposed. We use RSA encryption to encrypt patient data. The PVD embedding approach is then used to embed the encrypted data into the medical image.

1. RSA Encryption  
We take patient data such as name, age, patient id, health issue. We then try to encrypt this data using the RSA Encryption Algorithm.

  RSA Algorithm(To Generate Key Pair):-  
    A. Select a value of e from 3,5,17,257,65537  
    B. repeat  
    C. p ← genprime(k/2)  
    D. until (p mod e) ≠ 1  
    E. repeat  
    F. q ← genprime(k - k/2)  
    G. until (q mod e) ≠ 1  
    H. N ← pq  
    I. L ← (p-1)(q-1)  
    J. d ← modinv(e, L)  
    K. return (N,e,d)  
    
  Encryption :-  
  Sender does the following:-  
    A. Obtains the recipient B's public key (n,e)  
    B. Represents the plaintext message as a positive integer m with 1<m<n  
    C. Computes the ciphertext c= ( m ^ e ) mod n  
    D. Sends the ciphertext c to B.  

2. Embedding encrypted data into the image using PVD  
The pixel-value differencing (PVD) scheme uses the difference value between two consecutive pixels in a block to determine how many secret bits should be embedded.

The embedding algorithm is described as follows.  
  Step 1. Calculate the difference di= | pi-pi+1 | for each block of two consecutive pixels pi and pi+1 .  
  Step 2. Search the quantization range table for di to determine how many bits will be embedded. Obtain the range Ri in which Ri= [ li,ui ], where li and ui are the lower bound and the upper bound of Ri, and m= [ log2(ui-li) ] is the number of embedding bits.  
  Step 3. Read m secret bits from the secret bit stream, and transform it into decimal value b.  
  Step 4. Calculate the new difference di’= li + b. Ensure both di and di’ are in the same range Ri.  
  Step 5. Average di’ to pi and pi+1. The new pixel values pi’ and pi+1’ are obtained by a formula.  
  Repeat step 1-5 until all the secret bits are embedded.  
  
# System Design  
  
The project is designed in a manner that the working of the code is easily visible and understandable. All relevant Python scripts are in the main directory while the dataset and resultant outputs are in one of two directories embedding and extraction.  

The directory structure is as follows.  
pvd-steganography  
├── pvd_script  
├── rsa_script  
├── main_script  
├── embedding  
│   ├── reference_image  
│   ├── patient_data  
│   ├── encrypted_patient_data  
│   └── output  
│       └── embedded_image  
└── extraction  
    ├── reference_image  
    ├── embedded_image  
    └── output  
        ├── encrypted_patient_data  
        └── patient_data  
        
The reference image and the patient data are first used for encrypting and then embedding. Then the reference image and the embedded image are used to generate the encrypted data which is then used to obtain the decrypted patient data.  

# Results and Conclusion  

Patient data has been encrypted using RSA encryption. The encrypted data is subsequently embedded into the medical image using the PVD embedding method. Encryption and embedding are performed using the patient data and the reference image, respectively. The reference image and the embedded image are used to generate the encrypted data which is then used to obtain the decrypted patient data. In our project, patient data is inserted into a patient's medical scan using Pixel Value Differencing (PVD). The medical scan in question serves as the reference image and is the means through which the patient's private medical data can be safely conveyed. One of the benefits of using the PVD process for steganography is that there is no discernible difference between the two images. The project flawlessly completes the task of Pixel Value Differencing on the dataset of medical photos, embedding the encrypted patient data into those images.  
