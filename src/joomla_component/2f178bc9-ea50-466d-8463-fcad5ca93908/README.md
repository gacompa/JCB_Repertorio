### JCB! Joomla Component
# Bookings (v1.0.14)
## Bookings (Bookings)

> Management of bookings for hikes or routes

This component offer tools to manage bookings for hikes or routes.

### Company Details
- Scoutcodera
- gacompa
- [email](mailto:centralina.codera@gmail.com)
- [website](https://scoutcodera.it)

### Component Settings
| Setting                       | Value               |
|-------------------------------|---------------------|
| Add Custom Code Placeholders  | ![no](https://img.shields.io/badge/no-blue?style=flat-square)  |
| Debug (line numbers)          | ![no](https://img.shields.io/badge/no-blue?style=flat-square) |

### License
```text
GNU/GPL Version 2 or later - http://www.gnu.org/licenses/gpl-2.0.html
```

### Copyright
```text
Copyright (C) 2025. All Rights Reserved
```

<details>
<summary>README Template</summary>

```markdown
# ###com_bookings### (###VERSION###)
A digital environment to manage hikes and routes in a area.
+ Places are geographical points in the area, characterized by their geographic attributes as coordinates, altitude
+ Locations are places relevant for the description of footpaths, either sleeping stop or transit places. They are characterized by description and list of offered services.
+ Footpath are the trails connecting locations, they have a specific description and the link to a third-party trekking app map and profile.

Main administrative functionalities are
+ Places: the list of places managed by the component
+ Locations: descriptions of the subset of places for overnight stay for the night (either in-door or out-door)
+ Footpaths: the list of trails descriptions
While places data are geographical objective attributes (and then managed only bu administrator) the Location and Footpath descriptions are subjective and can be edited by a group of users by a front-end view.

Main viewer functionalities are
+ Llist of Locations and detailed card for each single location
+ Map of places
+ list of footpaths and detailed description of each single footpath


To be done
Reservations
+ a tool to simulate a route with stops and transit
+ a tool to submit the proposed route
+ a tool for administrators to interact with the proposer for modifications and at the end confirm the final version or reject the proposal
Reporting
+ a tool to archive the booking, recording main reporting data (effective number of people, payment methods, comments, images ...)
Keepers
+ a calendar to manage the presence of keepers in the Bases
Calendar
+ a calendar to display the presence of groups and the availability of places

T.b.d.

Analytics to display occupation of places, number of people ...
# Installation
The software is packaged in a standard Joomla zip component, to install follow the standard installation steps.
Create (and populate if needed) the media folder
+ in Images create the folder com_bookings and then the subfolders Icons and Locations to store the images
+ identify which group will be allowed to edit (from the front-end) the descriptions of Locations and Footpaths (remember that Places can be edited only by administrators)
+ create the relevant menu entry, in the following list the name of the Menu Item Type for Bookings are displayed
  + Locations list: the list of locations which links to the view of a single location
   > Locations list
  + Location single: hidden menu item, is required to route the request to view a single location
   >iLocation single
  + Places map: places shown on a map
   >Places map
  + Locations edit list: for the users group allowed to modify the locations description
   >Locations edit list
  + Location edit single: hidden menu item, is required to route the request to edit a single location
   >Create Location
  + Footpath list: the list of footpaths which links to the view of a single footpath
   >Footpaths list
  + Footpath single: hidden menu item, is required to route the request to view a single fottpath
   >Footpath single
  + Footpath edit list: for the users group allowed to modify the footpath description
   >Footpaths edit list
  + Footpath edit single: hidden menu item, is required to route the request to edit a single footpath
   >Create Footpath
+ check the routing of the edit single functions
```

</details>

> Harness the power of this fully self-contained Joomla Component — complete, customizable, and built to manage data, views, logic, and access control seamlessly through JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")