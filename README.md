# YapperBot

## Project Overview

YapperBot is a high-performance Telegram bot that delivers real-time Twitter/X analytics and leaderboard statistics through an intelligent web scraping architecture. Built from scratch with a focus on scalability and performance, the bot features an advanced browser pool system, comprehensive admin controls, and optimized async operations to handle concurrent user requests efficiently. This project demonstrates production-grade Python development, complex state management, and real-time data processing.

## Tech Stack

- **Backend Framework**: Python 3.8+ with asyncio for concurrent request handling
- **Telegram Integration**: python-telegram-bot 20.7 (async API)
- **Web Scraping**: Playwright (Chromium automation with headless browser pool)
- **Database**: SQLite with custom ORM layer for user analytics and caching
- **Architecture**: Event-driven async architecture with connection pooling
- **State Management**: In-memory user session tracking with TTL-based cleanup
- **Deployment**: Process management with systemd, environment-based configuration
- **Security**: Encrypted credential storage, admin authentication layer, rate limiting

## Key Features

- **Real-Time Statistics Scraping**: Fetch comprehensive Twitter/X analytics including leaderboard rankings, mindshare percentages, and historical performance data
- **Intelligent Browser Pool**: Pre-loaded page management system that reduces scrape time by 80% through connection reuse and smart state management
- **Admin Control Panel**: Full-featured admin interface for user management, analytics tracking, broadcast messaging, and data export capabilities
- **Animated Status Updates**: Progressive loading indicators that provide real-time feedback during long-running scrape operations
- **Session History**: Persistent search history with quick-access buttons for recently viewed profiles
- **Concurrent Request Handling**: Thread-safe request queuing with per-user concurrency controls to prevent resource exhaustion
- **Robust Error Recovery**: Automatic retry logic with exponential backoff, DOM error handling, and graceful degradation

## Performance & Optimization

Built with performance as a first-class concern. Implemented a custom browser pool manager that maintains warm Playwright instances, reducing cold-start scraping time from 15+ seconds to under 3 seconds. Async operations throughout the stack ensure the bot remains responsive even under heavy load, with non-blocking I/O for database operations and web scraping tasks running concurrently.

The scraper uses intelligent parsing algorithms that extract structured data from dynamic web content without relying on external APIs. Optimized selector strategies and minimal wait times balance speed with reliability, while DOM caching and selective reloading minimize unnecessary network overhead.

Database operations leverage indexed lookups and connection pooling to maintain sub-50ms query times. User session data is stored in-memory with time-based expiration to reduce database load, while persistent storage captures long-term analytics for admin insights.

## Architecture Overview

The project follows a modular component-driven architecture with clear separation of concerns:

- **Bot Layer** ([bot.py](bot.py)): Handles Telegram webhook events, message routing, and user interaction flows with inline keyboard management
- **Admin Layer** ([admin_handlers.py](admin_handlers.py), [admin_panel.py](admin_panel.py)): Isolated admin functionality with role-based access control and comprehensive management interfaces
- **Scraper Module** ([scraper.py](scraper.py)): Encapsulates all web scraping logic with custom text parsing and intelligent retry mechanisms
- **Browser Pool** ([browser_pool.py](browser_pool.py)): Connection pooling system that manages lifecycle of headless browser instances
- **Database Layer** ([database.py](database.py)): Abstraction layer for all persistence operations with prepared statements and transaction management
- **Configuration** ([config.py](config.py)): Environment-based configuration with secure credential handling

State management uses a hybrid approach: ephemeral user sessions in memory for active requests, persistent database storage for analytics and history. Environment variables manage all secrets and deployment-specific configuration—no credentials are committed to version control.

**Note**: Full implementation source code for the production scraping algorithms and browser automation strategies remains private.

## Development Challenges & Solutions

**Built a custom browser pool system** to solve the cold-start problem inherent in headless browser automation. Playwright instances typically take 10-15 seconds to initialize and navigate to target pages. Implemented a warm pool that pre-loads browsers and maintains them in a ready state, reducing average request time by 80%.

**Implemented thread-safe concurrent request handling** with per-user rate limiting to prevent system overload while maintaining responsive UX. Designed a non-blocking queue system that processes requests asynchronously while providing real-time progress updates through animated Telegram messages.

**Engineered intelligent DOM parsing algorithms** that extract structured data from dynamically rendered content without relying on fragile CSS selectors. Built a robust text-parsing system with multiple fallback strategies to handle site layout changes gracefully.

**Optimized database schema and query patterns** for high-read, low-write workloads typical of analytics tracking. Implemented selective indexing and connection pooling to maintain consistent sub-50ms query performance.

**Designed a scalable admin control panel** with role-based permissions, broadcast messaging, and comprehensive analytics dashboards—all within Telegram's inline keyboard constraints.

**Solved Markdown escaping challenges** in Telegram's message parser by implementing context-aware character escaping that preserves readability while preventing parse errors on user-generated content.

## Contact

I'm a backend engineer with expertise in Python, async systems, web automation, and scalable bot architectures. If you're looking for high-quality automation solutions, Telegram bot development, or backend engineering support, let's connect.

**GitHub**: [github.com/reza7277](https://github.com/reza7277)

---

**Disclaimer**: This bot is developed for educational and portfolio purposes. Users should ensure compliance with relevant Terms of Service when scraping public web data.
