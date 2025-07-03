# Quiz Builder and Hosting Platform

A web-based platform where administrators create quizzes, and users attempt them with instant scoring.

Technologies used...

- PHP (Laravel Framework)
- MySQL
- HTML / CSS (Bootstrap + SASS)
- JavaScript (Vanilla + AJAX)
- GitHub (for version control and CI/CD)
- GitHub Actions (for automated testing and deployment)

# 🚀 Full Stack Best Practices

This guide outlines **best practices** for building the **Quiz Builder and Hosting Platform**, covering frontend, backend, database, deployment, and testing. The goal is **readability, maintainability, scalability, security, and CI/CD readiness**.

---

## 📁 Project Structure

Maintain a **clean, modular, and organized project structure**:

```

/app
/Http
/Controllers   # Resource controllers (QuizController, AdminController, AuthController, ResultController)
/Middleware    # Custom middleware (e.g. Admin authentication)
/Models          # Eloquent models (Quiz, Question, User, Result)
/Policies        # Authorization policies (if used)
/Services        # Business logic services (e.g. scoring logic)

/resources
/views
/layouts       # Blade layouts (app.blade.php)
/partials      # Reusable Blade partials (navbar, footer, alerts)
/auth          # Login and registration views
/admin         # Admin dashboard, quiz builder views
/user          # User dashboard, quiz attempt, results views
/sass            # SASS modules (\_variables.scss, \_quiz.scss, \_admin.scss, etc.)
/js
timer.js       # Countdown timer functionality
quiz.js        # AJAX quiz interactions
app.js         # General scripts initialization
/css
app.css        # Compiled CSS

/routes
web.php          # Web routes grouped by middleware

/database
/migrations      # DB schema migrations
/seeders         # Seeders for demo data
/factories       # Model factories for testing

/public
/assets          # Images, compiled JS, CSS

/tests
/Feature         # Feature tests (auth, quiz flows)
/Unit            # Unit tests (score calculation logic)

.github
/workflows       # GitHub Actions CI/CD pipelines

.env               # Environment configuration
composer.json      # PHP dependencies
package.json       # JS dependencies
webpack.mix.js     # Laravel Mix configuration

```

🔖 **Rules:**

- **Flat is better than deeply nested**; keep modules organized by feature.
- **No generic ‘helpers’ folder**; place utilities in Services or within feature modules.
- Keep **controllers thin**, **services focused**, **models clean**, and **views logic-free**.

---

## ⚛️ Frontend UI & Styling Best Practices

✅ **Component & Blade Partial Guidelines:**

1. Extract Blade partials for **reusable UI blocks** (quiz cards, alerts, navbar, footer).
2. Write **custom styles in SASS modules**, compile using Laravel Mix.
3. Use **Bootstrap utility classes** first before adding custom CSS for rapid development.
4. Follow **BEM naming conventions** in custom CSS for clarity and maintainability.

✅ **Accessibility Guidelines:**

- Use **semantic HTML tags** for structure (`<nav>`, `<main>`, `<section>`, `<button>`).
- Implement **ARIA labels and roles** for timers, dynamic quiz elements.
- Ensure **keyboard navigability** for forms, quiz options, and buttons.
- Maintain **sufficient color contrast** for readability.

---

## 🛠️ JavaScript & AJAX Best Practices

✅ **Key Guidelines:**

- Use **vanilla JS with clean DOM selectors** and event delegation.
- Organize JS by feature (timer.js, quiz.js) for modularity.
- Use **AJAX for dynamic quiz submission**; handle success and errors gracefully with user-friendly feedback.
- Always **protect AJAX POST requests with CSRF tokens**.

---

## 🔐 Backend (Laravel / PHP / MySQL) Best Practices

✅ **Controller & Service Layer:**

- Use **RESTful resource controllers**.
- Delegate business logic to **Services** to keep controllers thin.
- Validate incoming data using **Form Request classes**.

✅ **Database & Models:**

- Use **normalized relational schemas** with proper foreign keys.
- Define clear **Eloquent relationships** (Quiz hasMany Questions, User hasMany Results).
- Apply all schema changes via **Laravel migrations** only.

✅ **Authentication & Authorization:**

- Implement **role-based access control** using an `is_admin` field or roles table.
- Protect admin routes with **custom middleware**.
- Use **Laravel Breeze or Jetstream** for authentication scaffolding.

---

## 🧪 Testing Best Practices

✅ **PHPUnit Testing:**

- **Feature tests** for:
  - User registration/login flows
  - Quiz creation/edit/deletion (admin)
  - Quiz attempt and scoring (user)
- **Unit tests** for:
  - Score calculation logic
  - Utility service methods

✅ **Manual Testing Flow:**

- Verify:
  - User registration and login flows
  - Quiz builder (creation, editing, deletion)
  - Quiz attempt with timer and auto-submit
  - Score calculation accuracy
  - Dashboard views for user and admin

✅ **JavaScript Testing:**

- JS testing can be minimal initially. Expand with Jest or similar in future enhancements.

---

## 🚀 CI/CD Deployment Best Practices

✅ **GitHub Actions Setup:**

- Create `.github/workflows/ci.yml` for automated testing on push/pull request:
  - Run `composer install`
  - Run `npm install && npm run dev` (if required for builds)
  - Run `php artisan migrate --env=testing`
  - Run PHPUnit tests

- Create `.github/workflows/deploy.yml` for deployment on push to `main`:
  - SSH into production server
  - Pull latest code
  - Run `composer install --no-dev --optimize-autoloader`
  - Run `npm install && npm run prod`
  - Run `php artisan migrate --force`
  - Restart PHP-FPM / queue workers if used

✅ **General Deployment Guidelines:**

- Never commit `.env` files; manage secrets securely.
- Test on **staging environment** before production deploy.
- Use **`php artisan config:cache`** and **`route:cache`** for optimized performance.
- Keep **backups and rollback plans** ready before each deploy.

---

## 🔒 Security Best Practices

✅ **Key Guidelines:**

- Always use **Laravel’s built-in protections** against SQL injection, XSS, and CSRF.
- Hash passwords with **bcrypt (default)**.
- Validate all inputs **server-side**, regardless of frontend validations.
- Sanitize user-generated content displayed in views to prevent XSS.
- Use **HTTPS** in production for all user data transmission.

---

By following these **end-to-end best practices**, the **Quiz Builder and Hosting Platform** will remain **scalable, secure, maintainable, and CI/CD-ready**, ensuring reliable delivery and long-term project success.
