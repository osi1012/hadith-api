# Hikmah Dynamics Hadith API

A self-hosted API for Islamic texts that you can run on your own server without relying on external services.

## Features

- **Self-Hosted**: Run the API on your own server or computer
- **Complete Control**: Manage your own data without external dependencies
- **No Rate Limits**: Use as much as you need
- **Multiple Languages**: Support for various translations
- **Multiple Hadith Collections**: All major hadith books included
- **Quran Integration**: Complete Quran text with translations
- **API Key Authentication**: Secure access for your applications
- **Simple Setup**: Easy to install and configure

## Installation

1. Clone this repository to your local machine:
   ```
   git clone https://github.com/osi1012/hadith-api.git
   ```

2. Install the required dependencies:
   ```
   cd hadith-api
   npm install
   ```

3. Configure your server settings in `config.js`

4. Start the server:
   ```
   npm start
   ```

## API Endpoints

### Hadith Endpoints

- `/api/editions` - List all available hadith collections
- `/api/editions/{editionName}` - Get a specific hadith collection
- `/api/editions/{editionName}/{hadithNumber}` - Get a specific hadith
- `/api/editions/{editionName}/sections/{sectionNumber}` - Get a specific section
- `/api/search?q={query}` - Search across all hadith collections

### Quran Endpoints

- `/api/quran/surah` - List all surahs
- `/api/quran/surah/{surahNumber}` - Get a specific surah
- `/api/quran/ayah/{surahNumber}/{ayahNumber}` - Get a specific ayah
- `/api/quran/translation/{language}/{surahNumber}` - Get translations
- `/api/quran/search?q={query}&lang={language}` - Search the Quran

## Authentication

To secure your API, you can enable API key authentication:

1. Generate an API key in the admin interface
2. Include the API key in your requests:
   ```
   /api/editions/eng-bukhari?api_key=YOUR_API_KEY
   ```

## Customization

You can customize the API by:

1. Editing the server configuration in `config.js`
2. Adding your own hadith collections to the `editions` directory
3. Modifying the API endpoints in `apiscript.js`

## Integration with Your App

### Example: Fetching a Random Hadith

```javascript
async function fetchRandomHadith() {
  try {
    const response = await fetch('http://your-server.com/api/editions/eng-bukhari/random');
    const data = await response.json();
    
    // Display the hadith
    document.getElementById('hadith-text').textContent = data.text;
    document.getElementById('hadith-reference').textContent = data.reference;
  } catch (error) {
    console.error('Error fetching hadith:', error);
  }
}
```

### Example: Searching the Quran

```javascript
async function searchQuran(query) {
  try {
    const response = await fetch(`http://your-server.com/api/quran/search?q=${query}&lang=en`);
    const results = await response.json();
    
    // Display results
    const resultsContainer = document.getElementById('search-results');
    resultsContainer.innerHTML = '';
    
    results.forEach(result => {
      const resultElement = document.createElement('div');
      resultElement.innerHTML = `
        <p><strong>Surah ${result.surah}:${result.ayah}</strong></p>
        <p>${result.text}</p>
      `;
      resultsContainer.appendChild(resultElement);
    });
  } catch (error) {
    console.error('Error searching Quran:', error);
  }
}
```

## Credits

This API is based on the work of [fawazahmed0's hadith-api](https://github.com/fawazahmed0/hadith-api) and has been modified to be self-hosted and customized for Hikmah Dynamics.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
