# XLIFF Sync

A VSCode extension to keep XLIFF translation files in sync with a specified, automatically generated base-XLIFF file.

This project originated from the need for a tool to automatically merge XLIFF translation files that are in the OASIS specification (instead of Angular's i18n).
More specifically, this extension is intended to ease merging new translations into XLIFF files from an `<ApplicationName>.g.xlf` file that is automatically generated by the [AL Language](https://github.com/Microsoft/AL) extension for Dynamics 365 Business Central extensions.

The intention is to keep this project simple with support for merging simple XLIFF files, i.e., only supporting the merge of `trans-unit` nodes that may or may not be contained in `group` nodes.
This extension is based on the [Angular Localization Helper extension](https://github.com/manux54/vsc-angular-localization-helper) by **[manux54](https://github.com/manux54)**!

![XLIFF Sync from Explorer](resources/xliffSync_explorer.gif)

## Features

* Merge new translations from a generated, base-XLIFF file into existing XLIFF files.
  - Merge from the base-XLIFF file into a manually specified target XLIFF file.
  - Merge from the base-XLIFF file into all XLIFF files in the open workspace.
* Search and highlight missing translations in an open XLIFF file.
* Run technical validations to check for problems in the translations of target XLIFF files.
* Support for XLIFF 1.2 and 2.0
* Convert between XLIFF 1.2 and 2.0 format.

## Contributions

### Commands

| Command | Explanation |
| ------- | ----------- |
| **XLIFF: Synchronize to Single File** | Merge new trans-units from base-XLIFF file into a manually specified target XLIFF file. |
| **XLIFF: Synchronize Translation Units** | Merge new trans-units from base-XLIFF file into all other XLIFF files in the open project folder. |
| **XLIFF: Check for Missing Translations** | Checks if there are any missing translations in the target XLIFF files in the open project folder. For each file with missing translations, an informational message will be shown (with a button to open the file externally). |
| **XLIFF: Check for Need Work Translations** | Checks if there are translations that need work in the target XLIFF files in the open project folder. For example, the source text contains placeholders (e.g., "%1" or "{0}") while the translation does not. Translations with problems will be tagged with `needs-adaptation`. For each file with translations that need work, an informational message will be shown (with a button to open the file externally). |
| **XLIFF: Next Missing Translation** | In an XLIFF file that is currently opened in the active editor, search for the next missing translation. |
| **XLIFF: Next Needs Work Translation** | In an XLIFF file that is currently opened in the active editor, search for the next translation tagged as `needs-adaptation`. |

![XLIFF Sync Command Palette Commands](resources/xliffSync_commandPaletteCommands.png)

### Settings

| Setting | Default | Explanation |
| ------- | ------- | ----------- |
| xliffSync.baseFile | `application.g.xlf` | Specifies which XLIFF file to use as the base (e.g., the generated XLIFF). If the file does not exist, you will be prompted to specify the file to use as base-XLIFF file the first time you use the Synchronize command. |
| xliffSync.fileType | `xlf` | The file type (`xlf` or `xlf2`). |
| xliffSync.missingTranslation | `%EMPTY%` | The placeholder for missing translations for trans-units that were synced/merged into target XLIFF files. You can use `%EMPTY%` if you want to use an empty string for missing translations. |
| "xliffSync.findByXliffGeneratorAndDeveloperNote" | `true` | Specifies whether or not the extension will try to find trans-units by XLIFF generator note and developer note. |
| xliffSync.findByXliffGeneratorNote | `true` | Specifies whether or not the extension will try to find translation unit by XLIFF generator note. |
| xliffSync.findBySource | `false` | Specifies whether or not the extension will try to find translation unit by source. If there are multiple translation units with the same source, then the translation of the first translation unit is used for all units. |
| xliffSync.developerNoteDesignation | `Developer` | Specifies the name that is used to designate a developer note. |
| xliffSync.xliffGeneratorNoteDesignation | `Xliff Generator` | Specifies the name that is used to designate a XLIFF generator note. |
| xliffSync.autoCheckMissingTranslations | `false` | Specifies whether or not the extension should automatically check for missing translations after syncing. |
| xliffSync.autoCheckNeedWorkTranslations | `false` | Specifies whether or not the extension should automatically run a technical validation on translations after syncing |
| xliffSync.needWorkTranslationRules | `["OptionMemberCount", "OptionLeadingSpaces", "Placeholders"]` | Specifies which technical validation rules should be used. |
| xliffSync.preserveTargetAttributes | `false` | Specifies whether or not syncing should use the attributes from the target files for the trans-unit nodes while syncing. |
| xliffSync.preserveTargetAttributesOrder | `false` | Specifies whether the attributes of trans-unit nodes should use the order found in the target files while syncing. |
| xliffSync.decoration | 'Highlight yellow, white border' | Specifies how to highlight missing translations or translations that need work in an XLIFF file opened in the editor. |

## Usage

The extension will try to find corresponding translations units within an existing file for each units in the base file by searching units in the following order:

> 1.  By Id
> 2.  By XLIFF Generator note & Source
> 3.  By XLIFF Generator note & Developer Note (optional)
> 4.  By XLIFF Generator note (optional)
> 5.  By Source (optional)

If no translation unit is found, the unit is added and tagged as missing.

### Synchronize to Single File

#### Using the Command Palette
> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Synchronize to Single File**

#### Using keyboard shortcut

> 1.  Alt + X, S (default shortcut)

By default, the extension expects the base-XLIFF file to be named `application.g.xlf`. If no matching file is found, you are prompted to identify the base file. This setting will be saved for future use. If the extension is invoked from a localization file, that file will be updated, otherwise the extension will prompt you for the file to update. You can also create a new file.

### Synchronize Translation Units

#### Using the Command Palette

> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Synchronize Translation Units**

*NOTE*: This command will merge new translations into all XLIFF files in your workspace folder (with, obviously, excluding the base-XLIFF file itself).

#### Using keyboard shortcut

> 1.  Alt + X, M (default shortcut)

#### From the Explorer

> 1. Right-click on a file with the .xlf extension.
> 2. Select: **Synchronize Translation Units**

If you select the base-XLIFF file, then translation units will be synced to all other XLIFF files in the workspace.
If you select any other XLIFF file, then translation untis will be synced from the base-XLIFF file to the selected file.

![XLIFF Sync Sync. Translation Units from Context Menu](resources/xliffSync_synchronizeTranslationUnits_contextMenu.png)

### Check for Missing Translations

#### Using the Command Palette

> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Check for Missing Translations**

This will check all XLIFF files in the workspace and notify about any missing translations in the files. You also have the option to open files with missing translations with your default XLIFF editor using the **Open Externally** button from the informational message.

![XLIFF Sync Check Missing Translations Messages](resources/xliffSync_checkMissingTranslations.png)

### Check for Need Work Translations

#### Using the Command Palette

> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Check for Need Work Translations**

This will run technical validation/checks for all XLIFF files in the workspace and notify about any translations that need work in the files. You also have the option to open files containing problems with your default XLIFF editor using the **Open Externally** button from the informational message.

![XLIFF Sync Check Need Work Translations Messages](resources/xliffSync_checkNeedWorkTranslations.png)

You can configure the checks that need to be run with the `xliffSync.needWorkTranslationRules` setting.
The currently implemented checks are the following:

| Rule ID               | Check                                                                                                     | Trigger                                                                                    | Example                                                                                                            |
|-----------------------|-----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| `OptionMemberCount`   | Number of options in caption are not matching.                                                            | Xliff Generator note with `Property OptionCaption` or `Property PromotedActionCategories`. | The source text includes 3 options, `A,B,C` , but the translation text includes 4 options, `A,B,C,D`.              |
| `OptionLeadingSpaces` | Number of leading spaces in options are not matching.                                                     | Xliff Generator note with `Property OptionCaption` or `Property PromotedActionCategories`. | The source text includes a space, `A, B` , but the translation text does not, `A,B`.                               |
| `Placeholders`        | Placeholders of source and translation are not matching.                                                  | Source/Translation text includes placeholders of the form `{0}` or `%1`.                   | The source text includes placeholders `%1 %2` , but the translation text only includes `%1`.                       |
| `SourceEqualsTarget`  | Source and translation are not the same, even though source-language = target-language for the .xlf file. | The source-language is the same as the target-language for the .xlf file.                  | The source text is 'A', but the translation text is 'B'. The source-language and target-language are both 'en-US'. |

### Find Next Missing Translation in XLIFF File

#### Using the Command Palette

> 1.  F1 or CMD + Shift + P to open the command palette
> 2.  **XLIFF: Next Missing Translation**

#### Using keyboard shortcut

> 1.  Alt + X, N (default shortcut)

Missing translations are tagged and highlighted. You can use the extension to navigate between missing translations.
On a Macbook Pro, this command appears on the touchbar within XLIFF files.

### Find Next Needs Work Translation in XLIFF File

#### Using the Command Palette

> 1.  F1 or CMD + Shift + P to open the command palette
> 2.  **XLIFF: Next Needs Work Translation**

#### Using keyboard shortcut

> 1.  Alt + X, W (default shortcut)

Translations that need work are tagged and highlighted. You can use this command to navigate between translations that need work.
On a Macbook Pro, this command appears on the touchbar within XLIFF files.

## Known Issues

* Automatically inserting new group nodes into target files may not work yet.
* The NAV2018 generated .g.xlf file does not include the Xliff Generator notes, therefore you should only synchronize based on ID with NAV2018.
