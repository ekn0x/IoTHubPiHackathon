## Azure Functions Lab

In this part of the lab, you will create an Azure function that will be used to programmatically send data back to the Raspberry Pi. 

### Obtain Values Required to Connect Function to the IoT Hub
1. Get the values associated with the Event Hub compatible endpoints as well as the IoT Hub Connection String:
  1. Open the Azure Portal [here](https://ms.portal.azure.com)
  1. Click on the IoT Hub that was created earlier. 
  1. Under the “Messaging” category click on “Endpoints”.
  1. In the list of "Built-in endpoints", click on “Events” to load the Events endpoint properties blade. 
  1. Take note of the values for the “Event Hub-compatible name” and “Event Hub-compatible endpoint" fields.  (EVENTHUB_CONFIG)<br />  
  ![Event Hub Endpoint](/images/EHendpointValues.jpg) <br />
  1. Create a new Shared Access Policy for the function that you will create. 
    1. Click on “Shared Access Policies”
    1. Click on “+ Add”
    1. Enter a name for your policy.  Eg. “Function”  
    1. Give the following permissions
      - Registry Read
      - Registry write
      - Service connect
    1. Click the "Create" button. 
    ![Create SAS](/images/CreateSAS.jpg)
    1. Once the new Shared Access Policy has been created, click the new policy. 
    1. Take note of the "Connection String-primary key".  This is the value for the new IoT Hub Functions connection string (IOT_HUB_CONNECTION_STRING) <br />
    ![Connection string](/images/ConnectionString.jpg) <br><br> 
    You should have three different values noted now: “Event Hub-compatible name", “Event Hub-compatible endpoint" and the IoT Hub Functions connection string. These values will be used to connect your function to the IoT Hub. 

### Create a Function
1.	Next, you will create an Azure Function. In this step, you will be creating a C# Azure Function that will be activated whenever the compatible event hub within the IoT hub service receives a new event. 
  1. Go to the Azure functions portal: [here](https://functions.azure.com/signin)
  1. Select your Subscription, enter a Name for your Function App, and select the Region you will deploy the function to. Click on "Create + get started" <br />
  ![Create Function](/images/CreateFunction.jpg)
  
  1. Click on "Custom Function" <br>
  ![Create Function](/images/CustomFunction.JPG)
  
  1. Click on the plus sign ("+") next to "Functions".
  
  1. Choose the “EventHubTrigger-CSharp”
    1. Enter a name for your new function in the “Name your function” field. eg. MessageTriggerFunction
    1. In the “Event Hub name” field, enter the Event hub-compatible name that was obtained above. eg. iothandsonlabc4f51. 
    ![Select EH Trigger](/images/EHTrigger.jpg)
    1. Next, you will create a new “Event Hub connection”.  The value for this connection will be the connection string for the event hub compatible endpoint built into the IoT Hub. The steps to create the new connection are as follows:
      - Click "new”.
      - Click "Add a connection string".
      - In the *Connection name* field, enter the IoT Hub Event Hub-compatible connection name that you obtained earlier
      - In the *Connection string* field, enter the IoT Event Hub compatible connection string. This connection string can be formed using a combination of strings obtained from the connection parameters noted earlier in the lab. The three strings are:
         1. The string "Endpoint="
         2. The value of the *Event Hub-compatible string* eg. sb://iothub-ns-iothandson-123156-90f62e3525.servicebus.windows.net/
         3. A subset string obtained from the *Functions connection string*. You will require the text associated with the ShareAccessKeyName and the ShareAccessKey. eg.  ;SharedAccessKeyName=functions;SharedAccessKey=hMfDUWMgNIXtLTqQ9Opr6/NtrqcxcJ9gKULcmPppZiA=*
         
         In our example, the values we obtained in the previous steps were:<br />
         ![Event Hub endpoint Name](/images/EHCompatibleEP.jpg)<br />
         and the <br />
         ![IoT Hub Functions Connection String](/images/FunctionsConnectionString.jpg) <br />
                  
         The newly formed Event Hub connection string will look like the following (join the values highlighted in yellow and green). Paste this new connection string value into the "Connection string" field. 
         <br />
         ![New Event Hub Connection String](/images/EHConnectionString.jpg)
         
   - Click "OK"
    
      <p align="center">
         <img src="/images/EHconnection.jpg" width="50%" height="50%" /> 
      </p>
      
  1. On the *New Function* page, click "Create". The template for your new Event Hub Trigger function is now created!
  1. Configure libraries for the new function created. 
    1. Expand the “Logs” view at the bottom of the page
    1. Click on “View Files”
    ![Expand Function views](/images/functionViews.jpg)
    1. Click on “+ Add” under the "View files" tab. 
    1. Enter “project.json” <br />
    ![Add project file](/images/addProject.jpg)
    1. Copy the text from [project.json](/AzureFunction/project.json) file in the github repo to the new json file you created.
    1. Click "Save". 
    <p align="center">
    <img src="/images/projectSave.jpg" width="50%" height="50%" />
    </p>    
        
    1. Copy the text from [Function.txt](/AzureFunction/AzureFunction.txt) in the github repo to the "run.csx" file. 
    1. In the run.csx file, find the CONNECTION_STRING variable and set the value to the IoT Hub Functions Connection String that you obtained earlier.  See “(IOT_HUB_CONNECTION_STRING)” above.
    <p align="center">
    <img src="/images/runFunction.jpg" />
    </p>
    1. Click “Run” to start the function

## Trying it out

You may have difficulties getting your Pi temperature over the threshold.  You can do one of the following:
- Lower the threshold in the device twin in the preconfigured solution website
- Update your Python script to use the Sense Hat emulator instead of the physical board.  

[Back to Main HOL Instructions](/README.md)
