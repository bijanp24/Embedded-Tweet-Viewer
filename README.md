# Embedded Tweet Viewer

A clean, responsive, single-page HTML template designed to display a specific X (formerly Twitter) embed. 

## Included Files

* `index.html`: The main web page containing the layout, CSS styling, and the embedded tweet code.
* `README.md`: Documentation for the project.

## Getting Started

1. Save both files into the same folder on your computer.
2. Double-click `index.html` to open it in your default web browser (Chrome, Safari, Firefox, Edge, etc.).
3. **Note:** You must have an active internet connection for the tweet to render properly. The browser needs to fetch the `widgets.js` script directly from X's servers to convert the blockquote into a fully styled, interactive embed.

## Modifying the Content

If you want to swap out the tweet in the future:
1. Open `index.html` in a text editor (like VS Code, Notepad, or TextEdit).
2. Locate the `<!-- Embedded Tweet Start -->` section.
3. Replace the `<blockquote ...>` and `<script ...>` tags with your new embed code from X.
4. Save the file and refresh your browser.