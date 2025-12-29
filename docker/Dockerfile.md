# Write Dockerfile for Project

### 🧩 Step 1: Base Image declaration
```bash
FROM php:8.2-alpine
# FROM nginx:alpine
# FROM httpd:alpine
# FROM node:18-alpine
# FROM openjdk:17-alpine
# FROM mcr.microsoft.com/dotnet/aspnet:8.0
```
### 🧩 Step 2: Copy Project Local Computer to Docker Image
```bash
WORKDIR /var/www/html

# COPY <source> <destination>
COPY . .
```
📌 যদি /var/www/html না থাকে → Docker নিজে তৈরি করে নেয়

### 🧩 Step 3: CMD
```bash
CMD ["php", "-S", "0.0.0.0:8000"]
```
