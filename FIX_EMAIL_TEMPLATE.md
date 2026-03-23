# Fix EmailJS Template - Complete Setup Guide

## The Problem
EmailJS emails always show YOUR email as the sender (not the visitor's email) for security reasons. This is normal behavior. However, we can properly display visitor information and set up reply-to functionality.

## Complete Solution

### 1. Login to EmailJS Dashboard
- Go to [https://dashboard.emailjs.com/](https://dashboard.emailjs.com/)
- Login with your account

### 2. Edit Your Email Template
- Find template ID: `template_kk0qj8c`
- Click "Edit" on that template

### 3. EXACT Template Setup

**Subject Line:**
```
طلب جديد من {{visitor_name}} - {{subject_project_type}}
```

**From Name:** (Leave as default - your email service name)

**From Email:** (Leave as default - your connected email)

**Reply To:** 
```
{{reply_to}}
```

**Email Body (HTML Format):**
```html
<div style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px; background-color: #f9f9f9;">
    <div style="background-color: #c9a96e; color: white; padding: 20px; text-align: center; border-radius: 10px 10px 0 0;">
        <h2 style="margin: 0;">طلب جديد من موقع احمد فرج المعماري</h2>
    </div>
    
    <div style="background-color: white; padding: 30px; border-radius: 0 0 10px 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
        <p style="font-size: 16px; color: #333; margin-bottom: 20px;">مرحباً {{to_name}},</p>
        
        <p style="color: #666; margin-bottom: 30px;">لقد وصلك طلب جديد من موقعك الإلكتروني:</p>
        
        <div style="background-color: #f8f9fa; padding: 20px; border-radius: 8px; margin-bottom: 20px;">
            <h3 style="color: #c9a96e; margin-top: 0; margin-bottom: 15px;">معلومات العميل</h3>
            <table style="width: 100%; border-collapse: collapse;">
                <tr>
                    <td style="padding: 8px 0; font-weight: bold; color: #333; width: 30%;">الاسم:</td>
                    <td style="padding: 8px 0; color: #666;">{{visitor_name}}</td>
                </tr>
                <tr>
                    <td style="padding: 8px 0; font-weight: bold; color: #333;">البريد الإلكتروني:</td>
                    <td style="padding: 8px 0; color: #666;">
                        <a href="mailto:{{visitor_email}}" style="color: #c9a96e; text-decoration: none;">{{visitor_email}}</a>
                    </td>
                </tr>
                <tr>
                    <td style="padding: 8px 0; font-weight: bold; color: #333;">رقم الهاتف:</td>
                    <td style="padding: 8px 0; color: #666;">{{visitor_phone}}</td>
                </tr>
                <tr>
                    <td style="padding: 8px 0; font-weight: bold; color: #333;">نوع المشروع:</td>
                    <td style="padding: 8px 0; color: #666;">{{visitor_project_type}}</td>
                </tr>
            </table>
        </div>
        
        <div style="background-color: #f8f9fa; padding: 20px; border-radius: 8px; margin-bottom: 20px;">
            <h3 style="color: #c9a96e; margin-top: 0; margin-bottom: 15px;">تفاصيل المشروع</h3>
            <p style="color: #333; line-height: 1.6; margin: 0; white-space: pre-wrap;">{{visitor_message}}</p>
        </div>
        
        <div style="background-color: #e9ecef; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
            <p style="margin: 0; color: #666; font-size: 14px;">
                <strong>تاريخ الإرسال:</strong> {{submission_date}}<br>
                <strong>المصدر:</strong> موقع احمد فرج المعماري
            </p>
        </div>
        
        <div style="text-align: center; margin-top: 30px;">
            <a href="mailto:{{visitor_email}}" style="background-color: #c9a96e; color: white; padding: 12px 30px; text-decoration: none; border-radius: 5px; display: inline-block; font-weight: bold;">
                الرد على العميل
            </a>
        </div>
        
        <p style="color: #999; font-size: 12px; text-align: center; margin-top: 30px; border-top: 1px solid #eee; padding-top: 20px;">
            هذه الرسالة تم إرسالها من نموذج الاتصال في موقع احمد فرج المعماري
        </p>
    </div>
</div>
```

### 4. Template Variables Used
Make sure these EXACT variable names are in your template:

- `{{visitor_name}}` - Client's name
- `{{visitor_email}}` - Client's email address
- `{{visitor_phone}}` - Client's phone number
- `{{visitor_project_type}}` - Type of project
- `{{visitor_message}}` - Client's message
- `{{to_name}}` - Your name (احمد فرج)
- `{{reply_to}}` - Sets reply-to field to client's email
- `{{submission_date}}` - Date and time of submission
- `{{subject_project_type}}` - Project type for subject line

### 5. Save and Test
1. Click "Save" in EmailJS dashboard
2. Test the contact form on your website
3. Check your email inbox

## Expected Result
After this setup, you'll receive emails that:

✅ **Show your email as sender** (normal EmailJS behavior)
✅ **Display visitor's name and email clearly** in the email body
✅ **Allow you to reply directly** to the visitor (reply-to field)
✅ **Include all form information** in a professional format
✅ **Have proper Arabic formatting** and styling

## Sample Email You'll Receive:

**From:** Your Email Service (abdotete142@gmail.com)
**Subject:** طلب جديد من محمد أحمد - مشروع سكني
**Reply-To:** mohamed@example.com (visitor's email)

**Email Body:** Professional HTML formatted email with all visitor details

## Important Notes:
- The "From" field will always show your email (this is correct)
- The visitor's email appears in the email body and reply-to field
- When you hit "Reply", it will automatically reply to the visitor's email
- All visitor information is clearly displayed in the email content

## Troubleshooting:
- Make sure variable names match exactly (case-sensitive)
- Use double curly braces {{ }} around all variables
- Save the template after making changes
- Clear browser cache and test again