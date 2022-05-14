## Unit 19 Homework: Protecting VSI from Future Attacks

### Scenario

In the previous class,  you set up your SOC and monitored attacks from JobeCorp. Now, you will need to design mitigation strategies to protect VSI from future attacks. 

You are tasked with using your findings from the Master of SOC activity to answer questions about mitigation strategies.

### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.

### Logs

Use the same log files you used during the Master of SOC activity:

- [Windows Logs](resources/windows_server_logs.csv)
- [Windows Attack Logs](resources/windows_server_attack_logs.csv)
- [Apache Webserver Logs](resources/apache_logs.txt	)
- [Apache Webserver Attack Logs](resources/apache_attack_logs.txt	)

---

### Part 1: Windows Server Attack

Note: This is a public-facing windows server that VSI employees access.
 
#### Question 1
- Several users were impacted during the attack on March 25th.
![Top 10 Users](https://user-images.githubusercontent.com/94859787/168401874-7b0fafcf-6f63-4c26-8460-6e7d987875b3.png)
![Top 10 Signatures](https://user-images.githubusercontent.com/94859787/168401881-b7cdf9e5-823f-4213-b0e3-b7f32aef05fb.png)


- Based on the attack signatures, what mitigations would you recommend to protect each user account? Provide global mitigations that the whole company can use and individual mitigations that are specific to each user.
- The best solution for global mitigations - That the whole company can use and individual mitigations that are specific to each user.
- Individual Solutions:
  - User: K - an attemtp was made to reset password
  - User: A - user was locked out - should reset his password 
![User A](https://user-images.githubusercontent.com/94859787/168402818-1baa8920-9b14-48f7-a846-9781e79bf699.png)
  - User: J - he was able to succesfully login 
  
#### Question 2
- VSI has insider information that JobeCorp attempted to target users by sending "Bad Logins" to lock out every user.
- What sort of mitigation could you use to protect against this?
  - Offer regular cyber awareness training and workshops. Regular, interactive cyber awareness programs, simulated phishing attacks.

  - Assess the security process of vendors before providing them with access. It makes sense to conduct a comprehensive, end-to-end vendor risk assessment for third parties to understand and evaluate their security posture before providing any access to the business network and prior to sharing any critical data.

  - Use official contact information (such as the person’s phone number from your organization’s internal contact directory) and not information that’s provided to you by the suspicious individual.
  

### Part 2: Apache Webserver Attack:

#### Question 1
<img width="1058" alt="Screen Shot 2022-05-13 at 7 18 26 PM" src="https://user-images.githubusercontent.com/94859787/168403475-aa56e075-e591-45a3-a2cf-69f73457d517.png">
<img width="1378" alt="Screen Shot 2022-05-13 at 7 20 47 PM" src="https://user-images.githubusercontent.com/94859787/168403512-bb5411d4-5088-43a5-b536-9f05fe0444b5.png">
<img width="1371" alt="Screen Shot 2022-05-13 at 7 22 31 PM" src="https://user-images.githubusercontent.com/94859787/168403592-747e8fd3-3b5a-4693-8834-aa0a422b3a78.png">

- Based on the geographic map, recommend a firewall rule that the networking team should implement.
  - Filtering out the traffic from the United States, the country which had the most activity is coming from Ukraine.
- Provide a "plain english" description of the rule.
  - For example: "Block all incoming HTTP traffic where the source IP comes from the city of Los Angeles."
   - Firewall Rule Description- Block all incoming HTTP traffic where the source IP comes from the country of Ukraine.
- Provide a screen shot of the geographic map that justifies why you created this rule. 
  
#### Question 2

- VSI has insider information that JobeCorp will launch the same webserver attack but use a different IP each time in order to avoid being stopped by the rule you just created.

- What other rules can you create to protect VSI from attacks against your webserver?
  - Most of the data coming from the Ukarine is approximately 34% of the network. There are 3 other vaules that could cause for the creation of more firewalls: bytes, ip, useragent.

  - Block all incoming HTTP traffic where the bytes are equal to 65748

  - Block all incoming HTTP traffic where the ip address is equal to 194.105.145.147 AND 79.171.127.34

  - Block all incoming HTTP traffic where the useragent is equal to Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.2; SV1; .NET CLR 2.0 50727987787; InfoPath.1)
  - Conceive of two more rules in "plain english". Hint: Look for other fields that indicate the attacker.
