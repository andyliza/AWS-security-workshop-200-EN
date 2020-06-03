# LAB 6 - AWS Web Application Firewall

**:heavy_exclamation_mark: Before we start check on http://whatismyip.com what is your public IP. We will be using it to block access to our ALB with AWS WAF.**

![images](images/0-whatismyip.png)

Take note of your public IP and write it down on a scratchpad.

**:heavy_exclamation_mark: Take note also of the ALB DNS name**

![images](images/alb-dns.png)

And paste the DNS name in a new tab.

![images](images/website.png)

*Now that we have this information lets start configuring the WAF*

1)  Got to the AWS WAF console and select *Go to AWS WAF*.

![images](images/0364236d876a9d7f3448dc62b86b5a07.png)

2) On left side menu you will see *IP sets*. Click on that section and select **Create IP set**. Make sure you are in the *Singapore* Region

![images](images/0-1-create-ip-set.png)

3) In the IP set wizzard fill in the name of the set, Region and **your public IP**. **DO NOT USE THE IP highligted in the image**. You must use your public IP.

![images](images/0-2-IP-set.png)

4) Once the IP set is successfully created we will see it in the list

![images](images/0-3-success-ip-list.png)

5)  Now from the left side menu go to *Getting started* and click on *Create Web ACL*. The web ACL wizard will guide us through all
    the steps necessary to create the conditions and rules that are necessary in a Web ACL.

![images](images/2-Create-Web-ACL.png)

6)  Fill in the Web ACL name, description, **the region**, CloudWatch Metric name  and click *Add AWS Resources*.
    once done.

![images](images/3-Name-the-Rule-Add-resource.png)

7) Select the Application Load Balancer created in the previous Lab. This might be named *techshift-alb* or other name that you might have used.

![images](images/3-1-add-alb.png)

8)  Once the AWS resource is added press **Next**

![images](images/4-Press-Next.png)

9)  In the *Add rules and rule groups* section click on **Add rules - > Add my own rules and rules groups**.

![images](images/5-add-rule.png)

10)  In the rule creation wizard select the **Rule builder** option and fill in all the fields as presented in the image below. Make sure you select the **IP Set** created in the previous steps.

![images](images/6-add-rule-content.png)

11)  Once the rule has been created press *Next* to add the rule

![images](images/7-add-rules-to-groups.png)

12)  Since this is the only rule we have there is no priority to be set so we are just going to move to the *Next* step.

![images](images/8-set-rule-priority.png)

13)  We will be configuring CloudWatch Metrics to measure the block rate of the rule. Press *Next* at this step.

![images](images/9-Configure-metrics.png)

14)  Go over the summary of the Web ACL and click *Create web ACL* at the bottom of the page

![images](images/10-create-web-acl.png)

15) You will see a success message once the rule is created properly

![images](images/11-completed.png)

Once the creation is completed go ahead and test it on your browser by accessing the DNS of the ALB that the WEB ACL is applied on. You will
notice that you are not allowed to access you ALB. since the traffic is com

![images](images/7205543d7b9f5e8b063fbe3a4b715446.png)

You can try accessing the website via your phone and you will see that the web page will be successfully displayed.

After completing this activity you can move on to [the next lab (Analyzing CloudTrail Logs with Athena)](../07-CT-Athena-Lab/README.md)
