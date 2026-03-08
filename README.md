# Product Service

A Node.js/Express microservice that handles product catalog management.

## Overview

This service is responsible for all product-related operations in the ecommerce platform. It is used by the `ecommerce-frontend` for displaying products and by the `order-service` to verify products exist when creating orders.

## API Endpoints

- GET    /health           - Health check
- GET    /products         - Fetch all products
- GET    /products/:id     - Fetch a single product
- POST   /products         - Create a new product

## Prerequisites

- Node.js v25.6.0 (see `.nvmrc`)
- npm (comes with Node.js)
- PostgreSQL database running

## Getting Started

1. Clone the repository
   git clone git@github.com:rileymo97/product-service.git

2. Install dependencies
   npm install

3. Set up environment variables
   cp .env.example .env
   Then open .env and fill in the required values

4. Start the service
   npm start

## Project Structure

product-service/
├── src/          # Application source code
├── tests/        # Test files
├── .env.example  # Environment variable template
├── .nvmrc        # Node.js version specification
└── index.js      # Application entry point

## Related Services
- ecommerce-frontend: https://github.com/rileymo97/ecommerce-frontend
- order-service: https://github.com/rileymo97/order-service
- database: https://github.com/rileymo97/database
