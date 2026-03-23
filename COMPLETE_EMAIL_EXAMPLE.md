# Complete Working EmailJS Example

## Understanding EmailJS Behavior

**IMPORTANT:** EmailJS will ALWAYS show your email as the sender, not the visitor's email. This is normal and secure behavior. However, we can:
1. Display visitor information clearly in the email body
2. Set up reply-to functionality so you can reply directly to visitors
3. Format the email professionally

## Complete HTML Form Code

```html
<form class="contact-form" id="contactForm">
    <div class="form-row">
        <div class="form-group">
            <label for="name">الاسم *</label>
            <input type="text" id="name" name="name" required>
            <span class="error-message" id="nameError"></span>
        </div>
        <div class="form-group">
            <label for="email">البريد الإلكتروني *</label>
            <input type="email" id="email" name="email" required>
            <span class="error-message" id="emailError"></span>
        </div>
    </div>
    <div class="form-group">
        <label for="phone">رقم الهاتف</label>
        <input type="tel" id="phone" name="phone">
        <span class="error-message" id="phoneError"></span>
    </div>
    <div class="form-group">
        <label for="project-type">نوع المشروع</label>
        <select id="project-type" name="project_type">
            <option value="">اختر نوع المشروع</option>
            <option value="مشروع سكني">مشروع سكني</option>
            <option value="مشروع تجاري">مشروع تجاري</option>
            <option value="مشروع عام">مشروع عام</option>
            <option value="أعمال الجبس">أعمال الجبس</option>
            <option value="تجديد وترميم">تجديد وترميم</option>
            <option value="استشارة معمارية">استشارة معمارية</option>
            <option value="أخرى">أخرى</option>
        </select>
    </div>
    <div class="form-group">
        <label for="message">تفاصيل المشروع *</label>
        <textarea id="message" name="message" rows="5" placeholder="اكتب تفاصيل مشروعك والمتطلبات الخاصة..." required></textarea>
        <span class="error-message" id="messageError"></span>
    </div>
    <button type="submit" class="btn btn-primary btn-full" id="submitBtn">
        <span class="btn-text" id="btnText">إرسال الرسالة</span>
        <i class="fas fa-paper-plane btn-icon" id="btnIcon"></i>
    </button>
    <div class="form-messages">
        <div class="success-message" id="successMessage">
            <i class="fas fa-check-circle"></i>
            <span>تم إرسال رسالتك بنجاح! سأتواصل معك قريباً.</span>
        </div>
        <div class="error-message-general" id="errorMessage">
            <i class="fas fa-exclamation-circle"></i>
            <span>فشل في إرسال الرسالة. يرجى المحاولة مرة أخرى أو التواصل مباشرة.</span>
        </div>
    </div>
</form>
```

## Complete JavaScript Code

