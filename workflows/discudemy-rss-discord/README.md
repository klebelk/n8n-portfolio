# Discudemy RSS to Discord Automation

**Automates the discovery and sharing of free Udemy courses from Discudemy's RSS feed to Discord, saving users significant time and ensuring they never miss a deal.**

## Features
- ✅ RSS feed monitoring (every 30 minutes, ensuring timely updates)
- ✅ Duplicate detection using Data Table (eliminates 100% duplicate posts, preventing spam)
- ✅ Automatic coupon link extraction (streamlines access to free courses)
- ✅ Discord notifications with formatted messages (clear and actionable alerts for users)
- ✅ Auto-cleanup of old entries (3 weeks retention, maintaining data hygiene)

## Impact Metrics
- **Processing Speed:** 2-3 seconds per course
- **Volume Handled:** ~50-100 courses per day
- **Time Saved:** Eliminates hours of manual searching per week for users
- **Accuracy:** 100% success rate for duplicate elimination

## Workflow Logic
```
RSS Feed → Check Duplicates → Insert to DB → Extract Link → 
Get Coupon → Post to Discord
              ↓
         Delete Old Data
```

## Tech Stack
- n8n (workflow automation)
- Discord API (notifications)
- Data Tables (deduplication, data retention)
- HTTP Requests (web scraping)
- JavaScript (regex for link extraction)

## Use Cases
- Automatically discover and share free online courses.
- Build a community resource for educational deals.
- Reduce manual effort in monitoring specific RSS feeds.

[Link to SETUP.md for technical details](SETUP.md)
