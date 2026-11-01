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


 - **Altitude** | [Details](src/field/bdee9804-cf65-46da-a49a-5397789c801e) | [Settings](src/field/bdee9804-cf65-46da-a49a-5397789c801e/item.json)
 - **Alto label** | [Details](src/field/d13d6928-3171-474e-8b98-060bc8ed20ab) | [Settings](src/field/d13d6928-3171-474e-8b98-060bc8ed20ab/item.json)
 - **Alto part** | [Details](src/field/bfeeedd3-9a3b-45e4-bfc1-e5e1c551fbaf) | [Settings](src/field/bfeeedd3-9a3b-45e4-bfc1-e5e1c551fbaf/item.json)
 - **Alto part YouTube** | [Details](src/field/76e3a927-a7e7-4031-adf4-e174efc33d20) | [Settings](src/field/76e3a927-a7e7-4031-adf4-e174efc33d20/item.json)
 - **Base** | [Details](src/field/cf7146a0-8c47-4fec-9490-34287ef14408) | [Settings](src/field/cf7146a0-8c47-4fec-9490-34287ef14408/item.json)
 - **Bass label** | [Details](src/field/52099a53-25a7-4ffd-bb3c-0eed6729d4e2) | [Settings](src/field/52099a53-25a7-4ffd-bb3c-0eed6729d4e2/item.json)
 - **Bass part** | [Details](src/field/14f0aad5-5c25-4b92-bc16-3fa0265dbe6f) | [Settings](src/field/14f0aad5-5c25-4b92-bc16-3fa0265dbe6f/item.json)
 - **Bass part Youtube** | [Details](src/field/d4688359-1193-4cc9-a4d9-ff5b23a91830) | [Settings](src/field/d4688359-1193-4cc9-a4d9-ff5b23a91830/item.json)
 - **Camp fire checkbox** | [Details](src/field/e984295c-77bf-437b-8361-4977646fae4c) | [Settings](src/field/e984295c-77bf-437b-8361-4977646fae4c/item.json)
 - **Camp fire comments** | [Details](src/field/790e3092-af3f-4179-859f-8362a33bff8d) | [Settings](src/field/790e3092-af3f-4179-859f-8362a33bff8d/item.json)
 - **Composer** | [Details](src/field/a5195930-14b9-4e13-81a8-e3fbf89ec302) | [Settings](src/field/a5195930-14b9-4e13-81a8-e3fbf89ec302/item.json)
 - **Concert location** | [Details](src/field/046cbe0a-493d-40ed-90b7-8c904a3396c9) | [Settings](src/field/046cbe0a-493d-40ed-90b7-8c904a3396c9/item.json)
 - **Concert name** | [Details](src/field/fae77b76-4350-4e98-9ab9-6f85f64bebdb) | [Settings](src/field/fae77b76-4350-4e98-9ab9-6f85f64bebdb/item.json)
 - **Credits** | [Details](src/field/897b1866-93ae-4c77-9d76-2d59fe32fc83) | [Settings](src/field/897b1866-93ae-4c77-9d76-2d59fe32fc83/item.json)
 - **DateFirstStop** | [Details](src/field/03995043-13fb-4ec7-bc66-e13434425a06) | [Settings](src/field/03995043-13fb-4ec7-bc66-e13434425a06/item.json)
 - **Eight stop** | [Details](src/field/b3974c81-418c-4117-8403-4463c492c69f) | [Settings](src/field/b3974c81-418c-4117-8403-4463c492c69f/item.json)
 - **Electricity_checkbox** | [Details](src/field/85beced9-a24c-4797-a94b-5aa7c460076e) | [Settings](src/field/85beced9-a24c-4797-a94b-5aa7c460076e/item.json)
 - **Electricity_comments** | [Details](src/field/e302de6a-6249-4ced-9894-ee0cf9a79e28) | [Settings](src/field/e302de6a-6249-4ced-9894-ee0cf9a79e28/item.json)
 - **Execution_notes** | [Details](src/field/93945801-c567-44ab-802c-43e8f8a98643) | [Settings](src/field/93945801-c567-44ab-802c-43e8f8a98643/item.json)
 - **Fifth stop** | [Details](src/field/ed30c695-5d2c-41b1-8849-6e75d2a7554a) | [Settings](src/field/ed30c695-5d2c-41b1-8849-6e75d2a7554a/item.json)
 - **First stop** | [Details](src/field/934eb37b-0fb1-4fed-b3ec-969cd0b364ee) | [Settings](src/field/934eb37b-0fb1-4fed-b3ec-969cd0b364ee/item.json)
 - **Footpath** | [Details](src/field/eee94b56-e5d2-4dbc-b576-8f0a676de8b4) | [Settings](src/field/eee94b56-e5d2-4dbc-b576-8f0a676de8b4/item.json)
 - **Fourth stop** | [Details](src/field/e9cd8058-7643-43d4-9738-d7138ed7039e) | [Settings](src/field/e9cd8058-7643-43d4-9738-d7138ed7039e/item.json)
 - **Group_name** | [Details](src/field/0d4a5caa-2199-4fb1-b07f-bd8071d71dbe) | [Settings](src/field/0d4a5caa-2199-4fb1-b07f-bd8071d71dbe/item.json)
 - **Heating checkbox** | [Details](src/field/fd05b628-8b23-42fc-aacc-78ebcf96ea60) | [Settings](src/field/fd05b628-8b23-42fc-aacc-78ebcf96ea60/item.json)
 - **Heating_comments** | [Details](src/field/cf695cba-a05d-422d-9886-d964feaad393) | [Settings](src/field/cf695cba-a05d-422d-9886-d964feaad393/item.json)
 - **Identification code** | [Details](src/field/68699537-3391-400c-af78-177327570b4e) | [Settings](src/field/68699537-3391-400c-af78-177327570b4e/item.json)
 - **Image** | [Details](src/field/3df662f4-5924-483e-8636-24c2ed4f27bf) | [Settings](src/field/3df662f4-5924-483e-8636-24c2ed4f27bf/item.json)
 - **Is a Stop** | [Details](src/field/2d01d455-4120-45bf-bce3-eba4354989c0) | [Settings](src/field/2d01d455-4120-45bf-bce3-eba4354989c0/item.json)
 - **Kitchen_checkbox** | [Details](src/field/7b541f51-6f3f-4f78-a8b4-2dd3009714d7) | [Settings](src/field/7b541f51-6f3f-4f78-a8b4-2dd3009714d7/item.json)
 - **Kitchen_comments** | [Details](src/field/f8c6ddf1-eee0-408d-9634-b7ff3b19193f) | [Settings](src/field/f8c6ddf1-eee0-408d-9634-b7ff3b19193f/item.json)
 - **Komoot_embed_code** | [Details](src/field/fa66abdf-89d9-452d-b68e-353c78a630f2) | [Settings](src/field/fa66abdf-89d9-452d-b68e-353c78a630f2/item.json)
 - **Latitude (decimal)** | [Details](src/field/b83771c3-ffd1-4827-a41d-a633873517c7) | [Settings](src/field/b83771c3-ffd1-4827-a41d-a633873517c7/item.json)
 - **Location** | [Details](src/field/44ac0436-5edb-4787-acea-afc18da84380) | [Settings](src/field/44ac0436-5edb-4787-acea-afc18da84380/item.json)
 - **Long description** | [Details](src/field/048ef402-65a6-443f-9e3a-1ac67dcd0bf6) | [Settings](src/field/048ef402-65a6-443f-9e3a-1ac67dcd0bf6/item.json)
 - **Long description** | [Details](src/field/382f24f4-aea2-448e-927c-99d89bb6ed40) | [Settings](src/field/382f24f4-aea2-448e-927c-99d89bb6ed40/item.json)
 - **Longitude (decimal)** | [Details](src/field/2c6061d1-eb07-4f29-858b-21e4439b237b) | [Settings](src/field/2c6061d1-eb07-4f29-858b-21e4439b237b/item.json)
 - **Musical genre** | [Details](src/field/4743eb8a-e4a4-4ff1-8d26-b5c2d1721e3e) | [Settings](src/field/4743eb8a-e4a4-4ff1-8d26-b5c2d1721e3e/item.json)
 - **Name** | [Details](src/field/ea8871b6-4f71-480b-bbd7-0d71322c6464) | [Settings](src/field/ea8871b6-4f71-480b-bbd7-0d71322c6464/item.json)
 - **Ninth stop** | [Details](src/field/2a0bda5d-0076-4f48-9f95-51742c73b564) | [Settings](src/field/2a0bda5d-0076-4f48-9f95-51742c73b564/item.json)
 - **Part_type** | [Details](src/field/6d03c3a1-ce6e-4ef1-867d-47a06c01e9d9) | [Settings](src/field/6d03c3a1-ce6e-4ef1-867d-47a06c01e9d9/item.json)
 - **Participants** | [Details](src/field/7f496a03-f125-4379-af46-1cec6b335b13) | [Settings](src/field/7f496a03-f125-4379-af46-1cec6b335b13/item.json)
 - **Piece_id** | [Details](src/field/a557cc9f-7c09-494e-a8b0-2845ad80d940) | [Settings](src/field/a557cc9f-7c09-494e-a8b0-2845ad80d940/item.json)
 - **Place** | [Details](src/field/38b8ba46-7137-4d4d-9da4-2c67b4e5c6a3) | [Settings](src/field/38b8ba46-7137-4d4d-9da4-2c67b4e5c6a3/item.json)
 - **Place_altitude** | [Details](src/field/90bae545-7186-4555-bfbc-6c135ae72898) | [Settings](src/field/90bae545-7186-4555-bfbc-6c135ae72898/item.json)
 - **Place_id** | [Details](src/field/143b101b-a9c9-41eb-9f23-ebf9e9b1146b) | [Settings](src/field/143b101b-a9c9-41eb-9f23-ebf9e9b1146b/item.json)
 - **Places indoor** | [Details](src/field/00ea1e01-ff68-4feb-8649-68c63d4e062c) | [Settings](src/field/00ea1e01-ff68-4feb-8649-68c63d4e062c/item.json)
 - **Places outdoor** | [Details](src/field/aaf3f211-ba95-45cc-a2a1-881d6ea35d50) | [Settings](src/field/aaf3f211-ba95-45cc-a2a1-881d6ea35d50/item.json)
 - **Program pieces** | [Details](src/field/a5153072-1cd3-454d-a41b-06c6f349f725) | [Settings](src/field/a5153072-1cd3-454d-a41b-06c6f349f725/item.json)
 - **Public performance** | [Details](src/field/f1d51293-83af-40f3-b52a-7d5615664dc6) | [Settings](src/field/f1d51293-83af-40f3-b52a-7d5615664dc6/item.json)
 - **Rest rooms checkbox** | [Details](src/field/7b8c2df6-7725-4d31-ac4f-adf9d4e3b5a7) | [Settings](src/field/7b8c2df6-7725-4d31-ac4f-adf9d4e3b5a7/item.json)
 - **Rest rooms comments** | [Details](src/field/cca6eefd-e461-430b-9213-62255017eb5d) | [Settings](src/field/cca6eefd-e461-430b-9213-62255017eb5d/item.json)
 - **Score** | [Details](src/field/52b08926-9a63-44b4-8a19-580996822e76) | [Settings](src/field/52b08926-9a63-44b4-8a19-580996822e76/item.json)
 - **Second stop** | [Details](src/field/4a87c014-04ca-4986-8aea-43ed407ff07a) | [Settings](src/field/4a87c014-04ca-4986-8aea-43ed407ff07a/item.json)
 - **Security rules** | [Details](src/field/e5acc3ed-593b-4318-a3fd-47a82e47bf45) | [Settings](src/field/e5acc3ed-593b-4318-a3fd-47a82e47bf45/item.json)
 - **Seventh stop** | [Details](src/field/aae1f2fc-19c1-420d-af91-b79efa778ba2) | [Settings](src/field/aae1f2fc-19c1-420d-af91-b79efa778ba2/item.json)
 - **Short Description** | [Details](src/field/c9896d41-82cf-42da-873f-2b7c59e22b81) | [Settings](src/field/c9896d41-82cf-42da-873f-2b7c59e22b81/item.json)
 - **Sixth stop** | [Details](src/field/adc03eca-4944-4244-a993-a6c30692fc23) | [Settings](src/field/adc03eca-4944-4244-a993-a6c30692fc23/item.json)
 - **Soprano label** | [Details](src/field/07f81786-8c38-4b30-b8cb-7cf819608092) | [Settings](src/field/07f81786-8c38-4b30-b8cb-7cf819608092/item.json)
 - **Soprano part** | [Details](src/field/24def5ef-d5be-4c86-9c67-2439ef3ffe4c) | [Settings](src/field/24def5ef-d5be-4c86-9c67-2439ef3ffe4c/item.json)
 - **Soprano part YouTube** | [Details](src/field/9cb0fa42-2119-4014-aaca-8cbef2ad9473) | [Settings](src/field/9cb0fa42-2119-4014-aaca-8cbef2ad9473/item.json)
 - **Telephone** | [Details](src/field/096fd1f5-480a-4a8b-98cf-4fceac5e7999) | [Settings](src/field/096fd1f5-480a-4a8b-98cf-4fceac5e7999/item.json)
 - **Tenor label** | [Details](src/field/b7393f14-c071-453a-b96e-3f246d95b51c) | [Settings](src/field/b7393f14-c071-453a-b96e-3f246d95b51c/item.json)
 - **Tenor part** | [Details](src/field/d4d78461-cb50-4d60-924b-c37e5737a2c7) | [Settings](src/field/d4d78461-cb50-4d60-924b-c37e5737a2c7/item.json)
 - **Tenor part YouTube** | [Details](src/field/e41f4b77-325a-4035-a25f-ef25fe04894d) | [Settings](src/field/e41f4b77-325a-4035-a25f-ef25fe04894d/item.json)
 - **Tenth stop** | [Details](src/field/a43b487c-51d6-4264-8925-067e3368bcbe) | [Settings](src/field/a43b487c-51d6-4264-8925-067e3368bcbe/item.json)
 - **Third stop** | [Details](src/field/f68fdba1-62f1-4396-b915-cacc79206db5) | [Settings](src/field/f68fdba1-62f1-4396-b915-cacc79206db5/item.json)
 - **Title** | [Details](src/field/2a2f971b-76ec-4d78-838c-45548ee7632c) | [Settings](src/field/2a2f971b-76ec-4d78-838c-45548ee7632c/item.json)
 - **Water checkbox** | [Details](src/field/d3a5af2d-6b37-49ba-a4b6-0940501091f8) | [Settings](src/field/d3a5af2d-6b37-49ba-a4b6-0940501091f8/item.json)
 - **Water comments** | [Details](src/field/7b9ada22-e39d-4ed6-8486-a0d81f31a709) | [Settings](src/field/7b9ada22-e39d-4ed6-8486-a0d81f31a709/item.json)

### All used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")