# EmailJS Setup Guide for Ahmed Farag's Architecture Portfolio

## Overview
The contact form is configured to use EmailJS service to send emails directly from the website without needing a backend server.

## Setup Steps

### 1. Create EmailJS Account
- Go to [https://www.emailjs.com/](https://www.emailjs.com/)
- Sign up for a free account (allows 200 emails/month)

### 2. Add Email Service
- In your EmailJS dashboard, go to "Email Services"
- Click "Add New Service"
- Choose your email provider (Gmail, Outlook, etc.)
- Follow the setup instructions to connect your email account

### 3. Create Email Template
- Go to "Email Templates" in your dashboard
- Click "Create New Template" OR edit your existing template_kk0qj8c
- Use this EXACT template structure:

**Subject Line:**
```
رسالة جديدة من موقع احمد فرج المعماري - {{project_type}}
```

**Email Body:**
```
مرحباً {{to_name}},

لقد وصلتك رسالة جديدة من موقع احمد فرج المعماري:

=== معلومات العميل ===
الاسم: {{from_name}}
البريد الإلكتروني: {{from_email}}
رقم الهاتف: {{phone}}
نوع المشروع: {{project_type}}

=== تفاصيل المشروع ===
{{message}}

=== معلومات إضافية ===
تاريخ الإرسال: {{current_date}}
الموقع: موقع احمد فرج المعماري

---
يرجى الرد على هذا البريد الإلكتروني للتواصل مع العميل مباشرة.
```

### 4. Update Configuration
In the `baba.html` file, update these values with your actual EmailJS credentials:

```javascript
const serviceID = 'your_service_id_here';     // From Email Services page
const templateID = 'your_template_id_here';   // From Email Templates page  
const publicKey = 'your_public_key_here';     // From Account > API Keys
```

### 5. Update Email Address
Replace the email address in the template parameters:

```javascript
to_email: 'afrj46453@gmail.com' // Ahmed Farag's actual email address
```

## Template Variables
The form sends these variables to your email template:

- `{{from_name}}` - Client's name
- `{{from_email}}` - Client's email address
- `{{phone}}` - Client's phone number
- `{{project_type}}` - Type of architectural project
- `{{message}}` - Client's message
- `{{to_email}}` - Your email address (Ahmed's email)

## Testing
1. Save your changes
2. Open the website in a browser
3. Fill out the contact form
4. Submit and check your email inbox
5. Check spam folder if email doesn't arrive

## Troubleshooting
- Make sure all IDs match exactly (case-sensitive)
- Verify your email service is properly connected
- Check EmailJS dashboard for error logs
- Ensure your domain is added to allowed origins (for production)

## Free Plan Limits
- 200 emails per month
- EmailJS branding in emails
- Basic support

For higher volume or to remove branding, consider upgrading to a paid plan.