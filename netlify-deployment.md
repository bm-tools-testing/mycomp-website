# Deploying to Netlify: A Complete Guide

## Prerequisites

- A [Netlify account](https://app.netlify.com/signup)
- Your website code in a Git repository (GitHub, GitLab, or Bitbucket)
- Basic understanding of Git and command line

## Deployment Steps

### 1. Initial Deployment

1. **Connect to Netlify**
   - Log in to your Netlify account
   - Click "New site from Git"
   - Choose your Git provider
   - Select your repository

2. **Configure Build Settings**
   ```yaml
   # No build command needed for static site
   Build command: (leave empty)
   Publish directory: ./
   ```

3. **Deploy Site**
   - Click "Deploy site"
   - Wait for deployment to complete
   - Your site will be live at `your-site-name.netlify.app`

### 2. Setting Up Netlify CMS

1. **Create Admin Configuration**
   Create a new file `admin/config.yml`:
   ```yaml
   backend:
     name: git-gateway
     branch: main

   local_backend: true

   media_folder: "images/uploads"
   public_folder: "/images/uploads"

   collections:
     - name: "pages"
       label: "Pages"
       files:
         - file: "index.html"
           label: "Home Page"
           name: "home"
           fields:
             - {label: "Layout", name: "layout", widget: "hidden", default: "home"}
             - {label: "Title", name: "title", widget: "string"}
             - {label: "Hero Title", name: "hero_title", widget: "string"}
             - {label: "Hero Subtitle", name: "hero_subtitle", widget: "string"}
             - {label: "Hero Image", name: "hero_image", widget: "image"}
             - {label: "Gallery Items", name: "gallery", widget: "list", fields:
                 - {label: "Title", name: "title", widget: "string"}
                 - {label: "Image", name: "image", widget: "image"}
                 - {label: "Description", name: "description", widget: "text"}
               }
   ```

2. **Add Admin Page**
   Create `admin/index.html`:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
     <meta charset="utf-8" />
     <meta name="viewport" content="width=device-width, initial-scale=1.0" />
     <title>Content Manager</title>
     <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
   </head>
   <body>
     <script src="https://unpkg.com/netlify-cms@^2.0.0/dist/netlify-cms.js"></script>
   </body>
   </html>
   ```

3. **Add Identity Widget**
   Add this script to your `index.html` before the closing `</body>` tag:
   ```html
   <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
   ```

### 3. Enable Netlify Identity

1. **Enable Identity Service**
   - Go to Site settings > Identity
   - Click "Enable Identity"
   - Configure registration preferences

2. **Enable Git Gateway**
   - Go to Site settings > Identity > Services
   - Click "Enable Git Gateway"

3. **Configure External Providers (Optional)**
   - Go to Site settings > Identity > External providers
   - Add Google, GitHub, or other providers

### 4. Set Up Forms

1. **Enable Form Detection**
   - Netlify automatically detects forms
   - No additional configuration needed for basic forms

2. **Form Handling**
   ```html
   <!-- Your existing form is already configured -->
   <form name="contact" method="POST" data-netlify="true">
     <!-- form fields -->
   </form>
   ```

### 5. Custom Domain Setup

1. **Add Custom Domain**
   - Go to Site settings > Domain management
   - Click "Add custom domain"
   - Follow the DNS configuration instructions

2. **SSL/TLS Configuration**
   - Netlify provides free SSL certificates
   - Automatic HTTPS is enabled by default

### 6. Environment Variables

1. **Add Environment Variables**
   - Go to Site settings > Build & deploy > Environment
   - Add any required environment variables

2. **Example Variables**
   ```env
   SITE_URL=https://your-site.com
   CONTACT_EMAIL=your@email.com
   ```

## Post-Deployment

### 1. Testing

- Test all forms
- Verify CMS functionality
- Check responsive design
- Test custom domain
- Verify SSL certificate

### 2. Monitoring

- Set up form notifications
- Configure deploy notifications
- Monitor site analytics

### 3. Maintenance

- Regular content updates
- Form submission management
- CMS user management
- Performance monitoring

## Troubleshooting

### Common Issues

1. **Form Submissions Not Working**
   - Verify `data-netlify="true"` attribute
   - Check form name attribute
   - Ensure proper field names

2. **CMS Access Issues**
   - Verify Identity service is enabled
   - Check user permissions
   - Clear browser cache

3. **Deployment Failures**
   - Check build settings
   - Verify repository access
   - Review build logs

## Resources

- [Netlify Documentation](https://docs.netlify.com/)
- [Netlify CMS Documentation](https://www.netlifycms.org/docs/)
- [Netlify Forms Documentation](https://docs.netlify.com/forms/setup/)
- [Netlify Identity Documentation](https://docs.netlify.com/visitor-access/identity/)

## Support

- [Netlify Support](https://www.netlify.com/support/)
- [Netlify Community](https://community.netlify.com/)
- [Netlify Status](https://www.netlifystatus.com/) 