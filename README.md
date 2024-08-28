# Recon-Attack-Analysis-and-Detection

## Project Overview

In this project, we focus on analyzing network traffic to identify and classify various types of attacks, with a particular emphasis on Reconnaissance Attacks and Benign Traffic. The dataset used for this analysis is a comprehensive collection of network traffic data that includes a wide range of features, such as protocol types, flag counts, and various traffic statistics.

Our primary goal is to develop a machine learning model that can accurately differentiate between benign traffic and reconnaissance attacks. By applying feature selection, encoding techniques, and filtering, we aim to enhance the model's performance and reduce computational complexity. This project is crucial for improving network security by enabling early detection of malicious activities, thus helping to prevent potential breaches and intrusions.

## Data Source

The data used in this project is sourced from the [IoT Dataset 2023](https://www.unb.ca/cic/datasets/iotdataset-2023.html), provided by the Canadian Institute for Cybersecurity (CIC). This dataset is specifically designed for cybersecurity research and includes a variety of attack scenarios and benign traffic data. The rich feature set and diverse attack types make it an ideal resource for developing and testing machine learning models for network intrusion detection.

## Dataset Overview
The dataset contains **445,755 records** with **47 features**. The features include:

- **flow_duration**
- **Header_Length**
- **Protocol Type**
- **Duration**
- **Rate**
- **Srate**
- **Drate**
- **fin_flag_number**
- **syn_flag_number**
- **rst_flag_number**
- **psh_flag_number**
- **ack_flag_number**
- **ece_flag_number**
- **cwr_flag_number**
- **ack_count**
- **syn_count**
- **fin_count**
- **urg_count**
- **rst_count**
- **HTTP**
- **HTTPS**
- **DNS**
- **Telnet**
- **SMTP**
- **SSH**
- **IRC**
- **TCP**
- **UDP**
- **DHCP**
- **ARP**
- **ICMP**
- **IPv**
- **LLC**
- **Tot sum**
- **Min**
- **Max**
- **AVG**
- **Std**
- **Tot size**
- **IAT**
- **Number**
- **Magnitue**
- **Radius**
- **Covariance**
- **Variance**
- **Weight**
- **label** (Output column, classifying records into different attack types or benign)

## Attack Categories and Types

### DDoS (Distributed Denial of Service) Attacks
- **DDoS-ICMP_Flood**
- **DDoS-RSTFINFlood**
- **DDoS-UDP_Flood**
- **DDoS-PSHACK_Flood**
- **DDoS-SynonymousIP_Flood**
- **DDoS-TCP_Flood**
- **DDoS-SYN_Flood**
- **DDoS-ACK_Fragmentation**
- **DDoS-ICMP_Fragmentation**
- **DDoS-UDP_Fragmentation**
- **DDoS-HTTP_Flood**
- **DDoS-SlowLoris**

### DoS (Denial of Service) Attacks
- **DoS-SYN_Flood**
- **DoS-UDP_Flood**
- **DoS-TCP_Flood**
- **DoS-HTTP_Flood**

### Reconnaissance Attacks
- **Recon-OSScan**
- **Recon-PortScan**
- **Recon-HostDiscovery**
- **Recon-PingSweep**
- **VulnerabilityScan**

### Mirai Malware Attacks
- **Mirai-greeth_flood**
- **Mirai-udpplain**
- **Mirai-greip_flood**

### Other Attack Types
- **DNS_Spoofing** (DNS Attack)
- **MITM-ArpSpoofing** (Man-in-the-Middle)
- **BrowserHijacking** (Hijacking web browsers)
- **DictionaryBruteForce** (Password brute force)
- **CommandInjection** (Injection attack)
- **XSS** (Cross-Site Scripting)
- **SqlInjection** (SQL Injection)
- **Backdoor_Malware** (Malware backdoor)
- **Uploading_Attack** (Uploading malicious content)

### Benign Traffic
- **BenignTraffic:** Normal network traffic without malicious activity.

## Focus: Reconnaissance Attacks Prediction

For our analysis, we are focusing on **Reconnaissance Attacks** and **Benign Traffic**. We filtered the records where the label column contains either `BenignTraffic` or any type of `Recon` attack. After filtering, the dataset shape is **(14,050, 47)**, meaning it has 14,050 records of benign and recon attacks only.

### Data Preparation
We removed columns with constant values, as these do not affect the model's output. The following features were removed:

- **Drate**
- **ece_flag_number**
- **cwr_flag_number**
- **Telnet**
- **SMTP**
- **SSH**
- **IRC**
- **DHCP**
- **ICMP**

After removing these features, the dataset shape is **(14,050, 38)**, representing 14,050 records with 38 features.

### Label Distribution
The label distribution after filtering is as follows:

- **BenignTraffic:** 10,507 records
- **Recon-HostDiscovery:** 1,310 records
- **Recon-OSScan:** 1,005 records
- **Recon-PortScan:** 813 records
- **VulnerabilityScan:** 387 records
- **Recon-PingSweep:** 28 records

### Label Encoding
We applied label encoding to map `BenignTraffic` to `0` and all types of `Recon` attacks to `1`, as shown below:

```python
label_mapping = {
    'BenignTraffic': 0,
    'Recon-OSScan': 1,
    'Recon-PortScan': 1,
    'VulnerabilityScan': 1,
    'Recon-HostDiscovery': 1,
    'Recon-PingSweep': 1,
}
```
## Conclusion

In this project, we successfully built and evaluated several machine learning models to classify network traffic into benign and reconnaissance attack categories. The models tested include K-Nearest Neighbors (KNN), Random Forest, Logistic Regression, and Decision Tree.

The accuracy of each model is as follows:

- **K-Nearest Neighbors (KNN):** 91%

- **Random Forest:** 96%
- **Logistic Regression:** 74%
- **Decision Tree:** 92%

Among these, the Random Forest model demonstrated the highest accuracy at 96%, making it the most effective for this classification task. This suggests that Random Forest’s ability to handle complex interactions between features and reduce overfitting through ensemble learning makes it particularly well-suited for detecting reconnaissance attacks in network traffic.

![Model Performance](https://github.com/user-attachments/assets/1460c08a-25df-4e8e-bd1c-65502155d693)


