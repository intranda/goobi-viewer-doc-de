# 8.2 Theme changes

## 4.8.0-SNAPSHOT

### Migration auf Bootstrap 4

In den `template*.html` Dateien müssen die CSS und Javascript Ressourcen angepasst werden. Dazu die alten Einträge löschen und die neuen hinzufügen:

**Alt:**

```markup
<link rel="stylesheet" href="#{request.contextPath}/resources/css/libs/bs/bootstrap.min.css" />
<script src="#{request.contextPath}/resources/javascript/libs/bs/bootstrap.min.js"></script>
```

**Neu:**

```markup
<link type="text/css" rel="stylesheet" href="#{request.contextPath}/resources/css/libs/bs/bootstrap.custom.css" />
<script type="text/javascript" src="#{request.contextPath}/resources/javascript/libs/bs/bootstrap.bundle.min.js"></script>
```

Durch die neue Bootstrap Version _können_ an verschiedenen Stellen Struktur- oder Stylingänderung notwendig werden. Insbesondere sind Struktur und Darstellung der Dateien `inlucdes/layout.xhtml` sowie die sonstigen überschriebenen Seiten unter `urlMappings` zu überprüfen.

Die Klasse `.col-xs-` existiert in Bootstrap 4 nicht mehr und sollte über Suchen & Ersetzen zu `.col-` geändert werden. Entsprechend müssen eventuell LESS und gegebenenfalls XHTML Dateien angepasst werden:

