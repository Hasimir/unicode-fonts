[![Build Status](https://secure.travis-ci.org/rolandwalker/unicode-fonts.png?branch=master)](http://travis-ci.org/rolandwalker/unicode-fonts)

unicode-fonts
=============

Configure Unicode fonts for Emacs.

![Using the Native Mac backend](https://raw.github.com/rolandwalker/unicode-fonts/master/native_mac_backend.png)

Quickstart
----------

* Remove Unifont from your system.

* Install these fonts
	* <http://users.teilar.gr/~g1951d/Symbola706.zip>
	* <http://www.quivira-font.com/files/Quivira.ttf>
	* <http://sourceforge.net/projects/dejavu/files/dejavu/2.33/dejavu-fonts-ttf-2.33.tar.bz2>

* Use an extended Latin font for your default face, such
  as Monaco, Consolas, or DejaVu Sans Mono.

* `(require 'unicode-fonts)`

* `(unicode-fonts-setup)`

Testing
-------

	C-h h                                         ; M-x view-hello-file

	M-x list-charset-chars RET unicode-bmp RET    ; search for eg 210x

	M-x list-charset-chars RET unicode-smp RET    ; if your backend supports astral chars

	M-x unicode-fonts-debug-insert-block RET Mathematical_Operators RET

Customization
-------------

	M-x customize-group RET unicode-fonts RET

Overview
--------

Emacs maintains font mappings on a per-glyph basis, meaning
that multiple fonts are used at the same time (transparently) to
display any character for which you have a font.  Furthermore,
Emacs does this out of the box.

However, font mappings via fontsets are a bit difficult to
configure.  In addition, the default setup does not always pick
the most legible fonts.  As the manual warns, the choice of font
actually displayed for a non-ASCII character is "somewhat random".

The Unicode standard provides a way to organize font mappings: it
divides character ranges into logical groups called "blocks".  This
library configures Emacs in a Unicode-friendly way by providing
mappings from

	each Unicode block  ---to--->   a font with good coverage

and makes the settings available via the customization interface.

This library provides font mappings for 205 of the 216 blocks in
the Unicode 6.3 standard with displayable characters.

To use unicode-fonts, place the unicode-fonts.el file somewhere
Emacs can find it, and add the following to your ~/.emacs file:

```lisp
(require 'unicode-fonts)
(unicode-fonts-setup)
```

See important notes about startup speed below.

Minimum Useful Fonts
--------------------

To gain any benefit from the library, you must have fonts with good
Unicode support installed on your system.  If you are running a
recent version of OS X or Microsoft Windows, you already own some
good multi-lingual fonts, though you would do very well to download
and install the four items below:

From <http://dejavu-fonts.org/wiki/Download>

	DejaVu Sans, DejaVu Sans Mono

From <http://www.quivira-font.com/downloads.php>

	Quivira

From <http://users.teilar.gr/~g1951d/>

	Symbola

It is also recommended to remove GNU Unifont from your system.
Unifont is very useful for debugging, but not useful for reading.

Startup Speed
-------------

The default options favor correctness and completeness over speed, and can
add **many** **seconds** to startup time in GUI mode.  Note that when
possible a font cache is kept between sessions, so try starting Emacs a
second time to see the true startup cost.  To further increase startup
speed, enter the customization interface and

1. Remove fonts from `unicode-fonts-block-font-mapping` which are not present on your system.

2. Disable blocks in `unicode-fonts-block-font-mapping` which you are not interested in displaying.

Unmapped Blocks
---------------

On the assumption that an extended Latin font such as Monaco,
Consolas, or DejaVu Sans Mono is already being used for the default
face, no separate mappings are provided for the following Unicode
blocks:

	Latin Extended Additional
	Latin Extended-A
	Latin-1 Supplement
	Spacing Modifier Letters

Emoji
----

Color Emoji are enabled by default when using the Native Mac port
on OS X.  This can be disabled by customizing each relevant mapping,
or by turning off all multicolor glyphs here:

	M-x customize-variable RET unicode-fonts-skip-font-groups RET

Bugs
----

Calling `set-fontset-font` can easily crash Emacs.  There is a
workaround, but it may not be sufficient on all platforms.
Tested on Cocoa Emacs, Native Mac Emacs, X11/XQuartz,
MS Windows XP.

Widths of alternate fonts do not behave as expected on MS Windows.
For example, DejaVu Sans Mono box-drawing characters may use a
different width than the default font.

Free International and Symbol Fonts
-----------------------------------

Free fonts recognized by this package may be downloaded
from the following locations:

From <http://scripts.sil.org/cms/scripts/page.php?item_id=DoulosSIL_download>

	Doulos SIL                    ; Extended European and diacritics

From <http://scripts.sil.org/cms/scripts/page.php?item_id=Gentium_download>

	Gentium Plus                  ; Greek

From <http://users.teilar.gr/~g1951d/>

	Aegean, Aegyptus, Akkadian    ; Ancient languages
	Analecta                      ; Ancient languages, Deseret
	Musica                        ; Musical Symbols

From <http://www.wazu.jp/gallery/views/View_MPH2BDamase.html>

	MPH 2B Damase                 ; Arabic, Armenian, Buginese, Cherokee, Georgian,
	                              ; Glagolitic, Hanunoo, Kharoshthi, Limbu, Osmanya,
	                              ; Shavian, Syloti Nagri, Tai Le, Thaana

From <http://wenq.org/enindex.cgi?Home>

	WenQuanYi Zen Hei             ; CJK (Simplified Chinese)

From <http://babelstone.co.uk/Fonts/>

	BabelStone Han                ; CJK (Simplified Chinese)
	BabelStone Phags-pa Book      ; Phags-pa

From <http://kldp.net/projects/unfonts/>

	Un Batang                     ; CJK (Hangul)

From <http://sourceforge.jp/projects/hanazono-font/releases/>

	Hana Min A, Hana Min B        ; CJK (Japanese)

From <http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=SILYi_home>

	Nuosu SIL                     ; CJK (Yi)

From <http://www.daicing.com/manchu/index.php?page=fonts-downloads>

	Daicing Xiaokai               ; Mongolian

From <http://www.library.gov.bt/IT/fonts.html>

	Jomolhari                     ; Tibetan

From <http://scripts.sil.org/cms/scripts/page.php?item_id=Padauk>

	Padauk                        ; Myanmar

From <https://code.google.com/p/myanmar3source/downloads/list>

	Myanmar3                      ; Myanmar

From <http://www.yunghkio.com/unicode/>

	Yunghkio                      ; Myanmar

From <https://code.google.com/p/tharlon-font/downloads/list>

	TharLon                       ; Myanmar

From <http://sourceforge.net/projects/prahita/files/Myanmar%20Unicode%20Fonts/MasterpieceUniSans/>

	Masterpiece Uni Sans          ; Myanmar

From <http://sarovar.org/projects/samyak/>

	Samyak                        ; Devanagari, Gujarati, Malayalam, Oriya, Tamil

From <http://guca.sourceforge.net/typography/fonts/anmoluni/>

	AnmolUni                      ; Gurmukhi

From <http://brahmi.sourceforge.net/downloads2.html>

	Kedage                        ; Kannada

From <http://www.omicronlab.com/bangla-fonts.html>

	Mukti Narrow                  ; Bengali

From <http://www.kamban.com.au/downloads.html>

	Akshar Unicode                ; Sinhala

From <http://tabish.freeshell.org/eeyek/download.html>

	Eeyek Unicode                 ; Meetei Mayek

From <http://scripts.sil.org/CMS/scripts/page.php?&item_id=Mondulkiri>

	Khmer Mondulkiri              ; Khmer

From <http://www.laoscript.net/downloads/>

	Saysettha MX                  ; Lao

From <http://www.geocities.jp/simsheart_alif/taithamunicode.html>

	Lanna Alif                    ; Tai Tham

From <http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=DaiBannaSIL>

	Dai Banna SIL                 ; New Tai Lue

From <http://scripts.sil.org/cms/scripts/page.php?item_id=TaiHeritage>

	Tai Heritage Pro              ; Tai Viet

From <http://sabilulungan.org/aksara/>

	Sundanese Unicode             ; Sundanese

From <http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=ArabicFonts>

	Scheherazade                  ; Arabic

From <http://www.farsiweb.ir/wiki/Persian_fonts>

	Koodak                        ; Arabic (Farsi)

From <http://openfontlibrary.org/font/ahuramazda/>

	Ahuramzda                     ; Avestan

From <http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=AbyssinicaSIL>

	Abyssinica SIL                ; Ethiopic

From <http://www.bethmardutho.org/index.php/resources/fonts.html>

	Estrangelo Nisibin            ; Syriac

From <http://www.evertype.com/fonts/nko/>

	Conakry                       ; N'ko

From <http://uni.hilledu.com/download-ribenguni>

	Ribeng                        ; Chakma

From <http://www.virtualvinodh.com/downloads>

	Adinatha Tamil Brahmi         ; Brahmi

From <https://code.google.com/p/noto/>

	Noto Sans                     ; Turkish Lira Sign (and others)

From <http://ftp.gnu.org/gnu/freefont/>

	FreeMono, etc (FreeFont)      ; Kayah Li (and others)

From <http://ulikozok.com/aksara-batak/batak-font/>

	Batak-Unicode                 ; Batak

From <http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=Mingzat>

	Mingzat                       ; Lepcha

From <http://phjamr.github.io/miao.html#install>

	Miao Unicode                  ; Miao, Lisu

From <http://scholarsfonts.net/cardofnt.html>

	Cardo                         ; Historical Languages

From <http://sourceforge.net/projects/junicode/files/junicode/>

	Junicode                      ; Historical Languages

Non-free Fonts
--------------

Many non-free fonts are referenced by the default settings.
However, free alternatives are also given wherever possible, and
patches are of course accepted to improve every case.

Chinese and Arabic Scripts
--------------------------

If you are using a language written in Chinese or Arabic script,
try customizing `unicode-fonts-skip-font-groups` to control which
script you see, and send a friendly bug report.

Compatibility and Requirements
------------------------------

	GNU Emacs version 24.4-devel     : yes, at the time of writing
	GNU Emacs version 24.3           : yes
	GNU Emacs version 23.3           : yes
	GNU Emacs version 22.3 and lower : no

Requires [fonts-utils.el](http://github.com/rolandwalker/font-utils), [ucs-utils.el](http://github.com/rolandwalker/ucs-utils)
