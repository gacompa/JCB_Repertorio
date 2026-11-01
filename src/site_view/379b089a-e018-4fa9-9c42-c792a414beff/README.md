### JCB! Site View
# Locations list (locations_list)

List of locations

## HTML:
```html
<form action="<?php echo Route::_('index.php?option=com_bookings'); ?>" method="post" name="adminForm" id="adminForm">
<?php echo $this->toolbar->render(); ?>
<?php echo LayoutHelper::render('rowslocations', []); ?>

<!-- Put here the route for the one-location view, i.e. index.php/booking/locations-single -->
<?php $one_location_path = "index.php/booking/location-single"; ?>

<table class="uk-table uk-table-hover">
    <caption><?php echo Text::_('LOCATIONS'); ?></caption>
    <thead>
        <tr>
        <th><?php echo Text::_('COM_BOOKINGS_IMAGE'); ?></th>
        <th><?php echo Text::_('COM_BOOKINGS_NAME'); ?></th>
        <th><?php echo Text::_('COM_BOOKINGS_LOCATION'); ?></th>
        <th><?php echo Text::_('COM_BOOKINGS_ALTITUDE'); ?></th>
        <th><?php echo Text::_('COM_BOOKINGS_IS_STOP'); ?></th>
        <th><?php echo Text::_('COM_BOOKINGS_IS_BASE'); ?></th>
        </tr>
    </thead>
    <tbody>
        <?php foreach ($this->items as $item): ?>
        <tr>
            <td><img src="<?php echo $this->escape($item->image); ?>" style="width: 100px; height: auto;"> </td>
            <td><b><?php echo "<a href=\"" . $this->escape($one_location_path) . "?id=" . (int)$item->id . "\" > " . $this->escape($item->name) . " </a>"; ?></b><br/><?php echo $this->escape($item->description); ?></td>
            <td><?php echo $this->escape($item->location); ?></td>
            <td><?php echo $this->escape($item->altitude); ?></td>
            <td align="center"><?php if ($item->is_stop) {
              // check icon by Free Icons (https://free-icons.github.io/free-icons/)
              echo '<svg xmlns="http://www.w3.org/2000/svg" height="1em" fill="currentColor" viewBox="0 0 512 512">
              <path d="M 501.7142857142857 83.42857142857143 Q 512 94.85714285714286 512 109.71428571428571 L 512 109.71428571428571 L 512 109.71428571428571 Q 512 124.57142857142857 501.7142857142857 136 L 209.14285714285714 428.57142857142856 L 209.14285714285714 428.57142857142856 Q 197.71428571428572 438.85714285714283 182.85714285714286 438.85714285714283 Q 168 438.85714285714283 156.57142857142858 428.57142857142856 L 10.285714285714286 282.2857142857143 L 10.285714285714286 282.2857142857143 Q 0 270.85714285714283 0 256 Q 0 241.14285714285714 10.285714285714286 229.71428571428572 Q 21.714285714285715 219.42857142857142 36.57142857142857 219.42857142857142 Q 51.42857142857143 219.42857142857142 62.857142857142854 229.71428571428572 L 182.85714285714286 350.85714285714283 L 182.85714285714286 350.85714285714283 L 449.14285714285717 83.42857142857143 L 449.14285714285717 83.42857142857143 Q 460.57142857142856 73.14285714285714 475.42857142857144 73.14285714285714 Q 490.2857142857143 73.14285714285714 501.7142857142857 83.42857142857143 L 501.7142857142857 83.42857142857143 Z"/>
              </svg>';}
            else {
              //xmark icon by Free Icons (https://free-icons.github.io/free-icons/)
              echo '<svg xmlns="http://www.w3.org/2000/svg" height="1em" fill="currentColor" viewBox="0 0 512 512">
              <path d="M 497.6 88 Q 512 72 512 51.2 L 512 51.2 L 512 51.2 Q 512 30.4 497.6 14.4 Q 481.6 0 460.8 0 Q 440 0 424 14.4 L 256 184 L 256 184 L 88 14.4 L 88 14.4 Q 72 0 51.2 0 Q 30.4 0 14.4 14.4 Q 0 30.4 0 51.2 Q 0 72 14.4 88 L 184 256 L 184 256 L 14.4 424 L 14.4 424 Q 0 440 0 460.8 Q 0 481.6 14.4 497.6 Q 30.4 512 51.2 512 Q 72 512 88 497.6 L 256 328 L 256 328 L 424 497.6 L 424 497.6 Q 440 512 460.8 512 Q 481.6 512 497.6 497.6 Q 512 481.6 512 460.8 Q 512 440 497.6 424 L 328 256 L 328 256 L 497.6 88 L 497.6 88 Z"/>
              </svg>';
            }; ?></td>            
            <td align="center"><?php if ($item->is_base) {
              // check icon by Free Icons (https://free-icons.github.io/free-icons/)
              echo '<svg xmlns="http://www.w3.org/2000/svg" height="1em" fill="currentColor" viewBox="0 0 512 512">
              <path d="M 501.7142857142857 83.42857142857143 Q 512 94.85714285714286 512 109.71428571428571 L 512 109.71428571428571 L 512 109.71428571428571 Q 512 124.57142857142857 501.7142857142857 136 L 209.14285714285714 428.57142857142856 L 209.14285714285714 428.57142857142856 Q 197.71428571428572 438.85714285714283 182.85714285714286 438.85714285714283 Q 168 438.85714285714283 156.57142857142858 428.57142857142856 L 10.285714285714286 282.2857142857143 L 10.285714285714286 282.2857142857143 Q 0 270.85714285714283 0 256 Q 0 241.14285714285714 10.285714285714286 229.71428571428572 Q 21.714285714285715 219.42857142857142 36.57142857142857 219.42857142857142 Q 51.42857142857143 219.42857142857142 62.857142857142854 229.71428571428572 L 182.85714285714286 350.85714285714283 L 182.85714285714286 350.85714285714283 L 449.14285714285717 83.42857142857143 L 449.14285714285717 83.42857142857143 Q 460.57142857142856 73.14285714285714 475.42857142857144 73.14285714285714 Q 490.2857142857143 73.14285714285714 501.7142857142857 83.42857142857143 L 501.7142857142857 83.42857142857143 Z"/>
              </svg>';}
            else {
              //xmark icon by Free Icons (https://free-icons.github.io/free-icons/)
              echo '<svg xmlns="http://www.w3.org/2000/svg" height="1em" fill="currentColor" viewBox="0 0 512 512">
              <path d="M 497.6 88 Q 512 72 512 51.2 L 512 51.2 L 512 51.2 Q 512 30.4 497.6 14.4 Q 481.6 0 460.8 0 Q 440 0 424 14.4 L 256 184 L 256 184 L 88 14.4 L 88 14.4 Q 72 0 51.2 0 Q 30.4 0 14.4 14.4 Q 0 30.4 0 51.2 Q 0 72 14.4 88 L 184 256 L 184 256 L 14.4 424 L 14.4 424 Q 0 440 0 460.8 Q 0 481.6 14.4 497.6 Q 30.4 512 51.2 512 Q 72 512 88 497.6 L 256 328 L 256 328 L 424 497.6 L 424 497.6 Q 440 512 460.8 512 Q 481.6 512 497.6 497.6 Q 512 481.6 512 460.8 Q 512 440 497.6 424 L 328 256 L 328 256 L 497.6 88 L 497.6 88 Z"/>
              </svg>';
            }; ?></td>
        </tr>
        <?php endforeach; ?>
    </tbody>
</table>

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
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")