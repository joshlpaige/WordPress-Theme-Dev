# Building a WordPress Theme From Scratch

Finished example WordPress app featuring a custom built theme. Instructions provided are specific to using Mac ecosystem. I tried to provide relevant links to explanations for Windows users, but many setup steps will differ. However all PHP, HTML, CSS code for creating the theme is platform independant and will be the same for both Mac and Windows users.

## Setup Local Server and Install WordPress

1. Download and install a code editor (if necessary) such as [Atom](https://atom.io).
2. Download an app to spin up a local PHP Apache Server such as [MAMP](https://www.mamp.info/en/) for Mac or [WAMP](http://www.wampserver.com/en/) for Windows.
3. Download Wordpress from [wordpress.org](https://wordpress.org/)
4. Open MAMP (or WAMP) App and click Start Servers. Please note: The following steps assume MAMP on Mac.
5. When your browser opens under MySQL heading click the phpMyAdmin link.
6. After logging into phpMyAdmin in the left hand navigation panel click new and under Create Database, name your database something, I called mine `wp_dev_db` (make sure there are no spaces in the name you choose). Then click Create. Then in the top navigation click Start. Let's leave this browser tab open and refer to the MySQL database details from here later on.
7. Move into the downloaded WordPress folder using Terminal $ `cd ~/Downloads/wordpress` or optionally you can rename the folder first if you like, I renamed mine building-a-wordpress-theme-from-scratch and moved it to my Development folder, I then ran the command $ `cd ~/Development/building-a-wordpress-theme-from-scratch`.
8. Rename __wp-config-sample.php__ to __wp-config.php__ with $ `mv wp-config-sample.php wp-config.php`.
9. Open the site in your code editor I'm using [Atom](https://atom.io) with the command $ `atom .`
10. Open __wp-config.php__ and set the database details to point to your local server the following are the instructions for MAMP on Mac directions for Windows may vary at this step so if your own windows instead refer to the instructions for setting up and connecting to databases on [WAMP](http://forum.wampserver.com/list.php?2). Here are the MAMP specific code using the details from the MAMP page we left open in our browser:  
```php
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wp_dev_db');

/** MySQL database username */
define('DB_USER', 'root');

/** MySQL database password */
define('DB_PASSWORD', 'root');

/** MySQL hostname */
define('DB_HOST', 'localhost:8889');

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');
```  
11. Then visit [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/) and copy the generated keys and paste them into your __wp-config.php__ file under the section labeled Authentication Unique Keys and Salts.
12. Also in __wp-config.php__ set debug from false to true `define('WP_DEBUG', true);`.
13. Then back to MAMP (WAMP instructions instead see their docs or forum) App click Stop Servers. Then click Preferences.
14. Click Web Server tab and set the document root to point to the folder for your WP (WordPress) Site. On Mac in MAMP you click the folder icon with three dots on it to browse for the root folder. It is important that it is set to the folder that contains the wp-config.php file. than click OK. Then click to Start Servers again.
15. In your browser set the URL to `http://localhost` if everything was done correctly this should forward to `http://localhost/wp-admin/install.php`.
16. Select your desired install language and click Continue.
17. On the next page set a Site Title I choose `WP Theme From Scratch`. Also set a username typically this is `admin`. Then set a password you will remember. Also set an admin email. Then click Install WordPress button.
18. On the next page click Log In and use your credentials to login to your site. If all goes well you should see the admin dashboard for your site.
19. Run any updates it suggests under Dashboard > updates

## Creating A Custom Theme

1. In Terminal (or in code editor) head to the theme folder at __wp-content/themes/__ $ `cd wp-content/themes`.
2. Create a new theme folder using Terminal $ `mkdir custom-theme` or via Atom by right clicking on the themes folder and select create new folder. Note: you can name your theme folder anything you like I choose custom-theme as a generic name for this example.
3. Inside __custom-theme__ create a __css__ folder $ `mkdir custom-theme/css` and also create a _js__ folder $ `mkdir custom-theme/js`.
4. Move into your custom theme folder $ `cd custom-theme` and create three files __index.php__ and __css/style.css__ and __js/app.js__$ `touch index.php css/style.css js/app.js`.
5. In __css/style.css__ in your code editor add the following code:
```css
/*
Theme Name: Custom Theme
Author: Jonathan Grover
Description: Example Theme from Github Repo (https://github.com/jongrover/building-a-wordpress-theme-from-scratch)
Version: 0.0.1
Tags: bootstrap
*/

h1 {
  color: red;
}
```  
Note: You can change any of the settings in the CSS comment at the top as you wish these will eventually appear in your admin dashboard view under Appearance>Themes as details for each theme.

6. In __js/app.js__ in your code editor add the following code:  
```javascript
console.log('Hello from your theme!');
```
7. In __index.php__ in your code editor put the code:  
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title><?php echo get_bloginfo('name'); ?></title>
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/style.css">
</head>
<body>
  <h1><?php echo get_bloginfo('name'); ?></h1>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/app.js"></script>
</body>
</html>
```  
Note that in our title element we put `<title><?php echo get_bloginfo('name'); ?></title>` this uses the get_bloginfo() function to print the name of our site that we first set when we installed WordPress. We also printed this site name in the heading inside our page body. We used this function again to link to our CSS and JS files by making use of `<?php echo get_bloginfo('template_directory'); ?>` which was essential for printing the correct file path to our assets. For full details of what can be done with this function take a look at the [docs here](https://developer.wordpress.org/reference/functions/get_bloginfo/).

8. Now head back to the admin dashboard in your browser and click Appearance>Themes
9. Under Custom Theme (or whatever your theme name you set was) click Activate.
10. Then visit `localhost` in your browser to see your site. It should say your site title in an h1 element and the loaded CSS should style the text color as red. Additionally if you view the JavaScript console using the Developer Tools you should see it print "Hello from your theme!".
11. Now that our theme is working let's delete the previous theme folders (you don't have to do this, but I won't be using the default themes any longer and they are just taking up space.) I'll get rid of __twentyseventeen__, __twentysixteen__, and __twentyfifteen__.

## Adding Bootstrap

1. Start by downloading [Bootstrap](http://getbootstrap.com/docs/4.0/getting-started/download/).
2. Next download [jQuery](https://code.jquery.com/jquery-3.2.1.slim.min.js) a Bootstrap dependency.
3. Also download [Popper](https://gist.github.com/FezVrasta/16c5d5e5ff1211922ddcf090c8454d74/archive/9372bdf66f7d899a5daaf0ff06ff89be92561c83.zip) another Bootstrap dependency.
4. After all downloads finish unzip them and move all CSS into your projects __css__ folder and move all JS files into your __js__ folder.
5. Now let's link to these new files for Bootstrap in our __index.php__ file in the root of our theme folder __custom-theme/index.php__. Here We'll link to the files the same way we linked to our __style.css__ and __app.js__.  
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title><?php echo get_bloginfo('name'); ?></title>
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/bootstrap.min.css">
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/style.css">
</head>
<body>
  <h1><?php echo get_bloginfo('name'); ?></h1>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/jquery-3.2.1.slim.min.js"></script>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/popper.min.js"></script>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/bootstrap.min.js"></script>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/app.js"></script>
</body>
</html>
```
6. Save all files and head to localhost in your browser, open the Network tab in the Developer  Tools and refresh the page. You should see Bootstrap CSS, JS, jQuery, and Popper are all correctly loading.

## Dividing Page Layout

1. Let's start by building our layout in __custom-theme/index.php__ and later we'll break it into separate PHP files. Here is my layout code:  
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title><?php echo get_bloginfo('name'); ?></title>
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/bootstrap.min.css">
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/style.css">
</head>
<body>

<header>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand" href="<?php echo get_bloginfo( 'wpurl' ); ?>"><?php echo get_bloginfo('name'); ?></a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <a class="nav-link" href="#">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Contact</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Blog</a>
          </li>
        </ul>
      </div>
    </div><!-- .container -->
  </nav>
</header>

  <main>
    <div class="container">
      <div class="row">

        <section class="col-md-9">
          <div class="jumbotron">
            <h1 class="display-3">Welcome</h1>
            <p class="lead">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
            <hr class="my-4">
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
          </div>
        </section>

        <aside class="col-md-3">
          <ul class="nav flex-column">
            <li class="nav-item">
              <a class="nav-link active" href="#">Active</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Link</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Link</a>
            </li>
            <li class="nav-item">
              <a class="nav-link disabled" href="#">Disabled</a>
            </li>
          </ul>
        </aside>

      </div><!-- .row -->
    </div><!-- .container -->
  </main>

  <footer>
    <div class="container">
      <div class="row">
        <div class="col">
          <small>&copy; 2017 Jonathan Grover. All Rights Reserved.</small>
        </div><!-- .col -->
      </div><!-- .row -->
    </div><!-- .container -->
  </footer>

  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/jquery-3.2.1.slim.min.js"></script>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/popper.min.js"></script>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/bootstrap.min.js"></script>
  <script src="<?php echo get_bloginfo('template_directory'); ?>/js/app.js"></script>
</body>
</html>
```
2. Then in __custom-theme/css/style.css__ add the code:  
```css
header {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;
}

main {
  margin-top: 80px;
}

.navbar-light .navbar-brand.active, .navbar-light .navbar-nav .nav-link.active, .nav .nav-link.active {
  color: darkblue;
}
```
3. Save all pages and refresh in the browser and you should see an updated page layout including a navigation bar, welcome page and sidebar as well as a footer.
4. Now create the files: __custom-theme/header.php__, __custom-theme/content.php__, __custom-theme/sidebar.php__, and __custom-theme/footer.php__.
5. In __index.php__ add the function call `<?php wp_head(); ?>` just before the closing `</head>` tag.  
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title><?php echo get_bloginfo('name'); ?></title>
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/bootstrap.min.css">
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/style.css">
  <?php wp_head(); ?>
</head>
<body>
```
6. In __index.php__ copy everything from `<!doctype>` all the way down to the closing `</header>` and paste it into __header.php__.  
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title><?php echo get_bloginfo('name'); ?></title>
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/bootstrap.min.css">
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/style.css">
  <?php wp_head() ?>
</head>
<body>
<header>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand" href="<?php echo get_bloginfo( 'wpurl' ); ?>"><?php echo get_bloginfo('name'); ?></a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <a class="nav-link" href="#">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Contact</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Blog</a>
          </li>
        </ul>
      </div>
    </div><!-- .container -->
  </nav>
</header>
```  
Notice I also added to the code above `<?php echo get_bloginfo( 'wpurl' ); ?>` into the href attribute for the navbar-brand link that shows our site title. This way when the user clicks our site title in the navbar it will head back to our site root (home page).

7. Back in __index.php__ remove that code you copied into __header.php__ replacing it with `<?php get_header(); ?>`.
8. In __index.php__ add the function call `<?php wp_footer(); ?>` just before the closing `</body>` tag.  
```php
    <script src="<?php echo get_bloginfo('template_directory'); ?>/js/jquery-3.2.1.slim.min.js"></script>
    <script src="<?php echo get_bloginfo('template_directory'); ?>/js/popper.min.js"></script>
    <script src="<?php echo get_bloginfo('template_directory'); ?>/js/bootstrap.min.js"></script>
    <script src="<?php echo get_bloginfo('template_directory'); ?>/js/app.js"></script>
    <?php wp_footer(); ?>
</body>
</html>
```
9. In __index.php__ copy everything from `<footer>` all the way down to the closing `</html>` and paste it into __footer.php__.  
```php
<footer>
  <div class="container">
    <div class="row">
      <div class="col">
        <small>&copy; 2017 Jonathan Grover. All Rights Reserved.</small>
      </div><!-- .col -->
    </div><!-- .row -->
  </div><!-- .container -->
</footer>

<script src="<?php echo get_bloginfo('template_directory'); ?>/js/jquery-3.2.1.slim.min.js"></script>
<script src="<?php echo get_bloginfo('template_directory'); ?>/js/popper.min.js"></script>
<script src="<?php echo get_bloginfo('template_directory'); ?>/js/bootstrap.min.js"></script>
<script src="<?php echo get_bloginfo('template_directory'); ?>/js/app.js"></script>
<?php wp_footer(); ?>
</body>
</html>
```
10. Back in __index.php__ remove that code you copied into __footer.php__ replacing it with `<?php get_footer(); ?>`.
11. In __index.php__ delete all the content inside of `<section>` element and replace with this:    
```php
<section class="col-md-9">
  <?php if ( have_posts() ) : while ( have_posts() ) : the_post();
    get_template_part( 'content', get_post_format() );
  endwhile; endif; ?>
</section>
```  
This will check if there are posts and if there are, it will loop over them and display them in this space.
12. Now in __content.php__ add the following skeleton for each blog post:  
```php
<article id="post-<?php the_ID(); ?>">
	<h2><a href="<?php the_permalink(); ?>" rel="bookmark"><?php the_title(); ?></a></h2>
	<small><?php the_date(); ?> by <?php the_author(); ?></small>
  <?php the_content(); ?>
</article>
```
13. In __index.php__ copy all the code from `<aside class="col-md-3">` to the closing `</aside>` and paste it into __sidebar.php__.  
```php
<aside class="col-md-3">
  <h4>Archives</h4>
  <ul class="nav flex-column">
    <?php wp_get_archives( 'type=monthly' ); ?>
  </ul>
</aside>
```  
Here we also removed all the `<li>` elements and are replacing it with dynamic code `<?php wp_get_archives( 'type=monthly' ); ?>` as well as a few `<h4>` to title the Archives list.

14. Back in __index.php__ remove that code you copied into __sidebar.php__ replacing it with `<?php get_sidebar(); ?>`.
15. After refreshing the page in the browser it should still look the same but the welcome box is now showing the Hello World post that WordPress creates for us when we first install it. Our sidebar now shows the about description and Archive month list.

## Custom Menu Locations

1. Create a __functions.php__ file in the root directory of your theme $ `touch functions.php`.
2. Inside __functions.php__ add the following code to register a new menu locations:  
```php
<?php
function register_my_menus() {
  register_nav_menus(array(
		'header-menu' => 'Header Menu'
	));
}
add_action( 'init', 'register_my_menus' );
?>
```
3. Add the first Menu Location in the __header.php__ by replacing the dummy `<li>` with the function `wp_nav_menu(array('theme_location' => 'header-menu'))` like so:  
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title><?php echo get_bloginfo('name'); ?></title>
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/bootstrap.min.css">
  <link rel="stylesheet" href="<?php echo get_bloginfo('template_directory'); ?>/css/style.css">
  <?php wp_head() ?>
</head>
<body>
  <header>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand active" href="<?php echo get_bloginfo( 'wpurl' ); ?>"><?php echo get_bloginfo('name'); ?></a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <?php wp_nav_menu(array('theme_location' => 'header-menu')); ?>
          </ul>
        </div>
      </div><!-- .container -->
    </nav>
  </header>
```
4. Then in __css/style.css__ add the following code to re-style the links:  
```css
.menu {
  list-style: none;
  padding-left: 0;
}

.menu-item a {
    display: inline-block;
    padding: .5rem 1rem;
}

.navbar-nav .menu-item a {
    padding-right: 0;
    padding-left: 0;
}

.navbar-light .navbar-nav .menu-item a {
    color: rgba(0,0,0,.5);
}

.navbar-light .navbar-nav .menu-item a:hover {
    color: rgba(0,0,0,.7);
    text-decoration: none;
}

.navbar-light .navbar-brand.active, .navbar-light .navbar-nav .menu-item a.active, .nav .menu-item a.active {
  color: darkblue;
}

@media (min-width: 992px) {
  .menu-item {
    display: inline-block;
  }
  .navbar-expand-lg .navbar-nav .menu-item a {
    padding-right: .5rem;
    padding-left: .5rem;
  }
}
```
5. Next in the browser head into the Admin dashboard and build a menu by going to Appearance>Menus and create a new menu assigning its location to Header Menu. Add your pages as desired. I created four pages: Home, About, Contact, and Blog. Save the Menu and refresh the browser page at localhost and your Header Navigation should appear.

## Creating Pages Layout

1. Next create a __custome-theme/page.php__ file in the themes root folder allowing Pages to have a different layout From blog Post pages. For instance we will have only single columns in our Pages vs 2 columns as we see now in our Posts. In __page.php__ insert this code:  
```php
<?php get_header(); ?>

  <main>
    <div class="container">

      <div class="row">
        <section class="col">
          <?php while ( have_posts() ) : the_post(); ?>

            <article>
              <h2><?php the_title(); ?></h2>
              <?php the_content(); ?>
            </article>

    			<?php endwhile; ?>
        </section>
      </div><!-- .row -->
    </div><!-- .container -->
  </main>

<?php get_footer(); ?>
```
2. Now links in the Header Menu should navigate to each page when clicked.

## Set Static Homepage.

1. Previously I created four pages: Home, About, Contact, and Blog; now we would like to set a static home page and have our blog posts show up under the blog page instead. In the browser in the Admin Dashboard view head to Settings>Reading and under _Front page displays_ heading select the radio button for _static page_, and under _Front page_ I will select _Home_ a page I created previously. Under _Posts page_ I will select _Blog_ a blank page I created previously.

## Create Custom Wiget Areas

1. In __functions.php__ add the following code:  
```php
function register_my_wigets() {
  register_sidebar(array(
    'name' => 'Sidebar',
    'id' => 'sidebar-1',
		'description'   => 'Custom Sidebar Widget',
    'before_widget' => '<div class="sidebar-widget">',
    'after_widget' => '</div>',
    'before_title' => '<h4>',
    'after_title' => '</h4>',
  ));
}
add_action( 'widgets_init', 'register_my_wigets' );
```
2. In __sidebar.php__ remove the code inside `<aside>`...`</aside>` and add the following code in its place:  
```php
<aside class="col-md-3">
  <?php if (is_active_sidebar('sidebar-1')) {
    dynamic_sidebar('sidebar-1');
  } ?>
</aside>
```
3. Now in the browser head to Appearance>Widgets and drag a Wiget such as Archives to the new widget area labeled Sidebar. Now in the user facing view of the side you should see the Wiget location appearing at in the sidebar of the blog link.

## ...

1. ...
