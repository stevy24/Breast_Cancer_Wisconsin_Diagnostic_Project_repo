<!DOCTYPE html>
<!-- saved from url=(0080)http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb -->
<html lang="fr-fr"><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    

    <title>Breast_Cancer_Wisconsin_Diagnostic_Project</title>
    
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <link rel="stylesheet" href="./README_files/jquery-ui.min.css" type="text/css">
    <link rel="stylesheet" href="./README_files/jquery.typeahead.min.css" type="text/css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    


<script type="text/javascript" src="./README_files/MathJax.js.download" charset="utf-8"></script>

<script type="text/javascript">
// MathJax disabled, set as null to distingish from *missing* MathJax,
// where it will be undefined, and should prompt a dialog later.
window.mathjax_url = "/static/components/MathJax/MathJax.js";
</script>

<link rel="stylesheet" href="./README_files/bootstrap-tour.min.css" type="text/css">
<link rel="stylesheet" href="./README_files/codemirror.css">


    <link rel="stylesheet" href="./README_files/style.min.css" type="text/css">
    

<link rel="stylesheet" href="./README_files/override.css" type="text/css">
<link rel="stylesheet" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb" id="kernel-css" type="text/css">


    <link rel="stylesheet" href="./README_files/custom.css" type="text/css">
    <script src="./README_files/promise.min.js.download" type="text/javascript" charset="utf-8"></script>
    <script src="./README_files/index.js.download" type="text/javascript"></script>
    <script src="./README_files/index.js(1).download" type="text/javascript"></script>
    <script src="./README_files/index.js(2).download" type="text/javascript"></script>
    <script src="./README_files/require.js.download" type="text/javascript" charset="utf-8"></script>
    <script>
      require.config({
          
          urlArgs: "v=20190219085620",
          
          baseUrl: '/static/',
          paths: {
            'auth/js/main': 'auth/js/main.min',
            custom : '/custom',
            nbextensions : '/nbextensions',
            kernelspecs : '/kernelspecs',
            underscore : 'components/underscore/underscore-min',
            backbone : 'components/backbone/backbone-min',
            jed: 'components/jed/jed',
            jquery: 'components/jquery/jquery.min',
            json: 'components/requirejs-plugins/src/json',
            text: 'components/requirejs-text/text',
            bootstrap: 'components/bootstrap/js/bootstrap.min',
            bootstraptour: 'components/bootstrap-tour/build/js/bootstrap-tour.min',
            'jquery-ui': 'components/jquery-ui/ui/minified/jquery-ui.min',
            moment: 'components/moment/min/moment-with-locales',
            codemirror: 'components/codemirror',
            termjs: 'components/xterm.js/xterm',
            typeahead: 'components/jquery-typeahead/dist/jquery.typeahead.min',
          },
          map: { // for backward compatibility
              "*": {
                  "jqueryui": "jquery-ui",
              }
          },
          shim: {
            typeahead: {
              deps: ["jquery"],
              exports: "typeahead"
            },
            underscore: {
              exports: '_'
            },
            backbone: {
              deps: ["underscore", "jquery"],
              exports: "Backbone"
            },
            bootstrap: {
              deps: ["jquery"],
              exports: "bootstrap"
            },
            bootstraptour: {
              deps: ["bootstrap"],
              exports: "Tour"
            },
            "jquery-ui": {
              deps: ["jquery"],
              exports: "$"
            }
          },
          waitSeconds: 30,
      });

      require.config({
          map: {
              '*':{
                'contents': 'services/contents',
              }
          }
      });

      // error-catching custom.js shim.
      define("custom", function (require, exports, module) {
          try {
              var custom = require('custom/custom');
              console.debug('loaded custom.js');
              return custom;
          } catch (e) {
              console.error("error loading custom.js", e);
              return {};
          }
      })

    document.nbjs_translations = {"domain": "nbjs", "locale_data": {"nbjs": {"": {"domain": "nbjs"}}}};
    document.documentElement.lang = navigator.language.toLowerCase();
    </script>

    
    

