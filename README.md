# Modified for moving boat.. 

Request update every 1 hours or 5 nm of movement: Done with extensive use of Cursor AI https://www.cursor.com/ 


<img src=https://github.com/allancph/node-red-DMI-API-forecast/blob/main/Sk%C3%A6rmbillede%202025-02-12%20kl.%2015.09.06.png width="50%" height="50%" />

# node-red-DMI-API-forecast
Node-Red flow to retrieve a 5 day weather forecast from DMI, Danish Meteorological Institute

<img src=https://user-images.githubusercontent.com/16189982/234341251-d8ef8c74-9044-4fd8-9600-31c7bf81fd15.png width="50%" height="50%" />


<img src=https://user-images.githubusercontent.com/16189982/234339735-ddf5c793-6803-4dfa-a801-3e68ba283ae4.png width="30%" height="30%" />

Full documentation available at https://pysselilivet.blogspot.com/2023/04/dmi-forecast-api-for-atmosphere-ocean.html

## Configuration

This flow requires a DMI API key to fetch weather data.

1.  **Create a Configuration File:**
    Create a file named `config.json` in the root directory of this project (alongside `DMI_moving.json`).

2.  **Add API Key:**
    Open `config.json` and add your DMI API key in the following format:
    ```json
    {
      "dmiApiKey": "YOUR_ACTUAL_DMI_API_KEY"
    }
    ```
    Replace `"YOUR_ACTUAL_DMI_API_KEY"` with your real API key.

3.  **Make API Key Available to Node-RED:**
    You need to make this API key available in Node-RED's global context. This is typically done by editing your Node-RED `settings.js` file (usually located in your Node-RED user directory, e.g., `~/.node-red/settings.js`).

    Add the following to the `functionGlobalContext` section in `settings.js`:

    ```javascript
    functionGlobalContext: {
        // ... other global context settings ...
        // dmiApiKey: process.env.DMI_API_KEY, // Option 1: Load from an environment variable

        // Option 2: Load from the config.json file.
        // Adjust the path to config.json to be the absolute path
        // to where you've cloned/placed this project.
        // For example, if this project is in '/home/user/node-red-DMI-API-forecast/',
        // the path would be '/home/user/node-red-DMI-API-forecast/config.json'.
        // If running Node-RED in Docker and this project is mounted at /data,
        // then the path might be '/data/config.json'.
        // The example below assumes the project is in '/app/node-red-DMI-API-forecast/'.
        dmiApiKey: (function() {
            const fs = require('fs');
            const configPath = '/app/config.json'; // IMPORTANT: Change this to the ABSOLUTE path to your config.json
            if (fs.existsSync(configPath)) {
                try {
                    return require(configPath).dmiApiKey;
                } catch (e) {
                    node.error("Error reading dmiApiKey from config.json: " + e);
                    return null;
                }
            } else {
                node.warn("config.json not found at: " + configPath);
                return null;
            }
        })()
        // ... other global context settings ...
    },
    ```
    **Important:**
    *   Replace the example path in `configPath` with the correct **absolute path** to the `config.json` file within your Node-RED environment.
    *   You only need one method to set `dmiApiKey` (either from `process.env` or by reading `config.json`). Choose the one that suits your setup.
    *   Ensure `fs` and `path` (if you choose to build path dynamically) modules are available in your `settings.js` context if you use them. `fs` is usually available.

    After editing `settings.js`, **restart Node-RED** for the changes to take effect.

The flow uses `{{global.dmiApiKey}}` in the HTTP request nodes to access your key. If the key is not configured, the API calls will likely fail.
