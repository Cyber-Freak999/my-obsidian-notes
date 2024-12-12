**CloudWatch**

 AWS CloudWatch is a monitoring and observability platform that gives us greater insight into our AWS environment by monitoring applications at multiple levels. CloudWatch provides functionalities such as the monitoring of system and application metrics and the configuration of alarms on those metrics for the purposes of today's investigation, though we want to focus specifically on CloudWatch logs. Running an application in a cloud environment can mean leveraging lots of different services (e.g. a service running the application, a service running functions triggered by that application, a service running the application backend, etc.); this translates to logs being generated from lots of different sources. CloudWatch logs make it easy for users to access, monitor and store the logs from all these various sources. A CloudWatch agent must be installed on the appropriate instance for application and system metrics to be captured.

A key feature of CloudWatch logs that will help the Warevile SOC squad and us make sense of what happened in their environment is the ability to query application logs using filter patterns. Here are some CloudWatch terms you should know before going further:

- **Log Events:** A log event is a single log entry recording an application "event"; these will be timestamped and packaged with log messages and metadata.
- **Log Streams:** Log streams are a collection of log events from a single source.
- **Log Groups:** Log groups are a collection of log streams. Log streams are collected into a log group when logically it makes sense, for example, if the same service is running across multiple hosts.

**CloudTrail**

CloudWatch can track infrastructure and application performance, but what if you wanted to monitor actions in your AWS environment? These would be tracked using another service called AWS CloudTrail. Actions can be those taken by a user, a role (granted to a user giving them certain permissions) or an AWS service and are recorded as events in AWS CloudTrail. Essentially, any action the user takes (via the management console or AWS CLI) or service will be captured and stored. Some features of CloudTrail include:

- **Always On:** CloudTrail is enabled by default for all users
- **JSON-formatted:** All event types captured by CloudTrail will be in the CloudTrail JSON format
- **Event History:** When users access CloudTrail, they will see an option "Event History", event history is a record of the actions that have taken place in the last 90 days. These records are queryable and can be filtered on attributes such as "resource" type.
- **Trails:** The above-mentioned event history can be thought of as the default "trail," included out of the box. However, users can define custom trails to capture specific actions, which is useful if you have bespoke monitoring scenarios you want to capture and store **beyond the 90-day event history retention period**.
- **Deliverable:**  As mentioned, CloudWatch can be used as a single access point for logs generated from various sources; CloudTrail is no different and has an optional feature enabling **CloudTrail logs to be delivered to CloudWatch**.

![JSON rain image](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1731078142249.png)  

As mentioned, Cloudtrail helps capture and record actions taken. These actions could be interactions with any number of AWS services. For example, services like **S3** (Amazon Simple Storage Service used for object storage) and **IAM** (AWS's Identity and Access Management service can be used to secure access to your AWS environment with the creation of identities and the assigning of access permissions to those identities) will have actions taken within their service recorded. These recorded events can be very helpful when performing an investigation.  

## Intro to JQ

**What is JQ?**

Earlier, it was mentioned that Cloudtrail logs were JSON-formatted. When ingested in large volumes, this machine-readable format can be tricky to extract meaning from, especially in the context of log analysis. The need then arises for something to help us transform and filter that JSON data into meaningful data we can understand and use to gain security insights. That's exactly what JQ is (and does!). Similar to command line tools like sed, awk and grep, JQ is a lightweight and flexible command line processor that can be used on JSON.

![Cloud JQ investigation image](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1731078090249.png)  

**How Can It Be Used?**

Now, let's take a look at how we use JQ to transform and filter JSON data. The wares being the wares, they stored their shopping list from the trip to the bookstore in JSON format. Let's take a look at that:

```javascript
[

{ "book_title": "Wares Wally", "genre": "children", "page_count": 20 },

{ "book_title": "Charlottes Web Crawler", "genre": "young_ware", "page_count": 120 },

{ "book_title": "Charlie and the 8 Bit Factory", "genre": "young_ware", "page_count": 108 },

{ "book_title": "The Princess and the Pcap", "genre": "children", "page_count": 48 },

{ "book_title": "The Lion, the Glitch and the Wardrobe", "genre": "young_ware", "page_count": 218 }

]
```

JQ takes two inputs: the filter you want to use, followed by the input file. We start our JQ filter with a `.` which just tells JQ we are accessing the current input. From here, we want to access the array of values stored in our JSON (with the `[]`). Making our filter a `.[]`. For example, let’s run the following command. 

JQ syntax

```shell-session
user@tryhackme$ jq '.[]' book_list.json
```

The command above would result in this output:

```javascript
{
  "book_title": "Wares Wally",
  "genre": "children",
  "page_count": 20
}
{
  "book_title": "Charlottes Web Crawler",
  "genre": "young_ware",
  "page_count": 120
}
{
  "book_title": "Charlie and the 8 Bit Factory",
  "genre": "young_ware",
  "page_count": 108
}
{
  "book_title": "The Princess and the Pcap",
  "genre": "children",
  "page_count": 48
}
{
  "book_title": "The Lion, the Glitch and the Wardrobe",
  "genre": "young_ware",
  "page_count": 218
}
```

Once we've accessed the array, we can grab elements from that array by going one step deeper. For example, we could run this JQ command:

JQ syntax

```shell-session
user@tryhackme$ jq  '.[] | .book_title' book_list.json
```

If we wanted to view all the book titles contained within this JSON file, this would return a nicely formatted output like this:

```javascript
"Wares Wally"
"Charlottes Web Crawler"
"Charlie and the 8 Bit Factory"
"The Princess and the Pcap"
"The Lion, the Glitch and the Wardrobe"
```

That's a lot nicer to look at, isn't it? It gives you an idea of what JQ is and what it does. Of course, JQ can filter and transform JSON data in many additional ways. In our upcoming investigation, we'll see the tool in action.