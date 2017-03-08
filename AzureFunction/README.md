## Azure Functions Lab

1. Get the IoT Hub Connection String
  1. Open the Azure Portal [here](https://ms.portal.azure.com)
  1. Click on “Endpoints” under “Messaging”
  1. Click on “Events”
  1. Save the “Event Hub-compatible name” and “Event Hub-compatible endpoint.  (EVENTHUB_CONFIG)
  1. Create a new Shared Access Policy for the function
    1. Click on “Shared Access Policies”
    1. Click on “+ Add”
    1. Enter a name for your policy.  Eg. “Function”  
    1. Give the following permissions
      1. Registry Read
      1. Registry write
      1. Service connect
      1. Save the Connection String.  
1.	Create Azure Function
  1. Go to the Azure functions portal: [here](https://functions.azure.com/signin)
  1. Enter Subscription, Name for Function App, and Region
  1. Click on “+ New Function”
  1. Choose the “EventHubTrigger-CSharp”
i.	Enter “Name of Function”
ii.	Enter “Event Hub name”.  See EVENTHUB_CONFIG above
iii.	Enter “Event Hub connection”.  This is the connection string for the event hub.
1.	Choose “Add”
2.	Enter IoT Event Hub compatible connection name (from IoT Hub above)
3.	Enter IoT Event Hub compatible connection string
Format: Endpoint=sb://<eventHubName>.servicebus.windows.net/;SharedAccessKeyName=<SASPolicyName>;SharedAccessKey=<SASPolicyKey>
e.	Configure libraries
i.	Expand “Logs” view at the bottom of the page
ii.	Click on “View Files”
iii.	Click on “+ Add”
iv.	Enter “project.json”
v.	Upload project.json file from github
vi.	Pause the function
vii.	Copy the text from Function.txt in github to run.csx
viii.	Update the CONNECTION_STRING variable to point to the IoT Hub Connection String.  See “(IOT_HUB_CONNECTION_STRING)” above.
ix.	Click “Start” to start the function