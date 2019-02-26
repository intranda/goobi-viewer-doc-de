# 9.2 Theme changes

## 2019-02-25

Umstellung der Dateistruktur für das neue Admin-Backend.

* ~~/boilerplate/css/less/viewer/views/admin/admin.less~~
* ~~/boilerplate/css/less/viewer/views/admin/adminBackendTables.less~~
* ~~/boilerplate/css/less/viewer/views/admin/adminIpRange.less~~
* ~~/boilerplate/css/less/viewer/views/admin/adminLicenseType.less~~
* ~~/boilerplate/css/less/viewer/views/admin/adminUser.less~~
* ~~/boilerplate/css/less/viewer/views/admin/adminUserGroup.less~~
* ~~/boilerplate/css/less/viewer/views/admin/tabUserLicenses.less~~
* ~~/boilerplate/css/less/viewer/widgets/widgetAdmin.less~~
* ~~/boilerplate/css/less/viewer/widgets/widgetCms.less~~
* /boilerplate/templateAdmin.html

## 2019-02-21

Änderungen an LESS-Template \(~~overflow-x: hidden;~~\).

* /boilerplate/css/less/general.less

## 2019-02-13

Änderungen an LESS-Template.

* /boilerplate/css/less/viewer/views/search/searchListGrid.less

## 2019-01-24

Neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/components/metaMuseal.less

## 2019-01-22

Neue Methode zum anzeigen von Subtheme-CSS.

* /boilerplate/template.html
* /boilerplate/templateAdmin.html
* /boilerplate/templateFullscreen.html

## 2019-01-21

Änderung eines CSS-Klassennamens.

* /boilerplate/css/less/viewer/components/imageControls.less

## 2019-01-17

Änderungen an HTML- und LESS-Templates.

* /boilerplate/templateMirador.html
* /boilerplate/css/less/viewer/views/viewMirador.less
* /boilerplate/css/less/viewer/components/imageControls.less

Refaktorisierung Lesemodus. Vereinigung Lesemodus und Vollbildanzeige.

* /boilerplate/images/icons/
* /boilerplate/includes/customJS.xhtml
* ~~/boilerplate/fullscreenTemplate.html~~
* ~~/boilerplate/templateReadingMode.html~~
* /boilerplate/templateFullscreen.html
* /boilerplate/css/less/viewer/constructor.less
* ~~/boilerplate/css/less/viewer/views/viewReadingMode.less~~
* ~~/boilerplate/css/less/viewer/views/viewFullscreen.less~~
* /boilerplate/css/less/viewer/views/viewObjectFullscreen.less
* /boilerplate/css/less/viewer/views/fullscreen/fsImageControls.less
* /boilerplate/css/less/viewer/views/fullscreen/fsMetadata.less
* /boilerplate/css/less/viewer/views/fullscreen/fsToc.less
* /boilerplate/css/less/viewer/views/fullscreen/fsUsage.less

## 2018-12-21

Refaktorisierung LESS Template.

* /boilerplate/css/less/viewer/widgets/widgetToc.less

## 2018-12-17

Änderungen an LESS Template.

* /boilerplate/css/less/viewer/components/buttons.less

## 2018-12-07

Änderungen an LESS Templates.

* /boilerplate/css/less/viewer/components/imageControls.less
* /boilerplate/css/less/viewer/widgets/widgetUsage.less

## 2018-12-05

Neues URL-Mapping für Werke und optionales META-Tag für Indexierung durch Roboter.

* /theme-url-mappings.xml
* /boilerplate/template.html

## 2018-11-30

Neue LESS-Templates.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/templates/23\_templateSearch.less
* /boilerplate/css/less/viewer/cms/templates/24\_templateTags.less

## 2018-11-21

Zusätzliches Thumbnail für nicht vorhandene Bildvorschauen.

* /boilerplate/images/image\_not\_found.png

## 2018-11-19 <a id="2018-07-05"></a>

LESS-Template gelöscht.

* /boilerplate/css/less/viewer/constructor.less
* ~~/boilerplate/css/less/viewer/search/searchTimeline.less~~

## 2018-11-16 <a id="2018-07-05"></a>

Neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/widgets/widgetUsage.less

## 2018-10-29

Setzen einer globalen Variablen im JavaScript, die den aktuellen Theme Namen enthält.

* /boilerplate/includes/customJS.xhtml
* /boilerplate/javascript/dev/custom.js

## 2018-10-12

LESS-Template Refaktorisierung.  
JavaScript Framework RiotJS zum Grunt-Task hinzugefügt und in die Templates eingebunden. Neuen Ordner für Tags angelegt.

* /boilerplate/css/less/viewer/components/buttons.less
* Gruntfile.js
* package.json
* /boilerplate/includes/customJS.xhtml
* /boilerplate/javascript/dev/tags/
* /boilerplate/javascript/dist/boilerplate-tags.js
* /boilerplate/template.html
* /boilerplate/templateAdmin.html
* ~~/boilerplate/templateReadingMode.html~~

