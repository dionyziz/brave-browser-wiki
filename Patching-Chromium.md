One of the primary goals of brave-core is to do changes in a way that makes it easy for Chromium rebases. This is because speed of updating to a new Chromium version is important to us. 

Please follow this order when doing patching from best to worst:

## Changes only inside brave-core

If changes can be made inside existing subclasses and code inside `src/brave`, then that is preferred.

## Subclass and override

When you can't make a change directly in existing brave-core code, it's often best to simply subclass a Chromium class, and override the functions needed.

You will need to patch (see the below documentation) for some small trivial things in this case:
- Create instances of your class instead of the Chromium class.
- Possibly add a `friend` member to the base class you're subclassing.
- Possibly add a `virtual` keyword to functions you'd like to subclass.

Header patches should use preprocessor defines when possible. The define should always be the last thing in `public` so you can change to `protected` or `private` inside the define.
```
  bool ShouldRunUnloadListenerBeforeClosing(content::WebContents* web_contents);
  bool RunUnloadListenerBeforeClosing(content::WebContents* web_contents);

  // Set if the browser is currently participating in a tab dragging process.
  // This information is used to decide if fast resize will be used during
  // dragging.
  void SetIsInTabDragging(bool is_in_tab_dragging);

  BRAVE_BROWSER_H
 private:
```
with chromium_src override
```
#ifndef BRAVE_CHROMIUM_SRC_CHROME_BROWSER_UI_BROWSER_H_
#define BRAVE_CHROMIUM_SRC_CHROME_BROWSER_UI_BROWSER_H_

#define BRAVE_BROWSER_H \
 private: \
  friend class BookmarkPrefsService;

#include "../../../../../chrome/browser/ui/browser.h"  // NOLINT

#undef BRAVE_BROWSER_H

#endif  // BRAVE_CHROMIUM_SRC_CHROME_BROWSER_UI_BROWSER_H_
```
## Using the preprocessor to use base implementations inside override files

One strategy that's preferred over patching is to use `src/brave/chromium_src` which overrides `.cc` and `.h` files but still use the source in the original Chromium code too.  To do that you can rename a function with the preprocessor in Chromium, and then provide your own real implementation of that file and use the Chromium implementation inside of it.

Here's an example:
https://github.com/brave/brave-core/blob/5293f0cab08816819bb307d02e404c2061e4368d/chromium_src/chrome/browser/browser_about_handler.cc

No BUILD.gn changes are needed for this.

## Override a .cc file completely

If you want to provide a completely different implementation of a file, it is often not safe, but sometimes applicable. You can just provide the alternate implementation inside the `src/brave/chromium_src` directory.

One way electron went wrong is they copied entire files for changes inside a similar setup, do NOT do this. This will lead to newer Chromium rebases over time using old stale code which causes problems and makes rebasing much harder.

No BUILD.gn changes are needed for this.

## Patch the Chromium files

When other options are exhausted, you can patch the code directly in `src/`. After making the changes, you can run the npm command `npm run update_patches`.   This will update the patches which are stored in  `src/brave/patches`.   Please note that removed changes in `src` currently will not update the patches, so you will have to do that manually. 

We aim to make the only patches required to be trivial changes, and not nested logic changes. 
If possible write the patch to add a new line vs appending/prepending to an existing line.

For example, instead of 
```
-  return !url.is_empty() && !url.SchemeIs(content::kChromeUIScheme) &&
+  return IsBraveTranslateEnabled() && !url.is_empty() && !url.SchemeIs(content::kChromeUIScheme) &&
!url.SchemeIs(content::kChromeDevToolsScheme) &&
``` 
it should be
```
return !url.is_empty() && !url.SchemeIs(content::kChromeUIScheme) &&
+  IsBraveTranslateEnabled() &&
!url.SchemeIs(content::kChromeDevToolsScheme) &&
```
Do not add comments in patches and ignore lint line length rules to squash patches onto one line whenever possible

Patch changes which affect the flow of execution should ideally be wrapped in `#if defined(BRAVE_CHROMIUM_BUILD)` and `#endif` blocks.

You should almost never patch in two methods calls in a row. We should prefer extensible patches. For instance https://github.com/brave/brave-core/pull/2693/files#diff-a9c9a8da7aa4df821394352a0ca04a27R12:
```
CopyBraveExtensionLocalization(config, staging_dir, g_archive_inputs)
CopyBraveRewardsExtensionLocalization(config, staging_dir, g_archive_inputs)
```
inside `CopyAllFilesToStagingDir` would be collapsed to
```
CopyBraveFilesToStagingDir
```

Make sure you do NOT have the following in your `~/.gitconfig`:

    [apply]
            whitespace = fix

as trailing whitespace can be essential in patch files.

## Patching gn/gni files
We should also prefer extensible patches in gn files where possible. 

Multiple deps should never be added to the same target. Always create a generic brave dep and then add other deps (public_deps if needed) inside that. 

The same thing goes for sources, but those should be added as `sources += my_brave_sources` where `my_brave_sources` is defined in a brave gni file. We have a gni file that is already included in nearly every gn build file in chromium through a patch in chrome_build.gni (`import("//brave/build/config/brave_guild.gni"`). Add new gni imports inside brave_guild.gni instead of patching them into another gn/gni file

## Patching java files

Try to extend Java class like in that example https://github.com/brave/brave-core/blob/master/android/java/org/chromium/chrome/browser/BraveActivity.java or https://github.com/brave/brave-core/blob/master/android/java/org/chromium/chrome/browser/toolbar/top/BraveToolbarLayout.java. 
After that just create the new class via `new ...` where the old class created.

## Patching Android xml files

- AndroidManifest.xml: Brave's addition to the manifest is included in the original chromium's and located in that place https://github.com/brave/brave-core/blob/master/android/java/AndroidManifest.xml. Add new items inside it.
- layouts: Layouts could be included in original chromium's layouts `<include layout="@layout/brave_toolbar" android:layout_height="wrap_content" android:layout_width="match_parent" />`
- styles: Add new style to https://github.com/brave/brave-core/blob/master/android/java/res/values/brave_styles.xml
- preferences: create your preference in a separate xml file https://github.com/brave/brave-core/blob/master/android/java/res/xml/brave_main_preferences.xml and inject it in runtime from java code https://github.com/brave/brave-core/blob/master/android/java/org/chromium/chrome/browser/preferences/BraveMainPreferencesBase.java#L51
- resources: add general resources, pictures and etc inside https://github.com/brave/brave-core/tree/master/android/java/res. They are copied inside original chromium's folder before a build.