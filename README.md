# LForms

## What is LForms?

[LForms](http://lhncbc.github.io/lforms/), a.k.a. LHC-Forms, is a feature-rich,
open-source Web Component that creates input forms, based on definition files, 
for Web-based applications. In addition to its native form-definition format, 
it partially supports the HL7 FHIR Questionnaire standard (SDC profile), and work
is in progress to expand that support.

It is being developed by the Lister Hill National Center for Biomedical
Communications ([LHNCBC](https://lhncbc.nlm.nih.gov)), National Library of
Medicine ([NLM](https://www.nlm.nih.gov)), part of the National Institutes of
Health ([NIH](https://www.nih.gov)), with the collaboration and support from 
the [Regenstrief Institute](https://www.regenstrief.org/), Inc. and the
[LOINC](https://loinc.org/) Committee.

For features and demos, please visit the [project
page](http://lhncbc.github.io/lforms/).

## Quick Start

The fastest way to get started with LForms:

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="https://clinicaltables.nlm.nih.gov/lforms-versions/38.3.0/webcomponent/styles.css">
</head>
<body>
  <wc-lhc-form></wc-lhc-form>

  <script src="https://clinicaltables.nlm.nih.gov/lforms-versions/38.3.0/webcomponent/assets/lib/zone.min.js"></script>
  <script src="https://clinicaltables.nlm.nih.gov/lforms-versions/38.3.0/webcomponent/runtime.js"></script>
  <script src="https://clinicaltables.nlm.nih.gov/lforms-versions/38.3.0/webcomponent/polyfills.js"></script>
  <script src="https://clinicaltables.nlm.nih.gov/lforms-versions/38.3.0/webcomponent/main.js"></script>
  <script src="https://clinicaltables.nlm.nih.gov/lforms-versions/38.3.0/fhir/lformsFHIRAll.min.js"></script>

  <script>
    window.addEventListener('DOMContentLoaded', function() {
      var formDef = {
        "type": "LOINC",
        "code": "54127-6", 
        "name": "US Surgeon General - family health portrait",
        "items": [{"questionCode": "54126-8", "question": "Patient name", "dataType": "ST"}]
      };
      LForms.Util.addFormToPage(formDef, document.querySelector('wc-lhc-form'));
    });
  </script>
</body>
</html>
```

See the [Installation](#installation) section below for other installation options.

## Installation

There are several ways to install and use LForms in your project:

### Option 1: Using npm (Recommended for Node.js projects)

Install the lforms package from npm:

```bash
npm install lforms
```

The package contains pre-built files in the `node_modules/lforms/dist/lforms` directory. You'll need to include these files in your project as described in the [Using the LHC-Forms Web Component](#using) section.

**Note**: The current npm package contains built files only. You cannot use `import` or `require` statements directly. Use the built files as described below.

### Option 2: Using CDN (Recommended for quick setup)

You can use the pre-built versions directly from the NLM CDN. Include these files in your HTML:

```html
<!-- CSS -->
<link rel="stylesheet" href="https://clinicaltables.nlm.nih.gov/lforms-versions/[VERSION]/webcomponent/styles.css">

<!-- JavaScript files -->
<script src="https://clinicaltables.nlm.nih.gov/lforms-versions/[VERSION]/webcomponent/assets/lib/zone.min.js"></script>
<script src="https://clinicaltables.nlm.nih.gov/lforms-versions/[VERSION]/webcomponent/runtime.js"></script>
<script src="https://clinicaltables.nlm.nih.gov/lforms-versions/[VERSION]/webcomponent/polyfills.js"></script>
<script src="https://clinicaltables.nlm.nih.gov/lforms-versions/[VERSION]/webcomponent/main.js"></script>

<!-- FHIR support (choose one) -->
<script src="https://clinicaltables.nlm.nih.gov/lforms-versions/[VERSION]/fhir/lformsFHIRAll.min.js"></script>
```

Replace `[VERSION]` with a specific version number (e.g., `38.3.0`). See available versions at https://clinicaltables.nlm.nih.gov/lforms-versions/.

### Option 3: Download and host locally

1. Download a release from https://clinicaltables.nlm.nih.gov/lforms-versions/
2. Extract the files to your project directory
3. Include the files as described in the [Using the LHC-Forms Web Component](#using) section

For more details about the files to load and how to work with the library, see the [Using the LHC-Forms Web Component](#using) section below.

## Licensing and Copyright Notice

See [LICENSE.md](LICENSE.md).

## Customizing and Contributing

If you wish to revise this package, the following steps will allow you to make
changes and test them:

- Install Node.js (version 14 is what we are currently using, but it should work 
  with later versions)
- Clone the lforms repository and cd to its directory
- `source bashrc.lforms` (make sure node dir is available at ~/)
- `npm ci`
- `source bashrc.lforms` # to add node_modules/.bin to your path
- `npm run build` # build both FHIR libs and LHC-Forms web component
- `npm run start` # starts the app we use for testing
- `npm run test` # runs the unit tests and e2e tests

If you are planning to contribute new functionality back to us, please
coordinate with us, so that the new code is in the right places, and so that
you don't accidentally add something that we are also working on.

## Development server

- Run `npm run start` for a dev server. Navigate to `http://localhost:4200/`.
  The app will automatically reload if you change any of the source files.

- Run `npm run start-public` if you need to access to the dev server from a 
  different machine. For example, to run Narrator from a Windows PC.

## Build

- Run `npm run build` to build the project and generate a production version of
  the js files, which are much smaller than the development version. It
  generates an ES2017 version of the js files under dist/lforms. For details on
  the files to load, see ["Using the LHC-Forms Web Component"](#using).  
  The `dist` directory is deleted and recreated during the process.

  The build also concatenates all the js files (except for zone.min.js and the
  FHIR support files) into a single `lhc-forms.js` file, and it works,
  but we don't currently recommend their use because the
  source maps don't work with these files. Also, there is a dist/webcomponent
  directory that is created with a copy of the files in dist/lforms, but that
  is only needed for the tests.

- **If you want to build LForms in a different language**, make sure your desired
  locale ID is listed under src/languages, e.g. `de_DE.json`. In `package.json`, edit
  config.localeID to your desired locale, e.g. "de_DE". Then run `npm run build`.
  To build on Windows, you may need to refer to the locale ID npm variable as
  `%npm_package_config_localeID%` instead of `$npm_package_config_localeID` in package.json.

  If your desired language is not yet listed under src/languages, please contact us
  to have it added, or submit a pull request for adding your own language config file.
  Please note that LForms cannot support more languages than listed
  here: https://ng.ant.design/docs/i18n/en.

## Running tests

1. Run `npm run test` to run unit tests and e2e tests, which also copies the 
   FHIR lib files and built files in places for testing.

## Running unit tests

1. Run `npm run test:unit` to execute the unit tests via 
   [Karma](https://karma-runner.github.io).

## Running end-to-end tests

1. Run `npm run test:e2e` to execute the end-to-end tests via 
   [Cypress](https://www.cypress.io/). The e2e tests are configured to use Chrome.

## <a id="using">Using the LHC-Forms Web Component</a>

### Required Files

You need to include the following files in your project (file paths are relative to the base directory, which is either `dist/lforms` if you're building from source, `node_modules/lforms/dist/lforms` if using npm, or the root of the versioned directory from https://clinicaltables.nlm.nih.gov/lforms-versions/):

1. **CSS**: `webcomponent/styles.css`
2. **JavaScript files** (in order):
   - `webcomponent/assets/lib/zone.min.js` (skip if you already have zone.js on the page)
   - `webcomponent/runtime.js`
   - `webcomponent/polyfills.js`
   - `webcomponent/main.js`
3. **FHIR support** (choose _one_ if you plan to use FHIR Questionnaires):
   - `fhir/lformsFHIRAll.min.js` (supports all FHIR versions)
   - `fhir/R5/lformsFHIR.min.js` (R5 only)
   - `fhir/R4B/lformsFHIR.min.js` (R4B only)
   - `fhir/R4/lformsFHIR.min.js` (R4 only)
   - `fhir/STU3/lformsFHIR.min.js` (STU3 only)

### Basic Usage Example

Once the files are loaded, you can use the `<wc-lhc-form>` web component in your HTML:

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="path/to/webcomponent/styles.css">
</head>
<body>
  <!-- The LForms web component -->
  <wc-lhc-form></wc-lhc-form>

  <!-- Include the JavaScript files -->
  <script src="path/to/webcomponent/assets/lib/zone.min.js"></script>
  <script src="path/to/webcomponent/runtime.js"></script>
  <script src="path/to/webcomponent/polyfills.js"></script>
  <script src="path/to/webcomponent/main.js"></script>
  <script src="path/to/fhir/lformsFHIRAll.min.js"></script>

  <script>
    // Wait for LForms to be available
    window.addEventListener('DOMContentLoaded', function() {
      // Get the form element
      var formElement = document.querySelector('wc-lhc-form');
      
      // Load a form definition (example with a simple form)
      var formDef = {
        "type": "LOINC",
        "code": "54127-6",
        "name": "US Surgeon General - family health portrait",
        "items": [{
          "questionCode": "54126-8",
          "question": "Patient name",
          "dataType": "ST"
        }]
      };
      
      // Set the form definition
      LForms.Util.addFormToPage(formDef, formElement);
    });
  </script>
</body>
</html>
```

### Additional Resources

- **Live example app**: https://lhcforms.nlm.nih.gov/lforms-fhir-app/
- **Full documentation**: https://lhncbc.github.io/lforms/
- **Announcements list**: See the documentation for subscription information

## <a id="npm-package">lforms npm package</a>

The lforms npm package contains pre-built files in the `node_modules/lforms/dist/lforms` directory after installation. 

**Important**: You cannot use `import` or `require` statements directly with this package. Instead, you need to include the built files from the `dist/lforms` directory in your HTML, as described in the [Installation](#installation) and [Using the LHC-Forms Web Component](#using) sections above.

For example, if you've installed lforms via npm:
```bash
npm install lforms
```

You can reference the files from `node_modules`:
```html
<link rel="stylesheet" href="node_modules/lforms/dist/lforms/webcomponent/styles.css">
<script src="node_modules/lforms/dist/lforms/webcomponent/assets/lib/zone.min.js"></script>
<!-- ... other files ... -->
```

Or you can copy the files to your public/static directory as part of your build process.

## <a id="docs">Related Documents</a>
- `form_definition.md` The internal data format of the LHC-Forms widget.
- `changed-features.md` The list of features that changes between the new 
version (v30.0.0) and previous versions.
- `r4-support.md` The FHIR R4 features supported by LHC-Forms widget. 
- `sdc-support.md` The FHIR SDC features supported by LHC-Forms widget.
