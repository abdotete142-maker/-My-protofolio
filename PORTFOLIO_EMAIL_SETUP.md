# Portfolio EmailJS Setup Guide - Abdelrahman Ahmed

## Updated JavaScript Implementation ✅

Your `index.html` has been updated with the correct EmailJS implementation that will properly display visitor information in emails.

## EmailJS Template Setup

### 1. Login to EmailJS Dashboard
- Go to [https://dashboard.emailjs.com/](https://dashboard.emailjs.com/)
- Login with your account

### 2. Edit Your Template
- Find template ID: `template_kk0qj8c`
- Click "Edit" on that template

### 3. EXACT Template Configuration

**Subject Line:**
```
New Project Inquiry from {{visitor_name}} - {{subject_line}}
```

**From Name:** (Leave as default - your email service name)

**From Email:** (Leave as default - your connected email)

**Reply To:** 
```
{{reply_to}}
```

**Email Body (HTML Format):**
```html
<div style="font-family: 'Inter', Arial, sans-serif; max-width: 700px; margin: 0 auto; padding: 20px; background-color: #f8fafc;">
    <!-- Header -->
    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 30px; text-align: center; border-radius: 12px 12px 0 0;">
        <h1 style="margin: 0; font-size: 24px; font-weight: 600;">New Project Inquiry</h1>
        <p style="margin: 10px 0 0 0; opacity: 0.9;">From your portfolio website</p>
    </div>
    
    <!-- Main Content -->
    <div style="background-color: white; padding: 40px; border-radius: 0 0 12px 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.1);">
        <p style="font-size: 18px; color: #1a202c; margin-bottom: 30px; font-weight: 500;">Hi {{to_name}},</p>
        
        <p style="color: #4a5568; margin-bottom: 30px; line-height: 1.6;">You've received a new project inquiry from your portfolio website. Here are the details:</p>
        
        <!-- Client Information -->
        <div style="background-color: #f7fafc; padding: 25px; border-radius: 10px; margin-bottom: 25px; border-left: 4px solid #667eea;">
            <h2 style="color: #667eea; margin-top: 0; margin-bottom: 20px; font-size: 18px; font-weight: 600;">Client Information</h2>
            <table style="width: 100%; border-collapse: collapse;">
                <tr>
                    <td style="padding: 10px 0; font-weight: 600; color: #2d3748; width: 25%; vertical-align: top;">Name:</td>
                    <td style="padding: 10px 0; color: #4a5568; font-size: 16px;">{{visitor_name}}</td>
                </tr>
                <tr>
                    <td style="padding: 10px 0; font-weight: 600; color: #2d3748; vertical-align: top;">Email:</td>
                    <td style="padding: 10px 0; color: #4a5568;">
                        <a href="mailto:{{visitor_email}}" style="color: #667eea; text-decoration: none; font-weight: 500;">{{visitor_email}}</a>
                    </td>
                </tr>
                <tr>
                    <td style="padding: 10px 0; font-weight: 600; color: #2d3748; vertical-align: top;">Subject:</td>
                    <td style="padding: 10px 0; color: #4a5568; font-size: 16px;">{{visitor_subject}}</td>
                </tr>
                <tr>
                    <td style="padding: 10px 0; font-weight: 600; color: #2d3748; vertical-align: top;">Project Type:</td>
                    <td style="padding: 10px 0; color: #4a5568;">
                        <span style="background-color: #667eea; color: white; padding: 4px 12px; border-radius: 20px; font-size: 14px; font-weight: 500;">{{visitor_project_type}}</span>
                    </td>
                </tr>
            </table>
        </div>
        
        <!-- Project Details -->
        <div style="background-color: #f7fafc; padding: 25px; border-radius: 10px; margin-bottom: 25px; border-left: 4px solid #48bb78;">
            <h2 style="color: #48bb78; margin-top: 0; margin-bottom: 15px; font-size: 18px; font-weight: 600;">Project Details</h2>
            <div style="background-color: white; padding: 20px; border-radius: 8px; border: 1px solid #e2e8f0;">
                <p style="color: #2d3748; line-height: 1.7; margin: 0; white-space: pre-wrap; font-size: 15px;">{{visitor_message}}</p>
            </div>
        </div>
        
        <!-- Submission Info -->
        <div style="background-color: #edf2f7; padding: 20px; border-radius: 8px; margin-bottom: 30px;">
            <p style="margin: 0; color: #4a5568; font-size: 14px; line-height: 1.5;">
                <strong style="color: #2d3748;">Submitted:</strong> {{submission_date}}<br>
                <strong style="color: #2d3748;">Source:</strong> Abdelrahman Ahmed Portfolio Website<br>
                <strong style="color: #2d3748;">Client IP:</strong> Will reply directly to {{visitor_email}}
            </p>
        </div>
        
        <!-- Action Buttons -->
        <div style="text-align: center; margin: 30px 0;">
            <a href="mailto:{{visitor_email}}?subject=Re: {{visitor_subject}}" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 15px 30px; text-decoration: none; border-radius: 8px; display: inline-block; font-weight: 600; margin-right: 15px; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);">
                Reply to Client
            </a>
            <a href="tel:{{visitor_email}}" style="background-color: #48bb78; color: white; padding: 15px 30px; text-decoration: none; border-radius: 8px; display: inline-block; font-weight: 600; box-shadow: 0 4px 15px rgba(72, 187, 120, 0.4);">
                Call Client
            </a>
        </div>
        
        <!-- Footer -->
        <div style="text-align: center; margin-top: 40px; padding-top: 25px; border-top: 2px solid #e2e8f0;">
            <p style="color: #a0aec0; font-size: 13px; margin: 0; line-height: 1.5;">
                This message was sent from the contact form on your portfolio website.<br>
                <strong>Abdelrahman Ahmed - Frontend Developer</strong><br>
                <a href="mailto:abdotete142@gmail.com" style="color: #667eea; text-decoration: none;">abdotete142@gmail.com</a>
            </p>
        </div>
    </div>
</div>
```

### 4. Template Variables Used

Make sure these EXACT variable names are in your template:

- `{{visitor_name}}` - Client's name
- `{{visitor_email}}` - Client's email address  
- `{{visitor_subject}}` - Email subject
- `{{visitor_project_type}}` - Type of project
- `{{visitor_message}}` - Client's message
- `{{to_name}}` - Your name (Abdelrahman Ahmed)
- `{{reply_to}}` - Sets reply-to field to client's email
- `{{submission_date}}` - Date and time of submission
- `{{subject_line}}` - Combined subject for email subject

### 5. Save and Test

1. Click "Save" in EmailJS dashboard
2. Test the contact form on your portfolio
3. Check your email inbox (abdotete142@gmail.com)

## Expected Email Result

**From:** Your Email Service (abdotete142@gmail.com)
**Subject:** New Project Inquiry from John Doe - Website Development - E-commerce Platform
**Reply-To:** john@example.com (client's email)

**Email Body:** Professional HTML formatted email with:
- ✅ Client's name prominently displayed
- ✅ Client's email as clickable link  
- ✅ Subject and project type clearly shown
- ✅ Full message content in formatted box
- ✅ Professional design with your branding
- ✅ Action buttons to reply or call client

## Key Benefits

1. **Professional Appearance:** Beautiful HTML email design
2. **Client Information:** All details clearly displayed
3. **Easy Reply:** Click button to reply directly to client
4. **Project Context:** Subject and project type highlighted
5. **Branding:** Consistent with your portfolio design

## Important Notes

- The "From" field will always show your email (this is secure and correct)
- The client's email appears in the email body and reply-to field
- When you hit "Reply", it automatically replies to the client's email
- All client information is professionally formatted and easy to read

Your portfolio contact form is now ready to receive professional project inquiries!