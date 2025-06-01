# Modified for moving boat.. 

Request update every 1 hours or 5 nm of movement: Done with extensive use of Cursor AI https://www.cursor.com/ 


<img src=https://github.com/allancph/node-red-DMI-API-forecast/blob/main/Sk%C3%A6rmbillede%202025-02-12%20kl.%2015.09.06.png width="50%" height="50%" />

# node-red-DMI-API-forecast
Node-Red flow to retrieve a 5 day weather forecast from DMI, Danish Meteorological Institute

<img src=https://user-images.githubusercontent.com/16189982/234341251-d8ef8c74-9044-4fd8-9600-31c7bf81fd15.png width="50%" height="50%" />


<img src=https://user-images.githubusercontent.com/16189982/234339735-ddf5c793-6803-4dfa-a801-3e68ba283ae4.png width="30%" height="30%" />

Full documentation available at https://pysselilivet.blogspot.com/2023/04/dmi-forecast-api-for-atmosphere-ocean.html

## API Key Configuration

This flow requires a DMI API key to fetch weather data. The API key is configured directly within the Node-RED flow editor.

1.  **Import the Flow**: If you haven't already, import the `DMI_moving.json` flow into your Node-RED editor.
2.  **Locate the API Key Inject Node**:
    - In the Node-RED editor, find the tab for the DMI flow (likely labeled "DMI made by cursor AI" or similar).
    - Look for an **Inject node** named "**SET DMI API KEY HERE (Edit to add your key)**". It's usually located towards the bottom of the flow canvas. You'll also see a comment node next to it titled "API Key Configuration".
3.  **Edit the Inject Node**:
    - Double-click on the "SET DMI API KEY HERE (Edit to add your key)" Inject node to open its configuration dialog.
    - In the "Payload" field, you will see the default value `"YOUR_DMI_API_KEY_HERE"`.
    - **Replace this default value with your actual DMI API key.** Make sure your API key is enclosed in double quotes (it should be a string).
    - Click the "**Done**" button in the Inject node's configuration dialog.
4.  **Deploy Changes**:
    - Click the main "**Deploy**" button in the Node-RED editor (usually red, in the top-right corner).

The flow will now use the API key you provided. This Inject node is configured to run once when the flow starts or is deployed, setting your API key for the DMI requests.
