# myPDF-Tool
Script zur Aanalyse und Modifikation einer PDF-Datei
ergänzt um Scripte und Aktionen für Kontextmenüs von Dateimanagern (Dolphin, Nemo)

- verschiedene Menüaktionen mit PDF-Dateien

Alle Scripte werden im Verzeichis ~/bin des aktuellen Users installiert und die
Menüs werden jeweils für den aktuellen Nutzer bereitgestellt.
Das Verzeichnis ~/bin sollte im Suchpfad sein. Es werden keine Root-Rechte
zur Installation benötigt. In jedem Verzeichnis liegt eine Datei _install_.

Der Aufruf erfolgt im Terminal mit

```
user@linux:~/Pfad/zu/den/entpackten/Dateien/maPDF-Tool> bash ./install
```

* install (Bash-Script) - Installiert Scripte und Menüs für den angemeldeten Nutzer

* ksm_pdf_tool (Bash-Script) - kan folgende Dinge mit PDF-Dateien tun:

  Aufruf:
```  
  user@host:~/bin> ./ksm_pdf_tool Dateiname.pdf PARAMETER1 <PARAMETER2> <PARAMETER3>
```  
  moegliche Werte PARAMETER1:
  
  INFO     --> 	ermittelt soviele Informationen wie moeglich schreibt
         		sie in Dateiname.pdfinfo
  
  TEXTEXT  --> 	extrahiert den in der PDF-Datei enthaltenen Text
		        in Dateiname.txt
	        Zur Texterkennung per OCR muss mindestens PARAMETER2
	        angegeben werden:
                    wird PARAMETER2 angegeben und ist eine natuerliche
                    Zahl zwischen 150 und 600 wird er als dpi-Angabe fuer die
                    Texterkennung per OCR interpretiert.
                    Sollte PARAMETER2 keine nat. Zahl sein, wird er als
                    Sprachangabe fuer die Texterkennung per OCR
                    interpretiert und Standardaufloesung (150dpi) gesetzt.
                    Wird PARAMETER3 angegeben, wird dieser als 
                    Sprachangabe fuer die Texterkennung genutzt.
                    Ansonsten wird als Standardsprache deutsch (deu) genutzt
  
  IMGEXT   --> 	extrahiert alle im PDF-Dokument vorhandenen Bilder in
                Originalaufloesung nach dem Schema:
	                    Dateiname-Seitenzahl-Bildnummer.[png|tiff|jpg|jp2|ppm]
	        und extrahiert aus den Bildern vorhandene Farbprofile
  
  SEPPAGES --> 	Erstellt aus jeder Seite der PDF-Datei ein eigenes PDF-Dokument
                nach dem Schema Dateiname-Seitenzahl.pdf
  
  DETACH   --> 	extrahiert alle Dateianhaenge (falls denn welche existieren)
  
  ATTACH   --> 	haengt eine Datei als Attachment an die PDF-Datei an
                (das Original der angehaengten Datei wird geloescht)
  
  HTML     --> 	Erstellt aus der PDF-Datei ein HTML-Dokument (nicht schoen)
  
  PS       --> 	Erstellt aus der PDF-Datei eine PostScript-Datei
  
  ALLES    --> 	Alles was INFO, TEXTEXT IMGEXT, SEPPAGES, DETACH, HTML und PS
	        machen. Des weiteren werden vorhandene Schriftdaten extrahiert,
	        Einzelseiten in SVG- und PostScript-Dateien gewandelt, damit
	        evtl. vorhandene Vektordaten daraus haendisch extrahiert werden
	        koennen und alle Dateien in entsprechende Unterverzeichnisse
	        einsortiert.
  
  PDFA1B   --> 	Erstellt eine Datei im Format PDF-A-1b
  
  ROTL     --> 	rotiert alle Seiten um 90° gegen den Uhrzeigersinn
                im Verhaeltnis zur Ausrichtung der Originaldatei
  
  ROTR     --> 	rotiert alle Seiten um 90° im Uhrzeigersinn
                im Verhaeltnis zur Ausrichtung der Originaldatei
  
  ROTD     --> 	rotiert alle Seiten um 180° 
                im Verhaeltnis zur Ausrichtung der Originaldatei
  
  REVERSE  -->	kehrt die Seitenreihenfolge um
  
  M2S      --> 	erstelle PDF mit 2 Seiten pro Blatt
  
  M4S      --> 	erstelle PDF mit 4 Seiten pro Blatt
  
  ALLFEAT  --> 	hebt alle Restriktionen innerhalb der PDF auf
                (Drucken erlaubt, Kommentiern erlaubt, usw.)
  
  CONVPNG  -->	konvertiert alle Seiten zu PNG-Pixelgrafiken mit der
                in PARAMETER2 angegebenen Aufloseung. Sollte PARAMETER2
                keine nat. Zahl zwischen 150 und 600 sein, wird die
                Standardaufloesung von 150dpi gesetzt
  CONVJPG  -->	konvertiert alle Seiten zu JPG-Pixelgrafiken  mit der
                in PARAMETER2 angegebenen Aufloseung. Sollte PARAMETER2
                keine nat. Zahl zwischen 150 und 600 sein, wird die
                Standardaufloesung von 150dpi gesetzt

  Benoetigt werden folgende Programme:
  
  realpath, basename, dirname, tr, grep, awk, ls, mv, mkdir, rm, cp, sort, file,
  uniq, pdfinfo, oyranos-icc, podofopdfinfo, pdffonts, pdfimages, pdfdetach,
  pdfseparate, pdftops, pdftocairo, pdftohtml, pdftotext, pdftoppm, pdftk,
  pdfjam, cfftot1, mutool, tesseract, qpdf, convert, rsync
  

* nemo_pdf_tool_wrapper (Bash-Script) - ruft für jede als Parameter übergebene Datei das Script _ksm_pdf_tool_ auf und </br>
lässt die Funktion ausfühern, die ebenfalls mit als Parameter übergeben wurde. Dieses Script wird für nemo installiert, um</br>
unter Nemo eine Mehrfachselektion zu ermöglichen, da _ksm_pdf_tool_ nur eine Datei pro Aufruf verarbeiten kann. 

* pdf_tool_alles.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter ALLES und allen markierten Dateien auf

* pdf_tool_allfeat.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter ALLFEAT und allen markierten Dateien auf

* pdf_tool_detach.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter DETACH und allen markierten Dateien auf

* pdf_tool_html.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter HTML und allen markierten Dateien auf

* df_tool_imgext.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter IMGEXT und allen markierten Dateien auf

* pdf_tool_info.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter INFO und allen markierten Dateien auf

* pdf_tool_pdfa1b.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter PDFA1B und allen markierten Dateien auf

* pdf_tool_ps.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter PS und allen markierten Dateien auf

* pdf_tool_reverse.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter REVERSE und allen markierten Dateien auf

* pdf_tool_rotd.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter ROTD und allen markierten Dateien auf

* pdf_tool_rotl.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter ROTL und allen markierten Dateien auf

* pdf_tool_rotr.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter ROTR und allen markierten Dateien auf

* pdf_tool_seppages.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter SEPPAGES und allen markierten Dateien auf

* pdf_tool_textext.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter TEXTEXT und allen markierten Dateien auf

* pdf_tool_textextocr.nemo_action - ruft das Script _nemowrapper_pdftool_ mit dem Parameter TEXTEXTOCR und allen markierten Dateien auf

* Submenu-PDF.desktop - Integriert alle oben angegebenen Mnüpunkte im Kontextmenü bei Dolphin.

* README.md - Diese Datei
