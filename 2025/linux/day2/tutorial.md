# USERS & Groups

# SSH [Most Important]

# File Permission

# Day to Day Life scenario (Awk, grep, sed, find)

# Networking Commands [practice]

# Volume [Video assignment]

# Shell Script

##################################################################

# I have two servers A and B.

A server location: India (Chandigarh)

B server location: USA

But I want to connect A to B.

So how to resolve this issue?

# Solution

### SSH Protocol

When one Linux system connects to another via SSH, you need the following things:

1. Keys for port 22:

    a. Private key

    b. Public key

2. SSH client installed on the local machine

3. SSH server running on the remote machine

### Connecting to an Amazon EC2 Instance using SSH

1. **Identify the Instance**: Each EC2 instance has a unique Instance ID (e.g., `i-0179550827f3bc678`).

2. **Open SSH Client**: Launch an SSH client on your local machine.

3. **Locate Private Key**: Find your private key file (`key.pem`). Ensure it is secure:
    ```sh
    chmod 400 "key.pem"
    ```

4. **Connect to Instance**: Use the Public DNS to connect:
    ```sh
    ssh -i "key.pem" ubuntu@ec2-3-135-200-211.us-east-2.compute.amazonaws.com
    ```
    - `-i`: Specifies the identity file (private key).
    - `ubuntu`: Default username for the instance.

##########################################################################################################################################################

# Question: How to connect one EC2 instance to another EC2 instance?

### Diagram

  - **Bastion Host**: 

  I have  two server  like  demo-server-a ,  demo-server-b  , and i want to connect  demo-server-a to demo-server-b . so server a should have private key and demo-server-b should have public  key.

  ठीक है! चलिए मैं आपको **step-by-step commands** के साथ समझाता हूँ कि आपने क्या किया और यह कैसे काम करता है। यहाँ पूरी प्रक्रिया को समझाया गया है:

---

### Step 1: Home Directory में फाइल्स और फोल्डर्स की लिस्ट देखना
आपने `ls` कमांड का इस्तेमाल किया ताकि आप देख सकें कि आपके होम डायरेक्टरी (`/home/ubuntu`) में कौन-कौन सी फाइल्स और फोल्डर्स हैं।

```bash
ubuntu@ip-172-31-8-111:~$ ls
a  abcd  b  c  cd  d  devops  my-file.txt  newfolder
```

- **यहाँ क्या हुआ?**
  - `ls` कमांड ने आपको होम डायरेक्टरी में मौजूद फाइल्स और फोल्डर्स की लिस्ट दिखाई।
  - यहाँ `a`, `b`, `c`, `d`, `abcd`, `devops`, `my-file.txt`, और `newfolder` जैसी फाइल्स और फोल्डर्स हैं।

---

### Step 2: Hidden Files और Folders देखना
आपने `ls -a` कमांड का इस्तेमाल किया ताकि आप छुपी हुई (hidden) फाइल्स और फोल्डर्स को भी देख सकें।

```bash
ubuntu@ip-172-31-8-111:~$ ls -a
.   .bash_history  .bashrc  .lesshst    .profile  .test  abcd  c   d       my-file.txt
..  .bash_logout   .cache   .newfolder  .ssh      a      b     cd  devops  newfolder
```

- **यहाँ क्या हुआ?**
  - `ls -a` कमांड ने सभी फाइल्स और फोल्डर्स को दिखाया, जिनमें hidden फाइल्स भी शामिल हैं।
  - Hidden फाइल्स और फोल्डर्स नाम में `.` (डॉट) से शुरू होते हैं, जैसे `.bashrc`, `.ssh`, आदि।

---

### Step 3: `.ssh` Directory में जाना
आपने `.ssh` डायरेक्टरी में जाने के लिए `cd .ssh` कमांड का इस्तेमाल किया।

```bash
ubuntu@ip-172-31-8-111:~$ cd .ssh
```

