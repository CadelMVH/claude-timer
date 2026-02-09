# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A standalone HTML page displaying current time with a responsive gradient background. Shows:
- Current time in 12-hour format with seconds
- Full date with weekday
- Dynamic greeting based on time of day

## Running the Project

Open `archive/timer.html` in any modern web browser for local testing. No build process, bundlers, or dependencies required.

## Project Structure

- `docs/index.html` - Main application (published via GitHub Pages)
- `archive/timer.html` - Local copy for development/testing
- `docs/.nojekyll` - GitHub Pages configuration
  - CSS styles embedded in `<style>` tags
  - JavaScript logic embedded in `<script>` tags

## Architecture Notes

- Time updates every second via `setInterval` (1000ms)
- Responsive design with breakpoint at 600px
- Time formatting converts to 12-hour format with AM/PM
- Uses English locale (`en-US`) for date display