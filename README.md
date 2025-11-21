# 🏨 Hotel Dynasty - Booking Management System

<div align="center">

![PHP](https://img.shields.io/badge/PHP-7.4+-blue.svg)
![MySQL](https://img.shields.io/badge/MySQL-Database-orange.svg)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow.svg)
![HTML5](https://img.shields.io/badge/HTML5-Markup-red.svg)
![CSS3](https://img.shields.io/badge/CSS3-Styling-blue.svg)

*A comprehensive hotel booking and management system where luxury meets functionality*

[Demo](#) | [Documentation](#) | [Report Bug](#)

</div>

## 📋 Overview

Hotel Dynasty is a full-featured hotel booking management system built with PHP and MySQL. The system provides a complete solution for hotel room reservations, user management, and administrative controls. With separate interfaces for customers, administrators, and hotel staff, it streamlines the entire booking process from search to checkout.

## ✨ Key Features

### Guest/Customer Features
- 🏠 **Browse Rooms** - View available rooms with images and descriptions
- 🔍 **Search & Filter** - Find rooms by type, date, and amenities
- 📅 **Date Selection** - Choose check-in and check-out dates
- 🔐 **User Registration** - Create account with secure authentication
- 👤 **Profile Management** - Update personal information
- 📋 **Booking History** - View past and current reservations
- 📧 **Contact Form** - Reach out to hotel management
- ✏️ **Edit Bookings** - Modify reservation details
- ❌ **Cancel Bookings** - Cancel reservations when needed

### Admin Features
- 📊 **Dashboard** - Overview of bookings, occupancy, and revenue
- 🏨 **Room Management** - Add, edit, and delete room listings
- 👥 **User Management** - View and manage customer accounts
- 📝 **Booking Management** - Process and update reservations
- 🔧 **Admin Creation** - Create new admin accounts
- 📈 **Reports** - Generate booking and revenue reports
- 🎯 **Occupancy Tracking** - Monitor room availability

### System Features
- 🔒 **Secure Authentication** - Session-based login for users and admins
- 📱 **Responsive Design** - Works seamlessly on all devices
- 🖼️ **Image Management** - Upload and manage room images
- 💾 **Database Integration** - MySQL for reliable data storage
- 🎨 **Modern UI** - Clean and intuitive interface

## 🛠️ Tech Stack

### Backend
- **PHP 7.4+** - Server-side scripting
- **MySQL** - Relational database
- **Session Management** - User authentication

### Frontend
- **HTML5** - Semantic markup
- **CSS3** - Modern styling with custom CSS
- **JavaScript** - Interactive features
- **Responsive Design** - Mobile-first approach

## 📦 Installation

### Prerequisites

- PHP 7.4 or higher
- MySQL 5.7 or higher
- Apache/Nginx web server
- phpMyAdmin (optional, for database management)

### Setup Instructions

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/hotel-dynasty.git
cd "Hotel Booking Management System"
```

2. **Database Setup**

Create a new MySQL database:
```sql
CREATE DATABASE hotel_dynasty;
```

Import the database schema:
```sql
-- Create users table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create rooms table
CREATE TABLE rooms (
    id INT AUTO_INCREMENT PRIMARY KEY,
    room_type VARCHAR(50) NOT NULL,
    room_name VARCHAR(100) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    capacity INT NOT NULL,
    amenities TEXT,
    image VARCHAR(255),
    status ENUM('available', 'occupied', 'maintenance') DEFAULT 'available',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create reservations table
CREATE TABLE reservations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    room_type VARCHAR(50) NOT NULL,
    check_in_date DATE NOT NULL,
    check_out_date DATE NOT NULL,
    total_amount DECIMAL(10,2),
    status ENUM('pending', 'confirmed', 'cancelled', 'completed') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Create admins table
CREATE TABLE admins (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

3. **Configure Database Connection**

Edit `config/connection.php`:
```php
<?php
$servername = "localhost";
$username = "your_username";
$password = "your_password";
$dbname = "hotel_dynasty";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

4. **Set up Web Server**

For Apache, add to `.htaccess`:
```apache
RewriteEngine On
RewriteBase /

# Redirect to HTTPS (optional)
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

5. **Set Permissions**

```bash
chmod 755 -R assets/
chmod 755 -R uploads/
chmod 644 config/connection.php
```

6. **Access the Application**

- Customer Portal: `http://localhost/hotel-dynasty/pages/index.php`
- Admin Panel: `http://localhost/hotel-dynasty/pages/admin/admin_login.php`

## 📁 New Organized Project Structure

```
Hotel Booking Management System/
├── config/                    # Configuration files
│   └── connection.php        # Database connection
│
├── includes/                  # Reusable components
│   ├── header.php            # Main site header
│   ├── adminheader.php       # Admin panel header
│   └── footer.php            # Site footer
│
├── pages/                     # All page files (NEW STRUCTURE)
│   ├── index.php             # Homepage
│   │
│   ├── auth/                 # Authentication pages
│   │   ├── login.php         # User login
│   │   ├── register.php      # User registration
│   │   └── logout.php        # User logout
│   │
│   ├── user/                 # User-facing pages
│   │   ├── welcome.php       # User dashboard
│   │   ├── account.php       # Account settings
│   │   ├── rooms.php         # Browse rooms
│   │   ├── details.php       # Room details
│   │   ├── my_booking.php    # Booking history
│   │   └── contact.php       # Contact form
│   │
│   └── admin/                # Admin panel pages
│       ├── admin_login.php   # Admin login
│       ├── admin_logout.php  # Admin logout
│       ├── dashboard.php     # Admin dashboard
│       ├── create_admin.php  # Create new admin
│       ├── add_room.php      # Add new room
│       ├── edit_room.php     # Edit room details
│       ├── add_user.php      # Add new user
│       ├── edit_user.php     # Edit user details
│       ├── edit_booking.php  # Edit reservations
│       └── dusers.php        # Manage users
│
├── assets/                    # Frontend assets (REORGANIZED)
│   ├── css/                  # Stylesheets
│   │   ├── index.css
│   │   ├── rooms.css
│   │   ├── admin.css
│   │   ├── dashboard.css
│   │   ├── account.css
│   │   ├── bookHere.css
│   │   ├── contact.css
│   │   ├── edit_user.css
│   │   ├── footer.css
│   │   ├── mybookings.css
│   │   ├── reg-log.css
│   │   ├── register.css
│   │   └── welcome.css
│   │
│   ├── js/                   # JavaScript files
│   │   ├── bookHere.js
│   │   ├── details.js
│   │   └── login-reg.js
│   │
│   └── images/               # Images and media
│       ├── images/           # General images
│       ├── room-types/       # Room type images
│       ├── services/         # Service images
│       └── login-reg-img/    # Auth page images
│
├── uploads/                   # User uploaded files
│   └── rooms/                # Room images
│
├── .gitignore
└── README.md                 # This file
```

## 🎯 Usage

### For Customers

1. **Register an Account**
   - Navigate to registration page
   - Fill in personal details
   - Submit to create account

2. **Browse and Book Rooms**
   - Login to your account
   - Browse available rooms
   - Select check-in and check-out dates
   - Choose room type
   - Confirm booking

3. **Manage Bookings**
   - View all bookings in "My Bookings"
   - Edit booking details
   - Cancel bookings if needed

### For Administrators

1. **Login to Admin Panel**
   - Access admin login page
   - Enter admin credentials
   - Access dashboard

2. **Manage Rooms**
   - Add new rooms with images
   - Edit room details and pricing
   - Update room availability
   - Delete rooms

3. **Manage Bookings**
   - View all reservations
   - Update booking status
   - Process cancellations
   - Generate reports

4. **Manage Users**
   - View registered users
   - Edit user information
   - Manage user accounts

## 🔑 Default Credentials

### Admin Account
```
Username: admin
Password: admin123
(Change after first login)
```

## 🔒 Security Features

- **Password Hashing** - Secure password storage with PHP password_hash()
- **SQL Injection Prevention** - Prepared statements and input validation
- **XSS Protection** - Input sanitization and output encoding
- **Session Security** - Secure session management
- **CSRF Protection** - Form tokens for sensitive operations
- **Access Control** - Role-based authentication

## 🎨 Customization

### Modify Branding

Edit header files:
```php
// includes/header.php
<h1>Your Hotel Name</h1>
```

### Update Colors

Edit CSS files in `assets/css/`:
```css
:root {
    --primary-color: #your-color;
    --secondary-color: #your-color;
}
```

### Add Room Types

Edit room management in admin panel or directly in database:
```sql
INSERT INTO rooms (room_type, room_name, description, price, capacity)
VALUES ('Deluxe', 'Deluxe Ocean View', 'Luxurious room with ocean view', 199.99, 2);
```

## 🐛 Troubleshooting

### Database Connection Issues
- Verify MySQL service is running
- Check credentials in `config/connection.php`
- Ensure database exists

### Session Issues
- Check PHP session configuration
- Verify write permissions on session directory
- Clear browser cookies

### Image Upload Problems
- Check `uploads/` directory permissions
- Verify PHP `upload_max_filesize` setting
- Ensure proper file extensions

## 🚀 Deployment

### Production Checklist

- [ ] Change default admin password
- [ ] Update database credentials
- [ ] Enable HTTPS/SSL
- [ ] Set proper file permissions
- [ ] Configure error logging
- [ ] Set up regular backups
- [ ] Implement rate limiting
- [ ] Add email notifications

### Hosting Requirements

- PHP 7.4+
- MySQL 5.7+
- Apache/Nginx
- Min 1GB RAM
- 10GB storage

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- PHP community for excellent documentation
- MySQL for reliable database solutions
- Contributors and testers

## 📞 Support

For issues and questions:
- Open an issue on GitHub
- Email: support@hoteldynasty.com

## 🔮 Future Enhancements

- [ ] Payment gateway integration
- [ ] Email notifications
- [ ] SMS alerts for bookings
- [ ] Multi-language support
- [ ] Advanced reporting
- [ ] Room availability calendar
- [ ] Review and rating system
- [ ] Loyalty program
- [ ] Mobile app
- [ ] API for third-party integrations

---

<div align="center">

**Hotel Dynasty - Where Luxury Meets Tranquility**

*Built with ❤️ for seamless hotel management*

</div>
