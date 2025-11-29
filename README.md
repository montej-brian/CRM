# SuiteCRM 8.9.1 - Minimum Viable Product (MVP)

## Executive Summary

SuiteCRM is an enterprise-ready, open-source Customer Relationship Management (CRM) system built on a modern technology stack. This MVP document outlines the essential features, architecture, and implementation roadmap for deploying a functional CRM system.

**Version**: 8.9.1  
**License**: AGPLv3  
**Technology Stack**: Symfony 6.4 (Backend) + Angular 18 (Frontend)

---

## 1. System Architecture

### 1.1 Technology Stack

#### Backend
- **Framework**: Symfony 6.4
- **Language**: PHP 8.1+
- **Database**: MySQL/MariaDB or PostgreSQL
- **API**: API Platform 3.4 (REST/GraphQL)
- **Authentication**: OAuth2, SAML, LDAP, Native
- **ORM**: Doctrine 2.17

#### Frontend
- **Framework**: Angular 18.2
- **UI Components**: 
  - ng-bootstrap 17.0
  - PrimeNG 17.18
- **State Management**: Apollo Client (GraphQL)
- **Charts**: ngx-charts 20.5
- **Rich Text**: TinyMCE 7.4

#### Infrastructure
- **Web Server**: Apache/Nginx
- **PHP Extensions Required**: 
  - ctype, curl, gd, iconv, json, openssl, pdo, zip
- **Optional**: imap (for email module)

### 1.2 Architecture Pattern

```mermaid
graph TB
    A[Angular Frontend] -->|GraphQL/REST| B[Symfony Backend]
    B -->|Doctrine ORM| C[Database]
    B -->|Authentication| D[Auth Providers]
    D -->|Native/OAuth2/SAML/LDAP| E[User Store]
    B -->|Email| F[SMTP/IMAP]
    B -->|Storage| G[File System/S3/Azure]
    A -->|Assets| H[Public Directory]
    B -->|Legacy API| I[Legacy PHP Modules]
```

---

## 2. Core Modules (MVP Features)

### 2.1 Customer Management

#### **Accounts Module**
> [!IMPORTANT]
> Core module for managing company/organization records

**Features**:
- Create, read, update, delete (CRUD) account records
- Account hierarchy (parent-child relationships)
- Custom fields support
- Activity tracking (calls, meetings, tasks)
- Document attachments
- Relationship management with contacts, opportunities, cases

**Key Fields**:
- Name, Type, Industry, Annual Revenue
- Billing/Shipping Address
- Phone, Email, Website
- Assigned User, Team

#### **Contacts Module**
**Features**:
- Individual contact management
- Link contacts to accounts
- Communication history
- Email integration
- Contact import/export
- Duplicate detection

**Key Fields**:
- First/Last Name, Title, Department
- Email, Phone, Mobile
- Mailing Address
- Reports To (hierarchy)
- Account relationship

#### **Leads Module**
**Features**:
- Lead capture and qualification
- Lead scoring
- Lead conversion to Account/Contact/Opportunity
- Lead assignment rules
- Campaign tracking
- Web-to-lead forms

**Key Fields**:
- Name, Company, Title
- Email, Phone
- Lead Source, Status
- Assigned User
- Conversion tracking

---

### 2.2 Sales Management

#### **Opportunities Module**
**Features**:
- Sales pipeline management
- Sales stages tracking
- Revenue forecasting
- Probability-based forecasting
- Product/service line items
- Quote generation
- Relationship with accounts and contacts

**Key Fields**:
- Name, Amount, Expected Close Date
- Sales Stage, Probability
- Lead Source, Campaign
- Account/Contact relationships
- Assigned User

**Sales Stages** (Default):
1. Prospecting
2. Qualification
3. Needs Analysis
4. Value Proposition
5. Negotiation/Review
6. Closed Won
7. Closed Lost

#### **Quotes Module**
**Features**:
- Professional quote generation
- Product catalog integration
- Pricing calculations (discounts, tax)
- PDF generation
- Quote versioning
- Email delivery
- E-signature support

#### **Invoices Module**
**Features**:
- Invoice creation from quotes
- Payment tracking
- Invoice templates
- PDF generation
- Email delivery

