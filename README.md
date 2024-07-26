# XLIFF Sync

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.png)](https://opensource.org/licenses/MIT)

<a href="https://www.buymeacoffee.com/robvanbekkum" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>


A VSCode extension to keep XLIFF translation files in sync with an automatically generated base-XLIFF file.

Note that there is also an ["XLIFF Sync" PowerShell module](https://github.com/rvanbekkum/ps-xliff-sync)!

## Summary

The ["XLIFF Sync"](https://marketplace.visualstudio.com/items?itemName=rvanbekkum.xliff-sync) extension for Visual Studio Code can help you work more efficiently with XLIFF translation files in various ways.
It is specifically targeted at easing translation of extensions for [Microsoft Dynamics 365 Business Central](https://dynamics.microsoft.com/en-us/business-central/overview/), by allowing you to more easily keep `.xlf` translation files of your extensions in sync with the `.g.xlf` files that are automatically generated by the [AL Language](https://marketplace.visualstudio.com/items?itemName=ms-dynamics-smb.al) extension.
However, it can also be used in combination with other software projects that use [XLIFF](https://en.wikipedia.org/wiki/XLIFF) translation files for translation, supporting both XLIFF 1.2 and XLIFF 2.0.
Apart from synchronizing trans-units from a base-XLIFF file, this extension contributes various other features, including commands to check for missing translations, detect problems in translations and import translations from external XLIFF files.

View the demo in the [Areopa](https://areopa.academy/) webinar recording: [VS Code AL Extensions - XLIFF Sync](https://youtu.be/28JghaJHNJ4?t=376) (starts at 6:16)

More information: [XLIFF Sync: Time for a complete overview](https://robvanbekkum.nl/xliff-sync-overview/)

- [XLIFF Sync](#xliff-sync)
  - [Summary](#summary)
  - [Features](#features)
  - [Contributions](#contributions)
    - [Commands](#commands)
    - [Settings](#settings)
  - [Usage](#usage)
    - [Create New Target File(s)](#create-new-target-files)
      - [Using the Command Palette](#using-the-command-palette)
    - [Synchronize to Single File](#synchronize-to-single-file)
      - [Using the Command Palette](#using-the-command-palette-1)
      - [Using keyboard shortcut](#using-keyboard-shortcut)
    - [Synchronize Translation Units](#synchronize-translation-units)
      - [Using the Command Palette](#using-the-command-palette-2)
      - [Using keyboard shortcut](#using-keyboard-shortcut-1)
      - [From the Explorer](#from-the-explorer)
    - [Check for Missing Translations](#check-for-missing-translations)
      - [Using the Command Palette](#using-the-command-palette-3)
    - [Check for Need Work Translations](#check-for-need-work-translations)
      - [Using the Command Palette](#using-the-command-palette-4)
    - [Find Next Missing Translation in XLIFF File](#find-next-missing-translation-in-xliff-file)
      - [Using the Command Palette](#using-the-command-palette-5)
      - [Using keyboard shortcut](#using-keyboard-shortcut-2)
    - [Find Next Needs Work Translation in XLIFF File](#find-next-needs-work-translation-in-xliff-file)
      - [Using the Command Palette](#using-the-command-palette-6)
      - [Using keyboard shortcut](#using-keyboard-shortcut-3)
    - [Import Translations from File(s)](#import-translations-from-files)
      - [Using the Command Palette](#using-the-command-palette-7)
    - [Build with Translations](#build-with-translations)
      - [Using the Command Palette](#using-the-command-palette-8)
      - [Using keyboard shortcut](#using-keyboard-shortcut-4)
  - [Known Issues](#known-issues)
  - [Contributors](#contributors)

## Features

* Merge new translations from a generated, base-XLIFF file into existing XLIFF files.
  - Merge from the base-XLIFF file into a manually specified target XLIFF file.
  - Merge from the base-XLIFF file into all XLIFF files in the open workspace.
* Search and highlight missing translations in an open XLIFF file.
* Run technical validations to check for problems in the translations of target XLIFF files.
* Import/Copy translations for matching sources from external XLIFF files to target XLIFF files.
* Support for XLIFF 1.2 and 2.0
* Convert between XLIFF 1.2 and 2.0 format.

## Contributions

### Commands

| Command | Explanation |
| ------- | ----------- |
| **XLIFF: Create New Target File(s)** | Create one or more new target XLIFF files from the base-XLIFF file. |
| **XLIFF: Synchronize to Single File** | Merge new trans-units from base-XLIFF file into a manually specified target XLIFF file. |
| **XLIFF: Synchronize Translation Units** | Merge new trans-units from base-XLIFF file into all other XLIFF files in the open project folder. |
| **XLIFF: Check for Missing Translations** | Checks if there are any missing translations in the target XLIFF files in the open project folder. For each file with missing translations, an informational message will be shown (with a button to open the file externally). |
| **XLIFF: Check for Need Work Translations** | Checks if there are translations that need work in the target XLIFF files in the open project folder. For example, the source text contains placeholders (e.g., "%1" or "{0}") while the translation does not. Translations with problems will be tagged with `needs-adaptation` and an "XLIFF Sync" note will be added to the trans-unit node. For each file with translations that need work, an informational message will be shown (with a button to open the file externally). |
| **XLIFF: Next Missing Translation** | In an XLIFF file that is currently opened in the active editor, search for the next missing translation. |
| **XLIFF: Next Needs Work Translation** | In an XLIFF file that is currently opened in the active editor, search for the next translation tagged as `needs-adaptation`. |
| **XLIFF: Import Translations from File(s)** | Import/Copy translations from external XLIFF files to trans-units with matching sources of target XLIFF files with the same target-language. |
| **XLIFF: Build with Translations** | Deletes, Builds and generates Translations all in one for the current opened files App |

![XLIFF Sync Command Palette Commands](resources/xliffSync_commandPaletteCommands.png)

### Settings

| Setting | Default | Explanation |
| ------- | ------- | ----------- |
| xliffSync.baseFile | `.g.xlf` | Specifies which XLIFF file to use as the base (e.g., the generated XLIFF). If the file does not exist, you will be prompted to specify the file to use as base-XLIFF file the first time you use the Synchronize command. |
| xliffSync.fileType | `xlf` | The file type (`xlf` or `xlf2`). |
| xliffSync.syncCrossWorkspaceFolders | `false` | Specifies whether the extension will sync from a base file to the translation files in all workspace folders. By default, the extension will always sync. per workspace folder. If you enable this setting, then you can have the base file in one workspace folder and target translation files in other workspace folders. |
| xliffSync.matchingOriginalOnly | `true` | Specifies whether the extension will sync only to files where the original-attribute is matching. |
| xliffSync.unitMaps | `All` | Specifies for which search purposes this command should create in-memory maps in preparation of syncing. |
| xliffSync.missingTranslation | `%EMPTY%` | The placeholder for missing translations for trans-units that were synced/merged into target XLIFF files. You can use `%EMPTY%` if you want to use an empty string for missing translations. |
| xliffSync.needsWorkTranslationSubstate | `xliffSync:needsWork` | Specifies the substate to use for translations that need work in xlf2 files. **Tip**: If you use [Poedit](https://poedit.net/), then you could also set this to `poedit:fuzzy`. |
| xliffSync.findByXliffGeneratorNoteAndSource | `true` | Specifies whether or not the extension will try to find trans-units by XLIFF generator note and source. |
| xliffSync.findByXliffGeneratorAndDeveloperNote | `true` | Specifies whether or not the extension will try to find trans-units by XLIFF generator note and developer note. |
| xliffSync.findByXliffGeneratorNote | `true` | Specifies whether or not the extension will try to find trans-units by XLIFF generator note. |
| xliffSync.findBySourceAndDeveloperNote | `false` | Specifies whether or not the extension will try to find translations by the combination of source and developer note. |
| xliffSync.findBySource | `false` | Specifies whether or not the extension will try to find translations by source. If there are multiple trans-units with the same source, then the translation of the first translation unit is used for all units. |
| xliffSync.parseFromDeveloperNote | `false` | Specifies whether translations should be parsed from the developer note. Translations can be retrieved from a Developer note in the following format: <code>en-US=My translation&#124;nl-NL=Mijn vertaling</code>. |
| xliffSync.parseFromDeveloperNoteOverwrite | `false` | Specifies whether translations parsed from the developer note should always overwrite existing translations. |
| xliffSync.parseFromDeveloperNoteSeparator | <code>&#124;</code> | Specifies the separator that is used when translations are parsed from the developer note. |
| xliffSync.parseFromDeveloperNoteTrimCharacters | `` | Specifies the characters that will be trimmed from the translation. |
| xliffSync.equivalentLanguages | `{ "de-DE": "de-.*", "en-US": "en-.*", "es-ES": "es-.*", "fr-FR": "fr-.*", "nl-NL": "nl-.*" }` | Specifies master and slave languages that should be treated as equivalent, i.e., translations are copied from the master language. |
| xliffSync.equivalentLanguagesEnabled | `false` | Specifies whether languages should be treated as equivalent as specified in the xliffSync.equivalentLanguages setting. |
| xliffSync.copyFromSourceForLanguages | `[]` | Specifies the languages for which translations should be copied from the source text of trans-units. |
| xliffSync.copyFromSourceForSameLanguage | `false` | Specifies whether translations should be copied from the source text if source-language = target-language. This will **not** overwrite existing translations of trans-units in target files. |
| xliffSync.copyFromSourceOverwrite | `false` | Specifies whether translations copied from the source text should overwrite existing translations. |
| xliffSync.detectSourceTextChanges | `true` | Specifies whether changes in the source text of a trans-unit should be detected. If a change is detected, the target state is changed to needs-adaptation and a note is added to indicate the translation should be reviewed. |
| xliffSync.ignoreLineEndingTypeChanges | `false` | Specifies whether changes in line ending type (CRLF vs. LF) should not be considered as changes to the source text of a trans-unit. |
| xliffSync.clearTranslationAfterSourceTextChange | `false` | Specifies whether translations should be cleared when the source text of a trans-unit changed. |
| xliffSync.addNeedsWorkTranslationNote | `true` | Specifies whether an XLIFF Sync note should be added to explain why a trans-unit was marked as needs-work. |
| xliffSync.useSelfClosingTags | `true` | Specifies whether the XML tags in the XLIFF target files should be self-closing tags. (i.e., `<note></note>` vs. `<note/>`). |
| xliffSync.keepEditorOpenAfterSync | `true` | Specifies whether XLIFF files should be opened in the editor after syncing. |
| xliffSync.openExternallyAfterEvent | `[]` | Specifies after which event translation files should be opened automatically with the default XLIFF editor. Options: "Check", "ProblemDetected", "Sync" |
| xliffSync.developerNoteDesignation | `Developer` | Specifies the name that is used to designate a developer note. |
| xliffSync.xliffGeneratorNoteDesignation | `Xliff Generator` | Specifies the name that is used to designate a XLIFF generator note. |
| xliffSync.autoCheckMissingTranslations | `false` | Specifies whether or not the extension should automatically check for missing translations after syncing. |
| xliffSync.autoCheckNeedWorkTranslations | `false` | Specifies whether or not the extension should automatically run a technical validation on translations after syncing |
| xliffSync.needWorkTranslationRules | `["OptionMemberCount", "OptionLeadingSpaces", "Placeholders"]` | Specifies which technical validation rules should be used. |
| xliffSync.needWorkTranslationRulesEnableAll | `false` | Specifies whether or not all available technical validation rules should be used. Enabling this setting makes `xliffSync.needWorkTranslationRules` redundant. |
| xliffSync.preserveTargetAttributes | `false` | Specifies whether or not syncing should use the attributes from the target files for the trans-unit nodes while syncing. |
| xliffSync.preserveTargetAttributesOrder | `false` | Specifies whether the attributes of trans-unit nodes should use the order found in the target files while syncing. |
| xliffSync.preserveTargetChildNodes | `false` | Specifies whether child nodes of trans-unit nodes specific to the target files should be preserved. This will preserve `alt-trans` nodes and custom nodes in XLIFF 1.2 target files. |
| xliffSync.replaceTranslationsDuringImport | `false` | Specifies whether existing translations will be replaced when the XLIFF: Import Translations from File(s) command is run. |
| xliffSync.decoration | `{"backgroundColor": "rgba(240, 210, 105, 0.35)", "overviewRulerColor": "rgba(240, 210, 105, 0.35)", "border": "1px solid white", "borderRadius": "4px"}` | Specifies how to highlight missing translations or translations that need work in an XLIFF file opened in the editor. |
| xliffSync.decorationEnabled | `true` | Specifies whether decorations for missing translations and translations that need work should be applied. |
| xliffSync.decorationTargetTextOnly | `false` | Specifies whether decorations for missing translations and translations that need work should only be applied to the target text. |
| xliffSync.enableSnippetsForLanguages | `[]` | Specifies the programming languages for which the XLIFF Sync snippets should be enabled. Currently supported: `al`. |
| xliffSync.snippetTargetLanguage | `TargetLanguageCode` | Specifies which target language to use by default in the XLIFF Sync snippets (e.g., `nl-NL`). |
| xliffSync.defaultLanguages | `[]` | Specifies the languages that should automatically be used for the translation file generation. If empty, asks which language to use. |
| xliffSync.buildCommandToExecute | `al.package` | Specifies the build command to execute when building with translations. |

## Usage

The extension will try to find corresponding trans-units and translations within an existing file as follows:

1. Finding trans-units:
> 1. By Id
> 2. By XLIFF Generator Note & Source (enabled by default, configurable with `xliffSync.findByXliffGeneratorNoteAndSource`)
> 3. By XLIFF Generator Note & Developer Note (enabled by default, configurable with `xliffSync.findByXliffGeneratorAndDeveloperNote`)
> 4. By XLIFF Generator Note (enabled by default, configurable with `xliffSync.findByXliffGeneratorNote`)

2. Finding translations:
> 5. By Source & Developer Note (disabled by default, configurable with `xliffSync.findBySourceAndDeveloperNote`)
> 6. By Source (disabled by default, configurable with `xliffSync.findBySource`)

3. Initial translation:
> 7. Parse from Developer Note (disabled by default, configurable with `xliffSync.parseFromDeveloperNote`)
> 8. Copy from Source, if applicable/configured for target language (disabled by default, configurable with `xliffSync.copyFromSourceFor...`)

If no trans-unit or translation is found, the unit is added and its target node is tagged with `state="needs-translation"`.

### Create New Target File(s)

#### Using the Command Palette
> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Create New Target File(s)**

This command will let you create one or more new target files, using the languages specified in the `xliffSync.defaultLanguages` setting or when empty letting you choose from a set of RFC 4646 or RFC 5646 language tags depending on the XLIFF file type (i.e., `xlf` or `xlf2`).
The new file is automatically synced with the base file; if it is not known you will be prompted to specify the file to use as the base file first.

![XLIFF Sync Create New Target Files Options](resources/xliffSync_createNewTargetFilesOptions.png)

More detailed instruction: [Create New Target Files](https://robvanbekkum.nl/xliff-sync-overview/#create-new-target-files)

### Synchronize to Single File

#### Using the Command Palette
> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Synchronize to Single File**

#### Using keyboard shortcut

> 1.  Alt + X, S (default shortcut)

By default, the extension expects the base-XLIFF file to end with `.g.xlf`.
If no matching file is found, you are prompted to identify the base file.
This setting will be saved for future use.
If the extension is invoked from a localization file, that file will be updated, otherwise the extension will prompt you for the file to update.

You can also use this command to create a new XLIFF file for a language.
For this, choose the "New File..." option and choose the language tag for the new target language.

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
If you select any other XLIFF file, then translation units will be synced from the base-XLIFF file to the selected file.

![XLIFF Sync Sync. Translation Units from Context Menu](resources/xliffSync_synchronizeTranslationUnits_contextMenu.png)

Here's a small demo:

![XLIFF Sync from Explorer](resources/xliffSync_explorer.gif)

More detailed instruction: [Synchronize Translation Files](https://robvanbekkum.nl/xliff-sync-overview/#synchronize-translation-files)

### Check for Missing Translations

#### Using the Command Palette

> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Check for Missing Translations**

This will check all XLIFF files in the workspace and notify about any missing translations in the files.
You also have the option to open files with missing translations with your default XLIFF editor using the **Open Externally** button from the informational message.

![XLIFF Sync Check Missing Translations Messages](resources/xliffSync_checkMissingTranslations.png)

More detailed instruction: [Check Translation Files](https://robvanbekkum.nl/xliff-sync-overview/#check-translation-files)

### Check for Need Work Translations

#### Using the Command Palette

> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Check for Need Work Translations**

This will run technical validation/checks for all XLIFF files in the workspace and notify about any translations that need work in the files.
You also have the option to open files containing problems with your default XLIFF editor using the **Open Externally** button from the informational message.

![XLIFF Sync Check Need Work Translations Messages](resources/xliffSync_checkNeedWorkTranslations.png)

The target node of the trans-units containing problems will be tagged with `state="needs-adaptation"`.
Additionally, a `note` will be added to the trans-unit to explain which problem was detected.
When you run the command again after resolving the issue, then this note will be automatically removed.

You can configure the checks that need to be run with the `xliffSync.needWorkTranslationRules` setting.
The currently implemented checks are the following:

| Rule ID               | Check                                                                                                     | Trigger                                                                                    | Example                                                                                                            |
|-----------------------|-----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| `ConsecutiveSpacesConsistent` | 'Consecutive space'-occurrences are not matching. | N.A. | The source text includes 3 consecutive spaces, the translation text includes 2 consecutive spaces. |
| `ConsecutiveSpacesExist` | Source or translation text contain consecutive spaces. | N.A. | The source text includes 2 consecutive spaces, e.g., <pre>Hello  World</pre> |
| `OptionMemberCount`   | Number of options in caption are not matching.                                                            | Xliff Generator note with `Property OptionCaption` or `Property PromotedActionCategories`. | The source text includes 3 options, `A,B,C` , but the translation text includes 4 options, `A,B,C,D`.              |
| `OptionLeadingSpaces` | Number of leading spaces in options are not matching.                                                     | Xliff Generator note with `Property OptionCaption` or `Property PromotedActionCategories`. | The source text includes a space, `A, B` , but the translation text does not, `A,B`.                               |
| `Placeholders`        | Placeholders of source and translation are not matching.                                                  | Source/Translation text includes placeholders of the form `{0}` or `%1` or `#1`.                   | The source text includes placeholders `%1 %2` , but the translation text only includes `%1`.                       |
| `PlaceholdersDevNote`        | Placeholders are not explained in the Developer note.                                                  | Source text includes placeholders of the form `{0}` or `%1` or `#1`.                   | The source text includes placeholders `%1 %2` , but the Developer note is empty and so does not contain the placeholders.                       |
| `SourceEqualsTarget`  | Source and translation are not the same, even though source-language = target-language for the .xlf file. | The source-language is the same as the target-language for the .xlf file.                  | The source text is 'A', but the translation text is 'B'. The source-language and target-language are both 'en-US'. |

**Note**: You may want to use rule `SourceEqualsTarget` in combination with setting `xliffSync.copyFromSourceForSameLanguage` set to `true`.

More detailed instruction: [Check Translation Files](https://robvanbekkum.nl/xliff-sync-overview/#check-translation-files)

### Find Next Missing Translation in XLIFF File

#### Using the Command Palette

> 1.  F1 or CMD + Shift + P to open the command palette
> 2.  **XLIFF: Next Missing Translation**

#### Using keyboard shortcut

> 1.  Alt + X, N (default shortcut)

Missing translations are tagged and highlighted.
You can use the extension to navigate between missing translations.
On a Macbook Pro, this command appears on the touchbar within XLIFF files.

### Find Next Needs Work Translation in XLIFF File

#### Using the Command Palette

> 1.  F1 or CMD + Shift + P to open the command palette
> 2.  **XLIFF: Next Needs Work Translation**

#### Using keyboard shortcut

> 1.  Alt + X, W (default shortcut)

Translations that need work are tagged and highlighted.
You can use this command to navigate between translations that need work.
On a Macbook Pro, this command appears on the touchbar within XLIFF files.

### Import Translations from File(s)

#### Using the Command Palette

> 1. F1 or Ctrl/Cmd + Shift + P to open the command palette
> 2. **XLIFF: Import Translations from File(s)**

This will open a file dialog in which you can select one or more XLIFF files (.xlf or .xlf2).
The command will copy translations from the selected files to trans-units in the XLIFF files in your project folder with the same target-language for matching sources.
It will try first to merge translations for trans-units with a matching combination of source-text and Developer note, and only after that try to merge translations to trans-units with matching source-text.
That way you could utilize the Developer note to have the import perform a more precise merge of the translations (e.g., based on tags in the Developer notes).

More detailed instruction: [Import Translations from Files](https://robvanbekkum.nl/xliff-sync-overview/#import-translations-from-files)

### Build with Translations

#### Using the Command Palette

> 1.  F1 or CMD + Shift + P to open the command palette
> 2.  **XLIFF: Build with Translations**

#### Using keyboard shortcut

> 1.  Ctrl + Shift + T (default shortcut)

This command combines multiple actions into one command:
> 1. Delete current translation files
> 2. Build App using the build command defined in new Setting `xliffSync.buildCommandToExecute`
> 3. Create new Target files for Languages defined in new Setting `xliffSync.defaultLanguages`
> 4. Syncs Translations files to show if translations are missing

To use this, a file from the App for which you want to update the Translations has to be opened. Then execute the command.

## Known Issues

* Automatically inserting _new_ groups into target files is not implemented.
* The NAV2018 XLIFF generator creates Xliff Generator Notes without any identifiers, therefore it is recommended to change the `xliffSync.findBy...` settings to not synchronize trans-units based on Xliff Generator notes.
* Files larger than 50 MB cannot be processed at the moment. For now, please use the ["XLIFF Sync" PowerShell module](https://github.com/rvanbekkum/ps-xliff-sync) instead.

## Contributors

* [dannoe](https://github.com/dannoe)
* [manux54](https://github.com/manux54)
* [rvanbekkum](https://github.com/rvanbekkum)
* [warlof](https://github.com/warlof)
* [der_floh](https://github.com/Der-Floh)

You can find the contributions in the [Changelog](https://marketplace.visualstudio.com/items/rvanbekkum.xliff-sync/changelog).
Thank you all! 🤍
