# conviva-roku-appinsights
## Conviva Application Insights Sensor for Roku
Use Application Insights to autocollect events, track application specific events and state changes, and track users anonymously.

## Usage
To use the video sensor, download the Conviva Roku Sensor (version 3.4.9 or above) from Conviva Roku Sensor Integration and unzip the downloaded file.
https://pulse.conviva.com/learning-center/content/sensor_developer_center/sensor_integration/roku/roku_stream_sensor_download.htm

### Download
To use the application sensor
1. unzip conviva_roku_app_sensor.zip from the current repository
2. Copy the following folders and files to your Roku project:
    - Contents of `source` into your `source` directory
    - Contents of `components` into your `components` directory


### Component Initialization

It is recommended that you instantiate Conviva Tracker and add it to the global scope. In this way, it will be accessible from anywhere within your SceneGraph application.
You may create the instance in the `init` function of your main scene.

Mount the component as follows:

```brs
m.global.AddField("appTracker", "node", false)
m.global.appTracker = CreateObject("roSGNode", "CAT")
```
### Initialize the tracker
Trackers are initialized by setting the `init` property with configuration of the tracker. Below is an example configuration

```brs
m.global.appTracker.init = {
    subject: {
        appId: "<<YOUR_APP_ID_ADVISED_BY_Conviva>>",
        convivaCustomerKey: "YOUR_CUSTOMER_KEY_ADVISED_BY_Conviva",
    },
    namespace: "CAT",
    network: {
        collector: "<<YOUR_APPGW_URL_ADVISED_BY_CONVIVA>>",
    }
}
```

### Report Screen View for tracking in-app screen navigations.
```brs
m.global.appTracker.CAT.screenView = {
    id: "videoscene", 'Optional' ' A unique ID to identify the screen'
    name: "Video Gallery Screen" ' Name. / Description of the screen'
}
```

### Custom event tracking to track your application specific events and state changes
Use trackCustomEvent() API to track all kinds of events. This API provides 2 fields to describe the tracked events.

name - Name of the custom event. (Mandatory)

data - Any type of data in string format.

The following example shows the implementation of the 'Click / Select' event listener to any UI component.
```brs
custom_data_json = {
  "identifier1": "test",
  "identifier2": 1,
  "identifier3":true
}

m.global.appTracker.convivaAppTracker.trackCustomEvent =  {
    name: "CustomEvent", ' Name. / Description of the screen'
    data: formatJSON(custom_data_json)
}
```
