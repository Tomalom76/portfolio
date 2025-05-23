
# Analiza Danych EDA Titanica: Eksploracja Domenowa

Data wykonania projektu: luty/marzec 2025

  Analiza danych osób, które przeżyły bądź nie przeżyły katastrofy statku Titanic dnia 12.04.1912 roku.
  Jest to czysta analiza danych wywnioskowana z tabeli ofiar tragedii. Na różnych wykres i tablicach można
  ocenić różne aspekty przetrwania, np. kto i z jakiej klasy pasażerskiej miał większą szansę przeżyć tragedię.
  Zachęcam do zapoznania się z treścią notebooka, który można sobie pobrać poniżej.


<a href="Titanic.ipynb" class="md-button md-button--primary">Pobierz Notebook</a>
<a href="26__titanic.csv" class="md-button md-button--primary">Pobierz Plik Bazy Danych</a>

<!DOCTYPE html>

<html lang="en">
<head><meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Titanic</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .pm { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation.Marker */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
  scrollbar-width: thin;
}

/* tiny scrollbar */

.jp-scrollbar-tiny::-webkit-scrollbar,
.jp-scrollbar-tiny::-webkit-scrollbar-corner {
  background-color: transparent;
  height: 4px;
  width: 4px;
}

.jp-scrollbar-tiny::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:horizontal {
  border-left: 0 solid transparent;
  border-right: 0 solid transparent;
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:vertical {
  border-top: 0 solid transparent;
  border-bottom: 0 solid transparent;
}

/*
 * Lumino
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
}

.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.lm-AccordionPanel[data-orientation='horizontal'] > .lm-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-CommandPalette-search {
  flex: 0 0 auto;
}

.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}

.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}

.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}

.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-close-icon {
  border: 1px solid transparent;
  background-color: transparent;
  position: absolute;
  z-index: 1;
  right: 3%;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 7px 0;
  display: none;
  vertical-align: middle;
  outline: 0;
  cursor: pointer;
}
.lm-close-icon:after {
  content: 'X';
  display: block;
  width: 15px;
  height: 15px;
  text-align: center;
  color: #000;
  font-weight: normal;
  font-size: 12px;
  cursor: pointer;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-DockPanel {
  z-index: 0;
}

.lm-DockPanel-widget {
  z-index: 0;
}

.lm-DockPanel-tabBar {
  z-index: 1;
}

.lm-DockPanel-handle {
  z-index: 2;
}

.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}

.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}

.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}

.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}

.lm-Menu-item {
  display: table-row;
}

.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}

.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}

.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}

.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

.lm-MenuBar-item {
  box-sizing: border-box;
}

.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}

.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}

.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}

.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}

.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-SplitPanel-child {
  z-index: 0;
}

.lm-SplitPanel-handle {
  z-index: 1;
}

.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
  align-items: flex-end;
}

.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
  align-items: flex-end;
}

.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}

.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}

.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}

.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
  touch-action: none; /* Disable native Drag/Drop */
}

.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}

.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

.lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
}

.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar-addButton.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}

.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}

.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

.lm-TabBar-tabLabel .lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
  background: inherit;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabPanel-tabBar {
  z-index: 1;
}

.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.jp-Collapse-header {
  padding: 1px 12px;
  background-color: var(--jp-layout-color1);
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  text-transform: uppercase;
  user-select: none;
}

.jp-Collapser-icon {
  height: 16px;
}

.jp-Collapse-header-collapsed .jp-Collapser-icon {
  transform: rotate(-90deg);
  margin: auto 0;
}

.jp-Collapser-title {
  line-height: 25px;
}

.jp-Collapse-contents {
  padding: 0 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add-above: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5MikiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik00Ljc1IDQuOTMwNjZINi42MjVWNi44MDU2NkM2LjYyNSA3LjAxMTkxIDYuNzkzNzUgNy4xODA2NiA3IDcuMTgwNjZDNy4yMDYyNSA3LjE4MDY2IDcuMzc1IDcuMDExOTEgNy4zNzUgNi44MDU2NlY0LjkzMDY2SDkuMjVDOS40NTYyNSA0LjkzMDY2IDkuNjI1IDQuNzYxOTEgOS42MjUgNC41NTU2NkM5LjYyNSA0LjM0OTQxIDkuNDU2MjUgNC4xODA2NiA5LjI1IDQuMTgwNjZINy4zNzVWMi4zMDU2NkM3LjM3NSAyLjA5OTQxIDcuMjA2MjUgMS45MzA2NiA3IDEuOTMwNjZDNi43OTM3NSAxLjkzMDY2IDYuNjI1IDIuMDk5NDEgNi42MjUgMi4zMDU2NlY0LjE4MDY2SDQuNzVDNC41NDM3NSA0LjE4MDY2IDQuMzc1IDQuMzQ5NDEgNC4zNzUgNC41NTU2NkM0LjM3NSA0Ljc2MTkxIDQuNTQzNzUgNC45MzA2NiA0Ljc1IDQuOTMwNjZaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC43Ii8+CjwvZz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgOS41VjExLjVMMi41IDExLjVWOS41TDExLjUgOS41Wk0xMiA4QzEyLjU1MjMgOCAxMyA4LjQ0NzcyIDEzIDlWMTJDMTMgMTIuNTUyMyAxMi41NTIzIDEzIDEyIDEzTDIgMTNDMS40NDc3MiAxMyAxIDEyLjU1MjMgMSAxMlY5QzEgOC40NDc3MiAxLjQ0NzcxIDggMiA4TDEyIDhaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5MiI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KC0xIDAgMCAxIDEwIDEuNTU1NjYpIi8+CjwvY2xpcFBhdGg+CjwvZGVmcz4KPC9zdmc+Cg==);
  --jp-icon-add-below: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5OCkiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik05LjI1IDEwLjA2OTNMNy4zNzUgMTAuMDY5M0w3LjM3NSA4LjE5NDM0QzcuMzc1IDcuOTg4MDkgNy4yMDYyNSA3LjgxOTM0IDcgNy44MTkzNEM2Ljc5Mzc1IDcuODE5MzQgNi42MjUgNy45ODgwOSA2LjYyNSA4LjE5NDM0TDYuNjI1IDEwLjA2OTNMNC43NSAxMC4wNjkzQzQuNTQzNzUgMTAuMDY5MyA0LjM3NSAxMC4yMzgxIDQuMzc1IDEwLjQ0NDNDNC4zNzUgMTAuNjUwNiA0LjU0Mzc1IDEwLjgxOTMgNC43NSAxMC44MTkzTDYuNjI1IDEwLjgxOTNMNi42MjUgMTIuNjk0M0M2LjYyNSAxMi45MDA2IDYuNzkzNzUgMTMuMDY5MyA3IDEzLjA2OTNDNy4yMDYyNSAxMy4wNjkzIDcuMzc1IDEyLjkwMDYgNy4zNzUgMTIuNjk0M0w3LjM3NSAxMC44MTkzTDkuMjUgMTAuODE5M0M5LjQ1NjI1IDEwLjgxOTMgOS42MjUgMTAuNjUwNiA5LjYyNSAxMC40NDQzQzkuNjI1IDEwLjIzODEgOS40NTYyNSAxMC4wNjkzIDkuMjUgMTAuMDY5M1oiIGZpbGw9IiM2MTYxNjEiIHN0cm9rZT0iIzYxNjE2MSIgc3Ryb2tlLXdpZHRoPSIwLjciLz4KPC9nPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMi41IDUuNUwyLjUgMy41TDExLjUgMy41TDExLjUgNS41TDIuNSA1LjVaTTIgN0MxLjQ0NzcyIDcgMSA2LjU1MjI4IDEgNkwxIDNDMSAyLjQ0NzcyIDEuNDQ3NzIgMiAyIDJMMTIgMkMxMi41NTIzIDIgMTMgMi40NDc3MiAxMyAzTDEzIDZDMTMgNi41NTIyOSAxMi41NTIzIDcgMTIgN0wyIDdaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5OCI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KDEgMS43NDg0NmUtMDcgMS43NDg0NmUtMDcgLTEgNCAxMy40NDQzKSIvPgo8L2NsaXBQYXRoPgo8L2RlZnM+Cjwvc3ZnPgo=);
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bell: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE2IDE2IiB2ZXJzaW9uPSIxLjEiPgogICA8cGF0aCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzMzMzMzIgogICAgICBkPSJtOCAwLjI5Yy0xLjQgMC0yLjcgMC43My0zLjYgMS44LTEuMiAxLjUtMS40IDMuNC0xLjUgNS4yLTAuMTggMi4yLTAuNDQgNC0yLjMgNS4zbDAuMjggMS4zaDVjMC4wMjYgMC42NiAwLjMyIDEuMSAwLjcxIDEuNSAwLjg0IDAuNjEgMiAwLjYxIDIuOCAwIDAuNTItMC40IDAuNi0xIDAuNzEtMS41aDVsMC4yOC0xLjNjLTEuOS0wLjk3LTIuMi0zLjMtMi4zLTUuMy0wLjEzLTEuOC0wLjI2LTMuNy0xLjUtNS4yLTAuODUtMS0yLjItMS44LTMuNi0xLjh6bTAgMS40YzAuODggMCAxLjkgMC41NSAyLjUgMS4zIDAuODggMS4xIDEuMSAyLjcgMS4yIDQuNCAwLjEzIDEuNyAwLjIzIDMuNiAxLjMgNS4yaC0xMGMxLjEtMS42IDEuMi0zLjQgMS4zLTUuMiAwLjEzLTEuNyAwLjMtMy4zIDEuMi00LjQgMC41OS0wLjcyIDEuNi0xLjMgMi41LTEuM3ptLTAuNzQgMTJoMS41Yy0wLjAwMTUgMC4yOCAwLjAxNSAwLjc5LTAuNzQgMC43OS0wLjczIDAuMDAxNi0wLjcyLTAuNTMtMC43NC0wLjc5eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-bug-dot: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiPgogICAgICAgIDxwYXRoIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMTcuMTkgOEgyMFYxMEgxNy45MUMxNy45NiAxMC4zMyAxOCAxMC42NiAxOCAxMVYxMkgyMFYxNEgxOC41SDE4VjE0LjAyNzVDMTUuNzUgMTQuMjc2MiAxNCAxNi4xODM3IDE0IDE4LjVDMTQgMTkuMjA4IDE0LjE2MzUgMTkuODc3OSAxNC40NTQ5IDIwLjQ3MzlDMTMuNzA2MyAyMC44MTE3IDEyLjg3NTcgMjEgMTIgMjFDOS43OCAyMSA3Ljg1IDE5Ljc5IDYuODEgMThINFYxNkg2LjA5QzYuMDQgMTUuNjcgNiAxNS4zNCA2IDE1VjE0SDRWMTJINlYxMUM2IDEwLjY2IDYuMDQgMTAuMzMgNi4wOSAxMEg0VjhINi44MUM3LjI2IDcuMjIgNy44OCA2LjU1IDguNjIgNi4wNEw3IDQuNDFMOC40MSAzTDEwLjU5IDUuMTdDMTEuMDQgNS4wNiAxMS41MSA1IDEyIDVDMTIuNDkgNSAxMi45NiA1LjA2IDEzLjQyIDUuMTdMMTUuNTkgM0wxNyA0LjQxTDE1LjM3IDYuMDRDMTYuMTIgNi41NSAxNi43NCA3LjIyIDE3LjE5IDhaTTEwIDE2SDE0VjE0SDEwVjE2Wk0xMCAxMkgxNFYxMEgxMFYxMloiIGZpbGw9IiM2MTYxNjEiLz4KICAgICAgICA8cGF0aCBkPSJNMjIgMTguNUMyMiAyMC40MzMgMjAuNDMzIDIyIDE4LjUgMjJDMTYuNTY3IDIyIDE1IDIwLjQzMyAxNSAxOC41QzE1IDE2LjU2NyAxNi41NjcgMTUgMTguNSAxNUMyMC40MzMgMTUgMjIgMTYuNTY3IDIyIDE4LjVaIiBmaWxsPSIjNjE2MTYxIi8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yMCA4aC0yLjgxYy0uNDUtLjc4LTEuMDctMS40NS0xLjgyLTEuOTZMMTcgNC40MSAxNS41OSAzbC0yLjE3IDIuMTdDMTIuOTYgNS4wNiAxMi40OSA1IDEyIDVjLS40OSAwLS45Ni4wNi0xLjQxLjE3TDguNDEgMyA3IDQuNDFsMS42MiAxLjYzQzcuODggNi41NSA3LjI2IDcuMjIgNi44MSA4SDR2MmgyLjA5Yy0uMDUuMzMtLjA5LjY2LS4wOSAxdjFINHYyaDJ2MWMwIC4zNC4wNC42Ny4wOSAxSDR2MmgyLjgxYzEuMDQgMS43OSAyLjk3IDMgNS4xOSAzczQuMTUtMS4yMSA1LjE5LTNIMjB2LTJoLTIuMDljLjA1LS4zMy4wOS0uNjYuMDktMXYtMWgydi0yaC0ydi0xYzAtLjM0LS4wNC0uNjctLjA5LTFIMjBWOHptLTYgOGgtNHYtMmg0djJ6bTAtNGgtNHYtMmg0djJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik05IDE2LjE3TDQuODMgMTJsLTEuNDIgMS40MUw5IDE5IDIxIDdsLTEuNDEtMS40MXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBzaGFwZS1yZW5kZXJpbmc9Imdlb21ldHJpY1ByZWNpc2lvbiI+CiAgICA8cGF0aCBkPSJNNi41OSwzLjQxTDIsOEw2LjU5LDEyLjZMOCwxMS4xOEw0LjgyLDhMOCw0LjgyTDYuNTksMy40MU0xMi40MSwzLjQxTDExLDQuODJMMTQuMTgsOEwxMSwxMS4xOEwxMi40MSwxMi42TDE3LDhMMTIuNDEsMy40MU0yMS41OSwxMS41OUwxMy41LDE5LjY4TDkuODMsMTZMOC40MiwxNy40MUwxMy41LDIyLjVMMjMsMTNMMjEuNTksMTEuNTlaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTExLjQgMTguNkw2LjggMTRMMTEuNCA5LjRMMTAgOEw0IDE0TDEwIDIwTDExLjQgMTguNlpNMTYuNiAxOC42TDIxLjIgMTRMMTYuNiA5LjRMMTggOEwyNCAxNEwxOCAyMEwxNi42IDE4LjZWMTguNloiLz4KCTwvZz4KPC9zdmc+Cg==);
  --jp-icon-collapse-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNNiAxM3YyaDh2LTJ6IiAvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1jb25zb2xlLWljb24tYmFja2dyb3VuZC1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtY29uc29sZS1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIj4KICAgIDxwYXRoIGQ9Ik0xMDUgMTI3LjNoNDB2MTIuOGgtNDB6TTUxLjEgNzdMNzQgOTkuOWwtMjMuMyAyMy4zIDEwLjUgMTAuNSAyMy4zLTIzLjNMOTUgOTkuOSA4NC41IDg5LjQgNjEuNiA2Ni41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copyright: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCI+CiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0xMS44OCw5LjE0YzEuMjgsMC4wNiwxLjYxLDEuMTUsMS42MywxLjY2aDEuNzljLTAuMDgtMS45OC0xLjQ5LTMuMTktMy40NS0zLjE5QzkuNjQsNy42MSw4LDksOCwxMi4xNCBjMCwxLjk0LDAuOTMsNC4yNCwzLjg0LDQuMjRjMi4yMiwwLDMuNDEtMS42NSwzLjQ0LTIuOTVoLTEuNzljLTAuMDMsMC41OS0wLjQ1LDEuMzgtMS42MywxLjQ0QzEwLjU1LDE0LjgzLDEwLDEzLjgxLDEwLDEyLjE0IEMxMCw5LjI1LDExLjI4LDkuMTYsMTEuODgsOS4xNHogTTEyLDJDNi40OCwyLDIsNi40OCwyLDEyczQuNDgsMTAsMTAsMTBzMTAtNC40OCwxMC0xMFMxNy41MiwyLDEyLDJ6IE0xMiwyMGMtNC40MSwwLTgtMy41OS04LTggczMuNTktOCw4LThzOCwzLjU5LDgsOFMxNi40MSwyMCwxMiwyMHoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-delete: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CiAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIiAvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjI2MjYyIiBkPSJNNiAxOWMwIDEuMS45IDIgMiAyaDhjMS4xIDAgMi0uOSAyLTJWN0g2djEyek0xOSA0aC0zLjVsLTEtMWgtNWwtMSAxSDV2MmgxNFY0eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-duplicate: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTIuNzk5OTggMC44NzVIOC44OTU4MkM5LjIwMDYxIDAuODc1IDkuNDQ5OTggMS4xMzkxNCA5LjQ0OTk4IDEuNDYxOThDOS40NDk5OCAxLjc4NDgyIDkuMjAwNjEgMi4wNDg5NiA4Ljg5NTgyIDIuMDQ4OTZIMy4zNTQxNUMzLjA0OTM2IDIuMDQ4OTYgMi43OTk5OCAyLjMxMzEgMi43OTk5OCAyLjYzNTk0VjkuNjc5NjlDMi43OTk5OCAxMC4wMDI1IDIuNTUwNjEgMTAuMjY2NyAyLjI0NTgyIDEwLjI2NjdDMS45NDEwMyAxMC4yNjY3IDEuNjkxNjUgMTAuMDAyNSAxLjY5MTY1IDkuNjc5NjlWMi4wNDg5NkMxLjY5MTY1IDEuNDAzMjggMi4xOTA0IDAuODc1IDIuNzk5OTggMC44NzVaTTUuMzY2NjUgMTEuOVY0LjU1SDExLjA4MzNWMTEuOUg1LjM2NjY1Wk00LjE0MTY1IDQuMTQxNjdDNC4xNDE2NSAzLjY5MDYzIDQuNTA3MjggMy4zMjUgNC45NTgzMiAzLjMyNUgxMS40OTE3QzExLjk0MjcgMy4zMjUgMTIuMzA4MyAzLjY5MDYzIDEyLjMwODMgNC4xNDE2N1YxMi4zMDgzQzEyLjMwODMgMTIuNzU5NCAxMS45NDI3IDEzLjEyNSAxMS40OTE3IDEzLjEyNUg0Ljk1ODMyQzQuNTA3MjggMTMuMTI1IDQuMTQxNjUgMTIuNzU5NCA0LjE0MTY1IDEyLjMwODNWNC4xNDE2N1oiIGZpbGw9IiM2MTYxNjEiLz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNOS40MzU3NCA4LjI2NTA3SDguMzY0MzFWOS4zMzY1QzguMzY0MzEgOS40NTQzNSA4LjI2Nzg4IDkuNTUwNzggOC4xNTAwMiA5LjU1MDc4QzguMDMyMTcgOS41NTA3OCA3LjkzNTc0IDkuNDU0MzUgNy45MzU3NCA5LjMzNjVWOC4yNjUwN0g2Ljg2NDMxQzYuNzQ2NDUgOC4yNjUwNyA2LjY1MDAyIDguMTY4NjQgNi42NTAwMiA4LjA1MDc4QzYuNjUwMDIgNy45MzI5MiA2Ljc0NjQ1IDcuODM2NSA2Ljg2NDMxIDcuODM2NUg3LjkzNTc0VjYuNzY1MDdDNy45MzU3NCA2LjY0NzIxIDguMDMyMTcgNi41NTA3OCA4LjE1MDAyIDYuNTUwNzhDOC4yNjc4OCA2LjU1MDc4IDguMzY0MzEgNi42NDcyMSA4LjM2NDMxIDYuNzY1MDdWNy44MzY1SDkuNDM1NzRDOS41NTM2IDcuODM2NSA5LjY1MDAyIDcuOTMyOTIgOS42NTAwMiA4LjA1MDc4QzkuNjUwMDIgOC4xNjg2NCA5LjU1MzYgOC4yNjUwNyA5LjQzNTc0IDguMjY1MDdaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC41Ii8+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-error: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjE5IiByPSIyIi8+PHBhdGggZD0iTTEwIDNoNHYxMmgtNHoiLz48L2c+CjxwYXRoIGZpbGw9Im5vbmUiIGQ9Ik0wIDBoMjR2MjRIMHoiLz4KPC9zdmc+Cg==);
  --jp-icon-expand-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNMTEgMTBIOXYzSDZ2MmgzdjNoMnYtM2gzdi0yaC0zeiIgLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-dot: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWRvdCIgZmlsbD0iI0ZGRiI+CiAgICA8Y2lyY2xlIGN4PSIxOCIgY3k9IjE3IiByPSIzIj48L2NpcmNsZT4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-filter: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-folder-favorite: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgwVjB6IiBmaWxsPSJub25lIi8+PHBhdGggY2xhc3M9ImpwLWljb24zIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxNjE2MSIgZD0iTTIwIDZoLThsLTItMkg0Yy0xLjEgMC0yIC45LTIgMnYxMmMwIDEuMS45IDIgMiAyaDE2YzEuMSAwIDItLjkgMi0yVjhjMC0xLjEtLjktMi0yLTJ6bS0yLjA2IDExTDE1IDE1LjI4IDEyLjA2IDE3bC43OC0zLjMzLTIuNTktMi4yNCAzLjQxLS4yOUwxNSA4bDEuMzQgMy4xNCAzLjQxLjI5LTIuNTkgMi4yNC43OCAzLjMzeiIvPgo8L3N2Zz4K);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-home: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPjxwYXRoIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xMCAyMHYtNmg0djZoNXYtOGgzTDEyIDMgMiAxMmgzdjh6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-info: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUwLjk3OCA1MC45NzgiPgoJPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KCQk8cGF0aCBkPSJNNDMuNTIsNy40NThDMzguNzExLDIuNjQ4LDMyLjMwNywwLDI1LjQ4OSwwQzE4LjY3LDAsMTIuMjY2LDIuNjQ4LDcuNDU4LDcuNDU4CgkJCWMtOS45NDMsOS45NDEtOS45NDMsMjYuMTE5LDAsMzYuMDYyYzQuODA5LDQuODA5LDExLjIxMiw3LjQ1NiwxOC4wMzEsNy40NThjMCwwLDAuMDAxLDAsMC4wMDIsMAoJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoKCQkJIE00Mi4xMDYsNDIuMTA1Yy00LjQzMiw0LjQzMS0xMC4zMzIsNi44NzItMTYuNjE1LDYuODcyaC0wLjAwMmMtNi4yODUtMC4wMDEtMTIuMTg3LTIuNDQxLTE2LjYxNy02Ljg3MgoJCQljLTkuMTYyLTkuMTYzLTkuMTYyLTI0LjA3MSwwLTMzLjIzM0MxMy4zMDMsNC40NCwxOS4yMDQsMiwyNS40ODksMmM2LjI4NCwwLDEyLjE4NiwyLjQ0LDE2LjYxNyw2Ljg3MgoJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4KCQk8cGF0aCBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1MwoJCQljMC40NjgtMC41MzYsMC45MjMtMS4wNjIsMS4zNjctMS41NzVjMC42MjYtMC43NTMsMS4xMDQtMS40NzgsMS40MzYtMi4xNzVjMC4zMzEtMC43MDcsMC40OTUtMS41NDEsMC40OTUtMi41CgkJCWMwLTEuMDk2LTAuMjYtMi4wODgtMC43NzktMi45NzljLTAuNTY1LTAuODc5LTEuNTAxLTEuMzM2LTIuODA2LTEuMzY5Yy0xLjgwMiwwLjA1Ny0yLjk4NSwwLjY2Ny0zLjU1LDEuODMyCgkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkKCQkJYzEuMDYyLTEuNjQsMi44NTUtMi40ODEsNS4zNzgtMi41MjdjMi4xNiwwLjAyMywzLjg3NCwwLjYwOCw1LjE0MSwxLjc1OGMxLjI3OCwxLjE2LDEuOTI5LDIuNzY0LDEuOTUsNC44MTEKCQkJYzAsMS4xNDItMC4xMzcsMi4xMTEtMC40MSwyLjkxMWMtMC4zMDksMC44NDUtMC43MzEsMS41OTMtMS4yNjgsMi4yNDNjLTAuNDkyLDAuNjUtMS4wNjgsMS4zMTgtMS43MywyLjAwMgoJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5CgkJCUMyNi41ODksMzIuMjE4LDIzLjU3OCwzMi4yMTgsMjMuNTc4LDMyLjIxOHogTTIzLjU3OCwzOC4yMnYtMy40ODRoMy4wNzZ2My40ODRIMjMuNTc4eiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaW5zcGVjdG9yLWljb24tY29sb3IganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtanNvbi1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0Y5QTgyNSI+CiAgICA8cGF0aCBkPSJNMjAuMiAxMS44Yy0xLjYgMC0xLjcuNS0xLjcgMSAwIC40LjEuOS4xIDEuMy4xLjUuMS45LjEgMS4zIDAgMS43LTEuNCAyLjMtMy41IDIuM2gtLjl2LTEuOWguNWMxLjEgMCAxLjQgMCAxLjQtLjggMC0uMyAwLS42LS4xLTEgMC0uNC0uMS0uOC0uMS0xLjIgMC0xLjMgMC0xLjggMS4zLTItMS4zLS4yLTEuMy0uNy0xLjMtMiAwLS40LjEtLjguMS0xLjIuMS0uNC4xLS43LjEtMSAwLS44LS40LS43LTEuNC0uOGgtLjVWNC4xaC45YzIuMiAwIDMuNS43IDMuNSAyLjMgMCAuNC0uMS45LS4xIDEuMy0uMS41LS4xLjktLjEgMS4zIDAgLjUuMiAxIDEuNyAxdjEuOHpNMS44IDEwLjFjMS42IDAgMS43LS41IDEuNy0xIDAtLjQtLjEtLjktLjEtMS4zLS4xLS41LS4xLS45LS4xLTEuMyAwLTEuNiAxLjQtMi4zIDMuNS0yLjNoLjl2MS45aC0uNWMtMSAwLTEuNCAwLTEuNC44IDAgLjMgMCAuNi4xIDEgMCAuMi4xLjYuMSAxIDAgMS4zIDAgMS44LTEuMyAyQzYgMTEuMiA2IDExLjcgNiAxM2MwIC40LS4xLjgtLjEgMS4yLS4xLjMtLjEuNy0uMSAxIDAgLjguMy44IDEuNC44aC41djEuOWgtLjljLTIuMSAwLTMuNS0uNi0zLjUtMi4zIDAtLjQuMS0uOS4xLTEuMy4xLS41LjEtLjkuMS0xLjMgMC0uNS0uMi0xLTEuNy0xdi0xLjl6Ii8+CiAgICA8Y2lyY2xlIGN4PSIxMSIgY3k9IjEzLjgiIHI9IjIuMSIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSI4LjIiIHI9IjIuMSIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-julia: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDMyNSAzMDAiPgogIDxnIGNsYXNzPSJqcC1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjY2IzYzMzIj4KICAgIDxwYXRoIGQ9Ik0gMTUwLjg5ODQzOCAyMjUgQyAxNTAuODk4NDM4IDI2Ni40MjE4NzUgMTE3LjMyMDMxMiAzMDAgNzUuODk4NDM4IDMwMCBDIDM0LjQ3NjU2MiAzMDAgMC44OTg0MzggMjY2LjQyMTg3NSAwLjg5ODQzOCAyMjUgQyAwLjg5ODQzOCAxODMuNTc4MTI1IDM0LjQ3NjU2MiAxNTAgNzUuODk4NDM4IDE1MCBDIDExNy4zMjAzMTIgMTUwIDE1MC44OTg0MzggMTgzLjU3ODEyNSAxNTAuODk4NDM4IDIyNSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzM4OTgyNiI+CiAgICA8cGF0aCBkPSJNIDIzNy41IDc1IEMgMjM3LjUgMTE2LjQyMTg3NSAyMDMuOTIxODc1IDE1MCAxNjIuNSAxNTAgQyAxMjEuMDc4MTI1IDE1MCA4Ny41IDExNi40MjE4NzUgODcuNSA3NSBDIDg3LjUgMzMuNTc4MTI1IDEyMS4wNzgxMjUgMCAxNjIuNSAwIEMgMjAzLjkyMTg3NSAwIDIzNy41IDMzLjU3ODEyNSAyMzcuNSA3NSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzk1NThiMiI+CiAgICA8cGF0aCBkPSJNIDMyNC4xMDE1NjIgMjI1IEMgMzI0LjEwMTU2MiAyNjYuNDIxODc1IDI5MC41MjM0MzggMzAwIDI0OS4xMDE1NjIgMzAwIEMgMjA3LjY3OTY4OCAzMDAgMTc0LjEwMTU2MiAyNjYuNDIxODc1IDE3NC4xMDE1NjIgMjI1IEMgMTc0LjEwMTU2MiAxODMuNTc4MTI1IDIwNy42Nzk2ODggMTUwIDI0OS4xMDE1NjIgMTUwIEMgMjkwLjUyMzQzOCAxNTAgMzI0LjEwMTU2MiAxODMuNTc4MTI1IDMyNC4xMDE1NjIgMjI1Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgPGcgY2xhc3M9ImpwLWp1cHl0ZXItaWNvbi1jb2xvciIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgIDxnIGNsYXNzPSJqcC1qdXB5dGVyLWljb24tY29sb3IiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launch: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMzIgMzIiIHdpZHRoPSIzMiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yNiwyOEg2YTIuMDAyNywyLjAwMjcsMCwwLDEtMi0yVjZBMi4wMDI3LDIuMDAyNywwLDAsMSw2LDRIMTZWNkg2VjI2SDI2VjE2aDJWMjZBMi4wMDI3LDIuMDAyNywwLDAsMSwyNiwyOFoiLz4KICAgIDxwb2x5Z29uIHBvaW50cz0iMjAgMiAyMCA0IDI2LjU4NiA0IDE4IDEyLjU4NiAxOS40MTQgMTQgMjggNS40MTQgMjggMTIgMzAgMTIgMzAgMiAyMCAyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4K);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-move-down: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMTIuNDcxIDcuNTI4OTlDMTIuNzYzMiA3LjIzNjg0IDEyLjc2MzIgNi43NjMxNiAxMi40NzEgNi40NzEwMVY2LjQ3MTAxQzEyLjE3OSA2LjE3OTA1IDExLjcwNTcgNi4xNzg4NCAxMS40MTM1IDYuNDcwNTRMNy43NSAxMC4xMjc1VjEuNzVDNy43NSAxLjMzNTc5IDcuNDE0MjEgMSA3IDFWMUM2LjU4NTc5IDEgNi4yNSAxLjMzNTc5IDYuMjUgMS43NVYxMC4xMjc1TDIuNTk3MjYgNi40NjgyMkMyLjMwMzM4IDYuMTczODEgMS44MjY0MSA2LjE3MzU5IDEuNTMyMjYgNi40Njc3NFY2LjQ2Nzc0QzEuMjM4MyA2Ljc2MTcgMS4yMzgzIDcuMjM4MyAxLjUzMjI2IDcuNTMyMjZMNi4yOTI4OSAxMi4yOTI5QzYuNjgzNDIgMTIuNjgzNCA3LjMxNjU4IDEyLjY4MzQgNy43MDcxMSAxMi4yOTI5TDEyLjQ3MSA3LjUyODk5WiIgZmlsbD0iIzYxNjE2MSIvPgo8L3N2Zz4K);
  --jp-icon-move-up: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMS41Mjg5OSA2LjQ3MTAxQzEuMjM2ODQgNi43NjMxNiAxLjIzNjg0IDcuMjM2ODQgMS41Mjg5OSA3LjUyODk5VjcuNTI4OTlDMS44MjA5NSA3LjgyMDk1IDIuMjk0MjYgNy44MjExNiAyLjU4NjQ5IDcuNTI5NDZMNi4yNSAzLjg3MjVWMTIuMjVDNi4yNSAxMi42NjQyIDYuNTg1NzkgMTMgNyAxM1YxM0M3LjQxNDIxIDEzIDcuNzUgMTIuNjY0MiA3Ljc1IDEyLjI1VjMuODcyNUwxMS40MDI3IDcuNTMxNzhDMTEuNjk2NiA3LjgyNjE5IDEyLjE3MzYgNy44MjY0MSAxMi40Njc3IDcuNTMyMjZWNy41MzIyNkMxMi43NjE3IDcuMjM4MyAxMi43NjE3IDYuNzYxNyAxMi40Njc3IDYuNDY3NzRMNy43MDcxMSAxLjcwNzExQzcuMzE2NTggMS4zMTY1OCA2LjY4MzQyIDEuMzE2NTggNi4yOTI4OSAxLjcwNzExTDEuNTI4OTkgNi40NzEwMVoiIGZpbGw9IiM2MTYxNjEiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtbm90ZWJvb2staWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-numbering: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTQgMTlINlYxOS41SDVWMjAuNUg2VjIxSDRWMjJIN1YxOEg0VjE5Wk01IDEwSDZWNkg0VjdINVYxMFpNNCAxM0g1LjhMNCAxNS4xVjE2SDdWMTVINS4yTDcgMTIuOVYxMkg0VjEzWk05IDdWOUgyM1Y3SDlaTTkgMjFIMjNWMTlIOVYyMVpNOSAxNUgyM1YxM0g5VjE1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-offline-bolt: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDIuMDJjLTUuNTEgMC05Ljk4IDQuNDctOS45OCA5Ljk4czQuNDcgOS45OCA5Ljk4IDkuOTggOS45OC00LjQ3IDkuOTgtOS45OFMxNy41MSAyLjAyIDEyIDIuMDJ6TTExLjQ4IDIwdi02LjI2SDhMMTMgNHY2LjI2aDMuMzVMMTEuNDggMjB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-pdf: url(data:image/svg+xml;base64,PHN2ZwogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMiIgd2lkdGg9IjE2Ij4KICAgIDxwYXRoIHRyYW5zZm9ybT0icm90YXRlKDQ1KSIgY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0ZGMkEyQSIKICAgICAgIGQ9Im0gMjIuMzQ0MzY5LC0zLjAxNjM2NDIgaCA1LjYzODYwNCB2IDEuNTc5MjQzMyBoIC0zLjU0OTIyNyB2IDEuNTA4NjkyOTkgaCAzLjMzNzU3NiBWIDEuNjUwODE1NCBoIC0zLjMzNzU3NiB2IDMuNDM1MjYxMyBoIC0yLjA4OTM3NyB6IG0gLTcuMTM2NDQ0LDEuNTc5MjQzMyB2IDQuOTQzOTU0MyBoIDAuNzQ4OTIgcSAxLjI4MDc2MSwwIDEuOTUzNzAzLC0wLjYzNDk1MzUgMC42NzgzNjksLTAuNjM0OTUzNSAwLjY3ODM2OSwtMS44NDUxNjQxIDAsLTEuMjA0NzgzNTUgLTAuNjcyOTQyLC0xLjgzNDMxMDExIC0wLjY3Mjk0MiwtMC42Mjk1MjY1OSAtMS45NTkxMywtMC42Mjk1MjY1OSB6IG0gLTIuMDg5Mzc3LC0xLjU3OTI0MzMgaCAyLjIwMzM0MyBxIDEuODQ1MTY0LDAgMi43NDYwMzksMC4yNjU5MjA3IDAuOTA2MzAxLDAuMjYwNDkzNyAxLjU1MjEwOCwwLjg5MDAyMDMgMC41Njk4MywwLjU0ODEyMjMgMC44NDY2MDUsMS4yNjQ0ODAwNiAwLjI3Njc3NCwwLjcxNjM1NzgxIDAuMjc2Nzc0LDEuNjIyNjU4OTQgMCwwLjkxNzE1NTEgLTAuMjc2Nzc0LDEuNjM4OTM5OSAtMC4yNzY3NzUsMC43MTYzNTc4IC0wLjg0NjYwNSwxLjI2NDQ4IC0wLjY1MTIzNCwwLjYyOTUyNjYgLTEuNTYyOTYyLDAuODk1NDQ3MyAtMC45MTE3MjgsMC4yNjA0OTM3IC0yLjczNTE4NSwwLjI2MDQ5MzcgaCAtMi4yMDMzNDMgeiBtIC04LjE0NTg1NjUsMCBoIDMuNDY3ODIzIHEgMS41NDY2ODE2LDAgMi4zNzE1Nzg1LDAuNjg5MjIzIDAuODMwMzI0LDAuNjgzNzk2MSAwLjgzMDMyNCwxLjk1MzcwMzE0IDAsMS4yNzUzMzM5NyAtMC44MzAzMjQsMS45NjQ1NTcwNiBRIDkuOTg3MTk2MSwyLjI3NDkxNSA4LjQ0MDUxNDUsMi4yNzQ5MTUgSCA3LjA2MjA2ODQgViA1LjA4NjA3NjcgSCA0Ljk3MjY5MTUgWiBtIDIuMDg5Mzc2OSwxLjUxNDExOTkgdiAyLjI2MzAzOTQzIGggMS4xNTU5NDEgcSAwLjYwNzgxODgsMCAwLjkzODg2MjksLTAuMjkzMDU1NDcgMC4zMzEwNDQxLC0wLjI5ODQ4MjQxIDAuMzMxMDQ0MSwtMC44NDExNzc3MiAwLC0wLjU0MjY5NTMxIC0wLjMzMTA0NDEsLTAuODM1NzUwNzQgLTAuMzMxMDQ0MSwtMC4yOTMwNTU1IC0wLjkzODg2MjksLTAuMjkzMDU1NSB6IgovPgo8L3N2Zz4K);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iLTEwIC0xMCAxMzEuMTYxMzYxNjk0MzM1OTQgMTMyLjM4ODk5OTkzODk2NDg0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzA2OTk4IiBkPSJNIDU0LjkxODc4NSw5LjE5Mjc0MjFlLTQgQyA1MC4zMzUxMzIsMC4wMjIyMTcyNyA0NS45NTc4NDYsMC40MTMxMzY5NyA0Mi4xMDYyODUsMS4wOTQ2NjkzIDMwLjc2MDA2OSwzLjA5OTE3MzEgMjguNzAwMDM2LDcuMjk0NzcxNCAyOC43MDAwMzUsMTUuMDMyMTY5IHYgMTAuMjE4NzUgaCAyNi44MTI1IHYgMy40MDYyNSBoIC0yNi44MTI1IC0xMC4wNjI1IGMgLTcuNzkyNDU5LDAgLTE0LjYxNTc1ODgsNC42ODM3MTcgLTE2Ljc0OTk5OTgsMTMuNTkzNzUgLTIuNDYxODE5OTgsMTAuMjEyOTY2IC0yLjU3MTAxNTA4LDE2LjU4NjAyMyAwLDI3LjI1IDEuOTA1OTI4Myw3LjkzNzg1MiA2LjQ1NzU0MzIsMTMuNTkzNzQ4IDE0LjI0OTk5OTgsMTMuNTkzNzUgaCA5LjIxODc1IHYgLTEyLjI1IGMgMCwtOC44NDk5MDIgNy42NTcxNDQsLTE2LjY1NjI0OCAxNi43NSwtMTYuNjU2MjUgaCAyNi43ODEyNSBjIDcuNDU0OTUxLDAgMTMuNDA2MjUzLC02LjEzODE2NCAxMy40MDYyNSwtMTMuNjI1IHYgLTI1LjUzMTI1IGMgMCwtNy4yNjYzMzg2IC02LjEyOTk4LC0xMi43MjQ3NzcxIC0xMy40MDYyNSwtMTMuOTM3NDk5NyBDIDY0LjI4MTU0OCwwLjMyNzk0Mzk3IDU5LjUwMjQzOCwtMC4wMjAzNzkwMyA1NC45MTg3ODUsOS4xOTI3NDIxZS00IFogbSAtMTQuNSw4LjIxODc1MDEyNTc5IGMgMi43Njk1NDcsMCA1LjAzMTI1LDIuMjk4NjQ1NiA1LjAzMTI1LDUuMTI0OTk5NiAtMmUtNiwyLjgxNjMzNiAtMi4yNjE3MDMsNS4wOTM3NSAtNS4wMzEyNSw1LjA5Mzc1IC0yLjc3OTQ3NiwtMWUtNiAtNS4wMzEyNSwtMi4yNzc0MTUgLTUuMDMxMjUsLTUuMDkzNzUgLTEwZS03LC0yLjgyNjM1MyAyLjI1MTc3NCwtNS4xMjQ5OTk2IDUuMDMxMjUsLTUuMTI0OTk5NiB6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2ZmZDQzYiIgZD0ibSA4NS42Mzc1MzUsMjguNjU3MTY5IHYgMTEuOTA2MjUgYyAwLDkuMjMwNzU1IC03LjgyNTg5NSwxNi45OTk5OTkgLTE2Ljc1LDE3IGggLTI2Ljc4MTI1IGMgLTcuMzM1ODMzLDAgLTEzLjQwNjI0OSw2LjI3ODQ4MyAtMTMuNDA2MjUsMTMuNjI1IHYgMjUuNTMxMjQ3IGMgMCw3LjI2NjM0NCA2LjMxODU4OCwxMS41NDAzMjQgMTMuNDA2MjUsMTMuNjI1MDA0IDguNDg3MzMxLDIuNDk1NjEgMTYuNjI2MjM3LDIuOTQ2NjMgMjYuNzgxMjUsMCA2Ljc1MDE1NSwtMS45NTQzOSAxMy40MDYyNTMsLTUuODg3NjEgMTMuNDA2MjUsLTEzLjYyNTAwNCBWIDg2LjUwMDkxOSBoIC0yNi43ODEyNSB2IC0zLjQwNjI1IGggMjYuNzgxMjUgMTMuNDA2MjU0IGMgNy43OTI0NjEsMCAxMC42OTYyNTEsLTUuNDM1NDA4IDEzLjQwNjI0MSwtMTMuNTkzNzUgMi43OTkzMywtOC4zOTg4ODYgMi42ODAyMiwtMTYuNDc1Nzc2IDAsLTI3LjI1IC0xLjkyNTc4LC03Ljc1NzQ0MSAtNS42MDM4NywtMTMuNTkzNzUgLTEzLjQwNjI0MSwtMTMuNTkzNzUgeiBtIC0xNS4wNjI1LDY0LjY1NjI1IGMgMi43Nzk0NzgsM2UtNiA1LjAzMTI1LDIuMjc3NDE3IDUuMDMxMjUsNS4wOTM3NDcgLTJlLTYsMi44MjYzNTQgLTIuMjUxNzc1LDUuMTI1MDA0IC01LjAzMTI1LDUuMTI1MDA0IC0yLjc2OTU1LDAgLTUuMDMxMjUsLTIuMjk4NjUgLTUuMDMxMjUsLTUuMTI1MDA0IDJlLTYsLTIuODE2MzMgMi4yNjE2OTcsLTUuMDkzNzQ3IDUuMDMxMjUsLTUuMDkzNzQ3IHoiLz4KPC9zdmc+Cg==);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-redo: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIi8+PHBhdGggZD0iTTE4LjQgMTAuNkMxNi41NSA4Ljk5IDE0LjE1IDggMTEuNSA4Yy00LjY1IDAtOC41OCAzLjAzLTkuOTYgNy4yMkwzLjkgMTZjMS4wNS0zLjE5IDQuMDUtNS41IDcuNi01LjUgMS45NSAwIDMuNzMuNzIgNS4xMiAxLjg4TDEzIDE2aDlWN2wtMy42IDMuNnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-share: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTSAxOCAyIEMgMTYuMzU0OTkgMiAxNSAzLjM1NDk5MDQgMTUgNSBDIDE1IDUuMTkwOTUyOSAxNS4wMjE3OTEgNS4zNzcxMjI0IDE1LjA1NjY0MSA1LjU1ODU5MzggTCA3LjkyMTg3NSA5LjcyMDcwMzEgQyA3LjM5ODUzOTkgOS4yNzc4NTM5IDYuNzMyMDc3MSA5IDYgOSBDIDQuMzU0OTkwNCA5IDMgMTAuMzU0OTkgMyAxMiBDIDMgMTMuNjQ1MDEgNC4zNTQ5OTA0IDE1IDYgMTUgQyA2LjczMjA3NzEgMTUgNy4zOTg1Mzk5IDE0LjcyMjE0NiA3LjkyMTg3NSAxNC4yNzkyOTcgTCAxNS4wNTY2NDEgMTguNDM5NDUzIEMgMTUuMDIxNTU1IDE4LjYyMTUxNCAxNSAxOC44MDgzODYgMTUgMTkgQyAxNSAyMC42NDUwMSAxNi4zNTQ5OSAyMiAxOCAyMiBDIDE5LjY0NTAxIDIyIDIxIDIwLjY0NTAxIDIxIDE5IEMgMjEgMTcuMzU0OTkgMTkuNjQ1MDEgMTYgMTggMTYgQyAxNy4yNjc0OCAxNiAxNi42MDE1OTMgMTYuMjc5MzI4IDE2LjA3ODEyNSAxNi43MjI2NTYgTCA4Ljk0MzM1OTQgMTIuNTU4NTk0IEMgOC45NzgyMDk1IDEyLjM3NzEyMiA5IDEyLjE5MDk1MyA5IDEyIEMgOSAxMS44MDkwNDcgOC45NzgyMDk1IDExLjYyMjg3OCA4Ljk0MzM1OTQgMTEuNDQxNDA2IEwgMTYuMDc4MTI1IDcuMjc5Mjk2OSBDIDE2LjYwMTQ2IDcuNzIyMTQ2MSAxNy4yNjc5MjMgOCAxOCA4IEMgMTkuNjQ1MDEgOCAyMSA2LjY0NTAwOTYgMjEgNSBDIDIxIDMuMzU0OTkwNCAxOS42NDUwMSAyIDE4IDIgeiBNIDE4IDQgQyAxOC41NjQxMjkgNCAxOSA0LjQzNTg3MDYgMTkgNSBDIDE5IDUuNTY0MTI5NCAxOC41NjQxMjkgNiAxOCA2IEMgMTcuNDM1ODcxIDYgMTcgNS41NjQxMjk0IDE3IDUgQyAxNyA0LjQzNTg3MDYgMTcuNDM1ODcxIDQgMTggNCB6IE0gNiAxMSBDIDYuNTY0MTI5NCAxMSA3IDExLjQzNTg3MSA3IDEyIEMgNyAxMi41NjQxMjkgNi41NjQxMjk0IDEzIDYgMTMgQyA1LjQzNTg3MDYgMTMgNSAxMi41NjQxMjkgNSAxMiBDIDUgMTEuNDM1ODcxIDUuNDM1ODcwNiAxMSA2IDExIHogTSAxOCAxOCBDIDE4LjU2NDEyOSAxOCAxOSAxOC40MzU4NzEgMTkgMTkgQyAxOSAxOS41NjQxMjkgMTguNTY0MTI5IDIwIDE4IDIwIEMgMTcuNDM1ODcxIDIwIDE3IDE5LjU2NDEyOSAxNyAxOSBDIDE3IDE4LjQzNTg3MSAxNy40MzU4NzEgMTggMTggMTggeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-table-rows: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMSw4SDNWNGgxOFY4eiBNMjEsMTBIM3Y0aDE4VjEweiBNMjEsMTZIM3Y0aDE4VjE2eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-tag: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjgiIGhlaWdodD0iMjgiIHZpZXdCb3g9IjAgMCA0MyAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTI4LjgzMzIgMTIuMzM0TDMyLjk5OTggMTYuNTAwN0wzNy4xNjY1IDEyLjMzNEgyOC44MzMyWiIvPgoJCTxwYXRoIGQ9Ik0xNi4yMDk1IDIxLjYxMDRDMTUuNjg3MyAyMi4xMjk5IDE0Ljg0NDMgMjIuMTI5OSAxNC4zMjQ4IDIxLjYxMDRMNi45ODI5IDE0LjcyNDVDNi41NzI0IDE0LjMzOTQgNi4wODMxMyAxMy42MDk4IDYuMDQ3ODYgMTMuMDQ4MkM1Ljk1MzQ3IDExLjUyODggNi4wMjAwMiA4LjYxOTQ0IDYuMDY2MjEgNy4wNzY5NUM2LjA4MjgxIDYuNTE0NzcgNi41NTU0OCA2LjA0MzQ3IDcuMTE4MDQgNi4wMzA1NUM5LjA4ODYzIDUuOTg0NzMgMTMuMjYzOCA1LjkzNTc5IDEzLjY1MTggNi4zMjQyNUwyMS43MzY5IDEzLjYzOUMyMi4yNTYgMTQuMTU4NSAyMS43ODUxIDE1LjQ3MjQgMjEuMjYyIDE1Ljk5NDZMMTYuMjA5NSAyMS42MTA0Wk05Ljc3NTg1IDguMjY1QzkuMzM1NTEgNy44MjU2NiA4LjYyMzUxIDcuODI1NjYgOC4xODI4IDguMjY1QzcuNzQzNDYgOC43MDU3MSA3Ljc0MzQ2IDkuNDE3MzMgOC4xODI4IDkuODU2NjdDOC42MjM4MiAxMC4yOTY0IDkuMzM1ODIgMTAuMjk2NCA5Ljc3NTg1IDkuODU2NjdDMTAuMjE1NiA5LjQxNzMzIDEwLjIxNTYgOC43MDUzMyA5Ljc3NTg1IDguMjY1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1iYWNrZ3JvdW5kLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgd2lkdGg9IjIwIiBoZWlnaHQ9IjIwIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyIDIpIiBmaWxsPSIjMzMzMzMzIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUtaW52ZXJzZSIgZD0iTTUuMDU2NjQgOC43NjE3MkM1LjA1NjY0IDguNTk3NjYgNS4wMzEyNSA4LjQ1MzEyIDQuOTgwNDcgOC4zMjgxMkM0LjkzMzU5IDguMTk5MjIgNC44NTU0NyA4LjA4MjAzIDQuNzQ2MDkgNy45NzY1NkM0LjY0MDYyIDcuODcxMDkgNC41IDcuNzc1MzkgNC4zMjQyMiA3LjY4OTQ1QzQuMTUyMzQgNy41OTk2MSAzLjk0MzM2IDcuNTExNzIgMy42OTcyNyA3LjQyNTc4QzMuMzAyNzMgNy4yODUxNiAyLjk0MzM2IDcuMTM2NzIgMi42MTkxNCA2Ljk4MDQ3QzIuMjk0OTIgNi44MjQyMiAyLjAxNzU4IDYuNjQyNTggMS43ODcxMSA2LjQzNTU1QzEuNTYwNTUgNi4yMjg1MiAxLjM4NDc3IDUuOTg4MjggMS4yNTk3NyA1LjcxNDg0QzEuMTM0NzcgNS40Mzc1IDEuMDcyMjcgNS4xMDkzOCAxLjA3MjI3IDQuNzMwNDdDMS4wNzIyNyA0LjM5ODQ0IDEuMTI4OTEgNC4wOTU3IDEuMjQyMTkgMy44MjIyN0MxLjM1NTQ3IDMuNTQ0OTIgMS41MTU2MiAzLjMwNDY5IDEuNzIyNjYgMy4xMDE1NkMxLjkyOTY5IDIuODk4NDQgMi4xNzk2OSAyLjczNDM3IDIuNDcyNjYgMi42MDkzOEMyLjc2NTYyIDIuNDg0MzggMy4wOTE4IDIuNDA0MyAzLjQ1MTE3IDIuMzY5MTRWMS4xMDkzOEg0LjM4ODY3VjIuMzgwODZDNC43NDAyMyAyLjQyNzczIDUuMDU2NjQgMi41MjM0NCA1LjMzNzg5IDIuNjY3OTdDNS42MTkxNCAyLjgxMjUgNS44NTc0MiAzLjAwMTk1IDYuMDUyNzMgMy4yMzYzM0M2LjI1MTk1IDMuNDY2OCA2LjQwNDMgMy43NDAyMyA2LjUwOTc3IDQuMDU2NjRDNi42MTkxNCA0LjM2OTE0IDYuNjczODMgNC43MjA3IDYuNjczODMgNS4xMTEzM0g1LjA0NDkyQzUuMDQ0OTIgNC42Mzg2NyA0LjkzNzUgNC4yODEyNSA0LjcyMjY2IDQuMDM5MDZDNC41MDc4MSAzLjc5Mjk3IDQuMjE2OCAzLjY2OTkyIDMuODQ5NjEgMy42Njk5MkMzLjY1MDM5IDMuNjY5OTIgMy40NzY1NiAzLjY5NzI3IDMuMzI4MTIgMy43NTE5NUMzLjE4MzU5IDMuODAyNzMgMy4wNjQ0NSAzLjg3Njk1IDIuOTcwNyAzLjk3NDYxQzIuODc2OTUgNC4wNjgzNiAyLjgwNjY0IDQuMTc5NjkgMi43NTk3NyA0LjMwODU5QzIuNzE2OCA0LjQzNzUgMi42OTUzMSA0LjU3ODEyIDIuNjk1MzEgNC43MzA0N0MyLjY5NTMxIDQuODgyODEgMi43MTY4IDUuMDE5NTMgMi43NTk3NyA1LjE0MDYyQzIuODA2NjQgNS4yNTc4MSAyLjg4MjgxIDUuMzY3MTkgMi45ODgyOCA1LjQ2ODc1QzMuMDk3NjYgNS41NzAzMSAzLjI0MDIzIDUuNjY3OTcgMy40MTYwMiA1Ljc2MTcyQzMuNTkxOCA1Ljg1MTU2IDMuODEwNTUgNS45NDMzNiA0LjA3MjI3IDYuMDM3MTFDNC40NjY4IDYuMTg1NTUgNC44MjQyMiA2LjMzOTg0IDUuMTQ0NTMgNi41QzUuNDY0ODQgNi42NTYyNSA1LjczODI4IDYuODM5ODQgNS45NjQ4NCA3LjA1MDc4QzYuMTk1MzEgNy4yNTc4MSA2LjM3MTA5IDcuNSA2LjQ5MjE5IDcuNzc3MzRDNi42MTcxOSA4LjA1MDc4IDYuNjc5NjkgOC4zNzUgNi42Nzk2OSA4Ljc1QzYuNjc5NjkgOS4wOTM3NSA2LjYyMzA1IDkuNDA0MyA2LjUwOTc3IDkuNjgxNjRDNi4zOTY0OCA5Ljk1NTA4IDYuMjM0MzggMTAuMTkxNCA2LjAyMzQ0IDEwLjM5MDZDNS44MTI1IDEwLjU4OTggNS41NTg1OSAxMC43NSA1LjI2MTcyIDEwLjg3MTFDNC45NjQ4NCAxMC45ODgzIDQuNjMyODEgMTEuMDY0NSA0LjI2NTYyIDExLjA5OTZWMTIuMjQ4SDMuMzMzOThWMTEuMDk5NkMzLjAwMTk1IDExLjA2ODQgMi42Nzk2OSAxMC45OTYxIDIuMzY3MTkgMTAuODgyOEMyLjA1NDY5IDEwLjc2NTYgMS43NzczNCAxMC41OTc3IDEuNTM1MTYgMTAuMzc4OUMxLjI5Njg4IDEwLjE2MDIgMS4xMDU0NyA5Ljg4NDc3IDAuOTYwOTM4IDkuNTUyNzNDMC44MTY0MDYgOS4yMTY4IDAuNzQ0MTQxIDguODE0NDUgMC43NDQxNDEgOC4zNDU3SDIuMzc4OTFDMi4zNzg5MSA4LjYyNjk1IDIuNDE5OTIgOC44NjMyOCAyLjUwMTk1IDkuMDU0NjlDMi41ODM5OCA5LjI0MjE5IDIuNjg5NDUgOS4zOTI1OCAyLjgxODM2IDkuNTA1ODZDMi45NTExNyA5LjYxNTIzIDMuMTAxNTYgOS42OTMzNiAzLjI2OTUzIDkuNzQwMjNDMy40Mzc1IDkuNzg3MTEgMy42MDkzOCA5LjgxMDU1IDMuNzg1MTYgOS44MTA1NUM0LjIwMzEyIDkuODEwNTUgNC41MTk1MyA5LjcxMjg5IDQuNzM0MzggOS41MTc1OEM0Ljk0OTIyIDkuMzIyMjcgNS4wNTY2NCA5LjA3MDMxIDUuMDU2NjQgOC43NjE3MlpNMTMuNDE4IDEyLjI3MTVIOC4wNzQyMlYxMUgxMy40MThWMTIuMjcxNVoiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMuOTUyNjQgNikiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo=);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtdGV4dC1lZGl0b3ItaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xNSAxNUgzdjJoMTJ2LTJ6bTAtOEgzdjJoMTJWN3pNMyAxM2gxOHYtMkgzdjJ6bTAgOGgxOHYtMkgzdjJ6TTMgM3YyaDE4VjNIM3oiLz4KPC9zdmc+Cg==);
  --jp-icon-toc: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik03LDVIMjFWN0g3VjVNNywxM1YxMUgyMVYxM0g3TTQsNC41QTEuNSwxLjUgMCAwLDEgNS41LDZBMS41LDEuNSAwIDAsMSA0LDcuNUExLjUsMS41IDAgMCwxIDIuNSw2QTEuNSwxLjUgMCAwLDEgNCw0LjVNNCwxMC41QTEuNSwxLjUgMCAwLDEgNS41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMy41QTEuNSwxLjUgMCAwLDEgMi41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMC41TTcsMTlWMTdIMjFWMTlIN000LDE2LjVBMS41LDEuNSAwIDAsMSA1LjUsMThBMS41LDEuNSAwIDAsMSA0LDE5LjVBMS41LDEuNSAwIDAsMSAyLjUsMThBMS41LDEuNSAwIDAsMSA0LDE2LjVaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tree-view: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMiAxMVYzaC03djNIOVYzSDJ2OGg3VjhoMnYxMGg0djNoN3YtOGgtN3YzaC0yVjhoMnYzeiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-user: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE2IDdhNCA0IDAgMTEtOCAwIDQgNCAwIDAxOCAwek0xMiAxNGE3IDcgMCAwMC03IDdoMTRhNyA3IDAgMDAtNy03eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-users: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAwIDM2IDI0IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogPGcgY2xhc3M9ImpwLWljb24zIiB0cmFuc2Zvcm09Im1hdHJpeCgxLjczMjcgMCAwIDEuNzMyNyAtMy42MjgyIC4wOTk1NzcpIiBmaWxsPSIjNjE2MTYxIj4KICA8cGF0aCB0cmFuc2Zvcm09Im1hdHJpeCgxLjUsMCwwLDEuNSwwLC02KSIgZD0ibTEyLjE4NiA3LjUwOThjLTEuMDUzNSAwLTEuOTc1NyAwLjU2NjUtMi40Nzg1IDEuNDEwMiAwLjc1MDYxIDAuMzEyNzcgMS4zOTc0IDAuODI2NDggMS44NzMgMS40NzI3aDMuNDg2M2MwLTEuNTkyLTEuMjg4OS0yLjg4MjgtMi44ODA5LTIuODgyOHoiLz4KICA8cGF0aCBkPSJtMjAuNDY1IDIuMzg5NWEyLjE4ODUgMi4xODg1IDAgMCAxLTIuMTg4NCAyLjE4ODUgMi4xODg1IDIuMTg4NSAwIDAgMS0yLjE4ODUtMi4xODg1IDIuMTg4NSAyLjE4ODUgMCAwIDEgMi4xODg1LTIuMTg4NSAyLjE4ODUgMi4xODg1IDAgMCAxIDIuMTg4NCAyLjE4ODV6Ii8+CiAgPHBhdGggdHJhbnNmb3JtPSJtYXRyaXgoMS41LDAsMCwxLjUsMCwtNikiIGQ9Im0zLjU4OTggOC40MjE5Yy0xLjExMjYgMC0yLjAxMzcgMC45MDExMS0yLjAxMzcgMi4wMTM3aDIuODE0NWMwLjI2Nzk3LTAuMzczMDkgMC41OTA3LTAuNzA0MzUgMC45NTg5OC0wLjk3ODUyLTAuMzQ0MzMtMC42MTY4OC0xLjAwMzEtMS4wMzUyLTEuNzU5OC0xLjAzNTJ6Ii8+CiAgPHBhdGggZD0ibTYuOTE1NCA0LjYyM2ExLjUyOTQgMS41Mjk0IDAgMCAxLTEuNTI5NCAxLjUyOTQgMS41Mjk0IDEuNTI5NCAwIDAgMS0xLjUyOTQtMS41Mjk0IDEuNTI5NCAxLjUyOTQgMCAwIDEgMS41Mjk0LTEuNTI5NCAxLjUyOTQgMS41Mjk0IDAgMCAxIDEuNTI5NCAxLjUyOTR6Ii8+CiAgPHBhdGggZD0ibTYuMTM1IDEzLjUzNWMwLTMuMjM5MiAyLjYyNTktNS44NjUgNS44NjUtNS44NjUgMy4yMzkyIDAgNS44NjUgMi42MjU5IDUuODY1IDUuODY1eiIvPgogIDxjaXJjbGUgY3g9IjEyIiBjeT0iMy43Njg1IiByPSIyLjk2ODUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-word: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KIDxnIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzQxNDE0MSI+CiAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiA8L2c+CiA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSguNDMgLjA0MDEpIiBmaWxsPSIjZmZmIj4KICA8cGF0aCBkPSJtNC4xNCA4Ljc2cTAuMDY4Mi0xLjg5IDIuNDItMS44OSAxLjE2IDAgMS42OCAwLjQyIDAuNTY3IDAuNDEgMC41NjcgMS4xNnYzLjQ3cTAgMC40NjIgMC41MTQgMC40NjIgMC4xMDMgMCAwLjItMC4wMjMxdjAuNzE0cS0wLjM5OSAwLjEwMy0wLjY1MSAwLjEwMy0wLjQ1MiAwLTAuNjkzLTAuMjItMC4yMzEtMC4yLTAuMjg0LTAuNjYyLTAuOTU2IDAuODcyLTIgMC44NzItMC45MDMgMC0xLjQ3LTAuNDcyLTAuNTI1LTAuNDcyLTAuNTI1LTEuMjYgMC0wLjI2MiAwLjA0NTItMC40NzIgMC4wNTY3LTAuMjIgMC4xMTYtMC4zNzggMC4wNjgyLTAuMTY4IDAuMjMxLTAuMzA0IDAuMTU4LTAuMTQ3IDAuMjYyLTAuMjQyIDAuMTE2LTAuMDkxNCAwLjM2OC0wLjE2OCAwLjI2Mi0wLjA5MTQgMC4zOTktMC4xMjYgMC4xMzYtMC4wNDUyIDAuNDcyLTAuMTAzIDAuMzM2LTAuMDU3OCAwLjUwNC0wLjA3OTggMC4xNTgtMC4wMjMxIDAuNTY3LTAuMDc5OCAwLjU1Ni0wLjA2ODIgMC43NzctMC4yMjEgMC4yMi0wLjE1MiAwLjIyLTAuNDQxdi0wLjI1MnEwLTAuNDMtMC4zNTctMC42NjItMC4zMzYtMC4yMzEtMC45NzYtMC4yMzEtMC42NjIgMC0wLjk5OCAwLjI2Mi0wLjMzNiAwLjI1Mi0wLjM5OSAwLjc5OHptMS44OSAzLjY4cTAuNzg4IDAgMS4yNi0wLjQxIDAuNTA0LTAuNDIgMC41MDQtMC45MDN2LTEuMDVxLTAuMjg0IDAuMTM2LTAuODYxIDAuMjMxLTAuNTY3IDAuMDkxNC0wLjk4NyAwLjE1OC0wLjQyIDAuMDY4Mi0wLjc2NiAwLjMyNi0wLjMzNiAwLjI1Mi0wLjMzNiAwLjcwNHQwLjMwNCAwLjcwNCAwLjg2MSAwLjI1MnoiIHN0cm9rZS13aWR0aD0iMS4wNSIvPgogIDxwYXRoIGQ9Im0xMCA0LjU2aDAuOTQ1djMuMTVxMC42NTEtMC45NzYgMS44OS0wLjk3NiAxLjE2IDAgMS44OSAwLjg0IDAuNjgyIDAuODQgMC42ODIgMi4zMSAwIDEuNDctMC43MDQgMi40Mi0wLjcwNCAwLjg4Mi0xLjg5IDAuODgyLTEuMjYgMC0xLjg5LTEuMDJ2MC43NjZoLTAuODV6bTIuNjIgMy4wNHEtMC43NDYgMC0xLjE2IDAuNjQtMC40NTIgMC42My0wLjQ1MiAxLjY4IDAgMS4wNSAwLjQ1MiAxLjY4dDEuMTYgMC42M3EwLjc3NyAwIDEuMjYtMC42MyAwLjQ5NC0wLjY0IDAuNDk0LTEuNjggMC0xLjA1LTAuNDcyLTEuNjgtMC40NjItMC42NC0xLjI2LTAuNjR6IiBzdHJva2Utd2lkdGg9IjEuMDUiLz4KICA8cGF0aCBkPSJtMi43MyAxNS44IDEzLjYgMC4wMDgxYzAuMDA2OSAwIDAtMi42IDAtMi42IDAtMC4wMDc4LTEuMTUgMC0xLjE1IDAtMC4wMDY5IDAtMC4wMDgzIDEuNS0wLjAwODMgMS41LTJlLTMgLTAuMDAxNC0xMS4zLTAuMDAxNC0xMS4zLTAuMDAxNGwtMC4wMDU5Mi0xLjVjMC0wLjAwNzgtMS4xNyAwLjAwMTMtMS4xNyAwLjAwMTN6IiBzdHJva2Utd2lkdGg9Ii45NzUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddAboveIcon {
  background-image: var(--jp-icon-add-above);
}

