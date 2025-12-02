# ESP32 Data Logger

A web-based data logging system that receives sensor data from ESP32 devices and displays it in a spreadsheet format.

## Features

- Receive data from ESP32 via HTTP POST requests
- Display data in an interactive spreadsheet
- Export data to CSV
- Real-time data updates
- Simple REST API

## Project Structure

```
esp32-data-logger/
├── server/
│   ├── server.js           # Node.js Express server
│   ├── package.json        # Node.js dependencies
│   └── data.json          # Data storage file
├── public/
│   ├── index.html         # Main web interface
│   ├── style.css          # Styles
│   └── script.js          # Frontend JavaScript
├── esp32/
│   └── esp32_sender.ino   # Arduino code for ESP32
└── README.md
```

## Setup Instructions

### Server Setup

1. Install Node.js (v14 or higher)

2. Navigate to the server directory:
```bash
cd server
npm install
```

3. Start the server:
```bash
node server.js
```

The server will run on `http://localhost:3000`

### ESP32 Setup

1. Open `esp32/esp32_sender.ino` in Arduino IDE
2. Update WiFi credentials:
   - `ssid`: Your WiFi network name
   - `password`: Your WiFi password
3. Update `serverUrl` with your server's IP address
4. Upload to your ESP32

## API Endpoints

### POST /api/data
Send data from ESP32 to the server.

**Request Body:**
```json
{
  "deviceId": "ESP32-001",
  "temperature": 25.5,
  "humidity": 60.2,
  "value1": 100
}
```

### GET /api/data
Retrieve all logged data.

**Response:**
```json
[
  {
    "id": 1,
    "timestamp": "2024-12-02T10:30:00.000Z",
    "deviceId": "ESP32-001",
    "temperature": 25.5,
    "humidity": 60.2,
    "value1": 100
  }
]
```

### DELETE /api/data
Clear all data.

## Usage

1. Power on your ESP32 (it will automatically connect to WiFi and start sending data)
2. Open `http://localhost:3000` in your browser
3. View incoming data in the spreadsheet
4. Click "Refresh Data" to manually update
5. Click "Export CSV" to download data
6. Click "Clear Data" to reset the database

## Customization

### Adding More Data Fields

**In ESP32 code:**
```cpp
// Add your sensor readings
doc["newField"] = yourValue;
```

**In server.js:**
Columns are automatically detected from incoming data.

**In index.html:**
The spreadsheet will automatically show new columns.

## License

MIT License
