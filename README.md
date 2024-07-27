# Retreat Booking System

### Prerequisites
- Python 3.11 and above
- PostgreSQL

### Set-Up Steps
1. Clone the repository:

   git clone https://github.com/steeven1001759481/retreats_app.git
   cd retreats_app
   
2. Create and activate virtual environment
   python -m venv env
   env\Scripts\activate

3. Install required packages
   pip install -r requirements.txt

4. Create Postgresql Database
   CREATE DATABASE <database_name>;
   CREATE USER <user_name> WITH PASSWORD <password>;
   ALTER ROLE <user_name> SET client_encoding TO 'utf8';
   ALTER ROLE <user_name> SET default_transaction_isolation TO 'read committed';
   GRANT ALL PRIVILEGES ON DATABASE <database_name> TO <user_name>;

5. Make changes in certain files to configure database
   - In 'retreat_app/models.py'
      - engine = create_engine('postgresql://<username>:<password>@<host>/<database_name>')
   - In 'retreats/settings.py'
      - DATABASES = {
          'default': {
              'ENGINE': 'django.db.backends.postgresql',
              'NAME': "<database_name>",
              'USER': '<user_name>',
              'PASSWORD': '<password>',
              'HOST': '<host>',
              'PORT': '5432',
          }
      }

6. Run Database Migrations
   - python manage.py makemigrations
   - python manage.py migrate

7. Run command to populate the Database with Retreats data from Api
   - python manage.py fetch_data

### Run Application Locally
1. Start Server
  - python manage.py runserver

2. Check Retreats Api endpoint
  - Fetch all
    - http://localhost:8000/retreats/
  - Fetch based on parameters
    - ex. http://localhost:8000/retreats/?location=Goa
  - Fetch based on Filter or Search
    - ex. http://localhost:8000/retreats/?filter=Wellness
    - ex. http://localhost:8000/retreats/?search=Wellness
  - Pagination Api
    - ex. http://localhost:8000/retreats/?page=1&limit=3

3. Check Book retreat Api endpoint
  - Create a new POST request in Postman
  - Set the method to 'POST' and URL to 'http://127.0.0.1:8000/book'
  - On Body tab, select "raw", and set type to "JSON"
  - Enter JSON data in the field below - 
    ex.
    {
          "user_id": 1,
          "user_name": "user1",
          "user_email": "user1@gmail.com",
          "user_phone": "213512",
          "retreat_id": 1,
          "retreat_title": "Yoga for Stress Relief",
          "retreat_location": "Goa",
          "retreat_price": 200,
          "retreat_duration": 3,
          "payment_details": "card",
          "booking_date": "12022024"
    }
    
  - Click Send to make the request
  - Check new booking using 'http://127.0.0.1:8000/booked'
