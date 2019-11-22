# 8.2 Theme changes

## 2019-11-20

Neue header-Zeilen in allen template\*.html-Dateien:  
Die Zeile

```markup
	<meta name="version" content="#{navigationHelper.version}" />
```

ersetzen durch

```markup
	<meta name="application" content="#{navigationHelper.applicationName}" />
	<meta name="version" content="#{navigationHelper.version}" />
	<meta name="public version" content="#{navigationHelper.publicVersion}" />
	<meta name="build date" content="#{navigationHelper.buildDate}" />
	<meta name="git-revision" content="#{navigationHelper.buildVersion}" />
```

## 2019-10-30

Neues Template Campaign hinzugefügt

* /boilerplate/templateCrowdsourcing.html

## 2019-09-05

Änderungen an der pom.xml. Damit keine Installationsresourcen mit in die war übernommen werden muss der Ordner bei der unpack-dependency des maven-dependency-plugins mit ausgeschlossen werden.

```text
Suchen:
<excludes>MANIFEST.MF,**/pom.*</excludes>

Ersetzen:
<excludes>MANIFEST.MF,**/pom.*,install/</excludes>
```

## 2019-07-04

Änderungen am Gruntfile und HTML-Templates.

* Gruntfile.js
* /boilerplate/template.html
* /boilerplate/templateFullscreen.html
* /boilerplate/includes/customJS.xhtml

Umstrukturierung der Ordner und Dateien im Verzeichnis `/boilerplate/css/less/`.

```text
less
  cms
   |_templates
  components
   |_forms
  crowdsourcing
   |_components
   |_views
  layout
  misc
  subthemes
   |_boilerplate-subtheme
  views
   |_common
   |_fulsscreen
   |_search
   |_user
  widgets
```

## 2019-06-24

Änderungen am Gruntfile. Entfernung des CSS-Dev-Ordners und der statischen Seiten.

* Gruntfile.js
* /themes/theme-url-mappings.xml
* ~~/boilerplate/css/dev/~~
* ~~/boilerplate/pages/~~
* ~~/boilerplate/css/less/views/common/styles.less~~

## 2019-06-21

Änderung an LESS-Templates.

* /boilerplate/css/less/build.less
* /boilerplate/css/less/components/forms/basics.less
* /boilerplate/css/less/components/forms/form-controls.less
* /boilerplate/css/less/components/buttons.less
* ~~/boilerplate/css/less/components/forms.less~~
* /boilerplate/css/less/widgets/widgets.less

## 2019-06-13

Änderung an LESS-Template.

* /boilerplate/css/less/components/title.less

## 2019-06-12

Ergänzungen in der Datei `/WebContent/WEB-INF/web.xml` zur korrekten Weiterleitung von CMS-Seiten. Hier muss folgendes eingetragen werden.

{% code title="web.xml" %}
```markup
<filter>
    <filter-name>UrlRedirectFilter</filter-name>
    <filter-class>io.goobi.viewer.filters.UrlRedirectFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>UrlRedirectFilter</filter-name>
    <url-pattern>*.xhtml</url-pattern>
    <dispatcher>REQUEST</dispatcher>
</filter-mapping>
```
{% endcode %}

## 2019-06-04

{% hint style="info" %}
Im Zuge der Umstellung auf Maven hat sich die Ordner- und Dateistruktur der Boilerplate geändert.

Themes müssen an diese neue Struktur angepasst werden, damit sie lauffähig bleiben. Eine Anleitung zur Umstellung findet sich unter [8.2.1 Theme Umstellung zu Maven](8.2.1.md).
{% endhint %}

Änderungen am Gruntflile.

* Gruntfile.js

## 2019-05-28

Änderung an HTML-Template: Bibliothek für PDF-Anzeige hinzugefügt.

* /boilerplate/template.html

## 2019-05-27

Änderungen an LESS-Templates.

* /boilerplate/css/less/resets.less
* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/components/loginNavigation.less
* ~~/boilerplate/css/less/viewer/components/modals.less~~
* /boilerplate/css/less/viewer/views/user/user.less
* ~~/boilerplate/css/less/viewer/views/user/userData.less~~
* ~~/boilerplate/css/less/viewer/views/user/userAccountCreate.less~~
* ~~/boilerplate/css/less/viewer/views/user/userAccountRetrieve.less~~

## 2019-05-23

Basis Schriftgröße auf 62.5% \(10px\) gesetzt, um besser mit der Einheit `rem` rechnen zu können.

* /boilerplate/css/less/general.less

## 2019-05-22

Änderungen an HTML-Templates.

* /boilerplate/template.html
* /boilerplate/templateFullscreen.html
* /boilerplate/templateMirador.html