---

### 2.3 Customer Support

#### **Cases Module**
**Features**:
- Support ticket management
- Case assignment and routing
- Priority and status tracking
- SLA management
- Knowledge base integration
- Email-to-case
- Case escalation

**Key Fields**:
- Case Number, Subject, Description
- Status, Priority, Type
- Account/Contact relationship
- Assigned User
- Resolution notes

**Case Statuses**:
- New, Assigned, Pending Input, Closed, Rejected

#### **Notes Module**
**Features**:
- Attach notes to any record
- File attachments
- Note history
- Search functionality

---

### 2.4 Marketing

#### **Campaigns Module**
**Features**:
- Marketing campaign management
- Campaign ROI tracking
- Target list management
- Email marketing integration
- Campaign analytics
- Lead source tracking

**Key Fields**:
- Name, Type, Status
- Budget, Expected Revenue
- Start/End Date
- Target List
- Campaign metrics (impressions, clicks, conversions)

#### **Prospects Module**
**Features**:
- Prospect list management
- Email opt-in/opt-out
- Prospect import
- Campaign targeting

#### **Email Marketing Module**
**Features**:
- Email template designer
- Mass email campaigns
- Email tracking (opens, clicks)
- Unsubscribe management
- A/B testing

---

### 2.5 Activity Management

#### **Tasks Module**
**Features**:
- Task creation and assignment
- Due date tracking
- Task priorities
- Task status workflow
- Recurring tasks
- Task reminders

#### **Calls Module**
**Features**:
- Call logging
- Call scheduling
- Call outcomes tracking
- Integration with contacts/accounts

#### **Meetings Module**
**Features**:
- Meeting scheduling
- Attendee management
- Calendar integration
- Meeting notes
- Reminders

#### **Calendar Module**
**Features**:
- Unified calendar view
- Day/Week/Month/Year views
- Shared calendars
- Google Calendar integration
- Activity color coding

---

### 2.6 Administration

#### **Users Module**
**Features**:
- User account management
- Role-based access control (RBAC)
- User preferences
- Password policies
- Two-factor authentication (2FA)
- User activity logging

#### **ACL (Access Control) Module**
**Features**:
- Role management
- Permission sets
- Field-level security
- Record-level security
- Team-based access

#### **Security Groups Module**
**Features**:
- Group-based access control
- Hierarchical security
- Record sharing rules

---

## 3. Essential Features

### 3.1 Authentication & Security

> [!CAUTION]
> Security configuration is critical for production deployment

**Supported Authentication Methods**:
- ✅ Native (username/password)
- ✅ OAuth2
- ✅ SAML 2.0
- ✅ LDAP/Active Directory
- ✅ Two-Factor Authentication (TOTP, Google Authenticator)

**Security Features**:
- Login throttling (configurable max attempts)
- Password complexity requirements
- Session management
- CSRF protection
- XSS protection (via voku/anti-xss)
- SQL injection prevention (Doctrine ORM)
- API rate limiting

### 3.2 Email Integration

**Features**:
- IMAP/SMTP integration
- Email client within CRM
- Email templates
- Email tracking
- Email-to-lead
- Email-to-case
- Group email accounts
- Email archiving

**Supported Providers**:
- Gmail (OAuth2)
- Microsoft 365
- Generic IMAP/SMTP

### 3.3 Reporting & Analytics

**Features**:
- Report builder
- Scheduled reports
- Report export (PDF, CSV, Excel)
- Dashboard widgets
- Custom charts
- Saved filters
- Report sharing

**Chart Types**:
- Bar, Line, Pie, Funnel
- Horizontal/Vertical grouping
- Time-based analytics

### 3.4 Workflow Automation

**Features**:
- Workflow designer
- Trigger-based actions
- Scheduled workflows
- Email notifications
- Field updates
- Record creation
- Conditional logic

### 3.5 Document Management

**Features**:
- Document upload/download
- Document versioning
- Document templates
- PDF generation
- Document categories
- Document search
- Storage options (local, S3, Azure Blob)

### 3.6 Import/Export

**Features**:
- CSV import
- Field mapping
- Duplicate detection
- Import history
- Export to CSV/Excel
- Mass update

