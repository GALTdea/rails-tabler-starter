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

## Template Usage & Updates

This repository is a **GitHub Template Repository**. Use it to start new Rails projects and still pull in future improvements from the boilerplate.

### 1. Create your project

- On GitHub, click **"Use this template"** (green button).
- Choose **"Create a new repository"** and pick a name for your project.
- Clone your new repo locally:
  ```bash
  git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git my_app
  cd my_app
  bin/setup
  ```

### 2. Link the boilerplate as upstream

To pull future updates from this template, add it as a remote:

```bash
git remote add upstream https://github.com/tarunvelli/rails-tabler-starter.git
```

*(If you use a different copy of this template, replace the URL with that repo.)*

### 3. Merging updates from the template

When the boilerplate changes and you want those updates in your project:

```bash
git fetch upstream
git merge upstream/main --allow-unrelated-histories
```

- Use `--allow-unrelated-histories` for the **first** merge (your project and the template have different commit histories). Later updates can usually be merged with:
  ```bash
  git fetch upstream
  git merge upstream/main
  ```
- Resolve any merge conflicts (e.g. in `app/views/common/_nav_items.html.erb` or config files), then commit.

### 4. After merging

- Run `bin/setup` if dependencies or env changed.
- Re-run your rename or customizations if they were overwritten (e.g. `bin/rename_app "Your App"`).

## The Stack

* **Core:** Rails 8.0+, Ruby 3.3+, SQLite (Production-optimized).
* **Auth:** Devise + OmniAuth (Google/GitHub).
* **UI:** Tabler (Bootstrap 5) + Hotwire/Turbo.
* **Background Jobs:** Solid Queue / Active Job.
* **Deployment:** Pre-configured for **Kamal**, Fly.io, or Heroku.

## Space Management & Architecture

The app uses a **Space-based** architecture for teams or organizations. A **Space** is the main tenant: it represents one team or organization, with its own members, roles, and subscription.

* **Standard Roles:** Admin and Member roles per space.
* **Permissions:** Built-in support for custom roles and granular access controls via Pundit.

### What the Space model is for

* **Multi-tenancy:** Each Space is an isolated tenant. When `multi_tenant_mode` is on, users pick a Space (or get assigned to one) and all data and navigation are scoped to that Space.
* **Teams/Organizations:** Spaces group users and assign roles (e.g. who can manage the space, invite users, or view billing). Use space-scoped paths in the UI (e.g. `space_xyz_path(@space)`).
* **Billing:** Subscriptions and plans are attached to a Space. The `Space#active_subscription` method drives feature limits and plan-based behavior (e.g. Free vs Pro).

### Examples

**Create a space and add a user with a role:**

```ruby
space = Space.create!(name: "Acme Corp", email: "billing@acme.com", status: :active)
admin_role = Role.find_by(type: "common", value: "admin") # or your space-specific role
UserRole.create!(user: current_user, space: space, role: admin_role)
```

**Scope resources to the current space (e.g. in a controller):**

```ruby
# Only list items for the current tenant
@items = @space.items
# Or use the space in policies
authorize @space, :manage?
```

**Check the space’s subscription for feature gating:**

```ruby
plan = @space.active_subscription.plan
if plan.name != "Free"
  # Allow premium feature
end
```

**Roles available in a space (global + space-specific):**

```ruby
@space.all_roles  # => roles that apply to this space (common roles + space_id = @space.id)
```

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

## Customizing the sidebar navigation

To **add or hide** sidebar links (including by role), edit **`app/views/common/_nav_items.html.erb`**.

- **Add a link:** Use the same pattern as existing items: `<%= nav_link your_path do %> ... <% end %>` inside the `<%= nav_bar do %> ... <% end %>` block. Nav items are shown when a space is present (`@space`); use space-scoped paths (e.g. `space_xyz_path(@space)`) for tenant-scoped resources.
- **Hide by role:** Wrap any item in a conditional, e.g. `<% if current_user.admin? %>` for global admins, or your Pundit policy (e.g. `<% if policy(@space).manage? %>`) for space-level visibility. Admin-only links (Setup, Rails Admin) already live in the profile dropdown; use the same approach in the sidebar for space roles.
- **Merge conflicts:** This file is part of the template. If you pull updates from the upstream template, changes to `_nav_items.html.erb` may conflict. Resolve manually or re-apply your custom links after merging.

## Contributing

1. Fork it.
2. Create your feature branch (`git checkout -b feature/name`).
3. Commit your changes (`git commit -m 'Add feature'`).
4. Push to the branch (`git push origin feature/name`).
5. Open a Pull Request.