- **यहाँ क्या हुआ?**
  - `cd .ssh` कमांड ने आपको `/home/ubuntu/.ssh` डायरेक्टरी में ले जाया।
  - `.ssh` डायरेक्टरी SSH keys और configuration files को स्टोर करने के लिए इस्तेमाल होती है।

---

### Step 4: `.ssh` Directory की Contents देखना
आपने `.ssh` डायरेक्टरी में मौजूद फाइल्स को देखने के लिए `ls` कमांड का इस्तेमाल किया।

```bash
ubuntu@ip-172-31-8-111:~/.ssh$ ls
authorized_keys
```

- **यहाँ क्या हुआ?**
  - `ls` कमांड ने `.ssh` डायरेक्टरी में मौजूद फाइल्स की लिस्ट दिखाई।
  - यहाँ सिर्फ `authorized_keys` फाइल है, जो SSH public keys को स्टोर करती है।

---

### Step 5: Current Directory का Path देखना
आपने `pwd` कमांड का इस्तेमाल किया ताकि आप देख सकें कि आप किस डायरेक्टरी में हैं।

```bash
ubuntu@ip-172-31-8-111:~/.ssh$ pwd
/home/ubuntu/.ssh
```

- **यहाँ क्या हुआ?**
  - `pwd` कमांड ने आपको बताया कि आप `/home/ubuntu/.ssh` डायरेक्टरी में हैं।

---

### Step 6: SSH Key Generate करना
आपने `ssh-keygen` कमांड का इस्तेमाल करके एक नई SSH key generate की।

```bash
ubuntu@ip-172-31-8-111:~/.ssh$ ssh-keygen
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/ubuntu/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ubuntu/.ssh/id_ed25519
Your public key has been saved in /home/ubuntu/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:hafgEhOmAPlVLz0tveKckBUftQ1Xc0ZZsHFcjpNzIoQ ubuntu@ip-172-31-8-111
The key's randomart image is:
+--[ED25519 256]--+
|+.  o.. . .o+ +*%|
|.. o.. o *Eo = X+|
| ...o o B * o O o|
|  .  + = * . . = |
|    . + S .      |
|     . + o       |
|        +        |
|                 |
|                 |
+----[SHA256]-----+
```

- **यहाँ क्या हुआ?**
  - `ssh-keygen` कमांड ने एक नई SSH key pair generate की।
  - यह key pair दो फाइल्स में स्टोर हुआ:
    1. **Private Key**: `/home/ubuntu/.ssh/id_ed25519`
    2. **Public Key**: `/home/ubuntu/.ssh/id_ed25519.pub`
  - आपने passphrase डालने का ऑप्शन छोड़ दिया (empty passphrase), जिसका मतलब है कि आपको key इस्तेमाल करते समय कोई पासवर्ड नहीं डालना पड़ेगा।

---

### Step 7: नई SSH Keys की जाँच करना
आपने `ls` कमांड का इस्तेमाल करके यह देखा कि नई SSH keys बन गई हैं।

```bash
ubuntu@ip-172-31-8-111:~/.ssh$ ls
authorized_keys  id_ed25519  id_ed25519.pub
```

- **यहाँ क्या हुआ?**
  - `ls` कमांड ने दिखाया कि `.ssh` डायरेक्टरी में अब तीन फाइल्स हैं:
    1. `authorized_keys`
    2. `id_ed25519` (private key)
    3. `id_ed25519.pub` (public key)

---

### Step 8: Private Key की Content देखना
आपने `cat` कमांड का इस्तेमाल करके `id_ed25519` (private key) की content देखी।

```bash
ubuntu@ip-172-31-8-111:~/.ssh$ cat id_ed25519
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACAk6b4u5N38CcHL6idjcpmWwEVNy5IBUN5rmYXPVikvkAAAAKAEbDxoBGw8
aAAAAAtzc2gtZWQyNTUxOQAAACAk6b4u5N38CcHL6idjcpmWwEVNy5IBUN5rmYXPVikvkA
AAAEAhaEwm0MezvWEY1b+2EYDAcyyLEhjxHh43/19usd8vayTpvi7k3fwJwcvqJ2NymZbA
RU3LkgFQ3muZhc9WKS+QAAAAFnVidW50dUBpcC0xNzItMzEtOC0xMTEBAgMEBQYH
-----END OPENSSH PRIVATE KEY-----
```

