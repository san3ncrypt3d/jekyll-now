---
layout: post
title: IOT Security & Performance comparison of cryptographic algorithms
---

**Abstract- A stand-alone IoT device is a non-standard computing device which has the ability to connect to the internet and transmit data. When various stand-alone IoT devices are connecting to the Internet, it brings a lot of challenges, such as scalability, naming, resource constraints, interoperability, security and privacy. Connectivity between the internet and everyday objects and the capability to exchange data between them arises a lot of potential privacy and security risks. As a result, potential security and privacy risks exist in broad scope, ranging from the physical world to the Internet, and if they are exploited it can cause a lot of damage. As a result of the risk’s mentioned above, it is critically important to test the existing cryptographic encryption/decryption techniques on IoT devices to determine if they are efficient enough in terms of execution time, power consumption and to determine if there is a need for a new lightweight cryptographic algorithm for IoT devices.**

*I.	 INTRODUCTION

The advent of IoT and the increase in the usage of application-based processors has led to a significant increase in the data being stored, transmitted and processed. As a result of this significant increase, the security around data storage, transmission and processing of data’s needs to be examined. The science of making digital data secure by preventing unauthorized access is called cryptography. The best practices used to secure communication is ideally by encrypting any communications. Some of the most common examples of IoT devices are Raspberry Pi Zero W, Raspberry Pi  3 Model B+ and BeagleBone Black. Figure [1],[2] and [3] depicts these IOT devices. Reference [1] depicts the various IoT based applications of these devices and [2] provides a comparison of Han algorithm with AES and RSA. However, implementing security mechanisms such as encryption or decryption may demand more power, increased resource consumption and delays. As a result, it is essential to analyze different encryption-decryption techniques and their effect on processors of IoT devices such as Raspberry Pi Zero W, Raspberry Pi 3 Model B+ and BeagleBone Black and analyze parameters such as efficiency, speed and power consumption. In this paper, we are going to implement, run and compare block ciphers such as AES, Blowfish, DES, Triple-DES and RC2. The ciphers will be running on the above mentioned IoT devices by encrypting file sizes ranging from 1 MB to 128 MB. By doing this will help to understand the need for light-weight cryptographic schemes for IoT devices.


*II.	 IoT DEVICES



A.	 Raspberry Pi Zero W

The Raspberry Pi family is a series of single-board computers with high memory, processors and ports that can be combined with a massive ecosystem of devices according to the requirement of the application. Reference [3] depicts a comparison between many IoT devices including Raspberry Pi. 

Raspberry Pi Zero W is designed to be as compact and flexible. It is a 1 GHz BCM2835 single-core processor with 512 MB RAM. The device is 65mm long by 30mm wide with802.11 b/g/n wireless LAN and Bluetooth. The device is also equipped with Mini HDMI and USB On-The-Go ports, Micro USB power, HAT-compatible 40-pin header, Composite video and reset headers and CSI camera connector. The devices mandate a microSD card with an OS (Raspbian Buster Lite) and a 5V power supply to power the board.

![](/images/2020-1-22-IOT/1.png)

Figure 1. Board Representation of Raspberry Pi Zero W


B.	Raspberry Pi 3 Model B+

The Raspberry Pi 3  Model B+ is the latest edition of the Raspberry Pi 3 range. This device is powered by a 64-bit quad-core Broadcom BCM2837B0, Cortex-A53 (ARMv8) processor running at 1.4GHz.  This device has an overall dimension of  85mm x 56mm x 17mm.  This device has 1GB LPDDR2 SDRAM which makes it a faster IoT device. This device also comes with a built-in 2.4GHz and 5GHz IEEE 802.11.b/g/n/ac wireless LAN, Bluetooth 4.2, BLE (low energy Bluetooth chip) on board. This board comes with a wide range of ports such as 4 USB 2.0 ports, Gigabit Ethernet over USB 2.0 (maximum throughput 300 Mbps), Extended 40-pin GPIO header pins, Full-size HDMI ports, CSI camera port for connecting a Raspberry Pi camera, 4-pole stereo output and composite video port and Power over Ethernet (PoE) capability via a separate PoE HAT as well as enhanced cooling features. This device needs an operating system (Raspbian or NOOBS) and a 3A charger at 5V for powering up the board.

