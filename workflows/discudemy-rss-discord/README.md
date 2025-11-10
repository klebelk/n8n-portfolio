# Discudemy RSS to Discord Automation

## Overview
Automated workflow that monitors Discudemy's RSS feed for free Udemy courses, extracts discount coupon links, and posts them to Discord with deduplication.

## Problem Solved
Manually checking for free Udemy courses is time-consuming. This workflow automatically finds, processes, and shares course deals in real-time.

## Features
- ✅ RSS feed monitoring (every 30 minutes)
- ✅ Duplicate detection using Data Table
- ✅ Automatic coupon link extraction
- ✅ Discord notifications with formatted messages
- ✅ Auto-cleanup of old entries (3 weeks retention)

## Workflow Logic



\`\`\`
RSS Feed → Check Duplicates → Insert to DB → Extract Link → 
Get Coupon → Post to Discord
              ↓
         Delete Old Data
\`\`\`

## Key Nodes

1. **RSS Feed Trigger** - Monitors Discudemy feed twice per hour
2. **Get Link** - Checks if course already posted (deduplication)
3. **Check If Processed** - Conditional logic for new courses only
4. **Insert to Data Table** - Stores course info in Data Table
5. **Take Course Link** - Extract course slug & parse coupon links
6. **HTTP Request** - Fetches course page HTML
7. **Get Discount Link** - Posts formatted message with link
8. **Delete Old Data** - Removes entries older than 3 weeks

## Technical Highlights

### Deduplication System
Uses n8n Data Table to track posted courses and prevent spam.

### Link Processing
Transforms RSS links into direct course pages:
\`\`\`
https://www.discudemy.com/python/course-name/
    ↓
https://www.discudemy.com/go/course-name
\`\`\`

### Regex Extraction
\`\`\`javascript
const match = html.match(/https:\/\/www\.udemy\.com\/course\/[^"]+couponCode=[^"]+/);
\`\`\`

## Metrics
- Processes ~50-100 courses per day
- Eliminates 100% duplicate posts
- Average processing time: 2-3 seconds per course

## Portfolio Value
Demonstrates: RSS parsing, web scraping, conditional logic, database operations, Discord API, data retention policies, regex pattern matching
