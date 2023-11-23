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

```sh
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.UnsupportedEncodingException;
import java.net.HttpURLConnection;
import java.net.URLEncoder;
import java.nio.charset.StandardCharsets;
import java.net.URL;

public class Main {
    private static String baseUrl="http://<Domain Name>/api/SmsApi/SendSingleApi";
    public static void main(String[] args) throws IOException, InterruptedException {
        // Replace the following values with your actual credentials
        String userId = "Your_UserID";
        String password = "Your_Password";
        String senderId = "Your_SenderID";
        String phoneNumber = "Your_Mobile_Number";
        String message = "Hello Java Sample Code This is a testing SMS to check delivery";
        String entityId = "Your_EntityID";
        String templateId = "Your_TemplateID";

        String response = sendSingleSms(userId, password, senderId, phoneNumber, message, entityId, templateId);
        System.out.println(response);
    }
    public static String sendSingleSms(String userId, String password, String senderId, String phoneNumber, String message, String entityId, String templateId) throws IOException, InterruptedException {
        String encodedMessage = URLEncoder.encode(message, StandardCharsets.UTF_8.toString());
        String encodedPassword = URLEncoder.encode(password, StandardCharsets.UTF_8.toString());

        String apiurl = String.format("%s?UserID=%s&Password=%s&SenderID=%s&Phno=%s&Msg=%s&EntityID=%s&TemplateID=%s",
                baseUrl, userId, encodedPassword, senderId, phoneNumber, encodedMessage, entityId, templateId);

        try {
            System.out.println(apiurl);
            URL url = new URL(apiurl);
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");

            int responseCode = connection.getResponseCode();

            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                return response.toString();
            } else {
                System.out.println("HTTP GET request failed with response code " + responseCode);
            }
        } catch (Exception e) {
            return "Error";
        }
        return "";
    }
    
}

```

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

const smsApiClient = new SmsApiClient("http://<Domain Name>/api/SmsApi/SendSingleApi");

// Replace the following values with your actual credentials
const userId = 'Your_UserID';
const password = 'Your_Password';
const senderId = 'Your_SenderId';
const phoneNumber = 'Your_Mobile_Number';
const message = 'Hello NodeJS Sample Code testing This is a testing SMS to check delivery';
const entityId = 'Your_Entity_ID';
const templateId = 'Your_Template_ID';

smsApiClient.sendSingleSms(userId, password, senderId, phoneNumber, message, entityId, templateId)
    .then(response => console.log(response))
    .catch(error => console.error(error));

```

## PHP

```sh
<?php
class SmsApiClient {
    private $baseUrl;

    public function __construct($baseUrl) {
        $this->baseUrl = $baseUrl;
    }

    public function sendSingleSms($userId, $password, $senderId, $phoneNumber, $message, $entityId, $templateId) {
        $encodedMessage = urlencode($message);
        $encodedPassword = urlencode($password);

        $url = "$this->baseUrl?UserID=$userId&Password=$encodedPassword&SenderID=$senderId&Phno=$phoneNumber&Msg=$encodedMessage&EntityID=$entityId&TemplateID=$templateId";

        return file_get_contents($url);
    }
}

$smsApiClient = new SmsApiClient("http://<Domain Name>/api/SmsApi/SendSingleApi");

// Replace the following values with your actual credentials
$userId = 'Your_UserID';
$password = 'Your_Password';
$senderId = 'Your_SenderID';
$phoneNumber = 'Your_Mobile_Number';
$message = 'Hello PHP Sample Code testing This is a testing SMS to check delivery';
$entityId = 'Your_EntityID';
$templateId = 'Your TemplateID';

$response = $smsApiClient->sendSingleSms($userId, $password, $senderId, $phoneNumber, $message, $entityId, $templateId);
echo $response;
?>

```

## Python

```sh
import requests
from urllib.parse import urlencode

class SmsApiClient:
    def __init__(self, base_url):
        self.base_url = base_url

    def send_single_sms(self, user_id, password, sender_id, phone_number, message, entity_id, template_id):
        encoded_message = urlencode({'Msg': message})[4:]  # Removing 'Msg=' from the start
        encoded_password = urlencode({'Password': password})[9:]  # Removing 'Password=' from the start
        url = f"{self.base_url}?UserID={user_id}&Password={encoded_password}&SenderID={sender_id}&Phno={phone_number}&Msg={encoded_message}&EntityID={entity_id}&TemplateID={template_id}"
        print(url)
        response = requests.get(url)
        return response.text

# Replace the following values with your actual credentials
user_id = 'Your_UserID'
password = 'Your_Password'
sender_id = 'Your_SenderID'
phone_number = 'Your_Mobile_Number'
message = 'Hello Python Sample Code testing This is a testing SMS to check delivery'
entity_id = 'Your_Entity_ID'
template_id = 'Your_TemplateID'

sms_api_client = SmsApiClient("http://<Domain Name>/api/SmsApi/SendSingleApi")
response = sms_api_client.send_single_sms(user_id, password, sender_id, phone_number, message, entity_id, template_id)
print(response)

```

Feel free to explore and use these code samples in your projects!