![](/images/2020-1-22-IOT/2.png)

Figure 2. Board Representation of Raspberry Pi 3 Model B+


C.	BeagleBone Black


Beagle Bone is very similar to Raspberry Pi, the BeagleBone family has multi-purpose hardware with a range of ports and features.  Reference [4] depicts an excellent explanation of different devices of the BeagleBone family. This device comes in a dimension of 86.40 mm × 53.3 mm. This device comes with an onboard 4GB 8-bit eMMC on-board flash storage, 512MB DDR3 RAM, 3D graphics accelerator, NEON floating-point accelerator and 2x PRU 32-bit microcontrollers. BeagleBone connectivity includes USB client for power & communications, USB host, Ethernet, HDMI and 2x 46 pin headers. The major advantage BeagleBone have over Raspberry Pi is the 65 GPIO pins.  Reference [5] shows a comparison of BeagleBone to Raspberry Pi and the architecture of BeagleBone in detail. 

![](/images/2020-1-22-IOT/3.png)
Figure 3. Board Representation of BeagleBone Black 


*III.	 BLOCK CIPHERS

Block cipher is a cryptographic method of converting a block of text into encrypted form with a symmetric key.  Block cipher has various modes of operation to eliminate the chances of the similar encryption of identical blocks. Some of the different modes of operation in block ciphers are cipher block chaining (CBC), cipher feedback (CFB), counter (CTR), and Galois/Counter Mode (GCM),  ElectronicCode Book Mode (ECB) among others.  The block ciphers used in this paper are CBC and CFB.  Reference [8] explains various modes of operation in more details and the attacks on these ciphers. The various block ciphers used in this paper are AES, Blowfish, DES, Triple-DES and RC2.



A.	Cipher Block Chaining

Created by IBM in 1976 according to reference [12], CBC mode performs an XOR to each plain text block to the ciphertext block that was created previously. And the final result is encrypted using whichever algorithm is used to encrypt like normal. The caveat for CBC mode is that due to the nature of this whole process, it cannot be performed on multiple threads at the same time, it only runs on a single thread, but despite this massive disadvantage, it is still widely used in a loT of applications. 

![](/images/2020-1-22-IOT/4.png)

Figure 4. Encryption in CBC mode 


B.	Cipher Feedback

Cipher Feedback (CFB) mode for block cipher is similar to CBC mode, but instead of XOR ciphertext with the plaintext for the next round, it encrypts the ciphertext from the previous rounds and then adds the output to the plaintext. CFB mode support multi-thread implementation, but the security level is comparable to CBC mode.

![](/images/2020-1-22-IOT/5.png)

Figure 5. Encryption in CFB mode




●	Advanced Encryption Standard (AES) 

AES, or Advanced Encryption Standards, is the standard symmetric encryption algorithm for US federal organizations and is the most widely used symmetric encryption algorithm in the world. According to the reference [9], this encryption method uses what is known as a block cipher algorithm, these “blocks” which are the size of the input plaintext and output ciphertext. AES-128 uses 128bits input/output and performs 9 rounds of encryption, AES-192 uses 192bits input/output and performs 11 rounds of encryption, and AES-256 uses 256bits input/output and performs 13 rounds of encryption. 


●	Blowfish 
Developed by Bruce Schneier, Blowfish can be used as a drop-in replacement for the DES algorithms. It uses the variable-length key, ranging from 32 bits to 448 bits. Unlike AES/DES which was designed with 64-bits processors in mind, Blowfish is designed for 32 bits processor. It is significantly faster than DES. Although the key size for Blowfish can be as large as 448 bits, the block size is 64 bits, which makes it significantly less secure compared to AES. Based on reference [10], due to the fact that Blowfish uses key-dependent lookup tables, the performance is more dependent on how the platform handles memory and caches, not CPU processing power. 


