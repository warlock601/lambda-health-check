# lambda-health-check
## lambda function to monitor the health of multiple applications and trigger SNS alerts
Even though the ELB health checks monitor these and respawn the errored out applications, we have seen situations where even the newly spawned app instances continue to crash and introduce downtimes.
So we needed a way to get notified if an application is down so we can manually intervene. Here we've used the example of springboot applications.
<br/>
<br/>
![Screenshot 2023-11-21 105223](https://github.com/warlock601/lambda-health-check/assets/32487715/1f9ae0e7-736e-4b9b-8c63-313371213d4e)

The above diagram explains the serverless monitoring architecture I came up with to solve this problem.

- A lambda function written in Python that can check a set of health check endpoints when invoked (Code is shown in a later section)
- A schedule defined in Cloud watch with the above lambda as a target. In our case, the schedule was every 5min.
- A SNS topic configured to send text messages and emails
