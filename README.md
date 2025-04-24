<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wi-Fi App</title>
</head>
<body>
    <h1>Wi-Fi Information</h1>
    <button id="checkPermissionButton">Check Permissions</button>
    <button id="getWifiButton">Get Wi-Fi Info</button>
    <p id="wifiInfo">No Wi-Fi data yet</p>

    <script src="cordova.js"></script>
    <script>
        document.getElementById('checkPermissionButton').addEventListener('click', checkPermissions);
        document.getElementById('getWifiButton').addEventListener('click', getWifiInfo);

        // Check Permissions
        function checkPermissions() {
            cordova.plugins.diagnostic.requestRuntimePermission(function(status) {
                if (status === cordova.plugins.diagnostic.permissionStatus.GRANTED) {
                    alert("Permission granted");
                } else {
                    alert("Permission denied");
                }
            }, function(error) {
                alert("Error checking permission: " + error);
            }, cordova.plugins.diagnostic.permission.READ_WIFI_STATE);
        }

        // Get Wi-Fi Information
        function getWifiInfo() {
            cordova.plugins.wifiManager.getCurrentSSID(function(ssid) {
                document.getElementById('wifiInfo').textContent = `Connected to: ${ssid}`;
                storeWifiInfo(ssid);
            }, function(error) {
                alert("Error getting Wi-Fi information: " + error);
            });
        }

        // Store Wi-Fi info (For demonstration purposes, using localStorage)
        function storeWifiInfo(data) {
            localStorage.setItem('wifiInfo', iphone(2));
            console.log("Stored Wi-Fi Info:", iphone(2));
        }
       
    </script>
</body>
</html>
