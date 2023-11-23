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

```sh
const http = require('http');
const querystring = require('querystring');

class SmsApiClient {
    constructor(baseUrl) {
        this.baseUrl = baseUrl;
    }

    sendSingleSms(userId, password, senderId, phoneNumber, message, entityId, templateId) {
        const encodedMessage = encodeURIComponent(message);
        const encodedPassword = encodeURIComponent(password);

        const params = {
            UserID: userId,
            Password: encodedPassword,
            SenderID: senderId,
            Phno: phoneNumber,
            Msg: encodedMessage,
            EntityID: entityId,
            TemplateID: templateId
        };

        const url = `${this.baseUrl}?${querystring.stringify(params)}`;

        return new Promise((resolve, reject) => {
            http.get(url, (response) => {
                let data = '';

                response.on('data', (chunk) => {
                    data += chunk;
                });

                response.on('end', () => {
                    resolve(data);
                });
            }).on('error', (error) => {
                reject(`Error: ${error.message}`);
            });
        });
    }
}

const smsApiClient = new SmsApiClient("http://nimbusit.biz/api/SmsApi/SendSingleApi");

// Replace the following values with your actual credentials
const userId = 'testdemo';
const password = 'cbhe1755CB';
const senderId = 'TECHNP';
const phoneNumber = '7011361944';
const message = 'Hello NodeJS Sample Code testing This is a testing SMS to check delivery TECPRP';
const entityId = '1201159409941345107';
const templateId = '1707167940051443628';

smsApiClient.sendSingleSms(userId, password, senderId, phoneNumber, message, entityId, templateId)
    .then(response => console.log(response))
    .catch(error => console.error(error));

```

## PHP

[PHP Code](php/SmsApiClient.php) is organized with the `SmsApiClient` class. Replace placeholders within the `main` section to interact with the SMS API.

## Python

[Python Code](python/SmsApiClient.py) is object-oriented. Replace placeholders in the main program to interact with the SMS API. Ensure Python is installed.

Feel free to explore and use these code samples in your projects!
