# CI/CD Pipeline for Symfony Project

This repository includes a simple CI/CD pipeline for a Symfony project, utilizing GitHub Actions for continuous integration and deployment.

---

## Pipeline Overview

The pipeline automates the following tasks:

### 1. 🛠️ Build and Test (`symfony-tests` job)

- **Environment Setup**: Configures PHP, Node.js, and a MySQL service.
- **Code Quality**: Runs PHP-CS-Fixer and PHPStan for code style and static analysis.
- **Database Setup**: Prepares a MySQL database for testing.
- **Testing**: Executes PHPUnit tests for unit and feature testing.

### 2. 🎉 Deploy (`web-deploy` job)

- Deploys the application to a production server using FTP after successful tests.

---

## How It Works

### Triggering

The pipeline runs on:

- **Push**: Any push to the repository.
- **Pull Requests**: On new or updated pull requests.

The deployment job is triggered only for the `main` branch after successful tests.

---

### Build and Test Steps

1. **Checkout Code**

   - Retrieves the latest code from the repository.

2. **Setup Environment**

   - Configures PHP 8.3 and Node.js 20.
   - Copies `.env.test.local` from `.env.test` if not already present.

3. **Install Dependencies**

   - Caches Composer dependencies for faster builds.
   - Installs PHP dependencies.

4. **Code Quality Checks**

   - Executes:
     - `PHP-CS-Fixer` for formatting.
     - `PHPStan` for static code analysis.

5. **Database Preparation**

   - Starts a MySQL 8.0 service.
   - Creates and migrates a test database.
   - Loads test fixtures.

6. **Run Tests**
   - Executes PHPUnit tests for validation.

---

### Deploy Steps

1. **Checkout Code**

   - Retrieves the latest code from the `main` branch.

2. **FTP Deployment**
   - Syncs application files to the production server via FTP.

---

## Prerequisites

### Environment Variables

The following GitHub Secrets are required for deployment:

- `ftp_server`: The FTP server URL.
- `ftp_username`: FTP server username.
- `ftp_password`: FTP server password.

### Dependencies

Ensure the following dependencies are installed in your project:

- Composer packages for PHP-CS-Fixer, PHPStan, PHPUnit.
- Symfony Doctrine and Fixtures bundles.

---

## Improvements and Customization

- **Additional Jobs**: Extend the pipeline with other quality checks or deployments.
- **Advanced Deployments**: Replace FTP with more secure alternatives (e.g., SFTP or SSH).
- **Scalability**: Add a staging environment for pre-production testing.

---

## Usage

Push your code or create a pull request to trigger the pipeline. For production deployment, merge changes into the `main` branch.
