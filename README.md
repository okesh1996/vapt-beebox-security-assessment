<h1>VAPT-Beebox-Security-Assessment</h1>


<h2>1. Introduction</h2>


This project presents a practical Vulnerability Assessment and Penetration Testing (VAPT) exercise performed on the vulnerable Bee-Box environment. The assessment was conducted in a controlled laboratory setup to identify security weaknesses in exposed network services and demonstrate their potential security impact.

The project covers the setup of the Bee-Box virtual machine, network and service scanning using Nmap, service enumeration using Metasploit, FTP security assessment, and remediation of anonymous FTP access.

The assessment follows a practical security workflow covering environment setup, reconnaissance, vulnerability identification, exploitation, remediation, and verification.
<br />


<h2>2. Objective</h2>

The objective of this project is to perform a vulnerability assessment and penetration testing exercise on a vulnerable Bee-Box environment to identify, assess, and remediate security weaknesses.

The project focuses on:

- <p>Setting up and configuring the Bee-Box vulnerable environment.  <br /> 
- <p>Scanning the target system to identify open ports and running services.  <br /> 
- <p>Performing service enumeration using Metasploit.  <br /> 
- <p>Assessing the security of the FTP service.  <br /> 
- <p>Testing anonymous FTP access and weak credentials in the controlled lab environment.  <br /> 
- <p>Identifying the security risk associated with unauthorized FTP access.  <br /> 
- <p>Disabling anonymous FTP access as a remediation measure.  <br /> 
- <p>Verifying that unauthorized anonymous FTP access is no longer permitted.  <br /> 

The overall objective is to understand the practical VAPT lifecycle from reconnaissance and vulnerability identification through exploitation and remediation verification.
<br />


<h2>3. Lab Environment</h2>

<p>The project was performed in a virtualized laboratory environment using VirtualBox.</p>

<h3>Target Machine</h3>

<ul>
  <li>Machine: Bee-Box</li>
  <li>Operating System: Bee-Box / vulnerable Linux environment</li>
  <li>Purpose: Vulnerable target for security assessment</li>
</ul>

<h3>Security Testing Machine</h3>

<ul>
  <li>Machine: Kali Linux</li>
  <li>Purpose: Vulnerability scanning, enumeration, and security testing</li>
</ul>

<h3>Network Configuration</h3>

<p>The Bee-Box and Kali Linux virtual machines were configured to communicate through a <strong>NAT Network</strong> in VirtualBox.</p>

<p>The Bee-Box IP address was identified during the lab and used as the target for subsequent scanning and testing activities.</p>

<h2>4. Tools and Technologies</h2>

<p>The following tools and technologies were used during the project:</p>

<table>
  <thead>
    <tr>
      <th>Tool / Technology</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Kali Linux</td>
      <td>Security testing environment</td>
    </tr>
    <tr>
      <td>Bee-Box</td>
      <td>Vulnerable target environment</td>
    </tr>
    <tr>
      <td>VirtualBox</td>
      <td>Virtual lab environment</td>
    </tr>
    <tr>
      <td>Nmap</td>
      <td>Network and service scanning</td>
    </tr>
    <tr>
      <td>Metasploit Framework</td>
      <td>Service enumeration</td>
    </tr>
    <tr>
      <td>Hydra</td>
      <td>FTP credential testing</td>
    </tr>
    <tr>
      <td>FTP</td>
      <td>FTP service assessment</td>
    </tr>
    <tr>
      <td>ProFTPD</td>
      <td>FTP server configuration and remediation</td>
    </tr>
    <tr>
      <td>Linux Terminal</td>
      <td>Security testing and configuration</td>
    </tr>
    <tr>
      <td>p7zip</td>
      <td>Extraction of the Bee-Box image</td>
    </tr>
  </tbody>
</table>

<p>The project documentation specifically uses Nmap for TCP and service scanning, Metasploit for SMTP enumeration, Hydra for FTP credential testing, and ProFTPD configuration for remediation.</p>


<h2>5. Assessment Methodology</h2>

<p>The assessment was performed in the following sequence:</p>

<ol>
  <li>Set up the Bee-Box vulnerable machine.</li>
  <li>Configure the virtual network between Bee-Box and Kali Linux.</li>
  <li>Identify the target IP address.</li>
  <li>Perform network and service discovery using Nmap.</li>
  <li>Perform service enumeration using Metasploit.</li>
  <li>Assess the FTP service.</li>
  <li>Test FTP authentication using a controlled credential list.</li>
  <li>Verify FTP access.</li>
  <li>Identify the anonymous FTP access issue.</li>
  <li>Modify the ProFTPD configuration to restrict anonymous access.</li>
  <li>Restart the FTP service.</li>
  <li>Verify that anonymous FTP login is no longer permitted.</li>
</ol>

<p>This methodology follows the sequence documented in the course-end project.</p>


<hr>

<h2>6. Project Workflow</h2>

<pre>
Bee-Box Setup
      ↓
Network Configuration
      ↓
Target IP Identification
      ↓
Nmap Scanning
      ↓
Service Enumeration
      ↓
FTP Security Assessment
      ↓
