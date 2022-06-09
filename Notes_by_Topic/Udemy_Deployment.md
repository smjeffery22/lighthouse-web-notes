# Deployment

  - In local development, entire application/database is in a single local database

  - In production, the application is no longer runnig on our machine
    - Hosted and running on a server somewhere (i.e. Heroku, AWS, etc.)
    - Serve the database over internet and connect to it

  - Want to separate development and production database
    - So the real data is not affected

  - Default storage mechanism/location for Express session
    - Uses a memory store and manages things in memory
      - Doesn't scale well and can't hold much information
    - `connect-mongo` npm package