### 3.7 Mobile Responsiveness

**Features**:
- Responsive design (Bootstrap 5)
- Touch-friendly interface
- Mobile-optimized views
- Progressive Web App (PWA) capabilities

### 3.8 Customization

**Features**:
- Custom fields (text, number, date, dropdown, etc.)
- Custom modules
- Studio (visual customization tool)
- Module builder
- Custom layouts
- Custom relationships
- Theme customization

---

## 4. Database Schema (Core Tables)

### Key Entity Relationships

```mermaid
erDiagram
    ACCOUNTS ||--o{ CONTACTS : has
    ACCOUNTS ||--o{ OPPORTUNITIES : has
    ACCOUNTS ||--o{ CASES : has
    CONTACTS ||--o{ OPPORTUNITIES : influences
    CONTACTS ||--o{ CASES : reports
    LEADS ||--o| ACCOUNTS : converts_to
    LEADS ||--o| CONTACTS : converts_to
    LEADS ||--o| OPPORTUNITIES : converts_to
    OPPORTUNITIES ||--o{ QUOTES : generates
    QUOTES ||--o{ INVOICES : generates
    CAMPAIGNS ||--o{ LEADS : generates
    USERS ||--o{ ACCOUNTS : owns
    USERS ||--o{ OPPORTUNITIES : owns
    USERS ||--o{ CASES : assigned_to
```

### Core Tables

| Table | Purpose | Key Fields |
|-------|---------|------------|
| `accounts` | Company/Organization records | name, industry, type, annual_revenue |
| `contacts` | Individual contacts | first_name, last_name, email, account_id |
| `leads` | Potential customers | name, email, status, lead_source |
| `opportunities` | Sales deals | name, amount, sales_stage, probability |
| `cases` | Support tickets | case_number, status, priority, type |
| `tasks` | To-do items | name, status, priority, due_date |
| `calls` | Call logs | name, date_start, duration, status |
| `meetings` | Meeting records | name, date_start, duration, location |
| `emails` | Email records | name, from_addr, to_addrs, status |
| `campaigns` | Marketing campaigns | name, budget, expected_revenue, status |
| `users` | System users | user_name, email, status, is_admin |
| `acl_roles` | User roles | name, description |
| `notes` | Notes/attachments | name, description, parent_type, parent_id |

---

## 5. API Endpoints (MVP)

### 5.1 GraphQL API

**Base URL**: `/api/graphql`

**Core Queries**:
```graphql
# Get account list
query {
  getAccountList(filter: {...}, sort: {...}) {
    records {
      id
      attributes {
        name
        industry
        annual_revenue
      }
    }
  }
}

# Get single record
query {
  getAccount(id: "123") {
    id
    attributes {
      name
      email
    }
  }
}
```

**Core Mutations**:
```graphql
# Create record
mutation {
  createAccount(input: {
    name: "Acme Corp"
    industry: "Technology"
  }) {
    record {
      id
      attributes {
        name
      }
    }
  }
}

# Update record
mutation {
  updateAccount(id: "123", input: {...}) {
    record {
      id
    }
  }
}

# Delete record
mutation {
  deleteAccount(id: "123") {
    success
  }
}
```

### 5.2 REST API

**Base URL**: `/api`

**Endpoints**:
- `GET /api/module/{module}/record/{id}` - Get record
- `POST /api/module/{module}/record` - Create record
- `PUT /api/module/{module}/record/{id}` - Update record
- `DELETE /api/module/{module}/record/{id}` - Delete record
- `GET /api/module/{module}/records` - List records
- `POST /api/login` - Authentication
- `POST /api/logout` - Logout

---

## 6. Installation & Setup

### 6.1 System Requirements

> [!IMPORTANT]
> Ensure all requirements are met before installation

**Minimum Requirements**:
- PHP 8.1 or higher
- MySQL 5.7+ / MariaDB 10.3+ / PostgreSQL 12+
- Apache 2.4+ or Nginx 1.18+
- Node.js 10+ (for frontend build)
- Composer 2.0+
- Yarn 4.10+

**PHP Extensions**:
- ctype, curl, gd, iconv, json, openssl, pdo, zip
- Optional: imap (for email module)

