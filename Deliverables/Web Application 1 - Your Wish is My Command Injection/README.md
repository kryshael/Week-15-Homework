
### Web Application 1: *Your Wish is My Command Injection*
<br/><br/>

**Deliverable**: Take a screen shot confirming that this exploit was successfully executed and provide 2-3 sentences outlining mitigation strategies.
<br/><br/>

![WebApp1passwd](https://github.com/kryshael/Week-15-Homework/blob/main/Assets/Screenshots/WebApp1passwd.png)


![WebApp1hosts](https://github.com/kryshael/Week-15-Homework/blob/main/Assets/Screenshots/WebApp1hosts.png)
<br/><br/>
### Mitigation Methods

- Limiting user input when calling for files from the web application.

- If the application does require user input when calling for files, using **input validation** to limit the user's ability to modify the file being accessed.

- Web servers should run under a special service user account that only has access to that web folder. Apache typically uses the `www-data` account.
