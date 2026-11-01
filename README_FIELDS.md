# JCB! Fields

### What Are Fields?
Fields are the **foundation** of every Joomla Component Builder (JCB) project.

They define how data is **stored**, **validated**, **rendered**, and **interacted with** in your Joomla extensions.

Fields let you control everything from the **underlying database schema** to the **user interface**, all within a single configuration.

Each Field:
- Defines **database structure** (type, size, default, null, unique keys, indexes)
- Binds to a **fieldtype**, determining HTML rendering and behavior
- Supports per-field **custom PHP** for model saving and retrieval
- Allows styling and scripting (HTML attributes, JS, CSS)
- Automatically generates Joomla-compliant XML field definitions

### Where Are Fields Used in JCB?
Fields are universal integrated — they are used in, highly structured areas:

- ✅ **Admin Views** (the native Joomla back-end editing views)
- ✅ **Modules** (frontend display configurations)
- ✅ **Plugins** (event-driven integrations)
- ✅ **Component Configurations** (global parameter settings)

### What Can a Field Do?
A Field in JCB can define:

- **Database Type & Schema**: `int`, `varchar`, `json`, custom, nullable, defaults, indexes
- **Permissions**: who can view/edit the field (ACL)
- **Rendering Options**: HTML classes, labels, JS behaviors
- **Model Integration**: how the value is saved or retrieved
- **Dynamic Logic**: PHP hooks for `onGet`, `onSave`, `onPrepareForm`, etc.
- **Fieldtypes**: link to rich behaviors like Model Selects, Subforms, Toggle Switches, Encrypted Fields, etc.

This centralization makes field management efficient and highly reusable.

### Reuse and Sharing
Fields are standalone entities:

- Define once, **reuse across multiple Admin Views**, Modules, or Plugins
- Fields can also be exported and shared via repositories
- JCB will automatically adjust them to fit into each consuming context

This means less duplication, and greater consistency across your entire component structure.

### Versioning and Customization
To update a field:

- Click **"reset"** in the JCB UI to sync with this repository
- Or **fork** this repository, customize the field, and point JCB to your fork

This preserves version control while allowing your own field improvements to live independently.

>Fields define both structure and behavior — they are where your data comes alive.

---
### Index of Fields


 - **Alto label** | [Details](src/field/d13d6928-3171-474e-8b98-060bc8ed20ab) | [Settings](src/field/d13d6928-3171-474e-8b98-060bc8ed20ab/item.json)
 - **Alto part** | [Details](src/field/bfeeedd3-9a3b-45e4-bfc1-e5e1c551fbaf) | [Settings](src/field/bfeeedd3-9a3b-45e4-bfc1-e5e1c551fbaf/item.json)
 - **Alto part YouTube** | [Details](src/field/76e3a927-a7e7-4031-adf4-e174efc33d20) | [Settings](src/field/76e3a927-a7e7-4031-adf4-e174efc33d20/item.json)
 - **Bass label** | [Details](src/field/52099a53-25a7-4ffd-bb3c-0eed6729d4e2) | [Settings](src/field/52099a53-25a7-4ffd-bb3c-0eed6729d4e2/item.json)
 - **Bass part** | [Details](src/field/14f0aad5-5c25-4b92-bc16-3fa0265dbe6f) | [Settings](src/field/14f0aad5-5c25-4b92-bc16-3fa0265dbe6f/item.json)
 - **Bass part Youtube** | [Details](src/field/d4688359-1193-4cc9-a4d9-ff5b23a91830) | [Settings](src/field/d4688359-1193-4cc9-a4d9-ff5b23a91830/item.json)
 - **Composer** | [Details](src/field/a5195930-14b9-4e13-81a8-e3fbf89ec302) | [Settings](src/field/a5195930-14b9-4e13-81a8-e3fbf89ec302/item.json)
 - **Concert location** | [Details](src/field/046cbe0a-493d-40ed-90b7-8c904a3396c9) | [Settings](src/field/046cbe0a-493d-40ed-90b7-8c904a3396c9/item.json)
 - **Concert name** | [Details](src/field/fae77b76-4350-4e98-9ab9-6f85f64bebdb) | [Settings](src/field/fae77b76-4350-4e98-9ab9-6f85f64bebdb/item.json)
 - **Musical genre** | [Details](src/field/4743eb8a-e4a4-4ff1-8d26-b5c2d1721e3e) | [Settings](src/field/4743eb8a-e4a4-4ff1-8d26-b5c2d1721e3e/item.json)
 - **Part_type** | [Details](src/field/6d03c3a1-ce6e-4ef1-867d-47a06c01e9d9) | [Settings](src/field/6d03c3a1-ce6e-4ef1-867d-47a06c01e9d9/item.json)
 - **Program pieces** | [Details](src/field/a5153072-1cd3-454d-a41b-06c6f349f725) | [Settings](src/field/a5153072-1cd3-454d-a41b-06c6f349f725/item.json)
 - **Public performance** | [Details](src/field/f1d51293-83af-40f3-b52a-7d5615664dc6) | [Settings](src/field/f1d51293-83af-40f3-b52a-7d5615664dc6/item.json)
 - **Score** | [Details](src/field/52b08926-9a63-44b4-8a19-580996822e76) | [Settings](src/field/52b08926-9a63-44b4-8a19-580996822e76/item.json)
 - **Soprano label** | [Details](src/field/07f81786-8c38-4b30-b8cb-7cf819608092) | [Settings](src/field/07f81786-8c38-4b30-b8cb-7cf819608092/item.json)
 - **Soprano part** | [Details](src/field/24def5ef-d5be-4c86-9c67-2439ef3ffe4c) | [Settings](src/field/24def5ef-d5be-4c86-9c67-2439ef3ffe4c/item.json)
 - **Soprano part YouTube** | [Details](src/field/9cb0fa42-2119-4014-aaca-8cbef2ad9473) | [Settings](src/field/9cb0fa42-2119-4014-aaca-8cbef2ad9473/item.json)
 - **Tenor label** | [Details](src/field/b7393f14-c071-453a-b96e-3f246d95b51c) | [Settings](src/field/b7393f14-c071-453a-b96e-3f246d95b51c/item.json)
 - **Tenor part** | [Details](src/field/d4d78461-cb50-4d60-924b-c37e5737a2c7) | [Settings](src/field/d4d78461-cb50-4d60-924b-c37e5737a2c7/item.json)
 - **Tenor part YouTube** | [Details](src/field/e41f4b77-325a-4035-a25f-ef25fe04894d) | [Settings](src/field/e41f4b77-325a-4035-a25f-ef25fe04894d/item.json)
 - **Title** | [Details](src/field/2a2f971b-76ec-4d78-838c-45548ee7632c) | [Settings](src/field/2a2f971b-76ec-4d78-838c-45548ee7632c/item.json)

### All used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")