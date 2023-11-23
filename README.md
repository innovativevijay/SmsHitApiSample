# SmsHitApiSample
Code samples in C#, Java, Node.js, PHP, and Python demonstrate how to perform HTTP GET requests for sending SMS via an API. 


# SMS API Integration

This repository provides code samples in C#, Java, Node.js, PHP, and Python for interacting with an SMS API through HTTP GET requests.

## C#

```sh
using System;
using System.Net;
using System.Web;

public class SmsApiClient
{
    private string baseUrl;

    public SmsApiClient(string baseUrl)
    {
        this.baseUrl = baseUrl;
    }

    public string SendSingleSms(string userId, string password, string senderId, string phoneNumber, string message, string entityId, string templateId)
    {
        string encodedMessage = HttpUtility.UrlEncode(message);
        string encodedPassword = HttpUtility.UrlEncode(password);

        string url = $"{baseUrl}?UserID={userId}&Password={encodedPassword}&SenderID={senderId}&Phno={phoneNumber}&Msg={encodedMessage}&EntityID={entityId}&TemplateID={templateId}";
		Console.WriteLine(url);
		return "Done";
        using (WebClient client = new WebClient())
        {
            return client.DownloadString(url);
        }		
    }
}

class Program
{
    static void Main()
    {
        SmsApiClient smsApiClient = new SmsApiClient("http://<DomainName>/api/SmsApi/SendSingleApi");

        // Replace the following values with your actual credentials
        string userId = "Your_UserID";
        string password = "Your_Password";
        string senderId = "Your_SMS_SenderId";
        string phoneNumber = "Your_Mobile_Number";
        string message = "Hello C-Sharp Code Testing This is a testing SMS to check delivery";
        string entityId = "Your Entity ID";
        string templateId = "Your Template ID";

        string response = smsApiClient.SendSingleSms(userId, password, senderId, phoneNumber, message, entityId, templateId);
        Console.WriteLine(response);
    }
}

```

## Java

[Java Code](java/SmsApiClient.java) showcases the `SmsApiClient` class, constructing the URL in the `sendSingleSms` method. Update credentials in the `main` method.

## Node.js

[Node.js Code](nodejs/smsApiClient.js) uses the `SmsApiClient` class for SMS API interaction. Update credentials in the main program and ensure Node.js is installed.

## PHP

[PHP Code](php/SmsApiClient.php) is organized with the `SmsApiClient` class. Replace placeholders within the `main` section to interact with the SMS API.

## Python

[Python Code](python/SmsApiClient.py) is object-oriented. Replace placeholders in the main program to interact with the SMS API. Ensure Python is installed.

Feel free to explore and use these code samples in your projects!
