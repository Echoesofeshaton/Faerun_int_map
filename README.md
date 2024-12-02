README: Interactive Sword Coast Map

Overview

This project provides an interactive map of the Sword Coast from the Dungeons & Dragons universe. The map is built using Leaflet.js, a popular open-source JavaScript library for creating interactive maps. Instead of using geographical coordinates, this map uses a high-resolution image of the Sword Coast as the background, with support for custom pins and note-taking functionality. Notes are saved locally using the browser’s localStorage.

Features

	1.	Custom Image Map:
	•	Utilizes a high-resolution map of the Sword Coast.
	•	Boundaries of the map correspond to the image dimensions (10,200 x 6,600).
	2.	Interactive Pins:
	•	Users can click anywhere on the map to place a draggable pin.
	•	Each pin supports a popup where users can write, save, and edit notes.
	3.	Note Persistence:
	•	Notes are saved using the browser’s localStorage and remain accessible even after the page is refreshed.
	4.	Responsive Design:
	•	Works across various devices and screen sizes.

File Structure

	•	index.html: Contains the core HTML, CSS, and JavaScript for rendering the map and implementing its features.

How It Works

1. Image Integration

	•	The map uses a custom image hosted at:

https://media.wizards.com/2015/images/dnd/resources/Sword-Coast-Map_HighRes.jpg


	•	The image is loaded as an overlay using Leaflet’s L.imageOverlay feature.
	•	The CRS.Simple coordinate reference system is used, which treats the image as a flat surface.

2. Map Bounds

	•	The dimensions of the image (10,200 x 6,600) are used to define the boundaries of the map:

const bounds = [
  [0, 0], // Top-left corner
  [mapHeight, mapWidth] // Bottom-right corner
];



3. Custom Pins

	•	Users can click anywhere on the map to add a pin:

map.on('click', function (event) {
  const { lat, lng } = event.latlng;
  const marker = L.marker([lat, lng], { draggable: true }).addTo(map);
});


	•	Pins are draggable and open a popup that includes a textarea for adding notes.

4. Notes and Local Storage

	•	Notes are stored in the browser’s localStorage using a unique key based on the pin’s coordinates:

function saveNotes(lat, lng, notes) {
  const key = `pin-${lat}-${lng}`;
  localStorage.setItem(key, notes);
}


	•	When a popup opens, the code retrieves saved notes for the corresponding pin.

Integrations

	1.	Leaflet.js:
	•	A lightweight open-source library for creating interactive maps.
	•	Version: 1.9.4.
	•	Included via CDN:

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>


	2.	Local Storage:
	•	The browser’s localStorage is used to save and retrieve notes for pins.

How to Use

	1.	Open the index.html file in any modern web browser.
	2.	Explore the map:
	•	Add a Pin: Click on any point on the map to place a custom pin.
	•	Add Notes: Click on the pin to open a popup, then enter and save notes.
	•	Edit Notes: Open the popup again to modify and save notes.
	3.	Refresh the page to ensure notes persist.

Customization

Change the Image Map

	•	Replace the URL in the imageUrl variable with the URL of your own image:

const imageUrl = "YOUR_IMAGE_URL";



Adjust Map Bounds

	•	Modify the mapWidth and mapHeight to match the dimensions of your new image:

const mapWidth = IMAGE_WIDTH;
const mapHeight = IMAGE_HEIGHT;

Known Issues

	•	Pins and notes are specific to the user’s browser. They won’t transfer between devices.
	•	Saving a large number of pins may impact performance depending on the browser’s local storage limits.

Attributions

	1.	Leaflet.js:
	•	Leaflet.js Official Documentation
	•	License: BSD-2-Clause License
	2.	Sword Coast Map:
	•	Image by Wizards of the Coast.
	•	Source: Sword Coast Map
	3.	JavaScript Concepts:
	•	Local Storage API: MDN Web Docs

License

This project is open source and distributed under the MIT License. See the LICENSE file for more details.

Future Improvements

	1.	Implement a database backend for cross-device note storage.
	2.	Add functionality to remove pins.
	3.	Improve the UI with more advanced styling for popups and notes.

Enjoy exploring the Sword Coast!