Einsetzen einer `<h:panelGroup id="subBody">...</h:panelGroup>`, um die Seite mit `<f:ajax render="subBody" />` neu laden zu können, ohne die angehängten Events vom Body-Element zu zerstören.

* /boilerplate/template.html

## 2019-05-20

Neue Komponente `/resources/includes/user/userLogin.xhtml` für Benutzeranmeldung.

* /boilerplate/includes/layout.xhtml

Neues LESS-Template.

* /boilerplate/css/less/viewer/views/user/userLogin.less
* /boilerplate/css/less/viewer/constructor.less

Entfernung des Widgets **widget\_user.xhtml** aus den Seitenleisten der XHTML-Dateien.

* /boilerplate/pages/styles.xhtml
* /boilerplate/pages/templateStaticPage.xhtml
* /boilerplate/urlMappings/index.xhtml

Änderung an LESS-Templates.

* ~~/boilerplate/css/less/viewer/widgets/widgetUser.less~~
* /boilerplate/css/less/viewer/constructor.less

## 2019-04-17

Änderungen an LESS-Templates.

* /boilerplate/css/less/viewer/widgets/widgetSearchDrillDown.less

## 2019-04-15

Einführung von Twitter Cards und Opengraph Vorschau Snippets.

* /boilerplate/template.html
* /boilerplate/templateFullscreen.html

Initialisierung des adminJS Moduls.

* /boilerplate/includes/customJS.xhtml

## 2019-04-04

Link für oEmbed Unterstützung eingefügt.

* /boilerplate/template.html
* /boilerplate/templateFullscreen.html

## 2019-03-29

Änderung an LESS-Template.

* /boilerplate/css/less/viewer/widgets/widgets.less

## 2019-03-27

Link zur Open Search Unterstützung eingefügt.

* /boilerplate/template.html
* /boilerplate/templateFullscreen.html

## 2019-03-25

Änderung an LESS-Template und neues LESS-Template.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/widgets/widgetUser.less
* /boilerplate/css/less/viewer/widgets/widgetUserInteractions.less

## 2019-03-11

Änderungen an LESS-Templates.

* ~~/boilerplate/css/less/viewer/components/icons.less~~
* /boilerplate/css/less/viewer/widgets/widgetBookshelfList.less
* /boilerplate/css/less/layout.less
* /boilerplate/css/less/viewer/constructor.less

## 2019-03-01

Entfernung nicht mehr benötigter LESS-Templates.

* ~~/boilerplate/css/less/viewer/cms/components/~~
* ~~/boilerplate/css/less/viewer/cms/modules/~~
* ~~/boilerplate/css/less/viewer/cms/views/~~
* ~~/boilerplate/css/less/viewer/views/viewOverview.less~~
* ~~/boilerplate/css/less/viewer/widgets/widgetDownloads.less~~
* ~~/boilerplate/css/less/viewer/components/mobileNavigation.less~~
* ~~/boilerplate/css/less/viewer/components/mobileToggleWrapper.less~~
* ~~/boilerplate/css/less/viewer/components/responsiveColumnGallery.less~~

Änderungen an LESS-Templates.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/widgets/widgetBookshelfList.less

Änderungen an HTML-Templates.

* /boilerplate/template.html
* /boilerplate/templateAdmin.html
* /boilerplate/templateFullscreen.html

## 2019-02-27

Neue LESS-Templates.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/templates/25\_templateOverviewPage.less
* /boilerplate/css/less/viewer/cms/templates/26\_templateOverviewPageLegacy.less

## 2019-02-25

Umstellung der Dateistruktur für das neue Admin-Backend.

* ~~/boilerplate/css/less/viewer/views/admin/~~
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
* ~~/boilerplate/css/less/viewer/cms/modules/options.less~~
* ~~/boilerplate/css/less/viewer/cms/views/cmsMenuItems.less~~
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

* ~~/boilerplate/fullscreenTemplate.html~~
* /boilerplate/template.html
* /boilerplate/templateAdmin.html
* /boilerplate/templateMirador.html
* ~~/boilerplate/templateReadingMode.html~~

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
* ~~/boilerplate/css/less/viewer/views/viewReadingMode.less~~

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
* ~~/boilerplate/css/less/viewer/views/user/userBookshelf.less~~
* /boilerplate/css/less/viewer/views/user/userBookshelfEdit.less
* /boilerplate/css/less/viewer/views/user/userBookshelfSingle.less
* /boilerplate/css/less/viewer/views/user/userBookshelves.less

## 2018-02-08

Neue LESS-Templates.

* /boilerplate/css/less/viewer/constructor.less
* /boilerplate/css/less/viewer/cms/templates/18\_templatePrivacy.less
* /boilerplate/css/less/viewer/cms/templates/19\_templateFeedback.less