.jp-AddBelowIcon {
  background-image: var(--jp-icon-add-below);
}

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}

.jp-BellIcon {
  background-image: var(--jp-icon-bell);
}

.jp-BugDotIcon {
  background-image: var(--jp-icon-bug-dot);
}

.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}

.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}

.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}

.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}

.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}

.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}

.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}

.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}

.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}

.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}

.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}

.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}

.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}

.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}

.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}

.jp-CodeCheckIcon {
  background-image: var(--jp-icon-code-check);
}

.jp-CodeIcon {
  background-image: var(--jp-icon-code);
}

.jp-CollapseAllIcon {
  background-image: var(--jp-icon-collapse-all);
}

.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}

.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}

.jp-CopyrightIcon {
  background-image: var(--jp-icon-copyright);
}

.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}

.jp-DeleteIcon {
  background-image: var(--jp-icon-delete);
}

.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}

.jp-DuplicateIcon {
  background-image: var(--jp-icon-duplicate);
}

.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}

.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}

.jp-ErrorIcon {
  background-image: var(--jp-icon-error);
}

.jp-ExpandAllIcon {
  background-image: var(--jp-icon-expand-all);
}

.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}

.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}

.jp-FileIcon {
  background-image: var(--jp-icon-file);
}

.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}

.jp-FilterDotIcon {
  background-image: var(--jp-icon-filter-dot);
}

.jp-FilterIcon {
  background-image: var(--jp-icon-filter);
}

.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}

.jp-FolderFavoriteIcon {
  background-image: var(--jp-icon-folder-favorite);
}

.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}

.jp-HomeIcon {
  background-image: var(--jp-icon-home);
}

.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}

.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}

.jp-InfoIcon {
  background-image: var(--jp-icon-info);
}

.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}

.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}

.jp-JuliaIcon {
  background-image: var(--jp-icon-julia);
}

.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}

.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}

.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}

.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}

.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}

.jp-LaunchIcon {
  background-image: var(--jp-icon-launch);
}

.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}

.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}

.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}

.jp-ListIcon {
  background-image: var(--jp-icon-list);
}

.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}

.jp-MoveDownIcon {
  background-image: var(--jp-icon-move-down);
}

.jp-MoveUpIcon {
  background-image: var(--jp-icon-move-up);
}

.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}

.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}

.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}

.jp-NumberingIcon {
  background-image: var(--jp-icon-numbering);
}

.jp-OfflineBoltIcon {
  background-image: var(--jp-icon-offline-bolt);
}

.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}

.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}

.jp-PdfIcon {
  background-image: var(--jp-icon-pdf);
}

.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}

.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}

.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}

.jp-RedoIcon {
  background-image: var(--jp-icon-redo);
}

.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}

.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}

.jp-RunIcon {
  background-image: var(--jp-icon-run);
}

.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}

.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}

.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}

.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}

.jp-ShareIcon {
  background-image: var(--jp-icon-share);
}

.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}

.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}

.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}

.jp-TableRowsIcon {
  background-image: var(--jp-icon-table-rows);
}

.jp-TagIcon {
  background-image: var(--jp-icon-tag);
}

.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}

.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}

.jp-TocIcon {
  background-image: var(--jp-icon-toc);
}

.jp-TreeViewIcon {
  background-image: var(--jp-icon-tree-view);
}

.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}

.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}

.jp-UserIcon {
  background-image: var(--jp-icon-user);
}

.jp-UsersIcon {
  background-image: var(--jp-icon-users);
}

.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}

.jp-WordIcon {
  background-image: var(--jp-icon-word);
}

.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.lm-TabBar .lm-TabBar-addButton {
  align-items: center;
  display: flex;
  padding: 4px;
  padding-bottom: 5px;
  margin-right: 1px;
  background-color: var(--jp-layout-color2);
}

.lm-TabBar .lm-TabBar-addButton:hover {
  background-color: var(--jp-layout-color1);
}

.lm-DockPanel-tabBar .lm-TabBar-tab {
  width: var(--jp-private-horizontal-tab-width);
}

.lm-DockPanel-tabBar .lm-TabBar-content {
  flex: unset;
}

.lm-DockPanel-tabBar[data-orientation='horizontal'] {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}

/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}

.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}

.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}

.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}

.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}

.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}

.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}

.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}

.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}

/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}

.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}

.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}

.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}

.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}

.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}

.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}

/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

.jp-icon-dot[fill] {
  fill: var(--jp-warn-color0);
}

.jp-jupyter-icon-color[fill] {
  fill: var(--jp-jupyter-icon-color, var(--jp-warn-color0));
}

.jp-notebook-icon-color[fill] {
  fill: var(--jp-notebook-icon-color, var(--jp-warn-color0));
}

.jp-json-icon-color[fill] {
  fill: var(--jp-json-icon-color, var(--jp-warn-color1));
}

.jp-console-icon-color[fill] {
  fill: var(--jp-console-icon-color, white);
}

.jp-console-icon-background-color[fill] {
  fill: var(--jp-console-icon-background-color, var(--jp-brand-color1));
}

.jp-terminal-icon-color[fill] {
  fill: var(--jp-terminal-icon-color, var(--jp-layout-color2));
}

.jp-terminal-icon-background-color[fill] {
  fill: var(
    --jp-terminal-icon-background-color,
    var(--jp-inverse-layout-color2)
  );
}

.jp-text-editor-icon-color[fill] {
  fill: var(--jp-text-editor-icon-color, var(--jp-inverse-layout-color3));
}

.jp-inspector-icon-color[fill] {
  fill: var(--jp-inspector-icon-color, var(--jp-inverse-layout-color3));
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* stylelint-disable selector-max-class, selector-max-compound-selectors */

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}

