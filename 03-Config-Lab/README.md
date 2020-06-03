# LAB 3 - AWS Config

1)  Go to the AWS Search Service bar and find *AWS Config*. Press *Get started*.

![images](images/1f913f3da05e7bddd31bbe4f2ae66eff.png)

2)  In the *Settings* section make sure you select both options in *All
    resources* and make sure that a S3 bucket is configured to store the
    configuration history and configurations snapshot.

![images](images/7b5b0af103e0179df544484801f14914.png)

3)  In the *SNS topic* provide a name for the new topic created. In this case
    *config-topic*, press *Next* once done.

![images](images/036c0dde57bac060954ae8fc4ff8c332.png)

4)  Select the following 3 rules:
* ec2-instance-detailed-monitoring-enabled
* cloudtrail-enabled 
* multi-region-cloudtrail-enabled

**:heavy_exclamation_mark: Use the search bar to find them.** Click *Next* once done.

![images](images/a6966fb42a24a42322f3a8f6b6fcef18.png)

5).  Review the configuration page and click *Confirm*.

![images](images/de37869ace958028cfeabed59551966a.png)

6)  You will wait a couple of minutes till the rules are set up.

![images](images/92c267b2f113ff4908ef3ef5cbdf0862.png)

7)  Refresh the console to make sure that all the metrics are displayed on the
    console

![images](images/b7f2e48c1c44f5f73eb79f7c7000a658.png)

8)  Once done you will see the following the dashboard

![images](images/7d7b49f223c61764d8af1d1a00f597cb.png)

As we can see there is an alarm raised. This alarm states that there is an EC2 instance that does not have "Detailed Monitoring" Enabled. Let’s proceed and remediate this
alarm.

9)  Lets click on the alarm and see what EC2 instance does not comply with our configuration rule. Take note of the instance ID so we can remediate this alarm.

![images](images/config-bad-rule.png)

10)  Now that we have the EC2 instance that is not compliant let's go and enable the "Detaied Monitoring". Go to the *EC2 console* and under __Instances__ search for the 
instance ID that has the alarm. 

![images](images/6ca4ad538d4c9721fa5ee1deaf09ea43.png)

11)  Click on the monitoring tab after selecting the EC2 instance and then click __"Enable Detailed Monitoring"__.

![images](images/a857e16c7e873ae562fe0e594698d396.png)

12)  Click __Yes, Enable__ and then click __Close__ .

![images](images/yes-enable-dm.png)

13)  After enbling the detail monitoring, return to the AWS Config Console and re-evaluate the rule that shows the alarm.

![images](images/351dc23980958dc249d36d40ee4301e0.png)

Refresh the page a couple of times and the alarm should dissapear.

![images](images/no-alarms-config.png)

14) Check also the dashboard and make sure that no alarms are being reported

![images](images/dashboard-all-ok.png)

Now that all the alarms dissapeared we can proceed to the [next lab (KMS Lab)](../04-KMS-Lab/README.md)