**Server Configuration**:
- Memory: 512MB minimum, 1GB+ recommended
- Disk Space: 500MB minimum
- Upload Max Filesize: 20MB+
- Post Max Size: 20MB+
- Max Execution Time: 300 seconds

### 6.2 Installation Steps

#### Step 1: Download & Extract
```bash
# Extract SuiteCRM
cd /var/www/html
unzip SuiteCRM-8.9.1.zip
cd SuiteCRM-8.9.1
```

#### Step 2: Set Permissions
```bash
# Set ownership
chown -R www-data:www-data .

# Set directory permissions
find . -type d -exec chmod 755 {} \;

# Set file permissions
find . -type f -exec chmod 644 {} \;

# Writable directories
chmod -R 775 cache/ logs/ public/legacy/cache/ public/legacy/custom/ public/legacy/upload/
```

#### Step 3: Configure Database
```bash
# Copy environment file
cp .env .env.local

# Edit .env.local
nano .env.local
```

**Database Configuration**:
```bash
DATABASE_URL="mysql://username:password@localhost:3306/suitecrm?serverVersion=8.0&charset=utf8mb4"
```

#### Step 4: Install Dependencies
```bash
# Install PHP dependencies
composer install --no-dev --optimize-autoloader

# Install Node dependencies
yarn install

# Build frontend
yarn build
```

#### Step 5: Run Installation
```bash
# Web-based installer
# Navigate to: http://yourdomain.com/install.php

# OR CLI installation
php bin/console suitecrm:app:install \
  --db_username=username \
  --db_password=password \
  --db_name=suitecrm \
  --db_host=localhost \
  --site_username=admin \
  --site_password=admin123 \
  --site_url=http://yourdomain.com
```

#### Step 6: Post-Installation
```bash
# Clear cache
php bin/console cache:clear

# Set up cron jobs
crontab -e

# Add this line:
* * * * * cd /var/www/html/SuiteCRM-8.9.1 && php bin/console suitecrm:app:scheduler >> /dev/null 2>&1
```

### 6.3 Web Server Configuration

#### Apache (.htaccess included)
```apache
<VirtualHost *:80>
    ServerName crm.example.com
    DocumentRoot /var/www/html/SuiteCRM-8.9.1/public
    
    <Directory /var/www/html/SuiteCRM-8.9.1/public>
        AllowOverride All
        Require all granted
    </Directory>
    
    ErrorLog ${APACHE_LOG_DIR}/suitecrm_error.log
    CustomLog ${APACHE_LOG_DIR}/suitecrm_access.log combined
</VirtualHost>
```

#### Nginx
```nginx
server {
    listen 80;
    server_name crm.example.com;
    root /var/www/html/SuiteCRM-8.9.1/public;
    
    index index.php;
    
    location / {
        try_files $uri /index.php$is_args$args;
    }
    
    location ~ ^/index\.php(/|$) {
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        fastcgi_param DOCUMENT_ROOT $realpath_root;
        internal;
    }
    
    location ~ \.php$ {
        return 404;
    }
}
```

---

## 7. Configuration

### 7.1 Environment Variables (.env.local)

**Essential Configuration**:
```bash
# Application Environment
APP_ENV=prod

# Database
DATABASE_URL="mysql://user:pass@localhost:3306/suitecrm?serverVersion=8.0&charset=utf8mb4"

# Authentication
AUTH_TYPE=native

# CORS (for API access)
CORS_ALLOW_ORIGIN='^https?://(localhost|yourdomain\.com)(:[0-9]+)?$'

# Logging
MAIN_LOG_LEVEL=warning
DEPRECATION_LOG_LEVEL=error
SECURITY_LOG_LEVEL=error

# Login Security
LOGIN_THROTTLING_MAX_ATTEMPTS=5
LOGIN_THROTTLING_IP_LOGIN_MAX_ATTEMPTS=50
LOGIN_THROTTLING_INTERVAL="30 minutes"

# Lock mechanism
LOCK_DSN=flock
```

### 7.2 Email Configuration

```bash
# SMTP Configuration
MAILER_DSN=smtp://user:pass@smtp.example.com:587?encryption=tls
```

