# Themes for Foundation

This is a theme package for foundation
```

## Adding Themes

When installed, this package will look inside of the `resources/views/themes` folder for any folder containing a `.json` file with the same name as the folder. Example: `resources/views/themes/cool-beans/cool-beans.json` 

> If you wish to change the theme folder location, you can do so in the config

As an example if you have a folder called **cool-beans** and inside that folder you have another file called **cool-beans.json** with the following contents:

```
{
    "name": "Cool Beans",
    "version": "1.0"
}
```

This new theme will now be detected and available to use in your application. You can also include a sample screenshot of your theme, which would be **cool-beans.jpg** *(800x500px) for best results*

You can checkout a sample-theme repo here: [https://github.com/thedevdojo/sample-theme](https://github.com/thedevdojo/sample-theme)

The theme inside of the `themes` table with `active` set to 1 will the the active theme. You can then specify the theme view like the following:

```
return view('theme::welcome')
```

This will then look in the current active theme folder for a new view called `welcome.blade.php` :D

## Theme Configs

You may choose to publish a config to your project by running:

```
php artisan vendor:publish
```

You will want to publish the `voyager-themes-config`, and you will now see a new config located at `config/themes.php`, which will look like the following:

```
<?php

return [

    'themes_folder' => resource_path('views/themes'),
    'publish_assets' => true

];
```

Now, you can choose an alternate location for your themes folder. By default this will be put into the `resources/views` folder; however, you can change that to any location you would like.

Additionally, you can set **publish_assets** to *true* or *false*, if it is set to *true* anytime the themes directory is scanned it will publish the `assets` folder in your theme to the public folder inside a new `themes` folder. Set this to *false* and this will no longer happen.

## Theme Options

You can also easily add a number of options by including another file in the theme folder called `options.blade.php`

![Voyager Theme Options Page](https://i.imgur.com/eAoNt0W.png)

Inside the `options.blade.php` file you can now add a new field as simple as:

```
{!! theme_field('text', 'title') !!}
```

This will now add a new **text field** and store it with a **key** of *title*. So, now if you wanted to reference this value anywhere in your theme files you can simple echo it out like so:

```
{{ theme('title') }}
```

Couldn't be easier, right!

Take a look at all the following explanation of the `theme_field` function.

### The theme_field() function

The `theme_field()` function can be used to display fields in our theme options page. Take a look at the function DEFINITION, EXAMPLE, EXPLANATION, and TYPES OF FIELDS below:

**DEFINITION:**
  
    theme_field(
        $type, 
        $key,
        $title = '',
        $content = '', 
        $details = '', 
        $placeholder = '', 
        $required = 1)
  
**EXAMPLE** of a textbox asking for headline:
    
    {!! theme_field(
            'text', 
            'headline', 
            'My Aweseome Headline', 
            '{}', 
            'Add your Headline here', 
            0) 
     !!}

Only the first 2 are arguments are required

    {!! theme_field('text', 'headline') !!}

**EXPLANATION:**
    
    $type
        This is the type of field you want to display, you can
        take a look at all the fields from the TYPES OF FIELDS
        section below.
     $key
        This is the key you want to create to reference the
        field in your theme.
     $title
        This is the title or the label above the field
      $content 
        The current contents or value of the field, if the field
        has already been created in the db, the value in the
        database will be used instead
      $details
        The details of the field in JSON. You can find more 
        info about the details from the following URL:
        https://voyager.readme.io/docs/additional-field-options
      $placeholder
        The placeholder value of the field
      $required
        Whether or not this field is required

**TYPES OF FIELDS**
    
    checkbox, color, date, file, image, multiple_images,
    number, password, radio_btn, rich_text_box, code_editor,
    markdown_editor, select_dropdown, select_multiple, text,
    text_area, timestamp, hidden, coordinates

---