* [ ] boilerplate/css/less/views/search/**searchListGrid.less**
* [ ] boilerplate/css/less/views/search/**searchListList.less**
* [ ] boilerplate/css/less/widgets/**widgetGeoLocations.less**
* [ ] boilerplate/css/less/widgets/**widgetSearchDrillDown.less**

Die CSS Klasse `.input-group-addon` existiert ebenso nicht mehr und wird - abhängig davon, ob der Input Button vor- oder nachgelagert im Inputfeld ist - zu `.input-group-append` oder `.input-group-prepend`

* [ ] boilerplate/css/less/views/fullscreen/**fsSearchInCurrentItem.less**
* [ ] boilerplate/css/less/search/search/**searchAdvanced.less**
* [ ] boilerplate/css/less/search/search/**searchList.less**
* [ ] boilerplate/css/less/widgets/**widgetSearchfield.less**
* [ ] boilerplate/css/less/widgets/**widgetSearchInCurrentItem.less**

Aus der CSS Klasse `.label-default` wird `.badge`:

* [ ] boilerplate/css/less/views/fullscreen/**fsUsage.less**
* [ ] boilerplate/css/less/widgets/**widgetUsage.less**

Aus der CSS Klasse `.panel` wird `.card` wobei die Darstellung der Elemente sich erheblich unterscheiden kann:

* [ ] boilerplate/css/less/cms/templates/**15\_templateStackedCollections.less**
* [ ] boilerplate/css/less/cms/templates/**21\_templateFaq.less**
* [ ] boilerplate/css/less/components/**searchHelpText.less**
* [ ] boilerplate/css/less/views/search/**searchStandard.less**
* [ ] boilerplate/css/less/views/**viewDownload.less**

Weiter kann es insbesondere bei folgenden Elementen zu Veränderungen kommen, abhängig vom Design des Themes:

* Bookmarks
* CMS Templates
* Image Controls
* Buttons
* Input Felder

## 4.7.0

### Karten

Für die individuellen Marker auf Karten sowie der oEmbed Anzeige sind die folgenden Anpassungen notwendig. 

Hinzufügen der neuen Template Datei `templateBlank.html`

* [ ] boilerplate/**templateBlank.html**

Hinzufügen des Overlay includes in die `layout.xhtml` nach dem userLogin:

* [ ] boilerplate/includes/**layout.xhtml**

{% code title="layout.xhtml" %}
```markup
<ui:include src="/resources/includes/overlay.xhtml" />
```
{% endcode %}

Hinzufügen der CSS und JS Resourcen für das Leaflet Extra Markers Plugin in die template Dateien:

```markup
<link type="text/css" rel="stylesheet" href="#{request.contextPath}/resources/css/libs/leaflet/extra-markers/leaflet.extra-markers.min.css?${buildNumber}" />
<script type="text/javascript" src="#{request.contextPath}/resources/javascript/libs/leaflet/extra-markers/leaflet.extra-markers.min.js"></script>
```

* [ ] boilerplate/**template.html**
* [ ] boilerplate/**templateAdmin.html**

### Widget für Serien

Das Widget für die Anzeige von Verlinkungen zu Serien / Konvoluten und mehrbändigen Werken wurde umbenannt und die LESS Struktur überarbeitet:

* [ ] boilerplate/css/less/~~widgets~~/~~**widgetConvolutes**~~**.**~~**less**~~
* [ ] boilerplate/css/less/widgets**/widgetRelatedGroups.less**
* [ ] boilerplate/css/less/**constructor.less**

## 4.6.0

### HTML language attribute

Für eine bessere  Sprachunterstützung sollte in den `template*.html` Dateien im `<html>`-Tag der folgende Eintrag ergänzt werden:

```markup
lang="#{navigationHelper.localeString}"
```

* [ ] /boilerplate/**template.html**
* [ ] /boilerplate/**templateAdmin.html**
* [ ] /boilerplate/**templateCrowdsourcing.html**
* [ ] /boilerplate/**templateFullscreen.html**
* [ ] /boilerplate/**templateMirador.html**

### e-pub vs. born-digital

Um besser zwischen dem EPUB-Format für E-Bookreader und E-Publikationen unterscheiden zu können wurde das LESS Template sowie die darin enthaltene CSS-Klasse `e-pub` zu `born-digital` umbenannt:

* [ ] ~~/boilerplate/css/less/components/**ePub.less**~~
* [ ] /boilerplate/css/less/components/**bornDigital.less**
* [ ] /boilerplate/css/less/**constructor.less**

### Timematrix

Die Timematrix wurde refaktorisiert, nutzt nun einen riotJS Tag und folgt den Goobi viewer CSS Konventionen:

* [ ] /boilerplate/css/less/views/**viewTimematrix.less**

### Subthemes

Der Standardwert für Subthemes hat sich verändert, war er früher leer, so ist es nun "-". Aus diesem Grund muss in der `template.html` und der `templateFullscreen.html` die rendered Bedingung angepasst werden:

```markup
rendered="#{navigationHelper.subthemeSelected and navigationHelper.subThemeDiscriminatorValue!='-'}"
```

* [ ] /boilerplate/**template.html**
* [ ] /boilerplate/**templateFullscreen.html**

### Karten

Damit die Kartenunterstützung funktioniert, muss das CSS und JavaScript von Leaflet geladen werden. Dafür sind die folgenden beiden Zeilen in der `template.html` und der `templateAdmin.html` Dateien einzufügen:

```markup
<link type="text/css" rel="stylesheet" href="#{request.contextPath}/resources/css/libs/leaflet/leaflet.css?${buildNumber}" />
<script type="text/javascript" src="#{request.contextPath}/resources/javascript/libs/leaflet/leaflet.js"></script>
```

* [ ] /boilerplate/**template.html**
* [ ] /boilerplate/**templateAdmin.html**

Eventuell vorhandene Referenzen zu dem alten Geokoordinaten-Widget in individuellen Seiten oder Templates müssen gelöscht werden. Der Code lautet:

```markup
<widgetComponent:widget_geoLocations widget="#{element}" />
```



### CSS für 3D-Objekte

* [ ] /boilerplate/css/less/views/**viewObject.less**

## 4.5.0

### MapBox Token

In der Datei `customJS.xhtml` folgende Zeile bei der Deklaration der Javascript-Variablen ergänzen:

```markup
var mapBoxToken = "#{configurationBean.mapBoxToken}";
```

## 4.4.0

### Javascript Library Update in template-Dateien

In den `template*.html` Dateien die folgende Zeile ersetzen:

**Alt:**

```markup
<script src="#{request.contextPath}/resources/javascript/libs/reactiveX/rx.lite.min.js"></script>
```

**Neu:**

```markup
<script src="#{request.contextPath}/resources/javascript/libs/reactiveX/rxjs.umd.min.js"></script>
```

Aufgrund von Änderungen im Core ist es außerdem gut das Styling der folgenden Elemente zu prüfen:

* widget-chronology-slider \(Facettierung nach Zeitraum in der Suche\)
* currentSearchForm \(Sucheingabefeld auf Suchtrefferliste bei öffnen von Sammlung\)

### **Änderungen an der custom.js und customJS.xhtml:**

Löschen des folgenden Blocks aus der `custom.js`:

{% code title="custom.js" %}
```javascript
// init bookmarks if enabled
if ( bookshelvesEnabled ) {
    viewerJS.bookmarks.init( watchlistConfig );
}
```
{% endcode %}

Suchen und Ersetzen des folgenden Blocks in der `customJS.xhtml.`

**Suchen**:

{% code title="customJS.xhtml" %}
```javascript
var bookshelvesEnabled = #{configurationBean.bookshelvesEnabled};
var watchlistConfig = {
    root: "#{request.contextPath}",
    msg: {
        resetBookmarkLists: "#{msg.bookmarkList_reset}",
        deleteBookmarkList: "#{msg.bookmarkList_delete}",
        sendBookmarkList: "#{msg.bookmarkList_session_mail_sendList}",
        searchInBookmarkList: "#{msg.action__search_in_bookmarks}",
        resetBookmarkListsConfirm: "#{msg.bookmarkList_resetConfirm}",
        noItemsAvailable: "#{msg.bookmarkList_noItemsAvailable}",
        selectBookmarkList: "#{msg.bookmarkList_selectBookmarkList}",
        addNewBookmarkList: "#{msg.bookmarkList_addNewBookmarkList}",
        openInMirador: "#{msg.bookmarkList_openMirador}",
        type_label: "#{msg.bookmarkList_type_label}",
        typeRecord: "#{msg.bookmarkList_typeRecord}",
        typePage: "#{msg.bookmarkList_typePage}"
    },
    userLoggedIn: userLoggedIn
};
```
{% endcode %}

**Ersetzen**:

{% code title="customJS.xhtml" %}
```javascript
var bookmarksEnabled = #{configurationBean.bookmarksEnabled};
var rootURL = "#{request.contextPath}";
var restURL = "#{configurationBean.restApiUrl}";
```
{% endcode %}

### **Änderungen an LESS Templates:**

* /boilerplate/css/less/constructor.less
  * -&gt; build.less umbenennen zu constructor.less \(falls Dateiname = build.less\)
* /boilerplate/Gruntfile.js
  * Sofern die build.less umbenannt wurde, in der Gruntfile nach build.less suchen und durch constructor.less ersetzen
* -&gt; Dateinamen aus der folgenden Auflistung umbenennen

Durch die Refaktorisierung der Bücherregale/Merklisten müssen die folgenden LESS Templates umbenannt werden:

* /boilerplate/css/less/constructor.less
* /boilerplate/css/less/components/**bookshelves.less → bookmarks.less**
* /boilerplate/css/less/views/user/**userBookshelfEdit.less → userBookmarkEdit.less**
* /boilerplate/css/less/views/user/**userBookshelfSendList.less → userBookmarkSendList.less**
* /boilerplate/css/less/views/user/**userBookshelfSingle.less → userBookmarkSingle.less**
* /boilerplate/css/less/views/user/**userBookshelves.less → userBookmarks.less**
* ~~/boilerplate/css/less/views/user/userBookshelfOther.less~~
* ~~/boilerplate/css/less/widgets/widgetBookshelfList.less~~
* ~~/boilerplate/css/less/widgets/widgetBookshelves.less~~

### **Anpassung der Klassennamen:**

#### **bookmarks.less**

| Alt | Neu |
| :--- | :--- |
| .bookshelf-navigation | .bookmark-navigation |
| .bookshelf-popup | .bookmark-popup |

#### **imageControls.less**

| Alt | Neu |
| :--- | :--- |
| .add-to-bookshelf | .add-to-bookmark |

#### **userBookmarkEdit.less**

| Alt | Neu |
| :--- | :--- |
| .user-bookshelf-edit | .user-bookmark-edit |

#### **userBookmarks.less**

| Alt | Neu |
| :--- | :--- |
| .user-bookshelves | .user-bookmark |
| &add-bookshelf | &add-bookmark |

#### **userBookmarkSendList.less**

| Alt | Neu |
| :--- | :--- |
| .user-bookshelf-send-list | .user-bookmark-send-list |

#### **userBookmarkSingle.less**

| Alt | Neu |
| :--- | :--- |
| .view-bookshelf | .view-bookmark |

### **Weitere Änderungen im Theme:**

* In der layout.xhtml die Komponente `<viewerComponent:bookshelfNavigation />` umbenennen zu `<viewerComponent:bookmarkListNavigation />`
* In der **pageheader.xhtml** oder **layout.xhtml** prüfen ob in dem div mit der Klasse topactions -&gt; whatchlist existiert und gegebenenfalls watchlist zu bookmark ändern
* `data-` __Attribute mit bookshel\* löschen

Links zu Anchor und Serienwerken werden nun standardmäßig angezeigt. Deswegen das `display:none;` und `visibility:hidden;` entfernen:

* /boilerplate/css/less/widgets/widgetConvolutes.less

Das Widget zum Facettieren nach Zeitraum wurde umgebaut:

* /boilerplate/css/less/widgets/widgetChronology.less

## 2019-12-02

Folgende Komponenten sind im Core entfernt worden:

* `resources/components/widgets/widget_bookshelves.xhtml`
* `resources/components/widgets/widget_bookshelfList.xhtml`
* `resources/components/widgets/widget_mySearches.xhtml`
* `resources/components/dialogAddToBookshelf.xhtml`

Die entsprechenden Includes müssen aus den HTML/XHTML Dateien der Themes entfernt werden.

Änderung an LESS-Templates:

* boilerplate/css/less/build.less
* ~~boilerplate/css/less/widgets/widgetBookshelves.less~~
* ~~boilerplate/css/less/widgets/widgetBookshelfList.less~~
* ~~boilerplate/css/less/widgets/widgetMySearches.less~~

 Die entsprechenden Funktionalitäten können im Login-Menü hinzugefügt werden \(vgl. Reference-Theme\).

## 2019-11-29

In die Datei template.html folgende Zeile einfügen:

```markup
    <script type="text/javascript" src="#{request.contextPath}/resources/javascript/dist/browsersupport.min.js"></script>
```

Am besten oberhalb der Zeile, die das viewer.min.js Script einbindet.

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
* /boilerplate/css/less/constructor.less
* /boilerplate/css/less/components/loginNavigation.less
* ~~/boilerplate/css/less/components/modals.less~~
* /boilerplate/css/less/views/user/user.less
* ~~/boilerplate/css/less/views/user/userData.less~~
* ~~/boilerplate/css/less/views/user/userAccountCreate.less~~
* ~~/boilerplate/css/less/views/user/userAccountRetrieve.less~~

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

* /boilerplate/css/less/views/user/userLogin.less
* /boilerplate/css/less/constructor.less

Entfernung des Widgets **widget\_user.xhtml** aus den Seitenleisten der XHTML-Dateien.

* /boilerplate/pages/styles.xhtml
* /boilerplate/pages/templateStaticPage.xhtml
* /boilerplate/urlMappings/index.xhtml

Änderung an LESS-Templates.

* ~~/boilerplate/css/less/widgets/widgetUser.less~~
* /boilerplate/css/less/constructor.less

## 2019-04-17

Änderungen an LESS-Templates.

* /boilerplate/css/less/widgets/widgetSearchDrillDown.less

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

* /boilerplate/css/less/widgets/widgets.less

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



