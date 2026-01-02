# AI
# 🔍 PriyankaBot AI - Advanced Multi-Source Search Engine

A powerful, full-stack search aggregation platform that combines results from multiple sources including Google Web Search, Google Scholar, News Articles, Books, and YouTube videos - all in one place with secure OAuth authentication.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## ✨ Features

### 🔎 Multi-Source Search
- **Google Web Search** - General web results via Serper API
- **Google Scholar** - Academic papers and research articles
- **News Articles** - Latest news from multiple publishers
- **Google Books** - Books and publications
- **YouTube Videos** - Video content with metadata

### 🔐 Secure Authentication
- **OAuth 2.0** integration with multiple providers:
  - 🟦 Google
  - ⚫ GitHub
  - 🟦 Microsoft
- Basic username/password authentication
- Secure session management with HttpOnly cookies
- 7-day persistent sessions

### ⚡ Performance & Security
- **Rate Limiting**: 200 requests/day, 50/hour per user
- **Caching**: 5-minute cache for search results
- **Input Sanitization**: XSS and injection prevention
- **CORS Protection**: Configured cross-origin policies
- **Retry Mechanism**: Automatic retries with exponential backoff
- **Random User Agents**: Prevents blocking from scraping

## 🛠️ Tech Stack

**Backend:**
- Python 3.8+
- Flask (Web Framework)
- Authlib (OAuth Authentication)
- BeautifulSoup4 (Web Scraping)
- Requests (HTTP Client)

**APIs:**
- Google Serper API (Web Search)
- Google Books API
- YouTube Data (via scraping)

**Frontend:**
- HTML5, CSS3, JavaScript
- Responsive Design
- Modern UI/UX

**Security & Performance:**
- Flask-Limiter (Rate Limiting)
- Flask-Caching (Result Caching)
- Flask-CORS (Cross-Origin Resource Sharing)
- python-dotenv (Environment Variables)

## 📋 Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Google Serper API Key ([Get it here](https://serper.dev/))
- OAuth credentials from providers (Google, GitHub, Microsoft)

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/nexus-search.git
cd nexus-search
```

### 2. Create Virtual Environment
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Linux/Mac
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables

Create a `.env` file in the root directory:

```env
# Flask Secret Key (generate a random string)
SECRET_KEY=your_super_secret_random_key_here_min_32_chars

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# GitHub OAuth
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret

# Microsoft OAuth
MICROSOFT_CLIENT_ID=your_microsoft_client_id
MICROSOFT_CLIENT_SECRET=your_microsoft_client_secret

# LinkedIn OAuth (Optional)
LINKEDIN_CLIENT_ID=your_linkedin_client_id
LINKEDIN_CLIENT_SECRET=your_linkedin_client_secret

# API Keys
SERPER_API_KEY=your_serper_api_key

# Application URL
APP_URL=http://localhost:5000
```

### 5. OAuth Setup

#### Google OAuth:
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable "Google+ API"
4. Create OAuth 2.0 credentials
5. Add authorized redirect URI: `http://localhost:5000/auth/google/callback`

