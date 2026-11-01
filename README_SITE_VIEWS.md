# JCB! Site Views

### What Are Site Views?
**Site Views** are the public-facing view of your Joomla component — 
offering full control over how data is presented to users on the frontend of your website.

Built with the same powerful toolset as Custom Admin Views, Site Views let you design:
- Custom list views for data records
- Single-item detail pages
- Frontend editors, galleries, dashboards
- AJAX loaders, tabs, and filters
...anything your user interface demands.

Each Site View is composed using:
- One or more **Dynamic Gets** (for safe, powerful data access)
- Integrated **Templates** and **Layouts** (to organize the UI)
- Optional **Custom Code** blocks (to inject reusable frontend logic)
- Optional **JavaScript/CSS Libraries** (to enhance interactivity or styling)

You decide how data is loaded, styled, filtered, and displayed — 
JCB simply generates the Joomla-native view, model, and controller code automatically.

---
### How Are Site Views Built?
You start by creating a Site View and selecting a **Main Dynamic Get**,  
which defines what data will be loaded.

You can then attach:
- **Custom Templates** to control view logic
- **Layouts** for modular rendering
- **Custom Code placeholders** for reusable logic blocks
- **Libraries** for loading external or internal JS/CSS assets

Every part is modular, reusable, and version-controlled via JCB repositories.

And when your project evolves, JCB makes it simple to:
- Reset to default Site View definitions
- Extend or override templates/layouts
- Push updates to shared repositories
- Fork for long-term customization

---
### Version Control and Updates
Whenever you need to update Site Views in any JCB project:

- **Select** the relevant Site Views
- Click **"Reset"** to sync them with the latest maintained version
- Or **Fork** this repository and point JCB to your version for full control

This ensures consistent updates while preserving your customizations and logic.

> Site Views are where your component meets your users. Use JCB to control that interaction fully — with logic, layout, and style exactly how you define it.

---
### Index of Site Views


 - **App Piece single** | [Details](src/site_view/e46f60a7-ec6a-4cab-9f94-c6c65f206a27) | [Settings](src/site_view/e46f60a7-ec6a-4cab-9f94-c6c65f206a27/item.json) | Show the data of a single piece
 - **App Select piece** | [Details](src/site_view/cfeb89a2-1f80-457e-82c9-a3fe8ca80f20) | [Settings](src/site_view/cfeb89a2-1f80-457e-82c9-a3fe8ca80f20/item.json) | The form to identify the required piece in the list, the ID will be passed to the display page
 - **Default view** | [Details](src/site_view/715839f3-0de7-4b1f-a94e-aca0954d03b9) | [Settings](src/site_view/715839f3-0de7-4b1f-a94e-aca0954d03b9/item.json) | The default view
 - **Footpath single** | [Details](src/site_view/e8a6f606-582c-41d6-b0b0-147d1c75c7ca) | [Settings](src/site_view/e8a6f606-582c-41d6-b0b0-147d1c75c7ca/item.json) | Display of one path description, map and other info
 - **Footpaths edit list** | [Details](src/site_view/13989926-5894-4344-83dc-fba6eff3b3af) | [Settings](src/site_view/13989926-5894-4344-83dc-fba6eff3b3af/item.json) | List of footpaths for edit
 - **Footpaths list** | [Details](src/site_view/d8443ac1-247d-4f5a-813a-6c71400a4294) | [Settings](src/site_view/d8443ac1-247d-4f5a-813a-6c71400a4294/item.json) | List of Footpaths
 - **Location map** | [Details](src/site_view/7d637624-7dd1-4f4e-a7aa-cfc7d333ded0) | [Settings](src/site_view/7d637624-7dd1-4f4e-a7aa-cfc7d333ded0/item.json) | Map of locations
 - **Location single** | [Details](src/site_view/47acca5d-c194-47fe-8961-0c849fcadbe0) | [Settings](src/site_view/47acca5d-c194-47fe-8961-0c849fcadbe0/item.json) | Display of one location description, map and other info
 - **Locations blocks** | [Details](src/site_view/d6f6a358-be9d-49d0-931e-ac2cbe37ba38) | [Settings](src/site_view/d6f6a358-be9d-49d0-931e-ac2cbe37ba38/item.json) | Main view for Locations - blocks view
 - **Locations edit list** | [Details](src/site_view/f1681276-fff6-4dab-bc58-2b229d83316f) | [Settings](src/site_view/f1681276-fff6-4dab-bc58-2b229d83316f/item.json) | List of locations for edit
 - **Locations list** | [Details](src/site_view/379b089a-e018-4fa9-9c42-c792a414beff) | [Settings](src/site_view/379b089a-e018-4fa9-9c42-c792a414beff/item.json) | List of locations
 - **Locations table** | [Details](src/site_view/df889519-71e3-40be-b74a-5abdbff5c003) | [Settings](src/site_view/df889519-71e3-40be-b74a-5abdbff5c003/item.json) | Site locations - table view
 - **Occupancy map** | [Details](src/site_view/ba21a497-c1a5-40c2-a486-3d637bb1a9a5) | [Settings](src/site_view/ba21a497-c1a5-40c2-a486-3d637bb1a9a5/item.json) | Map of occupancy of locations
 - **Piece single** | [Details](src/site_view/1af8efa1-f4dd-4f10-ab34-4e4b1070c46d) | [Settings](src/site_view/1af8efa1-f4dd-4f10-ab34-4e4b1070c46d/item.json) | Show the data of a single piece
 - **Pieces list** | [Details](src/site_view/96f146c6-0957-4ad5-a353-8056728dd4fb) | [Settings](src/site_view/96f146c6-0957-4ad5-a353-8056728dd4fb/item.json) | List of Pieces
 - **Places map** | [Details](src/site_view/e6bc3a5f-909e-493c-ba8a-6a79b555b2f7) | [Settings](src/site_view/e6bc3a5f-909e-493c-ba8a-6a79b555b2f7/item.json) | Display of places map
 - **Select piece** | [Details](src/site_view/140407ee-4631-4cd3-a04d-7cdc26fc8061) | [Settings](src/site_view/140407ee-4631-4cd3-a04d-7cdc26fc8061/item.json) | The form to identify the required piece in the list, the ID will be passed to the display page

### All used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")