●	Data Encryption Standard (DES)
DES is one of the most widely used and accepted encryption algorithms. It uses 64 bits block and 64 bits key, although the input key for DES is 64 bits long, the actual size of the key is 56 bits long. DES goes through 16 calculations to encrypt the plain text with the key. DES is considered the de-facto “legacy” standard algorithm for encryption, and it's still widely used by many devices, due to its compatibility with older devices. 

●	Triple-Data Encryption Standard (3DES) 
Triple DES was designed to correct the previous flaws of the DES system without coming up with a brand-new cryptosystem. Previously, DES uses a 56-bit key and it’s not secure enough to encrypt sensitive data, Triple-DES effectively extends the key size by performing the algorithm three times, which makes it a 168-bit key size equability, the three generated keys are marked as K1, K2, and K3. The plain text encrypted by K1 will be passed onto K2 and then finally processed by K3, other than that, Triple-DES is fundamentally doing the same thing as DES, but instead of performing one round with a 56-bit key, it performs three rounds and effectively making a 168-bit key. Unlike DES, 3DES is still considered strong encryption by today’s standard.


●	Rivest Cipher 2 (RC2) 
RC2, also known as ARC2, having a key length of 40-bit, and it's the weakest among the other cryptosystems that we are comparing it against (AES, DES,3DES). It was designed and built in the late ’80s for export, due to the regulation back then, restricting American companies to export more complex encryption system. By today’s hardware standard, RC2 can be broken by Brute Force attacks.


*IV.	EVALUATION OF CRYPTOGRAPHIC ALGORITHMS


The comparison of devices used for this experiment is shown below: 

![](/images/2020-1-22-IOT/6.png)



Evaluation of efficiency, performance and swiftness of Intel processors are explained in reference [6] and [7]. However, these evaluations are not the same for IoT devices, therefore, a similar approach is taken to evaluate cryptographic algorithms on IoT devices to find out the execution time and power consumption.

Figure [6] depicts the procedure that we used to obtain all the data in this paper. The cryptographic algorithms that we used are all from the pycrypto library based on reference [14], which ensures that all the algorithms implementations are from the same sources, and in a similar manner. We’ve created different scripts for each algorithm, which inputs a text file, and performs encryption using corresponding algorithms and output an encrypted file. The program also records the execution times in seconds. Each algorithm is executed 5 times, and the average execution time was taken, this has been performed for each algorithm, each files size for all devices in both CBC and CFB mode. While executing the file, we also used a power consumption monitor to calculate the power draw. Figure [7] depicts a power consumption monitor. Since the power draws on maximum load is a constant on each device (e.g. encrypting 128MB using RC2 draws the same constant power as encrypting 128MB using DES) regardless of the algorithms. The total power consumption for various file sizes are calculated using the formula: 
1.	Amp * 120 V = Watt
2.	Watt * Execution time (convert to Hrs) = Watt hours/Day
3.	Watt hours/Day Converted to mAh [15] 

![](/images/2020-1-22-IOT/7.png)

![](/images/2020-1-22-IOT/8.png)

Figure 7. Power Consumption Monitor 


The execution time in seconds and power consumption in milli-Ampere-hours for various files for block ciphers on the Raspberry Pi Zero W in CBC mode and CFB mode are as shown in Table I & Table II:

![](/images/2020-1-22-IOT/9.png)
![](/images/2020-1-22-IOT/10.png)

The execution time in seconds and power consumption in milli-Ampere-hours for various files for block ciphers on the Raspberry Pi 3 Model B+ in CBC mode and CFB mode are as shown in Table III & Table IV:


![](/images/2020-1-22-IOT/11.png)
![](/images/2020-1-22-IOT/12.png)


The execution time in seconds and power consumption in milli-Ampere-hours for various files for block ciphers on the BeagleBone Black in CBC mode and CFB mode are as shown in Table V & Table VI:


![](/images/2020-1-22-IOT/13.png)
![](/images/2020-1-22-IOT/14.png)