- **यहाँ क्या हुआ?**
  - `cat` कमांड ने `id_ed25519` फाइल की content दिखाई।
  - यह content आपकी private key है, जिसे कभी किसी के साथ share नहीं करना चाहिए।

---

### अगले Steps:
1. **Public Key को Remote Server पर Add करना**:
   - अगर आप इस key का इस्तेमाल किसी remote server पर SSH करने के लिए करना चाहते हैं, तो `id_ed25519.pub` की content को remote server के `~/.ssh/authorized_keys` फाइल में add करें।
   - उदाहरण:
     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```
     फिर इस output को remote server के `~/.ssh/authorized_keys` फाइल में paste करें।

2. **SSH का इस्तेमाल करना**:
   - अब आप इस key का इस्तेमाल करके remote server पर SSH कर सकते हैं:
     ```bash
     ssh -i ~/.ssh/id_ed25519 user@remote-server-ip
     ```

---

आपने SSH का उपयोग करके एक remote server (`3.145.199.152`) से कनेक्ट किया है, और यहाँ पर कुछ महत्वपूर्ण बातें हुई हैं। चलिए इसे step-by-step समझते हैं:

---

### Step 1: SSH Command का इस्तेमाल
आपने निम्नलिखित कमांड का इस्तेमाल किया:
```bash
ssh -i id_ed25519 ubuntu@3.145.199.152
```

- **यहाँ क्या हुआ?**
  - `ssh -i id_ed25519`: यह आपकी private key (`id_ed25519`) का इस्तेमाल करके SSH कनेक्शन बनाने के लिए है।
  - `ubuntu@3.145.199.152`: यह remote server का IP address और username (`ubuntu`) है।

---

### Step 2: Warning - Identity File Not Found
```bash
Warning: Identity file id_ed25519 not accessible: No such file or directory.
```

- **यहाँ क्या हुआ?**
  - SSH क्लाइंट को `id_ed25519` फाइल नहीं मिली, क्योंकि यह फाइल current directory (`~`) में मौजूद नहीं है।
  - SSH key फाइल (`id_ed25519`) आपके `.ssh` डायरेक्टरी (`/home/ubuntu/.ssh/id_ed25519`) में है, लेकिन आपने सही path नहीं दिया।

---

### Step 3: Server का Fingerprint Verify करना
```bash
The authenticity of host '3.145.199.152 (3.145.199.152)' can't be established.
ED25519 key fingerprint is SHA256:SFy50qVIfq0g22ZmZ/QY/9G/e4FUUlxgHsfntVhXIDc.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

- **यहाँ क्या हुआ?**
  - यह पहली बार है जब आप इस server से कनेक्ट हो रहे हैं, इसलिए SSH क्लाइंट server के fingerprint को verify कर रहा है।
  - आपने `yes` टाइप करके server के fingerprint को accept किया है।
  - यह fingerprint आपके local machine के `~/.ssh/known_hosts` फाइल में save हो गया है।

---

### Step 4: Successful Connection
```bash
Warning: Permanently added '3.145.199.152' (ED25519) to the list of known hosts.
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-1021-aws x86_64)
```

- **यहाँ क्या हुआ?**
  - SSH कनेक्शन सफलतापूर्वक बन गया है।
  - आप अब remote server पर logged in हैं।

---

### Step 5: Remote Server पर Files की लिस्ट देखना
आपने `ls` कमांड का इस्तेमाल करके remote server पर मौजूद फाइल्स की लिस्ट देखी।

```bash
ubuntu@ip-172-31-3-95:~$ ls
new-file.txt
```

- **यहाँ क्या हुआ?**
  - `ls` कमांड ने remote server के होम डायरेक्टरी (`/home/ubuntu`) में मौजूद फाइल्स की लिस्ट दिखाई।
  - यहाँ सिर्फ एक फाइल (`new-file.txt`) है।