## 2018-10-11

Neues LESS-Template, sowie LESS-Template Refaktorisierung. Aktivierung neuer JavaScript Funktionalität \(_cmsJS.modules.init\(\);_\).

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/modules/options.less
* /boilerplate/css/less/viewer/cms/views/cmsMenuItems.less
* /boilerplate/css/less/variables.less
* /boilerplate/css/less/viewer/views/user/user.less
* /boilerplate/includes/customJS.xhtml

## 2018-09-07

Link für Sitelinks zu SEO Zwecken hinzugefügt.  
Änderungen an LESS Template.

* /boilerplate/components/footerNavigation.xhtml
* /boilerplate/css/less/viewer/cms/templates/12\_templateSingleCollection.less

## 2018-09-03

Relative Links zu vorheriger und nachfolgender Seite zu SEO Zwecken hinzugefügt.

* /boilerplate/fullscreenTemplate.html
* /boilerplate/template.html
* /boilerplate/templateAdmin.html
* /boilerplate/templateMirador.html
* /boilerplate/templateReadingMode.html

## 2018-08-24

Zusätzliches Thumbnail für Audiodateien.

* /boilerplate/images/thumbnail\_audio.jpg

## 2018-07-25

Änderungen am Gruntfile \(MS Edge konforme SourceMaps\).

* Gruntfile.js

## 2018-07-13

Neues LESS- und HTML-Template, sowie LESS-Template Refaktorisierung.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/views/viewMirador.less
* /boilerplate/css/less/templateMirador.html
* /boilerplate/css/less/viewer/components/mobileNavigation.less

## 2018-07-05

Neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/views/cmsCollections.less

## 2018-07-03

LESS-Template Refaktorisierung.

* /boilerplate/css/less/viewer/components/bookshelves.less
* /boilerplate/css/less/viewer/components/loginNavigation.less

## 2018-06-27

LESS-Template Refaktorisierung.

* /boilerplate/css/less/viewer/views/viewThumbs.less

## 2018-06-25

LESS-Template Refaktorisierung.

* /boilerplate/css/less/viewer/views/viewMetadata.less

## 2018-06-21

LESS-Template Änderungen und neue LESS-Templates.

* /boilerplate/css/less/viewer/views/search/searchList.less
* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/views/search/searchListGrid.less
* /boilerplate/css/less/viewer/views/search/searchListList.less

## 2018-06-13

Neue LESS-Templates.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/templates/22\_templateFaqSingle.less
* /boilerplate/css/less/viewer/cms/templates/21\_templateFaq.less

## 2018-06-12

Neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/widgets/widgetChronology.less

## 2018-05-28

Neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/views/common/sitelinks.less

## 2018-05-07

Umbenennung und Refaktorisierung eines LESS-Templates.

* /boilerplate/css/less/viewer/components/userComments.less

## 2018-05-03

Refaktorisierung von LESS-Templates.

* /boilerplate/css/less/viewer/widgets/widgetSearchInCurrentItem.less
* /boilerplate/css/less/viewer/widgets/widgetSearchField.less
* /boilerplate/css/less/viewer/views/common/privacy.less
* /boilerplate/css/less/viewer/views/common/feedback.less
* /boilerplate/css/less/viewer/views/common/error.less

## 2018-05-02

Refaktorisierung von LESS-Templates.

* /boilerplate/css/less/viewer/components/imageControls.less
* /boilerplate/css/less/viewer/views/viewReadingMode.less

## 2018-04-19

Neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/views/viewObject.less

## 2018-04-13

Refaktorisierung eines LESS-Templates.

* /boilerplate/css/less/viewer/components/simplePaginator.less

## 2018-04-12

Refaktorisierung eines LESS-Templates.

* /boilerplate/css/less/viewer/components/ePub.less

## 2018-04-10

Refaktorisierung eines LESS-Templates.

* /boilerplate/css/less/viewer/components/alphabeticPaginator.less

## 2018-03-29

Neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/templates/20\_templateGlossary.less

## 2018-02-22

Refaktorisierung eines LESS-Templates.

* /boilerplate/css/less/viewer/views/user/userSavedSearches.less

## 2018-02-13

Neue LESS-Templates.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/views/user/userBookshelf.less
* /boilerplate/css/less/viewer/views/user/userBookshelfEdit.less
* /boilerplate/css/less/viewer/views/user/userBookshelfSingle.less
* /boilerplate/css/less/viewer/views/user/userBookshelves.less

## 2018-02-08

Neue LESS-Templates.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/templates/18\_templatePrivacy.less
* /boilerplate/css/less/viewer/cms/templates/19\_templateFeedback.less



