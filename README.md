# Inception

A Docker-based WordPress infrastructure project that sets up a complete development environment using multiple containers and services.

## 🎯 Project Overview

This project involves setting up a small infrastructure composed of different services using Docker containers. The entire setup is designed to run in a virtual machine, with each service running in its own dedicated container.

## 🔧 Technical Requirements

- Virtual Machine environment
- Docker and Docker Compose
- Make

## 📦 Services

The infrastructure includes the following services, each running in its own container:

1. **NGINX**
   - Configured with TLSv1.2 or TLSv1.3 only
   - Acts as the only entry point (port 443)

2. **WordPress + php-fpm**
   - WordPress installation with php-fpm configuration
   - Runs without nginx in its own container

3. **MariaDB**
   - Database service
   - Runs in a dedicated container

## 💾 Volumes

The project uses two Docker volumes:

1. WordPress database volume
2. WordPress website files volume

Volumes are mounted in `/home/login/data` on the host machine.

## 🌐 Networking

- Custom Docker network for inter-container communication
- Domain configuration: `login.42.fr` pointing to local IP
- No use of `network: host`, `--link`, or `links:`

## 🔐 Security Features

- TLS encryption (v1.2 or v1.3)
- Environment variables for sensitive data
- No hardcoded passwords in Dockerfiles
- WordPress admin username restrictions (cannot contain admin/Admin or administrator/Administrator)



## 🚀 Getting Started

1. Clone the repository
2. Create a `.env` file in the `srcs` directory with required environment variables
3. Run `make` to build and start the infrastructure

### Environment Variables

Create a `srcs/.env` file with the following variables:

```
DOMAIN_NAME=your_login.42.fr
CERTS_=./path_to_certificates
MYSQL_ROOT_PASSWORD=your_root_password
MYSQL_USER=your_username
MYSQL_PASSWORD=your_password
```

## 📝 Additional Notes

- Containers are configured to restart automatically in case of crashes
- No infinite loops or hacky patches (tail -f, bash, sleep infinity, etc.)
- Latest tag is prohibited in Docker images
- Images must be built from either Alpine or Debian (penultimate stable version)

## 🎉 Bonus Features 

- Redis cache for WordPress
- FTP server container
- Static website (non-PHP)
- Adminer
- Additional useful service (must be justified)

## ⚠️ Important Reminders

- Don't commit sensitive data or credentials
- Keep .env file in .gitignore
- Ensure all services are properly configured before deployment
- Follow Docker best practices for daemon processes and PID 1