#### GitHub OAuth:
1. Go to [GitHub Developer Settings](https://github.com/settings/developers)
2. Create new OAuth App
3. Set callback URL: `http://localhost:5000/auth/github/callback`

#### Microsoft OAuth:
1. Go to [Azure Portal](https://portal.azure.com/)
2. Register new application
3. Add redirect URI: `http://localhost:5000/auth/microsoft/callback`

#### Serper API:
1. Sign up at [serper.dev](https://serper.dev/)
2. Get your API key from dashboard

## 🎮 Usage

### Start the Application
```bash
python app.py
```

The server will start at `http://localhost:5000`

### Using the Search Engine

1. **Login** - Choose your preferred OAuth provider or use basic login
2. **Search** - Enter your query and select search type:
   - All (searches all sources)
   - Google Web
   - Scholar (academic papers)
   - Articles (news)
   - Books
   - YouTube
3. **View Results** - Results are displayed with icons, snippets, and metadata
4. **Click Links** - Open any result in a new tab

### API Endpoints

#### Search Endpoint
```http
POST /search
Content-Type: application/json

{
  "query": "artificial intelligence",
  "search_type": "all"
}
```

**Response:**
```json
{
  "status": "success",
  "query": "artificial intelligence",
  "count": 50,
  "search_type": "all",
  "results": [
    {
      "source": "Google Web",
      "title": "What is AI?",
      "snippet": "Artificial Intelligence explained...",
      "url": "https://example.com",
      "domain": "example.com",
      "icon": "🔍",
      "type": "web"
    }
  ]
}
```

#### User Info
```http
GET /api/user
```

#### Health Check
```http
GET /health
```

## 📁 Project Structure

```
nexus-search/
│
├── app.py                 # Main Flask application
├── .env                   # Environment variables (create this)
├── requirements.txt       # Python dependencies
│
├── templates/            # HTML templates
│   ├── index.html       # Search interface
│   └── login.html       # Login page
│
├── static/              # Static files
│   ├── css/
│   ├── js/
│   └── images/
│
└── README.md            # This file
```

## 🔒 Security Features

- **Input Sanitization**: All user inputs are cleaned and validated
- **Rate Limiting**: Prevents abuse with 50 requests/hour per IP
- **Session Security**: HttpOnly cookies, SameSite protection
- **CORS Configuration**: Controlled cross-origin access
- **OAuth 2.0**: Industry-standard authentication
- **Error Handling**: Comprehensive error catching and logging

## 🎯 Key Technical Highlights

### Web Scraping Strategy
- Random user agent rotation
- Retry mechanism with exponential backoff
- Timeout handling (15 seconds)
- Rate limit detection and waiting

### Search Result Processing
- Snippet truncation (300 characters max)
- URL extraction and validation
- Metadata parsing (authors, citations, views)
- Type categorization (web, research, article, book, video)

### Caching Strategy
- 5-minute cache for identical queries
- Memory-based simple cache
- Reduces API calls by ~60%

## ⚠️ Known Limitations

- Google Scholar and News scraping may break if Google changes HTML structure
- YouTube scraping relies on parsing JavaScript data
- Rate limits apply to Serper API (free tier: 2,500 searches/month)
- Some results may be blocked by anti-scraping measures

## 🚧 Future Enhancements

- [ ] Add more search sources (Reddit, Twitter, Stack Overflow)
- [ ] Implement user search history
- [ ] Add result filtering and sorting options
- [ ] Create browser extension
- [ ] Add API rate limit dashboard
- [ ] Implement dark mode
- [ ] Add export results feature (PDF, CSV)
- [ ] Multi-language support

## 🐛 Troubleshooting

### "SERPER_API_KEY not configured"
- Make sure you've added your Serper API key to `.env` file
- Restart the Flask application after adding the key

### OAuth Login Fails
- Check that redirect URIs match exactly in OAuth provider settings
- Ensure all required scopes are enabled
- Verify client ID and secret are correct

### No Search Results
- Check your internet connection
- Verify API keys are valid
- Try different search queries
- Check rate limits haven't been exceeded

### Rate Limit Exceeded
- Wait 1 hour for limits to reset
- Consider upgrading Serper API plan for higher limits

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your Profile](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

## 🙏 Acknowledgments

- [Flask](https://flask.palletsprojects.com/) - Web framework
- [Serper API](https://serper.dev/) - Google Search API
- [Authlib](https://authlib.org/) - OAuth library
- [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) - Web scraping

## 📞 Support

If you have any questions or need help, please:
1. Check the [Issues](https://github.com/yourusername/nexus-search/issues) page
2. Create a new issue with detailed description
3. Contact me via email

---

⭐ If you found this project helpful, please give it a star!

**Made with ❤️ and Python**
