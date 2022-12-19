# Flask React Project

This is the starter for the Flask React project.

## Getting started

1. Clone this repository (only this branch)

   ```bash
   git clone https://github.com/grau-maus/flask-react-starter-flyio.git
   ```

2. Install dependencies

      ```bash
      pipenv install --dev -r dev-requirements.txt && pipenv install -r requirements.txt
      ```

3. Create a **.env** file based on the example with proper settings for your
   development environment
4. Setup your PostgreSQL user, password and database and make sure it matches your **.env** file

5. Get into your pipenv, migrate your database, seed your database, and run your flask app

   ```bash
   pipenv shell
   ```

   ```bash
   flask db upgrade
   ```

   ```bash
   flask seed all
   ```

   ```bash
   flask run
   ```

6. To run the React App in development, checkout the [README](./react-app/README.md) inside the `react-app` directory.

***
*IMPORTANT!*
   If you add any python dependencies to your pipfiles, you'll need to regenerate your requirements.txt before deployment.
   You can do this by running:

   ```bash
   pipenv lock -r > requirements.txt
   ```

*ALSO IMPORTANT!*
   psycopg2-binary MUST remain a dev dependency because you can't install it on apline-linux.
   There is a layer in the Dockerfile that will install psycopg2 (not binary) for us.
***

## Deploy to Fly.io

1. Before you deploy, don't forget to run the following command in order to
ensure that your production environment has all of your up-to-date
dependencies. You only have to run this command when you have installed new
Python packages since your last deployment, but if you aren't sure, it won't
hurt to run it again.

      ```bash
      pipenv lock -r > requirements.txt
      ```

2. Install the [flyctl CLI](https://fly.io/docs/hands-on/install-flyctl/)

3. Run:

      ```bash
      fly auth login
      ```

4. Launch your app:

      ```bash
      fly launch
      ```

5. Type in your app name (or leave blank to generate a random app name)

6. Select a region for deployment (preferably the nearest location unless a majority of your users are based in another region)

7. Select `` N `` if the CLI asks you if you would like to set up a Postgresql database

8. Select `` N `` if the CLI asks you if you would like to set up an Upstash Redis database

9. Select `` y `` if the CLI asks you if you would like to deploy

10. After deploying, set up your secret key by running:

      ```bash
      fly secrets set SECRET_KEY=<your secret key>
      ```

11. Set up your PostgreSQL database:

      ```bash
      fly postgres create
      ```

12. Type in the name for your app's database (preferably your app name with "-db" appended)

13. Select a region (preferably in the same location as your app)

14. Select ``Development``

15. Attach your app to your database:

      ```bash
      fly postgres attach --app <app-name> <postgres-app-name>
      ```

16. SSH into your app:

      ```bash
      fly ssh console
      ```

17. Navigate into your app folder:

      ```bash
      cd var/www/
      ```

18. Set up your database

      ```bash
      flask db upgrade
      flask seed all
      ```

19. profit

### For M1 Mac users

(WIP)
