# Rails Tabler Starter

**Skip the first 40 hours of setup. Build your product instead.**

`rails-tabler-starter` is a production-ready boilerplate for developers who want a high-quality UI without the frontend fatigue. It uses a modern **Rails 8** stack (Solid Queue, Solid Cache) and **Tabler (Bootstrap 5)** for a clean, professional dashboard out of the box.

<div align="center">
<img src="./app/assets/images/saas-example.gif" alt="Rails Tabler Preview" width="800px" style="border-radius: 8px;" />

**[Explore the Demo](https://rails-tabler.tarunvelli.site)**

</div>

## The Goal

1. **Pure Rails:** No proprietary DSLs or "magic". If you know Rails, you know this starter.
2. **Readability > Cleverness:** Standard patterns over complex abstractions.
3. **Batteries Included:** Authentication, Multi-tenancy, and UI components are pre-configured.

## Why this starter?

* **Zero-Config UI:** Tabler components integrated with Hotwire. Dark mode, responsive layouts, and dashboards work immediately.
* **Built-in Multi-Tenancy:** "Spaces" support included. Switch between single-user and B2B SaaS modes via config.
* **Simplified Infrastructure:** Built for Rails 8. Uses `solid_queue` and `solid_cache`—no Redis required for small-to-medium deployments.
* **Secure:** Pre-loaded with Pundit (AuthZ), Devise (AuthN), and Brakeman security auditing.

## The Stack

* **Core:** Rails 8.0+, Ruby 3.3+, SQLite (Production-optimized).
* **Auth:** Devise + OmniAuth (Google/GitHub).
* **UI:** Tabler (Bootstrap 5) + Hotwire/Turbo.
* **Background Jobs:** Solid Queue / Active Job.
* **Deployment:** Pre-configured for **Kamal**, Fly.io, or Heroku.

## Space Management & Architecture

The app uses a **Space-based** architecture for teams or organizations.

* **Standard Roles:** Admin and Member roles per space.
* **Permissions:** Built-in support for custom roles and granular access controls via Pundit.

## Theming Engine

Overhaul the UI via the `AppSettings` singleton. No CSS hunting required. All settings are database-backed and can be modified at runtime.

### Visual Configuration

| Category | Setting | Options |
| --- | --- | --- |
| **Layout** | `interface_layout` | `VERTICAL`, `VERTICAL-TRANSPARENT`, `OVERLAP`, `CONDENSED`, `HORIZONTAL` |
| **Mode** | `color_mode` | `LIGHT`, `DARK` |
| **Primary Color** | `color_scheme` | `BLUE`, `AZURE`, `INDIGO`, `PURPLE`, `PINK`, `RED`, `ORANGE`, `YELLOW`, `LIME`, `GREEN`, `TEAL`, `CYAN` |
| **Theme** | `theme_base` | `NEUTRAL`, `SLATE`, `ZINC`, `GRAY`, `STONE`, `PINK` |
| **Typography** | `font_family` | `SANS-SERIF`, `SERIF`, `MONOSPACE`, `COMIC` |
| **Shapes** | `corner_radius` | `0` to `2` |

### Logic Configuration

| Setting | Default | Description |
| --- | --- | --- |
| `multi_tenant_mode` | `true` | Toggle SaaS-style "Spaces" vs. a single-user app. |
| `show_landing_page` | `true` | Toggle the public marketing page. |

---

## ⚡ Quick Start

```bash
# Clone and setup
git clone https://github.com/tarunvelli/rails-tabler-starter.git my_app
cd my_app
bin/setup

# Start server
bin/dev

```

## Rename Your App

This template includes a rename helper so new projects can be rebranded in one step.

```bash
# Preview changes only
bin/rename_app "My New App" --dry-run

# Apply changes
bin/rename_app "My New App" \
  --slug my-new-app \
  --module MyNewApp \
  --host app.mynewapp.com \
  --from-email noreply@mynewapp.com \
  --update-test-host
```

What it updates:
- Rails module namespace (`config/application.rb`)
- App title fallbacks in layout files
- PWA manifest name/description
- Deployment identifiers in `config/deploy.yml` and Docker image comments
- Template/documentation name references
- `.env.sample` URL values when `--host` or `--app-url` is provided
- Devise and application mailer sender email (defaults to `noreply@<slug>.test`, overridable with `--from-email`)
- Test mailer host only when `--update-test-host` is provided

Recommended flow after cloning:
1. Run `bin/rename_app "Your App Name" --dry-run`
2. Run the command again without `--dry-run`
3. Run `bin/setup`

**Promote User to Admin:**

```ruby
User.first.update(admin: true)

```

## Contributing

1. Fork it.
2. Create your feature branch (`git checkout -b feature/name`).
3. Commit your changes (`git commit -m 'Add feature'`).
4. Push to the branch (`git push origin feature/name`).
5. Open a Pull Request.
