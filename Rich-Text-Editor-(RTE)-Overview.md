## Table of contents

* [Introduction](#introduction)
* [Usage](#usage)
* [Third-Party Libraries](#third-party-libraries)
  * [Upgrading CKEditor](#upgrading-ckeditor)
* [Rich Text Components](#rich-text-components)
* [RTE implementation](#rte-implementation)
  * [Adding a new plugin](#adding-a-new-plugin)
    * [Adding rich text components to CKEditor](#adding-rich-text-components-to-ckeditor)
  * [Hidden components](#hidden-components)

## Introduction

Oppia has a rich text editor (RTE), used by exploration creators to create or edit the content of their explorations. This document is an overview of usage and implementation. The code portion of the document will largely focus on how the Rich Text Components are integrated into the RTE, since that is the most complicated part of Oppia's RTE setup.

## Usage

The directive is called `ck-editor-4-rte`, and can be used as simply as this example from [`suggestion-modal-for-creator-view.directive.html`](https://github.com/oppia/oppia/blob/develop/core/templates/pages/creator-dashboard-page/suggestion-modal-for-creator-view/suggestion-modal-for-creator-view.directive.html):

```html
<ck-editor-4-rte [value]="suggestionData.newSuggestionHtml"
                 (value-change)="updateValue($event)">
</ck-editor-4-rte>
```

See [`schema-based-html-editor.directive.html`](https://github.com/oppia/oppia/blob/develop/core/templates/components/forms/schema-based-editors/schema-based-html-editor.directive.html) for a more complicated usage example.

The directive exposes the following attributes:

* `[value]`: Bind to the variable storing the content the RTE is editing.
* `(value-change)`: Function call that handles the user's changes to the RTE.
* `[ui-config]` (optional): Used to configure the RTE. For example, you can set the placeholder text or whether to hide complex extensions.

## Third-Party Libraries

The RTE depends on the following third-party libraries, all specified in our `manifest.json`:

* [CKEditor 4](https://github.com/ckeditor/ckeditor4): CKEditor is a WYSIWYG rich text editor. The RTE is largely just a wrapper around CKEditor. We currently use version 4.
* [SharedSpace](https://ckeditor.com/cke4/addon/sharedspace): ensures that the toolbar will always remain in one designated place on the page.
* [Bootstrap](https://ckeditor.com/cke4/addon/bootstrapck): provides the skin of CKEditor's toolbar.

### Upgrading CKEditor

As described above, the core of our RTE is the 3rd party library CKEditor. If you are upgrading the CKEditor version we are using, it is important to check that the new CKEditor version does not cause any regressions in the RTE. After upgrading the CKEditor version, use the RTE in the exploration editor to perform the following checks in both the Chrome and Firefox browsers:

* Input some plain text and save. Ensure that the content doesn't disappear upon save.
* Input a single Rich Text Component (such as the Math component) and then save. Make sure it is saved properly.
* Try using backspace to delete the Rich Text Component. Make sure it is actually deleted.
* Try copying-and-pasting a Rich Text Component. Hit save and make sure that the component is copied properly.
* Try dragging-and-dropping a Rich Text Component from one place in the content to another, then saving. Make sure the component is moved properly.
* Input text with multiple paragraphs. Make sure the paragraphs are correctly spaced apart.
* Insert an Image component with a large image, and save. Make sure the image does not overflow the content boundaries.
* Insert an Image component with a small image, and save. Make sure the image is not stretched out.

## Rich Text Components

Oppia explorations can have Rich Text Components, which are custom widgets that creators can insert into their content. Note that we have two kinds of components at play here: rich text components and Angular components. Each rich text component is an Angular component of the form `<oppia-noninteractive-*></oppia-noninteractive-*>`, with different attributes depending on the component. Examples include the Math (for inserting Latex) component, the Image component, and the Video component. This section describes how the components are defined in case you want to add your own component, or need to modify an existing one.

The code for defining the Rich Text Components are housed in [`extensions/rich_text_components`](https://github.com/oppia/oppia/tree/develop/extensions/rich_text_components). In this folder each component has its own folder, with the following files and subfolders:

* `/directives` contains the TypeScript and HTML files that define the rich text component's Angular component.

  Each rich text component has one main Angular component defined by the following files:

  * `{{rich text component name}}.component.html`: Contains the HTML of the Angular component. This HTML will be inserted in place of the `<oppia-noninteractive-*>` tag.
  * `oppia-noninteractive-{{rich text component name}}.component.ts`: Defines the component logic.
  * `oppia-noninteractive-{{rich text component name}}.component.spec.ts`: Tests for the component logic.

  Some rich text components have additional Angular components like modals. These will have additional triplets of files.

* `{{rich text component name}}.png` is an icon representing the component, used in the RTE toolbar button.

* `protractor.js` exports two functions that are used by the end-to-end tests: `customizeComponent` configures a new instance of the component (e.g. sets the destination of a newly added Link component), and `expectComponentDetailsToMatch` checks that a component has the expected properties.

The properties of components are specified in [`assets/rich_text_components_definitions.js`](https://github.com/oppia/oppia/blob/develop/assets/rich_text_components_definitions.ts). Each component is described by the following properties:

* `backend_id`: A string used to identify this rich text component in the backend.
* `category`: The category the rich text component falls under in the repository.
* `description`: A description of the rich text component.
* `frontend_id`: The HTML tag name for the component.
* `tooltip`: The tooltip for the icon in the rich text editor.
* `icon_data_url`: URL of the component icon.
* `is_complex`: Whether the component is large enough to discourage its use when the rich text editor is intended to be lightweight.
* `requires_fs`: Whether the component requires the filesystem in some way that prevents it from being used by unauthorized users.
* `is_block_element`: Whether the component should be displayed as a block element.
* `customization_arg_specs`: Each dictionary defines a customizable option of that component. For example, the Math component has the sole customizable option `raw_latex` for the latex to be rendered. Each dictionary in the list has the form:
  * `name`: the name of the option.
  * `description`: a string describing the option, which will be displayed when the component is being edited/inserted.
  * `schema`: a [[schema|Schema-Based-Forms]] specifies type, and optionally validation rules or UI configurations.
  * `default_value`: initial value for the option.

Each rich text component must also be registered in `feconf.py`.

## RTE implementation

This section is a code overview of how the RTE is actually implemented. This is mostly useful if you plan to modify the RTE when fixing a bug or adding a new feature.

`CkEditor4RteComponent` is the Angular component, defined in [`ck-editor-4-rte.component.ts`](https://github.com/oppia/oppia/blob/develop/core/templates/components/ck-editor-helpers/ck-editor-4-rte.component.ts). There we define a `ckConfig` object that configures the editor. This configuration includes the `toolbar` attribute, which specifies the order in which rich text components appear in the editor toolbar.

Near the end of the `ngAfterViewInit()` function, we use `ck.on` to specify the following callback functions:

* The function passed to `ck.on('instanceReady', ...)` is executed when any new instance of CKEditor is ready. For example it will be executed when we click on the content of a card, for each option that we have for multiple choice options etc. Here we can add the css and icons to the buttons in the toolbar.
* The function passed to `ck.on('change', ...)` is executed whenever the content of CKEditor changes. It handles user updates to the rich text.

### Adding a new plugin

To add a new plugin, follow these steps:

1. Add the plugin to the `manifest.json` to download it. `SharedSpace` can be looked as an example. Alternatively, define your own custom plugin like we did with `pre`.
2. Add a call to `CKEditor.plugins.addExternal` to the component's `ngAfterViewInit()` method.
3. Add this plugin to `extraPlugins` in `ckConfig`.

#### Adding rich text components to CKEditor

Rich text components are added to CKEditor in [`ck-editor-4-widgets.initializer.ts`](https://github.com/oppia/oppia/blob/develop/core/templates/components/ck-editor-helpers/ck-editor-4-widgets.initializer.ts). The components are dynamically added to CKEditor as [widgets](https://docs.ckeditor.com/ckeditor4/latest/guide/widget_sdk_intro.html). We use the `getRichTextComponents()` function to obtain the information of each rich text component and construct there respective widgets. We also have a function `isInlineComponent()` to check whether a rich text component is inline or block component.

`componentTemplate` defines a template to wrap the rich text components. Inline components are wrapped in a span, and block components are wrapped in a div.

The plugins are added to CKEditor in the line `CKEDITOR.plugins.add(ckName, {`. The `init` function passed to `add()` is executed when the plugin is initialised and it adds a widget for each component using the line `editor.widgets.add(ckName, {`. `editor.widgits.add` is passed an object with the following attributes:

* `button`: The button label for the widget.
* `inline`: Whether the widget is an inline component or block component. The link and the math component are inline and the rest are declared block components.
* `template`: The wrapper template for the widget.
* `edit`: A function that will be executed when a widget is being edited. In this function the default action is canceled since we have used our own edit modal. `RteHelperService._openCustomizationModal()`is a helper function for opening the modal which is used to insert new components or editing existing ones. It uses the customizationArgSpecs (obtained from the component definition) to know what the editable fields are for each component, which allows it to render the modal properly for any component.
* `downcast()`: A function that downcasts the widget instance by clearing the Angular rendering content and returning the rich text component without any wrapper. Downcasting a widget means removing any property which is not needed in the output's source.
* `upcast()`: A function that upcasts an element to this widget. It returns whether an element is an instance of the widget. The element will be upcasted if it is an instance of the widget. Upcasting an element means changing that element into a widget.
* `data()`: A function that will be executed every time the widget data changes. It will set the attributes of rich text components according to the change in data values.
* `init()`: A function that will be executed when initialising a widget (after a widget instance is created, but before it is ready). It is executed before the first time when data function is exceuted. It reads and saves values from the component attributes.

### Hidden components

Sometimes, we want to disable or hide components in the RTE. There are 2 cases where this happens right now:

* "Complex" components such as tabs contain rich text content themselves, but we don't want the possibility of recursion where people can use the RTE to insert tabs inside tabs inside tabs...etc. For this case, the `ckEditorRte` directive [link function](http://websystique.com/angularjs/angularjs-custom-directives-link-function-guide/) checks the `uiConfig.hide_complex_extensions` flag. When `hide_complex_extensions` is set, complex extensions will be hidden from the user.
* There are cases, such as when a learner uses the RTE to submit a suggestion, where the user is not an editor and doesn't have filesystem-related permissions. For example, the learner can't upload a picture, so it makes sense to hide the functionality for inserting a new image (but images that may already be in the content should be left alone). The check `canUseFs && componentDefn.requiresFs` in the link function ensures that the image plugin is hidden.
