# Unit 15 Homework

## Overview

In this homework scenario, you will continue as an application security engineer at Replicants. Replicants created several new web applications and would like you to continue testing them for vulnerabilities. Additionally, your manager would like you to research and test a security tool called **BeEF** in order to understand the impact it could have on the organization if Replicants was targeted with this tool. 

### Lab Environment

You will continue to use your Vagrant virtual machine for this assignment.

### Topics Covered in Your Assignment

- Web application vulnerability assessments
- Injection
- Brute force attacks
- Broken authentication
- Burp Suite
- Web proxies
- Directory traversal
- Dot dot slash attacks
- Beef
- Cross-site scripting
- Malicious payloads


---

## Instructions

In this assignment, you will test three web application vulnerabilities. For each vulnerability you will be provided with the following:

  - Steps detailing how to setup and access the application.

  - A walkthrough explaining how the application is intended to work.

  - A task that will test the application for vulnerabilities.

Your goal is to determine if the application is vulnerable and provide mitigations.

### Submission Guidelines

You will submit a document (Word or Google Docs) that contains the following for each web application: 

- Screen shots confirming the successful exploit.

- Two to three sentences detailing recommended mitigation strategies. 

When complete, submit the file on BCS.   


---

### Web Application 1: *Your Wish is My Command Injection*

1. Complete the following to set up the activity. 

    - Access Vagrant and open a browser.

    - Navigate to the following webpage: <http://192.168.13.25> and select the **Command Injection** option.
      
      - Alternatively, access the webpage directly at this page: <http://192.168.13.25/vulnerabilities/exec/>
      
      - The web page should look like the following:

        ![wd_hw1](Images/wd_hw1.png)

   **Note:** If you have any issues accessing this webpage,  refer to the Activity Setup steps we completed in the activity `06_SQL_Injection` on Day 1 of this unit. 

    - <details><summary> Click here to view the set up instructions.</summary>


      - To launch the environment, complete the following:

        - Launch Vagrant from GitBash or the Mac terminal using the following command: `vagrant up`
        
        - Then, open the command line inside Vagrant and run the following command: `cd ./Documents/web-vulns && docker-compose up`.

        - Leave this page open and continue to the next step. 

      - To access the Replicants website, open a web browser within Vagrant and access the following webpage: <http://192.168.13.25/setup.php>.

        - On the bottom of this page, click **Create / Reset Database**.
      
        - This will configure the database for the application.
        
        - The message "Setup Successful" at the bottom of the page will indicate that it is complete. 

      - To log in to the mock Replicants website, access the following webpage: <http://192.168.13.25/login.php>.

        - Log in with the following credentials:
          
          - Username: `admin`
          
          - Password: `password`

    </details>


2. This page is a new web application built by Replicants in order to enable their customers to `ping` an IP address. The web page will return the results of the ping command back to the user.

   Complete the following steps to walkthrough the intended purpose of the web application. 

   - Test the webpage by entering the IP address `8.8.8.8`. Press Submit to see the results display on the web application.

     ![wd_hw2](Images/wd_hw2.png)

     - Behind the scenes, when you select Submit, the IP you type in the field is *injected* into a command that is run against the Replicants webserver. The specific command that ran on the webserver is `ping <IP>` and `8.8.8.8` is the field value that is injected into that command.
     
     - This process is no different than if we went to the command line and typed that same command: `ping 8.8.8.8`

       ![wd_hw3](Images/wd_hw3.png)

3. Test if we can manipulate the input to cause an unintended result.

    - On the same webpage, enter the following command (payload) in the field: `8.8.8.8 && pwd`

    - This command uses two ampersands to add a second command to the original request:

      - `pwd` is the second command. It will display the directory location where the command is run on the Replicants webserver.
     
      - This would be no different than running `ping 8.8.8.8 && pwd` on the command line. 
  
   - Press Enter. Note the ping results are the results of the second `pwd` command:

     ![wd_hw4](Images/wd_hw4.png)

    This type of injection attack is called **Command Injection**, and it is dependent on the web application taking user input to run a command against an operating system.

4. Now that you have determined that Replicants new application is vulnerable to command injection, you are tasked with using the dot-dot-slash method to design two payloads that will display the contents of the following files:
   
   - `/etc/passwd`
   
   - `/etc/hosts`
  
   **Hint:** Try testing out a command directly on the command line to help design your payload.

5. **Deliverable**: Take a screen shot confirming that this exploit was successfully executed and provide 2-3 sentences outlining mitigation strategies. 

