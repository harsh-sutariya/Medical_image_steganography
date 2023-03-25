# Securing Medical Images with PVD

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