---

### समस्या का समाधान (Identity File Not Found)
आपको `id_ed25519` फाइल नहीं मिली क्योंकि आपने सही path नहीं दिया। इसे ठीक करने के लिए निम्नलिखित कदम उठाएँ:

1. **सही Path दें**:
   - `id_ed25519` फाइल आपके `.ssh` डायरेक्टरी में है, इसलिए आपको पूरा path देना चाहिए।
   - उदाहरण:
     ```bash
     ssh -i ~/.ssh/id_ed25519 ubuntu@3.145.199.152
     ```

2. **Permissions Check करें**:
   - SSH key फाइल्स की permissions सही होनी चाहिए। निम्नलिखित कमांड्स चलाएँ:
     ```bash
     chmod 600 ~/.ssh/id_ed25519
     chmod 644 ~/.ssh/id_ed25519.pub
     ```

3. **Public Key को Remote Server पर Add करें**:
   - अगर आपने `id_ed25519.pub` को remote server के `~/.ssh/authorized_keys` फाइल में add नहीं किया है, तो ऐसा करें:
     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```
     फिर इस output को remote server के `~/.ssh/authorized_keys` फाइल में paste करें।

---

### अगले Steps:
1. **फाइल्स और डायरेक्टरीज Manage करना**:
   - अब आप remote server पर फाइल्स और डायरेक्टरीज create, edit, delete कर सकते हैं।
   - उदाहरण:
     ```bash
     touch newfile.txt          # नई फाइल बनाएँ
     mkdir newfolder            # नया फोल्डर बनाएँ
     nano newfile.txt           # फाइल edit करें
     ```

2. **SSH Connection बंद करना**:
   - SSH session को बंद करने के लिए `exit` कमांड का इस्तेमाल करें:
     ```bash
     exit
     ```

---

==========================================================================================================================================================

#  Now copy file from one servert tp another servet ec2


### **EC2 सर्वर A से सर्वर B पर फाइल ट्रांसफर कैसे करें?**  
अगर आपके पास **दो EC2 सर्वर** हैं (जैसे कि **Server A (India)** और **Server B (USA)**) और आप Server A से Server B पर फाइल कॉपी करना चाहते हैं, तो **SCP (Secure Copy Protocol)** का उपयोग करें।

---

## **चरण 1: SSH एक्सेस को सक्षम करें (Authentication सेट करें)**  
#### **1. Server A पर SSH Key बनाएं**  
अगर आपके पास पहले से SSH Key नहीं है, तो इसे जनरेट करें:
```bash
ssh-keygen -t ed25519
```
यह दो फाइलें बनाएगा:
- **प्राइवेट की** → `/home/ubuntu/.ssh/id_ed25519`
- **पब्लिक की** → `/home/ubuntu/.ssh/id_ed25519.pub`

#### **2. पब्लिक की को Server B पर कॉपी करें**  
ताकि Server A, Server B से कनेक्ट हो सके, हमें **पब्लिक की** को Server B में जोड़ना होगा।  
इसके लिए यह कमांड चलाएं:
```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub ubuntu@<server-b-ip>
```
अगर `ssh-copy-id` काम नहीं कर रहा है, तो मैन्युअली की को **Server B** के `~/.ssh/authorized_keys` में जोड़ें:
```bash
cat ~/.ssh/id_ed25519.pub | ssh ubuntu@<server-b-ip> "cat >> ~/.ssh/authorized_keys"
```
अब, Server A से Server B पर SSH लॉगिन करना आसान हो जाएगा।

#### **3. SSH कनेक्शन को टेस्ट करें**
अब जांचें कि Server A से Server B पर SSH कनेक्शन बन रहा है या नहीं:
```bash
ssh ubuntu@<server-b-ip>
```
अगर आप बिना पासवर्ड डाले लॉगिन कर सकते हैं, तो SSH सही से सेटअप हो गया है। ✅

---

## **चरण 2: SCP का उपयोग करके फाइल ट्रांसफर करें**

### **A. एकल फाइल कॉपी करें**
```bash
scp -i ~/.ssh/id_ed25519 /path/to/file ubuntu@<server-b-ip>:/path/to/destination/
```
**उदाहरण:**  
अगर आप Server A से `my-file.txt` को Server B के `/home/ubuntu/` में कॉपी करना चाहते हैं, तो:
```bash
scp -i ~/.ssh/id_ed25519 ~/my-file.txt ubuntu@<server-b-ip>:/home/ubuntu/
```

---

### **B. पूरी डायरेक्ट्री कॉपी करें**
अगर आप पूरी डायरेक्ट्री ट्रांसफर करना चाहते हैं, तो `-r` (recursive) ऑप्शन का उपयोग करें:
```bash
scp -i ~/.ssh/id_ed25519 -r /path/to/directory ubuntu@<server-b-ip>:/path/to/destination/
```
**उदाहरण:**  
अगर आप Server A की `newfolder` को Server B पर `/home/ubuntu/` में कॉपी करना चाहते हैं:
```bash
scp -i ~/.ssh/id_ed25519 -r ~/newfolder ubuntu@<server-b-ip>:/home/ubuntu/
```

---

### **C. Server B से Server A पर फाइल कॉपी करें**
अगर आपको **उल्टा ट्रांसफर** करना है (यानि Server B से Server A पर फाइल कॉपी करनी है), तो:
```bash
scp -i ~/.ssh/id_ed25519 ubuntu@<server-b-ip>:/path/to/file /path/to/destination/
```
**उदाहरण:**  
अगर आप Server B से `backup.tar.gz` को Server A पर `/home/ubuntu/` में कॉपी करना चाहते हैं:
```bash
scp -i ~/.ssh/id_ed25519 ubuntu@<server-b-ip>:/home/ubuntu/backup.tar.gz ~/backup.tar.gz
```

---

### **D. Bastion Host के माध्यम से फाइल कॉपी करें (अगर डायरेक्ट एक्सेस नहीं है)**
अगर Server A **डायरेक्ट** Server B से कनेक्ट नहीं हो सकता है और **Bastion Host** (एक बीच का सर्वर) के जरिए कनेक्ट करना है, तो:
```bash
scp -i ~/.ssh/id_ed25519 -o ProxyJump ubuntu@bastion-ip /path/to/file ubuntu@server-b-ip:/path/to/destination/
```

---

## **चरण 3: फाइल ट्रांसफर को वेरिफाई करें**
अब **Server B** पर लॉगिन करें और यह चेक करें कि फाइल सही से कॉपी हुई या नहीं:
```bash
ssh ubuntu@<server-b-ip>
ls -l /home/ubuntu/
```
अगर फाइल दिख रही है, तो आपका ट्रांसफर **सफलतापूर्वक हो गया है!** 🎉

---

## **निष्कर्ष**
🔹 **SSH Key Setup करें** (Server A से Server B पर कनेक्ट करने के लिए)  
🔹 **SCP का उपयोग करें** (`scp -i id_ed25519 source destination`)  
🔹 **सफलता को वेरिफाई करें** (`ls -l`)  

अब आप अपने दो EC2 सर्वरों के बीच आसानी से फाइल ट्रांसफर कर सकते हैं! 🚀  
==========================================================================================================================================================

## **Linux में यूज़र्स और ग्रुप्स को मैनेज करना (Step-by-Step Guide in Hindi)**

आपने Linux सिस्टम में **यूज़र और ग्रुप्स** को मैनेज करने के लिए कुछ कमांड्स का उपयोग किया है। चलिए इन कमांड्स को **स्टेप बाय स्टेप** समझते हैं।

---

## **1. `ls -l` कमांड से फाइल लिस्टिंग**  
```bash
ubuntu@ip-172-31-3-95:~$ ls -l
```
👉 यह कमांड आपके होम डायरेक्टरी की फाइल्स और उनकी **permissions** दिखाती है।

उदाहरण आउटपुट:
```
total 4
-rw-rw-r-- 1 ubuntu ubuntu 17 Feb  9 16:20 new-file.txt
```
📌 **मतलब:** `new-file.txt` फाइल `ubuntu` यूज़र और `ubuntu` ग्रुप के स्वामित्व में है।

---

## **2. नया यूज़र (`dholu`) बनाना**
```bash
sudo useradd -m dholu
```
🔹 **`useradd`** कमांड का उपयोग नया यूज़र बनाने के लिए किया जाता है।  
🔹 **`-m`** ऑप्शन से **होम डायरेक्टरी** भी बन जाती है (`/home/dholu`)।

---

## **3. यूज़र डिलीट करना (`userdel`)**
```bash
sudo userdel dholu
```
📌 **मतलब:** `dholu` यूज़र को हटा दिया गया।  
⚠ **अगर होम डायरेक्टरी को भी हटाना हो, तो यह कमांड चलाएँ:**
```bash
sudo userdel -r dholu
```

---

## **4. `/etc/passwd` फ़ाइल देखना**  
```bash
cat /etc/passwd
```
📌 **मतलब:** `/etc/passwd` फाइल में **सभी यूज़र्स** की जानकारी होती है।  
👉 जब हमने `userdel` कमांड चलाई, तो `dholu` यूज़र हटा दिया गया था, लेकिन `/home/dholu/` डायरेक्टरी अभी भी मौजूद थी।

---

## **5. फिर से `dholu` यूज़र बनाना**  
```bash
sudo useradd -m dholu
```
⚠ **Warning:**  
```
useradd: warning: the home directory /home/dholu already exists.
```
🔹 यह मैसेज बता रहा है कि `/home/dholu` डायरेक्टरी पहले से मौजूद है, इसलिए नया होम डायरेक्टरी नहीं बनाया जाएगा।  
🔹 यह **कोई एरर नहीं है**, सिर्फ़ एक वार्निंग है।

---

## **6. नया ग्रुप बनाना (`groupadd`)**
```bash
sudo groupadd devops
```
📌 **मतलब:** `devops` नाम का एक नया ग्रुप बनाया गया।

---

## **7. `/etc/group` फाइल देखना**
```bash
cat /etc/group
```
📌 **मतलब:** `/etc/group` फ़ाइल में **सभी ग्रुप्स और उनके यूज़र्स** की जानकारी होती है।  
🔹 यहाँ `devops` ग्रुप भी दिखाई देगा:
```
devops:x:1002:
```

---

## **8. `gpasswd` से यूज़र को ग्रुप में जोड़ना**
```bash
sudo gpasswd -M dholu devops
```
📌 **मतलब:**  
🔹 `dholu` यूज़र को `devops` ग्रुप में जोड़ा गया।  
🔹 `-M` ऑप्शन का उपयोग करके **एक से अधिक यूज़र्स** को जोड़ सकते हैं।

---

## **9. `usermod` से यूज़र को ग्रुप में ऐड करना**
```bash
sudo usermod -aG devops dholu
```
📌 **मतलब:** `dholu` यूज़र को `devops` ग्रुप में जोड़ दिया गया।  
👉 `-aG` ऑप्शन से **यूज़र के पुराने ग्रुप्स भी सुरक्षित रहते हैं**।  
⚠ **अगर `-aG` की बजाय `-G` उपयोग करते, तो पुराने ग्रुप्स हट जाते!**

---

## **10. ग्रुप वेरिफाई करना**  
अब चेक करें कि `dholu` किस-किस ग्रुप में है:
```bash
groups dholu
```
अगर आउटपुट में `devops` आ रहा है, तो यूज़र सफलतापूर्वक जोड़ दिया गया।

---

## **निष्कर्ष (Summary)**  
✅ `useradd` से नया यूज़र बनाया।  
✅ `userdel` से यूज़र हटाया।  
✅ `groupadd` से नया ग्रुप (`devops`) बनाया।  
✅ `gpasswd` और `usermod` से यूज़र को ग्रुप में जोड़ा।  
✅ `/etc/passwd` और `/etc/group` से सभी यूज़र्स और ग्रुप्स को देखा।  

🎯 **अब `dholu` यूज़र `devops` ग्रुप का हिस्सा है और सिस्टम को एक्सेस कर सकता है!** 🚀

==========================================================================================================================================================

## **Linux में डायरेक्टरी और फाइल परमिशन्स समझें (Step-by-Step in Hindi)**

### **1. `ls -l` कमांड से फाइल और डायरेक्टरी की जानकारी देखना**
आपने निम्नलिखित कमांड चलाई:
```bash
ubuntu@ip-172-31-3-95:~$ ls -l
```
👉 यह **सभी फाइल्स और डायरेक्ट्रीज़ की डिटेल्स** दिखाता है।

#### **आउटपुट:**
```
total 8
-rw-rw-r-- 1 ubuntu ubuntu   17 Feb  9 16:20 new-file.txt
drwxrwxr-x 2 ubuntu ubuntu 4096 Feb  9 16:56 server2devops
```

---

## **2. फ़ाइल और डायरेक्टरी के परमिशन्स का अर्थ**
प्रत्येक लाइन का मतलब समझते हैं:

### **(A) `new-file.txt` फ़ाइल:**
```
-rw-rw-r-- 1 ubuntu ubuntu   17 Feb  9 16:20 new-file.txt
```
🔹 **पहला भाग (`-rw-rw-r--`)** → फाइल की परमिशन्स  
🔹 **`1`** → हार्ड लिंक की संख्या  
🔹 **`ubuntu ubuntu`** → ओनर (यूज़र) और ग्रुप  
🔹 **`17`** → फाइल साइज़ (Bytes में)  
🔹 **`Feb 9 16:20`** → फाइल का आखिरी मॉडिफिकेशन टाइम  
🔹 **`new-file.txt`** → फाइल का नाम  

✅ **फाइल परमिशन्स (`-rw-rw-r--`) का मतलब:**  
| Permission | Owner (ubuntu) | Group (ubuntu) | Others |
|------------|---------------|----------------|--------|
| Read (`r`) | ✅ | ✅ | ✅ |
| Write (`w`) | ✅ | ✅ | ❌ |
| Execute (`x`) | ❌ | ❌ | ❌ |

📌 **निष्कर्ष:**  
- ओनर (`ubuntu`) और ग्रुप (`ubuntu`) को **read (r)** और **write (w)** की अनुमति है।  
- अन्य यूज़र्स (`others`) को **सिर्फ़ read (r)** की अनुमति है।  
- कोई भी इसे **execute** नहीं कर सकता।

---

### **(B) `server2devops` डायरेक्टरी:**
```
drwxrwxr-x 2 ubuntu ubuntu 4096 Feb  9 16:56 server2devops
```
🔹 **पहला भाग (`drwxrwxr-x`)** → डायरेक्टरी की परमिशन्स  
🔹 **`d`** → दर्शाता है कि यह एक **डायरेक्टरी** है।  
🔹 **`2`** → हार्ड लिंक की संख्या  
🔹 **`ubuntu ubuntu`** → ओनर (यूज़र) और ग्रुप  
🔹 **`4096`** → डायरेक्टरी का साइज़ (Bytes में)  
🔹 **`Feb 9 16:56`** → आखिरी मॉडिफिकेशन टाइम  
🔹 **`server2devops`** → डायरेक्टरी का नाम  

✅ **डायरेक्टरी परमिशन्स (`drwxrwxr-x`) का मतलब:**  
| Permission | Owner (ubuntu) | Group (ubuntu) | Others |
|------------|---------------|----------------|--------|
| Read (`r`) | ✅ | ✅ | ✅ |
| Write (`w`) | ✅ | ✅ | ❌ |
| Execute (`x`) | ✅ | ✅ | ✅ |

📌 **निष्कर्ष:**  
- **ओनर (`ubuntu`) और ग्रुप (`ubuntu`) को `read (r)`, `write (w)`, और `execute (x)` की अनुमति है।**  
- **अन्य (`others`) को `read (r)` और `execute (x)` की अनुमति है, लेकिन `write (w)` नहीं।**  
- कोई भी **डायरेक्टरी को देख सकता है और खोल सकता है, लेकिन अन्य यूज़र्स इसमें फाइल एडिट या डिलीट नहीं कर सकते।**

---

## **3. फाइल और डायरेक्टरी परमिशन्स को बदलना (`chmod`)**
#### **(A) फाइल को executable (`x`) बनाने के लिए:**
```bash
chmod +x new-file.txt
```
अब चेक करें:
```bash
ls -l
```
नया आउटपुट:
```
-rwxrwxr-- 1 ubuntu ubuntu 17 Feb  9 16:20 new-file.txt
```
📌 अब **फाइल executable हो गई है।**

---

#### **(B) किसी भी यूज़र को फाइल से लिखने की अनुमति हटाने के लिए:**
```bash
chmod a-w new-file.txt
```
👉 अब **कोई भी इस फाइल में एडिट नहीं कर सकता।**

---

#### **(C) `server2devops` डायरेक्टरी को पूरी तरह से लॉक करने के लिए:**
```bash
chmod 700 server2devops
```
👉 अब सिर्फ़ **ओनर (ubuntu)** ही इस डायरेक्टरी को देख सकता है।

---

## **4. फाइल और डायरेक्टरी के ओनर को बदलना (`chown`)**
#### **(A) फाइल का ओनर बदलना:**
```bash
sudo chown newuser:newgroup new-file.txt
```
👉 `new-file.txt` का **ओनर और ग्रुप बदलकर** `newuser:newgroup` कर दिया जाएगा।

---

#### **(B) डायरेक्टरी का ओनर बदलना:**
```bash
sudo chown -R newuser:newgroup server2devops
```
📌 **अब `server2devops` डायरेक्टरी और उसके अंदर की सभी फाइल्स का ओनर `newuser:newgroup` हो जाएगा।**  

---

## **5. किसी भी फ़ाइल या डायरेक्टरी को खोजना (`find` command)**
#### **(A) पूरे सिस्टम में `new-file.txt` खोजने के लिए:**
```bash
find / -name "new-file.txt"
```
👉 `/` का मतलब **पूरा सिस्टम** स्कैन करेगा।

#### **(B) 7 दिनों से पुराने `.log` फाइल्स को `/var/log/` में खोजना:**
```bash
find /var/log/ -name "*.log" -mtime +7
```
👉 इससे **7 दिनों से पुराने `.log` फाइल्स** मिलेंगे।

---

## **6. ग्रुप्स मैनेज करना (`usermod`)**
#### **(A) `dholu` यूज़र को `devops` ग्रुप में जोड़ने के लिए:**
```bash
sudo usermod -aG devops dholu
```
📌 अब `dholu` को `devops` ग्रुप में एक्सेस मिल जाएगा।

#### **(B) ग्रुप को वेरिफाई करने के लिए:**
```bash
groups dholu
```
👉 आउटपुट:
```
dholu : dholu devops
```
📌 **मतलब `dholu` अब `devops` ग्रुप का हिस्सा है।**

---

## **निष्कर्ष (Summary)**
✅ **फाइल और डायरेक्टरी के परमिशन्स (`ls -l`) को समझा।**  
✅ **`chmod` से फाइल्स और डायरेक्टरी की परमिशन्स बदली।**  
✅ **`chown` से ओनर और ग्रुप बदला।**  
✅ **`find` से फाइल्स को खोजा।**  
✅ **`usermod` से यूज़र को ग्रुप में जोड़ा।**  

🎯 **अब आपको फाइल परमिशन और यूज़र मैनेजमेंट का पूरा ज्ञान हो गया है!** 🚀  
==========================================================================================================================================================