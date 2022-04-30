

# Summernote gallery
summernote-gallery extension/plugin/module for [summernote](https://github.com/summernote/summernote/) WYSIWYG, provides a bootstrap image-gallery modal to select images from the server and add them to the summernote editor with **the real path to the server** instead of using base64 encoding.

**For a complete module with more user-friendly components. see [Summernote bricks](https://github.com/eissasoubhi/summernote-bricks)**

# Summernote Gallery for Bootstrap 5
This is a fork of the original [summernote gallery](https://github.com/eissasoubhi/summernote-gallery) for tweaking it to work on [Bootstrap 5](http://getbootstrap.com) Summernote. To work the whole setup you must install a developement version of summernote. This plugin work with Bootstrap 5.1.3.

# Demo
Demo link - Bootstrap 5:
http://ranjithsiji.github.io/summernote-gallery <br><br>

Demo link - Bootstrap 3:
http://eissasoubhi.github.io/summernote-gallery <br><br>

![Summernote gallery demo](demo.gif?raw=true "Summernote gallery demo")

# Installing
- Include the required files, and the module file after summernote.min.js file

```html
<link href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet" >
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" />
<link href="summernote/summernote-bs5.min.css" rel="stylesheet">

<div id="summernote"></div>

<script type="text/javascript" src="//code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"></script>
<script type="text/javascript" src="//cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>
<script src="summernote/summernote-bs5.min.js" type="text/javascript"></script>
<!-- summernote-gallery -->
<script src="dist/summernote-gallery.min.js" type="text/javascript"></script>
```
- Add the gallery to the summernote editor toolbar

```javascript
$('#summernote').summernote({
        toolbar: [
                ['insert', ['picture', 'link', 'video', 'table', 'hr', 'summernoteGallery']],
                ['font style', ['fontname', 'fontsize', 'color', 'bold', 'italic',
                'underline', 'strikethrough', 'superscript', 'subscript', 'clear']],
                ['paragraph style', ['style', 'ol', 'ul', 'paragraph', 'height']],
                ['misc', ['fullscreen', 'codeview', 'undo', 'redo', 'help']]
                ['extensions', ['summernoteGallery']],
        ],
        summernoteGallery: {
            source: {
                // data: [],
                url: 'http://eissasoubhi.github.io/summernote-gallery/server/example.json',
                responseDataKey: 'data',
                nextPageKey: 'links.next',
            },
            modal: {
                loadOnScroll: true,
                maxHeight: 300,
                title: "Summernote Gallery",
                close_text: 'Close',
                ok_text: 'Add',
                selectAll_text: 'Select All',
                deselectAll_text: 'Deselect All',
                noImageSelected_msg: 'No image was selected, please select one by clicking it!',
            }
             buttonLabel: '<i class="fa fa-file-image-o"></i> Gallery'
        }
    });
```

I used a json file `server/example.json` as the `source.url` just for the demo, for a practical example you can check out the PHP file `server/example.php`.

# Options

The module has two main options: `source` and `modal`:<br>
The `source` option has sub-options that handle data and ajax requests.<br>
The `modal` option has sub-options that deal with the bootsrap modal.<br>


## Sub-options:

| Option                    | description                                                                                                                                                                                                                                                                                                                                                                                                                                                           | default                              | type    | example                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| source                    | This option is the parent of the following options:                                                                                                                                                                                                                                                                                                                                                                                                                   |                                      | object  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| source.data               | Array of objects with 'src' and 'title' properties                                                                                                                                                                                                                                                                                                                                                                                                                    | []                                   | array   | <pre><br>[{<br>    "src": "https://picsum.photos/id/40/200/200",<br>    "title": "a galerie test"<br>}, {<br>    "src": "https://picsum.photos/id/50/200/200",<br>    "title": "a galerie test"<br>}]<br></pre>                                                                                                                                                                                                                                                                                  |
| source.url                | A full valid URL. the response of the URL must have `data` property that holds the data.<br> The data format is the same as the `source.data`'s. the `data` property name can be changed with the `source.responseDataKey` option.<br> If `modal.loadOnScroll` is set to true, in addition to `data`, the response is expected  to have `links.next` property for the next page URL, this property name can also be changed with the `source.nextPageKey` option.<br> | null                                 | string  | URL example: http://mywebsite.com/api/images?page=1  <br> Response example:<br> <pre><br>{<br>    "data": [{<br>        "src": "https://picsum.photos/id/40/200/200",<br>        "title": "a galerie test"<br>    }, {<br>        "src": "https://picsum.photos/id/50/200/200",<br>        "title": "a galerie test"<br>    }],<br>    "links": {<br>        "next": "http://mywebsite.com/api/images?page=2"<br>    }<br>}<br></pre>                                                            |
| source.responseDataKey    | The property name that holds the data array from `source.url`.<br> For sub-properties, use dot notation, eg: `"data.key.subkey"`                                                                                                                                                                                                                                                                                                                                      | data                                 | string  | If the `source.responseDataKey` option value is `"data.items"`,<br> The `source.url` response is expected to be:  <pre><br>{<br>    "data": {<br>        "items": [{<br>            "src": "https://picsum.photos/id/40/200/200",<br>            "title": "a galerie test"<br>        }, {<br>            "src": "https://picsum.photos/id/50/200/200",<br>            "title": "a galerie test"<br>        }]<br>    },<br>    "links": {<br>        "next": "...."<br>    }<br>}<br></pre><br> |
| source.nextPageKey        | The property name that holds the next page link from `source.url`.<br> For sub-properties, use dot notation, eg: `"data.key.subkey"`                                                                                                                                                                                                                                                                                                                                  | links.next                           | string  | If the `source.nextPageKey` option value is `"next_page"`,<br> the `source.url` response is expected to be:  <pre><br>{<br>    "data": [],<br>    "next_page": "http://mywebsite.com/api/images?page=2"<br>}<br></pre>                                                                                                                                                                                                                                                                           |
| modal                     | This option is the parent of the following options:                                                                                                                                                                                                                                                                                                                                                                                                                   |                                      | object  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| modal.loadOnScroll        | Reloads the next page data when the modal scroll is near to the bottom.<br> The module reloads the next page data using `source.nextPageKey` value to extract the next page  link from the last `source.url` response, that means when `modal.loadOnScroll` is set to true,  every request must provide the link to the next page, unless it's the last page, in that case,  the value of the next page link  has to be null or unset.                                | false                                | boolean | true                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| modal.maxHeight           | The modal body max height                                                                                                                                                                                                                                                                                                                                                                                                                                             | 500                                  | integer | 300                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| modal.title               | The modal title                                                                                                                                                                                                                                                                                                                                                                                                                                                       | summernote image gallery             | string  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| modal.close_text          | The modal close button text                                                                                                                                                                                                                                                                                                                                                                                                                                           | Close                                | string  | Fermer                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| modal.ok_text             | The modal save button text                                                                                                                                                                                                                                                                                                                                                                                                                                            | Add                                  | string  | Ajouter                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| modal.selectAll_text      | The modal select-all button text                                                                                                                                                                                                                                                                                                                                                                                                                                      | Select all                           | string  | Sélectionner Tout                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| modal.deselectAll_text    | The modal deselect-all button text                                                                                                                                                                                                                                                                                                                                                                                                                                    | Deselect all                         | string  | Désélectionner Tout                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| modal.noImageSelected_msg | The message error to display when no image is selected                                                                                                                                                                                                                                                                                                                                                                                                                | One image at least must be selected. | string  | No image was selected, please select one by clicking it!                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| buttonLabel | The text displayed on the plugin button, it accepts HTML                                                                                                                                                                                                                                                                                                                                                                                                                | <i class="fa fa-file-image-o"></i> SN Gallery | string  | My <strong>Button</strong>                                                                                                                                                                                                                                                                                                                                                                                                                                         |

Feel free to modify the source file to suit your needs.

# Contribution || Edit

**Requirements: node v16**

To run the plugin on local, head to the project root folder and run:
1. `npm install`
2. `npm run start` to start the project on 127.0.0.1:9090
3. `npm run dev` to start the webpack watch mode
4. Edit plugin files in the `/src` folder 
5. `npm run build` to generate the build in `/dist` folder

If you found any bugs or have suggestions, dont hesitate to throw it in the issues sections.

For more undestanding of how this module works take a look on the [v1](https://github.com/eissasoubhi/summernote-gallery/tree/v1) branch or the summernote extension basic sample [hello](https://github.com/summernote/summernote/blob/v0.7.0/examples/plugin-hello.html) .

# License
The contents of this repository is licensed under [The MIT License.](https://opensource.org/licenses/MIT)
