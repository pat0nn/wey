# Wey Backend

A Django REST API backend for the Wey social media platform, providing user authentication, social networking features, messaging, posts, and notifications.

## 🚀 Features

- **User Management**: Custom user authentication with JWT tokens
- **Social Networking**: Friend requests, friend suggestions, and social connections
- **Posts & Feed**: Create, share, and interact with posts including media attachments
- **Real-time Chat**: Messaging system for user communication
- **Notifications**: Real-time notification system for user interactions
- **Search**: User and content search functionality
- **Trending**: Trend analysis and content discovery
- **Media Handling**: Image upload and management for avatars and post attachments

## 🛠 Tech Stack

- **Framework**: Django 4.2
- **API**: Django REST Framework 3.14.0
- **Authentication**: JWT (djangorestframework-simplejwt)
- **Database**: SQLite (development) / PostgreSQL (production ready)
- **Image Processing**: Pillow
- **CORS**: django-cors-headers

## 📦 Installation

### Prerequisites

- Python 3.8+
- pip
- Virtual environment (recommended)

### Setup

1. **Clone the repository and navigate to backend directory**
   ```bash
   cd wey_backend
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run database migrations**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Create superuser (optional)**
   ```bash
   python manage.py createsuperuser
   ```

6. **Run the development server**
   ```bash
   python manage.py runserver
   ```

The API will be available at `http://127.0.0.1:8000/`

## 🏗 Project Structure

```
wey_backend/
├── account/           # User authentication and profile management
├── chat/             # Real-time messaging system
├── notification/     # Notification management
├── post/            # Posts, comments, likes, and trends
├── search/          # Search functionality
├── scripts/         # Utility scripts for maintenance
├── media/           # User uploaded files (avatars, attachments)
├── wey_backend/     # Main Django project settings
├── manage.py        # Django management script
└── requirements.txt # Python dependencies
```

## 🔌 API Endpoints

### Authentication
- `POST /api/signup/` - User registration
- `POST /api/login/` - User login (returns JWT tokens)
- `POST /api/refresh/` - Refresh JWT token
- `GET /api/me/` - Get current user profile
- `POST /api/editprofile/` - Update user profile

### Social Features
- `GET /api/friends/` - Get user's friends list
- `GET /api/friends/suggested/` - Get friend suggestions
- `POST /api/friends/<user_id>/request/` - Send friend request
- `POST /api/friends/<user_id>/request/handle/` - Accept/reject friend request

### Posts
- `GET /api/posts/` - Get feed posts
- `POST /api/posts/create/` - Create new post
- `GET /api/posts/<post_id>/` - Get specific post
- `POST /api/posts/<post_id>/like/` - Like/unlike post
- `POST /api/posts/<post_id>/comment/` - Add comment
- `GET /api/posts/trends/` - Get trending topics

### Chat
- `GET /api/chat/` - Get user conversations
- `GET /api/chat/<conversation_id>/` - Get conversation messages
- `POST /api/chat/<conversation_id>/send/` - Send message

### Notifications
- `GET /api/notifications/` - Get user notifications
- `POST /api/notifications/<notification_id>/read/` - Mark notification as read

### Search
- `GET /api/search/` - Search users and content

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
DATABASE_URL=sqlite:///db.sqlite3
WEBSITE_URL=http://127.0.0.1:8000
```

### CORS Settings

The backend is configured to accept requests from the frontend at `http://localhost:5173`. Update `CORS_ALLOWED_ORIGINS` in `settings.py` for production.

### Media Files

User-uploaded files are stored in the `media/` directory:
- `media/avatars/` - User profile pictures
- `media/post_attachments/` - Post images and attachments

## 🚀 Deployment

### Production Settings

1. **Create production settings file**
   ```bash
   cp wey_backend/settings.py wey_backend/settings_prod.py
   ```

2. **Update production settings**:
   - Set `DEBUG = False`
   - Configure proper database (PostgreSQL recommended)
   - Set secure `SECRET_KEY`
   - Configure `ALLOWED_HOSTS`
   - Set up proper media/static file serving

3. **Environment Variables**:
   ```env
   DJANGO_SETTINGS_MODULE=wey_backend.settings_prod
   SECRET_KEY=your-production-secret-key
   DEBUG=False
   DATABASE_URL=postgresql://user:password@localhost/dbname
   ```

## 🔨 Utility Scripts

### Friend Suggestions
```bash
python manage.py shell < scripts/generate_friend_suggestions.py
```
Generates friend suggestions based on mutual connections and user activity.

### Trending Topics
```bash
python manage.py shell < scripts/generate_trends.py
```
Analyzes posts and generates trending topics and hashtags.

## 🧪 Testing

Run the test suite:
```bash
python manage.py test
```

Run tests for specific app:
```bash
python manage.py test account
python manage.py test post
```

## 📊 Database Management

### Migrations
```bash
# Create new migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Show migration status
python manage.py showmigrations
```

### Database Shell
```bash
python manage.py dbshell
```

### Django Shell
```bash
python manage.py shell
```

## 🔐 Security

- JWT tokens are used for authentication
- CORS is configured for frontend integration
- Custom user model with UUID primary keys
- Password validation enabled
- CSRF protection enabled

