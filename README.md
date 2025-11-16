# MediSynth (Current repository contents: Hospital Management System)

Note: This repository currently contains a Hospital Management System demo web application (PHP + static assets) and a MySQL-compatible SQL dump. This README explains what is present, how to run the app locally for testing, and quick troubleshooting tips.

Contents snapshot
- Hospital-management-system-master/ — web application (PHP files, images, subfolders for admin/doctor/patient)
  - Key files detected: index.php, adminlogin.php, doctorlogin.php, patientlogin.php, connection.php, account.php, header.php, contact.html, img/, admin/, doctor/, patient/, etc.
- hms.sql — SQL dump with schema and seed data for the application database.

Prerequisites
- PHP 7.x or 8.x with mysqli support
- MySQL or MariaDB server (or compatible)
- A web server (Apache / Nginx) or the PHP built-in server for quick testing
- Optional: XAMPP / MAMP / LAMP, or Docker for containerized setup

Quick start (local machine)
1. Clone the repository
   git clone https://github.com/MOHIT-SINGH-RATHORE/MediSynth.git
   cd MediSynth

2. Inspect the app folder to confirm file types and any config files
   ls -la Hospital-management-system-master
   # Look for connection.php, config.php, .env or README inside that folder.

3. Import the database
   # create a database and import the dump (example using `hms_db`)
   mysql -u root -p
   CREATE DATABASE hms_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
   EXIT
   mysql -u root -p hms_db < hms.sql

   (You can also use phpMyAdmin or MySQL Workbench to import `hms.sql`.)

4. Configure the application DB connection
   - Open Hospital-management-system-master/connection.php and update DB host, username, password, and DB name to match the database you created.
   - Example minimal connection.php (adapt to the variables used in the repo):

   ```php
   <?php
   $db_host = '127.0.0.1';
   $db_user = 'root';
   $db_pass = 'your_password';
   $db_name = 'hms_db';
   $conn = new mysqli($db_host, $db_user, $db_pass, $db_name);
   if ($conn->connect_error) {
       die("Connection failed: " . $conn->connect_error);
   }
   ?>
   ```

5. Serve the application
   - Option A: Copy `Hospital-management-system-master` into your web server's document root (e.g. XAMPP's htdocs) and browse to http://localhost/<folder>.
   - Option B: Quick test using PHP built-in server:
     php -S localhost:8000 -t Hospital-management-system-master
     Open http://localhost:8000

6. Login & test
   - Check `hms.sql` to find any seeded users or default credentials (search for INSERT statements into users/admin tables).
   - Use the UI pages (admin login, doctor login, patient login) to explore functionality: appointments, patients, billing, accounts, etc.

Troubleshooting
- Blank pages / PHP errors: enable error display in PHP (development only) or check server logs.
- Database connection errors: verify host, user, password, and that the DB server is running and the DB was imported successfully.
- Missing images/CSS: confirm `img/` and other static folders are present and accessible by the web server.
- If the app uses sessions, ensure PHP session support and correct directory permissions.

Security notes
- This is a demo/learning app. Do not expose it to the public internet without securing credentials, sanitizing inputs, and reviewing code for vulnerabilities.
- Replace default passwords and avoid running with production DB credentials.
- Review `hms.sql` before sharing; it may contain sample data.

Next useful actions (suggestions you can request)
- I can inspect the admin/, doctor/, and patient/ subfolders and list exact dependencies and any hard-coded credentials.
- I can generate a docker-compose.yml + Dockerfile that runs a php:apache container and a MySQL container and imports `hms.sql` automatically.
- I can search `hms.sql` and PHP files to find seeded credentials and show them.

Contributing
- If you want to add documentation, tests, or containerization, create a branch and open a PR. I can draft the PR title/description and files if you want.

License
- None specified in this repository. Add a LICENSE file (e.g., MIT) if you want to set licensing terms.

Maintainer
- Repository: MOHIT-SINGH-RATHORE/MediSynth
- Contact: (use your GitHub account)
