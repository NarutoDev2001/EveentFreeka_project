# EventFreeka Setup Guide

## Step-by-Step Installation

### 1. Prerequisites

Ensure you have installed:
- Ruby 3.2.0 (`ruby -v`)
- Rails 7.0.0 (`rails -v`)
- PostgreSQL (`psql --version`)
- Git

### 2. Clone Repository

```bash
git clone https://github.com/NarutoDev2001/EveentFreeka_project.git
cd EveentFreeka_project
```

### 3. Install Ruby Gems

```bash
bundle install
```

This installs all dependencies including:
- Rails 7
- Devise (authentication)
- Stripe (payments)
- Pundit (authorization)
- Bootstrap (UI)
- Kaminari (pagination)

### 4. Database Setup

#### Create database
```bash
rails db:create
```

#### Run migrations
```bash
rails db:migrate
```

#### Seed data (optional)
```bash
rails db:seed
```

### 5. Environment Variables

Create `.env` file from template:
```bash
cp .env.example .env
```

Edit `.env` and add your credentials:
```env
# Stripe API Keys (get from https://dashboard.stripe.com)
STRIPE_PUBLIC_KEY=pk_test_your_key_here
STRIPE_SECRET_KEY=sk_test_your_key_here

# Database URL (optional, defaults to PostgreSQL)
DATABASE_URL=postgresql://localhost/eventfreeka_development
```

### 6. Devise Setup

Initialize Devise (if not already done):
```bash
rails generate devise:install
rails generate devise User
rails db:migrate
```

### 7. Start Server

```bash
rails server
```

Visit: `http://localhost:3000`

## First Time Setup Checklist

- [ ] Ruby 3.2.0 installed
- [ ] PostgreSQL running
- [ ] `.env` file created with Stripe keys
- [ ] Database created and migrated
- [ ] Server started successfully
- [ ] Can access http://localhost:3000

## Stripe Test Cards

For testing payments, use these test card numbers:

| Card Type | Card Number | CVC | Date |
|-----------|------------|-----|------|
| Visa | 4242 4242 4242 4242 | Any 3 digits | Any future date |
| Visa (decline) | 4000 0000 0000 0002 | Any 3 digits | Any future date |
| Amex | 3782 822463 10005 | Any 4 digits | Any future date |

Any email address and any future expiration date will work.

## Common Issues

### Database already exists
```bash
rails db:drop
rails db:create
rails db:migrate
```

### Port 3000 already in use
```bash
rails server -p 3001
```

### Gems not installing
```bash
gem install bundler
bundle install
```

### Stripe keys not working
- Check `.env` file is in project root
- Restart the server after changing `.env`
- Verify keys are from test environment (start with `pk_test_` and `sk_test_`)

### Database connection error
- Ensure PostgreSQL is running
- Check `config/database.yml`
- Verify DATABASE_URL in `.env`

## Development Server

```bash
rails server
# or
rails s
```

Access at: `http://localhost:3000`

## Useful Commands

```bash
# Console
rails console

# Generate model
rails generate model ModelName

# Generate migration
rails generate migration CreateTableName

# Run specific migration
rails db:migrate:up VERSION=xxx

# Rollback migrations
rails db:rollback

# Check routes
rails routes

# Server on different port
rails server -p 3001

# Precompile assets
rails assets:precompile
```

## Production Deployment

### Heroku

```bash
# Install Heroku CLI
# Login to Heroku
heroku login

# Create Heroku app
heroku create your-app-name

# Set environment variables
heroku config:set STRIPE_PUBLIC_KEY=your_key
heroku config:set STRIPE_SECRET_KEY=your_key

# Push to Heroku
git push heroku main

# Run migrations
heroku run rails db:migrate

# Open app
heroku open
```

## Next Steps

1. **Create a user account**
   - Go to http://localhost:3000/users/sign_up
   - Sign up with email and password

2. **Create your first event**
   - Click "Create Event"
   - Fill in event details
   - Set price or leave 0 for free

3. **Test the payment flow**
   - Create another account or use different browser
   - Try to join a paid event
   - Use test Stripe card numbers

## Support

If you encounter issues:
1. Check error messages in console
2. Review logs in `log/development.log`
3. Open an issue on GitHub
4. Check Stripe documentation at https://stripe.com/docs