Credential Testing
      ↓
Unauthorized Access Identification
      ↓
FTP Configuration Remediation
      ↓
Service Restart
      ↓
Remediation Verification
</pre>

<p>The project therefore demonstrates the progression from identifying exposed services to validating and remediating a specific FTP security weakness.</p>


<h2>Step 1 — Bee-Box Setup</h2>

<p>The first phase involved downloading and setting up the Bee-Box vulnerable machine.</p>

<p>The Bee-Box image was downloaded and extracted using <code>p7zip</code>. The extracted virtual disk was then added to VirtualBox as an existing virtual hard disk.</p>

<p>The Bee-Box virtual machine was configured with:</p>

<ul>
  <li>Linux operating system type</li>
  <li>Ubuntu 32-bit configuration</li>
  <li>Existing Bee-Box virtual disk</li>
  <li>NAT Network connectivity</li>
</ul>

<p>The machine was then started and its network configuration was checked to identify its IP address.</p>

<h3>Result</h3>

<p>The Bee-Box environment was successfully prepared as the target machine for the subsequent security assessment.</p>


<h2>Step 2 — Vulnerability Scanning</h2>

<p>After setting up the target, Kali Linux was configured on the same NAT Network.</p>

<p>Connectivity between Kali Linux and Bee-Box was verified using <code>ping</code>.</p>

<p>Nmap was then used to identify open ports and running services.</p>

<p>The project used the following scanning approach:</p>

<pre>
Nmap TCP SYN Scan
        +
Service Version Detection
        +
Targeted Port Scanning
</pre>

<p>The documented Nmap scan used <code>-Pn</code>, <code>-sS</code>, and <code>-sV</code> options to perform TCP SYN scanning and service/version identification.</p>

<p>Targeted scans were also performed against ports including <strong>25 (SMTP)</strong> and <strong>21 (FTP)</strong>.</p>

<h3>Result</h3>

<p>The scanning phase provided information about the services exposed by the Bee-Box system and identified services requiring further assessment.</p>


<h2>Step 3 — Service Enumeration with Metasploit</h2>

<p>The Metasploit Framework was installed and launched on Kali Linux.</p>

<p>The project used Metasploit to search for and enumerate SMTP-related functionality.</p>

<p>The documented workflow included:</p>

<pre>
Launch Metasploit
      ↓
Search SMTP
      ↓
Use SMTP Enumeration Module
      ↓
View Module Options
      ↓
Configure RHOSTS
      ↓
Configure THREADS
      ↓
Execute Enumeration
</pre>

<p>The <code>smtp_enum</code> auxiliary scanner was used to enumerate available SMTP user accounts on the target.</p>

<p>The resulting usernames were collected for subsequent testing activities.</p>

<h3>Result</h3>

<p>The enumeration phase provided usernames that were subsequently organized into a username list for the FTP security assessment.</p>


<h2>Step 4 — FTP Security Assessment</h2>

<p>The next phase focused on assessing the FTP service running on the Bee-Box system.</p>

<p>A username file and password file were created for controlled credential testing.</p>

<p>Hydra was installed and used to test FTP authentication against the target.</p>

<p>The documented command used the FTP service together with the username and password lists to identify valid credentials in the controlled lab environment.</p>

<p>After obtaining valid FTP access, the FTP service was accessed and the available files were listed.</p>

<p>The project documentation also demonstrated anonymous FTP access using:</p>

<pre>
Username: ftp
Password: bin
</pre>

<p>The FTP connection was then terminated after verifying access.</p>

<h3>Security Finding</h3>

<p>The assessment demonstrated that the FTP configuration permitted anonymous access, creating a potential unauthorized-access risk.</p>


<h2>Step 5 — Remediation: Disable Anonymous FTP</h2>

<p>After identifying the anonymous FTP access issue, the project implemented a remediation step on the Bee-Box machine.</p>

<p>The ProFTPD configuration file was opened and the relevant anonymous FTP configuration sections were disabled.</p>

<p>The configuration was then saved and the ProFTPD service was restarted.</p>

<p>The documented remediation process was:</p>

<pre>
Open Bee-Box
      ↓
Open ProFTPD Configuration
      ↓
Disable Anonymous FTP Configuration
      ↓
Save Configuration
      ↓
Restart ProFTPD
      ↓
Verify FTP Connection
</pre>

<p>The project specifically modified <code>/etc/proftpd/proftpd.conf</code> and restarted the ProFTPD service after applying the configuration change.</p>


<h2>Results and Findings</h2>

<p>The assessment identified an FTP security weakness in the vulnerable Bee-Box environment.</p>

<h3>Finding</h3>

<p><strong>Anonymous FTP access was enabled.</strong></p>

<p>This allowed an unauthenticated user to attempt access to the FTP service.</p>

<h3>Assessment Activities</h3>

<p>The project performed:</p>

<ul>
  <li>Network scanning</li>
  <li>Service/version identification</li>
  <li>SMTP enumeration</li>
  <li>Username collection</li>
  <li>FTP credential testing</li>
  <li>FTP login verification</li>
  <li>Anonymous FTP access testing</li>
