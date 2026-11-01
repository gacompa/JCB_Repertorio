### JCB! Site View
# Locations blocks (locations_blocks)

Main view for Locations - blocks view

## HTML:
```html
<?php JustTEXT::_('Altitude'); ?>
<?php JustTEXT::_('Is a base'); ?>
<?php JustTEXT::_('Is not a base'); ?>
<?php JustTEXT::_('Is a stop'); ?>
<?php JustTEXT::_('Is not a stop'); ?>
<?php JustTEXT::_('m above sea level'); ?>
<?php JustTEXT::_('Places indoor | places outdoor'); ?>
<?php JustTEXT::_('Indoor'); ?>
<?php JustTEXT::_('Outdoor'); ?>

<?php echo $this->toolbar->render(); ?><form action="<?php echo Route::_('index.php?option=com_bookings'); ?>" method="post" name="adminForm" id="adminForm">
<?php echo $this->toolbar->render(); ?>
<?php echo LayoutHelper::render('rowslocations', []); ?>



<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Box con Tre Sezioni</title>
<style>
/* BASE E CONTENITORE PRINCIPALE */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px 0;
            display: flex;
            justify-content: center;
        }

        .custom-box {
            width: 90%; /* spans to 90% of the window width */
            max-width: 850px; /* Maximum width for desktop */
            min-width: 300px; /* Minimum width for smartphone */
            border: 1px solid #ccc;
            border-radius: 12px;
            overflow: hidden; 
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        /* --- PRIMA RIGA: BARRA SUPERIORE (Titolo) --- */
        .top-bar {
            background-color: #4CAF50; /* Green */
            color: white;
            padding: 15px 20px;
            font-size: 1.5em; /* Size of responsive text */
            font-weight: bold;
            text-align: center;
        }

        /* --- SECONDA RIGA: IMMAGINE E TESTO (Flexbox) --- */
        .middle-content {
            padding: 20px;
            display: flex; /* Activate Flexbox */
            gap: 20px; /* space between columns */
            border-bottom: 1px solid #eee;
        }

        /* Contenitore Immagine (35% su Desktop) */
        .image-container {
            flex: 0 0 35%; /* Do not increase, do not squeeze, base is 35% */
            max-width: 35%;
        }

        .image-container img {
            width: 100%; 
            height: auto;
            display: block;
            border-radius: 8px; 
        }

        /* Contenitore Testo (65% su Desktop) */
        .text-content {
            flex-grow: 1; /* fills the remaining space */
            padding-right: 10px; /* little space on the right */
        }

        .text-content h3 {
            margin-top: 0;
            color: #333;
        }
       
        /* The Modal/Lightbox (hidden by default) */
        .lightbox {
            display: none; /* Hidden by default */
            position: fixed; /* Stay fixed on the screen */
           z-index: 9999; /* Sit on top of everything */
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto; /* Enable scroll if needed */
            background-color: rgba(0, 0, 0, 0.9); /* Black background with opacity */
        }

        /* Image inside the Modal */
        .lightbox-content {
            margin: auto;
            display: block;
            max-width: 90%; /* Limits the image width */
            max-height: 90vh; /* Limits the image height to 90% of the viewport height */
            position: relative;
            top: 50%;
            transform: translateY(-50%); /* Centers vertically */
        }

        /* The Close Button */
        .close-button {
            position: absolute;
            top: 15px;
            right: 35px;
            color: #f1f1f1;
            font-size: 40px;
            font-weight: bold;
            transition: 0.3s;
            cursor: pointer;
        }

        /* --- TERZA RIGA: TABELLA DATI --- */
        .bottom-content {
            padding: 20px;
        }
        
        .data-table {
            width: 100%;
            border-collapse: collapse;
        }

        .data-table td {
            padding: 10px 15px;
            border-bottom: 1px solid #f0f0f0;
            font-size: 0.9em;
        }

        .data-table .label {
            width: 40%;
            font-weight: bold;
            color: #555;
            background-color: #f9f9f9;
        }

        /* --- MEDIA QUERY: adapt to small screens (Mobile) --- */
        @media (max-width: 600px) {
            
            .middle-content {
                flex-direction: column; /* stacks image and text vertically */
                gap: 15px;
            }
            
            .image-container {
                /* The image spans to occupy all available space */
                flex: 1 1 100%; 
                max-width: 100%;
            }

            .text-content {
                padding-right: 0;
            }

            .data-table td {
                /* REduce padding for small size screens */
                padding: 8px 10px;
            }

            .data-table .label {
                width: 50%; /* The label is larget to avoid breaking lines */
            }
        }
    </style>
    </head>

<?php foreach ($this->items as $item): ?>
<body>

<div class="custom-box">
    <div class="top-bar">
        <?php $link_singolo = Route::_('index.php?option=com_bookings&view=location_single&id='. $item->id); ?>
        <b><?php echo "<a href=\"$link_singolo\"> $item->name</a>"; ?></b><br/><?php echo $item->description; ?>    
    </div>
    <div class="middle-content">
        <div class="image-container">
            <?php $baseurl = Uri::root(); ?>
            <?php $fullImageUrl = $baseurl . $item->image; ?>
            <img 
                src="<?php echo $item->image; ?>" 
                alt="Click to Enlarge" 
                onclick="openLightbox('<?php echo htmlspecialchars($fullImageUrl); ?>')"
                style="cursor: pointer; width: 300px; height: auto;" 
            />
            <?php echo JText::_('Click image to enlarge') ; ?>
        </div>
        <div id="lightbox-modal" class="lightbox" onclick="closeLightbox()">
            <span class="close-button">&times;</span>
            <img id="lightbox-image" class="lightbox-content" src="<?php echo JPATH_ROOT . "/" .  $item->image; ?>" alt="Enlarged Image">
        </div>       
        <div class="text-content">
            <p>
            <?php echo $item->longdescription ; ?>  
            </p>
        </div>
    </div>
    <div class="bottom-content">
        <table class="data-table">
            <tr>
                <td class="label"><?php echo Text::_('COM_BOOKINGS_ALTITUDE'); ?> </td>
                <td class="value"><?php echo $item->place_altitude . " " . Text::_('COM_BOOKINGS_M_ABOVE_SEA_LEVEL') ?> </td>
            </tr>
            <tr>
                <td class="label"><?php echo JText::_('Type'); ?> </td>
                <td class="value"><?php echo ($item->is_base) ? Text::_('COM_BOOKINGS_IS_A_BASE' ) : Text::_('COM_BOOKINGS_IS_NOT_A_BASE' ); echo " | "; echo ($item->is_stop) ? Text::_('COM_BOOKINGS_IS_A_STOP' ) : Text::_('COM_BOOKINGS_IS_NOT_A_STOP' ); ?> </td>
            </tr>
          <?php if ($item->is_stop) { ?>
            <tr>
                <td class="label"><?php echo Text::_('COM_BOOKINGS_PLACES_INDOOR_PLACES_OUTDOOR'); ?> </td>
                <td class="value"><?php echo $item->places_indoor .  " " . Text::_('COM_BOOKINGS_INDOOR') . " | " . $item->places_outdoor . " " . Text::_('COM_BOOKINGS_OUTDOOR'); ?> </td>
            </tr>
            <?php } ?>
        </table>
    </div>
</div>
<div>
    <p>
    <?php echo " " ; ?>  
    </p>
</div>
</body>
<?php endforeach; ?>


<?php if (isset($this->items) && isset($this->pagination) && isset($this->pagination->pagesTotal) && $this->pagination->pagesTotal > 1): ?>
	<div class="pagination">
		<?php if ($this->params->def('show_pagination_results', 1)) : ?>
			<p class="counter pull-right"> <?php echo $this->pagination->getPagesCounter(); ?> <?php echo $this->pagination->getLimitBox(); ?></p>
		<?php endif; ?>
		<?php echo $this->pagination->getPagesLinks(); ?>
	</div>
<?php endif; ?>
<input type="hidden" name="task" value="" />
<?php echo Html::_('form.token'); ?>
</form>


<script>
function openLightbox(imageSource) {
    // Get the modal and image elements
    const modal = document.getElementById('lightbox-modal');
    const modalImg = document.getElementById('lightbox-image');

    // Set the image source and display the modal
    modalImg.src = imageSource;
    modal.style.display = 'block';
}

function closeLightbox() {
    const modal = document.getElementById('lightbox-modal');
    modal.style.display = 'none';
}

// Optional: Close the modal if the user presses the ESC key
document.addEventListener('keydown', function(event) {
    if (event.key === "Escape") {
        closeLightbox();
    }
});
</script>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")