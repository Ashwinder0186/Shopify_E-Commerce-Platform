# 🛒 Shopify2 - E-Commerce Platform

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Django](https://img.shields.io/badge/Django-4.0+-green.svg)
![SQLite](https://img.shields.io/badge/SQLite-3-lightgrey.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

**A full-featured e-commerce web application built with Django, replicating core functionalities of modern online marketplaces**

[Features](#features) • [Demo](#demo) • [Installation](#installation) • [Tech Stack](#tech-stack)

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Key Functionalities](#key-functionalities)
- [Screenshots](#screenshots)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

## 🎯 Overview

**Shopify2** is a comprehensive e-commerce platform developed using Django framework that demonstrates full-stack web development capabilities. The application replicates essential features of popular online marketplaces including product browsing, shopping cart management, secure payment processing, and order tracking.

This project showcases:
- **Full-Stack Development**: Django backend with responsive frontend
- **Database Design**: Efficient data modeling with SQLite
- **Payment Integration**: Secure payment gateway implementation (RazorPay)
- **User Experience**: Intuitive interface with search, filtering, and cart management
- **Security**: Authentication, authorization, and secure transaction handling

---

## ✨ Features

### 🛍️ Shopping Experience
- **Product Catalog**: Browse extensive product listings with detailed information
- **Advanced Search**: Algorithmic search with optimized database queries
- **Smart Filtering**: Filter products by category, price range, and attributes
- **Shopping Cart**: Add, update, and remove items with real-time calculations
- **Wishlist**: Save favorite products for later

### 💳 Payment & Orders
- **Secure Checkout**: Integrated RazorPay payment gateway
- **Order Management**: Complete order history and status tracking
- **Email Notifications**: Automated order confirmations and updates
- **Invoice Generation**: Digital receipts for completed purchases

### 👤 User Management
- **User Authentication**: Secure registration and login system
- **Profile Management**: Edit personal information and preferences
- **Address Book**: Save multiple shipping addresses
- **Order History**: Track past and current orders

### 🔧 Admin Features
- **Product Management**: Add, edit, and delete products
- **Inventory Control**: Track stock levels and availability
- **Order Processing**: Manage and fulfill customer orders
- **User Management**: Admin dashboard for system oversight

---

## 🛠️ Tech Stack

### Backend
- **Framework**: Django 4.0+
- **Language**: Python 3.8+
- **Database**: SQLite3
- **ORM**: Django ORM

### Frontend
- **Templates**: Django Templates
- **Styling**: Bootstrap 5
- **JavaScript**: Vanilla JS for dynamic interactions
- **Icons**: Font Awesome

### Payment Integration
- **Gateway**: RazorPay API
- **Security**: PCI DSS compliant payment processing

### Additional Tools
- **Email**: Django SMTP for notifications
- **Media**: Django media handling for product images
- **Static Files**: Django static files management

---

## 📥 Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Virtual environment (recommended)

### Step 1: Clone the Repository
```bash
git clone https://github.com/Ashwinder0186/Shopify2.git
cd Shopify2
```

### Step 2: Create Virtual Environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Configure Environment Variables
Create a `.env` file in the root directory:
```env
SECRET_KEY=your_django_secret_key
DEBUG=True
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
EMAIL_HOST_USER=your_email@gmail.com
EMAIL_HOST_PASSWORD=your_email_password
```

### Step 5: Database Setup
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

### Step 6: Collect Static Files
```bash
python manage.py collectstatic
```

### Step 7: Run Development Server
```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` in your browser.

---

## 🚀 Usage

### For Customers

1. **Browse Products**
   - Navigate to the home page
   - Browse categories or use search functionality
   - Apply filters to find specific products

2. **Add to Cart**
   - Click on product for details
   - Select quantity and add to cart
   - View cart and proceed to checkout

3. **Checkout Process**
   - Enter shipping information
   - Select payment method
   - Complete payment via RazorPay
   - Receive order confirmation email

4. **Track Orders**
   - Login to your account
   - View order history
   - Track order status

### For Administrators

1. **Access Admin Panel**
   ```
   http://127.0.0.1:8000/admin/
   ```

2. **Manage Products**
   - Add new products with images and details
   - Update inventory and pricing
   - Categorize products

3. **Process Orders**
   - View pending orders
   - Update order status
   - Generate shipping labels

---

## 📁 Project Structure

```
Shopify2/
│
├── manage.py                   # Django management script
├── db.sqlite3                  # SQLite database
├── requirements.txt            # Project dependencies
│
├── shop/                       # Main shop application
│   ├── models.py              # Database models
│   ├── views.py               # View controllers
│   ├── urls.py                # URL routing
│   ├── forms.py               # Form definitions
│   ├── admin.py               # Admin configurations
│   └── templates/             # HTML templates
│
├── mycart/                     # Shopping cart application
│   ├── models.py              # Cart models
│   ├── views.py               # Cart views
│   └── urls.py                # Cart URLs
│
├── PayTm/                      # Payment integration
│   ├── views.py               # Payment processing
│   └── urls.py                # Payment URLs
│
├── media/                      # User uploaded content
│   └── product_images/        # Product photos
│
├── static/                     # Static files
│   ├── css/                   # Stylesheets
│   ├── js/                    # JavaScript files
│   └── images/                # Site images
│
└── Procfile                    # Deployment configuration
```

---

## 🔑 Key Functionalities

### 1. Product Management System
```python
# models.py
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    description = models.TextField()
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    stock = models.IntegerField()
    image = models.ImageField(upload_to='product_images/')
```

### 2. Shopping Cart Logic
- Session-based cart for guest users
- Database-stored carts for authenticated users
- Real-time price calculations with tax
- Quantity management with stock validation

### 3. Payment Processing
- RazorPay integration for secure payments
- Order verification and confirmation
- Failed payment handling and retry logic
- Transaction history tracking

### 4. Search & Filter Algorithm
```python
# Optimized database queries
products = Product.objects.filter(
    Q(name__icontains=query) | 
    Q(description__icontains=query)
).select_related('category').order_by('-created_at')
```

### 5. Email Notification System
- Order confirmation emails
- Shipping status updates
- Payment receipts
- Password reset functionality

---

## 📸 Screenshots

### Home Page
*Browse products with featured items and categories*

### Product Detail
*Detailed product information with add to cart*

### Shopping Cart
*Review items before checkout*

### Checkout & Payment
*Secure payment processing with RazorPay*

### Order Tracking
*Track order status and history*

---

## 🔮 Future Enhancements

- [ ] **Product Reviews & Ratings**: Customer feedback system
- [ ] **Advanced Analytics**: Sales dashboard with charts and insights
- [ ] **Recommendation Engine**: ML-based product suggestions
- [ ] **Multi-Vendor Support**: Marketplace functionality
- [ ] **Mobile App**: React Native companion app
- [ ] **Live Chat**: Customer support integration
- [ ] **Social Media Integration**: Share products on social platforms
- [ ] **Coupon & Discount System**: Promotional code functionality
- [ ] **Multi-Currency Support**: International payment options
- [ ] **Inventory Alerts**: Low stock notifications for admins

---

## 📊 Performance Features

- **Optimized Queries**: Used `select_related()` and `prefetch_related()` for efficiency
- **Caching**: Implemented Django caching for frequently accessed data
- **Pagination**: Efficient pagination for large product catalogs
- **Image Optimization**: Compressed images for faster loading
- **CDN Ready**: Static files configured for CDN deployment

---

## 🧪 Testing

Run tests with:
```bash
python manage.py test
```

### Test Coverage
- Unit tests for models
- Integration tests for views
- Payment gateway testing (sandbox mode)
- Form validation tests

---

## 🚀 Deployment

### Heroku Deployment
```bash
heroku create shopify2-app
git push heroku master
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```

### Environment Setup
- Configure environment variables on hosting platform
- Set `DEBUG=False` for production
- Use PostgreSQL for production database
- Configure media file storage (AWS S3)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Ashwinder Singh**
- **GitHub**: [@Ashwinder0186](https://github.com/Ashwinder0186)
- **LinkedIn**: [singh-ashwinder](https://linkedin.com/in/singh-ashwinder)
- **Email**: singhashwinder0186@gmail.com
- **Education**: MS in Computer Science, University of Texas at Arlington (GPA: 4.0/4.0)

### Background
Full-stack developer with experience in Python, Django, and financial technology solutions. Previously worked at Tata Consultancy Services developing automation tools for JPMorgan Chase.

---

## 🙏 Acknowledgments

- [Django Documentation](https://docs.djangoproject.com/)
- [Bootstrap](https://getbootstrap.com/) for responsive design
- [RazorPay](https://razorpay.com/) for payment gateway
- [Font Awesome](https://fontawesome.com/) for icons

---

## 📞 Support

For support, email singhashwinder0186@gmail.com or create an issue in the repository.

---

<div align="center">

**⭐ If you found this project helpful, please consider giving it a star!**

Made with ❤️ using Django

</div>
