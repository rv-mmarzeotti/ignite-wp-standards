# Ignite WordPress Standards

Some basic standards to avoid conflicts with modules used in different order and on different pages.

### Best Practices

This repo uses `tabs` instead of `spaces`. Tabs are set to the size of 4 spaces. This is defined in the EditorConfig included in the repo. You may override this in your editor if you like.

### PHP

When working with HTML in a PHP document, the HTML should be formatted as such whenever possible.

Good:

```PHP
<?php
if ( is_author() ) { ?>
    <p>You are the author.</p>
<?php } ?>
```

Bad:

```PHP
<?php
if ( is_author() ) {
    echo '<p>You are the author.</p>';
} ?>
```

PHP should be properly spaced based on the WordPress coding standards.

Good:

```PHP
<?php
$author_id = get_the_author();

function get_author_name( $author_id ) {
    $author_name = get_the_author_meta( 'first_name', $author_id );
    return $author_name;
}

$author = get_author_name( $author_id );

if ( ! empty( $author_id ) && ! empty( $author ) ) { ?>
    <p>The author is <?php echo $author; ?>.</p>
<?php } ?>
```

Bad:

```PHP
<?php
$author_id = get_the_author();

function get_author_name($author_id) {
    $author_name = get_the_author_meta('first_name',$author_id);
    return $author_name;
}

$author = get_author_name($author_id);

if (!empty($author_id) && !empty($author)) { ?>
    <p>The author is <?php echo $author; ?>.</p>
<?php } ?>
```

PHP functions and variables should be spelled out and underscore separated.

Good:

```PHP
<?php
$author_id = get_the_author();

function get_author_name( $author_id ) {
    $author_name = get_the_author_meta( 'first_name', $author_id );
    return $author_name;
}
?>
```

Bad:

```PHP
<?php
$authId = get_the_author();

function getAuthName( $authId ) {
    $authName = get_the_author_meta( 'first_name', $authId );
    return $authName;
}
?>
```

### JavaScript

Javascript follows a lot of the same rules as PHP with a few exceptions. 

Spacing and quote usage should remain the same. 

Variable and function names should be camelCase.

### SCSS

SCSS should always use single quotes unless double quotes are explicitly necessary.

Vertical spacing should be used to separate sets of attributes.

Good:

```SCSS
.class {
    att: 1;

    @media screen and (min-width: 1025) {
        att: 2;
    }
}
```

Bad:

```SCSS
.class {
    att: 1;
    @media screen and (min-width: 1025) {
        att: 2;
    }
}
```

Media queries should be spcified on the item they modify and should not nest items. The media query should be the very first nested item outside of individual attributes.

Good:

```SCSS
.class {
    att: 1;

    @media screen and (min-width: 1025) {
        att: 2;
    }

    .class-2 {
        att: 3;

        @media screen and (min-width: 1025) {
            att: 4;
        }
    }
}
```

Bad:

```SCSS
.class {
    att: 1;

    @media screen and (min-width: 1025) {
        att: 2;

        .class-2 {
            att: 4;
        }
    }

    .class-2 {
        att: 3;
    }
}
```

## Variables

All variables should follow BEM naming convention. 

Fonts should be based on the base font name.

```scss
$font__roboto: 'roboto';
$font__roboto-condensed: 'roboto-condensed';
```