Figure. 8 and 9 depict graphs comparing the execution speed of the various block ciphers on the Raspberry Pi Zero W, Raspberry Pi 3 Model B+ and Beagle Bone Black. Analyzing the graph, we can see the different execution speed for various file sizes.

From the graphs and the values shown in the table it is clear that for Raspberry Pi Zero W, Raspberry Pi 3 Model B+ and BeagleBone Black, the fastest cipher among the other ciphers tested in the paper is Blowfish. Therefore, Blowfish is considered the lightest, fastest and most efficient among the other ciphers tested on the IoT devices. Moreover, for various encryption schemes, Beagle bone and Raspberry Pi Zero W averaged about 72 percent of CPU and memory Consumption whereas Raspberry Pi 3 Model B+ executed the encryption schemes with an average of 40 percent.

From the Figure 10, 11 and 12, it's clear that power consumption and execution time has a linear correlation, which means the ratio between execution time and power consumption are 1:1. Due to the maximum power draw being a constant value across all devices (0.062 Amp for Raspberry Pi 3B+, 0.057 Amp for BeagleBone Black, 0.014 Amp for Raspberry Pi Zero W), it is safe to assume that when it comes to power consumption, the only variable that factors in is the execution time. Parameters like mode of operation, type of algorithms, and different file sizes do not directly impact power consumption, the only variable that affect power consumption is the time taken to run a cipher. Therefore, we can exclude all factors but time, when we calculate power consumption. (e.g. If DES and AES took exactly the same time to encrypt a file, power consumption should be relatively identical).


![](/images/2020-1-22-IOT/15.png)

Figure 8. Execution Speed Comparison of Block Ciphers in CBC Mode between Raspberry Pi Zero W, Raspberry Pi 3 Model B+, BeagleBone Black.   

![](/images/2020-1-22-IOT/16.png)

Figure 9. Execution Speed Comparison of Block Ciphers in CBC Mode between Raspberry Pi Zero W, Raspberry Pi 3 Model B+, BeagleBone Black


![](/images/2020-1-22-IOT/17.png)

Figure 10. Power consumption of Raspberry Pi 3B+ 

![](/images/2020-1-22-IOT/18.png)

Figure 11. Power consumption of BeagleBone Black

![](/images/2020-1-22-IOT/19.png)

Figure 12. Power consumption of Raspberry Pi Zero W


*V.	CONCLUSION


In this paper, we tested and compared the performance of the most widely used IoT devices. The execution time of the various ciphers tested on BeagleBone Black and Raspberry Pi Zero W was nearly double the amount of time taken to perform the various schemes on Raspberry Pi 3 Model B+ due to the processing speed of both  BeagleBone Black and Raspberry Pi Zero W being lower than that of the Raspberry Pi 3 Model B+. Moreover, the power consumption and memory consumption on BeagleBone Black and Raspberry Pi Zero W were also noticed to be higher than that of Raspberry Pi 3 Model B+. As a result, the Raspberry Pi 3 Model B+ can perform efficient, secure and faster data transmission when compared to the other two IoT devices. However, the BeagleBone Black has better available functionality (replete GPIO pins) if there is a situation where several interfaces needed to be added. Moreover, when it comes to power consumption, we've concluded that based on the devices that we had, when performing different encryption algorithms, the type of algorithms does not have any impact on power consumption, running 60 seconds of AES will consume the exact same amount of power as running 60 seconds of RC2, the only variable dependent is time. However, there could be some alternative assumption to be made here; there might be some algorithms/mode of operations that can only be run on a single core while others might be able to utilize all the cores and threads on a device, which could potentially change the power consumption for a fixed amount of run time on a device. Based on the latest information provided by reference [12], only CFB mode and CTR mode supports multithreaded encryption operations. 








*VI.	AREA OF FURTHER RESEARCH 


From reference[16] and [17] there already exist suitable lightweight cryptographic schemes for IoT applications so the next step in the project would be to either develop a new lightweight cryptographic algorithm that improves the performance, memory and resource consumption for various IoT devices discussed in the paper or to refine the cryptographic schemes that already exists.