.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* stylelint-enable selector-max-class, selector-max-compound-selectors */

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) .jp-icon-hoverShow-content {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FormGroup-content fieldset {
  border: none;
  padding: 0;
  min-width: 0;
  width: 100%;
}

/* stylelint-disable selector-max-type */

.jp-FormGroup-content fieldset .jp-inputFieldWrapper input,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper select,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper textarea {
  font-size: var(--jp-content-font-size2);
  border-color: var(--jp-input-border-color);
  border-style: solid;
  border-radius: var(--jp-border-radius);
  border-width: 1px;
  padding: 6px 8px;
  background: none;
  color: var(--jp-ui-font-color0);
  height: inherit;
}

.jp-FormGroup-content fieldset input[type='checkbox'] {
  position: relative;
  top: 2px;
  margin-left: 0;
}

.jp-FormGroup-content button.jp-mod-styled {
  cursor: pointer;
}

.jp-FormGroup-content .checkbox label {
  cursor: pointer;
  font-size: var(--jp-content-font-size1);
}

.jp-FormGroup-content .jp-root > fieldset > legend {
  display: none;
}

.jp-FormGroup-content .jp-root > fieldset > p {
  display: none;
}

/** copy of `input.jp-mod-styled:focus` style */
.jp-FormGroup-content fieldset input:focus,
.jp-FormGroup-content fieldset select:focus {
  -moz-outline-radius: unset;
  outline: var(--jp-border-width) solid var(--md-blue-500);
  outline-offset: -1px;
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-FormGroup-content fieldset input:hover:not(:focus),
.jp-FormGroup-content fieldset select:hover:not(:focus) {
  background-color: var(--jp-border-color2);
}

/* stylelint-enable selector-max-type */

.jp-FormGroup-content .checkbox .field-description {
  /* Disable default description field for checkbox:
   because other widgets do not have description fields,
   we add descriptions to each widget on the field level.
  */
  display: none;
}

.jp-FormGroup-content #root__description {
  display: none;
}

.jp-FormGroup-content .jp-modifiedIndicator {
  width: 5px;
  background-color: var(--jp-brand-color2);
  margin-top: 0;
  margin-left: calc(var(--jp-private-settingeditor-modifier-indent) * -1);
  flex-shrink: 0;
}

.jp-FormGroup-content .jp-modifiedIndicator.jp-errorIndicator {
  background-color: var(--jp-error-color0);
  margin-right: 0.5em;
}

/* RJSF ARRAY style */

.jp-arrayFieldWrapper legend {
  font-size: var(--jp-content-font-size2);
  color: var(--jp-ui-font-color0);
  flex-basis: 100%;
  padding: 4px 0;
  font-weight: var(--jp-content-heading-font-weight);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-arrayFieldWrapper .field-description {
  padding: 4px 0;
  white-space: pre-wrap;
}

.jp-arrayFieldWrapper .array-item {
  width: 100%;
  border: 1px solid var(--jp-border-color2);
  border-radius: 4px;
  margin: 4px;
}

.jp-ArrayOperations {
  display: flex;
  margin-left: 8px;
}

.jp-ArrayOperationsButton {
  margin: 2px;
}

.jp-ArrayOperationsButton .jp-icon3[fill] {
  fill: var(--jp-ui-font-color0);
}

button.jp-ArrayOperationsButton.jp-mod-styled:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

/* RJSF form validation error */

.jp-FormGroup-content .validationErrors {
  color: var(--jp-error-color0);
}

/* Hide panel level error as duplicated the field level error */
.jp-FormGroup-content .panel.errors {
  display: none;
}

/* RJSF normal content (settings-editor) */

.jp-FormGroup-contentNormal {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-FormGroup-contentItem {
  margin-left: 7px;
  color: var(--jp-ui-font-color0);
}

.jp-FormGroup-contentNormal .jp-FormGroup-description {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-default {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-fieldLabel {
  font-size: var(--jp-content-font-size1);
  font-weight: normal;
  min-width: 120px;
}

.jp-FormGroup-contentNormal fieldset:not(:first-child) {
  margin-left: 7px;
}

.jp-FormGroup-contentNormal .field-array-of-string .array-item {
  /* Display `jp-ArrayOperations` buttons side-by-side with content except
    for small screens where flex-wrap will place them one below the other.
  */
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-objectFieldWrapper .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

/* RJSF compact content (metadata-form) */

.jp-FormGroup-content.jp-FormGroup-contentCompact {
  width: 100%;
}

.jp-FormGroup-contentCompact .form-group {
  display: flex;
  padding: 0.5em 0.2em 0.5em 0;
}

.jp-FormGroup-contentCompact
  .jp-FormGroup-compactTitle
  .jp-FormGroup-description {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color2);
}

.jp-FormGroup-contentCompact .jp-FormGroup-fieldLabel {
  padding-bottom: 0.3em;
}

.jp-FormGroup-contentCompact .jp-inputFieldWrapper .form-control {
  width: 100%;
  box-sizing: border-box;
}

.jp-FormGroup-contentCompact .jp-arrayFieldWrapper .jp-FormGroup-compactTitle {
  padding-bottom: 7px;
}

.jp-FormGroup-contentCompact
  .jp-objectFieldWrapper
  .jp-objectFieldWrapper
  .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

.jp-FormGroup-contentCompact ul.error-detail {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
  padding-inline-start: 1em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-SidePanel {
  display: flex;
  flex-direction: column;
  min-width: var(--jp-sidebar-min-width);
  overflow-y: auto;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size1);
}

.jp-SidePanel-header {
  flex: 0 0 auto;
  display: flex;
  border-bottom: var(--jp-border-width) solid var(--jp-border-color2);
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin: 0;
  padding: 2px;
  text-transform: uppercase;
}

.jp-SidePanel-toolbar {
  flex: 0 0 auto;
}

.jp-SidePanel-content {
  flex: 1 1 auto;
}

.jp-SidePanel-toolbar,
.jp-AccordionPanel-toolbar {
  height: var(--jp-private-toolbar-height);
}

.jp-SidePanel-toolbar.jp-Toolbar-micro {
  display: none;
}

.lm-AccordionPanel .jp-AccordionPanel-title {
  box-sizing: border-box;
  line-height: 25px;
  margin: 0;
  display: flex;
  align-items: center;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  font-size: var(--jp-ui-font-size0);
}

.jp-AccordionPanel-title {
  cursor: pointer;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  text-transform: uppercase;
}

.lm-AccordionPanel[data-orientation='horizontal'] > .jp-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleLabel {
  user-select: none;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleCollapser {
  transform: rotate(-90deg);
  margin: auto 0;
  height: 16px;
}

.jp-AccordionPanel-title.lm-mod-expanded .lm-AccordionPanel-titleCollapser {
  transform: rotate(0deg);
}

.lm-AccordionPanel .jp-AccordionPanel-toolbar {
  background: none;
  box-shadow: none;
  border: none;
  margin-left: auto;
}

.lm-AccordionPanel .lm-SplitPanel-handle:hover {
  background: var(--jp-layout-color3);
}

.jp-text-truncated {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent::before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent::after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input[type='checkbox'].jp-mod-styled {
  appearance: checkbox;
  -webkit-appearance: checkbox;
  -moz-appearance: checkbox;
  height: auto;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper:not(.multiple) {
  height: 28px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select.jp-mod-styled:not([multiple]) {
  height: 32px;
}

select.jp-mod-styled[multiple] {
  max-height: 200px;
  overflow-y: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-switch {
  display: flex;
  align-items: center;
  padding-left: 4px;
  padding-right: 4px;
  font-size: var(--jp-ui-font-size1);
  background-color: transparent;
  color: var(--jp-ui-font-color1);
  border: none;
  height: 20px;
}

.jp-switch:hover {
  background-color: var(--jp-layout-color2);
}

.jp-switch-label {
  margin-right: 5px;
  font-family: var(--jp-ui-font-family);
}

.jp-switch-track {
  cursor: pointer;
  background-color: var(--jp-switch-color, var(--jp-border-color1));
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
  height: 16px;
  width: 35px;
  position: relative;
}

.jp-switch-track::before {
  content: '';
  position: absolute;
  height: 10px;
  width: 10px;
  margin: 3px;
  left: 0;
  background-color: var(--jp-ui-inverse-font-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

.jp-switch[aria-checked='true'] .jp-switch-track {
  background-color: var(--jp-switch-true-position-color, var(--jp-warn-color0));
}

.jp-switch[aria-checked='true'] .jp-switch-track::before {
  /* track width (35) - margins (3 + 3) - thumb width (10) */
  left: 19px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 8;
  overflow-x: hidden;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0;
  margin: 0;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0 6px;
  margin: 0;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent > span {
  padding: 0;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar.jp-Toolbar-micro {
  padding: 0;
  min-height: 0;
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar {
  border: none;
  box-shadow: none;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-WindowedPanel-outer {
  position: relative;
  overflow-y: auto;
}

.jp-WindowedPanel-inner {
  position: relative;
}

.jp-WindowedPanel-window {
  position: absolute;
  left: 0;
  right: 0;
  overflow: visible;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

body {
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
}

/* Disable native link decoration styles everywhere outside of dialog boxes */
a {
  text-decoration: unset;
  color: unset;
}

a:hover {
  text-decoration: unset;
  color: unset;
}

/* Accessibility for links inside dialog box text */
.jp-Dialog-content a {
  text-decoration: revert;
  color: var(--jp-content-link-color);
}

.jp-Dialog-content a:hover {
  text-decoration: revert;
}

/* Styles for ui-components */
.jp-Button {
  color: var(--jp-ui-font-color2);
  border-radius: var(--jp-border-radius);
  padding: 0 12px;
  font-size: var(--jp-ui-font-size1);

  /* Copy from blueprint 3 */
  display: inline-flex;
  flex-direction: row;
  border: none;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  text-align: left;
  vertical-align: middle;
  min-height: 30px;
  min-width: 30px;
}

.jp-Button:disabled {
  cursor: not-allowed;
}

.jp-Button:empty {
  padding: 0 !important;
}

.jp-Button.jp-mod-small {
  min-height: 24px;
  min-width: 24px;
  font-size: 12px;
  padding: 0 7px;
}

/* Use our own theme for hover styles */
.jp-Button.jp-mod-minimal:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Button.jp-mod-minimal {
  background: none;
}

.jp-InputGroup {
  display: block;
  position: relative;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border: none;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
  padding-bottom: 0;
  padding-top: 0;
  padding-left: 10px;
  padding-right: 28px;
  position: relative;
  width: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  font-weight: 400;
  height: 30px;
  line-height: 30px;
  outline: none;
  vertical-align: middle;
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input:disabled {
  cursor: not-allowed;
  resize: block;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input:disabled ~ span {
  cursor: not-allowed;
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color2);
}

.jp-InputGroupAction {
  position: absolute;
  bottom: 1px;
  right: 0;
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
  cursor: not-allowed;
  resize: block;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled ~ span {
  cursor: not-allowed;
}

/* Use our own theme for hover and option styles */
/* stylelint-disable-next-line selector-max-type */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}

select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-StatusBar-Widget {
  display: flex;
  align-items: center;
  background: var(--jp-layout-color2);
  min-height: var(--jp-statusbar-height);
  justify-content: space-between;
  padding: 0 10px;
}

.jp-StatusBar-Left {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-StatusBar-Middle {
  display: flex;
  align-items: center;
}

.jp-StatusBar-Right {
  display: flex;
  align-items: center;
  flex-direction: row-reverse;
}

.jp-StatusBar-Item {
  max-height: var(--jp-statusbar-height);
  margin: 0 2px;
  height: var(--jp-statusbar-height);
  white-space: nowrap;
  text-overflow: ellipsis;
  color: var(--jp-ui-font-color1);
  padding: 0 6px;
}

.jp-mod-highlighted:hover {
  background-color: var(--jp-layout-color3);
}

.jp-mod-clicked {
  background-color: var(--jp-brand-color1);
}

.jp-mod-clicked:hover {
  background-color: var(--jp-brand-color0);
}

.jp-mod-clicked .jp-StatusBar-TextItem {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-StatusBar-HoverItem {
  box-shadow: '0px 4px 4px rgba(0, 0, 0, 0.25)';
}

.jp-StatusBar-TextItem {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  line-height: 24px;
  color: var(--jp-ui-font-color1);
}

.jp-StatusBar-GroupItem {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-Statusbar-ProgressCircle svg {
  display: block;
  margin: 0 auto;
  width: 16px;
  height: 24px;
  align-self: normal;
}

.jp-Statusbar-ProgressCircle path {
  fill: var(--jp-inverse-layout-color3);
}

.jp-Statusbar-ProgressBar-progress-bar {
  height: 10px;
  width: 100px;
  border: solid 0.25px var(--jp-brand-color2);
  border-radius: 3px;
  overflow: hidden;
  align-self: center;
}

.jp-Statusbar-ProgressBar-progress-bar > div {
  background-color: var(--jp-brand-color2);
  background-image: linear-gradient(
    -45deg,
    rgba(255, 255, 255, 0.2) 25%,
    transparent 25%,
    transparent 50%,
    rgba(255, 255, 255, 0.2) 50%,
    rgba(255, 255, 255, 0.2) 75%,
    transparent 75%,
    transparent
  );
  background-size: 40px 40px;
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 14px;
  color: #fff;
  text-align: center;
  animation: jp-Statusbar-ExecutionTime-progress-bar 2s linear infinite;
}

.jp-Statusbar-ProgressBar-progress-bar p {
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  line-height: 10px;
  width: 100px;
}

@keyframes jp-Statusbar-ExecutionTime-progress-bar {
  0% {
    background-position: 0 0;
  }

  100% {
    background-position: 40px 40px;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Modal variant
|----------------------------------------------------------------------------*/

.jp-ModalCommandPalette {
  position: absolute;
  z-index: 10000;
  top: 38px;
  left: 30%;
  margin: 0;
  padding: 4px;
  width: 40%;
  box-shadow: var(--jp-elevation-z4);
  border-radius: 4px;
  background: var(--jp-layout-color0);
}

.jp-ModalCommandPalette .lm-CommandPalette {
  max-height: 40vh;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-close-icon::after {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-header {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-item {
  margin-left: 4px;
  margin-right: 4px;
}

.jp-ModalCommandPalette
  .lm-CommandPalette
  .lm-CommandPalette-item.lm-mod-disabled {
  display: none;
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-SearchIconGroup {
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  padding: 5px 5px 1px;
}

.jp-SearchIconGroup svg {
  height: 20px;
  width: 20px;
}

.jp-SearchIconGroup .jp-icon3[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color2);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item.lm-mod-active {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active .jp-icon-selectable[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.6;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty::after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px 24px 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
  resize: both;
}

.jp-Dialog-content.jp-Dialog-content-small {
  max-width: 500px;
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus {
  outline: 1px solid var(--jp-accept-color-normal, var(--jp-brand-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus {
  outline: 1px solid var(--jp-warn-color-normal, var(--jp-error-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline: 1px solid var(--jp-reject-color-normal, var(--md-grey-600));
}

button.jp-Dialog-close-button {
  padding: 0;
  height: 100%;
  min-width: unset;
  min-height: unset;
}

.jp-Dialog-header {
  display: flex;
  justify-content: space-between;
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-checkbox {
  padding-right: 5px;
}

.jp-Dialog-checkbox > input:focus-visible {
  outline: 1px solid var(--jp-input-active-border-color);
  outline-offset: 1px;
}

.jp-Dialog-spacer {
  flex: 1 1 auto;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Input-Boolean-Dialog {
  flex-direction: row-reverse;
  align-items: end;
  width: 100%;
}

.jp-Input-Boolean-Dialog > label {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error {
  padding: 6px;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error > pre {
  width: auto;
  padding: 10px;
  background: var(--jp-error-color3);
  border: var(--jp-border-width) solid var(--jp-error-color1);
  border-radius: var(--jp-border-radius);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  white-space: pre-wrap;
  word-wrap: break-word;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;
  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;
  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #a0f;
  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;
  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;
  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;
  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;
  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;
  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;
  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;
  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;
  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;
  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ff0;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;
  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;
  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;
  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;
  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;
  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;
  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

:root {
  /* This is the padding value to fill the gaps between lines containing spans with background color. */
  --jp-private-code-span-padding: calc(
    (var(--jp-code-line-height) - 1) * var(--jp-code-font-size) / 2
  );
}

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0;
  padding: 0;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}

.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}

.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}

.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}

.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}

.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}

.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}

.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}

.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}

.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}

.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}

.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}

.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}

.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}

.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}

.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}

.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);

  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

/* stylelint-disable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0;
}

/* stylelint-enable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  table-layout: fixed;
  margin-left: auto;
  margin-bottom: 1em;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}

[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}

.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}

.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}

.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}

.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}

.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}

.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}

.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}

.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: var(--jp-ui-font-size0);
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-cursor-backdrop {
  position: fixed;
  width: 200px;
  height: 200px;
  margin-top: -100px;
  margin-left: -100px;
  will-change: transform;
  z-index: 100;
}

.lm-mod-drag-image {
  will-change: transform;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-lineFormSearch {
  padding: 4px 12px;
  background-color: var(--jp-layout-color2);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
  font-size: var(--jp-ui-font-size1);
}

.jp-lineFormCaption {
  font-size: var(--jp-ui-font-size0);
  line-height: var(--jp-ui-font-size1);
  margin-top: 4px;
  color: var(--jp-ui-font-color0);
}

.jp-baseLineForm {
  border: none;
  border-radius: 0;
  position: absolute;
  background-size: 16px;
  background-repeat: no-repeat;
  background-position: center;
  outline: none;
}

.jp-lineFormButtonContainer {
  top: 4px;
  right: 8px;
  height: 24px;
  padding: 0 12px;
  width: 12px;
}

.jp-lineFormButtonIcon {
  top: 0;
  right: 0;
  background-color: var(--jp-brand-color1);
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  padding: 4px 6px;
}

.jp-lineFormButton {
  top: 0;
  right: 0;
  background-color: transparent;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.jp-lineFormWrapper {
  overflow: hidden;
  padding: 0 8px;
  border: 1px solid var(--jp-border-color0);
  background-color: var(--jp-input-active-background);
  height: 22px;
}

.jp-lineFormWrapperFocusWithin {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-lineFormInput {
  background: transparent;
  width: 200px;
  height: 100%;
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  line-height: 28px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/
.jp-DocumentSearch-input {
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  font-size: var(--jp-ui-font-size1);
  background-color: var(--jp-layout-color0);
  font-family: var(--jp-ui-font-family);
  padding: 2px 1px;
  resize: none;
}

.jp-DocumentSearch-overlay {
  position: absolute;
  background-color: var(--jp-toolbar-background);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  border-left: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  top: 0;
  right: 0;
  z-index: 7;
  min-width: 405px;
  padding: 2px;
  font-size: var(--jp-ui-font-size1);

  --jp-private-document-search-button-height: 20px;
}

.jp-DocumentSearch-overlay button {
  background-color: var(--jp-toolbar-background);
  outline: 0;
}

.jp-DocumentSearch-overlay button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-overlay button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-overlay-row {
  display: flex;
  align-items: center;
  margin-bottom: 2px;
}

.jp-DocumentSearch-button-content {
  display: inline-block;
  cursor: pointer;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-button-content svg {
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-input-wrapper {
  border: var(--jp-border-width) solid var(--jp-border-color0);
  display: flex;
  background-color: var(--jp-layout-color0);
  margin: 2px;
}

.jp-DocumentSearch-input-wrapper:focus-within {
  border-color: var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper {
  all: initial;
  overflow: hidden;
  display: inline-block;
  border: none;
  box-sizing: border-box;
}

.jp-DocumentSearch-toggle-wrapper {
  width: 14px;
  height: 14px;
}

.jp-DocumentSearch-button-wrapper {
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
}

.jp-DocumentSearch-toggle-wrapper:focus,
.jp-DocumentSearch-button-wrapper:focus {
  outline: var(--jp-border-width) solid
    var(--jp-cell-editor-active-border-color);
  outline-offset: -1px;
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper,
.jp-DocumentSearch-button-content:focus {
  outline: none;
}

.jp-DocumentSearch-toggle-placeholder {
  width: 5px;
}

.jp-DocumentSearch-input-button::before {
  display: block;
  padding-top: 100%;
}

.jp-DocumentSearch-input-button-off {
  opacity: var(--jp-search-toggle-off-opacity);
}

.jp-DocumentSearch-input-button-off:hover {
  opacity: var(--jp-search-toggle-hover-opacity);
}

.jp-DocumentSearch-input-button-on {
  opacity: var(--jp-search-toggle-on-opacity);
}

.jp-DocumentSearch-index-counter {
  padding-left: 10px;
  padding-right: 10px;
  user-select: none;
  min-width: 35px;
  display: inline-block;
}

.jp-DocumentSearch-up-down-wrapper {
  display: inline-block;
  padding-right: 2px;
  margin-left: auto;
  white-space: nowrap;
}

.jp-DocumentSearch-spacer {
  margin-left: auto;
}

.jp-DocumentSearch-up-down-wrapper button {
  outline: 0;
  border: none;
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
  vertical-align: middle;
  margin: 1px 5px 2px;
}

.jp-DocumentSearch-up-down-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-up-down-button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-filter-button {
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-filter-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled:hover {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-search-options {
  padding: 0 8px;
  margin-left: 3px;
  width: 100%;
  display: grid;
  justify-content: start;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  justify-items: stretch;
}

.jp-DocumentSearch-search-filter-disabled {
  color: var(--jp-ui-font-color2);
}

.jp-DocumentSearch-search-filter {
  display: flex;
  align-items: center;
  user-select: none;
}

.jp-DocumentSearch-regex-error {
  color: var(--jp-error-color0);
}

.jp-DocumentSearch-replace-button-wrapper {
  overflow: hidden;
  display: inline-block;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color0);
  margin: auto 2px;
  padding: 1px 4px;
  height: calc(var(--jp-private-document-search-button-height) + 2px);
}

.jp-DocumentSearch-replace-button-wrapper:focus {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-replace-button {
  display: inline-block;
  text-align: center;
  cursor: pointer;
  box-sizing: border-box;
  color: var(--jp-ui-font-color1);

  /* height - 2 * (padding of wrapper) */
  line-height: calc(var(--jp-private-document-search-button-height) - 2px);
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-replace-button:focus {
  outline: none;
}

.jp-DocumentSearch-replace-wrapper-class {
  margin-left: 14px;
  display: flex;
}

.jp-DocumentSearch-replace-toggle {
  border: none;
  background-color: var(--jp-toolbar-background);
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-replace-toggle:hover {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.cm-editor {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;

  /* Changed to auto to autogrow */
}

.cm-editor pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .cm-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

.jp-CodeMirrorEditor {
  cursor: text;
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.cm-editor.jp-mod-readOnly .cm-cursor {
  display: none;
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.cm-searching,
.cm-searching span {
  /* `.cm-searching span`: we need to override syntax highlighting */
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.cm-searching::selection,
.cm-searching span::selection {
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.jp-current-match > .cm-searching,
.jp-current-match > .cm-searching span,
.cm-searching > .jp-current-match,
.cm-searching > .jp-current-match span {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.jp-current-match > .cm-searching::selection,
.cm-searching > .jp-current-match::selection,
.jp-current-match > .cm-searching span::selection {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.cm-trailingspace {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAFCAYAAAB4ka1VAAAAsElEQVQIHQGlAFr/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA7+r3zKmT0/+pk9P/7+r3zAAAAAAAAAAABAAAAAAAAAAA6OPzM+/q9wAAAAAA6OPzMwAAAAAAAAAAAgAAAAAAAAAAGR8NiRQaCgAZIA0AGR8NiQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQyoYJ/SY80UAAAAASUVORK5CYII=);
  background-position: center left;
  background-repeat: repeat-x;
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/* Styles for shared cursors (remote cursor locations and selected ranges) */
.jp-CodeMirrorEditor .cm-ySelectionCaret {
  position: relative;
  border-left: 1px solid black;
  margin-left: -1px;
  margin-right: -1px;
  box-sizing: border-box;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret > .cm-ySelectionInfo {
  white-space: nowrap;
  position: absolute;
  top: -1.15em;
  padding-bottom: 0.05em;
  left: -1px;
  font-size: 0.95em;
  font-family: var(--jp-ui-font-family);
  font-weight: bold;
  line-height: normal;
  user-select: none;
  color: white;
  padding-left: 2px;
  padding-right: 2px;
  z-index: 101;
  transition: opacity 0.3s ease-in-out;
}

.jp-CodeMirrorEditor .cm-ySelectionInfo {
  transition-delay: 0.7s;
  opacity: 0;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret:hover > .cm-ySelectionInfo {
  opacity: 1;
  transition-delay: 0s;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser .jp-SidePanel-content {
  display: flex;
  flex-direction: column;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  flex-wrap: wrap;
  row-gap: 12px;
  border-bottom: none;
  height: auto;
  margin: 8px 12px 0;
  box-shadow: none;
  padding: 0;
  justify-content: flex-start;
}

.jp-FileBrowser-Panel {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 8px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0 2px;
  padding: 0 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  padding-left: 0;
  padding-right: 2px;
  align-items: center;
  height: unset;
}

.jp-FileBrowser-toolbar > .jp-Toolbar-item .jp-ToolbarButtonComponent {
  width: 40px;
}

/*-----------------------------------------------------------------------------
| Other styles
|----------------------------------------------------------------------------*/

.jp-FileDialog.jp-mod-conflict input {
  color: var(--jp-error-color1);
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

.jp-LastModified-hidden {
  display: none;
}

.jp-FileSize-hidden {
  display: none;
}

.jp-FileBrowser .lm-AccordionPanel > h3:first-child {
  display: none;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-headerItem.jp-id-filesize {
  flex: 0 0 75px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-id-narrow {
  display: none;
  flex: 0 0 5px;
  padding: 4px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
  color: var(--jp-border-color2);
}

.jp-DirListing-narrow .jp-id-narrow {
  display: block;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-content mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.jp-DirListing-content .jp-DirListing-item.jp-mod-selected mark {
  color: var(--jp-ui-inverse-font-color0);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-checkboxWrapper {
  /* Increases hit area of checkbox. */
  padding: 4px;
}

.jp-DirListing-header
  .jp-DirListing-checkboxWrapper
  + .jp-DirListing-headerItem {
  padding-left: 4px;
}

.jp-DirListing-content .jp-DirListing-checkboxWrapper {
  position: relative;
  left: -4px;
  margin: -4px 0 -4px -8px;
}

.jp-DirListing-checkboxWrapper.jp-mod-visible {
  visibility: visible;
}

/* For devices that support hovering, hide checkboxes until hovered, selected...
*/
@media (hover: hover) {
  .jp-DirListing-checkboxWrapper {
    visibility: hidden;
  }

  .jp-DirListing-item:hover .jp-DirListing-checkboxWrapper,
  .jp-DirListing-item.jp-mod-selected .jp-DirListing-checkboxWrapper {
    visibility: visible;
  }
}

.jp-DirListing-item[data-is-dot] {
  opacity: 75%;
}

.jp-DirListing-item.jp-mod-selected {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemText:focus {
  outline-width: 2px;
  outline-color: var(--jp-inverse-layout-color1);
  outline-style: solid;
  outline-offset: 1px;
}

.jp-DirListing-item.jp-mod-selected .jp-DirListing-itemText:focus {
  outline-color: var(--jp-layout-color1);
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-itemFileSize {
  flex: 0 0 90px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon::before {
  color: var(--jp-success-color1);
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.jp-mod-running.jp-mod-selected
  .jp-DirListing-itemIcon::before {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-OutputPrompt {
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-prompt {
  display: table-cell;
  vertical-align: top;
}

.jp-OutputArea-output {
  display: table-cell;
  width: 100%;
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea .jp-RenderedText {
  padding-left: 1ch;
}

/**
 * Prompt overlay.
 */

.jp-OutputArea-promptOverlay {
  position: absolute;
  top: 0;
  width: var(--jp-cell-prompt-width);
  height: 100%;
  opacity: 0.5;
}

.jp-OutputArea-promptOverlay:hover {
  background: var(--jp-layout-color2);
  box-shadow: inset 0 0 1px var(--jp-inverse-layout-color0);
  cursor: zoom-out;
}

.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay:hover {
  cursor: zoom-in;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0;
  padding: 0;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

.jp-TrimmedOutputs pre {
  background: var(--jp-layout-color3);
  font-size: calc(var(--jp-code-font-size) * 1.4);
  text-align: center;
  text-transform: uppercase;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/* Hide empty lines in the output area, for instance due to cleared widgets */
.jp-OutputArea-prompt:empty {
  padding: 0;
  border: 0;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0;
  width: 100%;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
  border-top: var(--jp-border-width) solid transparent;
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;

  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;

  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0 0.25em;
  margin: 0 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input::placeholder {
  opacity: 0;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

.jp-Stdin-input:focus::placeholder {
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

@media print {
  .jp-OutputArea-child {
    break-inside: avoid-page;
  }
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-OutputPrompt {
    display: table-row;
    text-align: left;
  }

  .jp-OutputArea-child .jp-OutputArea-output {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }
}

/* Trimmed outputs warning */
.jp-TrimmedOutputs > a {
  margin: 10px;
  text-decoration: none;
  cursor: pointer;
}

.jp-TrimmedOutputs > a:hover {
  text-decoration: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Table of Contents
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toc-active-width: 4px;
}

.jp-TableOfContents {
  display: flex;
  flex-direction: column;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  height: 100%;
}

.jp-TableOfContents-placeholder {
  text-align: center;
}

.jp-TableOfContents-placeholderContent {
  color: var(--jp-content-font-color2);
  padding: 8px;
}

.jp-TableOfContents-placeholderContent > h3 {
  margin-bottom: var(--jp-content-heading-margin-bottom);
}

.jp-TableOfContents .jp-SidePanel-content {
  overflow-y: auto;
}

.jp-TableOfContents-tree {
  margin: 4px;
}

.jp-TableOfContents ol {
  list-style-type: none;
}

/* stylelint-disable-next-line selector-max-type */
.jp-TableOfContents li > ol {
  /* Align left border with triangle icon center */
  padding-left: 11px;
}

.jp-TableOfContents-content {
  /* left margin for the active heading indicator */
  margin: 0 0 0 var(--jp-private-toc-active-width);
  padding: 0;
  background-color: var(--jp-layout-color1);
}

.jp-tocItem {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-tocItem-heading {
  display: flex;
  cursor: pointer;
}

.jp-tocItem-heading:hover {
  background-color: var(--jp-layout-color2);
}

.jp-tocItem-content {
  display: block;
  padding: 4px 0;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow-x: hidden;
}

.jp-tocItem-collapser {
  height: 20px;
  margin: 2px 2px 0;
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
}

.jp-tocItem-collapser:hover {
  background-color: var(--jp-layout-color3);
}

/* Active heading indicator */

.jp-tocItem-heading::before {
  content: ' ';
  background: transparent;
  width: var(--jp-private-toc-active-width);
  height: 24px;
  position: absolute;
  left: 0;
  border-radius: var(--jp-border-radius);
}

.jp-tocItem-heading.jp-tocItem-active::before {
  background-color: var(--jp-brand-color1);
}

.jp-tocItem-heading:hover.jp-tocItem-active::before {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;

  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0;
  bottom: 0;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Hiding collapsers in print mode.

Note: input and output wrappers have "display: block" propery in print mode.
*/

@media print {
  .jp-Collapser {
    display: none;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0;
  width: 100%;
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-InputArea-editor {
  display: table-cell;
  overflow: hidden;
  vertical-align: top;

  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  display: table-cell;
  vertical-align: top;
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-InputArea-editor {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }

  .jp-InputPrompt {
    display: table-row;
    text-align: left;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: table;
  table-layout: fixed;
  width: 100%;
}

.jp-Placeholder-prompt {
  display: table-cell;
  box-sizing: border-box;
}

.jp-Placeholder-content {
  display: table-cell;
  padding: 4px 6px;
  border: 1px solid transparent;
  border-radius: 0;
  background: none;
  box-sizing: border-box;
  cursor: pointer;
}

.jp-Placeholder-contentContainer {
  display: flex;
}

.jp-Placeholder-content:hover,
.jp-InputPlaceholder > .jp-Placeholder-content:hover {
  border-color: var(--jp-layout-color3);
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

.jp-PlaceholderText {
  white-space: nowrap;
  overflow-x: hidden;
  color: var(--jp-inverse-layout-color3);
  font-family: var(--jp-code-font-family);
}

.jp-InputPlaceholder > .jp-Placeholder-content {
  border-color: var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0;
  margin: 0;

  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 24em;
  margin-left: var(--jp-private-cell-scrolling-output-offset);
  resize: vertical;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea[style*='height'] {
  max-height: unset;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea::after {
  content: ' ';
  box-shadow: inset 0 0 6px 2px rgb(0 0 0 / 30%);
  width: 100%;
  height: 100%;
  position: sticky;
  bottom: 0;
  top: 0;
  margin-top: -50%;
  float: left;
  display: block;
  pointer-events: none;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-child {
  padding-top: 6px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  width: calc(
    var(--jp-cell-prompt-width) - var(--jp-private-cell-scrolling-output-offset)
  );
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay {
  left: calc(-1 * var(--jp-private-cell-scrolling-output-offset));
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  display: table-cell;
  width: 100%;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/* collapseHeadingButton (show always if hiddenCellsButton is _not_ shown) */
.jp-collapseHeadingButton {
  display: flex;
  min-height: var(--jp-cell-collapser-min-height);
  font-size: var(--jp-code-font-size);
  position: absolute;
  background-color: transparent;
  background-size: 25px;
  background-repeat: no-repeat;
  background-position-x: center;
  background-position-y: top;
  background-image: var(--jp-icon-caret-down);
  right: 0;
  top: 0;
  bottom: 0;
}

.jp-collapseHeadingButton.jp-mod-collapsed {
  background-image: var(--jp-icon-caret-right);
}

/*
 set the container font size to match that of content
 so that the nested collapse buttons have the right size
*/
.jp-MarkdownCell .jp-InputPrompt {
  font-size: var(--jp-content-font-size1);
}

/*
  Align collapseHeadingButton with cell top header
  The font sizes are identical to the ones in packages/rendermime/style/base.css
*/
.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='1'] {
  font-size: var(--jp-content-font-size5);
  background-position-y: calc(0.3 * var(--jp-content-font-size5));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='2'] {
  font-size: var(--jp-content-font-size4);
  background-position-y: calc(0.3 * var(--jp-content-font-size4));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='3'] {
  font-size: var(--jp-content-font-size3);
  background-position-y: calc(0.3 * var(--jp-content-font-size3));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='4'] {
  font-size: var(--jp-content-font-size2);
  background-position-y: calc(0.3 * var(--jp-content-font-size2));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='5'] {
  font-size: var(--jp-content-font-size1);
  background-position-y: top;
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='6'] {
  font-size: var(--jp-content-font-size0);
  background-position-y: top;
}

/* collapseHeadingButton (show only on (hover,active) if hiddenCellsButton is shown) */
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-collapseHeadingButton {
  display: none;
}

.jp-Notebook.jp-mod-showHiddenCellsButton
  :is(.jp-MarkdownCell:hover, .jp-mod-active)
  .jp-collapseHeadingButton {
  display: flex;
}

/* showHiddenCellsButton (only show if jp-mod-showHiddenCellsButton is set, which
is a consequence of the showHiddenCellsButton option in Notebook Settings)*/
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton {
  margin-left: calc(var(--jp-cell-prompt-width) + 2 * var(--jp-code-padding));
  margin-top: var(--jp-code-padding);
  border: 1px solid var(--jp-border-color2);
  background-color: var(--jp-border-color3) !important;
  color: var(--jp-content-font-color0) !important;
  display: flex;
}

.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton:hover {
  background-color: var(--jp-border-color2) !important;
}

.jp-showHiddenCellsButton {
  display: none;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Using block instead of flex to allow the use of the break-inside CSS property for
cell outputs.
*/

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-notebook-toolbar-padding: 2px 5px 2px 2px;
}

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: var(--jp-notebook-toolbar-padding);

  /* disable paint containment from lumino 2.0 default strict CSS containment */
  contain: style size !important;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

.jp-Toolbar-responsive-popup {
  position: absolute;
  height: fit-content;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: var(--jp-notebook-toolbar-padding);
  z-index: 1;
  right: 0;
  top: 0;
}

.jp-Toolbar > .jp-Toolbar-responsive-opener {
  margin-left: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-Notebook-ExecutionIndicator {
  position: relative;
  display: inline-block;
  height: 100%;
  z-index: 9997;
}

.jp-Notebook-ExecutionIndicator-tooltip {
  visibility: hidden;
  height: auto;
  width: max-content;
  width: -moz-max-content;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color1);
  text-align: justify;
  border-radius: 6px;
  padding: 0 5px;
  position: fixed;
  display: table;
}

.jp-Notebook-ExecutionIndicator-tooltip.up {
  transform: translateX(-50%) translateY(-100%) translateY(-32px);
}

.jp-Notebook-ExecutionIndicator-tooltip.down {
  transform: translateX(calc(-100% + 16px)) translateY(5px);
}

.jp-Notebook-ExecutionIndicator-tooltip.hidden {
  display: none;
}

.jp-Notebook-ExecutionIndicator:hover .jp-Notebook-ExecutionIndicator-tooltip {
  visibility: visible;
}

.jp-Notebook-ExecutionIndicator span {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  color: var(--jp-ui-font-color1);
  line-height: 24px;
  display: block;
}

.jp-Notebook-ExecutionIndicator-progress-bar {
  display: flex;
  justify-content: center;
  height: 100%;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*
 * Execution indicator
 */
.jp-tocItem-content::after {
  content: '';

  /* Must be identical to form a circle */
  width: 12px;
  height: 12px;
  background: none;
  border: none;
  position: absolute;
  right: 0;
}

.jp-tocItem-content[data-running='0']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background: none;
}

.jp-tocItem-content[data-running='1']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background-color: var(--jp-inverse-layout-color3);
}

.jp-tocItem-content[data-running='0'],
.jp-tocItem-content[data-running='1'] {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Notebook-footer {
  height: 27px;
  margin-left: calc(
    var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
      var(--jp-cell-padding)
  );
  width: calc(
    100% -
      (
        var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
          var(--jp-cell-padding) + var(--jp-cell-padding)
      )
  );
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  color: var(--jp-ui-font-color3);
  margin-top: 6px;
  background: none;
  cursor: pointer;
}

.jp-Notebook-footer:focus {
  border-color: var(--jp-cell-editor-active-border-color);
}

/* For devices that support hovering, hide footer until hover */
@media (hover: hover) {
  .jp-Notebook-footer {
    opacity: 0;
  }

  .jp-Notebook-footer:focus,
  .jp-Notebook-footer:hover {
    opacity: 1;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-side-by-side-output-size: 1fr;
  --jp-side-by-side-resized-cell: var(--jp-side-by-side-output-size);
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

/* stylelint-disable selector-max-class */

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-MainAreaWidget-ContainStrict .jp-Notebook * {
  contain: strict;
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* cell is dirty */
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt {
  color: var(--jp-warn-color1);
}

.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt::before {
  color: var(--jp-warn-color1);
  content: '•';
}

.jp-Notebook .jp-Cell.jp-mod-active.jp-mod-dirty .jp-Collapser {
  background: var(--jp-warn-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: block;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-ActiveCellTool {
  padding: 12px 0;
  display: flex;
}

.jp-ActiveCellTool-Content {
  flex: 1 1 auto;
}

.jp-ActiveCellTool .jp-ActiveCellTool-CellContent {
  background: var(--jp-cell-editor-background);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  min-height: 29px;
}

.jp-ActiveCellTool .jp-InputPrompt {
  min-width: calc(var(--jp-cell-prompt-width) * 0.75);
}

.jp-ActiveCellTool-CellContent > pre {
  padding: 5px 4px;
  margin: 0;
  white-space: normal;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label,
.jp-NumberSetter label {
  line-height: 1.4;
}

.jp-NotebookTools .jp-select-wrapper {
  margin-top: 4px;
  margin-bottom: 0;
}

.jp-NumberSetter input {
  width: 100%;
  margin-top: 4px;
}

.jp-NotebookTools .jp-Collapse {
  margin-top: 16px;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Side-by-side Mode (.jp-mod-sideBySide)
|----------------------------------------------------------------------------*/
.jp-mod-sideBySide.jp-Notebook .jp-Notebook-cell {
  margin-top: 3em;
  margin-bottom: 3em;
  margin-left: 5%;
  margin-right: 5%;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell {
  display: grid;
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-output-size)
    );
  grid-template-rows: auto minmax(0, 1fr) auto;
  grid-template-areas:
    'header header header'
    'input handle output'
    'footer footer footer';
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell.jp-mod-resizedCell {
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-resized-cell)
    );
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellHeader {
  grid-area: header;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-inputWrapper {
  grid-area: input;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-outputWrapper {
  /* overwrite the default margin (no vertical separation needed in side by side move */
  margin-top: 0;
  grid-area: output;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellFooter {
  grid-area: footer;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle {
  grid-area: handle;
  user-select: none;
  display: block;
  height: 100%;
  cursor: ew-resize;
  padding: 0 var(--jp-cell-padding);
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle::after {
  content: '';
  display: block;
  background: var(--jp-border-color2);
  height: 100%;
  width: 5px;
}

.jp-mod-sideBySide.jp-Notebook
  .jp-CodeCell.jp-mod-resizedCell
  .jp-CellResizeHandle::after {
  background: var(--jp-border-color0);
}

.jp-CellResizeHandle {
  display: none;
}

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Cell-Placeholder {
  padding-left: 55px;
}

.jp-Cell-Placeholder-wrapper {
  background: #fff;
  border: 1px solid;
  border-color: #e5e6e9 #dfe0e4 #d0d1d5;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  margin: 10px 15px;
}

.jp-Cell-Placeholder-wrapper-inner {
  padding: 15px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body {
  background-repeat: repeat;
  background-size: 50% auto;
}

.jp-Cell-Placeholder-wrapper-body div {
  background: #f6f7f8;
  background-image: -webkit-linear-gradient(
    left,
    #f6f7f8 0%,
    #edeef1 20%,
    #f6f7f8 40%,
    #f6f7f8 100%
  );
  background-repeat: no-repeat;
  background-size: 800px 104px;
  height: 104px;
  position: absolute;
  right: 15px;
  left: 15px;
  top: 15px;
}

div.jp-Cell-Placeholder-h1 {
  top: 20px;
  height: 20px;
  left: 15px;
  width: 150px;
}

div.jp-Cell-Placeholder-h2 {
  left: 15px;
  top: 50px;
  height: 10px;
  width: 100px;
}

div.jp-Cell-Placeholder-content-1,
div.jp-Cell-Placeholder-content-2,
div.jp-Cell-Placeholder-content-3 {
  left: 15px;
  right: 15px;
  height: 10px;
}

div.jp-Cell-Placeholder-content-1 {
  top: 100px;
}

div.jp-Cell-Placeholder-content-2 {
  top: 120px;
}

div.jp-Cell-Placeholder-content-3 {
  top: 140px;
}

</style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0 2px 1px -1px var(--jp-shadow-umbra-color),
    0 1px 1px 0 var(--jp-shadow-penumbra-color),
    0 1px 3px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0 3px 1px -2px var(--jp-shadow-umbra-color),
    0 2px 2px 0 var(--jp-shadow-penumbra-color),
    0 1px 5px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0 2px 4px -1px var(--jp-shadow-umbra-color),
    0 4px 5px 0 var(--jp-shadow-penumbra-color),
    0 1px 10px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0 3px 5px -1px var(--jp-shadow-umbra-color),
    0 6px 10px 0 var(--jp-shadow-penumbra-color),
    0 1px 18px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0 5px 5px -3px var(--jp-shadow-umbra-color),
    0 8px 10px 1px var(--jp-shadow-penumbra-color),
    0 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0 7px 8px -4px var(--jp-shadow-umbra-color),
    0 12px 17px 2px var(--jp-shadow-penumbra-color),
    0 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0 8px 10px -5px var(--jp-shadow-umbra-color),
    0 16px 24px 2px var(--jp-shadow-penumbra-color),
    0 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0 10px 13px -6px var(--jp-shadow-umbra-color),
    0 20px 31px 3px var(--jp-shadow-penumbra-color),
    0 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0 11px 15px -7px var(--jp-shadow-umbra-color),
    0 24px 38px 3px var(--jp-shadow-penumbra-color),
    0 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-inverse-border-color: var(--md-grey-600);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;
  --jp-ui-font-family: system-ui, -apple-system, blinkmacsystemfont, 'Segoe UI',
    helvetica, arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;
  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);
  --jp-content-link-color: var(--md-blue-900);
  --jp-content-font-family: system-ui, -apple-system, blinkmacsystemfont,
    'Segoe UI', helvetica, arial, sans-serif, 'Apple Color Emoji',
    'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: menlo, consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-900);
  --jp-brand-color1: var(--md-blue-700);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);
  --jp-accent-color0: var(--md-green-900);
  --jp-accent-color1: var(--md-green-700);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-900);
  --jp-warn-color1: var(--md-orange-700);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);
  --jp-error-color0: var(--md-red-900);
  --jp-error-color1: var(--md-red-700);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);
  --jp-success-color0: var(--md-green-900);
  --jp-success-color1: var(--md-green-700);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);
  --jp-info-color0: var(--md-cyan-900);
  --jp-info-color1: var(--md-cyan-700);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;
  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;
  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);
  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: var(--jp-code-font-family-default);
  --jp-cell-prompt-letter-spacing: 0;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);

  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;

  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Statusbar specific styles */

  --jp-statusbar-height: 24px;

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-inverse-border-color);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: rgb(0, 54, 109);
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #a2f;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #a2f;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /*
    RTC user specific colors.
    These colors are used for the cursor, username in the editor,
    and the icon of the user.
  */

  --jp-collaborator-color1: #ffad8e;
  --jp-collaborator-color2: #dac83d;
  --jp-collaborator-color3: #72dd76;
  --jp-collaborator-color4: #00e4d0;
  --jp-collaborator-color5: #45d4ff;
  --jp-collaborator-color6: #e2b1ff;
  --jp-collaborator-color7: #ff9de6;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 250px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);

  /* Button colors */
  --jp-accept-color-normal: var(--md-blue-700);
  --jp-accept-color-hover: var(--md-blue-800);
  --jp-accept-color-active: var(--md-blue-900);
  --jp-warn-color-normal: var(--md-red-700);
  --jp-warn-color-hover: var(--md-red-800);
  --jp-warn-color-active: var(--md-red-900);
  --jp-reject-color-normal: var(--md-grey-600);
  --jp-reject-color-hover: var(--md-grey-700);
  --jp-reject-color-active: var(--md-grey-800);

  /* File or activity icons and switch semantic variables */
  --jp-jupyter-icon-color: #f37626;
  --jp-notebook-icon-color: #f37626;
  --jp-json-icon-color: var(--md-orange-700);
  --jp-console-icon-background-color: var(--md-blue-700);
  --jp-console-icon-color: white;
  --jp-terminal-icon-background-color: var(--md-grey-800);
  --jp-terminal-icon-color: var(--md-grey-200);
  --jp-text-editor-icon-color: var(--md-grey-700);
  --jp-inspector-icon-color: var(--md-grey-700);
  --jp-switch-color: var(--md-grey-400);
  --jp-switch-true-position-color: var(--md-orange-900);
}
</style>
<style type="text/css">
/* Force rendering true colors when outputing to pdf */
* {
  -webkit-print-color-adjust: exact;
}

/* Misc */
a.anchor-link {
  display: none;
}

/* Input area styling */
.jp-InputArea {
  overflow: hidden;
}

.jp-InputArea-editor {
  overflow: hidden;
}

.cm-editor.cm-s-jupyter .highlight pre {
/* weird, but --jp-code-padding defined to be 5px but 4px horizontal padding is hardcoded for pre.cm-line */
  padding: var(--jp-code-padding) 4px;
  margin: 0;

  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  color: inherit;

}

.jp-OutputArea-output pre {
  line-height: inherit;
  font-family: inherit;
}

.jp-RenderedText pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
}

/* Hiding the collapser by default */
.jp-Collapser {
  display: none;
}

@page {
    margin: 0.5in; /* Margin for each printed piece of paper */
}

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}
</style>
<!-- Load mathjax -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-AMS_CHTML-full,Safe"> </script>
<!-- MathJax configuration -->
<script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                messageStyle: 'none',
                CommonHTML: {
                    linebreaks: {
                    automatic: true
                    }
                }
            });

            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
<!-- End of mathjax configuration --><script type="module">
  document.addEventListener("DOMContentLoaded", async () => {
    const diagrams = document.querySelectorAll(".jp-Mermaid > pre.mermaid");
    // do not load mermaidjs if not needed
    if (!diagrams.length) {
      return;
    }
    const mermaid = (await import("https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.7.0/mermaid.esm.min.mjs")).default;
    const parser = new DOMParser();

    mermaid.initialize({
      maxTextSize: 100000,
      maxEdges: 100000,
      startOnLoad: false,
      fontFamily: window
        .getComputedStyle(document.body)
        .getPropertyValue("--jp-ui-font-family"),
      theme: document.querySelector("body[data-jp-theme-light='true']")
        ? "default"
        : "dark",
    });

    let _nextMermaidId = 0;

    function makeMermaidImage(svg) {
      const img = document.createElement("img");
      const doc = parser.parseFromString(svg, "image/svg+xml");
      const svgEl = doc.querySelector("svg");
      const { maxWidth } = svgEl?.style || {};
      const firstTitle = doc.querySelector("title");
      const firstDesc = doc.querySelector("desc");

      img.setAttribute("src", `data:image/svg+xml,${encodeURIComponent(svg)}`);
      if (maxWidth) {
        img.width = parseInt(maxWidth);
      }
      if (firstTitle) {
        img.setAttribute("alt", firstTitle.textContent);
      }
      if (firstDesc) {
        const caption = document.createElement("figcaption");
        caption.className = "sr-only";
        caption.textContent = firstDesc.textContent;
        return [img, caption];
      }
      return [img];
    }

    async function makeMermaidError(text) {
      let errorMessage = "";
      try {
        await mermaid.parse(text);
      } catch (err) {
        errorMessage = `${err}`;
      }

      const result = document.createElement("details");
      result.className = 'jp-RenderedMermaid-Details';
      const summary = document.createElement("summary");
      summary.className = 'jp-RenderedMermaid-Summary';
      const pre = document.createElement("pre");
      const code = document.createElement("code");
      code.innerText = text;
      pre.appendChild(code);
      summary.appendChild(pre);
      result.appendChild(summary);

      const warning = document.createElement("pre");
      warning.innerText = errorMessage;
      result.appendChild(warning);
      return [result];
    }

    async function renderOneMarmaid(src) {
      const id = `jp-mermaid-${_nextMermaidId++}`;
      const parent = src.parentNode;
      let raw = src.textContent.trim();
      const el = document.createElement("div");
      el.style.visibility = "hidden";
      document.body.appendChild(el);
      let results = null;
      let output = null;
      try {
        let { svg } = await mermaid.render(id, raw, el);
        svg = cleanMermaidSvg(svg);
        results = makeMermaidImage(svg);
        output = document.createElement("figure");
        results.map(output.appendChild, output);
      } catch (err) {
        parent.classList.add("jp-mod-warning");
        results = await makeMermaidError(raw);
        output = results[0];
      } finally {
        el.remove();
      }
      parent.classList.add("jp-RenderedMermaid");
      parent.appendChild(output);
    }


    /**
     * Post-process to ensure mermaid diagrams contain only valid SVG and XHTML.
     */
    function cleanMermaidSvg(svg) {
      return svg.replace(RE_VOID_ELEMENT, replaceVoidElement);
    }


    /**
     * A regular expression for all void elements, which may include attributes and
     * a slash.
     *
     * @see https://developer.mozilla.org/en-US/docs/Glossary/Void_element
     *
     * Of these, only `<br>` is generated by Mermaid in place of `\n`,
     * but _any_ "malformed" tag will break the SVG rendering entirely.
     */
    const RE_VOID_ELEMENT =
      /<\s*(area|base|br|col|embed|hr|img|input|link|meta|param|source|track|wbr)\s*([^>]*?)\s*>/gi;

    /**
     * Ensure a void element is closed with a slash, preserving any attributes.
     */
    function replaceVoidElement(match, tag, rest) {
      rest = rest.trim();
      if (!rest.endsWith('/')) {
        rest = `${rest} /`;
      }
      return `<${tag} ${rest}>`;
    }

    void Promise.all([...diagrams].map(renderOneMarmaid));
  });
</script>
<style>
  .jp-Mermaid:not(.jp-RenderedMermaid) {
    display: none;
  }

  .jp-RenderedMermaid {
    overflow: auto;
    display: flex;
  }

  .jp-RenderedMermaid.jp-mod-warning {
    width: auto;
    padding: 0.5em;
    margin-top: 0.5em;
    border: var(--jp-border-width) solid var(--jp-warn-color2);
    border-radius: var(--jp-border-radius);
    color: var(--jp-ui-font-color1);
    font-size: var(--jp-ui-font-size1);
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  .jp-RenderedMermaid figure {
    margin: 0;
    overflow: auto;
    max-width: 100%;
  }

  .jp-RenderedMermaid img {
    max-width: 100%;
  }

  .jp-RenderedMermaid-Details > pre {
    margin-top: 1em;
  }

  .jp-RenderedMermaid-Summary {
    color: var(--jp-warn-color2);
  }

  .jp-RenderedMermaid:not(.jp-mod-warning) pre {
    display: none;
  }

  .jp-RenderedMermaid-Summary > pre {
    display: inline-block;
    white-space: normal;
  }
</style>
<!-- End of mermaid configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=c9703a66-8fc6-409b-a837-774ef94641b5">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Analiza-TITANIC">Analiza TITANIC<a class="anchor-link" href="#Analiza-TITANIC">¶</a></h1>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=bbb8dc32-759e-431d-a81f-24b258348e15">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Import-bibliotek">Import bibliotek<a class="anchor-link" href="#Import-bibliotek">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs" id="cell-id=6d1e2d55-840c-4323-9e0d-41834b3d3b3c">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [1]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span><span class="w"> </span><span class="nn">pandas</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">pd</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">matplotlib.pyplot</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">plt</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">seaborn</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">sns</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=c33d90e0-d631-4a70-a606-6d4da4165678">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Import-pliku-z-baz%C4%85-danych-i-pokazanie-10-losowych-wierszy">Import pliku z bazą danych i pokazanie 10 losowych wierszy<a class="anchor-link" href="#Import-pliku-z-baz%C4%85-danych-i-pokazanie-10-losowych-wierszy">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=4d5745ef-2646-4f44-a4c6-1e8186cac0af">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [2]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'26__titanic.csv'</span><span class="p">,</span> <span class="n">sep</span><span class="o">=</span><span class="s1">','</span><span class="p">)</span>

<span class="n">df</span><span class="o">.</span><span class="n">sample</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[2]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>pclass</th>
<th>survived</th>
<th>name</th>
<th>sex</th>
<th>age</th>
<th>sibsp</th>
<th>parch</th>
<th>ticket</th>
<th>fare</th>
<th>cabin</th>
<th>embarked</th>
<th>boat</th>
<th>body</th>
<th>home.dest</th>
</tr>
</thead>
<tbody>
<tr>
<th>480</th>
<td>2.0</td>
<td>0.0</td>
<td>Laroche, Mr. Joseph Philippe Lemercier</td>
<td>male</td>
<td>25.0</td>
<td>1.0</td>
<td>2.0</td>
<td>SC/Paris 2123</td>
<td>41.5792</td>
<td>NaN</td>
<td>C</td>
<td>NaN</td>
<td>NaN</td>
<td>Paris / Haiti</td>
</tr>
<tr>
<th>943</th>
<td>3.0</td>
<td>0.0</td>
<td>Laitinen, Miss. Kristina Sofia</td>
<td>female</td>
<td>37.0</td>
<td>0.0</td>
<td>0.0</td>
<td>4135</td>
<td>9.5875</td>
<td>NaN</td>
<td>S</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>543</th>
<td>2.0</td>
<td>0.0</td>
<td>Reeves, Mr. David</td>
<td>male</td>
<td>36.0</td>
<td>0.0</td>
<td>0.0</td>
<td>C.A. 17248</td>
<td>10.5000</td>
<td>NaN</td>
<td>S</td>
<td>NaN</td>
<td>NaN</td>
<td>Brighton, Sussex</td>
</tr>
<tr>
<th>189</th>
<td>1.0</td>
<td>0.0</td>
<td>Long, Mr. Milton Clyde</td>
<td>male</td>
<td>29.0</td>
<td>0.0</td>
<td>0.0</td>
<td>113501</td>
<td>30.0000</td>
<td>D6</td>
<td>S</td>
<td>NaN</td>
<td>126.0</td>
<td>Springfield, MA</td>
</tr>
<tr>
<th>44</th>
<td>1.0</td>
<td>1.0</td>
<td>Burns, Miss. Elizabeth Margaret</td>
<td>female</td>
<td>41.0</td>
<td>0.0</td>
<td>0.0</td>
<td>16966</td>
<td>134.5000</td>
<td>E40</td>
<td>C</td>
<td>3</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>610</th>
<td>3.0</td>
<td>0.0</td>
<td>Ahlin, Mrs. Johan (Johanna Persdotter Larsson)</td>
<td>female</td>
<td>40.0</td>
<td>1.0</td>
<td>0.0</td>
<td>7546</td>
<td>9.4750</td>
<td>NaN</td>
<td>S</td>
<td>NaN</td>
<td>NaN</td>
<td>Sweden Akeley, MN</td>
</tr>
<tr>
<th>526</th>
<td>2.0</td>
<td>1.0</td>
<td>Pallas y Castello, Mr. Emilio</td>
<td>male</td>
<td>29.0</td>
<td>0.0</td>
<td>0.0</td>
<td>SC/PARIS 2147</td>
<td>13.8583</td>
<td>NaN</td>
<td>C</td>
<td>9</td>
<td>NaN</td>
<td>Spain / Havana, Cuba</td>
</tr>
<tr>
<th>698</th>
<td>3.0</td>
<td>0.0</td>
<td>Cacic, Mr. Jego Grga</td>
<td>male</td>
<td>18.0</td>
<td>0.0</td>
<td>0.0</td>
<td>315091</td>
<td>8.6625</td>
<td>NaN</td>
<td>S</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>1161</th>
<td>3.0</td>
<td>0.0</td>
<td>Rush, Mr. Alfred George John</td>
<td>male</td>
<td>16.0</td>
<td>0.0</td>
<td>0.0</td>
<td>A/4. 20589</td>
<td>8.0500</td>
<td>NaN</td>
<td>S</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>1259</th>
<td>3.0</td>
<td>0.0</td>
<td>Turcin, Mr. Stjepan</td>
<td>male</td>
<td>36.0</td>
<td>0.0</td>
<td>0.0</td>
<td>349247</td>
<td>7.8958</td>
<td>NaN</td>
<td>S</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=a5388c53-f86d-4c64-94ab-02cfac8829f3">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pro%C5%9Bba-o-podanie-parametr%C3%B3w-bazy-(informacji-o-polach)">Prośba o podanie parametrów bazy (informacji o polach)<a class="anchor-link" href="#Pro%C5%9Bba-o-podanie-parametr%C3%B3w-bazy-(informacji-o-polach)">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=abbd077b-13f3-49b8-90f4-116744200745">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [3]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 1310 entries, 0 to 1309
Data columns (total 14 columns):
 #   Column     Non-Null Count  Dtype  
---  ------     --------------  -----  
 0   pclass     1309 non-null   float64
 1   survived   1309 non-null   float64
 2   name       1309 non-null   object 
 3   sex        1309 non-null   object 
 4   age        1046 non-null   float64
 5   sibsp      1309 non-null   float64
 6   parch      1309 non-null   float64
 7   ticket     1309 non-null   object 
 8   fare       1308 non-null   float64
 9   cabin      295 non-null    object 
 10  embarked   1307 non-null   object 
 11  boat       486 non-null    object 
 12  body       121 non-null    float64
 13  home.dest  745 non-null    object 
dtypes: float64(7), object(7)
memory usage: 143.4+ KB
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=d73aaff6-16f0-4fdd-aae1-c1e700fbdd34">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>W wielu rekordach brakuje danych, np. w informacji o przypisaniu do kabiny lub czy ciało zostało odnalezione.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=95d5e0b7-9d24-46a5-876f-b7839ebb6c89">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pro%C5%9Bba-o-wy%C5%9Bwietlenie-duplikat%C3%B3w">Prośba o wyświetlenie duplikatów<a class="anchor-link" href="#Pro%C5%9Bba-o-wy%C5%9Bwietlenie-duplikat%C3%B3w">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=ce1bad32-ee55-4923-a5d0-a5b04beeaa0c">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [4]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">duplicated</span><span class="p">()]</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[4]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>pclass</th>
<th>survived</th>
<th>name</th>
<th>sex</th>
<th>age</th>
<th>sibsp</th>
<th>parch</th>
<th>ticket</th>
<th>fare</th>
<th>cabin</th>
<th>embarked</th>
<th>boat</th>
<th>body</th>
<th>home.dest</th>
</tr>
</thead>
<tbody>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=1c249071-1f9c-4148-8aa7-73ae951851fd">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Duplikatów brak</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=957b19b4-545a-420b-be57-bd1ff6fe901f">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pro%C5%9Bba-o-wy%C5%9Bwietlenie-unikatowych-warto%C5%9Bci">Prośba o wyświetlenie unikatowych wartości<a class="anchor-link" href="#Pro%C5%9Bba-o-wy%C5%9Bwietlenie-unikatowych-warto%C5%9Bci">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=04c84655-3fad-4aa6-85ee-4cc3de75d25f">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [5]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">nunique</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[5]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>pclass          3
survived        2
name         1307
sex             2
age            98
sibsp           7
parch           8
ticket        929
fare          281
cabin         186
embarked        3
boat           27
body          121
home.dest     369
dtype: int64</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=e72b94e3-f016-4e53-8838-d569dc8bf6c0">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Tu można zauważyć, które pola są polami typu bool, można to porównać z informacją o bazie danych i potwierdzić. Np. kolumna 'survived' przyjmuje tylko</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=bbe6e5c8-fcc6-47f8-9ad4-c582231cd1ab">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>dwie wartości unikatowe - survived(1) lub not survived(0). Czyli mimo iż jest to pole typu Float, w rzeczywistości jest polem logicznym True or False.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=c31958b7-53fa-4122-a12b-ed1f1ca28113">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Mimo wszystko pozostawię to pole takim jakie ono jest i w toku dalszych przeliczeń sprawdzę czy do wykresów lepiej się nadaje jako pole logiczne czy Float.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=a396edc0-430e-4768-8a7b-9699ce1a71ac">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pro%C5%9Bba-o-wy%C5%9Bwietlenie-wykresu-s%C5%82upkowego-wed%C5%82ug-tego-kto-prze%C5%BCy%C5%82-z-podzia%C5%82em-na-p%C5%82e%C4%87">Prośba o wyświetlenie wykresu słupkowego według tego kto przeżył z podziałem na płeć<a class="anchor-link" href="#Pro%C5%9Bba-o-wy%C5%9Bwietlenie-wykresu-s%C5%82upkowego-wed%C5%82ug-tego-kto-prze%C5%BCy%C5%82-z-podzia%C5%82em-na-p%C5%82e%C4%87">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=2cba7e9d-d41b-4d9f-8b2a-517165925401">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [6]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df_clean</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">dropna</span><span class="p">(</span><span class="n">subset</span><span class="o">=</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">,</span> <span class="s1">'sex'</span><span class="p">])</span>
<span class="n">survived_sex_counts</span> <span class="o">=</span> <span class="n">df_clean</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'sex'</span><span class="p">,</span> <span class="s1">'survived'</span><span class="p">])</span><span class="o">.</span><span class="n">size</span><span class="p">()</span><span class="o">.</span><span class="n">unstack</span><span class="p">()</span>
<span class="n">survived_sex_counts</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">'bar'</span><span class="p">,</span> <span class="n">stacked</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Przeżywalność według płci'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'Płeć'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'Liczba'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="n">rotation</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Przeżyli'</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="p">[</span><span class="s1">'Nie'</span><span class="p">,</span> <span class="s1">'Tak'</span><span class="p">])</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[6]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>&lt;matplotlib.legend.Legend at 0x2000ef33e10&gt;</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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rrvu0o033qjY2Fg1bNhQH374ob788kvde++9kn69i/N9992nRx55RMXFxRo6dKhcLpe2bdum/fv3+4zKVCUuLk7PPvus9u/fr1mzZvnMX7BggRo3buxz2XlN38sGDRrokUce0ahRozRo0CDdcccd+vnnn5WamlrlIaOjXX311WrSpImSkpL08MMPKzAwUBkZGZVuOXD++edr6NChevLJJxUQEKArr7xSW7du1ZNPPimXy6UGDWp2ZkNAQID69Omje+65RxUVFZo2bZoKCwuP+fqFh4frySef1KhRoxQfH6877rhDbrdb3333nb744gvNmTOnRs8NnBB/py3gdHKyIztH/mqtajr6r/c33njDXHHFFSYyMtI4nU7TunVrc8MNN5iVK1f69FLddLSdO3caSWbMmDHV9v3UU08ZSeaOO+7wmd+nTx8jybz11luV1nn88cdNmzZtjNPpNO3btzfPP/98lX+dn+jIzhF///vfzQUXXGAaNmxoXC6Xufbaa83WrVut5fv27TMjR440f/jDH0xYWJgJDw83F1xwgZk5c6Y5fPiwz7YWLlxoLr74YhMcHGzCw8NN586dKz1fVfLz802DBg1MWFiYKS0tteb/4x//MJLM4MGDq1zveO/lb/cxNjbWNGzY0LRr18688MILZsSIEccd2THGmA0bNpgePXqYsLAwc9ZZZ5kHH3zQ/P3vf/cZXTHGmEOHDpl77rnHNG/e3AQHB5tLLrnErFu3zrhcLnP33Xcfc/+PvDfTpk0zDz30kGnZsqVp2LCh6dy5s/nggw98ao8e2TnivffeM7169TJhYWEmNDTUnHfeeT4jX4zs4FRwGGNMXQUrAP4ze/ZsjR8/Xlu2bKl0Izyc2dauXatLL71U//jHPzRs2LBq63bu3KmYmBg98cQTmjhxYh12CJwcDmMBNrdp0yZlZ2fr4Ycf1rXXXkvQOcNlZmZq3bp16tq1q0JCQvTFF1/o8ccfV2xsrAYPHuzv9oBTgrAD2NygQYOUm5uryy+/XM8995y/24GfRUZGasWKFZo1a5aKiorUtGlT9evXT+np6T73zgHshMNYAADA1ripIAAAsDXCDgAAsDXCDgAAsDVOUNavX4y4d+9eRURE8AV1AACcJowxKioqktfrPeZNMQk7+vX7dX7v9+QAAID6Yffu3cf8klnCjqSIiAhJv75Y1X1LNQAAqF8KCwsVHR1tfY5Xh7Cj/307dWRkJGEHAIDTzPFOQeEEZQAAYGuEHQAAYGuEHQAAYGucs/M7lJeXq6yszN9t1CtBQUEKCAjwdxsAAFSLsFMDxhjl5ubq559/9ncr9VKjRo3k8Xi4RxEAoF4i7NTAkaDTvHlzhYaG8qH+/xlj9MsvvygvL0+S1KJFCz93BABAZYSd4ygvL7eCTlRUlL/bqXdCQkIkSXl5eWrevDmHtAAA9Q4nKB/HkXN0QkND/dxJ/XXkteF8JgBAfUTYqSEOXVWP1wYAUJ8RdgAAgK0Rdmxi586dcjgc2rx58+9a7+OPP5bD4bCuNMvIyFCjRo1qvT8AAPyFsFPLRo4cKYfDIYfDoaCgILVt21YTJ07UwYMHT+nzRkdHKycnRx06dDip7QwZMkTffPNNLXUFAID/cTXWKXDVVVdpwYIFKisr0yeffKJRo0bp4MGDmjt3rk9dWVmZgoKCauU5AwIC5PF4Tno7ISEh1hVWAADYASM7p4DT6ZTH41F0dLSGDRumm2++WW+88YZSU1PVqVMnvfDCC2rbtq2cTqeys7OtkaDfTr1797a2t3btWvXs2VMhISGKjo7W+PHjrZGiI4ehjp5GjhypnTt3qkGDBvrss898+ps9e7Zat24tY0yl3jmMBQCwG8JOHQgJCbEuy/7uu+/0yiuv6LXXXtPmzZvVqlUr5eTkWNOmTZsUFRWlnj17SpK++uorJSQkaPDgwfryyy/18ssva82aNbrrrrskST169PBZ/8MPP1RwcLB69uypNm3aKD4+XgsWLPDpZ8GCBdbhNgAA7I7DWKfYhg0btGTJEsXFxUmSSktLtWjRIjVr1syqOXL46dChQ7ruuuvUvXt3paamSpKeeOIJDRs2TCkpKZKk2NhYPf300+rVq5fmzp2r4OBga/0ff/xRd9xxh5KSknT77bdLkkaNGqUxY8ZoxowZcjqd+uKLL7R582a9/vrrdfQKAPCbVJe/O0BdSi3wdwf1FiM7p8A777yj8PBwBQcHq3v37urZs6dmz54tSWrdurVP0PmtpKQkFRUVacmSJWrQ4Ne3JisrSxkZGQoPD7emhIQEVVRUKDs721q3rKxM119/vdq0aaNZs2ZZ86+77joFBgZq2bJlkqQXXnhBV1xxhdq0aXNqdh4AgHqGkZ1T4IorrtDcuXMVFBQkr9frcxJyWFhYles8+uijWr58uTZs2KCIiAhrfkVFhUaPHq3x48dXWqdVq1bWv//4xz/qP//5jzZs2KDAwP+9rQ0bNtTw4cO1YMECDR48WEuWLPEJQwAA2B1h5xQICwvTOeecU+P61157TQ8//LDef/99nX322T7LunTpoq1btx5zezNmzNA///lPrV+/Xo0bN660fNSoUerQoYOeffZZlZWVafDgwTXfGQAATnMcxvKzLVu26NZbb9XkyZN1/vnnKzc3V7m5ufrpp58kSZMnT9a6des0duxYbd68Wd9++63eeustjRs3TpK0cuVKTZo0SbNmzVKjRo2s9QsK/nfstn379rrkkks0efJkDR06lEvLAQBnFMKOn3322Wf65Zdf9Oijj6pFixbWdGT05YILLtDq1av17bff6vLLL1fnzp01depUtWjRQpK0Zs0alZeX67bbbvNZ/09/+pPP8yQlJam0tNQ6cRkAgDOFw1R1s5UzTGFhoVwulwoKChQZGemz7NChQ8rOzlZMTIyCg4P91OHJe+yxx7R06VJ99dVXtb5tu7xGgO1wNdaZ5Qy8GutYn9+/xciOzR04cEAbN27U7NmzqzzJGQAAuyPs2Nxdd92lyy67TL169eIQFgDgjMTVWDaXkZGhjIwMf7cBAIDfMLIDAABsjbADAABsjbADAABsza9h5/Dhw/rLX/6imJgYhYSEqG3btnr44YdVUVFh1RhjlJqaKq/Xq5CQEPXu3Vtbt2712U5JSYnGjRunpk2bKiwsTAMHDtSePXvqencAAEA95NewM23aND333HOaM2eOvv76a02fPl1PPPGE9aWZkjR9+nTNmDFDc+bM0caNG+XxeNSnTx8VFRVZNSkpKVq2bJmWLl2qNWvW6MCBA+rfv7/Ky8v9sVsAAKAe8evVWOvWrdO1116ra665RpLUpk0bvfTSS/rss88k/TqqM2vWLN1///3WHYVffPFFud1uLVmyRKNHj1ZBQYHmz5+vRYsWKT4+XpK0ePFiRUdHa+XKlUpISPDPzgEAgHrBryM7l112mVatWqVvvvlGkvTFF19ozZo1uvrqqyVJ2dnZys3NVd++fa11nE6nevXqpbVr10qSsrKyVFZW5lPj9XrVoUMHqwbVy8jIUKNGjfzdBgAAp4xfR3YmT56sgoIC/eEPf1BAQIDKy8v12GOPaejQoZKk3NxcSZLb7fZZz+1264cffrBqGjZsWOnbvt1ut7X+0UpKSlRSUmI9Liws/N29t7n33d+9zsnY+fg1v3udkSNH6sUXX1R6erruvfdea/4bb7yhQYMGyRijIUOGWOESAAA78uvIzssvv6zFixdryZIl+vzzz/Xiiy/qr3/9q1588UWfOofD4fPYGFNp3tGOVZOeni6Xy2VN0dHRJ7cj9VhwcLCmTZum/Pz8KpeHhISoefPmddwVAAB1x69h589//rPuvfde3XTTTerYsaOGDx+uu+++W+np6ZIkj8cjSZVGaPLy8qzRHo/Ho9LS0kof5r+tOdqUKVNUUFBgTbt3767tXas34uPj5fF4rNf0aFUdxnr77bfVtWtXBQcHq23btnrooYd0+PDhOugWAIDa59ew88svv6hBA98WAgICrEvPY2Ji5PF4lJmZaS0vLS3V6tWr1aNHD0lS165dFRQU5FOTk5OjLVu2WDVHczqdioyM9JnsKiAgQGlpaZo9e3aNLsf/4IMPdMstt2j8+PHatm2b/va3vykjI0OPPfZYHXQLAEDt82vYGTBggB577DG9++672rlzp5YtW6YZM2Zo0KBBkn49fJWSkqK0tDQtW7ZMW7Zs0ciRIxUaGqphw4ZJklwul5KSkjRhwgStWrVKmzZt0i233KKOHTtaV2ed6QYNGqROnTrpwQcfPG7tY489pnvvvVcjRoxQ27Zt1adPHz3yyCP629/+VgedAgBQ+/x6gvLs2bM1depUJScnKy8vT16vV6NHj9YDDzxg1UyaNEnFxcVKTk5Wfn6+unXrphUrVigiIsKqmTlzpgIDA5WYmKji4mLFxcUpIyNDAQEB/titemnatGm68sorNWHChGPWZWVlaePGjT4jOeXl5Tp06JB++eUXhYaGnupWAQCoVX4NOxEREZo1a5ZmzZpVbY3D4VBqaqpSU1OrrQkODtbs2bN9bkYIXz179lRCQoLuu+8+jRw5stq6iooKPfTQQ9Z9jX4rODj4FHYIAMCp4dewg7r1+OOPq1OnTmrXrl21NV26dNH27dt1zjnn1GFnAACcOoSdM0jHjh118803H3ME7IEHHlD//v0VHR2tG2+8UQ0aNNCXX36pr776So8++mgddgsAQO3gW8/PMI888oiMMdUuT0hI0DvvvKPMzExdfPHFuuSSSzRjxgy1bt26DrsEAKD2OMyxPvnOEIWFhXK5XCooKKh0GfqhQ4eUnZ2tmJgYzlmpBq8RUE+luvzdAepSaoG/O6hzx/r8/i1GdgAAgK0RdgAAgK0RdgAAgK0RdgAAgK0RdgAAgK0RdgAAgK0RdgAAgK0RdgAAgK0RdgAAgK0RdlBJ7969lZKS4u82AACoFXwR6Imq69uw/47bgDscjmMuHzFihDIyMk6yIQAATg+EHRvKycmx/v3yyy/rgQce0Pbt2615ISEh/mgLAAC/4DCWDXk8HmtyuVxyOBzW46CgII0ZM0YtW7ZUaGioOnbsqJdeeumY21u+fLlcLpcWLlxYR3sAAEDtIeycYQ4dOqSuXbvqnXfe0ZYtW3TnnXdq+PDh+vTTT6usX7p0qRITE7Vw4ULdeuutddwtAAAnj8NYZ5izzjpLEydOtB6PGzdOy5cv16uvvqpu3br51D777LO677779Oabb+qKK66o61YBAKgVhJ0zTHl5uR5//HG9/PLL+s9//qOSkhKVlJQoLCzMp+61117Tvn37tGbNGv3f//2fn7oFAODkcRjrDPPkk09q5syZmjRpkj788ENt3rxZCQkJKi0t9anr1KmTmjVrpgULFsgY46duAQA4eYzsnGE++eQTXXvttbrlllskSRUVFfr222/Vvn17n7qzzz5bTz75pHr37q2AgADNmTPHH+0CAHDSGNk5w5xzzjnKzMzU2rVr9fXXX2v06NHKzc2tsrZdu3b66KOP9Nprr3GTQQDAaYuwc4aZOnWqunTpooSEBPXu3Vsej0fXXXddtfXnnnuuPvzwQ7300kuaMGFC3TUKAEAtcRhOyFBhYaFcLpcKCgoUGRnps+zQoUPKzs5WTEyMgoOD/dRh/cZrBNRTdX2nd/jX77jTvl0c6/P7txjZAQAAtkbYAQAAtkbYAQAAtkbYAQAAtkbYqSHO464erw0AoD4j7BxHUFCQJOmXX37xcyf115HX5shrBQBAfeLXOyi3adNGP/zwQ6X5ycnJeuaZZ2SM0UMPPaR58+YpPz9f3bp10zPPPKPzzz/fqi0pKdHEiRP10ksvqbi4WHFxcXr22WfVsmXLWukxICBAjRo1Ul5eniQpNDRUDoejVrZ9ujPG6JdfflFeXp4aNWqkgIAAf7cEAEAlfg07GzduVHl5ufV4y5Yt6tOnj2688UZJ0vTp0zVjxgxlZGSoXbt2evTRR9WnTx9t375dERERkqSUlBS9/fbbWrp0qaKiojRhwgT1799fWVlZtfbh6/F4JMkKPPDVqFEj6zUCAKC+qVc3FUxJSdE777yjb7/9VpLk9XqVkpKiyZMnS/p1FMftdmvatGkaPXq0CgoK1KxZMy1atEhDhgyRJO3du1fR0dF67733lJCQUKPnrelNicrLy1VWVnaSe2kvQUFBjOgA9RU3FTyzcFPBauvqzReBlpaWavHixbrnnnvkcDi0Y8cO5ebmqm/fvlaN0+lUr169tHbtWo0ePVpZWVkqKyvzqfF6verQoYPWrl1bbdgpKSlRSUmJ9biwsLBGPQYEBPDBDgDAaabenKD8xhtv6Oeff9bIkSMlyfpySrfb7VPndrutZbm5uWrYsKEaN25cbU1V0tPT5XK5rCk6OroW9wQAANQn9SbszJ8/X/369ZPX6/WZf/TJwMaY454gfLyaKVOmqKCgwJp279594o0DAIB6rV6EnR9++EErV67UqFGjrHlHTng9eoQmLy/PGu3xeDwqLS1Vfn5+tTVVcTqdioyM9JkAAIA91Yuws2DBAjVv3lzXXHONNS8mJkYej0eZmZnWvNLSUq1evVo9evSQJHXt2lVBQUE+NTk5OdqyZYtVAwAAzmx+P0G5oqJCCxYs0IgRIxQY+L92HA6HUlJSlJaWptjYWMXGxiotLU2hoaEaNmyYJMnlcikpKUkTJkxQVFSUmjRpookTJ6pjx46Kj4/31y4BAIB6xO9hZ+XKldq1a5duv/32SssmTZqk4uJiJScnWzcVXLFihXWPHUmaOXOmAgMDlZiYaN1UMCMjg6umAACApHp2nx1/qel1+gBwWuE+O2cW7rNTbV29OGcHAADgVPH7YSwAwKnR5tASf7eAOrTT3w3UY4zsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAW/N72PnPf/6jW265RVFRUQoNDVWnTp2UlZVlLTfGKDU1VV6vVyEhIerdu7e2bt3qs42SkhKNGzdOTZs2VVhYmAYOHKg9e/bU9a4AAIB6yK9hJz8/X5deeqmCgoL0/vvva9u2bXryySfVqFEjq2b69OmaMWOG5syZo40bN8rj8ahPnz4qKiqyalJSUrRs2TItXbpUa9as0YEDB9S/f3+Vl5f7Ya8AAEB94jDGGH89+b333qt///vf+uSTT6pcboyR1+tVSkqKJk+eLOnXURy3261p06Zp9OjRKigoULNmzbRo0SINGTJEkrR3715FR0frvffeU0JCwnH7KCwslMvlUkFBgSIjI2tvBwHAj9rc+66/W0Ad2vn4Nf5uoc7V9PPbryM7b731li666CLdeOONat68uTp37qznn3/eWp6dna3c3Fz17dvXmud0OtWrVy+tXbtWkpSVlaWysjKfGq/Xqw4dOlg1RyspKVFhYaHPBAAA7MmvYWfHjh2aO3euYmNj9cEHH2jMmDEaP368Fi5cKEnKzc2VJLndbp/13G63tSw3N1cNGzZU48aNq605Wnp6ulwulzVFR0fX9q4BAIB6wq9hp6KiQl26dFFaWpo6d+6s0aNH64477tDcuXN96hwOh89jY0yleUc7Vs2UKVNUUFBgTbt37z65HQEAAPWWX8NOixYtdN555/nMa9++vXbt2iVJ8ng8klRphCYvL88a7fF4PCotLVV+fn61NUdzOp2KjIz0mQAAgD35Nexceuml2r59u8+8b775Rq1bt5YkxcTEyOPxKDMz01peWlqq1atXq0ePHpKkrl27KigoyKcmJydHW7ZssWoAAMCZK9CfT3733XerR48eSktLU2JiojZs2KB58+Zp3rx5kn49fJWSkqK0tDTFxsYqNjZWaWlpCg0N1bBhwyRJLpdLSUlJmjBhgqKiotSkSRNNnDhRHTt2VHx8vD93DwAA1AN+DTsXX3yxli1bpilTpujhhx9WTEyMZs2apZtvvtmqmTRpkoqLi5WcnKz8/Hx169ZNK1asUEREhFUzc+ZMBQYGKjExUcXFxYqLi1NGRoYCAgL8sVsAAKAe8et9duoL7rMDwI64z86Zhfvs1NP77AAAAJxqhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrfg07qampcjgcPpPH47GWG2OUmpoqr9erkJAQ9e7dW1u3bvXZRklJicaNG6emTZsqLCxMAwcO1J49e+p6VwAAQD3l95Gd888/Xzk5Odb01VdfWcumT5+uGTNmaM6cOdq4caM8Ho/69OmjoqIiqyYlJUXLli3T0qVLtWbNGh04cED9+/dXeXm5P3YHAADUM4F+byAw0Gc05whjjGbNmqX7779fgwcPliS9+OKLcrvdWrJkiUaPHq2CggLNnz9fixYtUnx8vCRp8eLFio6O1sqVK5WQkFCn+wIAAOofv4/sfPvtt/J6vYqJidFNN92kHTt2SJKys7OVm5urvn37WrVOp1O9evXS2rVrJUlZWVkqKyvzqfF6verQoYNVU5WSkhIVFhb6TAAAwJ78Gna6deumhQsX6oMPPtDzzz+v3Nxc9ejRQz/++KNyc3MlSW6322cdt9ttLcvNzVXDhg3VuHHjamuqkp6eLpfLZU3R0dG1vGcAAKC+8GvY6devn66//np17NhR8fHxevfddyX9erjqCIfD4bOOMabSvKMdr2bKlCkqKCiwpt27d5/EXgAAgPrM74exfissLEwdO3bUt99+a53Hc/QITV5enjXa4/F4VFpaqvz8/GprquJ0OhUZGekzAQAAe6pXYaekpERff/21WrRooZiYGHk8HmVmZlrLS0tLtXr1avXo0UOS1LVrVwUFBfnU5OTkaMuWLVYNAAA4s/n1aqyJEydqwIABatWqlfLy8vToo4+qsLBQI0aMkMPhUEpKitLS0hQbG6vY2FilpaUpNDRUw4YNkyS5XC4lJSVpwoQJioqKUpMmTTRx4kTrsBgAAIBfw86ePXs0dOhQ7d+/X82aNdMll1yi9evXq3Xr1pKkSZMmqbi4WMnJycrPz1e3bt20YsUKRUREWNuYOXOmAgMDlZiYqOLiYsXFxSkjI0MBAQH+2i0AAFCPOIwx5kRW/Oc//6lXXnlFu3btUmlpqc+yzz//vFaaqyuFhYVyuVwqKCjg/B0AttHm3nf93QLq0M7Hr/F3C3Wupp/fJ3TOztNPP63bbrtNzZs316ZNm/R///d/ioqK0o4dO9SvX78TbhoAAKC2nVDYefbZZzVv3jzNmTNHDRs21KRJk5SZmanx48eroKCgtnsEAAA4YScUdnbt2mVd7RQSEmJ9V9Xw4cP10ksv1V53AAAAJ+mEwo7H49GPP/4oSWrdurXWr18v6deveDjBU4AAAABOiRMKO1deeaXefvttSVJSUpLuvvtu9enTR0OGDNGgQYNqtUEAAICTcUKXns+bN08VFRWSpDFjxqhJkyZas2aNBgwYoDFjxtRqgwAAACfjhMJOgwYN1KDB/waFEhMTlZiYWGtNAQAA1JYTvqlgfn6+5s+fr6+//loOh0Pt27fXbbfdpiZNmtRmfzjVUl3+7gB1KZWrJQGceU7onJ3Vq1crJiZGTz/9tPLz8/XTTz/p6aefVkxMjFavXl3bPQIAAJywExrZGTt2rBITEzV37lzraxnKy8uVnJyssWPHasuWLbXaJAAAwIk6oZGd77//XhMmTPD5/qmAgADdc889+v7772utOQAAgJN1QmGnS5cu+vrrryvN//rrr9WpU6eT7QkAAKDW1Pgw1pdffmn9e/z48frTn/6k7777Tpdccokkaf369XrmmWf0+OOP136XAAAAJ6jGYadTp05yOBw+d0ieNGlSpbphw4ZpyJAhtdMdAADASapx2MnOzj6VfQAAAJwSNQ47rVu3PpV9AAAAnBIndIJyQECArrjiCv30008+8/ft2+dzhRYAAIC/nVDYMcaopKREF110UaV76vCt5wAAoD45obDjcDj02muvacCAAerRo4fefPNNn2UAAAD1xQmP7AQEBOipp57SX//6Vw0ZMkSPPvooozoAAKDeOeEvAj3izjvvVLt27XTDDTfwvVgAAKDeOaGRndatW/uciNy7d2+tX79ee/bsqbXGAAAAasMJjexUdc+dc845R5s2bdK+fftOuikAAIDackIjOxs3btSnn35aaf4XX3yh//73vyfdFAAAQG05obAzduxY7d69u9L8//znPxo7duxJNwUAAFBbTijsbNu2TV26dKk0v3Pnztq2bdtJNwUAAFBbTijsOJ3OKs/NycnJUWDgSV/gBQAAUGtOKOz06dNHU6ZMUUFBgTXv559/1n333ac+ffrUWnMAAAAn64SGYZ588kn17NlTrVu3VufOnSVJmzdvltvt1qJFi2q1QQAAgJNxQmHnrLPO0pdffql//OMf+uKLLxQSEqLbbrtNQ4cOVVBQUG33CAAAcMJO6DCWJIWFhenOO+/UM888o7/+9a+69dZbTyropKeny+FwKCUlxZpnjFFqaqq8Xq9CQkLUu3dvbd261We9kpISjRs3Tk2bNlVYWJgGDhzIzQ0BAIClxiM7b731lvr166egoCC99dZbx6wdOHDg72pi48aNmjdvni644AKf+dOnT9eMGTOUkZGhdu3a6dFHH1WfPn20fft2RURESJJSUlL09ttva+nSpYqKitKECRPUv39/ZWVl+dzlGQAAnJlqHHauu+465ebmqnnz5rruuuuqrXM4HCovL69xAwcOHNDNN9+s559/Xo8++qg13xijWbNm6f7779fgwYMlSS+++KLcbreWLFmi0aNHq6CgQPPnz9eiRYsUHx8vSVq8eLGio6O1cuVKJSQk1LgPAABgTzU+jFVRUaHmzZtb/65q2rlzp2699dbf1cDYsWN1zTXXWGHliOzsbOXm5qpv377WPKfTqV69emnt2rWSpKysLJWVlfnUeL1edejQwaoBAABnthM+Z6cq+fn5WrhwYY3rly5dqs8//1zp6emVluXm5kqS3G63z3y3220ty83NVcOGDdW4ceNqa6pSUlKiwsJCnwkAANhTrYad32P37t3605/+pMWLFys4OLjaOofD4fPYGFNp3tGOV5Oeni6Xy2VN0dHRv695AABw2vBb2MnKylJeXp66du2qwMBABQYGavXq1Xr66acVGBhojegcPUKTl5dnLfN4PCotLVV+fn61NVU5ckPEI1NV3/MFAADswW9hJy4uTl999ZU2b95sTRdddJFuvvlmbd68WW3btpXH41FmZqa1TmlpqVavXq0ePXpIkrp27aqgoCCfmpycHG3ZssWqqYrT6VRkZKTPBAAA7Ol33VTwyFVR1fn5559rvK2IiAh16NDBZ15YWJiioqKs+SkpKUpLS1NsbKxiY2OVlpam0NBQDRs2TJLkcrmUlJSkCRMmKCoqSk2aNNHEiRPVsWPHSic8AwCAM9PvCjsul+u4y3/v1VjHMmnSJBUXFys5OVn5+fnq1q2bVqxYYd1jR5JmzpypwMBAJSYmqri4WHFxccrIyOAeOwAAQJLkMMYYfzfhb4WFhXK5XCooKDjzDmmlHjvAwmZSC45fA9toc++7/m4BdWjn49f4u4U6V9PPb7+dswMAAFAXCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDW/Bp25s6dqwsuuECRkZGKjIxU9+7d9f7771vLjTFKTU2V1+tVSEiIevfura1bt/pso6SkROPGjVPTpk0VFhamgQMHas+ePXW9KwAAoJ7ya9hp2bKlHn/8cX322Wf67LPPdOWVV+raa6+1As306dM1Y8YMzZkzRxs3bpTH41GfPn1UVFRkbSMlJUXLli3T0qVLtWbNGh04cED9+/dXeXm5v3YLAADUIw5jjPF3E7/VpEkTPfHEE7r99tvl9XqVkpKiyZMnS/p1FMftdmvatGkaPXq0CgoK1KxZMy1atEhDhgyRJO3du1fR0dF67733lJCQUKPnLCwslMvlUkFBgSIjI0/ZvtVLqS5/d4C6lFrg7w5Qh9rc+66/W0Ad2vn4Nf5uoc7V9PO73pyzU15erqVLl+rgwYPq3r27srOzlZubq759+1o1TqdTvXr10tq1ayVJWVlZKisr86nxer3q0KGDVVOVkpISFRYW+kwAAMCe/B52vvrqK4WHh8vpdGrMmDFatmyZzjvvPOXm5kqS3G63T73b7baW5ebmqmHDhmrcuHG1NVVJT0+Xy+Wypujo6FreKwAAUF/4Peyce+652rx5s9avX68//vGPGjFihLZt22YtdzgcPvXGmErzjna8milTpqigoMCadu/efXI7AQAA6i2/h52GDRvqnHPO0UUXXaT09HRdeOGFeuqpp+TxeCSp0ghNXl6eNdrj8XhUWlqq/Pz8amuq4nQ6rSvAjkwAAMCe/B52jmaMUUlJiWJiYuTxeJSZmWktKy0t1erVq9WjRw9JUteuXRUUFORTk5OToy1btlg1AADgzBbozye/77771K9fP0VHR6uoqEhLly7Vxx9/rOXLl8vhcCglJUVpaWmKjY1VbGys0tLSFBoaqmHDhkmSXC6XkpKSNGHCBEVFRalJkyaaOHGiOnbsqPj4eH/uGgAAqCf8Gnb27dun4cOHKycnRy6XSxdccIGWL1+uPn36SJImTZqk4uJiJScnKz8/X926ddOKFSsUERFhbWPmzJkKDAxUYmKiiouLFRcXp4yMDAUEBPhrtwAAQD1S7+6z4w/cZwdnDO6zc0bhPjtnFu6zcxrcZwcAAOBUIOwAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABb82vYSU9P18UXX6yIiAg1b95c1113nbZv3+5TY4xRamqqvF6vQkJC1Lt3b23dutWnpqSkROPGjVPTpk0VFhamgQMHas+ePXW5KwAAoJ7ya9hZvXq1xo4dq/Xr1yszM1OHDx9W3759dfDgQatm+vTpmjFjhubMmaONGzfK4/GoT58+KioqsmpSUlK0bNkyLV26VGvWrNGBAwfUv39/lZeX+2O3AABAPeIwxhh/N3HEf//7XzVv3lyrV69Wz549ZYyR1+tVSkqKJk+eLOnXURy3261p06Zp9OjRKigoULNmzbRo0SINGTJEkrR3715FR0frvffeU0JCwnGft7CwUC6XSwUFBYqMjDyl+1jvpLr83QHqUmqBvztAHWpz77v+bgF1aOfj1/i7hTpX08/venXOTkHBr7+ImzRpIknKzs5Wbm6u+vbta9U4nU716tVLa9eulSRlZWWprKzMp8br9apDhw5WzdFKSkpUWFjoMwEAAHuqN2HHGKN77rlHl112mTp06CBJys3NlSS53W6fWrfbbS3Lzc1Vw4YN1bhx42prjpaeni6Xy2VN0dHRtb07AACgnqg3Yeeuu+7Sl19+qZdeeqnSMofD4fPYGFNp3tGOVTNlyhQVFBRY0+7du0+8cQAAUK/Vi7Azbtw4vfXWW/roo4/UsmVLa77H45GkSiM0eXl51miPx+NRaWmp8vPzq605mtPpVGRkpM8EAADsya9hxxiju+66S6+//ro+/PBDxcTE+CyPiYmRx+NRZmamNa+0tFSrV69Wjx49JEldu3ZVUFCQT01OTo62bNli1QAAgDNXoD+ffOzYsVqyZInefPNNRUREWCM4LpdLISEhcjgcSklJUVpammJjYxUbG6u0tDSFhoZq2LBhVm1SUpImTJigqKgoNWnSRBMnTlTHjh0VHx/vz90DAAD1gF/Dzty5cyVJvXv39pm/YMECjRw5UpI0adIkFRcXKzk5Wfn5+erWrZtWrFihiIgIq37mzJkKDAxUYmKiiouLFRcXp4yMDAUEBNTVrgAAgHqqXt1nx1+4zw7OGNxn54zCfXbOLNxn5zS5zw4AAEBtI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbC/R3A/CvNoeW+LsF1KGd/m4AAPyAkR0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrfg07//rXvzRgwAB5vV45HA698cYbPsuNMUpNTZXX61VISIh69+6trVu3+tSUlJRo3Lhxatq0qcLCwjRw4EDt2bOnDvcCAADUZ34NOwcPHtSFF16oOXPmVLl8+vTpmjFjhubMmaONGzfK4/GoT58+KioqsmpSUlK0bNkyLV26VGvWrNGBAwfUv39/lZeX19VuAACAesyvNxXs16+f+vXrV+UyY4xmzZql+++/X4MHD5Ykvfjii3K73VqyZIlGjx6tgoICzZ8/X4sWLVJ8fLwkafHixYqOjtbKlSuVkJBQZ/sCAADqp3p7zk52drZyc3PVt29fa57T6VSvXr20du1aSVJWVpbKysp8arxerzp06GDVVKWkpESFhYU+EwAAsKd6G3Zyc3MlSW6322e+2+22luXm5qphw4Zq3LhxtTVVSU9Pl8vlsqbo6Oha7h4AANQX9TbsHOFwOHweG2MqzTva8WqmTJmigoICa9q9e3et9AoAAOqfeht2PB6PJFUaocnLy7NGezwej0pLS5Wfn19tTVWcTqciIyN9JgAAYE/1NuzExMTI4/EoMzPTmldaWqrVq1erR48ekqSuXbsqKCjIpyYnJ0dbtmyxagAAwJnNr1djHThwQN999531ODs7W5s3b1aTJk3UqlUrpaSkKC0tTbGxsYqNjVVaWppCQ0M1bNgwSZLL5VJSUpImTJigqKgoNWnSRBMnTlTHjh2tq7MAAMCZza9h57PPPtMVV1xhPb7nnnskSSNGjFBGRoYmTZqk4uJiJScnKz8/X926ddOKFSsUERFhrTNz5kwFBgYqMTFRxcXFiouLU0ZGhgICAup8fwAAQP3jMMYYfzfhb4WFhXK5XCooKDjjzt9pc++7/m4BdWjn49f4uwXUIX6+zyxn4s93TT+/6+05OwAAALWBsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGyNsAMAAGzNNmHn2WefVUxMjIKDg9W1a1d98skn/m4JAADUA7YIOy+//LJSUlJ0//33a9OmTbr88svVr18/7dq1y9+tAQAAP7NF2JkxY4aSkpI0atQotW/fXrNmzVJ0dLTmzp3r79YAAICfnfZhp7S0VFlZWerbt6/P/L59+2rt2rV+6goAANQXgf5u4GTt379f5eXlcrvdPvPdbrdyc3OrXKekpEQlJSXW44KCAklSYWHhqWu0nqoo+cXfLaAOnYn/x89k/HyfWc7En+8j+2yMOWbdaR92jnA4HD6PjTGV5h2Rnp6uhx56qNL86OjoU9IbUF+4Zvm7AwCnypn8811UVCSXy1Xt8tM+7DRt2lQBAQGVRnHy8vIqjfYcMWXKFN1zzz3W44qKCv3000+KioqqNiDBPgoLCxUdHa3du3crMjLS3+0AqEX8fJ9ZjDEqKiqS1+s9Zt1pH3YaNmyorl27KjMzU4MGDbLmZ2Zm6tprr61yHafTKafT6TOvUaNGp7JN1EORkZH8MgRsip/vM8exRnSOOO3DjiTdc889Gj58uC666CJ1795d8+bN065duzRmzBh/twYAAPzMFmFnyJAh+vHHH/Xwww8rJydHHTp00HvvvafWrVv7uzUAAOBntgg7kpScnKzk5GR/t4HTgNPp1IMPPljpUCaA0x8/36iKwxzvei0AAIDT2Gl/U0EAAIBjIewAAABbI+wAAABbI+yg3jLG6M4771STJk3kcDi0efNmv/Sxc+dOvz4/gJM3cuRIXXfddf5uA35im6uxYD/Lly9XRkaGPv74Y7Vt21ZNmzb1d0sAgNMQYQf11vfff68WLVqoR48e/m4FAHAa4zAW6qWRI0dq3Lhx2rVrlxwOh9q0aSNjjKZPn662bdsqJCREF154of75z39a63z88cdyOBz64IMP1LlzZ4WEhOjKK69UXl6e3n//fbVv316RkZEaOnSofvnlf98GvXz5cl122WVq1KiRoqKi1L9/f33//ffH7G/btm26+uqrFR4eLrfbreHDh2v//v2n7PUAziS9e/fWuHHjlJKSosaNG8vtdmvevHk6ePCgbrvtNkVEROjss8/W+++/L0kqLy9XUlKSYmJiFBISonPPPVdPPfXUMZ/jeL9PYC+EHdRLTz31lB5++GG1bNlSOTk52rhxo/7yl79owYIFmjt3rrZu3aq7775bt9xyi1avXu2zbmpqqubMmaO1a9dq9+7dSkxM1KxZs7RkyRK9++67yszM1OzZs636gwcP6p577tHGjRu1atUqNWjQQIMGDVJFRUWVveXk5KhXr17q1KmTPvvsMy1fvlz79u1TYmLiKX1NgDPJiy++qKZNm2rDhg0aN26c/vjHP+rGG29Ujx499PnnnyshIUHDhw/XL7/8ooqKCrVs2VKvvPKKtm3bpgceeED33XefXnnllWq3X9PfJ7AJA9RTM2fONK1btzbGGHPgwAETHBxs1q5d61OTlJRkhg4daowx5qOPPjKSzMqVK63l6enpRpL5/vvvrXmjR482CQkJ1T5vXl6ekWS++uorY4wx2dnZRpLZtGmTMcaYqVOnmr59+/qss3v3biPJbN++/YT3F8CvevXqZS677DLr8eHDh01YWJgZPny4NS8nJ8dIMuvWratyG8nJyeb666+3Ho8YMcJce+21xpia/T6BvXDODk4L27Zt06FDh9SnTx+f+aWlpercubPPvAsuuMD6t9vtVmhoqNq2beszb8OGDdbj77//XlOnTtX69eu1f/9+a0Rn165d6tChQ6VesrKy9NFHHyk8PLzSsu+//17t2rU7sZ0EYPntz3FAQICioqLUsWNHa57b7ZYk5eXlSZKee+45/f3vf9cPP/yg4uJilZaWqlOnTlVu+/f8PoE9EHZwWjgSQN59912dddZZPsuO/g6coKAg698Oh8Pn8ZF5vz1ENWDAAEVHR+v555+X1+tVRUWFOnTooNLS0mp7GTBggKZNm1ZpWYsWLX7fjgGoUlU/t0f/bEu//jy+8soruvvuu/Xkk0+qe/fuioiI0BNPPKFPP/20ym3/nt8nsAfCDk4L5513npxOp3bt2qVevXrV2nZ//PFHff311/rb3/6myy+/XJK0Zs2aY67TpUsXvfbaa2rTpo0CA/kRAvztk08+UY8ePXy+DPpYFxmcqt8nqL/4TY3TQkREhCZOnKi7775bFRUVuuyyy1RYWKi1a9cqPDxcI0aMOKHtNm7cWFFRUZo3b55atGihXbt26d577z3mOmPHjtXzzz+voUOH6s9//rOaNm2q7777TkuXLtXzzz+vgICAE+oFwIk555xztHDhQn3wwQeKiYnRokWLtHHjRsXExFRZf6p+n6D+IuzgtPHII4+oefPmSk9P144dO9SoUSN16dJF99133wlvs0GDBlq6dKnGjx+vDh066Nxzz9XTTz+t3r17V7uO1+vVv//9b02ePFkJCQkqKSlR69atddVVV6lBAy5wBOramDFjtHnzZg0ZMkQOh0NDhw5VcnKydWl6VU7F7xPUXw5jjPF3EwAAAKcKf4YCAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAwG/Mnj1b69at83cbAGoRYQeAbezcuVMOh0ObN28+ofWfeuopvfrqq+rSpUvtNgbArwg7AE4rI0eOlMPhsL4Ysm3btpo4caIOHjx4Uttdv369XnjhBb355pt8GSRgM3xdBIDTzlVXXaUFCxaorKxMn3zyiUaNGqWDBw9q8uTJJ7zNSy65RF988UUtdgmgvmBkB8Bpx+l0yuPxKDo6WsOGDdPNN9+sN954w1q+f/9+/fzzz5Kkbdu26eqrr1Z4eLjcbreGDx+u/fv3W7UVFRWaNm2azjnnHDmdTrVq1UqPPfZYHe8RgFOJsAPgtBcSEqKysjLr8U033aQNGzYoJydHvXr1UqdOnfTZZ59p+fLl2rdvnxITE63aKVOmaNq0aZo6daq2bdumJUuWyO12+2M3AJwifBEogNPKyJEj9fPPP1sjORs2bNDVV1+tXr16qVWrVpo1a5aWL1+uhIQEPfDAA/r000/1wQcfWOvv2bNH0dHR2r59u1q0aKFmzZppzpw5GjVqlJ/2CMCpxjk7AE4777zzjsLDw3X48GGVlZXp2muv1aRJk/Tkk09KkjUyk5WVpY8++kjh4eGVtvH999/r559/VklJieLi4uq0fwB1i7AD4LRzxRVXaO7cuQoKCpLX61VQUJAkafr06Xr11VetuoqKCg0YMEDTpk2rtI0WLVpox44dddYzAP8h7AA47YSFhemcc845bl2XLl302muvqU2bNgoMrPzrLjY2ViEhIVq1ahWHsQAb4wRlALY1duxY/fTTTxo6dKg2bNigHTt2aMWKFbr99ttVXl6u4OBgTZ48WZMmTdLChQv1/fffa/369Zo/f76/WwdQixjZAWBbXq9X//73vzV58mQlJCSopKRErVu31lVXXaUGDX79W2/q1KkKDAzUAw88oL1796pFixYaM2aMnzsHUJu4GgsAANgah7EAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICt/T9Ox/BDcRmppgAAAABJRU5ErkJggg=="/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=5a324073-1fb0-4a1f-bd12-604385438e6f">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Na wykresie wyraźnie widać, że stosunkowo więcej kobiet niż mężczyzn uratowało się</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=af8a0dbd-1e8d-431e-ad15-15ad3dc658dd">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Czyli można wyciągnąć wniosek, że brano pod uwagę to czy osoba ratowana była kobietą a także, że w takim wypadku
należał jej się priorytet miejsca w szalupie.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=bdb00128-0c88-4cff-acb1-ead2c75d8ecd">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pro%C5%9Bba-o-pokazanie-liczby-pasa%C5%BCer%C3%B3w-wg.-podzia%C5%82u-na-p%C5%82e%C4%87">Prośba o pokazanie liczby pasażerów wg. podziału na płeć<a class="anchor-link" href="#Pro%C5%9Bba-o-pokazanie-liczby-pasa%C5%BCer%C3%B3w-wg.-podzia%C5%82u-na-p%C5%82e%C4%87">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=006d30c7-4051-48d7-9a8a-cd7a1cc82abf">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [7]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">pwp</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">'sex'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
<span class="n">result</span> <span class="o">=</span> <span class="p">{</span>
    <span class="s2">"type"</span><span class="p">:</span> <span class="s2">"dataframe"</span><span class="p">,</span>
    <span class="s2">"value"</span><span class="p">:</span> <span class="n">pwp</span><span class="o">.</span><span class="n">to_frame</span><span class="p">(</span><span class="n">name</span><span class="o">=</span><span class="s1">'count'</span><span class="p">)</span>
<span class="p">}</span>
<span class="n">pwp</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[7]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>sex
male      843
female    466
Name: count, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=dbe195fc-4249-47e8-9bb2-7c8ec6bff8b5">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Tutaj wyraźnie widać, że mężczyzn na pokładzie było więcej niemal dwukrotnie od kobiet,
co wzmacnia poziom relacji z wykresu powyżej, ponieważ mężczyzn zginęło więcej.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=1d0fc7b8-35e7-4616-aad5-a8badb777c0e">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Wniosek:">Wniosek:<a class="anchor-link" href="#Wniosek:">¶</a></h3>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=b96df932-b534-43cc-95ff-e3c28a56d5c6">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>mężczyzna miał o wiele mniejsze szanse przetrwania niż kobieta</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=b8c6599d-8f9a-478c-9e39-8de701bfd269">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pro%C5%9Bba-o-pokazanie-wykresu-punktowego-uczestnik%C3%B3w-rejsu-wed%C5%82ug-podzia%C5%82u-na-wiek">Prośba o pokazanie wykresu punktowego uczestników rejsu według podziału na wiek<a class="anchor-link" href="#Pro%C5%9Bba-o-pokazanie-wykresu-punktowego-uczestnik%C3%B3w-rejsu-wed%C5%82ug-podzia%C5%82u-na-wiek">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=24773c26-520d-4e5e-b89a-c22f9b048446">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [8]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">],</span> <span class="n">df</span><span class="o">.</span><span class="n">index</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Uczestnicy rejsu w podziale na wiek'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'Wiek'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'Index'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">grid</span><span class="p">(</span><span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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/uqv/grPP/88QqEQgsEgXnrpJbzzne+E2WxObudwOGbMgVQOHDiAG264AZdffjn++7//O2/VwnvvvRcXXHABzGYzRFGEJEnYtWsXDhw4kPNzv/vd77B+/Xq0t7enfa/XXXcdgPj9ko/zzz8f3d3dyb/NZjOWLVs2Yz7P9hytVisuu+yytO+3rq4On/zkJxGLxfCXv/wFQDzalev7jUQi2LVrF97xjnfAarXOmMeRSATPP/982mcef/xxXHXVVXjzm9+MHTt2oKGhIe94EARR25DYIghiXiOK8Wzp1PUZqaiqmiYERkdHDVdm27dvH97+9rfjqquuwo9+9KO090ZGRvD6669DkqS0fw6HA4yxZCn6N7/5zXj44Yehqir+7u/+Dp2dnVi1ahUeeughw9dotVrTDG8gvpg/Eonk/JzRa/2nf/onHDlyBDt27AAQT5m87LLLcMEFFxg6vwULFqT9nUh3+8QnPjFjfD784Q8DQNZS/RzHYdeuXdiyZQvuueceXHDBBWhubsZtt90Gv99v6HzyYTabccUVVySN8V27dmHTpk24+uqroWka/vznPyfHwqjYamtry/ja+Pg4ACT/f/pYAUB7ezt0XYfH44HH44Gu61n3l4nBwUFce+216OzsxK9//WvIspzzXL/5zW/iQx/6ENauXYtf/epXeP755/HSSy/h2muvRTgczvnZkZERPPLIIzO+10TaYrbvNZXGxsYZr5lMprRjF3OOQPx7e/755xEMBrFz505cc801aGxsxIUXXoidO3fixIkTOHHiRM7vd3x8HKqq4rvf/e6M673++uszXu/DDz+McDiMD33oQ4aLxBAEUdvQmi2CIOY1ra2tAOLrkxL/nYAxhqGhIVx00UXJ15qbm3H69Om8+z19+jSuvfZadHd341e/+lWaYAOApqYmWCyWGQv7U99P8La3vQ1ve9vbEI1G8fzzz+OrX/0qtm3bhp6enuSaknJg9FqvueYarFq1Ct/73vdgt9uxe/duPPDAA4aPMz2Kkrj2O++8E+985zszfmb58uVZ97dw4cKkuD18+DB+8Ytf4K677kIsFsO9994LIG6cTy8QApwRNfnYsGEDPv/5z+PFF1/E6dOnsWnTJjgcDlx88cXYsWMHBgcHsWzZMnR1dRna3/DwcMbXEsIi8f9DQ0MzthscHATP86ivrwdjDBzHZd3fdHw+H66//nrouo4//OEPaevusvHAAw/g6quvxr//+7+nvW5EzDY1NWHNmjVpUd5U2tvb8+7DCMWcIxD/fj/3uc/h6aefxq5du5JrqzZs2IAnnngCixYtSv6djfr6egiCgJtuugkf+chHMm6T2E+Cb33rW/j5z3+O6667Dr/5zW+wefNmQ+dLEETtQpEtgiDmNddccw04jsPPf/7zGe899thj8Pl8ad7r6667DocPH04WqMiE1+vFddddB47j8Ic//AFOp3PGNlu3bsWxY8fQ2NiIiy66aMa/np6eGZ8xmUxYt24dvva1rwFAslpdwgNuxGNfCNdddx2eeuqprCl7qdx22234/e9/jzvvvBOtra1497vfPevjLl++HEuXLsWePXsyjs1FF10Eh8NhaF/Lli3DZz/7WaxevRq7d+9Ovt7T04PXX389bdsnn3wSgUDA0H43btwIVVXxuc99Dp2dnVixYkXy9Z07d+LJJ580HNUCgIceeiiZhgkAJ0+exLPPPpss5LB8+XJ0dHTgwQcfTNsuGAziV7/6VbJCoc1mwyWXXIJf//rXaZFLv9+PRx55JO2YsVgM73jHO9DX14dHH33UcMSW47gZUZfXX389Y1XE6WzduhV79+7F4sWLM36vpRJbxZwjAFxyySVwOp349re/jeHhYWzatAlA/Pt99dVX8Ytf/ALnnHNOzvO1Wq1Yv349Xn31VaxZsybj9U6P0pnNZvz617/G1q1bccMNN+B///d/C7xygiBqDYpsEQQxr1m8eDE++tGP4utf/zomJydx/fXXw2Kx4KWXXsK//du/4aKLLsK2bduS299+++34+c9/jre97W349Kc/jUsuuQThcBh/+tOfsHXrVqxfvx7btm3D/v378R//8R/o7+9Hf39/8vOdnZ3o7OzE7bffjl/96ld485vfjI997GNYs2YNdF3HqVOn8MQTT+COO+7A2rVr8fnPfx6nT5/Ghg0b0NnZicnJSXznO9+BJElYt25d8hosFgt++tOfYuXKlbDb7Whvby/acP3iF7+IRx99FG9+85vxmc98BqtXr8bk5CQee+wxfPzjH08KDAD427/9W9x55514+umn8dnPfjZvKlo+fvjDH+K6667Dli1bcMstt6CjowMTExM4cOAAdu/ejV/+8pcZP/f666/jox/9KN797ndj6dKlkGUZTz75JF5//XV8+tOfTm5300034XOf+xw+//nPY926ddi/fz++973vGYrsAMCFF16I+vp6PPHEE9i+fXvy9Y0bN+JLX/pS8r+N4na78Y53vAMf+MAH4PV68YUvfAFmsxl33nknAIDnedxzzz1473vfi61bt+LWW29FNBpNztt/+7d/S+7rS1/6Eq699lps2rQJd9xxBzRNw9e+9jXYbLZklT4A+NjHPoYnn3wSX/nKVxAIBNLWDzU3N2dtzrt161Z86Utfwhe+8AWsW7cOhw4dwhe/+EUsWrQob/n2L37xi9ixYwcuv/xy3HbbbVi+fDkikQj6+vrwhz/8Affee29JGigXc44AIAgC1q1bh0ceeQSLFi1KjsUVV1wBk8mEXbt24bbbbsu7n+985zu48sorcdVVV+FDH/oQenp64Pf7cfToUTzyyCMZnTaSJOGhhx7C3//93+Nd73oX/t//+3/4m7/5m8IHgSCI2mAuq3MQBEFUAl3X2b//+7+ziy66iFmtVibLMlu6dCn71Kc+xfx+/4ztPR4P+6d/+ifW3d3NJEliLS0t7C1veQs7ePAgYyxeMQ1Axn+pldkCgQD77Gc/y5YvX85kWWYul4utXr2afexjH2PDw8OMMcZ+97vfseuuu451dHQwWZZZS0sLu/7669mf//zntHN66KGH2IoVK5gkSWnHufnmm5nNZptxDYkqjKlMPz/GGOvv72fve9/7WFtbG5MkibW3t7Mbb7yRjYyMzNjnLbfcwkRRZKdPn8475oydqd729a9/PeP7e/bsYTfeeCNraWlhkiSxtrY2ds0117B77703uU2iitsf//hHxhhjIyMj7JZbbmErVqxgNpuN2e12tmbNGvatb32Lqaqa/Fw0GmX//M//zLq6upjFYmHr1q1jr732mqFqhAne8Y53MADspz/9afK1WCzGbDYb43meeTyevPtInP9PfvITdtttt7Hm5mZmMpnYVVddxV5++eUZ2z/88MNs7dq1zGw2M5vNxjZs2MCeeeaZGdv99re/ZWvWrGGyLLPu7m72b//2bzO+83Xr1mWdp6ljMH1eRKNR9olPfIJ1dHQws9nMLrjgAvbwww+zm2++mS1cuDDtPDLNqdHRUXbbbbexRYsWMUmSWENDA7vwwgvZv/zLv7BAIJBzvBYuXMje8pa3zHh93bp1aVVDCznHbHznO99hANgHPvCBtNc3bdrEALDf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AyS2CIIgCKICTz/9NDiOw+zsrOm/GRwcxP3331+3YyIIgiAaHxJbBEEQxIriH//xH+Hz+aBpWvaxaDQKSZJwww035L322WefBcdx6O3txdjYGFpaWuw+XIIgCKKJIbFFEARBrCj27NmDaDSKl19+OfvYs88+i56eHvzhD39APB7PPv7000+jt7cXGzduRE9PDziOW4pDJgiCIJoUElsEQRDEimLTpk3o7e3F008/nX3s6aefxjvf+U6sX78e+/fvz3t8z549RdMI9+/fj7e85S1wuVzo7+/Hpz71KcRisZKf++CDD6KlpQX79u2rx9ciCIIgGhASWwRBEMSK48Ybb8RTTz2V/fdTTz2FG2+8Ebt3784+nkql8MILL2DPnj0Ff//666/j1ltvxbvf/W689tpr+MlPfoLnnnsOn/jEJ4p+3n/7b/8Nn/vc5/D444/j5ptvrs+XIgiCIBoOElsEQRDEiuPGG2/E888/D03TEIlE8Oqrr+Itb3kLdu/enY14vfjii0gkEkXF1t/+7d/ijjvuwN13340NGzZg586d+Pu//3v8y7/8C5LJZN5rv/jFL+Lb3/42nn76aVx33XV2fD2CIAiiQRCX+gAIgiAIwm727NmDWCyGP/zhDwiFQti4cSO6urqwe/duvP/970csFsPTTz+NgYEBrFu3DsPDw3l/f+DAAZw+fRr/9m//ln2MMQbDMHDu3Dls2bIFAPDf//t/RywWw8svv4x169bZ+h0JgiCIpYciWwRBEMSKY2hoCKtXr8ZTTz2Fp556Crt37wYA9PT0YO3atXj++efx1FNP4a1vfWvRvzcMAx/5yEdw8ODB7H+HDh3CqVOnsH79+uzrbrjhBui6jv/1v/6XLd+LIAiCaCwoskUQBEGsSDKNL0KhEP7yL/8y+/ju3bvx+OOP48UXX8QHP/jBon971VVX4ciRIxgaGir7Gddeey0++clP4tZbb4UgCHmfQxAEQSx/KLJFEARBrEj27NmD5557DgcPHsxGtoC02Pr+97+PZDJZtF4LAD7/+c/jhRdewF133YWDBw/i1KlTeOSRR/DJT36y4LXXX389Hn30UXzta1/D3/3d39Xt+xAEQRCNB0W2CIIgiBXJnj17kEgksHnzZnR3d2cf3717NyKRCNavX4/+/v6if7t9+3Y888wzuOeee3DDDTeAMYb169fjPe95T9HX79q1C7/61a/wx3/8xxAEAZ/61Kfq8p0IgiCIxoJjjLGlPgiCIAiCIAiCIIjlBqUREgRBEARBEARB1AESWwRBEARBEARBEHWAxBZBEARBEARBEEQdILFFEARBEARBEARRB0hsEQRBEARBEARB1AESWwRBEARBEARBEHWAxBZBEARBEARBEEQdILFFEARBEARBEARRB0hsEQRBEARBEARB1AESWwRBEARBEARBEHWAxBZBEARBEARBEEQd+P8Bn4wT5qI1hKEAAAAASUVORK5CYII="/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=7f44726d-ad66-442e-a703-96309fe1b1db">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Wykres punktowy przedstawia zakres wiekowy podróżnych
Wniosek jaki się nasuwa to to, że większośc pasażerów była w wieku 20-30 lat</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=c493f813-568b-4b35-bb68-9c6ee17d2866">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="A-teraz-poka%C5%BC%C4%99-ten-sam-wykres-z-oznaczeniem-innym-kolorem-wszystkich-pasa%C5%BCer%C3%B3w-poni%C5%BCej-18-roku-%C5%BCycia.">A teraz pokażę ten sam wykres z oznaczeniem innym kolorem wszystkich pasażerów poniżej 18 roku życia.<a class="anchor-link" href="#A-teraz-poka%C5%BC%C4%99-ten-sam-wykres-z-oznaczeniem-innym-kolorem-wszystkich-pasa%C5%BCer%C3%B3w-poni%C5%BCej-18-roku-%C5%BCycia.">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=205002c1-fae9-43fe-be3e-534776ee5527">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [9]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">dropna</span><span class="p">(</span><span class="n">subset</span><span class="o">=</span><span class="p">[</span><span class="s1">'age'</span><span class="p">])</span>
<span class="c1">#Oddzielenie dorosłych od dzieci</span>
<span class="n">children</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">]</span> <span class="o">&lt;</span> <span class="mi">18</span><span class="p">]</span>
<span class="n">adults</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">18</span><span class="p">]</span>

<span class="c1"># Zliczenie dorosłych i dzieci</span>
<span class="n">num_children</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">children</span><span class="p">)</span>
<span class="n">num_adults</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">adults</span><span class="p">)</span>

<span class="c1"># Stworzenie wykresu</span>
<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">children</span><span class="p">[</span><span class="s1">'age'</span><span class="p">],</span> <span class="n">children</span><span class="o">.</span><span class="n">index</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'blue'</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="sa">f</span><span class="s1">'Dzieci (&lt;18): </span><span class="si">{</span><span class="n">num_children</span><span class="si">}</span><span class="s1">'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">adults</span><span class="p">[</span><span class="s1">'age'</span><span class="p">],</span> <span class="n">adults</span><span class="o">.</span><span class="n">index</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'red'</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="sa">f</span><span class="s1">'Dorośli (&gt;=18): </span><span class="si">{</span><span class="n">num_adults</span><span class="si">}</span><span class="s1">'</span><span class="p">)</span>

<span class="c1"># Dodanie nazw osi i legendy</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'Wiek'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'Passenger Index'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Wykres punktowy uczestników według podziału na płeć'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">()</span>

<span class="c1"># Reverse axes</span>
<span class="n">plt</span><span class="o">.</span><span class="n">gca</span><span class="p">()</span><span class="o">.</span><span class="n">invert_yaxis</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA1sAAAIiCAYAAAA+ZtK4AAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjEwLjAsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvlHJYcgAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsnXl4FEX6x7+TCTkgB+QAQoIEERVUELwQDfexKhINiIAoioIXCiKwq7ICqy6IB+CB/mAVxMidIB4rShBYFFRWcAV1FRGEREAO5RAIMHl/f/T2kEmmu6una3q6J+/nefqZpKemurq6uvt9633rfT1ERGAYhmEYhmEYhmGkEhPpBjAMwzAMwzAMw0QjrGwxDMMwDMMwDMOEAVa2GIZhGIZhGIZhwgArWwzDMAzDMAzDMGGAlS2GYRiGYRiGYZgwwMoWwzAMwzAMwzBMGGBli2EYhmEYhmEYJgywssUwDMMwDMMwDBMGWNliGIZhGIZhGIYJA6xsMQzDMIwE/v3vfyMhIQGvv/56pJvCMDWGmTNnIikpCV9++WWkm8IwQWFli2EcypIlS+DxeLBw4cJq37Vu3Roejwcffvhhte+aNWuGtm3bmjrWnDlz4PF48O9//zvk9kYzq1evhsfjwZIlS3TLrVu3DhMmTMDvv/9uT8MYKX2uXt/Vq1f7991+++1ISkoSruP3339Hv3798Mgjj2DIkCEht8Wp3H777cjNzQ3Y5/F4MGHChIi0xy7UZ+OOHTtM/S43Nxe33357SMe08lu30KlTJ3Tq1MlyPV999RUefvhhLF68GJdccon1hjFMGGBli2EcSqdOneDxeLBq1aqA/QcPHsTmzZtRp06dat+Vlpbip59+QufOne1sKvM/1q1bh4kTJ7KyZSMy+rxt27ZYv3696UkKFSLC4MGD0blzZ4wfPz7kdjDRw9KlS/HXv/410s2Iag4fPoybbroJzz//PK655ppIN4dhNImNdAMYhglORkYGLrzwwoDZdgBYs2YNYmNjceedd1ZTttT/7VS2jh07htq1a9t2PIaRTUpKCtq1axfy7z0eD5YtWyaxRYzbadOmTaSbEPWkpKRg69atkW4GwxjCli2GcTCdO3fG999/j927d/v3rV69GpdddhmuvfZafPnllzhy5EjAd16vF3l5eTh69Cjq1q2Lu+++u1q9O3bsgNfrxTPPPKN57N27d+OSSy5B8+bN/S801bVq8+bN6NGjB5KTk9G1a1cAwMmTJ/Hkk0/i/PPPR3x8PDIzM3HHHXdg3759AfV+/PHH6NSpE9LT05GYmIizzjoLffr0wbFjx3T7Ijc3F7169cLSpUvRqlUrJCQk4Oyzz8YLL7wQUE7L7SeYq1inTp1w4YUXYsOGDcjLy0Pt2rVx9tlnY/LkyaioqNBtz+HDh9GzZ080aNAAX3zxBSZMmIAxY8YAAJo2bQqPxxNwvIqKCkyZMsXfP/Xr18dtt92G0tJSf50vv/wyYmJi8Ouvv/r3Pffcc/B4PLj//vv9+yoqKlCvXj08/PDDICI0b94cPXv2rNbGo0ePIjU1NeC3VdmxYwc8Hg/mzJlT7btgbmL//e9/MWDAADRo0ADx8fE466yzcNttt6G8vByAcp3Uc6+6Ve77rVu3YuDAgahfvz7i4+PRokULvPzyywHHqqiowJNPPonzzjsPiYmJqFu3Llq1aoXp06cDgGGfq2Nm+fLlaNu2LRITE3H++edXW1MVbGwE49NPP0VGRgZ69eqFP/74AwDwySefoGvXrkhOTkbt2rXRvn17vP/++/7fHD58GLGxsQH32v79+xETE4PU1FScPn3av//BBx9EZmYmiCjo8b/55ht4PB4sXrzYv+/LL7+Ex+PBBRdcEFC2d+/e1dyqFi5ciCuvvBJ16tRBUlISevbsiU2bNlU7zpw5c3Deeef5r8vcuXN1+0VlwoQJ8Hg8Qeurek+Wl5fj4YcfRsOGDVG7dm106NABX375pZALnTpmp0yZgqeeegpnnXUWEhIScOmll2LlypXVyhtdI5XPPvsMV111FRISEtCoUSM88sgjOHXqVNBzCbZVdoureh4nTpzAww8/jIsvvhipqalIS0vDlVdeKaSkm3mmBUO9Lt988w0GDBiA1NRUNGjQAEOGDMGhQ4cCyr788svo0KED6tevjzp16uCiiy7ClClTqvWD3nE2bdqEgoICpKSkIDU1FYMGDar2HgiG6DsEAObNm4crr7wSSUlJSEpKwsUXX4zXXnvN8BgMEwlY2WIYB6NaqCq/TFetWoWOHTviqquugsfjwdq1awO+a9u2LVJTU5GUlIQhQ4bgrbfeqvZCnTFjBuLi4jTXlmzZsgVXXHEF4uPjsX79ejRv3tz/3cmTJ9G7d2906dIFy5Ytw8SJE1FRUYH8/HxMnjwZAwcOxPvvv4/JkydjxYoV6NSpE44fPw5AEZKuu+46xMXF4fXXX8fy5csxefJk1KlTBydPnjTsj6+++gojR47EQw89hKVLl6J9+/YYMWIEnn32WeE+rcqePXtwyy23YNCgQXjnnXdwzTXX4JFHHkFhYaHmb0pLS3H11Vfj559/xvr163H55ZfjrrvuwgMPPAAAKC4uxvr16wNc0+699178+c9/Rvfu3fHOO+/giSeewPLly9G+fXvs378fANCtWzcQUYDAWFJSgsTERKxYscK/79///jd+//13dOvWDR6PBw888ABWrFhRbZZ37ty5OHz4sK6yZYb//Oc/uOyyy/DZZ5/hb3/7Gz744ANMmjQJ5eXl/uu3dOlS/7mvX78en376KS666CLUqVMHZ511FgDg22+/xWWXXYYtW7bgueeew3vvvYfrrrsODz74ICZOnOg/3pQpUzBhwgQMGDAA77//PhYuXIg777zT7zJo1Odqmx9++GE89NBDWLZsGVq1aoU777wT//rXv0yd+6JFi9C1a1f069cPy5YtQ506dbBmzRp06dIFhw4dwmuvvYb58+cjOTkZ119/vX+tZUpKCi677DKUlJT461q5ciXi4+Nx5MgRfPHFF/79JSUl6NKlS1CFBQAuuOACZGVlBdSljo9vv/0Wv/zyCwDg9OnTWLNmDbp16+Yv9/e//x0DBgxAy5YtsWjRIrz55ps4cuQI8vLy8O233/rLzZkzB3fccQdatGiBoqIijBs3Dk888QQ+/vjjoG1auXIlrrjiigClUYQ77rgD06ZNwx133IFly5ahT58+uPHGG025g7700ktYvnw5pk2bhsLCQsTExOCaa67B+vXr/WVErhGgjMmuXbvi999/x5w5c/Dqq69i06ZNePLJJwOOed111wWM7/Xr1+P5558HgGoKb2XKy8tx8OBBjB49Gm+//Tbmz5+Pq6++GgUFBUGV2a+//hqtW7fGb7/9JtwfRvTp0wfnnnsuioqK8Je//AXz5s3DQw89FFBm27ZtGDhwIN5880289957uPPOO/HMM88EnbTT4sYbb8Q555yDJUuWYMKECXj77bfRs2fPagpbaWkp2rRpg61btwq/QwDg8ccfxy233IJGjRphzpw5WLp0KQYPHoyff/7ZWgcxTLgghmEcy8GDBykmJoaGDRtGRET79+8nj8dDy5cvJyKiyy+/nEaPHk1ERDt37iQANHbsWP/vt23bRjExMTR16lT/vuPHj1N6ejrdcccd/n2zZ88mALRhwwZasWIFpaSkUN++fen48eMB7Rk8eDABoNdffz1g//z58wkAFRUVBezfsGEDAaAZM2YQEdGSJUsIAH311Vem+6JJkybk8Xiq/bZ79+6UkpJCf/zxR8C5bN++PaDcqlWrCACtWrXKv69jx44EgD7//POAsi1btqSePXtW++3ixYtp06ZN1KhRI8rLy6MDBw4E/O6ZZ54JeuzvvvuOANB9990XsP/zzz8nAPToo4/69+Xk5NCQIUOIiKi8vJzq1KlDf/7znwkA/fzzz0RE9NRTT1GtWrXo6NGjRER0+PBhSk5OphEjRlQ7j86dO1ftygC2b99OAGj27NnVvgNA48eP9//fpUsXqlu3Lv3666+6dVZm+PDhFBsbS//85z/9+3r27Ek5OTl06NChamUTEhLo4MGDRETUq1cvuvjii3Xr1+pzImXMJCQk+PuNSBn/aWlpdPfdd/v3BRsbgwcPpjp16hAR0eTJk8nr9dLTTz8dUH+7du2ofv36dOTIEf++06dP04UXXkg5OTlUUVFBRETjxo2jxMREOnHiBBER3XXXXfSnP/2JWrVqRRMnTiQiorKyMgJAM2fO1D3fQYMG0dlnn+3/v1u3bjR06FCqV68evfHGG0RE9OmnnxIA+uijj4hIeTbExsbSAw88EFDXkSNHqGHDhtSvXz8iIvL5fNSoUSNq27atv+1ERDt27KBatWpRkyZN/Pt2795NAOi8886jDRs2EBHR+PHjKZhYUfWe/OabbwgA/fnPfw4opz5HBg8erNsH6pht1KhRwDPq8OHDlJaWRt26dfPvE71GN998MyUmJtKePXsCyp1//vma44uI6L///S+lp6dT586dqby83L+/SZMmuudx+vRpOnXqFN15553Upk0b//5Dhw5RZmYmZWVl+Z/zZp5pwVCvy5QpUwL233fffZSQkBBwrSvj8/no1KlTNHfuXPJ6vf770ug4Dz30UMD+t956iwBQYWEhERGdOHGCWrVqRSkpKfTmm28Skfg75KeffiKv10u33HKLblsYxkmwZYthHEy9evXQunVrv2VrzZo18Hq9uOqqqwAAHTt29K/TCrZe6+yzz0avXr0wY8YMv2vSvHnzcODAAQwfPrza8d544w1ce+21uOuuu7Bo0SIkJCQEbVefPn0C/n/vvfdQt25dXH/99Th9+rR/u/jii9GwYUN/+y+++GLExcVh2LBheOONN/DTTz+Z6o8LLrgArVu3Dtg3cOBAHD58GBs3bjRVl0rDhg1x+eWXB+xr1apV0FnSDz/8EHl5eejQoQNWrFiBtLQ0oWOo16aqe9Tll1+OFi1aBFiyunbt6rdcrFu3DseOHcOoUaOQkZHht26VlJT43cEAIDk5GXfccQfmzJnjd2/7+OOP8e233wa9zqFw7NgxrFmzBv369UNmZqbQbyZPnoyXXnoJr776qn8B+4kTJ7By5UrceOONqF27dsB4ufbaa3HixAl89tln/v75z3/+g/vuuw8ffvghDh8+bLrdF198sd+iBgAJCQk499xzhWbBiQh33303xo8fj3nz5mHs2LH+7/744w98/vnn6Nu3b0DUQq/Xi1tvvRWlpaX4/vvvASjX9Pjx41i3bh0A5fp1794d3bp1C7imAAKsUcHo2rUrfvrpJ2zfvh0nTpzAJ598gj/96U/o3LlzQF3x8fG4+uqrASjj9vTp07jtttsC+jshIQEdO3b035/ff/89fvnlFwwcODDAutakSRO0b9/e/39JSYn/Puzfvz8uvfRSw76szJo1awAA/fr1C9jft29fxMaKLyUvKCgIeEapFqt//etf8Pl8pq7RqlWr0LVrVzRo0CCg3M0336x5/D179uBPf/oTsrKysHTpUsTFxem2d/HixbjqqquQlJSE2NhY1KpVC6+99hq+++47AIoV9qKLLsLBgwfRo0ePoK7BVujdu3fA/61atcKJEycC3JY3bdqE3r17Iz09HV6vF7Vq1cJtt90Gn8+HH374Qeg4t9xyS8D//fr1Q2xsLFatWoVdu3bhkksuwTfffIM2bdpg0KBBAMTfIStWrIDP55NmrWcYO2Bli2EcTufOnfHDDz/gl19+wapVq3DJJZf4BYeOHTti06ZNOHToEFatWoXY2Fi/gKUyYsQIbN261S+Ivfzyy7jyyiuDRl5bsGABEhMTcdddd2m6MtWuXRspKSkB+/bu3Yvff/8dcXFxqFWrVsC2Z88ev5tcs2bNUFJSgvr16+P+++9Hs2bN0KxZM/8aHCMaNmyoue/AgQNCdVQlPT292r74+PgAtxWVt99+G8ePH8e9996L+Ph44WOobcvKyqr2XaNGjQLa3q1bN+zcuRNbt25FSUkJ2rRpg/r166NLly4oKSnxC+1VhfIHHngAR44cwVtvvQVAcbHKyclBfn6+cDv1+O233+Dz+ZCTkyNUvrCwEI8++igef/xx3Hnnnf79Bw4cwOnTp/Hiiy9WGyvXXnstAPjHyyOPPIJnn30Wn332Ga655hqkp6eja9euplIUmLm+VTl58iQWLlyICy64oFq0s99++w1EpHlN1XMFgPbt26N27dooKSnBjz/+iB07dviVrc8//xxHjx5FSUkJzj77bDRt2lS3Tep1LykpwSeffIJTp06hS5cu6Natm19pLykpwVVXXYXExEQAyv0JAJdddlm1Pl+4cKG/v9X26t1nAHD++efjnXfeMeg9bdTjVFZsACA2Njbo9dJCq50nT57E0aNHTV2jAwcOGJ53ZY4cOYJrr70Wp06dwgcffIDU1FTdthYXF6Nfv37Izs5GYWEh1q9fjw0bNmDIkCE4ceIEAGVybNasWcL3mFmq9q36DFPvhZ07dyIvLw9lZWWYPn061q5diw0bNvjXUorcM0D1PlOv64EDB5CVlYUnn3yy2ntK9B2irt8KVx8xTDjgaIQM43A6d+6M559/HqtXr8bq1av9AikA/wvrX//6lz9wRtXcQF26dMGFF16Il156CUlJSdi4caPmeqS33noLf/3rX9GxY0d89NFHuPjii6uVCaaEZWRkID09HcuXLw9ab3Jysv/vvLw85OXlwefz4d///jdefPFFjBw5Eg0aNED//v11+2LPnj2a+1RBQp3pVgM2qKgvaytMnToVCxcuxDXXXIOlS5eiR48eQr9T27Z79+5qQsIvv/yCjIwM//9qwJGSkhKsWLEC3bt39+8fN24c/vWvf6G8vLyasnXOOefgmmuuwcsvv4xrrrkG77zzDiZOnAiv16vbNq3+qqq8pqWlwev1BgT00GLFihUYMmQIbr/99oA1WIBirVUtC1qz06rCERsbi1GjRmHUqFH4/fffUVJSgkcffRQ9e/bErl27wh4FMz4+HqtWrULPnj3RrVs3LF++HPXq1fOfR0xMTEDwGhV17ZR6XePi4nD11VejpKQEOTk5aNiwIS666CKcffbZAJQ1mStXrkSvXr0M25STk4Nzzz0XJSUlyM3NxaWXXoq6deuia9euuO+++/D555/js88+C+h3tR1LlixBkyZNNOtWx6nefaa2IZiwW3ksVZ6MqHrvqcfZu3cvsrOz/ftPnz5tatJEq51xcXF+65HoNUpPTzc8b5VTp06hT58+2LZtG9auXSsk+BcWFqJp06ZYuHBhwDO08n2XnJwc9JkSzmdaZd5++2388ccfKC4uDhgnX331lal69uzZE/S6pqenIzY2FjfccAOmTZsW8BvRd4hqVS8tLUXjxo1NtYthIgVbthjG4XTo0AFerxdLlizBN998ExDxKjU1FRdffDHeeOMN7NixQzPk+4MPPoj3338fjzzyCBo0aICbbropaLm0tDSUlJSgRYsW6Ny5s9+dy4hevXrhwIED8Pl8uPTSS6tt5513XrXfeL1eXHHFFf5ZUxE3wG+++Qb/+c9/AvbNmzcPycnJfkudmnj166+/DihnZSZeJSEhAcXFxejVqxd69+5dLZJY1ZlilS5dugBANSV3w4YN+O677/wKFqBYv1q2bImioiJ8+eWXfmWre/fu2LdvH55//nl/0IWqjBgxAl9//TUGDx4Mr9eLoUOHGp5TgwYNkJCQUK2/qp5bYmIiOnbsiMWLF+sKeV999RX69OmDLl26YObMmdW+r127Njp37oxNmzahVatWQcdLMOtG3bp10bdvX9x///04ePCgPzKbVp/Lok2bNlizZg1KS0vRqVMnv8tVnTp1cMUVV6C4uDjg2BUVFSgsLPQrRSrdunXDl19+iaKiIr+iXKdOHbRr1w4vvvgifvnlF0MXwsp1ffzxxwHK+LnnnouzzjoLjz/+OE6dOhVQV8+ePREbG4tt27YF7W/VDfC8885DVlYW5s+fHxAR8eeff/a7QOqhde+9++67Af936NABAKolbF+yZImpQBvFxcV+qxCgWJveffdd5OXlwev1mrpGnTt3xsqVK/1WQADw+XxBk8rfeeedWL16NYqLi9GqVSuhtno8HsTFxQUoWnv27BGKRhjOZ1rVNgIIUJSJCLNmzTJVj2pdV1m0aBFOnz6tm8RY9B3So0cPeL1evPLKK6baxDCRhC1bDONwUlJS0LZtW7z99tuIiYnxr9dS6dixo3+WUEvZGjRoEB555BH861//wrhx43TXFiQnJ2P58uUoKCjwR84zytvVv39/vPXWW7j22msxYsQIXH755ahVqxZKS0uxatUq5Ofn48Ybb8Srr76Kjz/+GNdddx3OOussnDhxwh+GW0TQbNSoEXr37o0JEyYgKysLhYWFWLFiBZ5++mm/leOyyy7Deeedh9GjR+P06dOoV68eli5dik8++cSwfhFq1aqF+fPn46677kLfvn0xd+5cDBgwAABw0UUXAQCmT5+OwYMHo1atWjjvvPNw3nnnYdiwYXjxxRf9EdN27NiBv/71r2jcuHG1iGBdu3bFiy++iMTERP/1btq0KZo2bYqPPvoIvXv3Drq2pXv37mjZsiVWrVqFQYMGoX79+obn4/F4MGjQILz++uto1qwZWrdujS+++ALz5s2rVvb555/H1VdfjSuuuAJ/+ctfcM4552Dv3r1455138H//938gIlx77bVITEzE6NGjq7n7tWzZEikpKZg+fTquvvpq5OXl4d5770Vubi6OHDmCH3/8Ee+++64/8t3111+PCy+8EJdeeikyMzPx888/Y9q0aWjSpIk/QqZWn1e2plqlRYsWWLt2Lbp164YOHTr4LVSTJk1C9+7d0blzZ4wePRpxcXGYMWMGtmzZgvnz5wcI1l27doXP58PKlSvxxhtv+Pd369YN48ePh8fj8SvlRnTt2hUzZszA/v37AywEXbt2xezZs1GvXr2AsO+5ubn429/+hsceeww//fQT/vSnP6FevXrYu3cvvvjiC9SpUwcTJ05ETEwMnnjiCdx111248cYbMXToUPz++++YMGGCpjtdZa699lqkpaXhzjvvxN/+9jfExsZizpw52LVrV0C5Cy64AAMGDMBzzz0Hr9eLLl264JtvvsFzzz2H1NRUxMSIzQN7vV50794do0aNQkVFBZ5++mkcPnw4wKoneo3GjRuHd955B126dMHjjz+O2rVr4+WXX/avgVR55pln8Oabb+KBBx5AnTp1AiakUlJS0LJly6Bt7dWrF4qLi3Hfffehb9++2LVrF5544glkZWUZ5ooK9zNNpXv37oiLi8OAAQMwduxYnDhxAq+88orpiIjFxcWIjY1F9+7d8c033+Cvf/0rWrduXW2NXmVE3yG5ubl49NFH8cQTT+D48eP+UPbffvst9u/fX82SzjCOIILBORiGEWTs2LEEgC699NJq37399tsEgOLi4vwR+YJx++23U2xsLJWWllb7rnI0QpXy8nLq06cPJSQk0Pvvv09EgRHaqnLq1Cl69tlnqXXr1pSQkEBJSUl0/vnn0913301bt24lIqL169fTjTfeSE2aNKH4+HhKT0+n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oMzChQupdevWlJiYSGeddRZNmTIl4PuioiLq1q0bZWRkUHJyMrVr184wWXNElK1GjRoFtVpt2bKFGjVqREREX375JaWnp5ut2tE4UdkiUhSXqhYurzdyipaKljwmK3+tmXbYqdhFDeXlRDEx+sKalvAZyc0oW7YMy8zcufLa6xTrgllriCtmDCTipoATbNliwoSbla0//elPtHv3biotLaUvv/ySnnrqKUpKSqJrrrmGTp06FXLdJ0+etNy+qsqWCE899VQ1o0ZZWZmlc9Hj6NGjdM8999DMmTOpZ8+eQZWttWvXUkxMDE2fPp1++uknWrt2LV1wwQV0ww03BJQrKCigsWPHmjr+4cOHqV69enT77bfTf//7X9qyZQv16dOH6tev778G//znPyk2NpZeeeUV2rZtG7333nvUsGFDevHFF/31jBgxgp5++mn64osv6IcffqBHHnmEatWqRRs3btQ8dkSUrTp16tCqIA/pVatWUVJSEhERbdu2jZKTk81W7WicqmwRKXLx1KlEw4crn3a7DmoRTB6zUw4wmqx32oS0o5AZCtzOraTE+NysWmZELVspKfKsIeFWbtgaoo+blC23WeIY1yBN2bJ5smbw4MFBlYOVK1cSAJo1a5Z/388//0y9e/emOnXqUHJyMt100020Z88e//eqi99rr71GTZs2JY/HQxUVFYa/++qrr6hTp06UlJREycnJ1LZtW9qwYQMRheZGeNFFF9FLL70UsG/ChAnUoEEDGjVqFH399dcmesgcWv35zDPP0Nlnnx2w74UXXqCcnJyAfXPmzKHGjRubOuaGDRsIAO3cudO/7+uvvyYA9OOPPxIR0YABA6hv374Bv5s6dSrl5ORQRUWFZt0tW7akiRMnan4vQ9kyndQ4Pz8fQ4YMwdKlS1FaWoqysjIsXboUd955J2644QYAwBdffIFzzz1XwooyRoS4OGW984svKp9xcZFukUKwXK52rjWXle+1RiJ6AerU0f7O4wEyM+W0BwASE/W/F82WHSyB7fbt4pEBRc/p9tuVT6vJe4uLgdxcoHNnYOBA5TM3V9kvC9FF2jIXc/t8SjTL+fOVT71kyJFENOCEU9rP2dwZJ2PH80yQLl26oHXr1ij+37GJCDfccAMOHjyINWvWYMWKFdi2bRtuvvnmgN/9+OOPWLRoEYqKivDVV18BgOHvbrnlFuTk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P/1009dZx/rV19eLUaNGie7ubtavBueff774wQ9+kPFcXV2dmDZtmhAifNcwhxGGwKFDh/Dqq6/i7LPPznj+7LPPxsaNGwtUquLU2tqKHTt2ZNR1//79MX78eNZ1ntrb2wEA5eXlAFjHOiWTSaxatQoHDhzAmDFjWLca/fjHP8b555+Ps846K+N51rEeW7duRXV1NUaOHIlLL70U77zzDgDWrw5PPvkkTj31VFx00UUYOnQovvrVr2L58uWp11nHeh06dAgrVqzAD37wA0QiEdavBqeffjqeffZZvP322wCAv/zlL3jxxRdx3nnnAQjfNdyn0AUgex9//DGSySSGDRuW8fywYcOwY8eOApWqOBn1mauu33333UIUKdSEEJg7dy5OP/10HH/88QBYxzps2bIFY8aMwaeffoqBAwdi7dq1OO6441I/Mqxbd1atWoXXXnsNr7zySq/XeP26941vfAO/+c1v8MUvfhEffvghbrnlFowdOxZvvPEG61eDd955Bw8++CDmzp2Lm266CS+//DKuvfZa9O/fH1dccQXrWLMnnngCe/fuxZVXXgmA3xE63HDDDWhvb8exxx6LaDSKZDKJW2+9FZdddhmA8NUxg60QiUQiGf8vhOj1HOnButZj5syZ+Otf/4oXX3yx12us4/x96UtfQktLC/bu3YvGxkbMmDEDzz33XOp11m3+3n//fdTX1+Ppp5/G5z73OdPtWMf5+853vpP67xNOOAFjxozBqFGj8Otf/xqnnXYaANavG93d3Tj11FPxi1/8AgDw1a9+FW+88QYefPBBXHHFFantWMd6/OpXv8J3vvMdVFdXZzzP+s3fY489hhUrVqChoQFf+cpX0NLSgtmzZ6O6uhozZsxIbReWOuYwwhAYMmQIotFor16snTt39orqyR0jIxbr2r1Zs2bhySefRCKRQDweTz3POnavX79++MIXvoBTTz0VS5YswUknnYR77rmHdavBq6++ip07d+KUU05Bnz590KdPHzz33HO499570adPn1Q9so71GTBgAE444QRs3bqV17AGRx55JI477riM57785S/jvffeA8DvYJ3effddbNiwAf/+7/+eeo716968efPw05/+FJdeeilOOOEETJ8+HXPmzMGSJUsAhK+OGWyFQL9+/XDKKafgmWeeyXj+mWeewdixYwtUquI0cuRIVFVVZdT1oUOH8Nxzz7GuFQkhMHPmTDQ1NeEPf/gDRo4cmfE661g/IQQ6OztZtxqceeaZ2LJlC1paWlKPU089FVOnTkVLSwuOOeYY1rFmnZ2d+L//+z8ceeSRvIY1+OY3v9lruY23334bI0aMAMDvYJ0eeeQRDB06FOeff37qOdavewcPHkRZWWaIEo1GU6nfQ1fHhcnLQU4Zqd9/9atfiTfffFPMnj1bDBgwQPzzn/8sdNFCZ9++fWLz5s1i8+bNAoBYunSp2Lx5cyqN/m233SZisZhoamoSW7ZsEZdddllg04kG0Q9/+EMRi8VEc3NzRmrcgwcPprZhHefvxhtvFM8//7xobW0Vf/3rX8VNN90kysrKxNNPPy2EYN16IT0boRCsY7d+8pOfiObmZvHOO++Il156SUyaNEkMGjQo9XvG+nXn5ZdfFn369BG33nqr2Lp1q1i5cqU4/PDDxYoVK1LbsI7dSyaT4qijjhI33HBDr9dYv+7MmDFDDB8+PJX6vampSQwZMkRcf/31qW3CVMcMtkLk/vvvFyNGjBD9+vUTJ598ciqVNjmTSCQEgF6PGTNmCCFkStGFCxeKqqoq0b9/f3HGGWeILVu2FLbQIZKrbgGIRx55JLUN6zh/P/jBD1LfA5WVleLMM89MBVpCsG69kB1ssY7dMdbD6du3r6iurhZ1dXXijTfeSL3O+nXvf/7nf8Txxx8v+vfvL4499ljx8MMPZ7zOOnbv97//vQAg3nrrrV6vsX7d6ejoEPX19eKoo44Sn/vc58Qxxxwj5s+fLzo7O1PbhKmOI0IIUZAuNSIiIiIioiLGOVtEREREREQeYLBFRERERETkAQZbREREREREHmCwRURERERE5AEGW0RERERERB5gsEVEREREROQBBltEREREREQeYLBFRERERETkAQZbRERENpqbmxGJRLB3717lvzn66KNx9913e1YmIiIKPgZbRERUUh566CEMGjQIXV1dqef279+Pvn37Yty4cRnbvvDCC4hEIqiursb27dsRi8X8Li4REYUYgy0iIiopEydOxP79+/HnP/859dwLL7yAqqoqvPLKKzh48GDq+ebmZlRXV+OLX/wiqqqqEIlEClFkIiIKKQZbRERUUr70pS+huroazc3Nqeeam5tRW1uLUaNGYePGjRnPT5w4Mecwwo0bN+KMM87AYYcdhpqaGlx77bU4cOCA6XEfeeQRxGIxPPPMM16cFhERBRCDLSIiKjkTJkxAIpFI/X8ikcCECRMwfvz41POHDh3Cpk2bMHHixF5/v2XLFpxzzjmoq6vDX//6Vzz22GN48cUXMXPmzJzHu/POO3Hdddfh97//Pb797W97c1JERBQ4DLaIiKjkTJgwAX/84x/R1dWFffv2YfPmzTjjjDMwfvz4VI/XSy+9hE8++SRnsHXHHXfg8ssvx+zZszF69GiMHTsW9957L37zm9/g008/zdj2xhtvxNKlS9Hc3IzTTjvNj9MjIqKA6FPoAhAREflt4sSJOHDgAF555RXs2bMHX/ziFzF06FCMHz8e06dPx4EDB9Dc3IyjjjoKxxxzDN57772Mv3/11Vfx97//HStXrkw9J4RAd3c3Wltb8eUvfxkAcNddd+HAgQP485//jGOOOcbXcyQiosJjzxYREZWcL3zhC4jH40gkEkgkEhg/fjwAoKqqCiNHjsQf//hHJBIJfOtb38r5993d3fiP//gPtLS0pB5/+ctfsHXrVowaNSq13bhx45BMJrF69WpfzouIiIKFPVtERFSSjMQXe/bswbx581LPjx8/Hr///e/x0ksv4fvf/37Ovz355JPxxhtv4Atf+ILlMb7+9a9j1qxZOOeccxCNRjOOQ0RExY89W0REVJImTpyIF198ES0tLameLUAGW8uXL8enn36ac74WANxwww3YtGkTfvzjH6OlpQVbt27Fk08+iVmzZvXadsyYMfjd736Hm2++GcuWLfPsfIiIKHjYs0VERCVp4sSJ+OSTT3Dsscdi2LBhqefHjx+Pffv2YdSoUaipqcn5tyeeeCKee+45zJ8/H+PGjYMQAqNGjcIll1ySc/tvfvOb+O1vf4vzzjsP0WgU1157rSfnREREwRIRQohCF4KIiIiIiKjYcBghERERERGRBxhsEREREREReYDBFhERERERkQcYbBEREREREXmAwRYREREREZEHGGwRERERERF5gMEWERERERGRBxhsEREREREReYDBFhERERERkQcYbBEREREREXmAwRYREREREZEH/j91X4YwGtCwZAAAAABJRU5ErkJggg=="/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=334e1dfe-6931-42ae-8ca8-a3ba156e0ecd">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>W kolumnie age w samej bazie danych mamy tylko 1046 elementów i ten wykres jest zrobiony tylko dla tej grupy, ale
wyraźnie widać, na podstawie tak dużej grupy próbnej jak kształtował się podział wiekowy i jaki mniej więcej odsetek stanowiły dzieci.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=50841e38-6036-4bba-97e1-379b4055aa1e">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Procentowo wyglądało to tak:</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=1dd7d2d4-eff3-464d-9b51-b0bb0caa485e">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [10]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Przeliczenie dorosłych i dzieci</span>
<span class="n">children_count</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">]</span> <span class="o">&lt;</span> <span class="mi">18</span><span class="p">]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">adults_count</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">18</span><span class="p">]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>

<span class="c1"># Stworzenie wykresu kołowego</span>
<span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Dzieci (&lt;18)'</span><span class="p">,</span> <span class="s1">'Dorośli (18+)'</span><span class="p">]</span>
<span class="n">sizes</span> <span class="o">=</span> <span class="p">[</span><span class="n">children_count</span><span class="p">,</span> <span class="n">adults_count</span><span class="p">]</span>
<span class="n">colors</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'#66b3ff'</span><span class="p">,</span><span class="s1">'#ff9999'</span><span class="p">]</span>
<span class="n">explode</span> <span class="o">=</span> <span class="p">(</span><span class="mf">0.1</span><span class="p">,</span> <span class="mi">0</span><span class="p">)</span>  <span class="c1"># wykrojenie kawałka</span>

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">8</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">sizes</span><span class="p">,</span> <span class="n">explode</span><span class="o">=</span><span class="n">explode</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">colors</span><span class="o">=</span><span class="n">colors</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%1.1f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">shadow</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">startangle</span><span class="o">=</span><span class="mi">140</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">'equal'</span><span class="p">)</span>  
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[10]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(np.float64(-1.202097982230382),
 np.float64(1.1048616765885606),
 np.float64(-1.0999999847206687),
 np.float64(1.0999998206482027))</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAzkAAAJ8CAYAAADd8G9yAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjEwLjAsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvlHJYcgAAAAlwSFlzAAAPYQAAD2EBqD+naQAAjrJJREFUeJzs3Xd8XPWd7//XjHqX1asl945xAWxsXMA2NhgMBAIEbJJsNtm7m/3tJje5d282d2/uluTevWyyYVN2s5sEUghsSIAkgGk2buBu494kW713zWjqOb8/xhYWtmxpLOlMeT8fDz3Ao3POfISNZ97z/ZzP12aapomIiIiIiEiEsFtdgIiIiIiIyEhSyBERERERkYiikCMiIiIiIhFFIUdERERERCKKQo6IiIiIiEQUhRwREREREYkoCjkiIiIiIhJRFHJERERERCSiKOSIiIiIiEhEUcgREREREZGIopAjIiIiIiIRRSFHREREREQiikKOiIiIiIhEFIUcERERERGJKAo5IiIiIiISURRyREREREQkoijkiIiIiIhIRFHIERERERGRiKKQIyIiIiIiEUUhR0REREREIopCjoiIiIiIRBSFHBERERERiSgKOSIiIiIiElEUckREREREJKIo5IiIiIiISERRyBERERERkYiikCMiIiIiIhFFIUdERERERCKKQo6IiIiIiEQUhRwREREREYkoCjkiIiIiIhJRFHJERERERCSiKOSIiIiIiEhEUcgREREREZGIopAjIiIiIiIRRSFHREREREQiikKOiIiIiIhElFirCxARkTDl94PLdfUvtxu83sAxPt9H/xzs3w3jo+vabIGvwf7dZgO7HeLihv6VmAhJSZCcHPh3uz7jExGJZAo5IiIykM8Hvb1XfjmdA4OMzzc6z2+ao3Pdy10eepKSBn4lJ0NaGqSmQqxeJkVEwpHNNMfi1UREREKGYUBXV+Crtxd6egaGmb4+qysMHUlJHwWe9PSPvjIyAmHo0iqTiIiEFIUcEZFI5fMFgkxHB3R2Bv7Z0QHd3QPbwyQ4sbGBADRuHGRlffSVlqbwIyJiMYUcEZFwZ5qBENPaCu3tH4Wanp6xaf2SgWJjrww+WVmBVSERERkTCjkiIuHENAMhprUVWloC/2xrG737Y2TkJCUFwk5uLuTnB74SE62uSkQkIinkiIiEMocDmpsDgebS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APB9n/1qleruLvu1Gvu1GvVqld2tLXYrFVrNJp2DA3hjulPMQiGisRiRSIRINNrdgufhc74aZIzB9zxc18VzXVzXxWm3D2MGYzB0J7nF4nGisRixRIKhfJ58oUB+ZITc8DBDwWM6m1XMiIicI4ocEZEBd7D606jXDwOoUa9TDVaC6rUanVYLx3XxHAfXdbunZVlWd5xzcD1QJBIhFA4TDocJhUKE3vUYPLcs63eHkjGmu/k+frAdBIvv+2+8fjxi3vhxdmSfD6ItnkiQGx5meHSUbD5PJpsllcmQzmZJZ7Mk02nCWuUSERkIihwREcFxnO5F9LZNq9nsPh553qjX2Q+uBeoEKyK+5x3Gx0F0+L6PdyRIILjvTRBMv8UAGINlWYexZB17PPo8Go2SOgiVTIZUJtO9LimReL0dfBxcs3SeV6dEROTDKXJEROR3OzwdzHFwHAf3yArQwWue6x6uvBjABKsyHPzYORIcB6s+4UiESCRCOBIhHA53Pw5WYiJHXwtWlRQtIiLyNoocEREREREZKLqKUkREREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBooiR0REREREBsr/A7Tvlf+UjSSUAAAAAElFTkSuQmCC"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=1399b496-6150-42f2-b0e9-ab1a590fdc82">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="A-jak-nazywa%C5%82y-si%C4%99-najm%C5%82odsze-osoby-kt%C3%B3re-prze%C5%BCy%C5%82y-katastrof%C4%99?">A jak nazywały się najmłodsze osoby które przeżyły katastrofę?<a class="anchor-link" href="#A-jak-nazywa%C5%82y-si%C4%99-najm%C5%82odsze-osoby-kt%C3%B3re-prze%C5%BCy%C5%82y-katastrof%C4%99?">¶</a></h1>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=6518167d-a9f3-484c-a870-e811a6dd4516">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [11]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">titanic_df</span> <span class="o">=</span> <span class="n">df</span>
<span class="n">prz_df</span> <span class="o">=</span> <span class="n">titanic_df</span><span class="p">[</span><span class="n">titanic_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">1</span><span class="p">]</span>
<span class="n">najm</span> <span class="o">=</span> <span class="n">prz_df</span><span class="o">.</span><span class="n">nsmallest</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="s1">'age'</span><span class="p">)</span>
<span class="n">result</span> <span class="o">=</span> <span class="p">{</span>
    <span class="s2">"type"</span><span class="p">:</span> <span class="s2">"dataframe"</span><span class="p">,</span>
    <span class="s2">"value"</span><span class="p">:</span> <span class="n">najm</span>
<span class="p">}</span>
<span class="n">najm</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[11]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>pclass</th>
<th>survived</th>
<th>name</th>
<th>sex</th>
<th>age</th>
<th>sibsp</th>
<th>parch</th>
<th>ticket</th>
<th>fare</th>
<th>cabin</th>
<th>embarked</th>
<th>boat</th>
<th>body</th>
<th>home.dest</th>
</tr>
</thead>
<tbody>
<tr>
<th>763</th>
<td>3.0</td>
<td>1.0</td>
<td>Dean, Miss. Elizabeth Gladys "Millvina"</td>
<td>female</td>
<td>0.1667</td>
<td>1.0</td>
<td>2.0</td>
<td>C.A. 2315</td>
<td>20.5750</td>
<td>NaN</td>
<td>S</td>
<td>10</td>
<td>NaN</td>
<td>Devon, England Wichita, KS</td>
</tr>
<tr>
<th>1240</th>
<td>3.0</td>
<td>1.0</td>
<td>Thomas, Master. Assad Alexander</td>
<td>male</td>
<td>0.4167</td>
<td>0.0</td>
<td>1.0</td>
<td>2625</td>
<td>8.5167</td>
<td>NaN</td>
<td>C</td>
<td>16</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>427</th>
<td>2.0</td>
<td>1.0</td>
<td>Hamalainen, Master. Viljo</td>
<td>male</td>
<td>0.6667</td>
<td>1.0</td>
<td>1.0</td>
<td>250649</td>
<td>14.5000</td>
<td>NaN</td>
<td>S</td>
<td>4</td>
<td>NaN</td>
<td>Detroit, MI</td>
</tr>
<tr>
<th>657</th>
<td>3.0</td>
<td>1.0</td>
<td>Baclini, Miss. Eugenie</td>
<td>female</td>
<td>0.7500</td>
<td>2.0</td>
<td>1.0</td>
<td>2666</td>
<td>19.2583</td>
<td>NaN</td>
<td>C</td>
<td>C</td>
<td>NaN</td>
<td>Syria New York, NY</td>
</tr>
<tr>
<th>658</th>
<td>3.0</td>
<td>1.0</td>
<td>Baclini, Miss. Helene Barbara</td>
<td>female</td>
<td>0.7500</td>
<td>2.0</td>
<td>1.0</td>
<td>2666</td>
<td>19.2583</td>
<td>NaN</td>
<td>C</td>
<td>C</td>
<td>NaN</td>
<td>Syria New York, NY</td>
</tr>
<tr>
<th>359</th>
<td>2.0</td>
<td>1.0</td>
<td>Caldwell, Master. Alden Gates</td>
<td>male</td>
<td>0.8333</td>
<td>0.0</td>
<td>2.0</td>
<td>248738</td>
<td>29.0000</td>
<td>NaN</td>
<td>S</td>
<td>13</td>
<td>NaN</td>
<td>Bangkok, Thailand / Roseville, IL</td>
</tr>
<tr>
<th>548</th>
<td>2.0</td>
<td>1.0</td>
<td>Richards, Master. George Sibley</td>
<td>male</td>
<td>0.8333</td>
<td>1.0</td>
<td>1.0</td>
<td>29106</td>
<td>18.7500</td>
<td>NaN</td>
<td>S</td>
<td>4</td>
<td>NaN</td>
<td>Cornwall / Akron, OH</td>
</tr>
<tr>
<th>611</th>
<td>3.0</td>
<td>1.0</td>
<td>Aks, Master. Philip Frank</td>
<td>male</td>
<td>0.8333</td>
<td>0.0</td>
<td>1.0</td>
<td>392091</td>
<td>9.3500</td>
<td>NaN</td>
<td>S</td>
<td>11</td>
<td>NaN</td>
<td>London, England Norfolk, VA</td>
</tr>
<tr>
<th>1</th>
<td>1.0</td>
<td>1.0</td>
<td>Allison, Master. Hudson Trevor</td>
<td>male</td>
<td>0.9167</td>
<td>1.0</td>
<td>2.0</td>
<td>113781</td>
<td>151.5500</td>
<td>C22 C26</td>
<td>S</td>
<td>11</td>
<td>NaN</td>
<td>Montreal, PQ / Chesterville, ON</td>
</tr>
<tr>
<th>590</th>
<td>2.0</td>
<td>1.0</td>
<td>West, Miss. Barbara J</td>
<td>female</td>
<td>0.9167</td>
<td>1.0</td>
<td>2.0</td>
<td>C.A. 34651</td>
<td>27.7500</td>
<td>NaN</td>
<td>S</td>
<td>10</td>
<td>NaN</td>
<td>Bournmouth, England</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=b8493f06-5ae9-45ed-9ae5-6c1b8390d8b4">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Tych ludzi jeszcze całkiem niedawno można było spotkać na ulicy :)</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=df34b38d-dd69-4819-9bf1-cc5506e5897b">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pokazanie-wykresu-ko%C5%82owego-procentowego-udzia%C5%82u-pasa%C5%BCer%C3%B3w-w-poszczeg%C3%B3lnych-klasach-z-uwzgl%C4%99dnieniem-p%C5%82ci.">Pokazanie wykresu kołowego procentowego udziału pasażerów w poszczególnych klasach z uwzględnieniem płci.<a class="anchor-link" href="#Pokazanie-wykresu-ko%C5%82owego-procentowego-udzia%C5%82u-pasa%C5%BCer%C3%B3w-w-poszczeg%C3%B3lnych-klasach-z-uwzgl%C4%99dnieniem-p%C5%82ci.">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=219030ff-8b8e-4cce-bd4a-80c9a3f9d288">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [12]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">dropna</span><span class="p">(</span><span class="n">subset</span><span class="o">=</span><span class="p">[</span><span class="s1">'pclass'</span><span class="p">,</span> <span class="s1">'sex'</span><span class="p">])</span>

<span class="c1"># Grupowanie po klasie i płci a potem zliczenie</span>
<span class="n">class_sex_counts</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'pclass'</span><span class="p">,</span> <span class="s1">'sex'</span><span class="p">])</span><span class="o">.</span><span class="n">size</span><span class="p">()</span><span class="o">.</span><span class="n">unstack</span><span class="p">()</span>

<span class="c1"># Przeliczenie całkowitej ilości pasażerów w każdej z klas</span>
<span class="n">class_totals</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">'pclass'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">sort_index</span><span class="p">()</span>

<span class="c1"># Stworzenie nazw labeli w wartości sumarycznej klas</span>
<span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="sa">f</span><span class="s1">'Class </span><span class="si">{</span><span class="nb">int</span><span class="p">(</span><span class="bp">cls</span><span class="p">)</span><span class="si">}</span><span class="s1"> (</span><span class="si">{</span><span class="n">total</span><span class="si">}</span><span class="s1">)'</span> <span class="k">for</span> <span class="bp">cls</span><span class="p">,</span> <span class="n">total</span> <span class="ow">in</span> <span class="n">class_totals</span><span class="o">.</span><span class="n">items</span><span class="p">()]</span>

<span class="c1"># Narysowanie wykresu z podziałem na płeć</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axes</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">class_sex_counts</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">'pie'</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">'male'</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%1.1f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axes</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">legend</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">class_sex_counts</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">'pie'</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">'female'</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%1.1f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axes</span><span class="p">[</span><span class="mi">1</span><span class="p">],</span> <span class="n">legend</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="c1"># Ustawienie tytułów</span>
<span class="n">axes</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">set_title</span><span class="p">(</span><span class="s1">'Mężczyźni'</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">set_title</span><span class="p">(</span><span class="s1">'Kobiety'</span><span class="p">)</span>
<span class="k">for</span> <span class="n">ax</span> <span class="ow">in</span> <span class="n">axes</span><span class="p">:</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_ylabel</span><span class="p">(</span><span class="s1">''</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">suptitle</span><span class="p">(</span><span class="s1">'Procentowy udział pasażerów z podziałem na klasę podróży i płeć'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">tight_layout</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABKUAAAJQCAYAAABfMtfbAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjEwLjAsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvlHJYcgAAAAlwSFlzAAAPYQAAD2EBqD+naQAA539JREFUeJzs3XV4U+ffBvA79VIXSmmBQnH34YMiw2HIGGMMZxtDBmPOsG38tiEzHIbDgA13dy9SoIUCLdSFukvkef/o24zQFlpo81Tuz3Xlgp4cuZPmpCffPKIQQggQERERERERERHpkYHsAEREREREREREVPawKEVERERERERERHrHohQREREREREREekdi1JERERERERERKR3LEoREREREREREZHesShFRERERERERER6x6IUERERERERERHpHYtSRERERERERESkdyxKERERERERERGR3rEoRURERNIlJCSgevXqGDlypOwoRFTI/vzzT1hbW8PLy0t2lGLl22+/RcWKFREYGCg7ChGRNCxKEVGZt379eigUCu3NyMgIlSpVwujRoxEaGio73mtLTU3FnDlzcObMGdlR9CogIAAKhQLr168v0HajRo1C1apVX+mYr7NtcdSpUyd06tRJL8caNWoUqlevjr/++ksvxyuust+PAgICCrRd1apVMWrUqFc65utsW5LNmTMHCoUC0dHRL1yvtJ3Xr+pV3w+uXbuGb7/9Fjt37kSTJk1yXSf7d1HYimK/hXW+HD58GEuWLMHBgwfh5ub2+sGIiEooI9kBiIiKi3Xr1qFOnTpIS0vDuXPn8NNPP+Hs2bO4e/cuLCwsZMd7ZampqZg7dy4A6K3AUJLNnDkTn376qewYxcKyZcv0cpxFixYhICAA586dg7GxsV6OWdrs3r0b1tbWsmMQ6YiNjcW7776LZcuWoVu3bnmuN27cOPTo0aPQj19U+31dwcHBGD16NLZv345mzZrJjkNEJBWLUkRE/69BgwZo0aIFAMDDwwNqtRo//PAD9uzZg/fffz/XbVJTU1GuXDl9xqQiVr16ddkRio169eoVyX6fP2+mT5+O6dOnF8mxyoqmTZvKjkAEpVKpbXEMAPb29njy5MlLt6tUqRIqVapU6HmKar+vq3LlyoiIiJAdg4ioWGD3PSKiPLRu3RoAtGM9jBo1CpaWlrh79y7eeustWFlZoUuX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rq655hrV19drwoQJuuOOOzR//nxJks1mU3FxsS677DLt2bNHcXFxmjRpku68805JUnNzs2bPnq3t27crIiJC5557bqud+w5ls9m0fv16/fGPf9T+/fsVGxur0047TZ988olycnLa/L5iY2M1adIkvfzyy7r33nslSQ6HQ6+88oruvPNO1dfXKyUlRbNmzWpZnP3g9d59911dffXVGjFihJxOp6ZNm6YHHnig1eufd955rUaHHRwNdejIrD//+c+aNWtWmxnhmyyeY42vAwAAAAAAOIpVq1YpPz9fBQUFCg8P9+q1V69erbPPPlsbNmxQZGSkV6+NU8P0Pfgti8WiN99803SME9LQ0KBevXpp6dKlXr/2E088ofPPP9/r1wUAAADQ+fXr10/333+/CgsLvX7tnTt36oUXXqCQ8kOUUvBJu3fv1rXXXqu0tDQ5HA51795dEydO1Icffmg6mqQDu1tkZmbK5XIpOjpa+fn5+uKLL4553tNPP62UlBSNGDGi5VhqaqosFkurr1tuuaXVeVu3btXEiRPlcrkUFxenOXPmtNpto66uTldccYX69esnu92uCy+88LBrz5o1S8uXL9enn3568t84AAAAALTh8ssvV79+/bx+3bFjx2rcuHFevy5OHWtKwecUFhZqxIgRioqK0v3336/c3Fw1Njbq/fff1+zZs7V+/XrTEZWRkaEnnnhCaWlpqq2t1cMPP6yxY8eqoKDgqFuQPv744y1zvw911113tZr/HBYW1vLj5uZmTZgwQfHx8fr0009VXFysyy+/XB6Pp2Ur1+bmZjmdTs2ZM0evvfbaEa/tcDg0bdo0Pf744xo5cuRJfucAAAAAALQPRkrB51x99dWyWCxatmyZLrroImVkZCgnJ0c33HCDPv/88zbPu/nmm5WRkaHQ0FClpaXpjjvuUGNjY8vj//3vfzVmzBiFh4crIiJCgwYN0pdffilJKioq0sSJExUdHS2Xy6WcnBy99957bV5r2rRpys/PV1pamnJycvTQQw+poqJC33zzTZvnrFixQgUFBZowYcJhj4WHhyspKanl69BSatGiRVq7dq1eeukl5eXlKT8/Xw8++KAWLlyoiooKSZLL5dKCBQs0a9YsJSUltZnh/PPP15tvvqna2to2nwMAAAAAgDdQSsGnlJSU6J///Kdmz54tl8t12ONRUVFtnhseHq7n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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=1751ec15-802d-456c-87b8-b449d668e4b1">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Nale%C5%BCy-zaznaczy%C4%87,-%C5%BCe-liczby-zawarte-w-nawiasach-oznaczaj%C4%85-liczb%C4%99-wszystkich-bilet%C3%B3w-w-danej-klasie.">Należy zaznaczyć, że liczby zawarte w nawiasach oznaczają liczbę wszystkich biletów w danej klasie.<a class="anchor-link" href="#Nale%C5%BCy-zaznaczy%C4%87,-%C5%BCe-liczby-zawarte-w-nawiasach-oznaczaj%C4%85-liczb%C4%99-wszystkich-bilet%C3%B3w-w-danej-klasie.">¶</a></h1>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=775b2667-9baa-4509-b7ad-0e8a04e14a87">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Wniosek jaki się nasuwa to to, że procentowo i liczebnie najwięcej kobiet oraz mężczyzn podróżowało w klasie 3</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=aadc7853-60be-4c64-b850-83c4580bbd42">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Poka%C5%BC-wykres-ko%C5%82owy-%C5%9Bmiertelno%C5%9Bci-do-prze%C5%BCycia-dla-klasy-1-wed%C5%82ug-podzia%C5%82u-na-wiek.">Pokaż wykres kołowy śmiertelności do przeżycia dla <em>klasy 1</em> według podziału na wiek.<a class="anchor-link" href="#Poka%C5%BC-wykres-ko%C5%82owy-%C5%9Bmiertelno%C5%9Bci-do-prze%C5%BCycia-dla-klasy-1-wed%C5%82ug-podzia%C5%82u-na-wiek.">¶</a></h1>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=bce4eeb8-3648-4425-90d6-9014692bfb10">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [13]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Odfiltrowanie klasy 1</span>
<span class="n">class_1_df</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'pclass'</span><span class="p">]</span> <span class="o">==</span> <span class="mf">1.0</span><span class="p">]</span>

<span class="c1"># Podział na wiek</span>
<span class="n">class_1_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">=</span> <span class="n">class_1_df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">'child'</span> <span class="k">if</span> <span class="n">x</span> <span class="o">&lt;</span> <span class="mi">18</span> <span class="k">else</span> <span class="s1">'adult'</span><span class="p">)</span>

<span class="c1"># Przeliczenie śmiertelności i przeżycia po grupie wiekowej</span>
<span class="n">survived_counts</span> <span class="o">=</span> <span class="n">class_1_df</span><span class="p">[</span><span class="n">class_1_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_children</span> <span class="o">=</span> <span class="n">class_1_df</span><span class="p">[(</span><span class="n">class_1_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">0</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">class_1_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'child'</span><span class="p">)]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_adults</span> <span class="o">=</span> <span class="n">class_1_df</span><span class="p">[(</span><span class="n">class_1_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">0</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">class_1_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'adult'</span><span class="p">)]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>

<span class="c1"># Przygotowanie danych pod wykres kołowy</span>
<span class="n">total_passengers</span> <span class="o">=</span> <span class="n">class_1_df</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_total</span> <span class="o">=</span> <span class="n">not_survived_children</span> <span class="o">+</span> <span class="n">not_survived_adults</span>
<span class="n">survived_total</span> <span class="o">=</span> <span class="n">total_passengers</span> <span class="o">-</span> <span class="n">not_survived_total</span>

<span class="c1"># Zrobienie wykresu</span>
<span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Przeżyli'</span><span class="p">,</span> <span class="s1">'Nie przeżyli - dzieci'</span><span class="p">,</span> <span class="s1">'Nie przeżyli - Dorośli'</span><span class="p">]</span>
<span class="n">sizes</span> <span class="o">=</span> <span class="p">[</span><span class="n">survived_total</span><span class="p">,</span> <span class="n">not_survived_children</span><span class="p">,</span> <span class="n">not_survived_adults</span><span class="p">]</span>
<span class="n">colors</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'#66b3ff'</span><span class="p">,</span> <span class="s1">'#ff9999'</span><span class="p">,</span> <span class="s1">'#99ff99'</span><span class="p">]</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">()</span>
<span class="n">ax</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">sizes</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">colors</span><span class="o">=</span><span class="n">colors</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%1.1f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">startangle</span><span class="o">=</span><span class="mi">90</span><span class="p">)</span>
<span class="n">ax</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">'equal'</span><span class="p">)</span>  
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr" tabindex="0">
<pre>C:\Users\tmirk\AppData\Local\Temp\ipykernel_19720\236861734.py:5: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  class_1_df['age_group'] = class_1_df['age'].apply(lambda x: 'child' if x &lt; 18 else 'adult')
</pre>
</div>
</div>
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[13]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(np.float64(-1.099999739845874),
 np.float64(1.099999095319948),
 np.float64(-1.0999989640946295),
 np.float64(1.0999999506711728))</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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6qskJSVdekGXaOPGjdx1111Oez17UgCSSgJ94P7LbG+QIuJ6gn3gH70hxLd2r+vn58eMGTPIycmp9hh/f38iIiJq94EvQmlpaa1dq7aeQ2hoqFO0hjVs2JCAgNp7w6/t69mTApCcI8zPFoJq+w1SRIwV6A0P9IHIoNq/9uDBg4mMjOTZZ5+t9piquo++/PJLevTogZ+fH7GxsUyePJny8vJqr3G262jy5MlEREQQEhLC3XffXSnkDBgwgPHjx/Pggw/SoEEDhgwZQlJSEiaT6ZyPxMTEivNmz55Nu3bt8PPzo23btsycObPia4mJiVWen5SUxNy5c6lfvz4lJSWVar3xxhu57bbbzvs8LtWGDRvo1q0bfn5+9OzZk82bN5/zOFXV/f333wPndlnl5uZy1113Vby2AwcOZOvWrZWuuWjRInr27Imfnx8NGjRg5MiRFV9TF5jUeRGBMKE3+HsZXYmI1IYAb/hnH2gSYp/re3p68swzz/D6669z5MiRizrnm2++4dZbb2XChAns2LGDt956i6SkJKZPn37e81asWMHOnTv57rvvmD9/PgsWLGDy5MmVjpkzZw5eXl789NNPvPXWW4waNYr09PSKj/nz5+Pl5UX//v0BmDVrFk888QTTp09n586dPPPMMzz11FPMmTMHgIkTJ1Y6/4UXXiAgIICePXty0003YTabWbRoUcXjZ2VlsXjxYu64446avIw1UlBQwPDhw2nTpg3JyckkJiYyceLESse8+uqrleq+//77iYiIoG3btudcz2q1cu2115KRkcGSJUtITk6me/fuDBo0iOzsbAC++uorRo4cybXXXsvmzZtZsWIFPXteeMNdZ6Rfb1Kt6FD4v17w2noosxhdjYj8UX5etj9o7L39zQ033EDXrl2ZNGkS77777gWPnz59Oo8++ii33347ALGxsUydOpWHH36YSZMmVXuej48P7733HgEBAXTo0IEpU6bw0EMPMXXqVDw8bH/Xt2rVin//+9+VzvP39wdg//79jB8/nmeeeYYhQ4YAMHXqVF588cWK1owWLVpUhLLbb7+doKAggoJsTWfr1q2rCEcdO9oWUrvllluYPXs2N910EwAffvghTZs2ZcCAARf78tXYhx9+iNlsrvRaHDlyhHvvvbfimNDQUEJDbf/jP//8c/773/+yfPlyIiMjz7ned999R0pKCidO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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=3b45caeb-0ad5-4ab1-93f9-91ecb68a8d57">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Poka%C5%BC-wykres-ko%C5%82owy-%C5%9Bmiertelno%C5%9Bci-do-prze%C5%BCycia-dla-klasy-2-wed%C5%82ug-podzia%C5%82u-na-wiek.">Pokaż wykres kołowy śmiertelności do przeżycia dla <em>klasy 2</em> według podziału na wiek.<a class="anchor-link" href="#Poka%C5%BC-wykres-ko%C5%82owy-%C5%9Bmiertelno%C5%9Bci-do-prze%C5%BCycia-dla-klasy-2-wed%C5%82ug-podzia%C5%82u-na-wiek.">¶</a></h1>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=f3eab5a2-edb0-4fe6-afb6-8258b602fd7c">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [14]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Odfiltrowanie klasy 2</span>
<span class="n">class_2_df</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'pclass'</span><span class="p">]</span> <span class="o">==</span> <span class="mf">2.0</span><span class="p">]</span>

<span class="c1"># Podział na wiek</span>
<span class="n">class_2_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">=</span> <span class="n">class_2_df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">'child'</span> <span class="k">if</span> <span class="n">x</span> <span class="o">&lt;</span> <span class="mi">18</span> <span class="k">else</span> <span class="s1">'adult'</span><span class="p">)</span>

<span class="c1"># Przeliczenie śmiertelności i przeżycia po grupie wiekowej</span>
<span class="n">survived_counts</span> <span class="o">=</span> <span class="n">class_2_df</span><span class="p">[</span><span class="n">class_2_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_children</span> <span class="o">=</span> <span class="n">class_2_df</span><span class="p">[(</span><span class="n">class_2_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">0</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">class_2_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'child'</span><span class="p">)]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_adults</span> <span class="o">=</span> <span class="n">class_2_df</span><span class="p">[(</span><span class="n">class_2_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">0</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">class_2_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'adult'</span><span class="p">)]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>

<span class="c1"># Przygotowanie danych pod wykres kołowy</span>
<span class="n">total_passengers</span> <span class="o">=</span> <span class="n">class_2_df</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_total</span> <span class="o">=</span> <span class="n">not_survived_children</span> <span class="o">+</span> <span class="n">not_survived_adults</span>
<span class="n">survived_total</span> <span class="o">=</span> <span class="n">total_passengers</span> <span class="o">-</span> <span class="n">not_survived_total</span>

<span class="c1"># Zrobienie wykresu</span>
<span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Przeżyli'</span><span class="p">,</span> <span class="s1">'Nie przeżyli - dzieci'</span><span class="p">,</span> <span class="s1">'Nie przeżyli - Dorośli'</span><span class="p">]</span>
<span class="n">sizes</span> <span class="o">=</span> <span class="p">[</span><span class="n">survived_total</span><span class="p">,</span> <span class="n">not_survived_children</span><span class="p">,</span> <span class="n">not_survived_adults</span><span class="p">]</span>
<span class="n">colors</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'#66b3ff'</span><span class="p">,</span> <span class="s1">'#ff9999'</span><span class="p">,</span> <span class="s1">'#99ff99'</span><span class="p">]</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">()</span>
<span class="n">ax</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">sizes</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">colors</span><span class="o">=</span><span class="n">colors</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%1.1f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">startangle</span><span class="o">=</span><span class="mi">90</span><span class="p">)</span>
<span class="n">ax</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">'equal'</span><span class="p">)</span> 
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr" tabindex="0">
<pre>C:\Users\tmirk\AppData\Local\Temp\ipykernel_19720\2736117718.py:5: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  class_2_df['age_group'] = class_2_df['age'].apply(lambda x: 'child' if x &lt; 18 else 'adult')
</pre>
</div>
</div>
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[14]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(np.float64(-1.0999930334354537),
 np.float64(1.0999991011840888),
 np.float64(-1.0999994078064712),
 np.float64(1.0999999718003082))</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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iQoNDeXRRx+luLi4yW3CwsLo2LGjy56zuWpqalx2LFe9hpiYGJeNyi1btoy8vDx++ukn/va3v1FeXs6IESN48cUXW3XclnzdQkJCWLt2LZMnTz7tdh06dCA8vPmnjVSi3EglStwtLaiUiMIcALK7aWkD8S6uGokCmDRpEgkJCTz88MNNbtPYqbCVK1cydOhQQkNDSU1NZfHixdTV1TV5jJOnwRYvXkzHjh2Jjo5m3rx5Dj/wx48fz/z587ntttto3749kydPJjMz02HU5uRHRkaGfb9ly5bRp08fQkND6d27N88++6z9sYyMjEb3z8zM5MUXXyQ+Pp7qasfrZV5yySVcffXVp30drhAbG0tCQgIpKSmcf/75vPHGG8yePZv58+c7lNo333yTfv36ERISQkpKCn/9618djpOSksIDDzzAnDlziImJsc9rOtN+zz77LGlpaYSGhtKpUycuvfTSJrPqdJ4HS1CJEje7iJ32d4VmR2tpA/EurixRAQEBPPTQQzz99NMcOnSoWft89NFHXHnllSxYsIBt27bx/PPPk5mZyYMPPnja/VavXs327dv59NNPeeWVV1ixYgWLFy922Gb58uUEBgby9ddf8/zzzzNr1izy8vLsH6+88gqBgYGMHj0agKVLl3LXXXfx4IMPsn37dh566CHuueceli9fDsDChQsd9n/ssccIDw9n2LBhXHbZZVgsFt555x378x85coR3332Xa6+9tiVfRpe59dZbKSsr45NPPgFg48aN/OY3v+Hyyy9n69atZGRkcM899zQ4pfiXv/yF/v37s3HjRu65554z7rdhwwYWLFjAfffdx86dO/nwww8ZO3asy16Hljhwow4REGiGOqvRScQfBGClR2H93IijqTFUmlSixLvEEuvS41188cUMGjSIRYsW8a9//euM2z/44IP8z//8D9dccw0Aqamp3H///dxxxx0sWrSoyf2Cg4N54YUXCA8Pp1+/ftx3333cfvvt3H///ZjN9WMXPXv25M9//rPDfmFh9QuL7t27l/nz5/PQQw/ZTz/df//9/PWvf2XmzJkAdO/e3V7srrnmGiIjI4mMrP9Nfe3atfaC1b9//WWJrrjiCpYtW8Zll10GwH/+8x+6dOnC+PHjm/vlc6nevXsDkJWVBcDjjz/OxIkTueee+utFpqens23bNv7yl78wZ84c+34TJkxg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1DB37lzuvvtuDhw4wKJFi5g/fz5mc9Pz/JctW8azzz7LihUrMJvN5OfnA/WnzSIjI8nIyGDBggVER0czdepUqqur2bBhA8XFxdx2221kZGSwZs0aVq1aRWlpKaWlpUD9UgUnC8zs2bNZuHAhS5cu5cUXX2zpl63FrrjiCu666y771yIrK4vHHnvMYZt58+aRnZ3N6tWrKSwstN/frl07goMdLy0yadIkRo0axYwZM3j00Ufp1asXubm5vP/++8yYMYNhw4axaNEiJk6cSI8ePbj88supq6vjgw8+4I477mjz1ysiIr5F785rwv3333/G001Tpkzh3Xff5ZNPPmH48OGMHDmSxx9/3D6vqSkTJ04kLS2NsWPH8pvf/IYLL7zQYamCxnz++edYLBamT59OYmKi/eNk6bj++uv55z//SWZmJmeddRbjxo0jMzOT7t272/cvLS3l7LPPdtj/tddesz9HdHQ0l1xyCZGRkW2yGvkvRUZGsnLlSrZt28bgwYO56667ePTRRxu87ry8PPr27euQ+5tvvmlwPJPJxPvvv8/YsWO57rrrSE9P5/LLLycrK4tOnToB9ctH/N///R/vvPMOgwYNYsKECXz33Xdt/lpFRMT36Np5bjZnzhxKSkp4++23jY7SqMmTJ9OnTx+eeuopo6OIiIh4NJ3OEwCKior4+OOPWbNmDc8884zRcURERDyeSpQA9ZOyi4uL7XOJRERE5PR0Ok9ERETECZpYLiIiIuIElSgRERERJ6hEiYiIiDhBJUpERETECSpRIiIiIk5QiRIRERFxgkqUiIiIiBNUokREREScoBIlIiIi4gSVKBEREREnqESJiIiIOOH/A2rqd1mLf89gAAAAAElFTkSuQmCC"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=f33a576c-5313-4ee2-a70c-9b9fcc94c6cd">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Poka%C5%BC-wykres-ko%C5%82owy-%C5%9Bmiertelno%C5%9Bci-do-prze%C5%BCycia-dla-klasy-3-wed%C5%82ug-podzia%C5%82u-na-wiek.">Pokaż wykres kołowy śmiertelności do przeżycia dla <em>klasy 3</em> według podziału na wiek.<a class="anchor-link" href="#Poka%C5%BC-wykres-ko%C5%82owy-%C5%9Bmiertelno%C5%9Bci-do-prze%C5%BCycia-dla-klasy-3-wed%C5%82ug-podzia%C5%82u-na-wiek.">¶</a></h1>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=89914e77-31aa-4151-a664-8a234b7d763b">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [15]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Odfiltrowanie klasy 3</span>
<span class="n">class_3_df</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">[</span><span class="s1">'pclass'</span><span class="p">]</span> <span class="o">==</span> <span class="mf">3.0</span><span class="p">]</span>

<span class="c1"># Podział na wiek</span>
<span class="n">class_3_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">=</span> <span class="n">class_3_df</span><span class="p">[</span><span class="s1">'age'</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">'child'</span> <span class="k">if</span> <span class="n">x</span> <span class="o">&lt;</span> <span class="mi">18</span> <span class="k">else</span> <span class="s1">'adult'</span><span class="p">)</span>

<span class="c1"># Przeliczenie śmiertelności i przeżycia po grupie wiekowej</span>
<span class="n">survived_counts</span> <span class="o">=</span> <span class="n">class_3_df</span><span class="p">[</span><span class="n">class_3_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_children</span> <span class="o">=</span> <span class="n">class_3_df</span><span class="p">[(</span><span class="n">class_3_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">0</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">class_3_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'child'</span><span class="p">)]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_adults</span> <span class="o">=</span> <span class="n">class_3_df</span><span class="p">[(</span><span class="n">class_3_df</span><span class="p">[</span><span class="s1">'survived'</span><span class="p">]</span> <span class="o">==</span> <span class="mi">0</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">class_3_df</span><span class="p">[</span><span class="s1">'age_group'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'adult'</span><span class="p">)]</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>

<span class="c1"># Przygotowanie danych pod wykres kołowy</span>
<span class="n">total_passengers</span> <span class="o">=</span> <span class="n">class_3_df</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">not_survived_total</span> <span class="o">=</span> <span class="n">not_survived_children</span> <span class="o">+</span> <span class="n">not_survived_adults</span>
<span class="n">survived_total</span> <span class="o">=</span> <span class="n">total_passengers</span> <span class="o">-</span> <span class="n">not_survived_total</span>

<span class="c1"># Zrobienie wykresu</span>
<span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Przeżyli'</span><span class="p">,</span> <span class="s1">'Nie przeżyli - dzieci'</span><span class="p">,</span> <span class="s1">'Nie przeżyli - Dorośli'</span><span class="p">]</span>
<span class="n">sizes</span> <span class="o">=</span> <span class="p">[</span><span class="n">survived_total</span><span class="p">,</span> <span class="n">not_survived_children</span><span class="p">,</span> <span class="n">not_survived_adults</span><span class="p">]</span>
<span class="n">colors</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'#66b3ff'</span><span class="p">,</span> <span class="s1">'#ff9999'</span><span class="p">,</span> <span class="s1">'#99ff99'</span><span class="p">]</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">()</span>
<span class="n">ax</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">sizes</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">labels</span><span class="p">,</span> <span class="n">colors</span><span class="o">=</span><span class="n">colors</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="s1">'</span><span class="si">%1.1f%%</span><span class="s1">'</span><span class="p">,</span> <span class="n">startangle</span><span class="o">=</span><span class="mi">90</span><span class="p">)</span>
<span class="n">ax</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">'equal'</span><span class="p">)</span> 
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr" tabindex="0">
<pre>C:\Users\tmirk\AppData\Local\Temp\ipykernel_19720\2790980588.py:5: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  class_3_df['age_group'] = class_3_df['age'].apply(lambda x: 'child' if x &lt; 18 else 'adult')
</pre>
</div>
</div>
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[15]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(np.float64(-1.0999998381915566),
 np.float64(1.0999991064053791),
 np.float64(-1.0999987116082428),
 np.float64(1.0999999386480115))</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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GHFxcW55vqooLi5222O56zXExMS4bZQzJSWFo0ePsmXLFv75z3+Sn5/P5ZdfzuzZs2v0uFV530JCQli1ahXDhg276HaNGjUi/MxqDpWlsifu16bmv+WKWU7g21HR5FkLTEcR8Witae22KdyhQ4eSkJDA008/fcFtKpoC/eyzz7jssssIDQ2lVatWTJ8+ndILrPkJP01/Tp8+nbi4OKKjo7nrrrvKFZNBgwYxZcoU7r//fho2bMiwYcNITU0tNwp29mPatGmu/VJSUujYsSOhoaF06NCBV1991XXftGnTKtw/NTWV2bNn06BBA2w2W7msN954IxMmTLjo63CH2NhYEhISSEpK4pprruGjjz5i3LhxTJkypVz5/vjjj+ncuTMhISEkJSXxt7/9rdzjJCUl8eSTTzJx4kRiYmK44447KrXfq6++Stu2bQkNDSU+Pp5f//rXF8yqaVzxDE2bQoguGeTNfrgukYNhWaZjiHg8d0zhnhUQEMBTTz3Fyy+/zKFDhyq1z9dff8348eO599572bp1K2+88QapqanMnDnzovstWrSIbdu28e233zJnzhzmzp3L9OnTy20za9YsAgMDWbFiBW+88QZjx47l6NGjro85c+YQGBjIgAEDAHjzzTd5+OGHmTlzJtu2beOpp57i0UcfZdasWQBMnTq13P7PP/884eHh9O7dmzFjxmC32/n0009dz5+VlcX8+fO5/fbbq/I2us19991HXl4eCxYsAGD9+vXcdNNN3HzzzaSlpTFt2jQeffTR86aSn3vuObp06cL69et59NFHL7nfunXruPfee3niiSfYsWMHX331FcnJyW59LVpnT9zPaoVWrWDbNtNJpBoO9WjID40zTMcQ8XgNztzcafTo0fTo0YPHH3+ct95665Lbz5w5kz//+c/cdtttALRq1YoZM2bw4IMP8vjjj19wv+DgYN5++23Cw8Pp3LkzTzzxBA888AAzZszAai0bB2rTpg1//etfy+0XFhYGwJ49e5gyZQpPPfWUa9pxxowZ/O1vf+OGG24AoGXLlq4CettttxEZGUnkmWuDr1q1ylUEu3TpAsCtt95KSkoKY8aMAeDdd9+ladOmDBo0qLJvn1t16NABgPT0dABeeOEFhgwZwqOPPgpAu3bt2Lp1K8899xwTJ0507Td48GCmTp3q+nzcuHEX3e/AgQNEREQwYsQIoqKiaNGiBT3PuUa6O2hkT2pHx46mE0g15MeFs6hPHk6Llt8UuZSO1M7PuWeffZZZs2axdevWS267fv16nnjiCVeRioyM5I477uDo0aOcPn36gvt179693HFf/fv3Jz8/n4MHD7q+1rt37wr3PXXqFCNGjODaa6/lgQceACAzM5ODBw8yadKkclmefPJJ9uzZU27/AwcOMGrUKB588EFXsQO44447+Oabbzh8+DBQNiV89sSV6jg3x+9+97sq7392GeKzz79t2zbXKOZZAwYMYNeuXdjPWV/25+/bpfYbNmwYLVq0oFWrVvzmN7/h3Xffveh/u+rQyJ7UjoYNoVEjyNSZnN7CHmhhwXUh2CwXPjhcRMoEEURb2tbKYycnJzN8+HD+8pe/lBsxqojD4WD69Omu0bRzhYaGVvm5zy1WERER591vt9sZO3Ys0dHR5daCczgcQNlU7uWXX15un4CAANffCwoKGDlyJFddddV5I489e/ake/fuzJ49m+HDh5OWlsZnn31W5ddw1saNG11/j46OrvL+287MTrVs2RIoK38/L54VXZfi5+/bpfaLiorihx9+YMmSJXzzzTc89thjTJs2jbVr17rtBBSVPak9nTrB0qWmU0glfT8qnswgTd+KVEZb2hJE7S0z9cwzz9CjRw/atWt30e169erFjh07aFPFE+M2bdpEYWGha1p21apVREZG0rRp04vud99995GWlsbatWvLlcn4+HiaNGnC3r17GTduXIX7Op1Oxo8fj9VqZdasWRWO2E2ePJm///3vHD58mKFDh9KsBgv1V/U9+bkXX3yR6Ohohg4dCkCnTp1Yvnx5uW1WrlxJu3btyhXan6vMfoGBgQwdOpShQ4fy+OOPExsby+LFiyss8dWhsie1p3VrWLUKfnZ2lXieXQPi2VpfRU+ksjrRqVYfv2vXrowbN46XX375ots99thjjBgxgmbNmjFmzBisViubN28mLS2NJ5988oL7FRcXM2nSJB555BH279/P448/zpQpU1zH61UkJSWFV199lblz52K1WsnIKPuZcXaqdNq0adx7771ER0dz7bXXYrPZWLduHTk5Odx///1MmzaNxYsXs3DhQnJzc8nNzQXKllA5WzrHjRvH1KlTefPNN2u87ElVnDx5koyMDGw2Gzt37uSNN95g3rx5zJ492zW69qc//Yk+ffowY8YM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+4WdOcNzz549TJkyhaeeeophw4YBMGPGDP72t7+5RqlatmzpKqC33XYbkZGRREZGArBq1SpXEezSpey3vVtvvZWUlBTGjBkDwLvvvkvTpk0ZNGhQZd++Knv33Xex2+3l3otDhw5x9913u7aJiYkhJqbsgOJPPvmE119/nYULF5KQkHDe43377bekpaVx/PhxQkJCAHj++eeZN28eH330EXfeeSczZ87k5ptvLleuu3fvXmuvkejositrrFtXe8/hg7JaxbC8vc68FampBBJoTWvTMURqRbXKHsCzzz7L4MGD+dOf/nTJbdevX8/atWvLjeTZ7XaKioo4ffr0BY/96t69e7n7+vfvT35+PgcPHqRFixYAFxxtOnXqFCNGjODaa6/lgQceACAzM5ODBw8yadIk7rjjDte2paWlrqJ01oEDBxg1ahQPPvigq9gB3HHHHfTp04fDhw/TpEkTUlJSXFOo1XG2WAKMHz+e119//bxttm3bVuF7UZENGzYwYcIE/vnPf3LllVdWuM369evJz8+nQYMG5b5eWFjInj17ANi4cWO596hOdO8OO3dCrq7jWhm2yCAWDrZjt9hNRxHxagEEkEwyFp3dJD6q2mUvOTmZ4cOH85e//IWJEydedFuHw8H06dPLHfN1Vmho1Q+EPbdYRUREnHe/3W5n7NixREdH8+abb5bLAWVTuZf/7KSAgHOmEAsKChg5ciRXXXXVeSOPPXv2pHv37syePZvhw4eTlpbGZ599VuXXcNa5S6dER0dXuI3T6azUY2VkZDBy5EgmTZrEpEmTLridw+EgMTHRdTzfuc4eaxlmYv27gAAYMAC+/LLun9vLOIElo2LJtWaajiLi9XrSk1hiTccQqTXVLnsAzzzzDD169KBdu3YX3a5Xr17s2LGDNm3aVOnxN23aRGFhoat4rFq1isjISJo2bXrR/e677z7S0tJYu3ZtuTIZHx9PkyZN2Lt3L+PGjatwX6fTyfjx47FarcyaNavCEbvJkyfz97//ncOHDzN06FCaNav+tRMr85506tSJd95557z34lxFRUX86le/okOHDrzwwgsXfbxevXqRkZFBYGAgSUlJFW7TrVs3Fi1aVKvHIlaoWTNo2RL27avb5/UyG69NZH+41tMTqal61KMHPUzHEKlVNSp7Xbt2Zdy4cbz88ssX3e6xxx5jxIgRNGvWjDFj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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=f8c577d6-932b-46ca-ab30-12482f6a8101">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="WNIOSKI:">WNIOSKI:<a class="anchor-link" href="#WNIOSKI:">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=34b15318-f52f-4e72-8acd-e17201fa96b9">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Niestety największa śmiertelnośc była w klasie 3 potem w klasie 2 a najmniejsza w klasie 1.
Równolegle, dzieci miały największą szanse przeżycia w klasie 1.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=856dfb21-a006-4a75-8320-28a2cf222381">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>To potwierdza, że klasa 1 była klasą najbardziej uprzywilejowaną, jednak macierz korelacji ceny biletu do przeżywalności tego nie potwierdza:</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=ad94baa9-1b71-4881-9aa8-ffe640cc3266">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [16]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Przeliczenie macierzy</span>
<span class="n">correlation_matrix</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">'pclass'</span><span class="p">,</span> <span class="s1">'fare'</span><span class="p">,</span> <span class="s1">'survived'</span><span class="p">]]</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span>

<span class="c1"># Wyrysowanie macierzy</span>
<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">heatmap</span><span class="p">(</span><span class="n">correlation_matrix</span><span class="p">,</span> <span class="n">annot</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">cmap</span><span class="o">=</span><span class="s1">'coolwarm'</span><span class="p">,</span> <span class="n">fmt</span><span class="o">=</span><span class="s2">".2f"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Correlation Matrix of Fare by Class to Survival'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[16]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>Text(0.5, 1.0, 'Correlation Matrix of Fare by Class to Survival')</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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HxEREekkiQErfepgpY+IiIhID7DSR0RERDpJYsjalTp4t4iIiIj0ACt9REREpJO4elc9rPQRERER6QFW+oiIiEgncfWuepj0ERERkU7i8K56OLxLREREpAdY6SMiIiKdxO/eVQ8rfURERER6gJU+IiIi0kkSA9au1MG7RURERKQHWOkjIiIincQtW9TDSh8RERGRHmClj4iIiHQS9+lTD5M+IiIi0kkc3lUPh3eJiIiI9AArfURERKSTuGWLeni3iIiIiPQAK31ERESkkzinTz2s9BERERHpAVb6iIiISCdxyxb1sNJHREREpAdY6SMiIiKdxDl96mHSR0RERDqJW7aoh3eLiIiISA+w0kdEREQ6icO76mGlj4iIiEgPsNJHREREOomVPvWw0kdERESkB1jpIyIiIp3ESp96WOkjIiIi0gOs9BEREZFO4j596mHSR0RERDqJ372rHqbIRERERJW0cuVKeHp6wtTUFD4+Pjhy5Ei5/Tdt2oTmzZvD3Nwcrq6uGDFiBDIyMrQaI5M+IiIi0kkSA4nWHurYsmULJk+ejI8//hixsbHo0KEDunXrhuTkZJX9jx49imHDhmHUqFH4559/sHXrVpw+fRqjR4+uittSJiZ9RERERJWwePFijBo1CqNHj0ajRo0QEREBNzc3rFq1SmX/EydOwMPDAxMnToSnpyfat2+PsWPH4syZM1qNk0kfERER6SSJgYHWHvn5+bh//77CIz8/XymGgoICnD17FoGBgQrtgYGBOHbsmMq4/f39cevWLezZswdCCNy9exc///wz3nrrLa3cpxIaJX03b97ErVu35D+fOnUKkydPRmRkZJUFRkRERFRdwsPDYW1trfAIDw9X6peeno7i4mI4OzsrtDs7OyM1NVXluf39/bFp0yYMHDgQJiYmcHFxgY2NDZYvX66VaymhUdIXFBSEgwcPAgBSU1PRpUsXnDp1Ch999BHmzZtXpQESERERqaLNOX1hYWHIyclReISFhZUdi0RxHqAQQqmtRHx8PCZOnIhPP/0UZ8+eRXR0NBITEzFu3LgqvT+labRly8WLF9G6dWsAwE8//YQmTZrgr7/+wr59+zBu3Dh8+umnVRokERER0fMklUohlUqf2c/BwQGGhoZKVb20tDSl6l+J8PBwtGvXDtOnTwcANGvWDBYWFujQoQPmz58PV1fXyl+AChpV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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=320a54a1-8018-4b45-aa9a-eeb3c6441320">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Porównanie ceny biletu do przeżycia nie wykazuje korelacji, ale ceny biletu do klasy podróży już pokazują lekką korelację.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=88ec2dea-b274-4d47-ac2c-1c2ff5ce1cf5">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Gdy rozbije się tę macierz na poszczególne klasy wtedy lepiej widać zależność ceny od śmiertelności jednak wykresy kołowe pokazują więcej.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=3ead7076-c9f6-4e10-829a-39937f0c0625">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [17]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Filter out rows with missing values in 'fare', 'pclass', or 'survived'</span>
<span class="n">df_filtered</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">dropna</span><span class="p">(</span><span class="n">subset</span><span class="o">=</span><span class="p">[</span><span class="s1">'fare'</span><span class="p">,</span> <span class="s1">'pclass'</span><span class="p">,</span> <span class="s1">'survived'</span><span class="p">])</span>

<span class="c1"># Create a correlation matrix for each class</span>
<span class="n">correlation_matrices</span> <span class="o">=</span> <span class="p">{}</span>
<span class="k">for</span> <span class="n">pclass</span> <span class="ow">in</span> <span class="n">df_filtered</span><span class="p">[</span><span class="s1">'pclass'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">():</span>
    <span class="n">class_data</span> <span class="o">=</span> <span class="n">df_filtered</span><span class="p">[</span><span class="n">df_filtered</span><span class="p">[</span><span class="s1">'pclass'</span><span class="p">]</span> <span class="o">==</span> <span class="n">pclass</span><span class="p">]</span>
    <span class="n">correlation_matrix</span> <span class="o">=</span> <span class="n">class_data</span><span class="p">[[</span><span class="s1">'fare'</span><span class="p">,</span> <span class="s1">'survived'</span><span class="p">]]</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span>
    <span class="n">correlation_matrices</span><span class="p">[</span><span class="n">pclass</span><span class="p">]</span> <span class="o">=</span> <span class="n">correlation_matrix</span>

<span class="c1"># Plot the correlation matrices</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axes</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">correlation_matrices</span><span class="p">),</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span> <span class="mi">5</span><span class="p">))</span>
<span class="n">fig</span><span class="o">.</span><span class="n">suptitle</span><span class="p">(</span><span class="s1">'Korelacja ceny biletu do przeżywalności według klas'</span><span class="p">)</span>

<span class="k">for</span> <span class="n">ax</span><span class="p">,</span> <span class="p">(</span><span class="n">pclass</span><span class="p">,</span> <span class="n">corr_matrix</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">zip</span><span class="p">(</span><span class="n">axes</span><span class="p">,</span> <span class="n">correlation_matrices</span><span class="o">.</span><span class="n">items</span><span class="p">()):</span>
    <span class="n">sns</span><span class="o">.</span><span class="n">heatmap</span><span class="p">(</span><span class="n">corr_matrix</span><span class="p">,</span> <span class="n">annot</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">cmap</span><span class="o">=</span><span class="s1">'coolwarm'</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">ax</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_title</span><span class="p">(</span><span class="sa">f</span><span class="s1">'Class </span><span class="si">{</span><span class="nb">int</span><span class="p">(</span><span class="n">pclass</span><span class="p">)</span><span class="si">}</span><span class="s1">'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABLYAAAHeCAYAAACG+YIFAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjEwLjAsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvlHJYcgAAAAlwSFlzAAAPYQAAD2EBqD+naQAAixxJREFUeJzs3XlYVdX+x/HPYTogCioozoiaQ1FpUIpDaiqlZmWDljdtkNIwTWmSazndbvzqlmG3sEzNLK95M20klbIc0nIIS8MmJ9JAAucJBPbvD+HcjqAynAHY79fz7OeJxdp7r30AP53vWWtvi2EYhgAAAAAAAIBqxsPdAwAAAAAAAAAqgsIWAAAAAAAAqiUKWwAAAAAAAKiWKGwBAAAAAACgWqKwBQAAAAAAgGqJwhYAAAAAAACqJQpbAAAAAAAAqJYobAEAAAAAAKBaorAFAAAAAACAaonCFgAAAKq1rKwsNWnSRGPGjHH3UAAAgItR2AIAE5g/f74sFos2b95s156dna3IyEjVrl1bKSkpLh3T1KlTZbFYnHb84mves2eP085R1X311VeyWCxasmTJRfuW9vPo1auXevXqVaFzJyUlaf78+RXatyKc/ftUlbRs2VL33nuvu4dxXsW/d1999ZVLzldYWKi//e1v6tKli/7973+Xe3+LxaKpU6c6fmAOUNpree+996ply5ZuGU+vXr0UHh5+0X5V/XcUAFCzeLl7AAAA99i3b5/69eunAwcO6PPPP1eXLl3cPSSHGjhwoDZs2KDGjRu7eyjVQkxMjG644QaHHS8pKUnBwcG8uXWCZcuWKSAgwN3DqDL+8Y9/6OTJk/r444/l4VH+z2w3bNigZs2aOWFkAADAFShsAYAJ/frrr+rbt6/OnDmj1atX6/LLL6/0MU+dOiVfX98qM2umQYMGatCggbuHUW00a9aMN/cOYhiGTp8+LT8/P6ccv1OnTk45bnU1ZcoUTZkypcL717SiPgAAZsNSRAAwma1bt6p79+7y8vLSunXrShS11q1bpz59+qhOnTqqVauWunbtqk8//dSuT/Eyv5UrV+r+++9XgwYNVKtWLeXm5kqSFi9erKioKPn7+6t27dq6/vrrlZqaetGxLV68WNHR0WrcuLH8/PzUoUMHTZw4USdOnCjR99tvv9WgQYMUFBQkX19ftW7dWuPHjy8xxr8uRUxJSdHNN9+sZs2aydfXV23atNGoUaOUnZ1dptfu8OHDevTRR9WqVStZrVY1bNhQAwYM0E8//WTrk5eXp2eeeUbt27eX1WpVgwYNdN999+nPP/+0O1bLli114403avny5brqqqvk5+en9u3ba968ebY+e/bskZeXlxISEkqMZc2aNbJYLHrvvfcuOu7Tp08rLi5OjRo1kp+fn3r27Fni51HWpXxlub6WLVvqxx9/1OrVq2WxWGSxWGxLp863RLQ8y9c+/fRTdezYUVarVWFhYXrhhRfOe93x8fEKCwuTj4+PmjZtqjFjxujw4cMXPce9996r2rVr68cff1SfPn3k7++vBg0a6OGHH9bJkyft+losFj388MN67bXX1KFDB1mtVr311lu69957bdd/7vbXpW9Hjx7VY489ZjfO8ePH2/3eF/98StvuvfdeGYahSy65RNdff32Jazl+/LgCAwM1ZswYGYahkJAQu3tRFRQUqF69evLw8NCBAwds7TNmzJCXl5ft9dq8ebPuvPNOtWzZUn5+fmrZsqXuuusu7d27t8yv52+//aYBAwaodu3aat68uR599FHbvxvFDh48qNjYWDVt2lQ+Pj5q1aqVJk2aVKLfe++9p86dOyswMFC1atVSq1atdP/999v1KcvfbFmWIl599dUaOHCgXdvll18ui8WiTZs22dqWLl0qi8Wibdu22dp+/fVXDRs2TA0bNpTValWHDh306quvljjHTz/9pBtuuEG1atVScHCwRo8erWPHjl1wXNLZfycsFkupS39Lu7YPP/xQV1xxhaxWq1q1aqWZM2dWainvsmXLVKtWLcXExCg/P7/UPqdPn9ajjz6qjh07KjAwUPXr11dUVJQ+/PDDEn3L8nMFAOCvmLEFACaybt06TZ06Vc2bN9fKlStLLNNbvXq1+vXrpyuuuEJz586V1WpVUlKSBg0apEWLFmno0KF2/e+//34NHDhQb7/9tk6cOCFvb289++yzeuqpp3TffffpqaeeUl5env71r3+pR48e2rhxoy699NLzju/XX3/VgAEDNH78ePn7++unn37Sc889p40bN2rVqlW2fitWrNCgQYPUoUMHzZgxQy1atNCePXu0cuXKC17/zp07FRUVpZiYGAUGBmrPnj2aMWOGunfvrm3btsnb2/u8+x47dkzdu3fXnj179OSTT6pz5846fvy41qxZo4yMDLVv316FhYW6+eabtXbtWj3xxBPq2rWr9u7dqylTpqhXr17avHmz3Sye77//Xo8++qgmTpyokJAQzZkzRyNHjlSbNm107bXXqmXLlrrpppv02muv6YknnpCnp6dt31deeUVNmjTR4MGDL3jNkvT3v/9dV111lebMmaMjR45o6tSp6tWrl1JTU9WqVauL7l+srNe3bNky3X777QoMDFRSUpIkyWq1lvk8F/LFF1/o5ptvVlRUlN59910VFBTo+eeftyvISGdnTd1yyy364osvFB8frx49euiHH37QlClTtGHDBm3YsOGiYzpz5owGDBigUaNGaeLEiVq/fr2eeeYZ7d27Vx9//LFd3w8++EBr167V5MmT1ahRIzVs2FD9+vXT6NGj7fq9+uqreuedd2x/BydPnlTPnj21b98+/f3vf9cVV1yhH3/8UZMnT9a2bdv0+eefy2KxlLpU9N1339XMmTN12WWXyWKxaOzYsRo/frx+/fVXXXLJJbZ+CxYs0NGjRzVmzBhZLBZdd911+vzzz23f37x5sw4fPiw/Pz998cUXGjZsmCTp888/V0REhOrWrSvpbAGlXbt2uvPOO1W/fn1lZGRo1qxZuvrqq5WWlqbg4OCLvp433XSTRo4cqUcffVRr1qzRP/7xDwUGBmry5MmSzhZAevfurZ07d2ratGm64oortHbtWiUkJGjr1q22IvuGDRs0dOhQDR06VFOnTpWvr6/27t1r9+9EWf5my6pv37565ZVXdObMGXl7e+vAgQPavn27/Pz8lJKSoquvvtr2moWEhNg+MEhLS1PXrl3VokULvfjii2rUqJFWrFihcePGKTs72zbT7MCBA+rZs6e8vb2VlJSkkJAQLVy4UA8//HCp4zl+/Li6d++uZ555plz321q+fLluvfVWXXvttVq8eLHy8/P1wgsvlPj7KauXXnpJjz/+uKZOnaqnnnrqvP1yc3N18OBBPfbYY2ratKny8vL0+eef69Zbb9Wbb76pESNGSCrbzxUAgBIMAECN9+abbxqSDElGYGCgkZWVVWq/Ll26GA0bNjSOHTtma8vPzzfCw8ONZs2aGYWFhXbHGzFihN3+6enphpeXlzF27Fi79mPHjhmNGjUyhgwZYmubMmWKcaEYKiwsNM6cOWOsXr3akGR8//33tu+1bt3aaN26tXHq1KmLXvPu3bsvePy9e/cakowPP/zwvMcyDMOYPn26IclISUk5b59FixYZkoz333/frn3Tpk2GJCMpKcnWFhoaavj6+hp79+61tZ06dcqoX7++MWrUKFvbl19+aUgyli1bZmvbv3+/4eXlZUybNu2CYy7e96qrrrL97AzDMPbs2WN4e3sbMTExtrbSfh49e/Y0evbsWaHru+yyy+z2LXa+n0vxWL/88ssLXlPnzp2NJk2a2P3sjx49atSvX99u/MuXLzckGc8//7zd/osXLzYkGbNnz77gee655x5DkjFz5ky79n/+85+GJGPdunW2tuK/q4MHD17wmP/9738Ni8Vi/P3vf7e1JSQkGB4eHsamTZvs+i5ZssSQZCQnJ5d6rC+//NLw8fEx7r77btvP9ujRo0adOnWMRx55xK7vpZdeavTu3dv29Zw5cwxJRnp6umEYhvHMM88Y7du3N2666SbjvvvuMwzDMPLy8gx/f3+7sZ4rPz/fOH78uOHv72/3OpX2syx+Pf/73//aHWPAgAFGu3btbF+/9tprpfZ77rnnDEnGypUrDcMwjBdeeMGQZBw+fPi84yvL36xhnP35TZky5YJ9Pv/8c0OSsWbNGsMwDOOdd94x6tSpY8TGxtq9tpdccokxbNgw29fXX3+90axZM+PIkSN2x3v44YcNX19f2+/Mk08+aVgsFmPr1q12/fr162f3WhYUFBj9+/c3vL29jRdffNEoKCgwdu/ebUgy3nzzzYte29VXX200b97cyM3NtbUdO3bMCAoKuuC/x8V69uxpXHbZZUZBQYHx8MMPGz4+PsY777xTol9oaKhxzz33nPc4+fn5xpkzZ4yRI0canTp1srWX5ecKAMC5WIoIACZy00036ciRIxo/frwKCgrsvnfixAl9++23uv3221W7dm1bu6enp4YPH659+/bp559/ttvntttus/t6xYoVys/P14gRI5Sfn2/bfH191bNnz4suM9u1a5eGDRumRo0aydPTU97e3urZs6ckaceOHZKkX375RTt37tTIkSPl6+tbruvPysrS6NGj1bx5c3l5ecnb21uhoaF2xz+fzz77TG3btlXfvn3P2+eTTz5R3bp1NWjQILvr79ixoxo1alTi+jt27KgWLVrYvvb19VXbtm3tlnb16tVLV155pd3Spddee00Wi0UPPvhgma572LBhdsuMQkND1bVrV3355Zdl2r+i1+doJ06c0KZNm3Trrbfa/ezr1KmjQYMG2fUtnuFx7s3r77jjDvn7++uLL74o0zn/9re/2X1dPJvp3NfuuuuuU7169c57nNWrV2v48OG6++679c9//tPW/sknnyg8PFwdO3a0e02vv/768y7N3L59u2655RZde+21mjdvnu1nW6dOHd13332aP3++bRnjqlWrlJaWZjfzp/h3uHjWVkpKivr166e+ffvano66YcMGnThxwu73/fjx43ryySfVpk0beXl5ycvLS7Vr19aJEycu+vcjnV0Wd+7P6YorrrD7fV+1apX8/f11++232/Ur/jkW/9yKZ0gNGTJE//3vf7V///4S5yvL32xZdevWTb6+vnavWa9evXTDDTdo/fr1OnnypH7//Xfb/Quls7PPvvjiCw0ePFi1atWy+/kOGDBAp0+f1jfffCPp7O/TZZddpiuvvNLuvMW/b9LZJas9e/bUypUr1aRJE8XFxZXrZvknTpzQ5s2bdcstt8jHx8fWXrt27RI/lws5ffq0brnlFi1cuFArV64s8TdyPu+99566deum2rVr2/79nTt3rt3vTll+rgAAnIvCFgCYyNNPP63JkyfrP//5j+6++2674tahQ4dkGEapTxFs0qSJJCknJ8eu/dy+xctZrr76anl7e9ttixcvvuC9rI4fP64ePXro22+/1TPPPKOvvvpKmzZt0tKlSyWdvTm9JNu9nMp7o/PCwkJFR0dr6dKleuKJJ/TFF19o48aNtjeWxcc/nz///POi5zxw4IAOHz4sHx+fEtefmZlZ4vqDgoJKHMNqtZYYy7hx4/TFF1/o559/1pkzZ/TGG2/o9ttvV6NGjcpy6aX2a9SoUYmf58WU9/oc7dChQyosLDzv9fxVTk6OvLy8SjxAwGKxlPnavby8SvyMis9zsb+Fv/rxxx91yy23qEePHpo7d67d9w4cOKAffvihxOtZp04dGYZR4jXdt2+f+vfvr7CwMC1durTE8tmxY8fq2LFjWrhwoaSzS1abNWumm2++2dYnNDRUrVu31ueff66TJ09qw4YNtsJWcQH7888/l5+fn7p27Wrbb9iwYXrllVcUExOjFStWaOPGjdq0aZMaNGhw0b8fSapVq1aJYrTVatXp06dtX+fk5KhRo0Yl7vfUsGFDeXl52V73a6+9Vh988IGtkN6sWTOFh4dr0aJFtn3K8jdbVr6+vurWrZutsPXFF1+oX79+6tWrlwoKCrR27VpbUbC4sJWTk6P8/Hz9+9//LvHzHTBggCTZfr7F132uv7YFBAQoLi7OrthVHsX/xoeEhJT4Xmlt55OVlaUVK1YoKirK7vfjQpYuXaohQ4aoadOmeuedd7RhwwZt2rRJ999/v93Pvyw/VwAAzsU9tgDAZKZNmyaLxaJp06apsLBQCxculJeXl+3m0RkZGSX2+eOPPySpxD10zn3zWfz9JUuW2GZCldWqVav0xx9/6KuvvrLN0pJU4kbfxYWKffv2lev427dv1/fff6/58+frnnvusbX/9ttvZdq/QYMGFz1ncHCwgoKCtHz58lK/X6dOnbIP+C+GDRumJ598Uq+++qq6dOmizMxMu5t/X0xmZmapbaUV1i7EEddXXNg490bgZSmK1atXTxaL5bzX81dBQUHKz8/Xn3/+aVfcMgxDmZmZtpkhF5Kfn6+cnBy716n4POe+due78fa+fft0ww03qEWLFnr//fdLFKKCg4Pl5+dn99CAc79f7MiRIxowYIA8PT2VnJxc6uvdpk0b9e/fX6+++qr69++vjz76SNOmTbO7P5sk9enTRx9++KFWr16twsJC9erVS3Xq1FGTJk2UkpKizz//XD169LDdh+zIkSP65JNPNGXKFE2cONF2nOJ7JzlKUFCQvv32WxmGYfeaZmVlKT8/3+71uPnmm3XzzTcrNzdX33zzjRISEjRs2DC1bNlSUVFRZfqbLY8+ffpo8uTJ2rhxo/bt26d+/fqpTp06uvrqq5WSkqI//vhDbdu2VfPmzSWd/X0tnvF6vr/XsLAw23WX5fd68ODBJW64fr6/qXOLr8V/P6XdT6u0c59PixYtNGPGDA0ePFi33nqr3nvvvYvOnn3nnXcUFhamxYsX2/1czx2zdPGfKwAA52LGFgCY0NSpUzVt2jT997//1bBhw5Sfny9/f3917txZS5cutZt9UVhYqHfeeUfNmjVT27ZtL3jc66+/Xl5eXtq5c6ciIyNL3c6n+M3OuTf0fv311+2+btu2rVq3bq158+aV+qaossc/n/79++uXX3654E2Mb7zxRuXk5KigoKDUa2/Xrl2Zx/tXvr6+evDBB/XWW29pxowZ6tixo7p161bm/RctWiTDMGxf7927V+vXr1evXr3KNY7yXF9pM88k2W50/cMPP9i1f/TRRxc9v7+/v6655hotXbrUbpbHsWPHStzMvU+fPpLOvqH+q/fff18nTpywff9iimc+FfvPf/4jSWV67Y4cOaL+/fvLYrEoOTlZAQEBJfrceOON2rlzp4KCgkp9TYtfr7y8PA0ePFj79u3TZ599dsEZYo888oh++OEH3XPPPfL09NQDDzxQok/fvn114MABJSYmqkuXLrYiWZ8+fbRs2TJt2rTJbgmfxWKRYRgl/n7mzJlTYllzZfTp00fHjx/XBx98YNe+YMEC2/fPZbVa1bNnTz333HOSZHviZ1n+Zsujb9++ys/P19NPP61mzZrZbj7ft29fff7551q1apXda1arVi317t1bqampuuKKK0r9+RYXSHv37q0ff/xR33//vd05i3/fLiQkJES+vr4l/qbOLYD5+/srMjJSH3zwgfLy8mztx48f1yeffFKu1yI6OlorVqzQmjVrdOONN5b65Nq/slgs8vHxsStqZWZmlvpUxGLn+7kCAHAuZmwBgElNnjxZHh4eevrpp2UYhhYtWqSEhAT169dPvXv31mOPPSYfHx8lJSVp+/btWrRo0UUfB9+yZUtNnz5dkyZN0q5du3TDDTeoXr16OnDggDZu3Ch/f39Nmzat1H27du2qevXqafTo0ZoyZYq8vb21cOHCEm/0pLNPlhs0aJC6dOmiCRMmqEWLFkpPT9eKFStKFCKKtW/fXq1bt9bEiRNlGIbq16+vjz/+2LZ86GLGjx+vxYsX6+abb9bEiRN1zTXX6NSpU1q9erVuvPFG9e7dW3feeacWLlyoAQMG6JFHHtE111wjb29v7du3T19++aVuvvnmMj3FsDSxsbF6/vnntWXLFs2ZM6dc+2ZlZWnw4MF64IEHdOTIEU2ZMkW+vr6Kj48v13HKc32XX3653n33XS1evFitWrWSr6+vLr/8cl199dVq166dHnvsMeXn56tevXpatmyZ1q1bV6Yx/OMf/9ANN9ygfv366dFHH1VBQYGee+45+fv7280c6tevn66//no9+eSTOnr0qLp162Z7KmKnTp00fPjwi57Lx8dHL774oo4fP66rr77a9lTE/v37q3v37hfdf9iwYUpLS9Ps2bP1+++/6/fff7d9r1mzZmrWrJnGjx+v999/X9dee60mTJigK664QoWFhUpPT9fKlSv16KOPqnPnzpowYYK+/PJL/etf/9KRI0dsS2ils7MJW7dubXftl156qb788kvdfffdatiwYYmxXXfddbJYLFq5cqXd32Tfvn1tMxr/WqQJCAjQtddeq3/9618KDg5Wy5YttXr1as2dO9f21ERHGDFihF599VXdc8892rNnjy6//HKtW7dOzz77rAYMGGAb0+TJk7Vv3z716dNHzZo10+HDhzVz5ky7+/KV5W+2PCIiIlSvXj2tXLlS9913n629b9+++sc//mH777+aOXOmunfvrh49euihhx5Sy5YtdezYMf3222/6+OOPbUW38ePHa968eRo4cKCeeeYZ21MRf/rpp4uOy2Kx6O6779a8efPUunVrXXnlldq4cWOpRbHp06dr4MCBuv766/XII4+ooKBA//rXv1S7du1yz7zr3r27vvjiC91www2Kjo5WcnKyAgMDS+174403aunSpYqNjdXtt9+u33//Xf/4xz/UuHFj/frrr7Z+Zfm5AgBQgttuWw8AcJniJ9Gd++Q1w/jfU95uvfVWIy8vz1i7dq1x3XXXGf7+/oafn5/RpUsX4+OPPy7z8QzDMD744AOjd+/eRkBAgGG1Wo3Q0FDj9ttvNz7//HNbn9Kewrd+/XojKirKqFWrltGgQQMjJibG+O6770p94teGDRuM/v37G4GBgYbVajVat25tTJgwocQY9+zZY2tLS0sz+vXrZ9SpU8eoV6+ecccddxjp6elleiqaYRjGoUOHjEceecRo0aKF4e3tbTRs2NAYOHCg8dNPP9n6nDlzxnjhhReMK6+80vD19TVq165ttG/f3hg1apTx66+/2vqFhoYaAwcOLHGOc59E+Fe9evUy6tevb5w8efKiYzWM/z2d7u233zbGjRtnNGjQwLBarUaPHj2MzZs32/Uty1MRy3N9e/bsMaKjo406deoYkozQ0FDb93755RcjOjraCAgIMBo0aGCMHTvW+PTTT8v0VETDMIyPPvrIuOKKKwwfHx+jRYsWxv/93/+VOv5Tp04ZTz75pBEaGmp4e3sbjRs3Nh566CHj0KFDFz3HPffcY/j7+xs//PCD0atXL8PPz8+oX7++8dBDDxnHjx+36yvJGDNmTIljhIaG2p5Geu7219+348ePG0899ZTRrl07w8fHxwgMDDQuv/xyY8KECUZmZqZhGGd/Fuc7VmlPn5s6daohyfjmm2/Oe42dOnUyJBlff/21rW3//v2GJCMoKMju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iyTpm2++0c6dO/X+++87dIAA4CpmvNFiVUXOAKipyJqqgZwBUFOZMWcqNGNrwIAB+uWXX3TTTTfp4MGDysnJ0c0336xffvlFAwYMcPQYAcAlWIpYdZAzAGoqcqZqIGcA1FRmzJkKzdiSzk7fffbZZx05FgAAbMgZAIAzkTMAUDNUaMaWJK1du1Z33323unbtqv3790uS3n77ba1bt85hgwMAV2LGVtVCzgCoiciZqoOcAVATmTFnKlTYev/993X99dfLz89P3333nXJzcyVJx44d41MPANVWoeHYrbySkpIUFhYmX19fRUREaO3atWXa7+uvv5aXl5c6duxY/pNWUeQMgJrKnTmD/yFnANRUZsyZChW2nnnmGb322mt644035O3tbWvv2rWrvvvuO4cNDgDMYvHixRo/frwmTZqk1NRU9ejRQ/3791d6evoF9zty5IhGjBihPn36uGikrkHOAACciZwBgJqjQoWtn3/+Wddee22J9oCAAB0+fLiyYwIAt3D0UsTc3FwdPXrUbiv+RPhcM2bM0MiRIxUTE6MOHTooMTFRzZs316xZsy445lGjRmnYsGGKiopyxkviNuQMgJrKjEtEqiJyBkBNZcacqVBhq3Hjxvrtt99KtK9bt06tWrWq9KAAwB0KCx27JSQkKDAw0G5LSEgocd68vDxt2bJF0dHRdu3R0dFav379ecf75ptvaufOnZoyZYrDXwt3I2cA1FSOzBlUHDkDoKYyY85U6KmIo0aN0iOPPKJ58+bJYrHojz/+0IYNG/TYY49p8uTJjh4jAFRL8fHxiouLs2uzWq0l+mVnZ6ugoEAhISF27SEhIcrMzCz12L/++qsmTpyotWvXysurwg+4rbLIGQCAM5EzAFBzVOjd0BNPPKEjR46od+/eOn36tK699lpZrVY99thjevjhhx09RgBwCUdPt7VaraUWss7HYrGcMx6jRJskFRQUaNiwYZo2bZratm1b6XFWReQMgJqqOi3tqMnIGQA1lRlzpsIf8//zn//UpEmTlJaWpsLCQl166aWqXbu2I8cGAKYQHBwsT0/PErOzsrKySsziks4+sWnz5s1KTU21/c93YWGhDMOQl5eXVq5cqeuuu84lY3cmcgYA4EzkDADUDBUqbL311lu6/fbb5e/vr8jISEePCQDcwl2fbvj4+CgiIkIpKSkaPHiwrT0lJUU3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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=0ffe8f35-58f3-41b6-acfd-5d97181e4450">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="WNIOSKI:">WNIOSKI:<a class="anchor-link" href="#WNIOSKI:">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=3c765a00-b6c6-4be0-aae3-93b277dfdd53">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<ul>
<li>w klasie 1:</li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=4eca1ab1-1f00-4fa7-8c69-d8bfc70aff60">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<pre><code>śmiertelność dorosłych wyniosła: 35.6%
śmiertelność dzieci wyniosła:    0.7%</code></pre>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=71dd8ac5-8966-4d2d-97b7-49fd42565e3c">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<ul>
<li>w klasie 2:</li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=a15797eb-30c5-45e5-865c-1e0494ae50d0">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<pre><code>śmiertelność dorosłych wyniosła: 54.4%
śmiertelność dzieci wyniosła:    1.5%</code></pre>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=9a050d13-7cfd-4f54-a83d-7446c8c1c6bc">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<ul>
<li>w klasie 3:</li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=9002d536-953e-4790-903d-68139f11cd23">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<pre><code>śmiertelność dorosłych wyniosła: 60.5%
śmiertelność dzieci wyniosła:    13.4%</code></pre>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=8799a7b8-5d04-4f4a-b5b1-103fe814583e">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Wniosek-jaki-si%C4%99-sam-nasuwa-to-taki,-%C5%BCe-wykres-zale%C5%BCno%C5%9Bci-ceny-od-prze%C5%BCywalno%C5%9Bci-jest-nieadekwatny-i-%C5%BCeby-uzyska%C4%87-bardziej-wiarygodne-dane-nale%C5%BCy-pos%C5%82u%C5%BCy%C4%87-sie-wykresem-ko%C5%82owym-osobnym-dla-ka%C5%BCdej-z-klas.-Wtedy-na-w%C5%82asne-oczy-mo%C5%BCemy-ujrze%C4%87-jak-w-rzeczywisto%C5%9Bci-wygl%C4%85da%C5%82a-sytuacja-i-gdzie-by%C5%82a-najwi%C4%99ksza-%C5%9Bmiertelno%C5%9B%C4%87.">Wniosek jaki się sam nasuwa to taki, że wykres zależności ceny od przeżywalności jest nieadekwatny i żeby uzyskać bardziej wiarygodne dane należy posłużyć sie wykresem kołowym osobnym dla każdej z klas. Wtedy na własne oczy możemy ujrzeć jak w rzeczywistości wyglądała sytuacja i gdzie była największa śmiertelność.<a class="anchor-link" href="#Wniosek-jaki-si%C4%99-sam-nasuwa-to-taki,-%C5%BCe-wykres-zale%C5%BCno%C5%9Bci-ceny-od-prze%C5%BCywalno%C5%9Bci-jest-nieadekwatny-i-%C5%BCeby-uzyska%C4%87-bardziej-wiarygodne-dane-nale%C5%BCy-pos%C5%82u%C5%BCy%C4%87-sie-wykresem-ko%C5%82owym-osobnym-dla-ka%C5%BCdej-z-klas.-Wtedy-na-w%C5%82asne-oczy-mo%C5%BCemy-ujrze%C4%87-jak-w-rzeczywisto%C5%9Bci-wygl%C4%85da%C5%82a-sytuacja-i-gdzie-by%C5%82a-najwi%C4%99ksza-%C5%9Bmiertelno%C5%9B%C4%87.">¶</a></h1>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs" id="cell-id=87191eb8-212c-47ff-8857-6e86e891e6dc">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span> 
</pre></div>
</div>
</div>
</div>
</div>
</div>
</main>
</body>
</html>