### 7.3 File Storage

**Local Storage** (Default):
- Files stored in `public/legacy/upload/`

**AWS S3**:
```bash
AWS_S3_INSTANCES='{
   "main": {
       "region": "us-east-1",
       "access_key": "YOUR_KEY",
       "access_secret": "YOUR_SECRET"
   }
}'

MEDIA_FLY_SYSTEM_STORAGES='{
   "private.documents.storage": {
       "adapter": "aws",
       "options": {
           "client": "aws.s3.client.main",
           "bucket": "my-suitecrm-bucket"
       }
   }
}'
```

---

## 8. User Roles & Permissions (MVP)

### 8.1 Default Roles

| Role | Description | Access Level |
|------|-------------|--------------|
| **Administrator** | Full system access | All modules, all records, system config |
| **Sales Manager** | Sales team management | Accounts, Contacts, Leads, Opportunities, Reports |
| **Sales Rep** | Individual sales user | Own records + team records |
| **Support Manager** | Support team management | Cases, Accounts, Contacts, Knowledge Base |
| **Support Agent** | Individual support user | Assigned cases + team cases |
| **Marketing User** | Marketing campaigns | Campaigns, Leads, Prospects, Email Marketing |
| **Standard User** | Basic CRM access | Limited module access, own records only |

### 8.2 Permission Levels

- **All** - Access to all records
- **Owner** - Access to own records only
- **Group** - Access to group/team records
- **None** - No access

### 8.3 Field-Level Security

- Hide sensitive fields from specific roles
- Read-only fields
- Required fields by role

---

## 9. Customization Guide

### 9.1 Custom Fields

**Via Studio**:
1. Admin → Studio → Select Module
2. Fields → Add Field
3. Configure field type, label, options
4. Add to layouts

**Field Types**:
- Text, TextArea, HTML
- Integer, Decimal, Currency
- Date, DateTime
- Dropdown, MultiSelect
- Checkbox, Radio
- Relate (relationship)
- Email, Phone, URL
- File Upload

### 9.2 Custom Modules

**Via Module Builder**:
1. Admin → Module Builder
2. New Package
3. New Module
4. Define fields and relationships
5. Deploy

### 9.3 Workflows

**Workflow Actions**:
- Send Email
- Create Record
- Modify Record
- Run Custom Logic

**Triggers**:
- On Save (new/modified)
- On Delete
- Scheduled (time-based)

---

## 10. MVP Implementation Roadmap

### Phase 1: Foundation (Weeks 1-2)
- [x] Install SuiteCRM 8.9.1
- [ ] Configure database
- [ ] Set up web server
- [ ] Configure email
- [ ] Create admin user
- [ ] Configure authentication
- [ ] Set up SSL/HTTPS
- [ ] Configure backups

### Phase 2: Core Modules Setup (Weeks 3-4)
- [ ] Configure Accounts module
- [ ] Configure Contacts module
- [ ] Configure Leads module
- [ ] Configure Opportunities module
- [ ] Set up sales pipeline stages
- [ ] Configure Cases module
- [ ] Set up email integration
- [ ] Import initial data

### Phase 3: User Management (Week 5)
- [ ] Create user roles
- [ ] Set up permissions
- [ ] Create user accounts
- [ ] Configure teams
- [ ] Set up security groups
- [ ] Configure 2FA
- [ ] User training materials

### Phase 4: Customization (Weeks 6-7)
- [ ] Add custom fields
- [ ] Customize layouts
- [ ] Create email templates
- [ ] Set up workflows
- [ ] Configure reports
- [ ] Create dashboards
- [ ] Theme customization

### Phase 5: Integration (Week 8)
- [ ] Email client setup
- [ ] Calendar integration
- [ ] Google/Microsoft integration
- [ ] API configuration
- [ ] Third-party integrations
- [ ] Mobile testing

### Phase 6: Testing & Training (Weeks 9-10)
- [ ] User acceptance testing
- [ ] Performance testing
- [ ] Security audit
- [ ] Data migration testing
- [ ] User training sessions
- [ ] Documentation
- [ ] Go-live preparation

