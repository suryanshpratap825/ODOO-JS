## ODOO 17 JS:

Odoo 17's JavaScript (JS) framework provides the building blocks for creating dynamic and interactive user interfaces within the Odoo business management system. This framework enables developers to craft custom web applications, add new features, and modify existing Odoo modules using JavaScript code.

## **Understanding Odoo JS and the setup() function**

In Odoo's JavaScript framework, the `setup()` function within a class acts similarly to a constructor in traditional JavaScript. However, there's a crucial reason why Odoo adopts the `setup()` approach:

- **Overridability:** A key advantage of using `setup()` instead of a standard `constructor()` lies in the ability to easily override its behavior. This allows developers to customize the initialization logic of Odoo components without encountering the limitations often imposed by overriding traditional JavaScript constructors..

## Assets

There are three types of the assets inside the ODOO:

- **JS Files (JavaScript):** These files are fundamental to Odoo's functionality. They control elements such as rendering various views (e.g., tree view, form view) and handling user interactions within the system.
- **XML Files:**  XML files serve as templates, loaded dynamically by Odoo when required.  They define the structural layout and content presentation within the interface.
- **CSS or SCSS Files:** These files are responsible for the visual styling of Odoo components. They dictate the appearance, including colors, fonts, and spacing of elements within the interface.

## **Bundles**

Odoo organizes its assets into bundles. These bundles are declared within the module's ***__manifest__.py*** file.

Ex: 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cd67c677-3bbe-491a-ba9d-7c6636182027/51e30b8d-9352-4bb6-98d5-69200558c33f/Untitled.png)

### Note:

Odoo asset bundles support the use of [glob](https://en.wikipedia.org/wiki/Glob_(programming)) syntax, providing flexibility in file inclusion.

## Adding a New File to a Bundle

Odoo offers several methods for adding files to asset bundles:

- **Prepend**: Add one or more files to the beginning of a bundle. This is useful when you need specific files to load first.
- **Before**: Position one or more files ahead of a designated file within the bundle.
- **After:**  Place one or more files after a designated file within the bundle.
- **Include:**  Incorporate nested bundles for more complex asset organization.
- **Remove**:  Delete one or more files from the bundle.
- **Replace**:  Substitute an existing asset file with one or more new files.

### Note

Later, we will cover the topic of adding files to bundles.

So far, we have discussed what JS is and its basic concepts. 

## **Overriding Functions / Patching Code in Odoo**

Odoo's web interface is comprised of modular components. This allows you to tailor its functionality to meet your specific needs by overriding the behavior of these components.  The process of overriding is commonly referred to as "patching" code.

Odoo provides a dedicated `patch` function, located within `@web/core/utils/patch`, to facilitate these customizations.

**Example: Overriding the ListController's setup() Function**

Let's illustrate how to patch the `setup()` function within the ListController component:

### **Step 1: Verify Exportability of the ListController Class**

Before attempting to override, ensure that the `ListController` class is configured for export. If the export statement precedes the class definition, you'll be able to import it for customization.

### **Step 2: Create a New JS File and Integrate into the Asset Bundle**

1. Create a new JavaScript file (`.js` extension).
2. Ensure you add this file to the same asset bundle where the `ListController` resides. This guarantees that your customization code loads alongside the original component.

EX:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cd67c677-3bbe-491a-ba9d-7c6636182027/8493ac58-91d9-4656-b9db-5277a425cbeb/Untitled.png)

In the provided image, the custom file has been correctly added to the `web.assets_backend` bundle, as this is the bundle containing the `ListController`.

## **Step 3: Import and Set Up Patching**

Inside your new JS file, perform the following:

`import { ListController } from '@web/views/list/list_controller';`

`import {patch} from "@web/core/utils/patch";`

## NOTE:

If you're utilizing the OWL framework within this file, ensure the following line is present at the very top:
`/** @odoo-module **/`

This line signifies to Odoo that the file contains OWL code.

### **Step 4: Override the Setup Function with Patching**

Use the `patch` function to override the `setup()` function as demonstrated below:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cd67c677-3bbe-491a-ba9d-7c6636182027/537f7a6f-de0d-4f23-8912-fda05da92455/Untitled.png)

## Note:

You can adapt this pattern to override any function.

> Thank you!
In the document above, we discussed the basics of OWL and patching. I will gradually add more topics related to OWL.

Suryansh Pratap Singh
>
