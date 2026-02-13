# Deployment Guide for Procurement

## Overview
This document outlines the steps required to deploy the Procurement application.

## Prerequisites
- Ensure you have the following installed:
  - Node.js (version X.X.X or higher)
  - npm (version X.X.X or higher)
  - MongoDB (version X.X.X or higher)

## Deployment Steps
1. **Clone the Repository**  
   Clone the repository to your local machine:
   ```bash
   git clone https://github.com/Adrianlyle/Procurement.git
   cd Procurement
   ```

2. **Install Dependencies**  
   Navigate to the project directory and install the required dependencies:
   ```bash
   npm install
   ```

3. **Configure Environment Variables**  
   Create a `.env` file in the root directory with the necessary environment variables:
   ```env
   PORT=3000
   DB_CONNECTION=mongodb://localhost:27017/procurement
   SECRET_KEY=your_secret_key
   ```

4. **Run Database Migrations**  
   If applicable, run any database migrations:
   ```bash
   npm run migrate
   ```

5. **Start the Application**  
   You can start the application in development mode with:
   ```bash
   npm run dev
   ```
   For production mode, run:
   ```bash
   npm start
   ```

6. **Access the Application**  
   Open your browser and go to [`http://localhost:3000`](http://localhost:3000) to access the application.

## Troubleshooting
- If you encounter issues, check the following:
  - Ensure that all services (Node.js, MongoDB) are running.
  - Check the application logs for errors.

## Conclusion
By following these steps, you should have Procurement deployed and running smoothly. For additional support, please refer to the project's GitHub pages or contact the developers.

## Last Updated
Date of last update: 2026-02-13