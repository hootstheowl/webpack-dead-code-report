# Webpack Dead Code Report Plugin

Generate a JSON file displaying all unused modules within your webpack application's source code.

## Installation
With npm:
```shell
npm install webpack-dead-code-report --save-dev
```

Or, with yarn:
```shell
yarn add webpack-dead-code-report --dev
```

## Usage

In your webpack configuration file:

1. Require the plugin

  ```js
  const DeadCodeReportPlugin = require('webpack-dead-code-report');
  ```

2. Add the plugin to the `plugins` array:

  ```js
  plugins: [
    new DeadCodeReportPlugin({
      directories: [
        path.resolve('./app/scripts'),
      ],
      exclude: [
        path.resolve('./app/scripts/Billing/'),
        path.resolve('./app/scripts/*'),
      ],
      extensions: ['.js', '.jsx'],
      output: './unusedModules.json',
    })
  ]
  ```
   
## Options

- `directories` (Array): A list of directories to search for dead modules
- `exclude` (Array): A list of directories where the plugin should ignore dead modules
- `extensions` (Array): A list of allowed extensions for modules to search (default: `['.js']`)
- `outputPath` (String): The full path to the generated JSON file (default './unusedModuleReport.json'),
- `reactLocation` (String): If your project is a react (or react-like) project, you can define location of your framework library to allow the plugin to identify components (default: './node_modules/react/index.js')

## Example Output

```
{
  "totalModules": 200,
  "totalUnusedModules": 9,
  "unusedModulesList": [
    "./app/scripts/UI/Form/EmailInput.js",
    "./app/scripts/UI/Form/PhoneNumberInput.js",
    "./app/scripts/UI/Form/index.js",
    "./app/scripts/UI/MasterDetail/DetailView.js",
    "./app/scripts/UI/MasterDetail/index.js",
    "./app/scripts/UI/VSection.js",
  ],
  "excludedModulesList": [
    "./app/scripts/Billing/BankForm.js",
    "./app/scripts/Billing/CreditCardForm.js",
    "./app/scripts/Billing/InvoiceRoute.js",
    "./app/scripts/main.js"
  ]
}
```

## Q&A

#### Does this plugin delete dead code?
No. This plugin does not assume that unused modules have no place in your application. This plugin will only generate a JSON file for your own eyes and / or implementation.

#### Can this plugin delete dead code?
No. The JSON file produced can either be used to cherry-pick the removal of modules manually, or used within your own software for the archival / removal of any unused modules reported.
