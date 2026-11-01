### JCB! Site View
# Location single (location_single)

Display of one location description, map and other info

## HTML:
```html
<?php JustTEXT::_(' [Space for interactive map]'); ?>
<?php JustTEXT::_('Detailed description'); ?>
<?php JustTEXT::_('Parameter'); ?>
<?php JustTEXT::_('Value'); ?>
<?php JustTEXT::_('Outdoor'); ?>
<?php JustTEXT::_('Sleeping places'); ?>
<?php JustTEXT::_('Outdoor'); ?>
<?php JustTEXT::_('Rest rooms'); ?>
<?php JustTEXT::_('Yes'); ?>
<?php JustTEXT::_('No'); ?>
<?php JustTEXT::_('Water'); ?>
<?php JustTEXT::_('Heating'); ?>
<?php JustTEXT::_('Electricity'); ?>
<?php JustTEXT::_('Kitchen'); ?>
<?php JustTEXT::_('Camp fire'); ?>

<?php 
// Get the application object.
$app = JFactory::getApplication();
// Get the JInput object.
$jinput = $app->input;
//Using getInt() ensures that the value is treated as a secure integer, which is crucial for preventing SQL injection and other vulnerabilities.
$itemId = $jinput->getInt('id');
?>

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Layout Dettagli Completo</title>
    <style>
        /* Base Reset and Body Styling */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        /* --- 1. TITLE ROW --- */
        .title-row {
             background-color: #4CAF50; /* Verde for header*/
            color: white;
            padding: 15px 20px;
            font-size: 1.8em;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        /* --- 2. MAIN CONTENT CONTAINER (Image + Map) --- */
        .main-content-container {
            display: flex; /* Enables Flexbox for side-by-side layout */
            flex-wrap: wrap; /* Allows wrapping on smaller screens */
            padding: 20px;
            gap: 20px; /* Space between the image and map columns */
        }

        /* Image Column (70%) */
        .image-column {
            flex: 1 1 70%; /* Base: 70% width, flexible growth/shrinkage */
            max-width: 70%;
            overflow: hidden;
            background-color: white;
            padding: 10px;
            border-radius: 12px;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
        }

        .image-column img {
            width: 100%;
            height: auto;
            display: block;
            border-radius: 8px; /* Rounded corners for the image itself */
        }

        /* Map Column (30%) */
        .map-column {
            flex: 1 1 25%; /* Base: 25% width (leaving space for gap) */
            max-width: 25%;
            background-color: #e0e0e0; /* Placeholder background */
            display: flex;
            align-items: center;
            justify-content: center;
            height: 400px; /* Set a fixed height for the map placeholder */
            border-radius: 8px;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            /* Important: The map frame should match the image height */
            height: 100%; 
        }

        /* --- 3. DETAIL TABLE ROW --- */
        .detail-table-row {
            padding: 0 20px 20px;
        }

        .data-table {
            width: 100%;
            border-collapse: collapse;
            background-color: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
        }

        .data-table th, .data-table td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        .data-table th {
            background-color: #f2f2f2;
            font-weight: bold;
            color: #333;
        }

        .data-table tr:last-child td {
            border-bottom: none;
        }

        /* --- RESPONSIVENESS (Mobile View) --- */
        @media (max-width: 800px) {
            .main-content-container {
                flex-direction: column; /* Stack columns vertically on small screens */
            }

            .image-column, .map-column {
                flex: 1 1 100%; /* Each item takes 100% width */
                max-width: 100%;
            }
        }
    </style>
</head>
<body>

    <div class="title-row">
        <?php echo $this->escape($this->item->name) ; ?>
    </div>

    <div class="main-content-container">
        
        <div class="image-column">
           <img src="<?php echo $this->escape($this->item->image) ; ?>" alt="Immagine Principale">
        </div>

        <div class="map-column">
           <?php echo Text::_('COM_BOOKINGS_SPACE_FOR_INTERACTIVE_MAP') ; ?>
        </div>

        
    </div>

    <div class="detail-table-row">
        <h2><?php echo Text::_('COM_BOOKINGS_DETAILED_DESCRIPTION') ; ?></h2>
        <table class="data-table">
            <thead>
                <tr>
                    <th><?php echo Text::_('COM_BOOKINGS_PARAMETER') ; ?></th>
                    <th><?php echo Text::_('COM_BOOKINGS_VALUE') ; ?></th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_ALTITUDE') ; ?></td>
                    <td><?php echo $this->escape($this->item->place_altitude) . " " .  Text::_('COM_BOOKINGS_M_ABOVE_SEA_LEVEL') ; ?></td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_LOCATION') ; ?></td>
                    <td><?php echo $this->escape($this->item->location) ; ?></td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_SLEEPING_PLACES') ; ?></td>
                    <td><?php echo $this->escape($this->item->places_indoor) . " " . Text::_('COM_BOOKINGS_INDOOR') . " | " . $this->escape($this->item->places_outdoor) . " " . Text::_('COM_BOOKINGS_OUTDOOR') ; ?></td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_REST_ROOMS') ; ?></td>
                    <td>
                        <?php echo (($this->escape($this->item->rest_room_checkbox)) ? Text::_('COM_BOOKINGS_YES') . " " : Text::_('COM_BOOKINGS_NO') . " ") ; ?>
                        <?php echo $this->escape($this->item->rest_room_comments) ;?>
                    </td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_WATER') ; ?></td>
                    <td>
                        <?php echo (($this->escape($this->item->water_checkbox)) ? Text::_('COM_BOOKINGS_YES') . " " : Text::_('COM_BOOKINGS_NO') . " ") ; ?>
                        <?php echo $this->escape($this->item->water_comments) ;?>
                    </td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_HEATING') ; ?></td>
                    <td>
                        <?php echo (($this->escape($this->item->rest_room_checkbox)) ? Text::_('COM_BOOKINGS_YES') . " " : Text::_('COM_BOOKINGS_NO') . " ") ; ?>
                        <?php echo $this->escape($this->item->heating_comments) ;?>
                    </td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_ELECTRICITY') ; ?></td>
                    <td>
                        <?php echo (($this->escape($this->item->electricity_checkbox)) ? Text::_('COM_BOOKINGS_YES') . " " : Text::_('COM_BOOKINGS_NO') . " ") ; ?>
                        <?php echo $this->escape($this->item->electricity_comments) ;?>
                    </td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_KITCHEN') ; ?></td>
                    <td>
                        <?php echo (($this->escape($this->item->kitchen_checkbox)) ? Text::_('COM_BOOKINGS_YES') . " " : Text::_('COM_BOOKINGS_NO') . " ") ; ?>
                        <?php echo $this->escape($this->item->kitchen_comments) ;?>
                    </td>
                </tr>
                <tr>
                    <td><?php echo Text::_('COM_BOOKINGS_CAMP_FIRE') ; ?></td>
                    <td>
                        <?php echo (($this->escape($this->item->camp_fire_checkbox)) ? Text::_('COM_BOOKINGS_YES') . " " : Text::_('COM_BOOKINGS_NO') . " ") ; ?>
                        <?php echo $this->escape($this->item->camp_fire_comments) ;?>
                    </td>
                </tr>

            </tbody>

        </table>
    </div>


</body>
</form>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")