### JCB! Site View
# Piece single (piece_single)

Show the data of a single piece

## HTML:
```html
<?php
use Joomla\CMS\Filesystem\File;
use Joomla\CMS\Uri\Uri;
?>
<!-- Bottone "Torna alla ricerca" -->
<?php $searchUrl = Route::_('index.php?option=com_repertorio&view=select_piece'); ?>
<div class="back-to-search-wrapper">
    <a href="<?php echo htmlspecialchars($searchUrl, ENT_QUOTES, 'UTF-8'); ?>" class="back-to-search-btn">
        <span class="back-icon">←</span> Torna alla ricerca
    </a>
</div>

<div class="choral-performance-grid">
    <!-- Left Column: PDF Flip-Book Viewer -->
    <?php 
        $cleanScore = File::makeSafe((string) $this->item->score);
        $pdfUrl     = Uri::root(true) . '/files/coro_della_svolta/scores/' . $cleanScore;
        $pdfUrlEsc  = htmlspecialchars($pdfUrl, ENT_QUOTES, 'UTF-8');
    ?>
    <div class="grid-section pdf-section">
        <button type="button" class="pdf-toggle-btn" id="pdf-toggle-btn"
                aria-expanded="false" aria-controls="pdf-wrapper">
            <span class="pdf-toggle-icon" id="pdf-toggle-icon">▾</span>
            <span id="pdf-toggle-label">Espandi spartito</span>
        </button>

        <div class="pdf-wrapper" id="pdf-wrapper">
            <div class="pdf-viewer-container" id="pdf-viewer-container">
                <!-- Toolbar del lettore PDF -->
                <div class="pdf-toolbar">
                    <div class="pdf-nav-controls">
                        <button type="button" id="pdf-prev" class="pdf-btn">‹ Prec</button>
                        <span class="pdf-page-info">
                            Pag. <span id="pdf-page-num">1</span> di <span id="pdf-page-count">--</span>
                        </span>
                        <button type="button" id="pdf-next" class="pdf-btn">Succ ›</button>
                    </div>

                    <!-- Controlli Zoom Manuali -->
                    <div class="pdf-zoom-controls">
                        <button type="button" id="pdf-zoom-in" class="pdf-btn-action" title="Ingrandisci (Zoom +)">➕</button>
                        <button type="button" id="pdf-zoom-out" class="pdf-btn-action" title="Riduci (Zoom -)">➖</button>
                        <button type="button" id="pdf-zoom-reset" class="pdf-btn-action" title="Ripristina dimensione">🔄</button>
                    </div>

                    <!-- Controlli Audio & Ruler per Modalità Espansa -->
                    <div class="pdf-fullscreen-audio-controls" id="pdf-fullscreen-audio-controls">
                        <div class="pdf-fs-audio-buttons" id="pdf-fs-audio-buttons"></div>
                        <div class="pdf-fs-audio-player-wrapper" id="pdf-fs-audio-player-wrapper">
                            <span class="pdf-fs-audio-label" id="pdf-fs-audio-label"></span>
                            <input type="range" class="pdf-fs-audio-progress" id="pdf-fs-audio-progress" value="0" min="0" max="100" step="0.1">
                            <span class="pdf-fs-audio-time" id="pdf-fs-audio-time">0:00 / 0:00</span>
                        </div>
                    </div>

                    <div class="pdf-actions">
                        <!-- Bottoni di Scorrimento veloce -->
                        <div class="pdf-scroll-controls">
                            <button type="button" id="pdf-scroll-up" class="pdf-btn-action" title="Scorri in alto">⬆️</button>
                            <button type="button" id="pdf-scroll-down" class="pdf-btn-action" title="Scorri in basso">⬇️</button>
                        </div>

                        <!-- Pulsante Schermo Intero Modal -->
                        <button type="button" id="pdf-fullscreen-btn" class="pdf-btn-action" title="Schermo intero">
                            <span class="action-icon">🔍</span> Ingrandisci
                        </button>

                        <!-- Pulsante Download PDF -->
                        <a href="<?php echo $pdfUrlEsc; ?>" download class="pdf-download-circular-btn" target="_blank" rel="noopener" title="Scarica PDF originale">
                            <span class="download-icon">📥</span>
                        </a>
                    </div>
                </div>

                <!-- Area Flip-Book Container -->
                <div class="pdf-canvas-wrapper" id="flipbook-wrapper">
                    <div id="pdf-loading-msg" style="color: #fff; padding: 2rem;">Caricamento dello spartito sfogliabile...</div>
                    <div id="pdf-book"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Right Column: Choral Parts & Youtube/Performance -->
    <div class="right-column">
    <?php
    $sopranoLabel = !empty(trim((string)($this->item->soprano_label ?? $this->item->sopranolabel ?? ''))) 
                    ? ($this->item->soprano_label ?? $this->item->sopranolabel) : 'Soprano';

    $altoLabel    = !empty(trim((string)($this->item->alto_label ?? $this->item->altolabel ?? ''))) 
                    ? ($this->item->alto_label ?? $this->item->altolabel) : 'Contralto';

    $tenorLabel   = !empty(trim((string)($this->item->tenor_label ?? $this->item->tenorlabel ?? ''))) 
                    ? ($this->item->tenor_label ?? $this->item->tenorlabel) : 'Tenore';

    $bassLabel    = !empty(trim((string)($this->item->bass_label ?? $this->item->basslabel ?? ''))) 
                    ? ($this->item->bass_label ?? $this->item->basslabel) : 'Basso';

    $parts = [
        'soprano' => ['initial' => 'S', 'label' => $sopranoLabel, 'audio' => $this->item->soprano_part ?? '', 'youtube' => $this->item->soprano_part_yt ?? ''],
        'alto'    => ['initial' => 'A', 'label' => $altoLabel,    'audio' => $this->item->alto_part ?? '',    'youtube' => $this->item->alto_part_yt ?? ''],
        'tenor'   => ['initial' => 'T', 'label' => $tenorLabel,   'audio' => $this->item->tenor_part ?? '',   'youtube' => $this->item->tenor_part_yt ?? ''],
        'bass'    => ['initial' => 'B', 'label' => $bassLabel,    'audio' => $this->item->bass_part ?? '',    'youtube' => $this->item->bass_part_yt ?? ''],
    ];

    $partType = strtolower(trim((string) ($this->item->part_type ?: 'recording')));

    $availableAudioParts = [];
    if ($partType !== 'youtube') {
        foreach ($parts as $key => $part) {
            if (!empty($part['audio'])) {
                $availableAudioParts[] = [
                    'key'     => $key,
                    'initial' => $part['initial'],
                    'label'   => $part['label'],
                    'audioId' => 'audio-' . $key
                ];
            }
        }
    }
    ?>
    <script>
        window.availableAudioParts = <?php echo json_encode($availableAudioParts); ?>;
    </script>

     <div class="grid-section parts-section">
     <?php $ytPointers = []; ?>
     <?php if ($partType === 'youtube') : ?>
     <div class="yt-pointer-grid">
     <?php endif; ?>
     <?php foreach ($parts as $key => $part) : ?>

        <?php if ($partType === 'youtube') : ?>
            <?php
            $videoId = RepertorioHelper::getYoutubeId($part['youtube']);
            if (!$videoId) { continue; }
            $ytPointers[] = ['key' => $key, 'label' => $part['label'], 'videoId' => $videoId];
            ?>
            <button type="button" class="yt-pointer-btn" data-yt-id="<?php echo htmlspecialchars($videoId); ?>"
                    aria-label="Riproduci parte <?php echo htmlspecialchars($part['label']); ?> su YouTube">
                <span class="yt-pointer-icon">
                    <svg viewBox="0 0 68 48" xmlns="http://www.w3.org/2000/svg">
                        <path d="M66.52 7.74c-.78-2.93-2.49-5.41-5.42-6.19C55.79.13 34 0 34 0S12.21.13 6.9 1.55C3.97 2.33 2.26 4.81 1.48 7.74.06 13.05 0 24 0 24s.06 10.95 1.48 16.26c.78 2.93 2.49 5.41 5.42 6.19C12.21 47.87 34 48 34 48s21.79-.13 27.1-1.55c2.93-.78 4.64-3.26 5.42-6.19C67.94 34.95 68 24 68 24s-.06-10.95-1.48-16.26z" fill="#f00"/>
                        <path d="M27 34l18-10-18-10z" fill="#fff"/>
                    </svg>
                </span>
                <span class="yt-pointer-label"><?php echo htmlspecialchars($part['label']); ?></span>
            </button>
        <?php else : ?>
            <?php if (empty($part['audio'])) : continue; endif; ?>
            <?php
            $audioId   = 'audio-' . $key;
            $cleanAudio = File::makeSafe((string) $part['audio']);
            $partsUrl  = Uri::root(true) . '/files/coro_della_svolta/parts/' . $cleanAudio;
            $partsUrlEsc  = htmlspecialchars($partsUrl, ENT_QUOTES, 'UTF-8');
            ?>
            <div class="part-audio-box">
                <button type="button" class="part-play-btn" data-audio="<?php echo $audioId; ?>"
                        aria-label="Riproduci parte <?php echo htmlspecialchars($part['label']); ?>">
                    <span class="play-icon">▶</span>
                </button>
                <div class="part-info">
                    <span class="part-title"><?php echo htmlspecialchars($this->item->title . ' - ' . $part['label'], ENT_QUOTES, 'UTF-8'); ?></span>
                    <div class="part-progress-row">
                        <input type="range" class="part-progress" data-audio="<?php echo $audioId; ?>"
                               value="0" min="0" max="100" step="0.1">
                        <span class="part-time" data-audio="<?php echo $audioId; ?>">0:00 / 0:00</span>
                    </div>
                </div>
                <audio id="<?php echo $audioId; ?>" preload="none" src="<?php echo $partsUrlEsc; ?>"></audio>
            </div>
        <?php endif; ?>
     <?php endforeach; ?>
     <?php if ($partType === 'youtube') : ?>
     </div>
     <?php endif; ?>
    </div>

    <?php if ($partType === 'youtube' && !empty($ytPointers)) : ?>
    <div class="grid-section yt-shared-player-section">
        <div class="yt-shared-player-wrapper" id="yt-shared-player-wrapper">
            <p class="yt-shared-placeholder" id="yt-shared-placeholder">Seleziona una parte qui sopra per avviare il video.</p>
            <iframe id="yt-shared-player" src="" title="Parte selezionata" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="display:none;"></iframe>
        </div>
    </div>
    <?php endif; ?>

    <!-- Bottom Right: Video Performance -->
    <?php 
        $publicVideoId = RepertorioHelper::getYoutubeId($this->item->public_performance);
        $videoUrl  = 'https://www.youtube.com/embed/' . $publicVideoId;
        $videoUrlEsc  = htmlspecialchars($videoUrl, ENT_QUOTES, 'UTF-8');
    ?>
    <?php if (!empty($publicVideoId) && !($publicVideoId===NULL)) : ?>
    <div class="grid-section video-section">
        <div class="video-responsive-wrapper">
            <iframe src="<?php echo $videoUrlEsc; ?>" title="Performance Video" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </div>
    </div>
    <?php endif; ?>

    </div>
</div>

<!-- Caricamento PDF.js v2.16.105 & StPageFlip via CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/page-flip/dist/js/page-flip.browser.js"></script>

<script>
document.addEventListener('DOMContentLoaded', function () {
    var pdfjsLib = window['pdfjs-dist/build/pdf'];

    if (pdfjsLib) {
        pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.worker.min.js';

        var url = '<?php echo $pdfUrlEsc; ?>';
        var bookContainer = document.getElementById('pdf-book');
        var loadingMsg = document.getElementById('pdf-loading-msg');
        var canvasWrapper = document.getElementById('flipbook-wrapper');
        var pageFlip = null;

        pdfjsLib.getDocument(url).promise.then(async function (pdfDoc) {
            var numPages = pdfDoc.numPages;
            document.getElementById('pdf-page-count').textContent = numPages;

            pageFlip = new St.PageFlip(bookContainer, {
                width: 450,
                height: 600,
                size: "stretch",
                minWidth: 300,
                maxWidth: 900,
                minHeight: 400,
                maxHeight: 1200,
                maxShadowOpacity: 0.5,
                showCover: true,
                mobileScrollSupport: false
            });

            var dpr = window.devicePixelRatio || 1;

            for (var pageNum = 1; pageNum <= numPages; pageNum++) {
                var page = await pdfDoc.getPage(pageNum);
                var viewport = page.getViewport({ scale: 1.5 * dpr });

                var pageDiv = document.createElement('div');
                pageDiv.className = 'page-slide';

                var canvas = document.createElement('canvas');
                var ctx = canvas.getContext('2d');

                canvas.height = viewport.height;
                canvas.width  = viewport.width;
                canvas.style.width  = '100%';
                canvas.style.height = '100%';

                pageDiv.appendChild(canvas);
                bookContainer.appendChild(pageDiv);

                await page.render({
                    canvasContext: ctx,
                    viewport: viewport
                }).promise;
            }

            if (loadingMsg) loadingMsg.style.display = 'none';

            pageFlip.loadFromHTML(document.querySelectorAll('.page-slide'));

            pageFlip.on('flip', (e) => {
                document.getElementById('pdf-page-num').textContent = e.data + 1;
                resetTransform();
            });

            document.getElementById('pdf-prev').addEventListener('click', function () {
                if (pageFlip) pageFlip.turnToPrevPage();
            });

            document.getElementById('pdf-next').addEventListener('click', function () {
                if (pageFlip) pageFlip.turnToNextPage();
            });

        }).catch(function (err) {
            console.error('Errore caricamento PDF Flipbook:', err);
            if (loadingMsg) loadingMsg.textContent = 'Errore durante il caricamento del PDF.';
        });

        // Gestione Zoom e Scroll/Drag
        var scale = 1;
        var isDragging = false;
        var startX = 0, startY = 0;
        var scrollLeft = 0, scrollTop = 0;

        function updateTransform() {
            if (!bookContainer) return;
            if (scale <= 1) {
                scale = 1;
                bookContainer.style.transform = 'none';
                canvasWrapper.classList.remove('is-zoomed');
            } else {
                canvasWrapper.classList.add('is-zoomed');
                bookContainer.style.transform = 'scale(' + scale + ')';
            }
        }

        function resetTransform() {
            scale = 1;
            updateTransform();
            if (canvasWrapper) {
                canvasWrapper.scrollTop = 0;
                canvasWrapper.scrollLeft = 0;
            }
        }

        if (canvasWrapper) {
            // ZOOM CON ROTELLINA DEL MOUSE
            canvasWrapper.addEventListener('wheel', function(e) {
                if (e.ctrlKey || scale > 1) {
                    e.preventDefault();
                    var zoomFactor = e.deltaY < 0 ? 0.15 : -0.15;
                    scale = Math.min(Math.max(scale + zoomFactor, 1), 3.5);
                    updateTransform();
                }
            }, { passive: false });

            // DRAG / PANNING CON MOUSE
            canvasWrapper.addEventListener('mousedown', function(e) {
                if (scale > 1) {
                    isDragging = true;
                    startX = e.pageX - canvasWrapper.offsetLeft;
                    startY = e.pageY - canvasWrapper.offsetTop;
                    scrollLeft = canvasWrapper.scrollLeft;
                    scrollTop = canvasWrapper.scrollTop;
                    canvasWrapper.style.cursor = 'grabbing';
                }
            });

            window.addEventListener('mousemove', function(e) {
                if (!isDragging || scale <= 1) return;
                e.preventDefault();
                var x = e.pageX - canvasWrapper.offsetLeft;
                var y = e.pageY - canvasWrapper.offsetTop;
                var walkX = (x - startX) * 1.5;
                var walkY = (y - startY) * 1.5;
                canvasWrapper.scrollLeft = scrollLeft - walkX;
                canvasWrapper.scrollTop = scrollTop - walkY;
            });

            window.addEventListener('mouseup', function() {
                isDragging = false;
                if (canvasWrapper) canvasWrapper.style.cursor = scale > 1 ? 'grab' : 'default';
            });
        }

        // PULSANTI ZOOM
        document.getElementById('pdf-zoom-in')?.addEventListener('click', function() {
            scale = Math.min(scale + 0.25, 3.5);
            updateTransform();
        });
        document.getElementById('pdf-zoom-out')?.addEventListener('click', function() {
            scale = Math.max(scale - 0.25, 1);
            updateTransform();
        });
        document.getElementById('pdf-zoom-reset')?.addEventListener('click', function() {
            resetTransform();
        });

        // FRECCE SCORRIMENTO VERTICALE (SU / GIÙ)
        document.getElementById('pdf-scroll-up')?.addEventListener('click', function () {
            canvasWrapper.scrollBy({ top: -200, behavior: 'smooth' });
        });
        document.getElementById('pdf-scroll-down')?.addEventListener('click', function () {
            canvasWrapper.scrollBy({ top: 200, behavior: 'smooth' });
        });

        // AUDIO FULLSCREEN RULER
        var activeFsAudioId = null;
        var fsPlayerWrapper = document.getElementById('pdf-fs-audio-player-wrapper');
        var fsAudioLabel   = document.getElementById('pdf-fs-audio-label');
        var fsAudioProgress= document.getElementById('pdf-fs-audio-progress');
        var fsAudioTime    = document.getElementById('pdf-fs-audio-time');
        var fsAudioButtonsContainer = document.getElementById('pdf-fs-audio-buttons');

        function formatTime(seconds) {
            if (isNaN(seconds)) return '0:00';
            var m = Math.floor(seconds / 60);
            var s = Math.floor(seconds % 60).toString().padStart(2, '0');
            return m + ':' + s;
        }

        if (fsAudioButtonsContainer && window.availableAudioParts && window.availableAudioParts.length > 0) {
            window.availableAudioParts.forEach(function (part) {
                var btn = document.createElement('button');
                btn.type = 'button';
                btn.className = 'pdf-fs-audio-btn';
                btn.setAttribute('data-audio-id', part.audioId);
                btn.setAttribute('title', 'Ascolta ' + part.label);
                btn.textContent = part.initial;

                btn.addEventListener('click', function () {
                    var audioEl = document.getElementById(part.audioId);
                    if (!audioEl) return;

                    activeFsAudioId = part.audioId;
                    if (fsAudioLabel) fsAudioLabel.textContent = part.initial;

                    if (audioEl.paused) {
                        document.querySelectorAll('audio').forEach(function (a) { a.pause(); });
                        audioEl.play();
                    } else {
                        audioEl.pause();
                    }
                });

                fsAudioButtonsContainer.appendChild(btn);
            });
        }

        if (fsAudioProgress) {
            fsAudioProgress.addEventListener('input', function () {
                if (!activeFsAudioId) return;
                var audioEl = document.getElementById(activeFsAudioId);
                if (audioEl && audioEl.duration) {
                    audioEl.currentTime = (fsAudioProgress.value / 100) * audioEl.duration;
                }
            });
        }

        window.updateFsRuler = function (audioId, audioEl) {
            if (fsPlayerWrapper) fsPlayerWrapper.style.display = 'flex';
            activeFsAudioId = audioId;

            if (window.availableAudioParts) {
                var matched = window.availableAudioParts.find(p => p.audioId === audioId);
                if (matched && fsAudioLabel) fsAudioLabel.textContent = matched.initial;
            }

            if (audioEl.duration && fsAudioProgress && fsAudioTime) {
                fsAudioProgress.value = (audioEl.currentTime / audioEl.duration) * 100;
                fsAudioTime.textContent = formatTime(audioEl.currentTime) + ' / ' + formatTime(audioEl.duration);
            }
        };

        // GESTIONE FULLSCREEN
        var fullScreenBtn = document.getElementById('pdf-fullscreen-btn');
        var pdfContainer = document.getElementById('pdf-viewer-container');

        if (fullScreenBtn && pdfContainer) {
            fullScreenBtn.addEventListener('click', function () {
                var isExpanded = pdfContainer.classList.toggle('pdf-fullscreen-mode');
                resetTransform();
                if (isExpanded) {
                    fullScreenBtn.innerHTML = '<span class="action-icon">❌</span> Chiudi';
                    document.body.style.overflow = 'hidden';
                } else {
                    fullScreenBtn.innerHTML = '<span class="action-icon">🔍</span> Ingrandisci';
                    document.body.style.overflow = '';
                }
                if (pageFlip) {
                    setTimeout(function() { 
                        pageFlip.update(); 
                        resetTransform();
                    }, 150);
                }
            });
        }
    }

    // CONTROLLI AUDIO TRACCE
    var buttons = document.querySelectorAll('.part-play-btn');

    buttons.forEach(function (btn) {
        var audioId = btn.getAttribute('data-audio');
        var audio   = document.getElementById(audioId);
        var icon    = btn.querySelector('.play-icon');

        if (!audio) return;

        btn.addEventListener('click', function () {
            if (audio.paused) {
                document.querySelectorAll('audio').forEach(function (a) {
                    if (a !== audio) a.pause();
                });
                audio.play();
            } else {
                audio.pause();
            }
        });

        function updateAudioStates(isPlaying) {
            var fsBtn = document.querySelector('.pdf-fs-audio-btn[data-audio-id="' + audioId + '"]');
            if (isPlaying) {
                icon.textContent = '⏸';
                btn.classList.add('is-playing');
                if (fsBtn) fsBtn.classList.add('is-playing');
            } else {
                icon.textContent = '▶';
                btn.classList.remove('is-playing');
                if (fsBtn) fsBtn.classList.remove('is-playing');
            }
        }

        audio.addEventListener('play',  function () { 
            updateAudioStates(true); 
            if (window.updateFsRuler) window.updateFsRuler(audioId, audio);
        });
        audio.addEventListener('pause', function () { updateAudioStates(false); });
        audio.addEventListener('ended', function () { updateAudioStates(false); });

        var progress  = document.querySelector('.part-progress[data-audio="' + audioId + '"]');
        var timeLabel = document.querySelector('.part-time[data-audio="' + audioId + '"]');

        function formatTime(seconds) {
            if (isNaN(seconds)) return '0:00';
            var m = Math.floor(seconds / 60);
            var s = Math.floor(seconds % 60).toString().padStart(2, '0');
            return m + ':' + s;
        }

        audio.addEventListener('loadedmetadata', function () {
            timeLabel.textContent = formatTime(audio.currentTime) + ' / ' + formatTime(audio.duration);
        });

        audio.addEventListener('timeupdate', function () {
            if (audio.duration) {
                progress.value = (audio.currentTime / audio.duration) * 100;
            }
            timeLabel.textContent = formatTime(audio.currentTime) + ' / ' + formatTime(audio.duration);

            if (window.updateFsRuler && !audio.paused) {
                window.updateFsRuler(audioId, audio);
            }
        });

        progress.addEventListener('input', function () {
            if (audio.duration) {
                audio.currentTime = (progress.value / 100) * audio.duration;
            }
        });
    });

    var ytButtons     = document.querySelectorAll('.yt-pointer-btn');
    var ytPlayer      = document.getElementById('yt-shared-player');
    var ytPlaceholder = document.getElementById('yt-shared-placeholder');

    ytButtons.forEach(function (btn) {
        btn.addEventListener('click', function () {
            var videoId = btn.getAttribute('data-yt-id');
            if (!ytPlayer || !videoId) return;

            ytPlayer.src = 'https://www.youtube.com/embed/' + videoId + '?autoplay=1';
            ytPlayer.style.display = 'block';
            if (ytPlaceholder) ytPlaceholder.style.display = 'none';

            ytButtons.forEach(function (b) { b.classList.remove('is-active'); });
            btn.classList.add('is-active');
        });
    });

    var pdfToggleBtn   = document.getElementById('pdf-toggle-btn');
    var pdfWrapper     = document.getElementById('pdf-wrapper');
    var pdfToggleLabel = document.getElementById('pdf-toggle-label');

    if (pdfToggleBtn && pdfWrapper) {
        pdfToggleBtn.addEventListener('click', function () {
            var isExpanded = pdfWrapper.classList.toggle('expanded');
            pdfToggleBtn.classList.toggle('is-expanded', isExpanded);
            pdfToggleBtn.setAttribute('aria-expanded', isExpanded ? 'true' : 'false');
            if (pdfToggleLabel) {
                pdfToggleLabel.textContent = isExpanded ? 'Comprimi spartito' : 'Espandi spartito';
            }
        });
    }
});
</script>

<style>
/* Contenitore PDF e Bordo Sottile */
.pdf-viewer-container {
    display: flex;
    flex-direction: column;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    overflow: hidden;
    background: #f8f9fa;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.04);
}

.pdf-toolbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5rem 0.8rem;
    background: #323639;
    color: #fff;
    font-size: 0.85rem;
    flex-wrap: wrap;
    gap: 0.5rem;
    z-index: 10;
}

.pdf-nav-controls, .pdf-zoom-controls, .pdf-actions {
    display: flex;
    align-items: center;
    gap: 0.4rem;
}

.pdf-fullscreen-audio-controls {
    display: none;
    align-items: center;
    gap: 0.8rem;
    flex: 1;
    justify-content: center;
    max-width: 500px;
}

.pdf-viewer-container.pdf-fullscreen-mode .pdf-fullscreen-audio-controls {
    display: flex;
}

.pdf-fs-audio-buttons {
    display: flex;
    align-items: center;
    gap: 0.4rem;
}

.pdf-fs-audio-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    border: 1px solid #2e7d32;
    background: #2e7d32;
    color: #ffffff;
    font-weight: bold;
    font-size: 0.85rem;
    cursor: pointer;
    transition: all 0.2s ease;
    flex-shrink: 0;
}

.pdf-fs-audio-btn:hover {
    background: #1b5e20;
    transform: scale(1.05);
}

.pdf-fs-audio-btn.is-playing {
    background: #ff9800;
    border-color: #e65100;
    box-shadow: 0 0 8px rgba(255, 152, 0, 0.6);
}

.pdf-fs-audio-player-wrapper {
    display: none;
    align-items: center;
    gap: 0.5rem;
    background: #232628;
    padding: 0.25rem 0.6rem;
    border-radius: 20px;
    border: 1px solid #444;
    flex: 1;
    min-width: 180px;
}

.pdf-fs-audio-label {
    font-weight: bold;
    color: #4caf50;
    font-size: 0.8rem;
}

.pdf-fs-audio-progress {
    flex: 1;
    height: 4px;
    accent-color: #4caf50;
    cursor: pointer;
}

.pdf-fs-audio-time {
    font-size: 0.75rem;
    color: #ccc;
    white-space: nowrap;
}

.pdf-scroll-controls {
    display: flex;
    gap: 0.3rem;
}

.pdf-btn, .pdf-btn-action {
    background: #4a4d51;
    color: #fff;
    border: 1px solid #666;
    border-radius: 4px;
    padding: 0.25rem 0.6rem;
    cursor: pointer;
    font-size: 0.8rem;
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
}
.pdf-btn:hover, .pdf-btn-action:hover { background: #606468; }

.pdf-download-circular-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 2.2rem;
    height: 2.2rem;
    border-radius: 50%;
    background: #2e7d32;
    color: #ffffff !important;
    text-decoration: none !important;
    font-size: 1rem;
    transition: background-color 0.2s ease, opacity 0.2s ease;
    flex-shrink: 0;
}
.pdf-download-circular-btn:hover {
    background: #1b5e20;
    opacity: 0.9;
}

.pdf-viewer-container.pdf-fullscreen-mode {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 99999;
    border-radius: 0;
    border: none;
    background: #323639;
    touch-action: none;
}

.pdf-canvas-wrapper {
    display: block;
    overflow: auto;
    padding: 1.5rem 1rem;
    background: #525659;
    min-height: 500px;
    height: 100%;
    max-height: 80vh;
    box-sizing: border-box;
    text-align: center;
}

.pdf-viewer-container.pdf-fullscreen-mode .pdf-canvas-wrapper {
    flex: 1;
    height: calc(100vh - 55px);
    max-height: calc(100vh - 55px);
    overflow: auto;
}

.pdf-canvas-wrapper.is-zoomed {
    cursor: grab;
}

#pdf-book {
    margin: 0 auto;
    display: inline-block;
    transform-origin: top center;
    transition: transform 0.15s ease-out;
}

.page-slide {
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
}
.page-slide canvas {
    width: 100%;
    height: 100%;
    image-rendering: -webkit-optimize-contrast;
    image-rendering: crisp-edges;
}

.part-audio-box { display: flex; align-items: center; gap: 0.6rem; margin-bottom: 0.4rem; }
.part-play-btn { 
    display: inline-flex; 
    align-items: center; 
    justify-content: center; 
    width: 2.2rem; 
    height: 2.2rem; 
    border-radius: 50%; 
    border: none; 
    background: #2e7d32; 
    color: #fff; 
    cursor: pointer; 
    font-size: 1rem; 
    flex-shrink: 0; 
}
.part-play-btn.is-playing { background: #1b5e20; }
.part-play-btn:hover { opacity: 0.85; }
.part-info { display: flex; flex-direction: column; flex: 1; min-width: 0; }
.part-progress-row { display: flex; align-items: center; gap: 0.5rem; margin-top: 0.2rem; }
.part-progress { flex: 1; height: 4px; accent-color: #2e7d32; cursor: pointer; }
.part-time { font-size: 0.75rem; color: #666; white-space: nowrap; min-width: 5.5em; text-align: right; }
.yt-pointer-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 0.4rem; }
.yt-pointer-btn { display: inline-flex; align-items: center; gap: 0.4rem; padding: 0.3rem 0.6rem; border: 1px solid #ddd; border-radius: 999px; background: #fff; cursor: pointer; font-size: 0.85rem; width: 100%; text-align: left; }
.yt-pointer-icon { display: inline-flex; width: 1.8rem; height: 1.3rem; flex-shrink: 0; }
.yt-pointer-icon svg { width: 100%; height: 100%; }
.yt-pointer-label { flex: 1; font-weight: 500; }
.yt-pointer-btn:hover { background: #f7f7f7; }
.yt-pointer-btn.is-active { border-color: #f00; background: #fff5f5; }
.yt-shared-player-wrapper { position: relative; width: 100%; padding-top: 56.25%; background: #111; border-radius: 6px; overflow: hidden; }
.yt-shared-player-wrapper iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0; }
.yt-shared-placeholder { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); color: #ccc; font-size: 0.9rem; margin: 0; text-align: center; width: 80%; }
.right-column { display: flex; flex-direction: column; gap: 0.75rem; }
.back-to-search-wrapper { margin-bottom: 0.75rem; }
.back-to-search-btn { display: inline-flex; align-items: center; gap: 0.4rem; padding: 0.4rem 0.9rem; border: 1px solid #ccc; border-radius: 999px; background: #fff; cursor: pointer; font-size: 0.9rem; color: #333; text-decoration: none; }
.back-to-search-btn:hover { background: #f2f2f2; }
.back-icon { font-size: 1rem; }
.pdf-toggle-btn { display: none; align-items: center; gap: 0.4rem; padding: 0.4rem 0.9rem; margin-bottom: 0.5rem; border: 1px solid #ccc; border-radius: 999px; background: #fff; cursor: pointer; font-size: 0.9rem; color: #333; }
.pdf-toggle-btn:hover { background: #f2f2f2; }
.pdf-toggle-icon { display: inline-block; transition: transform 0.25s ease; }
.pdf-toggle-btn.is-expanded .pdf-toggle-icon { transform: rotate(180deg); }

@media (max-width: 768px) {
    .pdf-toggle-btn { display: inline-flex; }
    .pdf-wrapper { max-height: 220px; overflow: hidden; transition: max-height 0.3s ease; }
    .pdf-wrapper.expanded { max-height: 2000px; }
}
</style>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")