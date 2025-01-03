# Proxy Smart Monitor

A robust Google Apps Script solution for monitoring multiple proxy servers and logging their performance metrics to Google Sheets. This tool provides real-time monitoring of proxy health, response times, and comprehensive performance analytics.

## 🌟 Features

- Automated proxy health monitoring
- Response time tracking and analysis
- Detailed logging in Google Sheets
- Performance metrics and statistics
- Configurable monitoring intervals
- Automatic error detection and reporting
- Summary dashboard with key metrics

## 📊 Monitoring Capabilities

The script monitors several key metrics for each proxy:
- Connection status (Working/Failed)
- Response time in milliseconds
- Error messages for failed connections
- Historical performance data
- Failure rate analysis
- Average latency calculations

## 📈 Data Organization

The script creates and maintains two sheets:

### Proxy Details Sheet
Contains detailed information for each proxy check:
- Timestamp of the check
- IP address and port
- Connection status
- Response time
- Error messages (if any)

### Proxy Summary Sheet
Provides aggregated statistics:
- Total number of proxies
- Count of working proxies
- Count of failed proxies
- Average response time
- Overall failure rate

## 🚀 Setup Instructions

1. Create a new Google Apps Script project
2. Copy the contents of `monitorProxies.js` into your script editor
3. Configure your proxy settings in the `proxies` array:
```javascript
const proxies = [
  { 
    ip: "ip-proxy1", 
    port: 6540, 
    username: "user", 
    password: "pass" 
  },
  // Add more proxies as needed
];
```
4. Set up your preferred monitoring interval in the `scheduleMonitoring` function:
```javascript
function scheduleMonitoring() {
  ScriptApp.newTrigger("monitorProxiesAndLogToSheet")
    .timeBased()
    .everyMinutes(15)  // Adjust frequency as needed
    .create();
}
```

## 💻 Usage

1. Run the `scheduleMonitoring` function once to set up automatic monitoring
2. The script will automatically:
   - Check all configured proxies
   - Log results to the Details sheet
   - Update summary statistics
   - Generate performance metrics

## ⚙️ Configuration Options

You can customize several aspects of the monitoring:
- Test URL: Modify the `testUrl` constant to test against different endpoints
- Monitoring frequency: Adjust the interval in `scheduleMonitoring`
- Proxy list: Add or remove proxies from the `proxies` array

## 📝 Notes

- The script uses Google Apps Script's `UrlFetchApp` for making requests
- All timestamps are in your spreadsheet's timezone
- Error handling is built in for reliable operation
- The script automatically creates necessary sheets if they don't exist

## 🔒 Security Considerations

- Proxy credentials are stored in the script
- Access to the Google Sheet should be properly restricted
- Consider encrypting sensitive information
- Regular auditing of access logs is recommended

## 🤝 Contributing

Feel free to contribute to this project by:
1. Forking the repository
2. Creating a feature branch
3. Committing your changes
4. Opening a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
