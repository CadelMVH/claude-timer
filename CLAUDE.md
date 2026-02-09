# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a simple, standalone HTML page that displays the current time with a responsive gradient background design. It shows:
- Current time in 12-hour format with seconds
- Full date with weekday
- Dynamic greeting based on time of day

## Running the Project

Simply open `timer.html` in any modern web browser. No build process, bundlers, or dependencies are required.

## Project Structure

- `timer.html` - Single HTML file containing all CSS, HTML, and JavaScript in one document
  - CSS styles are embedded in `<style>` tags
  - JavaScript logic is embedded in `<script>` tags

## Development Notes

- The application updates time every second using `setInterval`
- Responsive design adapts to screen sizes (max-width: 600px)
- Time is displayed in 12-hour format with AM/PM
- Uses English locale for date formatting