### Phase 7: Launch & Support (Week 11+)
- [ ] Production deployment
- [ ] Monitor system performance
- [ ] User support
- [ ] Bug fixes
- [ ] Feature requests
- [ ] Ongoing optimization

---

## 11. Best Practices

### 11.1 Data Management

> [!TIP]
> Regular data maintenance improves system performance

- **Regular Backups**: Daily database + file backups
- **Data Cleanup**: Archive old records quarterly
- **Duplicate Prevention**: Enable duplicate detection
- **Data Validation**: Use field validation rules
- **Import Validation**: Always test imports on staging

### 11.2 Performance Optimization

- **Database Indexing**: Ensure proper indexes on custom fields
- **Cache Configuration**: Use Redis/Memcached for production
- **Image Optimization**: Compress uploaded images
- **Query Optimization**: Monitor slow queries
- **CDN**: Use CDN for static assets

### 11.3 Security

> [!CAUTION]
> Security should be reviewed regularly

- **Regular Updates**: Apply security patches promptly
- **Strong Passwords**: Enforce password policies
- **2FA**: Enable for all admin users
- **API Security**: Use OAuth2 for API access
- **Audit Logs**: Enable and review regularly
- **File Upload Restrictions**: Limit file types
- **HTTPS Only**: Force SSL in production

### 11.4 User Adoption

- **Simplified UI**: Hide unused modules
- **Role-Based Dashboards**: Customize per role
- **Training**: Provide comprehensive training
- **Documentation**: Maintain user guides
- **Support**: Establish support channels
- **Feedback Loop**: Regular user feedback sessions

---

## 12. Monitoring & Maintenance

### 12.1 System Monitoring

**Key Metrics**:
- Server CPU/Memory usage
- Database query performance
- API response times
- User login activity
- Error logs
- Storage usage

**Tools**:
- Symfony Profiler (development)
- Application logs (`logs/prod/`)
- Database slow query log
- Web server access/error logs

### 12.2 Scheduled Maintenance

**Daily**:
- Automated backups
- Log rotation
- Scheduler jobs execution

**Weekly**:
- Database optimization
- Cache clearing
- Security log review

**Monthly**:
- Update check
- Performance review
- User access audit
- Data cleanup

**Quarterly**:
- Security audit
- Disaster recovery test
- User training refresher

---

## 13. Support & Resources

### 13.1 Official Resources

- **Website**: [https://suitecrm.com](https://suitecrm.com)
- **Documentation**: [https://docs.suitecrm.com/8.x/](https://docs.suitecrm.com/8.x/)
- **Forum**: [https://suitecrm.com/suitecrm/forum](https://suitecrm.com/suitecrm/forum)
- **GitHub**: [https://github.com/salesagility/SuiteCRM-Core](https://github.com/salesagility/SuiteCRM-Core)

### 13.2 Community

- **Gitter Chat**: [https://gitter.im/suitecrm/Lobby](https://gitter.im/suitecrm/Lobby)
- **Twitter**: [@suitecrm](https://twitter.com/suitecrm)

### 13.3 Getting Help

- **Forum**: Post questions on community forum
- **GitHub Issues**: Report bugs and feature requests
- **Professional Support**: Available from SalesAgility

---

## 14. Conclusion

This MVP provides a comprehensive foundation for deploying SuiteCRM 8.9.1 as a fully functional CRM system. The modular architecture allows for incremental implementation, starting with core customer management features and expanding to sales, support, and marketing capabilities.

### Key Success Factors

1. **Proper Planning**: Define business requirements before customization
2. **User Training**: Invest in comprehensive user training
3. **Data Quality**: Establish data entry standards
4. **Regular Maintenance**: Follow maintenance schedule
5. **Security First**: Implement security best practices from day one
6. **Iterative Improvement**: Continuously gather feedback and optimize

### Next Steps

1. Review this MVP with stakeholders
2. Customize the implementation roadmap based on priorities
3. Set up development/staging environment
4. Begin Phase 1 installation
5. Schedule user training sessions
6. Plan go-live date

---

**Document Version**: 1.0  
**Last Updated**: 2025-11-29  
**Prepared For**: SuiteCRM 8.9.1 Implementation