Colors should be named using [Name That Color](http://chir.ag/projects/name-that-color/) to avoid names like `$color__grey-light-2`.

```scss
$color__cornflower-blue: #6195ED;
```

## Padding, Margins and Borders

Padding, margins and borders should be kept to the bottom and right when used to create space between elements. The exception to this rule is if the module has a background color or image and needs padding on the top to match the design. This ensures that stacked modules have the correct spacing between them and could be placed in any order. Often times our modules will have transparent backgrounds with uniform spacing between them or very specific spacing based on the individual module. Complete buy in on the team will ensure that everyone knows where padding and margin will be located no matter the implementation and can make QA edits without worrying it breaks other areas of the design.

### Example

In a recent edit on FurnaceCompare.com, the dev team was tasked with adding a border above the "Reviews Overview" section on [product pages](https://www.furnacecompare.com/furnaces/products/trane/xv95/). Doing so exactly the way the request was posed would cause a double border on [brand pages](https://www.furnacecompare.com/furnaces/products/trane/) that also use the same "Reviews Overview" module. Buy in on borders only on the bottom of elements would prevent that from happening even if the developer making the change was unaware of the use of the module on brand pages.

##### Product Pages

![Product Pages](/images/example-1-1.png)

##### Brand Pages

![Brand Pages](/images/example-1-2.png)

## Module Style and Structure

[BEM](http://getbem.com/) should be used for all style classes in markup. The idea here is that we can be specific, while still being able to override wherever we might need to.

A *BLOCK* is anything that would be styled as its own individual thing. Maybe it can appear in multiple areas with similar styles like a post, or it might be a full section like a latest posts or resources section on the home page.

An *ELEMENT* is anything that might be used to make up a block. A post block might be made up of a title, image, category, content, and a link element. It might have more or it might have less. The elements that make it up might depend on where it is being displayed.

A *MODIFIER* is used when a block is similar to its base set of styles, but has some slight differences. It can be applied to a block or an element to modify the entire block or just a small piece of it.

Thinking about elements in this manner will allow us to move or reuse things throughout the site with relatively low lift. If we have a blog page, and then we want to add a sidebar that contains recent posts, we can reuse the markup, maybe remove anything we do not want to use like the category or the excerpt, and possibly only need to add a modifier to the post block to override font sizes. That modified style could and might in turn be used anywhere else we want that smaller implementation, therefore the modifier probably shouldnt be --sidebar, but maybe --small or --simple.

### Example

A resources section containing an intro, three blog posts, and a button to the blog page might be structured as follows.

```html
<section class="resources">
    <div class="container">
        <div class="resources__intro">
            <h2>Lorem ipsum dolor sit amet?</h2>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        </div>
        <div class="resources__post-container">
            <div class="container">
                <div clas="post post--featured">
                    <img class="post__image" src="#" alt="Lorem ipsum dolor sit amet" />
                    <div class="post__content">
                        <h3 class="post__title">Lorem ipsum dolor sit amet</h3>
                        <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                        <a class="post__link">Read more</a>
                    </div>
                </div>
                <div clas="post">
                    <img class="post__image" src="#" alt="Lorem ipsum dolor sit amet" />
                    <div class="post__content">
                        <h3 class="post__title">Lorem ipsum dolor sit amet</h3>
                        <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                        <a class="post__link">Read more</a>
                    </div>
                </div>
                <div clas="post">
                    <img class="post__image" src="#" alt="Lorem ipsum dolor sit amet" />
                    <div class="post__content">
                        <a class="post__category" href="#">Lorem</a>
                        <h3 class="post__title">Lorem ipsum dolor sit amet</h3>
                        <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                        <a class="post__link" href="#">Read more</a>
                    </div>
                </div>
            </div>
        </div>
        <div class="resources__button-container">
            <a class="button" href="#">Lorem ipsum</a>
        </div>
    </div>
</section>
```

In terms of BEM, there are a couple things going on here. There are:


* 2 blocks - resources and post each with different elements
    * resources
        * intro
        * post-container
        * button-container
    * post
        * image
        * content
        * category
        * title
        * link
* 2 utility/helper classes
    * container
    * button

The resources block is likely pretty specific, but the module can easily be used across different pages and templates. The post block is repeatable in other areas of the site and styles will only need to be defined once. The resources block can modify the post block by being more specific without affecting posts anywhere else.

#### _post.scss

```scss
.post {
    // post block styles

    &__title {
        // post title element styles
    }

    // additional post elements
}
```

#### _resources.scss

```scss
.resources {
    // resource blocks elements and modifiers

    .post {
        // post block styles

        &__title {
            // post title element styles
        }

        // additional post elements
    }
}
```

In terms of general naming standards, all class names should be as generic as possible. There should be consistency in element names as well. One block should not use __heading while another uses __title without good reason. If a post block has 2 different title styles, it should use a modifier rather than a different element name. It could be argued that a section has a heading, but a post has a title.

## Repeatable Components

Throughout a design we will encounter similar components across the various modules. Common areas to look are similar intro sections where base typography styles are modified to either use a different margin or font size than it would in long form content. These sections should be identified and get global styling.

In the example above, the intro section, `resources__intro`, might be similar to the intro to a block named `features`. Maybe they both have an H2 and an into paragraph, both are centered and span 6 columns in the grid. Maybe the blocks have different background colors and therefore font colors. The size, margin, width, text align, etc that is the same could be styled once, and if the differences are consistent enough could be styled with a helper class, if not they could be styled on a per block basis.

### Example

#### components/_intro.scss

Intro styles across any section (class name that ends in "__intro").

```scss
[class$="__intro"] {
    // intro component container styles

    h2 {
        ...
    }

    p {
        ...
    }
}
```

#### modules/_resources.scss

Intro styles specific to resources section.

```scss
.resources {
    background-color: #000000;

    &__intro {
        
        h2 {
            color: #ffffff;
        }
    }
}
```