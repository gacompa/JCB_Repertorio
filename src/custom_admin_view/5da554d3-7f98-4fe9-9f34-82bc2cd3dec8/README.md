### JCB! Custom Admin View
# Pieces tab (pieces_tab)

Pieces in tabular mode

## HTML:
```html
<form action="<?php echo Route::_('index.php?option=com_repertorio&view=tua_custom_view'); ?>" method="post" name="adminForm" id="adminForm">

    <?php if (!empty($this->sidebar)) : ?>
        <div id="j-sidebar-container" class="span2">
            <?php echo $this->sidebar; ?>
        </div>
        <div id="j-main-container" class="span10">
    <?php else : ?>
        <div id="j-main-container">
    <?php endif; ?>

    <div class="custom-admin-header mb-3">
        <h2><?php echo Text::_('Gestione e Manipolazione Schede Repertorio'); ?></h2>
        <p class="text-muted">Modifica rapida dei record raggruppati per sezioni funzionali.</p>
    </div>

    <?php if (empty($this->items)) : ?>
        <div class="alert alert-info">
            <?php echo Text::_('JGLOBAL_NO_MATCHING_RESULTS'); ?>
        </div>
    <?php else : ?>
        <div class="custom-records-grid">
            <?php foreach ($this->items as $i => $item) : ?>
                <?php $itemId = (int) $item->id; ?>
                <div class="record-card">
                    
                    <!-- Header Scheda -->
                    <div class="card-header-row">
                        <span class="badge bg-dark">ID: <?php echo $itemId; ?></span>
                        <div class="card-select">
                            <?php echo Html::_('grid.id', $i, $itemId); ?>
                        </div>
                    </div>

                    <div class="card-fields-body">
                        
                        <!-- SEZIONE 1: Dati Anagrafici -->
                        <div class="card-section">
                            <h4 class="section-title">📌 Dati Anagrafici</h4>
                            <div class="field-group mb-2">
                                <label for="title_<?php echo $itemId; ?>"><strong>Titolo</strong></label>
                                <input type="text" 
                                       name="items[<?php echo $itemId; ?>][title]" 
                                       id="title_<?php echo $itemId; ?>" 
                                       value="<?php echo htmlspecialchars($item->title ?? '', ENT_QUOTES, 'UTF-8'); ?>" 
                                       class="form-control form-control-sm" />
                            </div>

                            <div class="fields-row">
                                <div class="field-group">
                                    <label for="composer_<?php echo $itemId; ?>">Compositore</label>
                                    <input type="text" 
                                           name="items[<?php echo $itemId; ?>][composer]" 
                                           id="composer_<?php echo $itemId; ?>" 
                                           value="<?php echo htmlspecialchars($item->composer ?? '', ENT_QUOTES, 'UTF-8'); ?>" 
                                           class="form-control form-control-sm" />
                                </div>
                                <div class="field-group">
                                    <label for="genre_<?php echo $itemId; ?>">Genere</label>
                                    <input type="text" 
                                           name="items[<?php echo $itemId; ?>][genre]" 
                                           id="genre_<?php echo $itemId; ?>" 
                                           value="<?php echo htmlspecialchars($item->genre ?? '', ENT_QUOTES, 'UTF-8'); ?>" 
                                           class="form-control form-control-sm" />
                                </div>
                            </div>
                        </div>

                        <!-- SEZIONE 2: Spartito, Tipo & Public Performance -->
                        <div class="card-section">
                            <h4 class="section-title">📄 Spartito e Media Principali</h4>
                            <div class="fields-row mb-2">
                                <div class="field-group">
                                    <label for="score_<?php echo $itemId; ?>">File Spartito (PDF)</label>
                                    <input type="text" 
                                           name="items[<?php echo $itemId; ?>][score]" 
                                           id="score_<?php echo $itemId; ?>" 
                                           value="<?php echo htmlspecialchars($item->score ?? '', ENT_QUOTES, 'UTF-8'); ?>" 
                                           class="form-control form-control-sm" />
                                </div>
                                <div class="field-group">
                                    <label for="part_type_<?php echo $itemId; ?>">Tipo Parte</label>
                                    <select name="items[<?php echo $itemId; ?>][part_type]" id="part_type_<?php echo $itemId; ?>" class="form-select form-select-sm">
                                        <?php $pType = strtolower((string)($item->part_type ?? 'recording')); ?>
                                        <option value="recording" <?php echo ($pType === 'recording') ? 'selected' : ''; ?>>Recording (MP3/Audio)</option>
                                        <option value="youtube" <?php echo ($pType === 'youtube') ? 'selected' : ''; ?>>YouTube</option>
                                    </select>
                                </div>
                            </div>

                            <!-- Campo Public Performance -->
                            <div class="field-group">
                                <label for="public_performance_<?php echo $itemId; ?>">🎬 Public Performance (YouTube Video ID/Link)</label>
                                <input type="text" 
                                       name="items[<?php echo $itemId; ?>][public_performance]" 
                                       id="public_performance_<?php echo $itemId; ?>" 
                                       value="<?php echo htmlspecialchars($item->public_performance ?? '', ENT_QUOTES, 'UTF-8'); ?>" 
                                       class="form-control form-control-sm" 
                                       placeholder="es. dQw4w9WgXcQ o https://youtu.be/..." />
                            </div>
                        </div>

                        <!-- SEZIONE 3: Registrazioni MP3 / Audio -->
                        <div class="card-section">
                            <h4 class="section-title">🎵 Registrazioni delle Parti (Audio File)</h4>
                            <div class="fields-row mb-1">
                                <div class="field-group">
                                    <label>Soprano Part</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][soprano_part]" value="<?php echo htmlspecialchars($item->soprano_part ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                                <div class="field-group">
                                    <label>Contralto Part</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][alto_part]" value="<?php echo htmlspecialchars($item->alto_part ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                            </div>
                            <div class="fields-row">
                                <div class="field-group">
                                    <label>Tenore Part</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][tenor_part]" value="<?php echo htmlspecialchars($item->tenor_part ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                                <div class="field-group">
                                    <label>Basso Part</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][bass_part]" value="<?php echo htmlspecialchars($item->bass_part ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                            </div>
                        </div>

                        <!-- SEZIONE 4: Link YouTube delle Parti -->
                        <div class="card-section">
                            <h4 class="section-title">▶️ Video YouTube delle Singole Parti</h4>
                            <div class="fields-row mb-1">
                                <div class="field-group">
                                    <label>Soprano YT</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][soprano_part_yt]" value="<?php echo htmlspecialchars($item->soprano_part_yt ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                                <div class="field-group">
                                    <label>Contralto YT</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][alto_part_yt]" value="<?php echo htmlspecialchars($item->alto_part_yt ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                            </div>
                            <div class="fields-row">
                                <div class="field-group">
                                    <label>Tenore YT</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][tenor_part_yt]" value="<?php echo htmlspecialchars($item->tenor_part_yt ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                                <div class="field-group">
                                    <label>Basso YT</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][bass_part_yt]" value="<?php echo htmlspecialchars($item->bass_part_yt ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" />
                                </div>
                            </div>
                        </div>

                        <!-- SEZIONE 5: Etichette delle Parti -->
                        <div class="card-section">
                            <h4 class="section-title">🏷️ Etichette Personalizzate</h4>
                            <div class="fields-row mb-1">
                                <div class="field-group">
                                    <label>Etichetta Soprano</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][soprano_label]" value="<?php echo htmlspecialchars($item->soprano_label ?? $item->sopranolabel ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" placeholder="Soprano" />
                                </div>
                                <div class="field-group">
                                    <label>Etichetta Contralto</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][alto_label]" value="<?php echo htmlspecialchars($item->alto_label ?? $item->altolabel ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" placeholder="Contralto" />
                                </div>
                            </div>
                            <div class="fields-row">
                                <div class="field-group">
                                    <label>Etichetta Tenore</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][tenor_label]" value="<?php echo htmlspecialchars($item->tenor_label ?? $item->tenorlabel ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" placeholder="Tenore" />
                                </div>
                                <div class="field-group">
                                    <label>Etichetta Basso</label>
                                    <input type="text" name="items[<?php echo $itemId; ?>][bass_label]" value="<?php echo htmlspecialchars($item->bass_label ?? $item->basslabel ?? '', ENT_QUOTES, 'UTF-8'); ?>" class="form-control form-control-sm" placeholder="Basso" />
                                </div>
                            </div>
                        </div>

                    </div>

                    <!-- Footer Scheda -->
                    <div class="card-footer-row mt-3">
                        <?php $editUrl = Route::_('index.php?option=com_repertorio&task=piece.edit&id=' . $itemId); ?>
                        <a href="<?php echo $editUrl; ?>" class="btn btn-sm btn-outline-secondary" target="_blank">
                            <span class="icon-edit" aria-hidden="true"></span> Apri Modifica Standard
                        </a>
                    </div>

                </div>
            <?php endforeach; ?>
        </div>
    <?php endif; ?>

    <input type="hidden" name="task" value="" />
    <input type="hidden" name="boxchecked" value="0" />
    <?php echo Html::_('form.token'); ?>

    </div>
</form>

<style>
.custom-records-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(460px, 1fr));
    gap: 1.5rem;
    margin-top: 1rem;
}

.record-card {
    background: #ffffff;
    border: 1px solid #dcdcdc;
    border-radius: 8px;
    padding: 1.2rem;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.03);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.card-header-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 2px solid #e9ecef;
    padding-bottom: 0.5rem;
    margin-bottom: 0.8rem;
}

.card-section {
    background: #fdfdfd;
    border: 1px solid #f0f0f0;
    border-radius: 6px;
    padding: 0.75rem;
    margin-bottom: 0.75rem;
}

.section-title {
    font-size: 0.85rem;
    font-weight: 700;
    color: #333;
    margin-bottom: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 0.3px;
}

.fields-row {
    display: flex;
    gap: 0.6rem;
}

.fields-row .field-group {
    flex: 1;
}

.field-group label {
    font-size: 0.78rem;
    margin-bottom: 0.2rem;
    display: block;
    color: #555;
}

.card-footer-row {
    border-top: 1px solid #eee;
    padding-top: 0.6rem;
    text-align: right;
}
</style>
```

> Build powerful, tailored back-end interfaces with this reusable Custom Admin View designed for flexibility, performance, and seamless integration in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")