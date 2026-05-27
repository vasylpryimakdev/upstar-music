# Upstar Music

A desktop application for managing music artists and their albums, built with Electron, React, Redux, and MongoDB.

## Features

- **Artist Management**: Create, read, update, and delete artists
- **Advanced Filtering**: Filter artists by age range, years active, retirement status, and genre
- **Search**: Full-text search across artist names
- **Album Tracking**: Manage album details including title, release date, copies sold, and revenue
- **Pagination**: Efficiently browse through large artist collections
- **Seed Data**: Automatically generates realistic test data using Faker

## Tech Stack

### Frontend
- **React** (v0.14.3) - UI library
- **Redux** (v3.6.0) - State management
- **React Router** (v3.0.0) - Client-side routing
- **Redux Form** (v6.1.1) - Form handling
- **Redux Thunk** (v2.1.0) - Async actions
- **Materialize CSS** - UI framework
- **React Input Range** - Range slider component

### Backend
- **Electron** (v27.0.3) - Desktop application framework
- **MongoDB** (v3.6.12) - Database
- **Mongoose** (v5.13.21) - ODM for MongoDB

### Build Tools
- **Webpack** (v1.12.9) - Module bundler
- **Babel** - JavaScript transpiler
- **Sass** - CSS preprocessor

## Prerequisites

- Node.js (with npm)
- MongoDB (running locally on port 27017)

## Installation

1. Clone the repository:
```bash
git clone git@github.com:vasylpryimakdev/upstar-music.git
cd upstar-music
```

2. Install dependencies:
```bash
npm install
```

3. Ensure MongoDB is running:
```bash
# On Windows
net start MongoDB

# Or start MongoDB manually
mongod
```

## Running the Application

Start the application with:
```bash
npm start
```

This will:
- Launch the Electron desktop application
- Start the webpack dev server on port 4172
- Connect to MongoDB database `upstar_music`
- Seed the database with 15,000 artists if fewer than 200 exist

## Project Structure

```
mongodb-project/
├── database/
│   ├── models/
│   │   ├── artist.js          # Artist Mongoose model
│   │   └── album.js           # Album Mongoose schema
│   └── queries/
│       ├── CreateArtist.js    # Create artist query
│       ├── DeleteArtist.js    # Delete artist query
│       ├── EditArtist.js      # Update artist query
│       ├── FindArtist.js      # Find single artist
│       ├── GetAgeRange.js     # Filter by age range
│       ├── GetYearsActiveRange.js  # Filter by years active
│       ├── SearchArtists.js   # Search artists
│       ├── SetNotRetired.js   # Mark artist as active
│       └── SetRetired.js      # Mark artist as retired
├── src/
│   ├── actions/
│   │   ├── index.js           # Action creators
│   │   └── types.js           # Action types
│   ├── components/
│   │   ├── Header.js          # Application header
│   │   ├── Home.js            # Home page
│   │   ├── artists/
│   │   │   ├── ArtistCreate.js    # Artist creation form
│   │   │   ├── ArtistDetail.js    # Artist detail view
│   │   │   ├── ArtistEdit.js      # Artist edit form
│   │   │   ├── ArtistFilter.js    # Artist filter panel
│   │   │   ├── ArtistIndex.js     # Artist list view
│   │   │   ├── ArtistMain.js      # Artist main container
│   │   │   └── Paginator.js       # Pagination component
│   │   └── filters/
│   │       ├── Picker.js      # Genre picker
│   │       ├── Range.js       # Range slider
│   │       ├── Switch.js      # Toggle switch
│   │       └── index.js       # Filter exports
│   ├── reducers/
│   │   ├── ArtistsReducer.js      # Artists state
│   │   ├── ErrorReducer.js        # Error state
│   │   ├── FilterCriteriaReducer.js  # Filter state
│   │   ├── SelectionReducer.js   # Selection state
│   │   └── index.js               # Root reducer
│   ├── constants.js           # Application constants
│   ├── main.js                # Application entry point
│   ├── router.js              # React Router configuration
│   └── seeds.js               # Database seeding script
├── style/
│   └── style.css              # Application styles
├── index.html                 # HTML template
├── index.js                   # Electron main process
├── webpack.config.js          # Webpack configuration
└── package.json               # Project dependencies
```

## Database Schema

### Artist Model
```javascript
{
  name: String,
  age: Number,
  yearsActive: Number,
  image: String,
  genre: String,
  website: String,
  netWorth: Number,
  labelName: String,
  retired: Boolean,
  albums: [AlbumSchema]
}
```

### Album Schema
```javascript
{
  title: String,
  date: Date,
  copiesSold: Number,
  numberTracks: Number,
  image: String,
  revenue: Number
}
```

## Usage

### Viewing Artists
- Navigate to the home page to see all artists
- Use the filter panel to filter by:
  - Age range
  - Years active range
  - Retirement status
  - Genre
- Use the search bar to find artists by name
- Use pagination to navigate through results

### Managing Artists
- Click "Create Artist" to add a new artist
- Click on an artist to view details
- Use the edit button to modify artist information
- Use the delete button to remove an artist

### Seeding Data
The application automatically seeds the database with 15,000 artists on first launch if fewer than 200 artists exist. This uses Faker to generate realistic data including:
- Random names and ages
- Various music genres
- Album information with realistic sales figures
- Artist images from Picsum Photos

## Development

### Webpack Dev Server
The webpack dev server runs on port 4172 and provides hot-reloading during development.

### Electron
The Electron main process is defined in `index.js` and creates a browser window with Node.js integration enabled.

### MongoDB Connection
The application connects to MongoDB using both:
- Native MongoDB driver (for raw queries)
- Mongoose (for ORM operations)

Both connect to `mongodb://localhost/upstar_music`
