---
title: "Projects"
---

<div class="hero" markdown="1">

# 💻 Projects

Tools and scripts I've actually built and used — IT automation, home automation, data scraping, and a couple of just-for-fun ones. Source for most of these lives in private repos right now.

</div>

## 🛠️ Automation & IT Tooling

<div class="card-grid" markdown="1">

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### KACE Device Check-In Automator
Forces devices running KACE Agent 9.0+ that have been offline 14+ days to check back into the KACE server — reads a device list from CSV, pings each one, and kicks off an inventory update for anything that responds.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">IT Automation</span>
  <span class="tag">CSV</span>
</div>
</div>

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### Windows Event Log Analyzer
Pulls Windows Event Log data — either live from a local machine or from exported log files — and exports it to CSV, with sorting by column for faster triage.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">Windows</span>
  <span class="tag">Forensics</span>
</div>
</div>

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### Windows Temp File Cleanup Script
Sweeps specified drives for `.tmp`, `.dmp`, and `.hdmp` files and clears them out, logging what was found and what got deleted for an audit trail.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">Windows</span>
  <span class="tag">Disk Cleanup</span>
</div>
</div>

</div>

## 🏠 IoT & Home Automation

<div class="card-grid" markdown="1">

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### Fan Automation: IoT for Home
Automates fan control based on temperature and humidity to cut down on wasted electricity during hot summer days — reads a DHT11 sensor, drives a Sonoff S31 Lite Zigbee smart plug, and factors in time-of-day and local weather data.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">IoT</span>
  <span class="tag">Zigbee</span>
  <span class="tag">Home Automation</span>
</div>
</div>

</div>

## 🎬 Data & Movie Scraping

<div class="card-grid" markdown="1">

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### TMDb Horror Movie Scraper
Queries The Movie Database API for movies in a given genre, paging through all results and saving titles to CSV — built as the first stage of a movie-data pipeline.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">TMDb API</span>
  <span class="tag">Data</span>
</div>
</div>

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### IMDb Movie Info Scraper
Takes a CSV of movie titles (typically from the TMDb scraper) and enriches each one with IMDb rating, vote count, and genre data via IMDbPY, skipping titles it's already fetched.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">IMDbPY</span>
  <span class="tag">Data</span>
</div>
</div>

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### Rotten Tomatoes Scraper
Final stage of the movie pipeline — scrapes audience/critic scores, review counts, and streaming availability from Rotten Tomatoes and appends it to the CSV.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">Web Scraping</span>
  <span class="tag">Data</span>
</div>
</div>

</div>

## 🎮 Gaming Tools

<div class="card-grid" markdown="1">

<div class="card" markdown="1">
<span class="badge done">✅ Complete</span>

### OSRS Calculators
A Tkinter GUI calculator for Old School RuneScape ranged combat — DPS, XP/hour, and estimated time to a target level, accounting for attack style and Void/Elite Void bonuses. Built while actively playing; kept public in case it's useful to someone else.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">Tkinter</span>
  <span class="tag">Gaming</span>
</div>
</div>

</div>

## 🎵 Personal / AI-Assisted

<div class="card-grid" markdown="1">

<div class="card" markdown="1">
<span class="badge progress">📝 In Progress</span>

### sound-forager
Personal tooling for a tagged, organized local music library, paired with a Claude Code skill that fans out subagents to find and fetch new tracks from several distinct discovery angles instead of one algorithm's favorites.

<div class="tag-row">
  <span class="tag">Python</span>
  <span class="tag">yt-dlp</span>
  <span class="tag">Claude Code Skill</span>
</div>
</div>

</div>

<p class="private-note">🔒 Source for these lives in private repos right now — happy to share access on request.</p>

---

*More projects get added here as they're built. Feel free to check out everything else on [GitHub](https://github.com/SomeRandomStranger123?tab=repositories).*