</ul>

<h3>Security Impact</h3>

<p>An improperly configured FTP service can expose files or services to unauthorized users. In an enterprise environment, such access could result in unauthorized information disclosure or misuse of the exposed service.</p>


<h2>Remediation Verification</h2>

<p>After modifying the ProFTPD configuration, the FTP service was restarted.</p>

<p>A new FTP connection attempt was then performed from Kali Linux to verify whether anonymous access was still possible.</p>

<p>The project documentation shows that the subsequent login attempt failed, indicating that the anonymous FTP access restriction had been successfully applied.</p>

<p>The FTP service no longer permitted the previously demonstrated anonymous login, confirming the effectiveness of the remediation.</p>

<h2>7. Sceenshots:</h2>
Step 1: Bee-Box Setup: Screenshots showing the Bee-Box virtual machine configuration and startup. <br/>
<br>
<p align="center">
<!-- <p align="center"> -->
<img src="https://i.imgur.com/AiN8k9L.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/Vh9DCIY.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/2j2nLRh.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/Qt8Gi32.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/4R9guDv.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/hbBKYqR.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/0vn9I4F.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/rYyPNUB.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/3QrVQyv.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/SCEsvjB.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/6QNmkru.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
</p>
Step 2: Network Configuration: Screenshots showing the NAT Network configuration and target IP identification.
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/S4AgmMQ.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
</p>
Step 3: Nmap Scanning: Screenshots showing the network and service scanning performed against Bee-Box.
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/JFgXFfi.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/31kxxY8.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/s0kKWe0.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/Fh26Pjm.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/gaYB50N.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/UJKfEEO.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/0m9Za8t.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
</p>
Step 4:Metasploit Enumeration: Screenshots showing the Metasploit SMTP enumeration process.
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/WtRQJX3.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/ezGvX0S.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/L0NAgoi.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/mnOKmhz.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/nq8kCww.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/NMNbS5y.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/hSwT6ry.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/gq8sN9p.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/dZTFYXE.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/cUF7Xlo.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/GQECPxX.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
</p>
Step 5: FTP Assessment: Screenshots showing FTP testing and access verification.
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/Bu1fbhb.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/lHFT31R.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/9vtKZM2.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/6Tatq66.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
</p>
Step 6: Remediation: Screenshots showing the ProFTPD configuration changes and service restart.
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/1PzqMtX.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/mRnY2HG.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/05loxbM.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/51lvq70.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/kmoHQ6r.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/UkvTJDI.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
<img src="https://i.imgur.com/LG9lej4.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
</p>
Step 7: Verification: Screenshots showing the failed anonymous FTP login after remediation.
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/qLcbMNV.png" height="80%" width="80%" alt="VAPT-Beebox-Security-Assessment"/>
<br />
<br />
</p>
<h2>8. Key Learnings</h2>

<p>This project provided practical exposure to several cybersecurity concepts and tools.</p>

<h3>Technical Learnings</h3>

<ul>
  <li>Setting up a vulnerable virtual machine for security testing.</li>
  <li>Configuring communication between virtual machines.</li>
  <li>Identifying target IP addresses.</li>
  <li>Performing Nmap network and service scans.</li>
  <li>Understanding open ports and exposed services.</li>
  <li>Performing service enumeration using Metasploit.</li>
  <li>Assessing FTP authentication.</li>
  <li>Using Hydra for controlled credential testing.</li>
  <li>Understanding the security risks of anonymous FTP.</li>
  <li>Modifying Linux service configuration files.</li>
  <li>Restarting services after security configuration changes.</li>
  <li>Verifying that remediation controls are effective.</li>
</ul>

<h3>Security Learning</h3>

<p>The project demonstrated the importance of:</p>

<ul>
  <li>Identifying exposed services.</li>
  <li>Assessing insecure configurations.</li>
  <li>Testing the security impact of discovered weaknesses.</li>
  <li>Applying appropriate remediation.</li>
  <li>Verifying remediation after configuration changes.</li>
</ul>
<h2>9. Conclusion</h2>

<p>This project demonstrated a complete practical VAPT exercise against the vulnerable Bee-Box environment.</p>

<p>The assessment began with target environment setup and network configuration, followed by Nmap-based scanning and service enumeration. The FTP service was then assessed through controlled authentication testing and anonymous access verification.</p>

<p>After identifying the anonymous FTP access weakness, the ProFTPD configuration was modified to restrict anonymous access. The service was restarted and the configuration was subsequently verified through another FTP connection attempt.</p>

<p>The project provided practical experience with the VAPT process and demonstrated how a security weakness can be <strong>identified, assessed, remediated, and verified</strong> in a controlled laboratory environment.</p>

<hr>

<h2>10. Disclaimer</h2>

<p>This project was performed strictly in a controlled laboratory environment using the vulnerable Bee-Box machine for educational and cybersecurity learning purposes.</p>

<p>The techniques and tools demonstrated in this repository should only be used on systems for which you have explicit authorization to perform security testing.</p>

<p>Do not use these techniques against unauthorized systems, networks, accounts, or services.</p>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
