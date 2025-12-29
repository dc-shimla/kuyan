# KUYAN - Monthly Net Worth Tracker

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Python](https://img.shields.io/badge/python-3.11+-green.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

A local Python/Streamlit application to track net worth across multiple accounts and currencies. Privacy-focused with local-only data storage - your financial data never leaves your machine. Suitable for families, individuals, and businesses.

**About the Name:** KUYAN is short for "Kuber Yantra" - inspired by Kuber (the Hindu deity of wealth) and Yantra (a tool or instrument), symbolizing a tool for wealth management.

<p align="left">
  <img src="assets/logo.png" alt="KUYAN Logo" width="90"/>
</p>

**Current Version:** 1.0.0 (see [VERSION](VERSION) file)

## Try the Live Demo

Experience KUYAN without installation:

- **[Demo with Sample Data](https://kuyan-demo.streamlit.app/?mode=sandbox)** - Pre-populated with 24 months of financial data using a sandbox database. Perfect for exploring features and testing functionality.
- **[Blank Demo](https://kuyan-demo.streamlit.app/)** - Empty instance to get a feel for the interface.

**Note:** These demos are for exploration only. For production use, please host KUYAN locally following the installation instructions below to ensure your financial data remains private and secure on your machine.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Quick Start](#quick-start)
  - [Docker (Recommended)](#docker-recommended)
  - [Direct Python](#direct-python)
- [Usage Guide](#usage-guide)
- [Database & Data Persistence](#database--data-persistence)
  - [Docker Deployment](#docker-deployment-1)
  - [Direct Python Deployment](#direct-python-deployment)
- [Application Features](#application-features)
- [Database Schema](#database-schema)
- [Data Backup & Recovery](#data-backup--recovery)
- [Versioning](#versioning)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Features

- **Multi-currency support** - Choose 1-9 currencies from 32 options with customizable chart colors
- **Owner management** - Track accounts for family members, companies, trusts, or joint ownership
- **Monthly snapshots** - Record balances once per month with historical accuracy
- **Interactive visualizations** - Line graphs, bar charts, and trend analysis
- **Year-over-year comparison** - Compare financial performance across years
- **Built-in tools** - Calculator, calendar invite generator, exchange rate widget, dashboard export (PDF, PNG, HTML)
- **Real-time currency conversion** - Powered by frankfurter.app API
- **Privacy-first** - All financial data stored locally in SQLite (only exchange rates fetched from API)
- **Sandbox mode** - Pre-loaded demo environment with 24 months of sample data
- **Docker support** - Production-ready containerized deployment

## Tech Stack

- **Python 3.11+** - Application runtime
- **Streamlit** - Web UI framework for interactive web applications
- **SQLite** - Local database (no server needed)
- **Pandas** - Data manipulation and analysis
- **Plotly** - Interactive charts and visualizations
- **requests** - HTTP library for API calls
- **python-dateutil** - Advanced date/time handling
- **frankfurter.app API** - Free currency exchange rates (no API key required)
- **Docker** - Containerization for consistent deployment

---

## Installation

**Clone the repository:**

```bash
git clone https://github.com/dc-shimla/kuyan.git
cd kuyan
```

---

## Quick Start

### Recommended Deployment Methods

**Choose based on your use case:**

1. **For Daily Use** - Use Docker (production-ready, isolated, consistent)

   - Port: `8501`
   - Best for: Regular usage, data tracking, sharing with family
   - Available for: All platforms with Docker Desktop

2. **For Development & Testing** - Use Python directly (fastest setup, easy debugging)
   - Port: `8502`
   - Best for: Code changes, testing, debugging
   - Available for: macOS, Linux, and Windows

---

### Docker (Recommended for Daily Use)

**Requirements:** Docker Desktop installed

**Build and start the app:**

```bash
./scripts/docker-build-no-cache.sh && ./scripts/docker-start.sh
```

**Access:** Open browser to `http://localhost:8501`

**Try Sandbox Mode (Demo with Sample Data):**

```
http://localhost:8501/?mode=sandbox
```

- Pre-loaded with 24 months of sample financial data
- Safe to experiment - changes don't affect your real data
- Reset button available to restore sample data anytime

**Stop:**

```bash
./scripts/docker-stop.sh
```

**Why Docker for Daily Use?**

- **Data isolation**: Database stored in Docker volume, protected from accidental deletion
- **Consistent environment**: Same setup across all systems (Mac, Windows, Linux)
- **No Python conflicts**: Isolated from your system Python installation
- **Production-ready**: Optimized configuration with proper resource limits
- **Easy updates**: Rebuild and restart without affecting your data
- **Sandbox included**: Pre-built demo environment for testing features
- **Version control**: Each build is tagged with version number

---

### Direct Python (Recommended for Development)

**Requirements:** Python 3.11+

**Quick Start:**

**macOS/Linux:**

```bash
./scripts/setup-and-run-python.sh
```

**Windows:**

```cmd
scripts\setup-and-run-python.bat
```

**What these scripts do:**

- Create virtual environment (if needed)
- Install dependencies (if needed)
- Start the application on port 8502

**Access:** Open browser to `http://localhost:8502`

**Try Sandbox Mode (Demo with Sample Data):**

```
http://localhost:8502/?mode=sandbox
```

**Why Python for Development?**

- **Fastest iteration**: No build step required, instant code changes
- **Easy debugging**: Direct access to Python debugger and logs
- **Lower overhead**: No Docker daemon required
- **Quick testing**: Start/stop in seconds
- **Cross-platform**: Works on macOS, Linux, and Windows

#### **Option 1: Quick Start (Recommended)**

**macOS/Linux:**

```bash
./scripts/setup-and-run-python.sh
```

**Windows:**

```cmd
scripts\setup-and-run-python.bat
```

#### **Option 2: Manual Setup**

**1. Navigate to project:**

```bash
cd kuyan
```

**2. Create virtual environment:**

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

**3. Install dependencies:**

```bash
pip install -r requirements.txt
```

**4. Run application:**

```bash
streamlit run app.py --server.port 8502
```

**Access:** Open browser to `http://localhost:8502`

---

## Usage Guide

### Exploring with Sample Data (Recommended)

**Want to try KUYAN before adding your own data?** Use **Sandbox Mode**:

- **Docker**: `http://localhost:8501/?mode=sandbox`
- **Python**: `http://localhost:8502/?mode=sandbox`

Sandbox mode includes:

- Pre-loaded sample data (24 months of historical snapshots)
- 2 sample owners and 4 sample accounts
- Safe to experiment - completely separate from your production data
- Reset button available to restore sample data anytime

### Using the App

1. **Configure Currencies**: Go to "Currencies" to add/remove currencies and customize chart colors
2. **Add Owners**: Navigate to "Owners" to add family members, companies, trusts, or other account holders
3. **Add Accounts**: Go to "Accounts" to add your bank and investment accounts
4. **Update Balances**: Click "Dashboard" then use the snapshot form to record monthly balances
5. **View Dashboard**: Check net worth, charts, and trends
6. **Use Tools**: Access Calculator, Exchange Rates, Calendar Invite, and Export features from the sidebar
7. **Review History**: View and manage past snapshots organized by month and year

---

## Database & Data Persistence

### Docker Deployment

**Production Database:**

- **Location**: `/app/kuyan.db` inside the container
- **Persistence**: Stored in Docker named volume `kuyan_data`
- **Auto-created**: Database is created automatically on first launch
- **Default data**: Two default owners ("Me", "Wife") are pre-added
- **Data safety**: Data persists across container restarts and rebuilds

**Sandbox Database:**

- **Location**: `/app/kuyan-sandbox.db` inside the container
- **Pre-loaded**: Created during Docker build with 24 months of sample data
- **Access**: Visit `http://localhost:8501/?mode=sandbox`
- **Reset**: Use the "Reset Sandbox" button in the app to restore sample data

**Managing Docker Data:**

View volume location:

```bash
docker volume inspect kuyan_data
```

Backup database from Docker volume:

```bash
# Method 1: Using docker exec (if container is running)
docker exec kuyan cat /app/kuyan.db > kuyan-backup-$(date +%Y%m%d).db

# Method 2: Using docker cp (if container is running)
docker cp kuyan:/app/kuyan.db ./kuyan-backup-$(date +%Y%m%d).db
```

Remove volume (⚠️ deletes all data):

```bash
docker compose down -v
```

### Direct Python Deployment

**Production Database:**

- **Location**: `kuyan.db` (project root directory, same location as app.py)
- **Auto-created**: Database is created automatically on first run
- **Default data**: Two default owners ("Me", "Wife") are pre-added
- **Git safety**: Protected by `.gitignore` - will not be committed to repository

**Finding your database:**

```bash
# From project root
ls -la kuyan.db

# Full path (on macOS/Linux)
pwd  # Shows current directory
# Database is at: <current-directory>/kuyan.db
```

**Sandbox Database (Optional):**

```bash
# Create sandbox database with sample data
python3 create_sandbox_db.py

# Creates: kuyan-sandbox.db
# Access via: http://localhost:8502/?mode=sandbox
```

**Reset Production Database:**

```bash
# Stop the app first (Ctrl+C)
rm kuyan.db

# Restart the app - fresh database will be created
streamlit run app.py
```

**Backup Production Database:**

```bash
# Simple backup
cp kuyan.db kuyan-backup-$(date +%Y%m%d).db

# Or use the built-in backup script
./scripts/db-backup.sh
# Creates timestamped backup in backups/ directory
```

---

## Application Features

### Dashboard (📊)

The main dashboard has **three tabs**:

#### 📊 Overview

- Current net worth displayed in all enabled currencies
- Account breakdown table with multi-currency conversion
- Net worth trend chart (line graph showing growth over time)
- Currency-specific holdings growth comparison (bar charts)
- Year-over-year comparison (if 12+ months of data)
- Base currency selector for viewing net worth in different currencies

#### 💰 Update Balances

- Monthly snapshot form for recording balances (grouped by owner)
- Historical balance reference (previous months)
- Year/month selector
- Exchange rate confirmation before saving
- Snapshot overwrite detection

#### 📜 History

- Complete snapshot log organized by year and month
- Monthly net worth totals in your chosen base currency
- Account-by-account balance details grouped by owner
- Currency conversion display for each account
- Snapshot deletion with confirmation

### Sidebar Navigation

**Settings:**

#### Accounts (🏦)

- Add/edit/delete accounts
- Link accounts to owners
- Specify account type (Bank, Investment, Other) and currency
- View accounts organized by owner

#### Currencies (💱)

- Add/remove currencies (1-9 currencies supported)
- Choose from 32 supported currencies
- Customize chart colors (flags are auto-assigned based on currency)
- View which currencies are in use by accounts

#### Owners (👥)

- Add/edit/delete owners
- Owner type classification (Individual, Company, Joint/Shared, Trust, Other)
- Account count indicators
- Cascade update of accounts when owner name changes

**Tools:**

#### Calculator (🧮)

- Quick access financial calculator
- Perform calculations while updating balances

#### Exchange Rate Widget (💹)

- View current exchange rates for all currency pairs
- Fetch latest rates from frankfurter.app API

#### Calendar Invite (📅)

- Generate .ics calendar file for monthly balance updates
- Add attendee emails for shared reminders
- Customizable monthly recurrence

#### Export Dashboard (📥)

- Export dashboard as PNG (Image)
- Export dashboard as PDF (Document)
- Export dashboard as HTML (Interactive)

---

## Database Schema

### Currencies Table

```sql
CREATE TABLE currencies (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    code TEXT NOT NULL UNIQUE,
    flag_emoji TEXT NOT NULL,
    color TEXT NOT NULL,
    display_order INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Initial Default Currencies:**

- CAD (🇨🇦, Crimson Red)
- USD (🇺🇸, Navy Blue)
- INR (🇮🇳, Dark Orange)

_Note: These currencies are automatically added when the database is first created. You can add, remove, or customize them through the Currencies page._

### Owners Table

```sql
CREATE TABLE owners (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL UNIQUE,
    owner_type TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Accounts Table

```sql
CREATE TABLE accounts (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    owner TEXT NOT NULL,
    account_type TEXT NOT NULL,
    currency TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (owner) REFERENCES owners(name)
);
```

### Snapshots Table

```sql
CREATE TABLE snapshots (
    id INTEGER PRIMARY KEY,
    snapshot_date DATE NOT NULL,
    account_id INTEGER NOT NULL,
    balance DECIMAL(15,2) NOT NULL,
    exchange_rates TEXT,
    FOREIGN KEY (account_id) REFERENCES accounts(id)
);
```

**Key Features:**

- Foreign keys with cascade delete for data integrity
- Exchange rates stored with each snapshot for historical accuracy
- Indexed queries on snapshot_date for performance
- Default data seeding (Me, Wife owners on first run)

---

## Data Backup & Recovery

### How Your Data is Stored

All your financial data is stored in a **single SQLite database file**:

```
kuyan.db
```

This file contains:

- All account owners (family members, companies, etc.)
- All accounts (bank accounts, investments, etc.)
- All monthly snapshots (historical balance data)
- All exchange rates (stored with each snapshot)

**Important:** This file is stored **locally on your computer** - NOT in the cloud.

### Backup Strategies

#### Option 1: Manual Backup (Simplest)

**To backup:**

```bash
./scripts/db-backup.sh
```

This creates a timestamped backup in the `backups/` directory:

```
backups/kuyan_backup_20251217_235113.db
```

The script automatically:

- Creates timestamped backups
- Keeps the last 30 backups
- Deletes older backups automatically

**To restore:**

```bash
./scripts/db-restore.sh
```

This shows a list of available backups and lets you choose which one to restore.

### Backup File Size

The database file is very small:

- Empty database: ~12 KB
- With sample data (6 months): ~36 KB
- With 5 years of data: ~200-500 KB

**Conclusion:** Even with years of data, backups are tiny and easy to store.

### Security Considerations

Your database contains sensitive financial information:

1. **Secure local storage** - Keep your computer password-protected
2. **Access control** - Limit who can access your computer
3. **Protect backups** - Store backups securely (encrypted external drives recommended)

### Quick Reference

| Task                | Command                                |
| ------------------- | -------------------------------------- |
| Create backup       | `./scripts/db-backup.sh`               |
| Restore backup      | `./scripts/db-restore.sh`              |
| View backups        | `ls -lht backups/`                     |
| Copy database       | `cp kuyan.db kuyan_$(date +%Y%m%d).db` |
| Check database size | `ls -lh kuyan.db`                      |

---

## Versioning

KUYAN uses [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`

- **MAJOR** (1.x.x): Breaking changes, incompatible API/database changes
- **MINOR** (x.1.x): New features, backward-compatible
- **PATCH** (x.x.1): Bug fixes, backward-compatible

**Current version:** See [VERSION](VERSION) file or check the app sidebar

### Version Components

#### Where Version is Stored

1. **VERSION file** - Single source of truth

   ```
   1.0.0
   ```

2. **App UI** - Displayed in sidebar

   ```
   KUYAN
   Monthly Net Worth Tracker
   v1.0.0
   ```

3. **Docker image** - Tagged with version

   ```
   kuyan:1.0.0
   kuyan:latest
   ```

4. **Git tags** - Version releases
   ```
   git tag v1.0.0
   ```

### How to Release a New Version

**Quick version bump:**

```bash
./scripts/bump-version.sh patch   # Bug fixes (1.0.0 → 1.0.1)
./scripts/bump-version.sh minor   # New features (1.0.0 → 1.1.0)
./scripts/bump-version.sh major   # Breaking changes (1.0.0 → 2.0.0)
```

**Manual process:**

1. Update VERSION file:

   ```bash
   echo "1.1.0" > VERSION
   ```

2. Commit the change:

   ```bash
   git add VERSION
   git commit -m "Bump version to 1.1.0"
   ```

3. Create Git tag:

   ```bash
   VERSION=$(cat VERSION)
   git tag -a "v${VERSION}" -m "Release version ${VERSION}"
   git push origin "v${VERSION}"
   ```

4. Build Docker image:
   ```bash
   ./scripts/docker-build-no-cache.sh
   ```

### Checking Current Version

**In the App:** Look at the sidebar - version is displayed under the subtitle

**In Terminal:**

```bash
cat VERSION
```

**Docker Image:**

```bash
docker inspect kuyan:latest | grep -A 5 "Labels"
```

**Git Tags:**

```bash
git tag -l
git describe --tags
```

---

## Troubleshooting

### Common Issues

**Exchange rates not loading**

- Check internet connection
- frankfurter.app API may be temporarily unavailable

**Database errors**

- Ensure write permissions in application directory
- Restore from backup: `./scripts/db-restore.sh`
- Check if only one app instance is running

**Docker container won't start**

- Check logs: `docker compose logs`
- Port 8501 in use? Change port in `docker-compose.yml`
- Check database file permissions: `chmod 644 kuyan.db`

**Currency conversion warnings in console**

- Informational only, not errors
- Appear when new currencies added before rates fetched
- Auto-resolves when exchange rates are fetched (creating snapshot or viewing Exchange Rate widget)

**Backup script fails**

- Ensure you're in project directory
- Check file permissions: `chmod +x scripts/*.sh`

---

## File Structure

```
kuyan/
├── app.py                    # Main Streamlit application
├── database.py               # SQLite database operations
├── currency.py               # Exchange rate fetching
├── version.py                # Version management
├── create_sandbox_db.py      # Sandbox data generator
├── requirements.txt          # Python dependencies
├── kuyan.db                  # SQLite database (created on first run)
├── kuyan-sandbox.db          # Demo/sandbox database
├── Dockerfile                # Container image configuration
├── docker-compose.yml        # Docker orchestration
├── VERSION                   # Current version
├── LICENSE                   # MIT License
├── CONTRIBUTING.md           # Contribution guidelines
├── SECURITY.md               # Security policy
├── .gitignore                # Git ignore rules
├── assets/                   # Static assets
│   └── logo.png              # KUYAN logo
├── backups/                  # Backup storage directory
├── scripts/                  # Utility scripts
│   ├── setup-and-run-python.sh  # Python setup & run (macOS/Linux) - Port 8502
│   ├── setup-and-run-python.bat # Python setup & run (Windows)
│   ├── db-backup.sh          # Create database backup
│   ├── db-restore.sh         # Restore from backup
│   ├── bump-version.sh       # Version bump automation
│   ├── docker-build-no-cache.sh # Build Docker image (no cache)
│   ├── docker-start.sh       # Start Docker container
│   └── docker-stop.sh        # Stop Docker container
└── README.md                 # This file
```

---

## Available Scripts

The project includes several convenience scripts located in the `scripts/` directory:

### Application Scripts

| Script                     | Purpose                                                 | Usage                                |
| -------------------------- | ------------------------------------------------------- | ------------------------------------ |
| `setup-and-run-python.sh`  | Setup & start app with Python - macOS/Linux (Port 8502) | `./scripts/setup-and-run-python.sh`  |
| `setup-and-run-python.bat` | Setup & start app with Python - Windows (Port 8502)     | `scripts\setup-and-run-python.bat`   |
| `docker-build-no-cache.sh` | Build Docker image (no cache, ensures latest changes)   | `./scripts/docker-build-no-cache.sh` |
| `docker-start.sh`          | Start app with Docker (Port 8501)                       | `./scripts/docker-start.sh`          |
| `docker-stop.sh`           | Stop Docker container                                   | `./scripts/docker-stop.sh`           |

### Data Management Scripts

| Script          | Purpose                            | Usage                     |
| --------------- | ---------------------------------- | ------------------------- |
| `db-backup.sh`  | Create timestamped database backup | `./scripts/db-backup.sh`  |
| `db-restore.sh` | Restore from backup (interactive)  | `./scripts/db-restore.sh` |

### Development Scripts

| Script            | Purpose             | Usage                                             |
| ----------------- | ------------------- | ------------------------------------------------- |
| `bump-version.sh` | Bump version number | `./scripts/bump-version.sh [major\|minor\|patch]` |

### Script Details

**setup-and-run-python.sh** (macOS/Linux) / **setup-and-run-python.bat** (Windows)

- Checks Python 3.11+ installation
- Creates virtual environment (if needed)
- Installs dependencies (if needed)
- Starts Streamlit app on port 8502
- Best for development and testing
- Fastest iteration cycle
- Cross-platform support (macOS, Linux, Windows)

**docker-build-no-cache.sh**

- Reads version from VERSION file
- Stops any running containers
- Deletes existing kuyan images
- Clears Docker build cache
- Builds fresh image with `--no-cache` flag
- Tags as both `kuyan:VERSION` and `kuyan:latest`
- **Use this to ensure all code changes are incorporated**
- Takes longer but guarantees fresh build

**docker-start.sh**

- Checks if Docker is running
- Starts container with `docker compose up -d`
- Displays access URL and helpful commands
- Waits for container health check

**docker-stop.sh**

- Gracefully stops Docker container with `docker compose down`
- Preserves data (database remains in Docker volume)

**db-backup.sh**

- Creates timestamped backup in `backups/` directory
- Keeps last 30 backups automatically
- Format: `kuyan_backup_YYYYMMDD_HHMMSS.db`
- Can be run while app is running

**db-restore.sh**

- Lists available backups interactively
- Prompts for backup selection
- Creates backup of current database before restore
- Requires app to be stopped first

**bump-version.sh**

- Automatically increments version in VERSION file
- Creates git commit and tag
- Supports major, minor, and patch bumps
- Prompts for confirmation before changes
- Displays next steps for pushing and building

**Make scripts executable:**

```bash
chmod +x scripts/*.sh
```

---

## Tips

- Use the base currency selector to view net worth in different currencies
- The app stores exchange rates with each snapshot, so historical data remains accurate
- **Run `./scripts/db-backup.sh` monthly after entering snapshots**
- Use sandbox mode to test features before applying to your real data
- **Development workflow**: Use Python (port 8502) for making changes, then rebuild Docker when ready to deploy
- **Production usage**: Always use Docker (port 8501) with `docker-build-no-cache.sh` to ensure latest changes

---

## License

MIT License - Free to use and modify. See [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to contribute to this project.

## Security

KUYAN is privacy-focused and stores all data locally. For security best practices and reporting vulnerabilities, see [SECURITY.md](SECURITY.md).

## Disclaimer

This software is provided "as is" without warranty of any kind. While KUYAN takes security and data integrity seriously, users are responsible for:

- Maintaining regular backups of their financial data
- Securing their local environment
- Evaluating whether this tool meets their security requirements

KUYAN is designed for personal/family use in trusted environments and is not intended for production enterprise deployment or public internet access.