**References:

[1]   Mangla, Neha, and Priya Rathod. Iosrjournals.Org, 2017,    http://www.iosrjournals.org/iosr-jce/papers/Vol19-issue4/Version-3/K1904036272.pdf.


[2]   Safi, Amirhossein. Waset.Org, 2017, https://waset.org/publications/10007094/improving-the-security-of-internet-of-things-using-encryption-algorithms.


[3] Patil, Pankaj Naganath. Irjet.Net, 2016, https://www.irjet.net/archives/V3/i6/IRJET-V3I6299.pdf.

[4] Nayyar, Anand and Puri, Vikram. 2019, https://www.researchgate.net/publication/302915457_A_Comprehensive_Review_of_BeagleBone_Technology_Smart_Board_Powered_by_ARM 15 July 2019.

[5] DAIGNEAU, MADELEINE, and MICHELLE ADVENA. Meseec.Ce.Rit.Edu, 2019, http://meseec.ce.rit.edu/551-projects/spring2015/2-3.pdf.


[6] Mushtaq, Muhammad Faheem et al. Thesai.Org, 2017, https://thesai.org/Downloads/Volume8No11/Paper_41-A_Survey_on_the_Cryptographic_Encryption_Algorithms.pdf.

[7] Hossain, Alam et al. 2016, https://www.researchgate.net/publication/317258631_Performance_Analysis_of_Different_Cryptography_Algorithms.

[8] Montelius, Johan. People.Kth.Se, 2019, https://people.kth.se/~johanmon/attic/2g1704/lectures/modes.pdf.

[9] Report on the Develoment of the Advanced Encryption Standard (AES)
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4863838/

[10 ]A Study of New Trends in Blowfish Algorithm, Gurjeevan Singh*, Ashwani Kumar**, K. S. Sandha***, 2014
https://pdfs.semanticscholar.org/639a/bf3bf480cb862bc4adf92c11cb2e1f618ba0.pdf


[11]A Study of Encryption Algor ithms (RSA, DES, 3DES and AES) for Information Security, Gurpreet Singh, Supriya, 2013
https://pdfs.semanticscholar.org/187d/26258dc57d794ce4badb094e64cf8d3f7d88.pdf

[12]Block Ciphers Modes of Operation | Cryptography | Crypto-IT. (2019). Retrieved 25 July 2019
 http://www.crypto-it.net/eng/theory/modes-of-block-ciphers.html

[13]COMPARISON BETWEEN DES , 3DES, RC2 , RC6 , BLOWFISH AND AES, MILIND MATHUR, AYUSH KESARWANI, 2013
https://pdfs.semanticscholar.org/e684/4c748d38997bf0de71cd7d05e58b09e310f6.pdf

[14]pycrypto. (2019). Retrieved 25 July 2019
https://pypi.org/project/pycrypto/

[15] Watt-hours (Wh) to mAh conversion calculator. (2019). Retrieved 25 July 2019
https://www.rapidtables.com/calc/electric/wh-to-mah-calculator.html

[16] Sehrawat, Deepti, and Nasib Singh Gill. Ripublication.Com, 2019, https://www.ripublication.com/ijaer18/ijaerv13n5_26.pdf.

[17] P, Nandhini, and Vanitha V. Pdfs.Semanticscholar.Org, 2019, https://pdfs.semanticscholar.org/c301/69e8924d2de92016be8013724a52a9b50abb.pdf.



**Appendix 



![](/images/2020-1-22-IOT/20.png)
![](/images/2020-1-22-IOT/21.png)
![](/images/2020-1-22-IOT/22.png)
![](/images/2020-1-22-IOT/23.png)
![](/images/2020-1-22-IOT/24.png)
![](/images/2020-1-22-IOT/25.png)
![](/images/2020-1-22-IOT/26.png)
![](/images/2020-1-22-IOT/27.png)
![](/images/2020-1-22-IOT/28.png)
![](/images/2020-1-22-IOT/29.png)







