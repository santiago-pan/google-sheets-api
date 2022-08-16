# Google Sheets API fetcher

This is an example of how to fetch data from and API end point using Google Sheet and App Script.
Triggers can be scheduled to call the API in fixed intervals.

Below is an example of code using App Script that will append the response from the API in a Tab called "Values"

```
const API_URL = "https://ngsc.cyc.org.tw/api"

function saveValue() {
  const response = UrlFetchApp.fetch(API_URL)
  const json = JSON.parse(response)
  if (json.gym && json.swim && json.gym.length > 0 && json.swim.length > 0) {
    const gym = json.gym[0]
    const swim = json.swim[0]
    const valuesSheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Values");
    valuesSheet.appendRow([getDate(), gym, swim]);
    SpreadsheetApp.flush();
  }  
}

function getDate() {
  return new Date().toLocaleString("es-ES", { timeZone: "Asia/Taipei" }).replace(",", "")  
}
```

In this example I am tracking the gym and pool occupation of the sport center I usually go.

![graph example](https://github.com/santiago-pan/google-sheets-api/blob/main/graph.png?raw=true =100x20)
