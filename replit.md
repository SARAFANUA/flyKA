# FlyKA Tracker - GPS/GNSS Route Analyzer

## Overview
FlyKA Tracker is a web-based GPS/GNSS route analyzer that visualizes and analyzes route data from CSV and XLSX files on an interactive Leaflet/OpenStreetMap map. The application allows users to upload tracking data, visualize routes, analyze timestamps, and filter by dates.

## Recent Changes
- **October 20, 2025**: Configured for Replit environment
  - Modified routing service to work without OSRM backend (uses straight lines between points)
  - Set up Python HTTP server on port 5000
  - Updated .gitignore for Python and Replit environment
  - Created deployment configuration

## Project Architecture

### Technology Stack
- **Frontend**: Pure HTML, CSS, JavaScript (ES6 modules)
- **Mapping**: Leaflet.js with OpenStreetMap tiles
- **File Processing**: PapaParse (CSV), SheetJS (XLSX)
- **Clustering**: Leaflet.markercluster
- **Server**: Python HTTP server (for static file serving)

### File Structure
```
├── index.html              # Main application page
├── css/
│   └── style.css          # Application styles
├── js/
│   ├── main.js            # Main application logic
│   ├── api/
│   │   └── routingService.js    # OSRM routing (disabled)
│   ├── map/
│   │   ├── mapInitializer.js    # Leaflet map setup
│   │   ├── mapLayers.js         # Map layer management
│   │   └── markerRenderer.js    # Route rendering
│   ├── parser/
│   │   ├── csvParser.js         # CSV file processing
│   │   ├── xlsxParser.js        # Excel file processing
│   │   ├── fileHandler.js       # File upload handling
│   │   ├── geoParser.js         # GPS data parsing
│   │   └── zipParser.js         # ZIP file support
│   └── utils/
│       ├── colorUtils.js        # Route color generation
│       ├── dataNormalizer.js    # Data normalization
│       └── uiControls.js        # UI interaction handlers
└── osrm-data/             # (Excluded) OSRM routing data
```

### Key Features
1. **File Upload**: Drag-and-drop or browse for CSV/XLSX files containing GPS data
2. **Route Visualization**: Display multiple routes on the map with different colors
3. **Clustering**: Toggle marker clustering for better performance with many points
4. **Vehicle Types**: Support for car, truck, foot, and train route profiles
5. **Date Filtering**: Filter route points by specific dates
6. **Route Details**: View detailed information about each route point including timestamps and durations
7. **Interactive Map**: Zoom, pan, and click on route segments for details

### OSRM Configuration
The original project was designed to use OSRM (Open Source Routing Machine) for route optimization. OSRM is optional and can be configured by setting `window.OSRM_BASE_URL` in the HTML file or browser console.

**Default behavior (Replit)**: OSRM is disabled by default. The application uses straight lines between GPS points, which is suitable for visualization purposes.

**To enable OSRM**: 
1. Set up an OSRM server (requires large binary data files - see original README.md)
2. Uncomment and configure the `window.OSRM_BASE_URL` setting in index.html
3. Set it to your OSRM server URL (e.g., `http://localhost:5000`)

The application automatically falls back to straight lines if OSRM is unavailable or encounters errors.

## How to Use

1. **Upload Data**: Click "Обрати файли" or drag files into the drop zone
2. **View Routes**: Uploaded routes appear in the sidebar list
3. **Select Route**: Click on a route name to view details
4. **Filter by Date**: Use the date filter at the bottom to show specific days
5. **Adjust Settings**: 
   - Toggle clustering on/off
   - Change vehicle type (affects future OSRM integration)
6. **View Details**: Click the modal button to open route details in a separate window

## Deployment
The application is configured to deploy as an autoscale deployment, running a Python HTTP server to serve static files.

## User Preferences
None documented yet.

## Development Notes
- The application is fully client-side except for the static file server
- All data processing happens in the browser
- No backend database required
- Map tiles are loaded from OpenStreetMap CDN
