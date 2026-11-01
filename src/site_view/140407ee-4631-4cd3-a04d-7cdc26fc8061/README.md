### JCB! Site View
# Select piece (select_piece)

The form to identify the required piece in the list, the ID will be passed to the display page

## HTML:
```html
<?php
defined('_JEXEC') or die;

use Joomla\CMS\HTML\HTMLHelper;


// 1. get data from the Dynamic Get
$items = $this->items; 

// 2. Prepariamo gli array per i menu a tendina filtrando i duplicati
$genres  = [];
$composers = [];

if (!empty($items)) {
    foreach ($items as $item) {
        if (!empty($item->genre)) {
            $genres[$item->genre] = $item->genre;
        }
        if (!empty($item->composer)) {
            $composers[$item->composer] = $item->composer;
        }
    }
}

// 3. Recuperiamo i valori eventualmente già selezionati dall'utente (per mantenere lo stato dopo il submit)
$input        = Factory::getApplication()->input;
$selectGenre  = $input->get('filter_genre', '', 'string');
$selectcomposer = $input->get('filter_composer', '', 'string');
$selectPiece  = $input->get('filter_piece_id', 0, 'int');
?>

<div class="container my-4">
    <h3><?php echo TEXT::_('Select a piece from the Repertoire'); ?></h3>
    
    <form action="<?php echo htmlspecialchars(\Joomla\CMS\Uri\Uri::getInstance()->toString()); ?>" method="post" id="repertorioFilterForm">
        <div class="row g-3">

        <!-- TENDINA 3: Selezione per Genre (Punteggio/Tipo) -->
        <!-- cancellata, rimangono autore e titolo -->          
            
            <!-- TENDINA 1: Selezione per Autore -->
            <div class="col-md-4">
                <label for="filter_composer" class="form-label"><?php echo TEXT::_('Filter by composer'); ?>:</label>
                <select name="filter_composer" id="filter_composer" class="form-select" onchange="this.form.submit()">
                    <option value="">-- <?php echo TEXT::_('Select composer'); ?> --</option>
                    <?php foreach ($composers as $composer) : ?>
                        <option value="<?php echo htmlspecialchars($composer); ?>" <?php echo ($selectcomposer === $composer) ? 'selected' : ''; ?>>
                            <?php echo htmlspecialchars($composer); ?>
                        </option>
                    <?php endforeach; ?>
                </select>
            </div>

            <!-- TENDINA 2: Selezione del Singolo Brano (filtrato o totale) -->
            <div class="col-md-4">
                <label for="filter_piece_id" class="form-label"><?php echo TEXT::_('Select by title'); ?>:</label>
                <select name="filter_piece_id" id="filter_piece_id" class="form-select">
                    <option value="">-- <?php echo TEXT::_('Select title'); ?> --</option>
                    <?php foreach ($items as $item) : ?>
                        <?php 
                        // Se l'utente ha scelto un autore o uno genre nelle altre tendine, mostriamo solo i brani coerenti
                        if (!empty($selectcomposer) && $item->composer !== $selectcomposer) continue;
                        if (!empty($selectGenre) && $item->genre !== $selectGenre) continue;
                        ?>
                        <option value="<?php echo (int) $item->id; ?>" <?php echo ($selectPiece == $item->id) ? 'selected' : ''; ?>>
                            <?php echo htmlspecialchars($item->title) . ' (' . htmlspecialchars($item->composer) . ')'; ?>
                        </option>
                    <?php endforeach; ?>
                </select>
            </div>

        </div>

<div class="mt-3">
    <button type="submit" class="btn btn-primary"><?php echo Text::_('Confirm selection'); ?></button>
    <a href="<?php echo \Joomla\CMS\Uri\Uri::getInstance()->toString(); ?>" class="btn btn-text text-muted">
        <?php echo Text::_('Reset filters'); ?>
    </a>
</div>

        <?php echo HTMLHelper::_('form.token'); ?>
    </form>
</div>

<!-- Sezione per mostrare il risultato del brano identificato -->
<?php if ($selectPiece > 0) : ?>
    <hr>
    <div class="alert alert-success mt-3">
        <h5><?php echo TEXT::_('Selected piece'); ?>: <?php echo $selectPiece; ?></h5>
        <!-- Qui puoi fare logiche aggiuntive o caricare il dettaglio -->
        <?php $baseUrl = Route::_("index.php?option=com_repertorio&view=piece_single&id=$selectPiece"); ?>
<script>
    // Reindirizza il browser alla nuova pagina
    window.location.href = <?php echo json_encode($baseUrl); ?>;
</script>
    </div>
<?php endif; ?>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")