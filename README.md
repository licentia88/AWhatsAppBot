# AWhatsAppBot

**If you like the bot and feel like to donate I would really appreciate it as I am unemployed at the moment due to the pandemic.**

[Buy Me a Coffee or More](https://www.buymeacoffee.com/AsmG)

**Whatsapp Bot for C# .Net Framework  Easy & Simple to use**

*** READ ME FIRST ***

When you install the package from nuget you will be seeing a folder named Chrome Driver which located in your project directory.
**Move chromedriver.exe from the folder into your release and debug folders** 


In order for the bot to work the **chrome driver version** and  **Chrome version** should match.

**if the bot is throwing an exception you need to check the following:**

1- Open chrome and type in chrome://settings/help to the url field or go to Setting-> help to check your chrome version
**Example version Info:
Google Chrome is up to date
Version 83.0.4103.116 (Official Build) (64-bit)

2- Go to https://chromedriver.chromium.org/downloads and download the appropriate chrome driver that's matching your chrome version
in this case I should be using : version ChromeDriver 83.0.4103.39 that is listed on the page

3- Update to the latest version.

#**SAMPLE USAGE**

```csharp
public void SendBulkSms(List<string> phoneNumbers, string message, List<string> imagePaths )
        {
           //When initializing the bot we need to type timout second, we need parameter 
           //Because we do not know how long will it take the browser to load all the elements required for the bot to work
           //To be more precise: if for any reason(slow connection/invalid phone number etc) the bot will not send the message to a specific number
           //it will iterate to the next number after the defined timeout seconds 20 in this case.
            using (var newConnection = new AWhatsappBot(20)) 
            {
            
                //When your your code hits the below line you will be needing to scan the QR code through your mobile to open web whatsapp.
                //**Please Note that** if you do not scan the QR code in defined timeout second, it will return.
                if (!newConnection.Initialize()) return;   
                foreach (var phoneNumber in phoneNumbers)
                {
                   
                    Try
                    {
                    newConnection.SendMessage(phoneNumber,message); // send message
                    //or
                    newConnection.SendMessage(phoneNumber, message,imagePaths); // send images   ( directory path will be given here.
                    }
                    Catch
                    {
                       //IF your code hits this line it means: either you have an invalid phone number, 
                       //the phone number does not have whatsapp or It failed because of the slow internet connection
                    }
                }
            }
        }
 ```