<script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="services/contents" src="./README_files/contents.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="custom/custom" src="./README_files/custom.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/plotlywidget/extension" src="./README_files/extension.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/jupyter-js-widgets/extension" src="./README_files/extension.js(1).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/nbextensions_configurator/config_menu/main" src="./README_files/main.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/contrib_nbextensions_help_item/main" src="./README_files/main.js(1).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/varInspector/main" src="./README_files/main.js(2).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/code_prettify" src="./README_files/code_prettify.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/collapsible_headings/main" src="./README_files/main.js(3).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/toc2/main" src="./README_files/main.js(4).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/main" src="./README_files/main.js(5).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/export_embedded/main" src="./README_files/main.js(6).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/autopep8" src="./README_files/autopep8.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_font_size/code_font_size" src="./README_files/code_font_size.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/gist_it/main" src="./README_files/main.js(7).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/python-markdown/main" src="./README_files/main.js(8).download"></script><link type="text/css" rel="stylesheet" href="./README_files/main.css"><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/kernel_exec_on_cell" src="./README_files/kernel_exec_on_cell.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/toc2/toc2" src="./README_files/toc2.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/foldcode" src="./README_files/foldcode.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/foldgutter" src="./README_files/foldgutter.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/brace-fold" src="./README_files/brace-fold.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/indent-fold" src="./README_files/indent-fold.js.download"></script><style type="text/css">.MathJax_Hover_Frame {border-radius: .25em; -webkit-border-radius: .25em; -moz-border-radius: .25em; -khtml-border-radius: .25em; box-shadow: 0px 0px 15px #83A; -webkit-box-shadow: 0px 0px 15px #83A; -moz-box-shadow: 0px 0px 15px #83A; -khtml-box-shadow: 0px 0px 15px #83A; border: 1px solid #A6D ! important; display: inline-block; position: absolute}
.MathJax_Menu_Button .MathJax_Hover_Arrow {position: absolute; cursor: pointer; display: inline-block; border: 2px solid #AAA; border-radius: 4px; -webkit-border-radius: 4px; -moz-border-radius: 4px; -khtml-border-radius: 4px; font-family: 'Courier New',Courier; font-size: 9px; color: #F0F0F0}
.MathJax_Menu_Button .MathJax_Hover_Arrow span {display: block; background-color: #AAA; border: 1px solid; border-radius: 3px; line-height: 0; padding: 4px}
.MathJax_Hover_Arrow:hover {color: white!important; border: 2px solid #CCC!important}
.MathJax_Hover_Arrow:hover span {background-color: #CCC!important}
</style><style type="text/css">#MathJax_About {position: fixed; left: 50%; width: auto; text-align: center; border: 3px outset; padding: 1em 2em; background-color: #DDDDDD; color: black; cursor: default; font-family: message-box; font-size: 120%; font-style: normal; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; z-index: 201; border-radius: 15px; -webkit-border-radius: 15px; -moz-border-radius: 15px; -khtml-border-radius: 15px; box-shadow: 0px 10px 20px #808080; -webkit-box-shadow: 0px 10px 20px #808080; -moz-box-shadow: 0px 10px 20px #808080; -khtml-box-shadow: 0px 10px 20px #808080; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
#MathJax_About.MathJax_MousePost {outline: none}
.MathJax_Menu {position: absolute; background-color: white; color: black; width: auto; padding: 2px; border: 1px solid #CCCCCC; margin: 0; cursor: default; font: menu; text-align: left; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; z-index: 201; box-shadow: 0px 10px 20px #808080; -webkit-box-shadow: 0px 10px 20px #808080; -moz-box-shadow: 0px 10px 20px #808080; -khtml-box-shadow: 0px 10px 20px #808080; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
.MathJax_MenuItem {padding: 2px 2em; background: transparent}
.MathJax_MenuArrow {position: absolute; right: .5em; padding-top: .25em; color: #666666; font-size: .75em}
.MathJax_MenuActive .MathJax_MenuArrow {color: white}
.MathJax_MenuArrow.RTL {left: .5em; right: auto}
.MathJax_MenuCheck {position: absolute; left: .7em}
.MathJax_MenuCheck.RTL {right: .7em; left: auto}
.MathJax_MenuRadioCheck {position: absolute; left: 1em}
.MathJax_MenuRadioCheck.RTL {right: 1em; left: auto}
.MathJax_MenuLabel {padding: 2px 2em 4px 1.33em; font-style: italic}
.MathJax_MenuRule {border-top: 1px solid #CCCCCC; margin: 4px 1px 0px}
.MathJax_MenuDisabled {color: GrayText}
.MathJax_MenuActive {background-color: Highlight; color: HighlightText}
.MathJax_MenuDisabled:focus, .MathJax_MenuLabel:focus {background-color: #E8E8E8}
.MathJax_ContextMenu:focus {outline: none}
.MathJax_ContextMenu .MathJax_MenuItem:focus {outline: none}
#MathJax_AboutClose {top: .2em; right: .2em}
.MathJax_Menu .MathJax_MenuClose {top: -10px; left: -10px}
.MathJax_MenuClose {position: absolute; cursor: pointer; display: inline-block; border: 2px solid #AAA; border-radius: 18px; -webkit-border-radius: 18px; -moz-border-radius: 18px; -khtml-border-radius: 18px; font-family: 'Courier New',Courier; font-size: 24px; color: #F0F0F0}
.MathJax_MenuClose span {display: block; background-color: #AAA; border: 1.5px solid; border-radius: 18px; -webkit-border-radius: 18px; -moz-border-radius: 18px; -khtml-border-radius: 18px; line-height: 0; padding: 8px 0 6px}
.MathJax_MenuClose:hover {color: white!important; border: 2px solid #CCC!important}
.MathJax_MenuClose:hover span {background-color: #CCC!important}
.MathJax_MenuClose:hover:focus {outline: none}
</style><style type="text/css">.MathJax_Preview .MJXf-math {color: inherit!important}
</style><style type="text/css">.MJX_Assistive_MathML {position: absolute!important; top: 0; left: 0; clip: rect(1px, 1px, 1px, 1px); padding: 1px 0 0 0!important; border: 0!important; height: 1px!important; width: 1px!important; overflow: hidden!important; display: block!important; -webkit-touch-callout: none; -webkit-user-select: none; -khtml-user-select: none; -moz-user-select: none; -ms-user-select: none; user-select: none}
.MJX_Assistive_MathML.MJX_Assistive_MathML_Block {width: 100%!important}
</style><style type="text/css">#MathJax_Zoom {position: absolute; background-color: #F0F0F0; overflow: auto; display: block; z-index: 301; padding: .5em; border: 1px solid black; margin: 0; font-weight: normal; font-style: normal; text-align: left; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; -webkit-box-sizing: content-box; -moz-box-sizing: content-box; box-sizing: content-box; box-shadow: 5px 5px 15px #AAAAAA; -webkit-box-shadow: 5px 5px 15px #AAAAAA; -moz-box-shadow: 5px 5px 15px #AAAAAA; -khtml-box-shadow: 5px 5px 15px #AAAAAA; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
#MathJax_ZoomOverlay {position: absolute; left: 0; top: 0; z-index: 300; display: inline-block; width: 100%; height: 100%; border: 0; padding: 0; margin: 0; background-color: white; opacity: 0; filter: alpha(opacity=0)}
#MathJax_ZoomFrame {position: relative; display: inline-block; height: 0; width: 0}
#MathJax_ZoomEventTrap {position: absolute; left: 0; top: 0; z-index: 302; display: inline-block; border: 0; padding: 0; margin: 0; background-color: white; opacity: 0; filter: alpha(opacity=0)}
</style><style type="text/css">.MathJax_Preview {color: #888}
#MathJax_Message {position: fixed; left: 1em; bottom: 1.5em; background-color: #E6E6E6; border: 1px solid #959595; margin: 0px; padding: 2px 8px; z-index: 102; color: black; font-size: 80%; width: auto; white-space: nowrap}
#MathJax_MSIE_Frame {position: absolute; top: 0; left: 0; width: 0px; z-index: 101; border: 0px; margin: 0px; padding: 0px}
.MathJax_Error {color: #CC0000; font-style: italic}
</style><link type="text/css" rel="stylesheet" href="./README_files/main(1).css"><link id="collapsible_headings_css" rel="stylesheet" type="text/css" href="./README_files/main(2).css"><style id="collapsible_headings_indent_css">.collapsible_headings_toggle .h1 { margin-right: 40px; }
.collapsible_headings_toggle .h2 { margin-right: 32px; }
.collapsible_headings_toggle .h3 { margin-right: 24px; }
.collapsible_headings_toggle .h4 { margin-right: 16px; }
.collapsible_headings_toggle .h5 { margin-right: 8px; }
.collapsible_headings_toggle .h6 { margin-right: 0px; }</style><link type="text/css" rel="stylesheet" href="./README_files/main(3).css"><link type="text/css" rel="stylesheet" href="./README_files/foldgutter.css"><link type="text/css" rel="stylesheet" href="./README_files/foldgutter(1).css"><style type="text/css">div.MathJax_MathML {text-align: center; margin: .75em 0px; display: block!important}
.MathJax_MathML {font-style: normal; font-weight: normal; line-height: normal; font-size: 100%; font-size-adjust: none; text-indent: 0; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0; min-height: 0; border: 0; padding: 0; margin: 0}
span.MathJax_MathML {display: inline!important}
.MathJax_mmlExBox {display: block!important; overflow: hidden; height: 1px; width: 60ex; min-height: 0; max-height: none; padding: 0; border: 0; margin: 0}
[class="MJX-tex-oldstyle"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB}
[class="MJX-tex-oldstyle-bold"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB; font-weight: bold}
[class="MJX-tex-caligraphic"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB}
[class="MJX-tex-caligraphic-bold"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB; font-weight: bold}
@font-face /*1*/ {font-family: MathJax_Caligraphic-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Caligraphic-Regular.otf')}
@font-face /*2*/ {font-family: MathJax_Caligraphic-WEB; font-weight: bold; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Caligraphic-Bold.otf')}
[mathvariant="double-struck"] {font-family: MathJax_AMS, MathJax_AMS-WEB}
[mathvariant="script"] {font-family: MathJax_Script, MathJax_Script-WEB}
[mathvariant="fraktur"] {font-family: MathJax_Fraktur, MathJax_Fraktur-WEB}
[mathvariant="bold-script"] {font-family: MathJax_Script, MathJax_Caligraphic-WEB; font-weight: bold}
[mathvariant="bold-fraktur"] {font-family: MathJax_Fraktur, MathJax_Fraktur-WEB; font-weight: bold}
[mathvariant="monospace"] {font-family: monospace}
[mathvariant="sans-serif"] {font-family: sans-serif}
[mathvariant="bold-sans-serif"] {font-family: sans-serif; font-weight: bold}
[mathvariant="sans-serif-italic"] {font-family: sans-serif; font-style: italic}
[mathvariant="sans-serif-bold-italic"] {font-family: sans-serif; font-style: italic; font-weight: bold}
@font-face /*3*/ {font-family: MathJax_AMS-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_AMS-Regular.otf')}
@font-face /*4*/ {font-family: MathJax_Script-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Script-Regular.otf')}
@font-face /*5*/ {font-family: MathJax_Fraktur-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Fraktur-Regular.otf')}
@font-face /*6*/ {font-family: MathJax_Fraktur-WEB; font-weight: bold; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Fraktur-Bold.otf')}
</style><style type="text/css">.MJXp-script {font-size: .8em}
.MJXp-right {-webkit-transform-origin: right; -moz-transform-origin: right; -ms-transform-origin: right; -o-transform-origin: right; transform-origin: right}
.MJXp-bold {font-weight: bold}
.MJXp-italic {font-style: italic}
.MJXp-scr {font-family: MathJax_Script,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-frak {font-family: MathJax_Fraktur,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-sf {font-family: MathJax_SansSerif,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-cal {font-family: MathJax_Caligraphic,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-mono {font-family: MathJax_Typewriter,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-largeop {font-size: 150%}
.MJXp-largeop.MJXp-int {vertical-align: -.2em}
.MJXp-math {display: inline-block; line-height: 1.2; text-indent: 0; font-family: 'Times New Roman',Times,STIXGeneral,serif; white-space: nowrap; border-collapse: collapse}
.MJXp-display {display: block; text-align: center; margin: 1em 0}
.MJXp-math span {display: inline-block}
.MJXp-box {display: block!important; text-align: center}
.MJXp-box:after {content: " "}
.MJXp-rule {display: block!important; margin-top: .1em}
.MJXp-char {display: block!important}
.MJXp-mo {margin: 0 .15em}
.MJXp-mfrac {margin: 0 .125em; vertical-align: .25em}
.MJXp-denom {display: inline-table!important; width: 100%}
.MJXp-denom > * {display: table-row!important}
.MJXp-surd {vertical-align: top}
.MJXp-surd > * {display: block!important}
.MJXp-script-box > *  {display: table!important; height: 50%}
.MJXp-script-box > * > * {display: table-cell!important; vertical-align: top}
.MJXp-script-box > *:last-child > * {vertical-align: bottom}
.MJXp-script-box > * > * > * {display: block!important}
.MJXp-mphantom {visibility: hidden}
.MJXp-munderover {display: inline-table!important}
.MJXp-over {display: inline-block!important; text-align: center}
.MJXp-over > * {display: block!important}
.MJXp-munderover > * {display: table-row!important}
.MJXp-mtable {vertical-align: .25em; margin: 0 .125em}
.MJXp-mtable > * {display: inline-table!important; vertical-align: middle}
.MJXp-mtr {display: table-row!important}
.MJXp-mtd {display: table-cell!important; text-align: center; padding: .5em 0 0 .5em}
.MJXp-mtr > .MJXp-mtd:first-child {padding-left: 0}
.MJXp-mtr:first-child > .MJXp-mtd {padding-top: 0}
.MJXp-mlabeledtr {display: table-row!important}
.MJXp-mlabeledtr > .MJXp-mtd:first-child {padding-left: 0}
.MJXp-mlabeledtr:first-child > .MJXp-mtd {padding-top: 0}
.MJXp-merror {background-color: #FFFF88; color: #CC0000; border: 1px solid #CC0000; padding: 1px 3px; font-style: normal; font-size: 90%}
.MJXp-scale0 {-webkit-transform: scaleX(.0); -moz-transform: scaleX(.0); -ms-transform: scaleX(.0); -o-transform: scaleX(.0); transform: scaleX(.0)}
.MJXp-scale1 {-webkit-transform: scaleX(.1); -moz-transform: scaleX(.1); -ms-transform: scaleX(.1); -o-transform: scaleX(.1); transform: scaleX(.1)}
.MJXp-scale2 {-webkit-transform: scaleX(.2); -moz-transform: scaleX(.2); -ms-transform: scaleX(.2); -o-transform: scaleX(.2); transform: scaleX(.2)}
.MJXp-scale3 {-webkit-transform: scaleX(.3); -moz-transform: scaleX(.3); -ms-transform: scaleX(.3); -o-transform: scaleX(.3); transform: scaleX(.3)}
.MJXp-scale4 {-webkit-transform: scaleX(.4); -moz-transform: scaleX(.4); -ms-transform: scaleX(.4); -o-transform: scaleX(.4); transform: scaleX(.4)}
.MJXp-scale5 {-webkit-transform: scaleX(.5); -moz-transform: scaleX(.5); -ms-transform: scaleX(.5); -o-transform: scaleX(.5); transform: scaleX(.5)}
.MJXp-scale6 {-webkit-transform: scaleX(.6); -moz-transform: scaleX(.6); -ms-transform: scaleX(.6); -o-transform: scaleX(.6); transform: scaleX(.6)}
.MJXp-scale7 {-webkit-transform: scaleX(.7); -moz-transform: scaleX(.7); -ms-transform: scaleX(.7); -o-transform: scaleX(.7); transform: scaleX(.7)}
.MJXp-scale8 {-webkit-transform: scaleX(.8); -moz-transform: scaleX(.8); -ms-transform: scaleX(.8); -o-transform: scaleX(.8); transform: scaleX(.8)}
.MJXp-scale9 {-webkit-transform: scaleX(.9); -moz-transform: scaleX(.9); -ms-transform: scaleX(.9); -o-transform: scaleX(.9); transform: scaleX(.9)}
.MathJax_PHTML .noError {vertical-align: ; font-size: 90%; text-align: left; color: black; padding: 1px 3px; border: 1px solid}
</style><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/firstline-fold" src="./README_files/firstline-fold.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/magic-fold" src="./README_files/magic-fold.js.download"></script><style type="text/css">.MathJax_Display {text-align: center; margin: 0; position: relative; display: block!important; text-indent: 0; max-width: none; max-height: none; min-width: 0; min-height: 0; width: 100%}
.MathJax .merror {background-color: #FFFF88; color: #CC0000; border: 1px solid #CC0000; padding: 1px 3px; font-style: normal; font-size: 90%}
.MathJax .MJX-monospace {font-family: monospace}
.MathJax .MJX-sans-serif {font-family: sans-serif}
#MathJax_Tooltip {background-color: InfoBackground; color: InfoText; border: 1px solid black; box-shadow: 2px 2px 5px #AAAAAA; -webkit-box-shadow: 2px 2px 5px #AAAAAA; -moz-box-shadow: 2px 2px 5px #AAAAAA; -khtml-box-shadow: 2px 2px 5px #AAAAAA; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true'); padding: 3px 4px; z-index: 401; position: absolute; left: 0; top: 0; width: auto; height: auto; display: none}
.MathJax {display: inline; font-style: normal; font-weight: normal; line-height: normal; font-size: 100%; font-size-adjust: none; text-indent: 0; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0; min-height: 0; border: 0; padding: 0; margin: 0}
.MathJax:focus, body :focus .MathJax {display: inline-table}
.MathJax.MathJax_FullWidth {text-align: center; display: table-cell!important; width: 10000em!important}
.MathJax img, .MathJax nobr, .MathJax a {border: 0; padding: 0; margin: 0; max-width: none; max-height: none; min-width: 0; min-height: 0; vertical-align: 0; line-height: normal; text-decoration: none}
img.MathJax_strut {border: 0!important; padding: 0!important; margin: 0!important; vertical-align: 0!important}
.MathJax span {display: inline; position: static; border: 0; padding: 0; margin: 0; vertical-align: 0; line-height: normal; text-decoration: none; box-sizing: content-box}
.MathJax nobr {white-space: nowrap!important}
.MathJax img {display: inline!important; float: none!important}
.MathJax * {transition: none; -webkit-transition: none; -moz-transition: none; -ms-transition: none; -o-transition: none}
.MathJax_Processing {visibility: hidden; position: fixed; width: 0; height: 0; overflow: hidden}
.MathJax_Processed {display: none!important}
.MathJax_ExBox {display: block!important; overflow: hidden; width: 1px; height: 60ex; min-height: 0; max-height: none}
.MathJax .MathJax_EmBox {display: block!important; overflow: hidden; width: 1px; height: 60em; min-height: 0; max-height: none}
.MathJax_LineBox {display: table!important}
.MathJax_LineBox span {display: table-cell!important; width: 10000em!important; min-width: 0; max-width: none; padding: 0; border: 0; margin: 0}
.MathJax .MathJax_HitBox {cursor: text; background: white; opacity: 0; filter: alpha(opacity=0)}
.MathJax .MathJax_HitBox * {filter: none; opacity: 1; background: transparent}
#MathJax_Tooltip * {filter: none; opacity: 1; background: transparent}
@font-face {font-family: MathJax_Blank; src: url('about:blank')}
.MathJax .noError {vertical-align: ; font-size: 90%; text-align: left; color: black; padding: 1px 3px; border: 1px solid}
</style><style type="text/css">/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/* Override the correction for the prompt area in https://github.com/jupyter/notebook/blob/dd41d9fd5c4f698bd7468612d877828a7eeb0e7a/IPython/html/static/notebook/less/outputarea.less#L110 */

.jupyter-widgets-output-area div.output_subarea {
    max-width: 100%;
}

/* Work-around for the bug fixed in https://github.com/jupyter/notebook/pull/2961 */

.jupyter-widgets-output-area > .out_prompt_overlay {
    display: none;
}
</style><style type="text/css">/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-Widget {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: relative;
  overflow: hidden;
  cursor: default;
}
.p-Widget.p-mod-hidden {
  display: none !important;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-CommandPalette {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-CommandPalette-search {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-content {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}
.p-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.p-CommandPalette-item {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-CommandPalette-itemIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-itemContent {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
}
.p-CommandPalette-itemShortcut {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-DockPanel {
  z-index: 0;
}
.p-DockPanel-widget {
  z-index: 0;
}
.p-DockPanel-tabBar {
  z-index: 1;
}
.p-DockPanel-handle {
  z-index: 2;
}
.p-DockPanel-handle.p-mod-hidden {
  display: none !important;
}
.p-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}
.p-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}
.p-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}
.p-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  -webkit-transform: translateX(-50%);
          transform: translateX(-50%);
}
.p-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  -webkit-transform: translateY(-50%);
          transform: translateY(-50%);
}
.p-DockPanel-overlay {
  z-index: 3;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  pointer-events: none;
}
.p-DockPanel-overlay.p-mod-hidden {
  display: none !important;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-Menu {
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
.p-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}
.p-Menu-item {
  display: table-row;
}
.p-Menu-item.p-mod-hidden,
.p-Menu-item.p-mod-collapsed {
  display: none !important;
}
.p-Menu-itemIcon,
.p-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}
.p-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}
.p-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-MenuBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  list-style-type: none;
}
.p-MenuBar-item {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
}
.p-MenuBar-itemIcon,
.p-MenuBar-itemLabel {
  display: inline-block;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-ScrollBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-ScrollBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-ScrollBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-ScrollBar-button {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-ScrollBar-track {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: relative;
  overflow: hidden;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
}
.p-ScrollBar-thumb {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: absolute;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-SplitPanel-child {
  z-index: 0;
}
.p-SplitPanel-handle {
  z-index: 1;
}
.p-SplitPanel-handle.p-mod-hidden {
  display: none !important;
}
.p-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle {
  cursor: ew-resize;
}
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle {
  cursor: ns-resize;
}
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  -webkit-transform: translateX(-50%);
          transform: translateX(-50%);
}
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  -webkit-transform: translateY(-50%);
          transform: translateY(-50%);
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-TabBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-TabBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-TabBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-TabBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  list-style-type: none;
}
.p-TabBar[data-orientation='horizontal'] > .p-TabBar-content {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-TabBar[data-orientation='vertical'] > .p-TabBar-content {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-TabBar-tab {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  overflow: hidden;
}
.p-TabBar-tabIcon,
.p-TabBar-tabCloseIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-TabBar-tabLabel {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}
.p-TabBar-tab.p-mod-hidden {
  display: none !important;
}
.p-TabBar.p-mod-dragging .p-TabBar-tab {
  position: relative;
}
.p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab {
  left: 0;
  -webkit-transition: left 150ms ease;
  transition: left 150ms ease;
}
.p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab {
  top: 0;
  -webkit-transition: top 150ms ease;
  transition: top 150ms ease;
}
.p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging {
  -webkit-transition: none;
  transition: none;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-TabPanel-tabBar {
  z-index: 1;
}
.p-TabPanel-stackedPanel {
  z-index: 0;
}
</style><style type="text/css">/* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 .jupyter-widgets-disconnected::before {
    content: "\F127"; /* chain-broken */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #d9534f;
    padding: 3px;
    -ms-flex-item-align: start;
        align-self: flex-start;
}
</style><style type="text/css">/* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 /* We import all of these together in a single css file because the Webpack
loader sees only one file at a time. This allows postcss to see the variable
definitions when they are used. */

 /*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

 /*
This file is copied from the JupyterLab project to define default styling for
when the widget styling is compiled down to eliminate CSS variables. We make one
change - we comment out the font import below.
*/

 /**
 * The material design colors are adapted from google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 * https://github.com/danlevan/google-material-color/blob/f67ca5f4028b2f1b34862f64b0ca67323f91b088/dist/palette.var.css
 *
 * The license for the material design color CSS variables is as follows (see
 * https://github.com/danlevan/google-material-color/blob/f67ca5f4028b2f1b34862f64b0ca67323f91b088/LICENSE)
 *
 * The MIT License (MIT)
 *
 * Copyright (c) 2014 Dan Le Van
 *
 * Permission is hereby granted, free of charge, to any person obtaining a copy
 * of this software and associated documentation files (the "Software"), to deal
 * in the Software without restriction, including without limitation the rights
 * to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 * copies of the Software, and to permit persons to whom the Software is
 * furnished to do so, subject to the following conditions:
 *
 * The above copyright notice and this permission notice shall be included in
 * all copies or substantial portions of the Software.
 *
 * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 * IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 * FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 * AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 * LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 * OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 * SOFTWARE.
 */

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

 /*
 * Optional monospace font for input/output prompt.
 */

 /* Commented out in ipywidgets since we don't need it. */

 /* @import url('https://fonts.googleapis.com/css?family=Roboto+Mono'); */

 /*
 * Added for compabitility with output area
 */

 :root {

  /* Borders

  The following variables, specify the visual styling of borders in JupyterLab.
   */

  /* UI Fonts

  The UI font CSS variables are used for the typography all of the JupyterLab
  user interface elements that are not directly user generated content.
  */ /* Base font size */ /* Ensures px perfect FontAwesome icons */

  /* Use these font colors against the corresponding main layout colors.
     In a light theme, these go from dark to light.
  */

  /* Use these against the brand/accent/warn/error colors.
     These will typically go from light to darker, in both a dark and light theme
   */

  /* Content Fonts

  Content font variables are used for typography of user generated content.
  */ /* Base font size */


  /* Layout

  The following are the main layout colors use in JupyterLab. In a light
  theme these would go from light to dark.
  */

  /* Brand/accent */

  /* State colors (warn, error, success, info) */

  /* Cell specific styles */
  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */

  /* Notebook specific styles */

  /* Console specific styles */

  /* Toolbar specific styles */
}

 /* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 /*
 * We assume that the CSS variables in
 * https://github.com/jupyterlab/jupyterlab/blob/master/src/default-theme/variables.css
 * have been defined.
 */

 /* This file has code derived from PhosphorJS CSS files, as noted below. The license for this PhosphorJS code is:

Copyright (c) 2014-2017, PhosphorJS Contributors
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of the copyright holder nor the names of its
  contributors may be used to endorse or promote products derived from
  this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

*/

 /*
 * The following section is derived from https://github.com/phosphorjs/phosphor/blob/23b9d075ebc5b73ab148b6ebfc20af97f85714c4/packages/widgets/style/tabbar.css 
 * We've scoped the rules so that they are consistent with exactly our code.
 */

 .jupyter-widgets.widget-tab > .p-TabBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar > .p-TabBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  list-style-type: none;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='horizontal'] > .p-TabBar-content {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='vertical'] > .p-TabBar-content {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  overflow: hidden;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabIcon,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabCloseIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabLabel {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-hidden {
  display: none !important;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging .p-TabBar-tab {
  position: relative;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab {
  left: 0;
  -webkit-transition: left 150ms ease;
  transition: left 150ms ease;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab {
  top: 0;
  -webkit-transition: top 150ms ease;
  transition: top 150ms ease;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging {
  -webkit-transition: none;
  transition: none;
}

 /* End tabbar.css */

 :root { /* margin between inline elements */

    /* From Material Design Lite */
}

 .jupyter-widgets {
    margin: 2px;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    color: black;
    overflow: visible;
}

 .jupyter-widgets.jupyter-widgets-disconnected::before {
    line-height: 28px;
    height: 28px;
}

 .jp-Output-result > .jupyter-widgets {
    margin-left: 0;
    margin-right: 0;
}

 /* vbox and hbox */

 .widget-inline-hbox {
    /* Horizontal widgets */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
    -webkit-box-align: baseline;
        -ms-flex-align: baseline;
            align-items: baseline;
}

 .widget-inline-vbox {
    /* Vertical Widgets */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
}

 .widget-box {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    margin: 0;
    overflow: auto;
}

 .widget-gridbox {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: grid;
    margin: 0;
    overflow: auto;
}

 .widget-hbox {
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
}

 .widget-vbox {
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 /* General Button Styling */

 .jupyter-button {
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 0px;
    padding-bottom: 0px;
    display: inline-block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: center;
    font-size: 13px;
    cursor: pointer;

    height: 28px;
    border: 0px solid;
    line-height: 28px;
    -webkit-box-shadow: none;
            box-shadow: none;

    color: rgba(0, 0, 0, .8);
    background-color: #EEEEEE;
    border-color: #E0E0E0;
    border: none;
}

 .jupyter-button i.fa {
    margin-right: 4px;
    pointer-events: none;
}

 .jupyter-button:empty:before {
    content: "\200B"; /* zero-width space */
}

 .jupyter-widgets.jupyter-button:disabled {
    opacity: 0.6;
}

 .jupyter-button i.fa.center {
    margin-right: 0;
}

 .jupyter-button:hover:enabled, .jupyter-button:focus:enabled {
    /* MD Lite 2dp shadow */
    -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
                0 3px 1px -2px rgba(0, 0, 0, .2),
                0 1px 5px 0 rgba(0, 0, 0, .12);
            box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
                0 3px 1px -2px rgba(0, 0, 0, .2),
                0 1px 5px 0 rgba(0, 0, 0, .12);
}

 .jupyter-button:active, .jupyter-button.mod-active {
    /* MD Lite 4dp shadow */
    -webkit-box-shadow: 0 4px 5px 0 rgba(0, 0, 0, .14),
                0 1px 10px 0 rgba(0, 0, 0, .12),
                0 2px 4px -1px rgba(0, 0, 0, .2);
            box-shadow: 0 4px 5px 0 rgba(0, 0, 0, .14),
                0 1px 10px 0 rgba(0, 0, 0, .12),
                0 2px 4px -1px rgba(0, 0, 0, .2);
    color: rgba(0, 0, 0, .8);
    background-color: #BDBDBD;
}

 .jupyter-button:focus:enabled {
    outline: 1px solid #64B5F6;
}

 /* Button "Primary" Styling */

 .jupyter-button.mod-primary {
    color: rgba(255, 255, 255, 1.0);
    background-color: #2196F3;
}

 .jupyter-button.mod-primary.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #1976D2;
}

 .jupyter-button.mod-primary:active {
    color: rgba(255, 255, 255, 1);
    background-color: #1976D2;
}

 /* Button "Success" Styling */

 .jupyter-button.mod-success {
    color: rgba(255, 255, 255, 1.0);
    background-color: #4CAF50;
}

 .jupyter-button.mod-success.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #388E3C;
 }

 .jupyter-button.mod-success:active {
    color: rgba(255, 255, 255, 1);
    background-color: #388E3C;
 }

 /* Button "Info" Styling */

 .jupyter-button.mod-info {
    color: rgba(255, 255, 255, 1.0);
    background-color: #00BCD4;
}

 .jupyter-button.mod-info.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #0097A7;
}

 .jupyter-button.mod-info:active {
    color: rgba(255, 255, 255, 1);
    background-color: #0097A7;
}

 /* Button "Warning" Styling */

 .jupyter-button.mod-warning {
    color: rgba(255, 255, 255, 1.0);
    background-color: #FF9800;
}

 .jupyter-button.mod-warning.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #F57C00;
}

 .jupyter-button.mod-warning:active {
    color: rgba(255, 255, 255, 1);
    background-color: #F57C00;
}

 /* Button "Danger" Styling */

 .jupyter-button.mod-danger {
    color: rgba(255, 255, 255, 1.0);
    background-color: #F44336;
}

 .jupyter-button.mod-danger.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #D32F2F;
}

 .jupyter-button.mod-danger:active {
    color: rgba(255, 255, 255, 1);
    background-color: #D32F2F;
}

 /* Widget Button*/

 .widget-button, .widget-toggle-button {
    width: 148px;
}

 /* Widget Label Styling */

 /* Override Bootstrap label css */

 .jupyter-widgets label {
    margin-bottom: 0;
    margin-bottom: initial;
}

 .widget-label-basic {
    /* Basic Label */
    color: black;
    font-size: 13px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    line-height: 28px;
}

 .widget-label {
    /* Label */
    color: black;
    font-size: 13px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    line-height: 28px;
}

 .widget-inline-hbox .widget-label {
    /* Horizontal Widget Label */
    color: black;
    text-align: right;
    margin-right: 8px;
    width: 80px;
    -ms-flex-negative: 0;
        flex-shrink: 0;
}

 .widget-inline-vbox .widget-label {
    /* Vertical Widget Label */
    color: black;
    text-align: center;
    line-height: 28px;
}

 /* Widget Readout Styling */

 .widget-readout {
    color: black;
    font-size: 13px;
    height: 28px;
    line-height: 28px;
    overflow: hidden;
    white-space: nowrap;
    text-align: center;
}

 .widget-readout.overflow {
    /* Overflowing Readout */

    /* From Material Design Lite
        shadow-key-umbra-opacity: 0.2;
        shadow-key-penumbra-opacity: 0.14;
        shadow-ambient-shadow-opacity: 0.12;
     */
    -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .2),
                        0 3px 1px -2px rgba(0, 0, 0, .14),
                        0 1px 5px 0 rgba(0, 0, 0, .12);

    box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .2),
                0 3px 1px -2px rgba(0, 0, 0, .14),
                0 1px 5px 0 rgba(0, 0, 0, .12);
}

 .widget-inline-hbox .widget-readout {
    /* Horizontal Readout */
    text-align: center;
    max-width: 148px;
    min-width: 72px;
    margin-left: 4px;
}

 .widget-inline-vbox .widget-readout {
    /* Vertical Readout */
    margin-top: 4px;
    /* as wide as the widget */
    width: inherit;
}

 /* Widget Checkbox Styling */

 .widget-checkbox {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-checkbox input[type="checkbox"] {
    margin: 0px 8px 0px 0px;
    line-height: 28px;
    font-size: large;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 0;
        flex-shrink: 0;
    -ms-flex-item-align: center;
        align-self: center;
}

 /* Widget Valid Styling */

 .widget-valid {
    height: 28px;
    line-height: 28px;
    width: 148px;
    font-size: 13px;
}

 .widget-valid i:before {
    line-height: 28px;
    margin-right: 4px;
    margin-left: 4px;

    /* from the fa class in FontAwesome: https://github.com/FortAwesome/Font-Awesome/blob/49100c7c3a7b58d50baa71efef11af41a66b03d3/css/font-awesome.css#L14 */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

 .widget-valid.mod-valid i:before {
    content: "\F00C";
    color: green;
}

 .widget-valid.mod-invalid i:before {
    content: "\F00D";
    color: red;
}

 .widget-valid.mod-valid .widget-valid-readout {
    display: none;
}

 /* Widget Text and TextArea Stying */

 .widget-textarea, .widget-text {
    width: 300px;
}

 .widget-text input[type="text"], .widget-text input[type="number"]{
    height: 28px;
    line-height: 28px;
}

 .widget-text input[type="text"]:disabled, .widget-text input[type="number"]:disabled, .widget-textarea textarea:disabled {
    opacity: 0.6;
}

 .widget-text input[type="text"], .widget-text input[type="number"], .widget-textarea textarea {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    padding: 4px 8px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -ms-flex-negative: 1;
        flex-shrink: 1;
    outline: none !important;
}

 .widget-textarea textarea {
    height: inherit;
    width: inherit;
}

 .widget-text input:focus, .widget-textarea textarea:focus {
    border-color: #64B5F6;
}

 /* Widget Slider */

 .widget-slider .ui-slider {
    /* Slider Track */
    border: 1px solid #BDBDBD;
    background: #BDBDBD;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    position: relative;
    border-radius: 0px;
}

 .widget-slider .ui-slider .ui-slider-handle {
    /* Slider Handle */
    outline: none !important; /* focused slider handles are colored - see below */
    position: absolute;
    background-color: white;
    border: 1px solid #9E9E9E;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    z-index: 1;
    background-image: none; /* Override jquery-ui */
}

 /* Override jquery-ui */

 .widget-slider .ui-slider .ui-slider-handle:hover, .widget-slider .ui-slider .ui-slider-handle:focus {
    background-color: #2196F3;
    border: 1px solid #2196F3;
}

 .widget-slider .ui-slider .ui-slider-handle:active {
    background-color: #2196F3;
    border-color: #2196F3;
    z-index: 2;
    -webkit-transform: scale(1.2);
            transform: scale(1.2);
}

 .widget-slider  .ui-slider .ui-slider-range {
    /* Interval between the two specified value of a double slider */
    position: absolute;
    background: #2196F3;
    z-index: 0;
}

 /* Shapes of Slider Handles */

 .widget-hslider .ui-slider .ui-slider-handle {
    width: 16px;
    height: 16px;
    margin-top: -7px;
    margin-left: -7px;
    border-radius: 50%;
    top: 0;
}

 .widget-vslider .ui-slider .ui-slider-handle {
    width: 16px;
    height: 16px;
    margin-bottom: -7px;
    margin-left: -7px;
    border-radius: 50%;
    left: 0;
}

 .widget-hslider .ui-slider .ui-slider-range {
    height: 8px;
    margin-top: -3px;
}

 .widget-vslider .ui-slider .ui-slider-range {
    width: 8px;
    margin-left: -3px;
}

 /* Horizontal Slider */

 .widget-hslider {
    width: 300px;
    height: 28px;
    line-height: 28px;

    /* Override the align-items baseline. This way, the description and readout
    still seem to align their baseline properly, and we don't have to have
    align-self: stretch in the .slider-container. */
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
}

 .widgets-slider .slider-container {
    overflow: visible;
}

 .widget-hslider .slider-container {
    height: 28px;
    margin-left: 6px;
    margin-right: 6px;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
}

 .widget-hslider .ui-slider {
    /* Inner, invisible slide div */
    height: 4px;
    margin-top: 12px;
    width: 100%;
}

 /* Vertical Slider */

 .widget-vbox .widget-label {
    height: 28px;
    line-height: 28px;
}

 .widget-vslider {
    /* Vertical Slider */
    height: 200px;
    width: 72px;
}

 .widget-vslider .slider-container {
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 6px;
    margin-top: 6px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 .widget-vslider .ui-slider-vertical {
    /* Inner, invisible slide div */
    width: 4px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-left: auto;
    margin-right: auto;
}

 /* Widget Progress Styling */

 .progress-bar {
    -webkit-transition: none;
    transition: none;
}

 .progress-bar {
    height: 28px;
}

 .progress-bar {
    background-color: #2196F3;
}

 .progress-bar-success {
    background-color: #4CAF50;
}

 .progress-bar-info {
    background-color: #00BCD4;
}

 .progress-bar-warning {
    background-color: #FF9800;
}

 .progress-bar-danger {
    background-color: #F44336;
}

 .progress {
    background-color: #EEEEEE;
    border: none;
    -webkit-box-shadow: none;
            box-shadow: none;
}

 /* Horisontal Progress */

 .widget-hprogress {
    /* Progress Bar */
    height: 28px;
    line-height: 28px;
    width: 300px;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;

}

 .widget-hprogress .progress {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-top: 4px;
    margin-bottom: 4px;
    -ms-flex-item-align: stretch;
        align-self: stretch;
    /* Override bootstrap style */
    height: auto;
    height: initial;
}

 /* Vertical Progress */

 .widget-vprogress {
    height: 200px;
    width: 72px;
}

 .widget-vprogress .progress {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    width: 20px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 0;
}

 /* Select Widget Styling */

 .widget-dropdown {
    height: 28px;
    width: 300px;
    line-height: 28px;
}

 .widget-dropdown > select {
    padding-right: 20px;
    border: 1px solid #9E9E9E;
    border-radius: 0;
    height: inherit;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    outline: none !important;
    -webkit-box-shadow: none;
            box-shadow: none;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    vertical-align: top;
    padding-left: 8px;
	appearance: none;
	-webkit-appearance: none;
	-moz-appearance: none;
    background-repeat: no-repeat;
	background-size: 20px;
	background-position: right center;
    background-image: url("data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDE5LjIuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IgoJIHZpZXdCb3g9IjAgMCAxOCAxOCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMTggMTg7IiB4bWw6c3BhY2U9InByZXNlcnZlIj4KPHN0eWxlIHR5cGU9InRleHQvY3NzIj4KCS5zdDB7ZmlsbDpub25lO30KPC9zdHlsZT4KPHBhdGggZD0iTTUuMiw1LjlMOSw5LjdsMy44LTMuOGwxLjIsMS4ybC00LjksNWwtNC45LTVMNS4yLDUuOXoiLz4KPHBhdGggY2xhc3M9InN0MCIgZD0iTTAtMC42aDE4djE4SDBWLTAuNnoiLz4KPC9zdmc+Cg");
}

 .widget-dropdown > select:focus {
    border-color: #64B5F6;
}

 .widget-dropdown > select:disabled {
    opacity: 0.6;
}

 /* To disable the dotted border in Firefox around select controls.
   See http://stackoverflow.com/a/18853002 */

 .widget-dropdown > select:-moz-focusring {
    color: transparent;
    text-shadow: 0 0 0 #000;
}

 /* Select and SelectMultiple */

 .widget-select {
    width: 300px;
    line-height: 28px;

    /* Because Firefox defines the baseline of a select as the bottom of the
    control, we align the entire control to the top and add padding to the
    select to get an approximate first line baseline alignment. */
    -webkit-box-align: start;
        -ms-flex-align: start;
            align-items: flex-start;
}

 .widget-select > select {
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    outline: none !important;
    overflow: auto;
    height: inherit;

    /* Because Firefox defines the baseline of a select as the bottom of the
    control, we align the entire control to the top and add padding to the
    select to get an approximate first line baseline alignment. */
    padding-top: 5px;
}

 .widget-select > select:focus {
    border-color: #64B5F6;
}

 .wiget-select > select > option {
    padding-left: 4px;
    line-height: 28px;
    /* line-height doesn't work on some browsers for select options */
    padding-top: calc(28px - var(--jp-widgets-font-size) / 2);
    padding-bottom: calc(28px - var(--jp-widgets-font-size) / 2);
}

 /* Toggle Buttons Styling */

 .widget-toggle-buttons {
    line-height: 28px;
}

 .widget-toggle-buttons .widget-toggle-button {
    margin-left: 2px;
    margin-right: 2px;
}

 .widget-toggle-buttons .jupyter-button:disabled {
    opacity: 0.6;
}

 /* Radio Buttons Styling */

 .widget-radio {
    width: 300px;
    line-height: 28px;
}

 .widget-radio-box {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-bottom: 8px;
}

 .widget-radio-box label {
    height: 20px;
    line-height: 20px;
    font-size: 13px;
}

 .widget-radio-box input {
    height: 20px;
    line-height: 20px;
    margin: 0 8px 0 1px;
    float: left;
}

 /* Color Picker Styling */

 .widget-colorpicker {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-colorpicker > .widget-colorpicker-input {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    min-width: 72px;
}

 .widget-colorpicker input[type="color"] {
    width: 28px;
    height: 28px;
    padding: 0 2px; /* make the color square actually square on Chrome on OS X */
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    border-left: none;
    -webkit-box-flex: 0;
        -ms-flex-positive: 0;
            flex-grow: 0;
    -ms-flex-negative: 0;
        flex-shrink: 0;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    -ms-flex-item-align: stretch;
        align-self: stretch;
    outline: none !important;
}

 .widget-colorpicker.concise input[type="color"] {
    border-left: 1px solid #9E9E9E;
}

 .widget-colorpicker input[type="color"]:focus, .widget-colorpicker input[type="text"]:focus {
    border-color: #64B5F6;
}

 .widget-colorpicker input[type="text"] {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    outline: none !important;
    height: 28px;
    line-height: 28px;
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    font-size: 13px;
    padding: 4px 8px;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -ms-flex-negative: 1;
        flex-shrink: 1;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
}

 .widget-colorpicker input[type="text"]:disabled {
    opacity: 0.6;
}

 /* Date Picker Styling */

 .widget-datepicker {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-datepicker input[type="date"] {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    outline: none !important;
    height: 28px;
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    padding: 4px 8px;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
}

 .widget-datepicker input[type="date"]:focus {
    border-color: #64B5F6;
}

 .widget-datepicker input[type="date"]:invalid {
    border-color: #FF9800;
}

 .widget-datepicker input[type="date"]:disabled {
    opacity: 0.6;
}

 /* Play Widget */

 .widget-play {
    width: 148px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .widget-play .jupyter-button {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    height: auto;
}

 .widget-play .jupyter-button:disabled {
    opacity: 0.6;
}

 /* Tab Widget */

 .jupyter-widgets.widget-tab {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar {
    /* Necessary so that a tab can be shifted down to overlay the border of the box below. */
    overflow-x: visible;
    overflow-y: visible;
}

 .jupyter-widgets.widget-tab > .p-TabBar > .p-TabBar-content {
    /* Make sure that the tab grows from bottom up */
    -webkit-box-align: end;
        -ms-flex-align: end;
            align-items: flex-end;
    min-width: 0;
    min-height: 0;
}

 .jupyter-widgets.widget-tab > .widget-tab-contents {
    width: 100%;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    margin: 0;
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    padding: 15px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    overflow: auto;
}

 .jupyter-widgets.widget-tab > .p-TabBar {
    font: 13px Helvetica, Arial, sans-serif;
    min-height: 25px;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab {
    -webkit-box-flex: 0;
        -ms-flex: 0 1 144px;
            flex: 0 1 144px;
    min-width: 35px;
    min-height: 25px;
    line-height: 24px;
    margin-left: -1px;
    padding: 0px 10px;
    background: #EEEEEE;
    color: rgba(0, 0, 0, .5);
    border: 1px solid #9E9E9E;
    border-bottom: none;
    position: relative;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-current {
    color: rgba(0, 0, 0, 1.0);
    /* We want the background to match the tab content background */
    background: white;
    min-height: 26px;
    -webkit-transform: translateY(1px);
            transform: translateY(1px);
    overflow: visible;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-current:before {
    position: absolute;
    top: -1px;
    left: -1px;
    content: '';
    height: 2px;
    width: calc(100% + 2px);
    background: #2196F3;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab:first-child {
    margin-left: 0;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab:hover:not(.p-mod-current) {
    background: white;
    color: rgba(0, 0, 0, .8);
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-mod-closable > .p-TabBar-tabCloseIcon {
    margin-left: 4px;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-mod-closable > .p-TabBar-tabCloseIcon:before {
    font-family: FontAwesome;
    content: '\F00D'; /* close */
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabIcon,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabLabel,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabCloseIcon {
    line-height: 24px;
}

 /* Accordion Widget */

 .p-Collapse {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .p-Collapse-header {
    padding: 4px;
    cursor: pointer;
    color: rgba(0, 0, 0, .5);
    background-color: #EEEEEE;
    border: 1px solid #9E9E9E;
    padding: 10px 15px;
    font-weight: bold;
}

 .p-Collapse-header:hover {
    background-color: white;
    color: rgba(0, 0, 0, .8);
}

 .p-Collapse-open > .p-Collapse-header {
    background-color: white;
    color: rgba(0, 0, 0, 1.0);
    cursor: default;
    border-bottom: none;
}

 .p-Collapse .p-Collapse-header::before {
    content: '\F0DA\A0';  /* caret-right, non-breaking space */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

 .p-Collapse-open > .p-Collapse-header::before {
    content: '\F0D7\A0'; /* caret-down, non-breaking space */
}

 .p-Collapse-contents {
    padding: 15px;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    border-left: 1px solid #9E9E9E;
    border-right: 1px solid #9E9E9E;
    border-bottom: 1px solid #9E9E9E;
    overflow: auto;
}

 .p-Accordion {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .p-Accordion .p-Collapse {
    margin-bottom: 0;
}

 .p-Accordion .p-Collapse + .p-Collapse {
    margin-top: 4px;
}

 /* HTML widget */

 .widget-html, .widget-htmlmath {
    font-size: 13px;
}

 .widget-html > .widget-html-content, .widget-htmlmath > .widget-html-content {
    /* Fill out the area in the HTML widget */
    -ms-flex-item-align: stretch;
        align-self: stretch;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    /* Makes sure the baseline is still aligned with other elements */
    line-height: 28px;
    /* Make it possible to have absolutely-positioned elements in the html */
    position: relative;
}
</style><link id="favicon" type="image/x-icon" rel="shortcut icon" href="http://localhost:8888/static/base/images/favicon-notebook.ico"><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/varInspector/jquery.tablesorter.min" src="./README_files/jquery.tablesorter.min.js.download"></script></head>

<body class="notebook_app command_mode" data-jupyter-api-token="2150ec7615b4bd606dba5e6ee1da8c2f45f78eb635aed1aa" data-base-url="/" data-ws-url="" data-notebook-name="Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb" data-notebook-path="Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb" dir="ltr" style=""><div style="visibility: hidden; overflow: hidden; position: absolute; top: 0px; height: 1px; width: auto; padding: 0px; border: 0px; margin: 0px; text-align: left; text-indent: 0px; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal;"><div id="MathJax_Hidden"></div></div><div id="MathJax_Message" style="display: none;"></div>

<noscript>
    <div id='noscript'>
      Jupyter Notebook requires JavaScript.<br>
      Please enable it to proceed. 
  </div>
</noscript>

<div id="header" style="display: block;">
  <div id="header-container" class="container">
  <div id="ipython_notebook" class="nav navbar-brand"><a href="http://localhost:8888/tree?token=2150ec7615b4bd606dba5e6ee1da8c2f45f78eb635aed1aa" title="dashboard">
      <img src="./README_files/logo.png" alt="Jupyter Notebook">
  </a></div>

  


<span id="save_widget" class="save_widget">
    <span id="notebook_name" class="filename">Breast_Cancer_Wisconsin_Diagnostic_Project</span>
    <span class="checkpoint_status" title="mar. 19 févr. 2019 15:01">Last Checkpoint: il y a 3 minutes</span>
    <span class="autosave_status">(autosaved)</span>
<i id="notebook-trusted-indicator" class="fa notebook-trusted fa-check" title="Notebook is trusted"></i></span>

<span id="kernel_logo_widget">
  
  <img class="current_kernel_logo" alt="Current Kernel Logo" src="./README_files/logo-64x64.png" title="Python 3" style="display: inline;">
  
</span>


  
  
  
  

    <span id="login_widget">
      
        <button id="logout" class="btn btn-sm navbar-btn">Logout</button>
      
    </span>

  

  
  
  </div>
  <div class="header-bar"></div>

  
<div id="menubar-container" class="container">
<div id="menubar">
    <div id="menus" class="navbar navbar-default" role="navigation">
        <div class="container-fluid">
            <button type="button" class="btn btn-default navbar-btn navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
              <i class="fa fa-bars"></i>
              <span class="navbar-text">Menu</span>
            </button>
            <p id="kernel_indicator" class="navbar-text indicator_area">
              <span class="kernel_indicator_name">Python 3</span>
              <i id="kernel_indicator_icon" class="kernel_idle_icon" title="Kernel Idle"></i>
            </p>
            <i id="readonly-indicator" class="navbar-text" title="This notebook is read-only" style="display: none;">
                <span class="fa-stack">
                    <i class="fa fa-save fa-stack-1x"></i>
                    <i class="fa fa-ban fa-stack-2x text-danger"></i>
                </span>
            </i>
            <i id="modal_indicator" class="navbar-text modal_indicator" title="Command Mode"></i>
            <span id="notification_area"><div id="notification_kernel" class="notification_widget btn btn-xs navbar-btn undefined info" style="display: none;"><span></span></div><div id="notification_notebook" class="notification_widget btn btn-xs navbar-btn" style="display: none;"><span></span></div><div id="notification_trusted" class="notification_widget btn btn-xs navbar-btn" style="cursor: help;" disabled="disabled"><span title="Javascript enabled for notebook display">Trusted</span></div><div id="notification_widgets" class="notification_widget btn btn-xs navbar-btn" style="display: none;"><span></span></div></span>
            <div class="navbar-collapse collapse">
              <ul class="nav navbar-nav">
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown" aria-expanded="false">File</a>
                    <ul id="file_menu" class="dropdown-menu">
                        <li id="new_notebook" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">New Notebook</a>
                            <ul class="dropdown-menu" id="menu-new-notebook-submenu"><li id="new-notebook-submenu-python3"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Python 3</a></li></ul>
                        </li>
                        <li id="open_notebook" title="Opens a new window with the Dashboard view">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Open...</a></li>
                        <!-- <hr/> -->
                        <li class="divider"></li>
                        <li id="copy_notebook" title="Open a copy of this notebook&#39;s contents and start a new kernel">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Make a Copy...</a></li>
                        <li id="save_notebook_as" title="Save a copy of the notebook&#39;s contents and start a new kernel">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Save as...</a></li>
                        <li id="rename_notebook"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Rename...</a></li>
                        <li id="save_checkpoint"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Save and Checkpoint</a></li>
                        <!-- <hr/> -->
                        <li class="divider"></li>
                        <li id="restore_checkpoint" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Revert to Checkpoint</a>
                          <ul class="dropdown-menu"><li><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">mardi 19 février 2019 15:01</a></li></ul>
                        </li>
                        <li class="divider"></li>
                        <li id="print_preview"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Print Preview</a></li>
                        <li class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Download as</a>
                            <ul id="download_menu" class="dropdown-menu">
                                <li id="download_ipynb"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Notebook (.ipynb)</a></li>
                                <li id="download_script"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Python (.py)</a></li>
                                <li id="download_html"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">HTML (.html)</a></li>
                                <li id="download_slides"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Reveal.js slides (.html)</a></li>
                                <li id="download_markdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Markdown (.md)</a></li>
                                <li id="download_rst"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">reST (.rst)</a></li>
                                <li id="download_latex"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">LaTeX (.tex)</a></li>
                                <li id="download_pdf"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">PDF via LaTeX (.pdf)</a></li>
                                
                                <li id="download_asciidoc">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">asciidoc (.asciidoc)</a>
                                </li>
                                
                                <li id="download_custom">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.txt)</a>
                                </li>
                                
                                <li id="download_html">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_ch">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_embed">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_toc">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_with_toclenvs">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_latex">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">latex (.tex)</a>
                                </li>
                                
                                <li id="download_latex_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">latex (.tex)</a>
                                </li>
                                
                                <li id="download_markdown">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">markdown (.md)</a>
                                </li>
                                
                                <li id="download_notebook">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">notebook (.ipynb)</a>
                                </li>
                                
                                <li id="download_pdf">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">pdf (.tex)</a>
                                </li>
                                
                                <li id="download_python">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">python (.py)</a>
                                </li>
                                
                                <li id="download_rst">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">rst (.rst)</a>
                                </li>
                                
                                <li id="download_script">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">custom (.txt)</a>
                                </li>
                                
                                <li id="download_selectLanguage">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">notebook (.ipynb)</a>
                                </li>
                                
                                <li id="download_slides">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">slides (.slides.html)</a>
                                </li>
                                
                                <li id="download_slides_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">slides (.slides.html)</a>
                                </li>
                                
                            <li id="download_html_embed"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">HTML Embedded (.html)</a></li></ul>
                        </li>
                        <li class="dropdown-submenu hidden"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Deploy as</a>
                            <ul id="deploy_menu" class="dropdown-menu"></ul>
                        </li>
                        <li class="divider"></li>
                        <li id="trust_notebook" title="Trust the output of this notebook" class="disabled">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Trusted Notebook</a></li>
                        <li class="divider"></li>
                        <li id="close_and_halt" title="Shutdown this notebook&#39;s kernel, and close this window">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Close and Halt</a></li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Edit</a>
                    <ul id="edit_menu" class="dropdown-menu">
                        <li id="cut_cell"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Cut Cells</a></li>
                        <li id="copy_cell"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Copy Cells</a></li>
                        <li id="paste_cell_above" class="disabled"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Paste Cells Above</a></li>
                        <li id="paste_cell_below" class="disabled"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Paste Cells Below</a></li>
                        <li id="paste_cell_replace" class="disabled"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Paste Cells &amp; Replace</a></li>
                        <li id="delete_cell"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Delete Cells</a></li>
                        <li id="undelete_cell" class="disabled"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Undo Delete Cells</a></li>
                        <li class="divider"></li>
                        <li id="split_cell"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Split Cell</a></li>
                        <li id="merge_cell_above"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Merge Cell Above</a></li>
                        <li id="merge_cell_below"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Merge Cell Below</a></li>
                        <li class="divider"></li>
                        <li id="move_cell_up"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Move Cell Up</a></li>
                        <li id="move_cell_down"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Move Cell Down</a></li>
                        <li class="divider"></li>
                        <li id="edit_nb_metadata"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Edit Notebook Metadata</a></li>
                        <li class="divider"></li>
                        <li id="find_and_replace"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#"> Find and Replace </a></li>
                        <li class="divider"></li>
                        <li id="cut_cell_attachments"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Cut Cell Attachments</a></li>
                        <li id="copy_cell_attachments"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Copy Cell Attachments</a></li>
                        <li id="paste_cell_attachments" class="disabled"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Paste Cell Attachments</a></li>
                        <li class="divider"></li>
                        <li id="insert_image" class="disabled"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#"> Insert Image </a></li>
                    <li class="divider"></li><li><a target="_blank" title="Opens in a new window" href="http://localhost:8888/nbextensions/"> <i class="fa fa-cogs menu-icon pull-right"></i><span>nbextensions config</span></a></li></ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">View</a>
                    <ul id="view_menu" class="dropdown-menu">
                        <li id="toggle_header" title="Show/Hide the logo and notebook title (above menu bar)">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Toggle Header</a>
                        </li>
                        <li id="toggle_toolbar" title="Show/Hide the action icons (below menu bar)">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Toggle Toolbar</a>
                        </li>
                        <li id="toggle_line_numbers" title="Show/Hide line numbers in cells">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Toggle Line Numbers</a>
                        </li>
                        <li id="menu-cell-toolbar" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Cell Toolbar</a>
                            <ul class="dropdown-menu" id="menu-cell-toolbar-submenu"><li data-name="None"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">None</a></li><li data-name="Edit%20Metadata"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Edit Metadata</a></li><li data-name="Raw%20Cell%20Format"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Raw Cell Format</a></li><li data-name="Slideshow"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Slideshow</a></li><li data-name="Attachments"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Attachments</a></li><li data-name="Tags"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Tags</a></li></ul>
                        </li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Insert</a>
                    <ul id="insert_menu" class="dropdown-menu">
                        <li id="insert_cell_above" title="Insert an empty Code cell above the currently active cell">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Insert Cell Above</a></li>
                        <li id="insert_cell_below" title="Insert an empty Code cell below the currently active cell">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Insert Cell Below</a></li>
                    <li class="divider"></li><li><a title="Insert a heading cell above the selected cell" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Insert Heading Above</a></li><li><a title="Insert a heading cell below the selected cell&#39;s section" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Insert Heading Below</a></li></ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Cell</a>
                    <ul id="cell_menu" class="dropdown-menu">
                        <li id="run_cell" title="Run this cell, and move cursor to the next one">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Run Cells</a></li>
                        <li id="run_cell_select_below" title="Run this cell, select below">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Run Cells and Select Below</a></li>
                        <li id="run_cell_insert_below" title="Run this cell, insert below">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Run Cells and Insert Below</a></li>
                        <li id="run_all_cells" title="Run all cells in the notebook">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Run All</a></li>
                        <li id="run_all_cells_above" title="Run all cells above (but not including) this cell">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Run All Above</a></li>
                        <li id="run_all_cells_below" title="Run this cell and all cells below it">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Run All Below</a></li>
                        <li class="divider"></li>
                        <li id="change_cell_type" class="dropdown-submenu" title="All cells in the notebook have a cell type. By default, new cells are created as &#39;Code&#39; cells">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Cell Type</a>
                            <ul class="dropdown-menu">
                              <li id="to_code" title="Contents will be sent to the kernel for execution, and output will display in the footer of cell">
                                  <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Code</a></li>
                              <li id="to_markdown" title="Contents will be rendered as HTML and serve as explanatory text">
                                  <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Markdown</a></li>
                              <li id="to_raw" title="Contents will pass through nbconvert unmodified">
                                  <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Raw NBConvert</a></li>
                            </ul>
                        </li>
                        <li class="divider"></li>
                        <li id="current_outputs" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Current Outputs</a>
                            <ul class="dropdown-menu">
                                <li id="toggle_current_output" title="Hide/Show the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Toggle</a>
                                </li>
                                <li id="toggle_current_output_scroll" title="Scroll the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Toggle Scrolling</a>
                                </li>
                                <li id="clear_current_output" title="Clear the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Clear</a>
                                </li>
                            </ul>
                        </li>
                        <li id="all_outputs" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">All Output</a>
                            <ul class="dropdown-menu">
                                <li id="toggle_all_output" title="Hide/Show the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Toggle</a>
                                </li>
                                <li id="toggle_all_output_scroll" title="Scroll the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Toggle Scrolling</a>
                                </li>
                                <li id="clear_all_output" title="Clear the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Clear</a>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Kernel</a>
                    <ul id="kernel_menu" class="dropdown-menu">
                        <li id="int_kernel" title="Send Keyboard Interrupt (CTRL-C) to the Kernel">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Interrupt</a>
                        </li>
                        <li id="restart_kernel" title="Restart the Kernel">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Restart</a>
                        </li>
                        <li id="restart_clear_output" title="Restart the Kernel and clear all output">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Restart &amp; Clear Output</a>
                        </li>
                        <li id="restart_run_all" title="Restart the Kernel and re-run the notebook">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Restart &amp; Run All</a>
                        </li>
                        <li id="reconnect_kernel" title="Reconnect to the Kernel">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Reconnect</a>
                        </li>
                        <li id="shutdown_kernel" title="Shutdown the Kernel">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Shutdown</a>
                        </li>
                        <li class="divider"></li>
                        <li id="menu-change-kernel" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Change kernel</a>
                            <ul class="dropdown-menu" id="menu-change-kernel-submenu"><li id="kernel-submenu-python3"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Python 3</a></li></ul>
                        </li>
                    </ul>
                </li><li id="Navigate" class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" id="Navigate_sub" class="dropdown-toggle" data-toggle="dropdown">Navigate</a><ul id="Navigate_menu" class="dropdown-menu ui-resizable" style=""><div id="navigate_menu" class="toc" style="width: 160px; height: 0px;"><ul class="toc-item"><li><span><i class="fa fa-fw fa-caret-down"></i><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Project-Overview----KNN" data-toc-modified-id="Project-Overview----KNN-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>Project Overview -- KNN</a></span><ul class="toc-item"><li><ul class="toc-item"><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#1.0.1--Breast-Cancer-Wisconsin-Diagnostic" data-toc-modified-id="1.0.1--Breast-Cancer-Wisconsin-Diagnostic-1.0.1"><span class="toc-item-num">1.0.1&nbsp;&nbsp;</span>1.0.1  Breast Cancer Wisconsin Diagnostic</a></span></li></ul></li></ul></li></ul></div><div class="ui-resizable-handle ui-resizable-e" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div></ul></li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" data-toggle="dropdown" class="dropdown-toggle">Widgets</a><ul id="widget-submenu" class="dropdown-menu"><li title="Save the notebook with the widget state information for static rendering"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Save Notebook Widget State</a></li><li title="Clear the widget state information from the notebook"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Clear Notebook Widget State</a></li><ul class="divider"></ul><li title="Download the widget state as a JSON file"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Download Widget State</a></li><li title="Embed interactive widgets"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Embed Widgets</a></li></ul></li><li class="dropdown"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Help</a>
                    <ul id="help_menu" class="dropdown-menu">
                        
                        <li id="notebook_tour" title="A quick tour of the notebook user interface"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">User Interface Tour</a></li>
                        <li id="keyboard_shortcuts" title="Opens a tooltip with all keyboard shortcuts"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Keyboard Shortcuts</a></li>
                        <li id="edit_keyboard_shortcuts" title="Opens a dialog allowing you to edit Keyboard shortcuts"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">Edit Keyboard Shortcuts</a></li>
                        <li class="divider"></li>
                        

						
                        
                            
                                <li><a rel="noreferrer" href="http://nbviewer.jupyter.org/github/ipython/ipython/blob/3.x/examples/Notebook/Index.ipynb" target="_blank" title="Opens in a new window">
                                
                                    <i class="fa fa-external-link menu-icon pull-right"></i>
                                

                                Notebook Help
                                </a></li>
                            
                                <li><a rel="noreferrer" href="https://help.github.com/articles/markdown-basics/" target="_blank" title="Opens in a new window">
                                
                                    <i class="fa fa-external-link menu-icon pull-right"></i>
                                

                                Markdown
                                </a></li>
                            
                            
                        
                        <li><a title="Jupyter_contrib_nbextensions documentation" id="jupyter_contrib_nbextensions_help" href="http://jupyter-contrib-nbextensions.readthedocs.io/en/latest/" target="_blank">Jupyter-contrib <br> nbextensions<i class="fa fa-external-link menu-icon pull-right"></i></a></li><li id="kernel-help-links" class="divider"></li><li><a target="_blank" title="Opens in a new window" href="https://docs.python.org/3.7?v=20190219085620"><i class="fa fa-external-link menu-icon pull-right"></i><span>Python Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://ipython.org/documentation.html?v=20190219085620"><i class="fa fa-external-link menu-icon pull-right"></i><span>IPython Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://docs.scipy.org/doc/numpy/reference/?v=20190219085620"><i class="fa fa-external-link menu-icon pull-right"></i><span>NumPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://docs.scipy.org/doc/scipy/reference/?v=20190219085620"><i class="fa fa-external-link menu-icon pull-right"></i><span>SciPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://matplotlib.org/contents.html?v=20190219085620"><i class="fa fa-external-link menu-icon pull-right"></i><span>Matplotlib Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="http://docs.sympy.org/latest/index.html?v=20190219085620"><i class="fa fa-external-link menu-icon pull-right"></i><span>SymPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://pandas.pydata.org/pandas-docs/stable/?v=20190219085620"><i class="fa fa-external-link menu-icon pull-right"></i><span>pandas Reference</span></a></li><li class="divider"></li>
                        <li title="About Jupyter Notebook"><a id="notebook_about" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#">About</a></li>
                        
                    </ul>
                </li>
              </ul>
            </div>
        </div>
    </div>
</div>

<div id="maintoolbar" class="navbar">
  <div class="toolbar-inner navbar-inner navbar-nobg">
    <div id="maintoolbar-container" class="container toolbar"><div class="btn-group" id="save-notbook"><button class="btn btn-default" title="Save and Checkpoint" data-jupyter-action="jupyter-notebook:save-notebook"><i class="fa-save fa"></i></button></div><div class="btn-group" id="insert_above_below"><button class="btn btn-default" title="insert cell below" data-jupyter-action="jupyter-notebook:insert-cell-below"><i class="fa-plus fa"></i></button></div><div class="btn-group" id="cut_copy_paste"><button class="btn btn-default" title="cut selected cells" data-jupyter-action="jupyter-notebook:cut-cell"><i class="fa-cut fa"></i></button><button class="btn btn-default" title="copy selected cells" data-jupyter-action="jupyter-notebook:copy-cell"><i class="fa-copy fa"></i></button><button class="btn btn-default" title="paste cells below" data-jupyter-action="jupyter-notebook:paste-cell-below"><i class="fa-paste fa"></i></button></div><div class="btn-group" id="move_up_down"><button class="btn btn-default" title="move selected cells up" data-jupyter-action="jupyter-notebook:move-cell-up"><i class="fa-arrow-up fa"></i></button><button class="btn btn-default" title="move selected cells down" data-jupyter-action="jupyter-notebook:move-cell-down"><i class="fa-arrow-down fa"></i></button></div><div class="btn-group" id="run_int"><button class="btn btn-default" title="Run" data-jupyter-action="jupyter-notebook:run-cell-and-select-next"><i class="fa-step-forward fa"></i><span class="toolbar-btn-label">Run</span></button><button class="btn btn-default" title="interrupt the kernel" data-jupyter-action="jupyter-notebook:interrupt-kernel"><i class="fa-stop fa"></i></button><button class="btn btn-default" title="restart the kernel (with dialog)" data-jupyter-action="jupyter-notebook:confirm-restart-kernel"><i class="fa-repeat fa"></i></button><button class="btn btn-default" title="restart the kernel, then re-run the whole notebook (with dialog)" data-jupyter-action="jupyter-notebook:confirm-restart-kernel-and-run-all-cells"><i class="fa-forward fa"></i></button></div><select id="cell_type" class="form-control select-xs"><option value="code">Code</option><option value="markdown">Markdown</option><option value="raw">Raw NBConvert</option><option value="heading">Heading</option><option value="multiselect" disabled="disabled" style="display: none;">-</option></select><div class="btn-group"><button class="btn btn-default" title="open the command palette" data-jupyter-action="jupyter-notebook:show-command-palette"><i class="fa-keyboard-o fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Variable Inspector" data-jupyter-action="varInspector:toggle-variable-inspector" id="varInspector_button"><i class="fa-crosshairs fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Increase code font size" data-jupyter-action="code_font_size:increase-code-font-size"><i class="fa-search-plus fa"></i></button><button class="btn btn-default" title="Decrease code font size" data-jupyter-action="code_font_size:decrease-code-font-size"><i class="fa-search-minus fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Create/Edit Gist of Notebook" data-jupyter-action="gist_it:create-gist-from-notebook"><i class="fa-github fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Table of Contents" data-jupyter-action="toc2:toggle-toc" id="toc_button"><i class="fa-list fa"></i></button></div><div class="btn-group" id="code_prettify_button"><button class="btn btn-default" title="code_prettify selected cell(s) (add shift for all cells)"><i class="fa-legal fa"></i></button></div><div class="btn-group" id="autopep8_button"><button class="btn btn-default" title="autopep8 selected cell(s) (add shift for all cells)"><i class="fa-legal fa"></i></button></div></div>
  </div>
</div>
</div>

<div class="lower-header-bar"></div>

</div>

<div id="site" style="display: block; height: 603.444px;"><div id="toc-wrapper" style="display: none; position: relative; width: 20%; top: 139.556px; left: 0px;" class="ui-draggable ui-resizable sidebar-wrapper"><div id="toc-header"><span class="header">Contents </span><i class="fa fa-fw hide-btn" title="Hide ToC"></i><i class="fa fa-fw fa-refresh" title="Reload ToC"></i><i class="fa fa-fw fa-cog" title="ToC settings"></i></div><div id="toc" class="toc"><ul class="toc-item"><li><span><i class="fa fa-fw fa-caret-down"></i><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Project-Overview----KNN" data-toc-modified-id="Project-Overview----KNN-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>Project Overview -- KNN</a></span><ul class="toc-item"><li><ul class="toc-item"><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#1.0.1--Breast-Cancer-Wisconsin-Diagnostic" data-toc-modified-id="1.0.1--Breast-Cancer-Wisconsin-Diagnostic-1.0.1"><span class="toc-item-num">1.0.1&nbsp;&nbsp;</span>1.0.1  Breast Cancer Wisconsin Diagnostic</a></span></li></ul></li></ul></li></ul></div><div class="ui-resizable-handle ui-resizable-n" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-e ui-icon ui-icon-grip-dotted-vertical" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-w" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-sw" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-ne" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-nw" style="z-index: 90;"></div></div>


<div id="ipython-main-app">
    <div id="notebook_panel">
        <div id="notebook" tabindex="-1"><div class="container" id="notebook-container"><div class="cell text_cell rendered selected collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h1"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59721px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 33px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 21.3333px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-1"># Project Overview -- KNN</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 33px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 44px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h1 id="Project-Overview----KNN" data-toc-modified-id="Project-Overview----KNN-1"><a class="toc-mod-link" id="Project-Overview----KNN-1"></a><span class="toc-item-num">1&nbsp;&nbsp;</span>Project Overview -- KNN<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Project-Overview----KNN">¶</a></h1>
</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h3"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59721px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 30px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 18.6667px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-3">### 1.0.1  Breast Cancer Wisconsin Diagnostic</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 30px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 41px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h3 id="1.0.1--Breast-Cancer-Wisconsin-Diagnostic" data-toc-modified-id="1.0.1--Breast-Cancer-Wisconsin-Diagnostic-1.0.1"><a class="toc-mod-link" id="1.0.1--Breast-Cancer-Wisconsin-Diagnostic-1.0.1"></a><span class="toc-item-num">1.0.1&nbsp;&nbsp;</span>1.0.1  Breast Cancer Wisconsin Diagnostic<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#1.0.1--Breast-Cancer-Wisconsin-Diagnostic">¶</a></h3>
</div></div></div><div class="cell text_cell unselected rendered" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.5972px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 147px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>4</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">In this project, we are going to work with the real dataset on Breast Cancer Wisconsin (Diagnostic). The dataset is available on kaggle and originally belong to UCI Machine Learning Repository.</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">This dataset was donated to UCI by Nick Street in 1995 for the public use. Relevant Papers and detailed description on the dataset are provided at UCI website.</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">3</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">4</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 147px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 158px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p>In this project, we are going to work with the real dataset on Breast Cancer Wisconsin (Diagnostic). The dataset is available on kaggle and originally belong to UCI Machine Learning Repository.
This dataset was donated to UCI by Nick Street in 1995 for the public use. Relevant Papers and detailed description on the dataset are provided at UCI website.</p>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[2]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.5972px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 247.181px; margin-bottom: -19px; border-right-width: 11px; min-height: 96px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">pandas</span> <span class="cm-keyword">as</span> <span class="cm-variable">pd</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">seaborn</span> <span class="cm-keyword">as</span> <span class="cm-variable">sns</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">3</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">matplotlib</span>.<span class="cm-property">pyplot</span> <span class="cm-keyword">as</span> <span class="cm-variable">plt</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">4</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">numpy</span> <span class="cm-keyword">as</span> <span class="cm-variable">np</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">5</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-operator">%</span><span class="cm-variable">matplotlib</span> <span class="cm-variable">inline</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 96px;"></div><div class="CodeMirror-gutters" style="height: 107px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[3]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 378.028px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span> <span class="cm-operator">=</span> <span class="cm-variable">pd</span>.<span class="cm-property">read_csv</span>(<span class="cm-string">'Breast_Cancer_Diagnostic.csv'</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">columns</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="height: 56px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[3]:</bdi></div><div class="output_subarea output_text output_result"><pre>Index(['id', 'diagnosis', 'radius_mean', 'texture_mean', 'perimeter_mean',
       'area_mean', 'smoothness_mean', 'compactness_mean', 'concavity_mean',
       'concave points_mean', 'symmetry_mean', 'fractal_dimension_mean',
       'radius_se', 'texture_se', 'perimeter_se', 'area_se', 'smoothness_se',
       'compactness_se', 'concavity_se', 'concave points_se', 'symmetry_se',
       'fractal_dimension_se', 'radius_worst', 'texture_worst',
       'perimeter_worst', 'area_worst', 'smoothness_worst',
       'compactness_worst', 'concavity_worst', 'concave points_worst',
       'symmetry_worst', 'fractal_dimension_worst', 'Unnamed: 32'],
      dtype='object')</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### We will only consider ten real-valued features in this project for diagnostic.</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="We-will-only-consider-ten-real-valued-features-in-this-project-for-diagnostic.">We will only consider ten real-valued features in this project for diagnostic.<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#We-will-only-consider-ten-real-valued-features-in-this-project-for-diagnostic.">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[4]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true" style="display: block; right: 0px; left: 46px;"><div style="height: 100%; min-height: 1px; width: 663px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 662.556px; margin-bottom: -19px; border-right-width: 11px; min-height: 79px; padding-right: 0px; padding-bottom: 19px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div><div class="CodeMirror-gutter-elt" style="left: 33px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[[<span class="cm-string">'radius_mean'</span>, <span class="cm-string">'texture_mean'</span>, <span class="cm-string">'perimeter_mean'</span>,</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">       <span class="cm-string">'area_mean'</span>, <span class="cm-string">'smoothness_mean'</span>, <span class="cm-string">'compactness_mean'</span>, <span class="cm-string">'concavity_mean'</span>,</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">3</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">       <span class="cm-string">'concave points_mean'</span>, <span class="cm-string">'symmetry_mean'</span>, <span class="cm-string">'fractal_dimension_mean'</span>,<span class="cm-string">'diagnosis'</span>]]</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">4</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">head</span>()</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 19px solid transparent; top: 79px;"></div><div class="CodeMirror-gutters" style="height: 109px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[4]:</bdi></div><div class="output_subarea output_html rendered_html output_result"><div>
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
      <th>radius_mean</th>
      <th>texture_mean</th>
      <th>perimeter_mean</th>
      <th>area_mean</th>
      <th>smoothness_mean</th>
      <th>compactness_mean</th>
      <th>concavity_mean</th>
      <th>concave points_mean</th>
      <th>symmetry_mean</th>
      <th>fractal_dimension_mean</th>
      <th>diagnosis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17.99</td>
      <td>10.38</td>
      <td>122.80</td>
      <td>1001.0</td>
      <td>0.11840</td>
      <td>0.27760</td>
      <td>0.3001</td>
      <td>0.14710</td>
      <td>0.2419</td>
      <td>0.07871</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20.57</td>
      <td>17.77</td>
      <td>132.90</td>
      <td>1326.0</td>
      <td>0.08474</td>
      <td>0.07864</td>
      <td>0.0869</td>
      <td>0.07017</td>
      <td>0.1812</td>
      <td>0.05667</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>19.69</td>
      <td>21.25</td>
      <td>130.00</td>
      <td>1203.0</td>
      <td>0.10960</td>
      <td>0.15990</td>
      <td>0.1974</td>
      <td>0.12790</td>
      <td>0.2069</td>
      <td>0.05999</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.42</td>
      <td>20.38</td>
      <td>77.58</td>
      <td>386.1</td>
      <td>0.14250</td>
      <td>0.28390</td>
      <td>0.2414</td>
      <td>0.10520</td>
      <td>0.2597</td>
      <td>0.09744</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20.29</td>
      <td>14.34</td>
      <td>135.10</td>
      <td>1297.0</td>
      <td>0.10030</td>
      <td>0.13280</td>
      <td>0.1980</td>
      <td>0.10430</td>
      <td>0.1809</td>
      <td>0.05883</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's get an overview of our data using info(), and let's check if there are any missing values.</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 58px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-get-an-overview-of-our-data-using-info(),-and-let&#39;s-check-if-there-are-any-missing-values.">Let's get an overview of our data using info(), and let's check if there are any missing values.<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-get-an-overview-of-our-data-using-info(),-and-let&#39;s-check-if-there-are-any-missing-values.">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[5]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 77.6667px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">info</span>()</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_text output_stream output_stdout"><pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 569 entries, 0 to 568
Data columns (total 11 columns):
radius_mean               569 non-null float64
texture_mean              569 non-null float64
perimeter_mean            569 non-null float64
area_mean                 569 non-null float64
smoothness_mean           569 non-null float64
compactness_mean          569 non-null float64
concavity_mean            569 non-null float64
concave points_mean       569 non-null float64
symmetry_mean             569 non-null float64
fractal_dimension_mean    569 non-null float64
diagnosis                 569 non-null object
dtypes: float64(10), object(1)
memory usage: 49.0+ KB
</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59729px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's see which type cancer is common</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-see-which-type-cancer-is-common">Let's see which type cancer is common<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-see-which-type-cancer-is-common">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[9]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 239.444px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>[<span class="cm-string">'diagnosis'</span>].<span class="cm-property">value_counts</span>()</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[9]:</bdi></div><div class="output_subarea output_text output_result"><pre>B    357
M    212
Name: diagnosis, dtype: int64</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59729px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's standardize the variable/features to get your data ready for knn</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-standardize-the-variable/features-to-get-your-data-ready-for-knn">Let's standardize the variable/features to get your data ready for knn<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-standardize-the-variable/features-to-get-your-data-ready-for-knn">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[10]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59729px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 378.014px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">preprocessing</span> <span class="cm-keyword">import</span> <span class="cm-variable">StandardScaler</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's create a scaler</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-create-a-scaler">Let's create a scaler<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-create-a-scaler">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[12]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59729px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 201px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">scaler</span> <span class="cm-operator">=</span> <span class="cm-variable">StandardScaler</span>()</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's split data into features and target to fit scaler to the features only.</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-split-data-into-features-and-target-to-fit-scaler-to-the-features-only.">Let's split data into features and target to fit scaler to the features only.<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-split-data-into-features-and-target-to-fit-scaler-to-the-features-only.">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[13]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 324.111px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">features</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>.<span class="cm-property">drop</span>(<span class="cm-string">'diagnosis'</span>, <span class="cm-variable">axis</span> <span class="cm-operator">=</span> <span class="cm-number">1</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">target</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[<span class="cm-string">'diagnosis'</span>]</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="height: 56px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Fitting scaler to the features</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Fitting-scaler-to-the-features">Fitting scaler to the features<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Fitting-scaler-to-the-features">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[14]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 162.514px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">scaler</span>.<span class="cm-property">fit</span>(<span class="cm-variable">features</span>)</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[14]:</bdi></div><div class="output_subarea output_text output_result"><pre>StandardScaler(copy=True, with_mean=True, with_std=True)</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's get the scaled features into scaled_features</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-get-the-scaled-features-into-scaled_features">Let's get the scaled features into scaled_features<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-get-the-scaled-features-into-scaled_features">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[16]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 347.236px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">scaled_features</span> <span class="cm-operator">=</span> <span class="cm-variable">scaler</span>.<span class="cm-property">transform</span>(<span class="cm-variable">features</span>)</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's do the train_test_split by using test_size = 0.33, random_state = 42</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-do-the-train_test_split-by-using-test_size-=-0.33,-random_state-=-42">Let's do the train_test_split by using test_size = 0.33, random_state = 42<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-do-the-train_test_split-by-using-test_size-=-0.33,-random_state-=-42">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[22]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true" style="display: block; right: 0px; left: 46px;"><div style="height: 100%; min-height: 1px; width: 678px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 678.194px; margin-bottom: -19px; border-right-width: 11px; min-height: 96px; padding-right: 0px; padding-bottom: 19px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">model_selection</span> <span class="cm-keyword">import</span> <span class="cm-variable">train_test_split</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">X</span> <span class="cm-operator">=</span> <span class="cm-variable">scaled_features</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">3</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">y</span> <span class="cm-operator">=</span> <span class="cm-variable">target</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">4</div><div class="CodeMirror-gutter-elt" style="left: 33px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">X_train</span>, <span class="cm-variable">X_test</span>, <span class="cm-variable">y_train</span>, <span class="cm-variable">y_test</span> <span class="cm-operator">=</span> <span class="cm-variable">train_test_split</span>(<span class="cm-variable">X</span>,</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">5</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">                                                    <span class="cm-variable">y</span>, <span class="cm-variable">test_size</span><span class="cm-operator">=</span><span class="cm-number">0.33</span>, <span class="cm-variable">random_state</span><span class="cm-operator">=</span><span class="cm-number">42</span>)</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 19px solid transparent; top: 96px;"></div><div class="CodeMirror-gutters" style="height: 126px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's import the KNeighborsClassifier</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-import-the-KNeighborsClassifier">Let's import the KNeighborsClassifier<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-import-the-KNeighborsClassifier">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[23]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 393.222px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">neighbors</span> <span class="cm-keyword">import</span> <span class="cm-variable">KNeighborsClassifier</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's create a KNN model instance with n_neighbors=1</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-create-a-KNN-model-instance-with-n_neighbors=1">Let's create a KNN model instance with n_neighbors=1<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-create-a-KNN-model-instance-with-n_neighbors=1">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[24]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 324.153px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">knn</span> <span class="cm-operator">=</span> <span class="cm-variable">KNeighborsClassifier</span>(<span class="cm-variable">n_neighbors</span><span class="cm-operator">=</span><span class="cm-number">1</span>)</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's fit the model to training data</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-fit-the-model-to-training-data">Let's fit the model to training data<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-fit-the-model-to-training-data">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[25]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 200.986px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">knn</span>.<span class="cm-property">fit</span>(<span class="cm-variable">X_train</span>, <span class="cm-variable">y_train</span>)</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[25]:</bdi></div><div class="output_subarea output_text output_result"><pre>KNeighborsClassifier(algorithm='auto', leaf_size=30, metric='minkowski',
           metric_params=None, n_jobs=None, n_neighbors=1, p=2,
           weights='uniform')</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's do the prediction for the data test</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-do-the-prediction-for-the-data-test">Let's do the prediction for the data test<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-do-the-prediction-for-the-data-test">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[27]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 262.569px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">predictions</span> <span class="cm-operator">=</span> <span class="cm-variable">knn</span>.<span class="cm-property">predict</span>(<span class="cm-variable">X_test</span>)</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's print the Confusion matrix and the classifier report</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-print-the-Confusion-matrix-and-the-classifier-report">Let's print the Confusion matrix and the classifier report<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-print-the-Confusion-matrix-and-the-classifier-report">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[31]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 523.889px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">metrics</span> <span class="cm-keyword">import</span> <span class="cm-variable">classification_report</span>, <span class="cm-variable">confusion_matrix</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[32]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 385.736px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-builtin">print</span>(<span class="cm-variable">classification_report</span>(<span class="cm-variable">y_test</span>, <span class="cm-variable">predictions</span>))</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-builtin">print</span>(<span class="cm-variable">confusion_matrix</span>(<span class="cm-variable">y_test</span>, <span class="cm-variable">predictions</span>))</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="height: 56px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_text output_stream output_stdout"><pre>              precision    recall  f1-score   support

           B       0.95      0.94      0.95       121
           M       0.90      0.91      0.90        67

   micro avg       0.93      0.93      0.93       188
   macro avg       0.92      0.93      0.92       188
weighted avg       0.93      0.93      0.93       188

[[114   7]
 [  6  61]]
</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's use the Elbow method, and find the best value of k</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-use-the-Elbow-method,-and-find-the-best-value-of-k">Let's use the Elbow method, and find the best value of k<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-use-the-Elbow-method,-and-find-the-best-value-of-k">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[36]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 354.931px; margin-bottom: -19px; border-right-width: 11px; min-height: 130px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">err_rate</span> <span class="cm-operator">=</span> []</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div><div class="CodeMirror-gutter-elt" style="left: 33px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">for</span> <span class="cm-variable">i</span> <span class="cm-keyword">in</span> <span class="cm-builtin">range</span>(<span class="cm-number">1</span>,<span class="cm-number">100</span>):</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">3</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">knn</span> <span class="cm-operator">=</span> <span class="cm-variable">KNeighborsClassifier</span>(<span class="cm-variable">n_neighbors</span><span class="cm-operator">=</span><span class="cm-variable">i</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">4</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">knn</span>.<span class="cm-property">fit</span>(<span class="cm-variable">X_train</span>,<span class="cm-variable">y_train</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">5</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">pred_i</span> <span class="cm-operator">=</span> <span class="cm-variable">knn</span>.<span class="cm-property">predict</span>(<span class="cm-variable">X_test</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">6</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    </span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">7</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">err_rate</span>.<span class="cm-property">append</span>(<span class="cm-variable">np</span>.<span class="cm-property">mean</span>(<span class="cm-variable">pred_i</span> <span class="cm-operator">!=</span><span class="cm-variable">y_test</span>))</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 130px;"></div><div class="CodeMirror-gutters" style="height: 141px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's plot the error rate Vs k to see wich value have the lowest error rate</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-plot-the-error-rate-Vs-k-to-see-wich-value-have-the-lowest-error-rate">Let's plot the error rate Vs k to see wich value have the lowest error rate<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-plot-the-error-rate-Vs-k-to-see-wich-value-have-the-lowest-error-rate">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[37]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 377.986px; margin-bottom: -19px; border-right-width: 11px; min-height: 147px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">figure</span>(<span class="cm-variable">figsize</span><span class="cm-operator">=</span>(<span class="cm-number">16</span>,<span class="cm-number">6</span>))</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div><div class="CodeMirror-gutter-elt" style="left: 33px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">plot</span>(<span class="cm-builtin">range</span>(<span class="cm-number">1</span>,<span class="cm-number">100</span>), <span class="cm-variable">err_rate</span>, <span class="cm-variable">color</span> <span class="cm-operator">=</span><span class="cm-string">'green'</span>,</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">3</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">        <span class="cm-variable">marker</span> <span class="cm-operator">=</span><span class="cm-string">'o'</span>, <span class="cm-variable">markerfacecolor</span> <span class="cm-operator">=</span> <span class="cm-string">'blue'</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">4</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">title</span>(<span class="cm-string">'Error Rate vs. K Value'</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">5</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">xlabel</span>(<span class="cm-string">'K_Value'</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">6</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">ylabel</span>(<span class="cm-string">'Error_Rate'</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">7</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">8</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span>()</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 147px;"></div><div class="CodeMirror-gutters" style="height: 158px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,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"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's use k for the minimum error rate, do the predictions and print confusion matrix and classification report</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 58px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-use-k-for-the-minimum-error-rate,-do-the-predictions-and-print-confusion-matrix-and-classification-report">Let's use k for the minimum error rate, do the predictions and print confusion matrix and classification report<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#Let&#39;s-use-k-for-the-minimum-error-rate,-do-the-predictions-and-print-confusion-matrix-and-classification-report">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[38]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59741px; left: 51.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 385.736px; margin-bottom: -19px; border-right-width: 11px; min-height: 96px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">knn</span> <span class="cm-operator">=</span> <span class="cm-variable">KNeighborsClassifier</span>(<span class="cm-variable">n_neighbors</span><span class="cm-operator">=</span><span class="cm-number">17</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">2</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">knn</span>.<span class="cm-property">fit</span>(<span class="cm-variable">X_train</span>,<span class="cm-variable">y_train</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">3</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">predictions</span> <span class="cm-operator">=</span> <span class="cm-variable">knn</span>.<span class="cm-property">predict</span>(<span class="cm-variable">X_test</span>)</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">4</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-builtin">print</span>(<span class="cm-variable">classification_report</span>(<span class="cm-variable">y_test</span>, <span class="cm-variable">predictions</span>))</span></pre></div><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">5</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-builtin">print</span>(<span class="cm-variable">confusion_matrix</span>(<span class="cm-variable">y_test</span>, <span class="cm-variable">predictions</span>))</span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 96px;"></div><div class="CodeMirror-gutters" style="height: 107px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_text output_stream output_stdout"><pre>              precision    recall  f1-score   support

           B       0.97      0.98      0.97       121
           M       0.95      0.94      0.95        67

   micro avg       0.96      0.96      0.96       188
   macro avg       0.96      0.96      0.96       188
weighted avg       0.96      0.96      0.96       188

[[118   3]
 [  4  63]]
</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell unselected rendered collapsible_headings_ellipsis" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 39.3333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 34px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -34px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### More data we have better we can train our model.</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 40px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="More-data-we-have-better-we-can-train-our-model.">More data we have better we can train our model.<a class="anchor-link" href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#More-data-we-have-better-we-can-train-our-model.">¶</a></h5>
</div></div></div><div class="cell code_cell unselected rendered" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[&nbsp;]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 51.5972px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 46px; min-width: 8.59723px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><div class="CodeMirror-linenumber CodeMirror-gutter-elt"><div>1</div></div></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 5.59723px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -46px;"><div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="left: 0px; width: 21px;">1</div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre></div></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="height: 39px; left: 0px;"><div class="CodeMirror-gutter CodeMirror-linenumbers" style="width: 33px;"></div><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div></div><div class="end_space"></div></div>
        <div id="tooltip" class="ipython_tooltip" style="display:none"><div class="tooltipbuttons"><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" role="button" class="ui-button"><span class="ui-icon ui-icon-close">Close</span></a><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="ui-corner-all" role="button" id="expanbutton" title="Grow the tooltip vertically (press shift-tab twice)"><span class="ui-icon ui-icon-plus">Expand</span></a><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" role="button" class="ui-button" title="show the current docstring in pager (press shift-tab 4 times)"><span class="ui-icon ui-icon-arrowstop-l-n">Open in Pager</span></a><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" role="button" class="ui-button" title="Tooltip will linger for 10 seconds while you type" style="display: none;"><span class="ui-icon ui-icon-clock">Close</span></a></div><div class="pretooltiparrow"></div><div class="tooltiptext smalltooltip"></div></div>
    </div>
</div>



</div>



<div id="pager" class="ui-resizable">
    <div id="pager-contents">
        <div id="pager-container" class="container"></div>
    </div>
    <div id="pager-button-area"><a role="button" title="Open the pager in an external window" class="ui-button"><span class="ui-icon ui-icon-extlink"></span></a><a role="button" title="Close the pager" class="ui-button"><span class="ui-icon ui-icon-close"></span></a></div>
<div class="ui-resizable-handle ui-resizable-n" style="z-index: 90;"></div></div>






<script type="text/javascript">
    sys_info = {"notebook_version": "5.6.0", "notebook_path": "C:\\Users\\Stevy\\Anaconda3\\lib\\site-packages\\notebook", "commit_source": "", "commit_hash": "", "sys_version": "3.7.0 (default, Jun 28 2018, 08:04:48) [MSC v.1912 64 bit (AMD64)]", "sys_executable": "C:\\Users\\Stevy\\Anaconda3\\python.exe", "sys_platform": "win32", "platform": "Windows-10-10.0.17134-SP0", "os_name": "nt", "default_encoding": "utf-8"};
</script>

<script src="./README_files/encoding.js.download" charset="utf-8"></script>

<script src="./README_files/main.min.js.download" type="text/javascript" charset="utf-8"></script>



<script type="text/javascript">
  function _remove_token_from_url() {
    if (window.location.search.length <= 1) {
      return;
    }
    var search_parameters = window.location.search.slice(1).split('&');
    for (var i = 0; i < search_parameters.length; i++) {
      if (search_parameters[i].split('=')[0] === 'token') {
        // remote token from search parameters
        search_parameters.splice(i, 1);
        var new_search = '';
        if (search_parameters.length) {
          new_search = '?' + search_parameters.join('&');
        }
        var new_url = window.location.origin + 
                      window.location.pathname + 
                      new_search + 
                      window.location.hash;
        window.history.replaceState({}, "", new_url);
        return;
      }
    }
  }
  _remove_token_from_url();
</script>


<div style="position: absolute; width: 0px; height: 0px; overflow: hidden; padding: 0px; border: 0px; margin: 0px;"><div id="MathJax_Font_Test" style="position: absolute; visibility: hidden; top: 0px; left: 0px; width: auto; min-width: 0px; max-width: none; padding: 0px; border: 0px; margin: 0px; white-space: nowrap; text-align: left; text-indent: 0px; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; font-size: 40px; font-weight: normal; font-style: normal;"></div></div><style>#toc li > span:hover { background-color: #DAA520 }
.toc-item-highlight-select  {background-color: #FFD700}
.toc-item-highlight-execute  {background-color: #FF0000}
.toc-item-highlight-execute.toc-item-highlight-select   {background-color: #FFD700}div#menubar-container, div#header-container {
width: auto;
padding-left: 20px; }#toc-wrapper { background-color: #FFFFFF}
#toc a, #navigate_menu a, .toc { color: #333333}#toc-wrapper .toc-item-num { color: #000000}.sidebar-wrapper { border-color: #EEEEEE}.highlight_on_scroll { border-left: solid 4px #2447f0}</style><div id="varInspector-wrapper" class="ui-draggable ui-resizable varInspector-float-wrapper" style="position: fixed; display: none; max-height: 727px;"><div id="varInspector-header" class="header">Variable Inspector <a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="kill-btn" title="Close window">[x]</a><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="hide-btn" title="Hide Variable Inspector">[-]</a><a href="http://localhost:8888/notebooks/Breast_Cancer_Wisconsin_Diagnostic_Project.ipynb#" class="reload-btn" title="Reload Variable Inspector">  ↻</a><span>&nbsp;&nbsp;</span><span>&nbsp;&nbsp;</span></div><div id="varInspector" class="varInspector" style="height: 92.222px; max-height: 707px;"><div class="inspector"><table class="table fixed table-condensed table-nonfluid tablesorter tablesorter-default" role="grid"><colgroup><col>  <col><col></colgroup><thead><tr role="row" class="tablesorter-headerRow"><th data-column="0" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="X: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">X</div></th><th data-column="1" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Name: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Name</div></th><th data-column="2" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Type: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Type</div></th><th data-column="3" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Size: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Size</div></th><th data-column="4" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Value: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Value</div></th></tr></thead><tbody aria-live="polite" aria-relevant="all"><tr role="row"><td>  </td></tr></tbody></table></div></div><div class="ui-resizable-handle ui-resizable-e" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div></div></body></html>