```javascript
// EmailJS Configuration
const serviceID = 'service_z0rrddd';     // Your service ID
const templateID = 'template_kk0qj8c';   // Your template ID  
const publicKey = 'QDSXBXp0ulRypL9ha';   // Your public key

// Initialize EmailJS
emailjs.init(publicKey);

// Form submission handler
document.getElementById('contactForm').addEventListener('submit', function(e) {
    e.preventDefault();
    
    // Get form values
    const name = document.getElementById('name').value.trim();
    const email = document.getElementById('email').value.trim();
    const phone = document.getElementById('phone').value.trim();
    const projectType = document.getElementById('project-type').value;
    const message = document.getElementById('message').value.trim();
    
    // Clear previous errors
    document.querySelectorAll('.error-message').forEach(error => {
        error.style.display = 'none';
        error.textContent = '';
    });
    
    // Hide previous messages
    document.getElementById('successMessage').style.display = 'none';
    document.getElementById('errorMessage').style.display = 'none';
    
    // Validation
    let hasErrors = false;
    
    if (name.length < 2) {
        showError('nameError', 'الاسم مطلوب ويجب أن يحتوي على حرفين على الأقل');
        hasErrors = true;
    }
    
    const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
    if (!email || !emailRegex.test(email)) {
        showError('emailError', 'يرجى إدخال بريد إلكتروني صحيح');
        hasErrors = true;
    }
    
    if (message.length < 10) {
        showError('messageError', 'الرسالة مطلوبة ويجب أن تحتوي على 10 أحرف على الأقل');
        hasErrors = true;
    }
    
    if (hasErrors) return;
    
    // Show loading state
    const submitBtn = document.getElementById('submitBtn');
    const btnText = document.getElementById('btnText');
    const btnIcon = document.getElementById('btnIcon');
    
    submitBtn.disabled = true;
    btnText.textContent = 'جاري الإرسال...';
    btnIcon.className = 'fas fa-spinner fa-spin btn-icon';
    
    // Prepare template parameters
    const templateParams = {
        // Visitor information (displayed in email body)
        visitor_name: name,
        visitor_email: email,
        visitor_phone: phone || 'غير محدد',
        visitor_project_type: projectType || 'استفسار عام',
        visitor_message: message,
        
        // Your information
        to_name: 'احمد فرج',
        to_email: 'abdotete142@gmail.com',
        
        // Reply-to field (enables direct reply to visitor)
        reply_to: email,
        
        // Additional information
        submission_date: new Date().toLocaleDateString('ar-EG', {
            year: 'numeric',
            month: 'long',
            day: 'numeric',
            hour: '2-digit',
            minute: '2-digit'
        }),
        subject_project_type: projectType || 'استفسار عام'
    };
    
    // Send email
    emailjs.send(serviceID, templateID, templateParams)
        .then(function(response) {
            console.log('SUCCESS!', response.status, response.text);
            
            // Show success message
            document.getElementById('successMessage').style.display = 'flex';
            
            // Reset form
            document.getElementById('contactForm').reset();
            
            // Hide success message after 8 seconds
            setTimeout(() => {
                document.getElementById('successMessage').style.display = 'none';
            }, 8000);
            
        }, function(error) {
            console.log('FAILED...', error);
            
            // Show error message
            document.getElementById('errorMessage').style.display = 'flex';
            
            // Hide error message after 8 seconds
            setTimeout(() => {
                document.getElementById('errorMessage').style.display = 'none';
            }, 8000);
        })
        .finally(function() {
            // Reset button state
            submitBtn.disabled = false;
            btnText.textContent = 'إرسال الرسالة';
            btnIcon.className = 'fas fa-paper-plane btn-icon';
        });
});

// Helper function to show errors
function showError(elementId, message) {
    const errorElement = document.getElementById(elementId);
    errorElement.textContent = message;
    errorElement.style.display = 'block';
}
```

## EmailJS Template Setup (EXACT FORMAT)

### Subject Line:
```
طلب جديد من {{visitor_name}} - {{subject_project_type}}
```

### Reply-To Field:
```
{{reply_to}}
```

### Email Body (HTML):
```html
<div style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px;">
    <h2 style="color: #c9a96e;">طلب جديد من موقع احمد فرج المعماري</h2>
    
    <p>مرحباً {{to_name}},</p>
    
    <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin: 20px 0;">
        <h3 style="color: #c9a96e;">معلومات العميل</h3>
        <p><strong>الاسم:</strong> {{visitor_name}}</p>
        <p><strong>البريد الإلكتروني:</strong> <a href="mailto:{{visitor_email}}">{{visitor_email}}</a></p>
        <p><strong>رقم الهاتف:</strong> {{visitor_phone}}</p>
        <p><strong>نوع المشروع:</strong> {{visitor_project_type}}</p>
    </div>
    
    <div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin: 20px 0;">
        <h3 style="color: #c9a96e;">تفاصيل المشروع</h3>
        <p style="white-space: pre-wrap;">{{visitor_message}}</p>
    </div>
    
    <p style="color: #666; font-size: 14px;">
        <strong>تاريخ الإرسال:</strong> {{submission_date}}<br>
        <strong>المصدر:</strong> موقع احمد فرج المعماري
    </p>
    
    <div style="text-align: center; margin: 30px 0;">
        <a href="mailto:{{visitor_email}}" style="background: #c9a96e; color: white; padding: 12px 24px; text-decoration: none; border-radius: 5px;">
            الرد على العميل
        </a>
    </div>
</div>
```

## What You'll Receive

**Email Header:**
- **From:** Your Email Service Name (abdotete142@gmail.com)
- **Subject:** طلب جديد من محمد أحمد - مشروع سكني
- **Reply-To:** mohamed@example.com (visitor's actual email)

**Email Body:** Professional HTML formatted email with all visitor details clearly displayed

## Key Points:
1. ✅ **Sender shows your email** (this is correct and secure)
2. ✅ **Visitor info is clearly displayed** in the email body
3. ✅ **Reply-to is set to visitor's email** (you can reply directly)
4. ✅ **Professional HTML formatting** with Arabic support
5. ✅ **All form data is captured** and displayed properly

This setup ensures you get all visitor information while maintaining security and enabling easy communication!