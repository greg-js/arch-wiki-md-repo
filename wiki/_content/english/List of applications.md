[Internet](/index.php/List_of_applications/Internet "List of applications/Internet") – [Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") – [Utilities](/index.php/List_of_applications/Utilities "List of applications/Utilities") – [Documents](/index.php/List_of_applications/Documents "List of applications/Documents") – [Security](/index.php/List_of_applications/Security "List of applications/Security") – [Science](/index.php/List_of_applications/Science "List of applications/Science") – [Other](/index.php/List_of_applications/Other "List of applications/Other")

Related articles

*   [Core utilities](/index.php/Core_utilities "Core utilities")
*   [List of games](/index.php/List_of_games "List of games")

This article is a general list of applications sorted by category, as a reference for those looking for packages. Many sections are split between console and graphical applications.

**Tip:**

*   This page exists primarily to make it easier to search for alternatives to an application that you do not know under which section has been added. Use the links in the template at the top to view the main sections as separate pages.
*   Please consider [installing](/index.php/Install "Install") the [pkgstats](/index.php/Pkgstats "Pkgstats") package, which provides a timer that sends a list of the packages installed on your system, along with the architecture and the mirrors you use, to the Arch Linux developers in order to help them prioritize their efforts and make the distribution even better. The information is sent anonymously and cannot be used to identify you. You can view the collected data at the [Statistics page](https://www.archlinux.de/?page=Statistics). More information is available in [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=105431).
*   Daemon packages usually include the relevant systemd unit file to [start](/index.php/Start "Start"); some packages even include different ones. After installation `pacman -Qql *package* | grep -Fe .service -e .socket` can be used to check and find the relevant one.

**Note:** Applications listed in "Console" sections can have graphical front-ends. Official ones are currently omitted.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Internet](#Internet)
    *   [1.1 Network connection](#Network_connection)
        *   [1.1.1 Network managers](#Network_managers)
        *   [1.1.2 VPN clients](#VPN_clients)
        *   [1.1.3 Proxy servers](#Proxy_servers)
        *   [1.1.4 Anonymizing networks](#Anonymizing_networks)
    *   [1.2 Web browsers](#Web_browsers)
        *   [1.2.1 Console](#Console)
        *   [1.2.2 Graphical](#Graphical)
            *   [1.2.2.1 Gecko-based](#Gecko-based)
                *   [1.2.2.1.1 Firefox spin-offs](#Firefox_spin-offs)
            *   [1.2.2.2 Blink-based](#Blink-based)
                *   [1.2.2.2.1 Privacy-focused chromium spin-offs](#Privacy-focused_chromium_spin-offs)
                *   [1.2.2.2.2 Proprietary chromium spin-offs](#Proprietary_chromium_spin-offs)
                *   [1.2.2.2.3 Browsers based on qt5-webengine](#Browsers_based_on_qt5-webengine)
                *   [1.2.2.2.4 Browsers based on electron](#Browsers_based_on_electron)
            *   [1.2.2.3 WebKit-based](#WebKit-based)
                *   [1.2.2.3.1 Browsers based on webkit2gtk](#Browsers_based_on_webkit2gtk)
                *   [1.2.2.3.2 Browsers based on qt5-webkit](#Browsers_based_on_qt5-webkit)
            *   [1.2.2.4 Other](#Other)
    *   [1.3 Web servers](#Web_servers)
        *   [1.3.1 Static web servers](#Static_web_servers)
        *   [1.3.2 Specialized web servers](#Specialized_web_servers)
        *   [1.3.3 WSGI servers](#WSGI_servers)
        *   [1.3.4 Performance testing](#Performance_testing)
    *   [1.4 File sharing](#File_sharing)
        *   [1.4.1 Download managers](#Download_managers)
            *   [1.4.1.1 Console](#Console_2)
            *   [1.4.1.2 Graphical](#Graphical_2)
        *   [1.4.2 Cloud storage servers](#Cloud_storage_servers)
        *   [1.4.3 Cloud synchronization clients](#Cloud_synchronization_clients)
        *   [1.4.4 FTP](#FTP)
            *   [1.4.4.1 FTP clients](#FTP_clients)
            *   [1.4.4.2 FTP servers](#FTP_servers)
        *   [1.4.5 BitTorrent clients](#BitTorrent_clients)
            *   [1.4.5.1 Console](#Console_3)
            *   [1.4.5.2 Graphical](#Graphical_3)
        *   [1.4.6 Other P2P networks](#Other_P2P_networks)
        *   [1.4.7 Pastebin clients](#Pastebin_clients)
    *   [1.5 Communication](#Communication)
        *   [1.5.1 Email clients](#Email_clients)
            *   [1.5.1.1 Console](#Console_4)
            *   [1.5.1.2 Graphical](#Graphical_4)
            *   [1.5.1.3 Web-based](#Web-based)
        *   [1.5.2 Mail servers](#Mail_servers)
        *   [1.5.3 Mail retrieval agents](#Mail_retrieval_agents)
        *   [1.5.4 Instant messaging clients](#Instant_messaging_clients)
            *   [1.5.4.1 Multi-protocol clients](#Multi-protocol_clients)
                *   [1.5.4.1.1 Console](#Console_5)
                *   [1.5.4.1.2 Graphical](#Graphical_5)
            *   [1.5.4.2 IRC clients](#IRC_clients)
                *   [1.5.4.2.1 Console](#Console_6)
                *   [1.5.4.2.2 Graphical](#Graphical_6)
            *   [1.5.4.3 XMPP clients](#XMPP_clients)
                *   [1.5.4.3.1 Console](#Console_7)
                *   [1.5.4.3.2 Graphical](#Graphical_7)
            *   [1.5.4.4 SIP clients](#SIP_clients)
            *   [1.5.4.5 Matrix clients](#Matrix_clients)
            *   [1.5.4.6 Tox clients](#Tox_clients)
            *   [1.5.4.7 Serverless (decentralized) clients](#Serverless_(decentralized)_clients)
            *   [1.5.4.8 Other IM clients](#Other_IM_clients)
        *   [1.5.5 Instant messaging servers](#Instant_messaging_servers)
            *   [1.5.5.1 IRC servers](#IRC_servers)
            *   [1.5.5.2 XMPP servers](#XMPP_servers)
            *   [1.5.5.3 SIP servers](#SIP_servers)
            *   [1.5.5.4 Other IM servers](#Other_IM_servers)
        *   [1.5.6 Collaborative software](#Collaborative_software)
    *   [1.6 News, RSS, and blogs](#News,_RSS,_and_blogs)
        *   [1.6.1 News aggregators](#News_aggregators)
            *   [1.6.1.1 Console](#Console_8)
            *   [1.6.1.2 Graphical](#Graphical_8)
        *   [1.6.2 Podcast clients](#Podcast_clients)
            *   [1.6.2.1 Console](#Console_9)
            *   [1.6.2.2 Graphical](#Graphical_9)
        *   [1.6.3 Usenet newsreaders](#Usenet_newsreaders)
            *   [1.6.3.1 Console](#Console_10)
            *   [1.6.3.2 Graphical](#Graphical_10)
        *   [1.6.4 Microblogging clients](#Microblogging_clients)
            *   [1.6.4.1 Console](#Console_11)
            *   [1.6.4.2 Graphical](#Graphical_11)
        *   [1.6.5 Blog engines](#Blog_engines)
        *   [1.6.6 Static site generators](#Static_site_generators)
    *   [1.7 Remote desktop](#Remote_desktop)
        *   [1.7.1 Remote desktop clients](#Remote_desktop_clients)
        *   [1.7.2 Remote desktop servers](#Remote_desktop_servers)
*   [2 Multimedia](#Multimedia)
    *   [2.1 Codecs](#Codecs)
    *   [2.2 Image](#Image)
        *   [2.2.1 Image viewers](#Image_viewers)
            *   [2.2.1.1 Framebuffer image viewers](#Framebuffer_image_viewers)
            *   [2.2.1.2 Graphical image viewers](#Graphical_image_viewers)
        *   [2.2.2 Image organizers](#Image_organizers)
        *   [2.2.3 Image processing](#Image_processing)
            *   [2.2.3.1 Image compression](#Image_compression)
        *   [2.2.4 Raster graphics editors](#Raster_graphics_editors)
        *   [2.2.5 Photo editors](#Photo_editors)
        *   [2.2.6 Vector graphics editors](#Vector_graphics_editors)
        *   [2.2.7 Font editors](#Font_editors)
        *   [2.2.8 2D animation](#2D_animation)
        *   [2.2.9 3D computer graphics](#3D_computer_graphics)
        *   [2.2.10 Color pickers](#Color_pickers)
        *   [2.2.11 Screenshot](#Screenshot)
        *   [2.2.12 Digital camera managers](#Digital_camera_managers)
    *   [2.3 Audio](#Audio)
        *   [2.3.1 Audio systems](#Audio_systems)
        *   [2.3.2 Audio players](#Audio_players)
            *   [2.3.2.1 Console](#Console_12)
            *   [2.3.2.2 Graphical](#Graphical_12)
                *   [2.3.2.2.1 GStreamer-based](#GStreamer-based)
                *   [2.3.2.2.2 Phonon-based](#Phonon-based)
                *   [2.3.2.2.3 Qt Multimedia-based](#Qt_Multimedia-based)
                *   [2.3.2.2.4 Other](#Other_2)
        *   [2.3.3 Audio tag editors](#Audio_tag_editors)
            *   [2.3.3.1 Console](#Console_13)
            *   [2.3.3.2 Graphical](#Graphical_13)
        *   [2.3.4 Lyrics](#Lyrics)
        *   [2.3.5 Audio converters](#Audio_converters)
        *   [2.3.6 Audio editors](#Audio_editors)
        *   [2.3.7 Digital audio workstations](#Digital_audio_workstations)
        *   [2.3.8 Audio analyzers](#Audio_analyzers)
        *   [2.3.9 Scorewriters](#Scorewriters)
        *   [2.3.10 Audio synthesis environments](#Audio_synthesis_environments)
        *   [2.3.11 Sound generators](#Sound_generators)
        *   [2.3.12 Music trackers](#Music_trackers)
        *   [2.3.13 DJ](#DJ)
        *   [2.3.14 Audio effects](#Audio_effects)
        *   [2.3.15 Audio visualizers](#Audio_visualizers)
        *   [2.3.16 Volume control](#Volume_control)
        *   [2.3.17 CD ripping](#CD_ripping)
    *   [2.4 Video](#Video)
        *   [2.4.1 Video players](#Video_players)
            *   [2.4.1.1 Console](#Console_14)
            *   [2.4.1.2 Graphical](#Graphical_14)
                *   [2.4.1.2.1 GStreamer-based](#GStreamer-based_2)
                *   [2.4.1.2.2 mpv-based](#mpv-based)
                *   [2.4.1.2.3 MPlayer-based](#MPlayer-based)
                *   [2.4.1.2.4 Other](#Other_3)
        *   [2.4.2 Video converters](#Video_converters)
            *   [2.4.2.1 Console](#Console_15)
            *   [2.4.2.2 Graphical](#Graphical_15)
        *   [2.4.3 Video editors](#Video_editors)
        *   [2.4.4 Subtitles](#Subtitles)
        *   [2.4.5 Subtitle editors](#Subtitle_editors)
        *   [2.4.6 Screencast](#Screencast)
        *   [2.4.7 Webcam](#Webcam)
        *   [2.4.8 DVD authoring](#DVD_authoring)
        *   [2.4.9 DVD ripping](#DVD_ripping)
        *   [2.4.10 Video thumbnails](#Video_thumbnails)
    *   [2.5 Collection managers](#Collection_managers)
    *   [2.6 Media servers](#Media_servers)
    *   [2.7 Metadata](#Metadata)
    *   [2.8 Mobile device managers](#Mobile_device_managers)
    *   [2.9 Optical disc burning](#Optical_disc_burning)
*   [3 Utilities](#Utilities)
    *   [3.1 Terminal](#Terminal)
        *   [3.1.1 Command shells](#Command_shells)
        *   [3.1.2 Terminal emulators](#Terminal_emulators)
            *   [3.1.2.1 VTE-based](#VTE-based)
            *   [3.1.2.2 KMS-based](#KMS-based)
            *   [3.1.2.3 framebuffer-based](#framebuffer-based)
        *   [3.1.3 Terminal pagers](#Terminal_pagers)
        *   [3.1.4 Terminal multiplexers](#Terminal_multiplexers)
    *   [3.2 Files](#Files)
        *   [3.2.1 File managers](#File_managers)
            *   [3.2.1.1 Console](#Console_16)
            *   [3.2.1.2 Graphical](#Graphical_16)
                *   [3.2.1.2.1 Twin-panel](#Twin-panel)
        *   [3.2.2 Trash management](#Trash_management)
        *   [3.2.3 File synchronization](#File_synchronization)
        *   [3.2.4 Archiving and compression tools](#Archiving_and_compression_tools)
            *   [3.2.4.1 Archive managers](#Archive_managers)
        *   [3.2.5 Comparison, diff, merge](#Comparison,_diff,_merge)
        *   [3.2.6 Batch renamers](#Batch_renamers)
        *   [3.2.7 File searching](#File_searching)
            *   [3.2.7.1 Console](#Console_17)
            *   [3.2.7.2 Graphical](#Graphical_17)
                *   [3.2.7.2.1 File indexers](#File_indexers)
        *   [3.2.8 Full-text searching](#Full-text_searching)
            *   [3.2.8.1 Full-text indexers](#Full-text_indexers)
    *   [3.3 Development](#Development)
        *   [3.3.1 Code forges](#Code_forges)
            *   [3.3.1.1 Code forge clients](#Code_forge_clients)
        *   [3.3.2 Version control systems](#Version_control_systems)
        *   [3.3.3 Build automation](#Build_automation)
        *   [3.3.4 Integrated development environments](#Integrated_development_environments)
            *   [3.3.4.1 Java IDEs](#Java_IDEs)
            *   [3.3.4.2 Python IDEs](#Python_IDEs)
            *   [3.3.4.3 Educational IDEs](#Educational_IDEs)
        *   [3.3.5 Debuggers](#Debuggers)
        *   [3.3.6 Lexing and parsing](#Lexing_and_parsing)
        *   [3.3.7 GUI builders](#GUI_builders)
        *   [3.3.8 Hex editors](#Hex_editors)
        *   [3.3.9 JSON tools](#JSON_tools)
        *   [3.3.10 Literate programming](#Literate_programming)
        *   [3.3.11 UML modelers](#UML_modelers)
        *   [3.3.12 API documentation browsers](#API_documentation_browsers)
        *   [3.3.13 Issue tracking systems](#Issue_tracking_systems)
        *   [3.3.14 Code review](#Code_review)
        *   [3.3.15 Game development](#Game_development)
        *   [3.3.16 Repository managers](#Repository_managers)
    *   [3.4 Text input](#Text_input)
        *   [3.4.1 Character selectors](#Character_selectors)
        *   [3.4.2 On-screen keyboards](#On-screen_keyboards)
        *   [3.4.3 Keyboard layout switchers](#Keyboard_layout_switchers)
        *   [3.4.4 Keybinding managers](#Keybinding_managers)
        *   [3.4.5 Input methods](#Input_methods)
    *   [3.5 Disks](#Disks)
        *   [3.5.1 Partitioning tools](#Partitioning_tools)
        *   [3.5.2 Formatting tools](#Formatting_tools)
        *   [3.5.3 Cloning tools](#Cloning_tools)
        *   [3.5.4 Mount tools](#Mount_tools)
        *   [3.5.5 Disk usage display](#Disk_usage_display)
        *   [3.5.6 Disk health status](#Disk_health_status)
        *   [3.5.7 File recovery tools](#File_recovery_tools)
        *   [3.5.8 Disk cleaning](#Disk_cleaning)
        *   [3.5.9 Disk image writing](#Disk_image_writing)
    *   [3.6 System](#System)
        *   [3.6.1 Task managers](#Task_managers)
        *   [3.6.2 System monitors](#System_monitors)
        *   [3.6.3 Hardware sensor monitoring](#Hardware_sensor_monitoring)
        *   [3.6.4 System information viewers](#System_information_viewers)
            *   [3.6.4.1 Console](#Console_18)
            *   [3.6.4.2 Graphical](#Graphical_18)
        *   [3.6.5 System log viewers](#System_log_viewers)
        *   [3.6.6 Font viewers](#Font_viewers)
        *   [3.6.7 Help viewers](#Help_viewers)
        *   [3.6.8 Command schedulers](#Command_schedulers)
        *   [3.6.9 Shutdown timers](#Shutdown_timers)
        *   [3.6.10 Clock synchronization](#Clock_synchronization)
        *   [3.6.11 Screen management](#Screen_management)
        *   [3.6.12 Backlight management](#Backlight_management)
        *   [3.6.13 Color management](#Color_management)
        *   [3.6.14 Printer management](#Printer_management)
        *   [3.6.15 Bluetooth management](#Bluetooth_management)
        *   [3.6.16 Power management](#Power_management)
        *   [3.6.17 Package management](#Package_management)
*   [4 Documents and texts](#Documents_and_texts)
    *   [4.1 Text editors](#Text_editors)
        *   [4.1.1 Console](#Console_19)
        *   [4.1.2 Graphical](#Graphical_19)
        *   [4.1.3 Emacs-style text editors](#Emacs-style_text_editors)
        *   [4.1.4 Vi-style text editors](#Vi-style_text_editors)
    *   [4.2 Office](#Office)
        *   [4.2.1 Office suites](#Office_suites)
        *   [4.2.2 Word processors](#Word_processors)
            *   [4.2.2.1 WYSIWYG HTML editors](#WYSIWYG_HTML_editors)
            *   [4.2.2.2 Desktop publishing](#Desktop_publishing)
        *   [4.2.3 Presentations](#Presentations)
        *   [4.2.4 Spreadsheets](#Spreadsheets)
        *   [4.2.5 Database tools](#Database_tools)
            *   [4.2.5.1 Simplified database software](#Simplified_database_software)
        *   [4.2.6 Formula editors](#Formula_editors)
    *   [4.3 Markup languages](#Markup_languages)
        *   [4.3.1 AsciiDoc](#AsciiDoc)
        *   [4.3.2 Markdown](#Markdown)
            *   [4.3.2.1 Python implementations](#Python_implementations)
            *   [4.3.2.2 Ruby implementations](#Ruby_implementations)
            *   [4.3.2.3 Markdown editors](#Markdown_editors)
        *   [4.3.3 Typesetting systems](#Typesetting_systems)
        *   [4.3.4 TeX editors](#TeX_editors)
        *   [4.3.5 TeX formula editors](#TeX_formula_editors)
        *   [4.3.6 XML editors](#XML_editors)
    *   [4.4 Document converters](#Document_converters)
    *   [4.5 Bibliographic reference managers](#Bibliographic_reference_managers)
    *   [4.6 Readers and viewers](#Readers_and_viewers)
        *   [4.6.1 PDF and DjVu](#PDF_and_DjVu)
        *   [4.6.2 E-book](#E-book)
        *   [4.6.3 Comic book](#Comic_book)
        *   [4.6.4 CHM](#CHM)
    *   [4.7 Document managers](#Document_managers)
    *   [4.8 Scanning software](#Scanning_software)
    *   [4.9 OCR software](#OCR_software)
        *   [4.9.1 Console](#Console_20)
        *   [4.9.2 Graphical](#Graphical_20)
    *   [4.10 Notes](#Notes)
        *   [4.10.1 Note-taking software](#Note-taking_software)
            *   [4.10.1.1 Console](#Console_21)
            *   [4.10.1.2 Graphical](#Graphical_21)
        *   [4.10.2 Stylus note-taking](#Stylus_note-taking)
        *   [4.10.3 Diary](#Diary)
        *   [4.10.4 Mind-mapping](#Mind-mapping)
        *   [4.10.5 Sticky notes](#Sticky_notes)
    *   [4.11 Special writing environments](#Special_writing_environments)
        *   [4.11.1 Distraction-free writing](#Distraction-free_writing)
        *   [4.11.2 Story writing](#Story_writing)
        *   [4.11.3 Screenwriting](#Screenwriting)
    *   [4.12 Language](#Language)
        *   [4.12.1 Dictionary and thesaurus](#Dictionary_and_thesaurus)
        *   [4.12.2 Spell checkers](#Spell_checkers)
        *   [4.12.3 Translation and localization](#Translation_and_localization)
    *   [4.13 Barcode generators and readers](#Barcode_generators_and_readers)
        *   [4.13.1 Console](#Console_22)
        *   [4.13.2 Graphical](#Graphical_22)
*   [5 Security](#Security)
    *   [5.1 Network security](#Network_security)
    *   [5.2 Firewall management](#Firewall_management)
    *   [5.3 Threat and vulnerability detection](#Threat_and_vulnerability_detection)
    *   [5.4 File security](#File_security)
    *   [5.5 Anti malware](#Anti_malware)
    *   [5.6 Backup programs](#Backup_programs)
    *   [5.7 Screen lockers](#Screen_lockers)
    *   [5.8 Password auditing](#Password_auditing)
    *   [5.9 Password managers](#Password_managers)
        *   [5.9.1 Console](#Console_23)
        *   [5.9.2 Graphical](#Graphical_23)
    *   [5.10 Cryptography](#Cryptography)
        *   [5.10.1 Hash checkers](#Hash_checkers)
        *   [5.10.2 Encryption, signing, steganography](#Encryption,_signing,_steganography)
        *   [5.10.3 Disk encryption](#Disk_encryption)
*   [6 Science](#Science)
    *   [6.1 Mathematics](#Mathematics)
        *   [6.1.1 Calculator](#Calculator)
        *   [6.1.2 Computer algebra system](#Computer_algebra_system)
        *   [6.1.3 Scientific or technical computing](#Scientific_or_technical_computing)
        *   [6.1.4 Statistics](#Statistics)
        *   [6.1.5 Data analysis and plotting](#Data_analysis_and_plotting)
        *   [6.1.6 Proof assistants](#Proof_assistants)
    *   [6.2 Physics](#Physics)
        *   [6.2.1 Physics simulation](#Physics_simulation)
        *   [6.2.2 Unit conversion](#Unit_conversion)
    *   [6.3 Chemistry](#Chemistry)
        *   [6.3.1 Molecules](#Molecules)
            *   [6.3.1.1 Viewers](#Viewers)
            *   [6.3.1.2 Drawing](#Drawing)
            *   [6.3.1.3 Modeling](#Modeling)
        *   [6.3.2 Periodic table](#Periodic_table)
    *   [6.4 Earth science](#Earth_science)
        *   [6.4.1 Geography](#Geography)
        *   [6.4.2 Meteorology](#Meteorology)
    *   [6.5 Astronomy](#Astronomy)
    *   [6.6 Biology](#Biology)
        *   [6.6.1 Computational biology and bioinformatics](#Computational_biology_and_bioinformatics)
        *   [6.6.2 Biochemistry](#Biochemistry)
        *   [6.6.3 Image manipulation](#Image_manipulation)
        *   [6.6.4 DICOM viewers and volume rendering](#DICOM_viewers_and_volume_rendering)
    *   [6.7 Engineering](#Engineering)
        *   [6.7.1 Computer-aided design](#Computer-aided_design)
        *   [6.7.2 Electronics](#Electronics)
            *   [6.7.2.1 Digital logic](#Digital_logic)
            *   [6.7.2.2 HDL](#HDL)
            *   [6.7.2.3 MCU IDE and programmers](#MCU_IDE_and_programmers)
            *   [6.7.2.4 Schematic capture editor](#Schematic_capture_editor)
    *   [6.8 Telecommunication](#Telecommunication)
        *   [6.8.1 Amateur radio](#Amateur_radio)
    *   [6.9 Simulation modeling](#Simulation_modeling)
    *   [6.10 Computer science](#Computer_science)
        *   [6.10.1 Artificial intelligence](#Artificial_intelligence)
*   [7 Others](#Others)
    *   [7.1 Organization](#Organization)
        *   [7.1.1 Personal information managers](#Personal_information_managers)
        *   [7.1.2 Time management](#Time_management)
            *   [7.1.2.1 Console](#Console_24)
            *   [7.1.2.2 Graphical](#Graphical_24)
        *   [7.1.3 Time trackers](#Time_trackers)
        *   [7.1.4 Task management](#Task_management)
            *   [7.1.4.1 Console](#Console_25)
            *   [7.1.4.2 Graphical](#Graphical_25)
        *   [7.1.5 Contacts management](#Contacts_management)
            *   [7.1.5.1 Console](#Console_26)
            *   [7.1.5.2 Graphical](#Graphical_26)
        *   [7.1.6 Financial management](#Financial_management)
        *   [7.1.7 Cryptocurrency](#Cryptocurrency)
        *   [7.1.8 Project management](#Project_management)
        *   [7.1.9 Recipe management](#Recipe_management)
    *   [7.2 Education](#Education)
        *   [7.2.1 Flashcards](#Flashcards)
        *   [7.2.2 Touch typing](#Touch_typing)
            *   [7.2.2.1 Console](#Console_27)
            *   [7.2.2.2 Graphical](#Graphical_27)
    *   [7.3 Accessibility](#Accessibility)
        *   [7.3.1 Speech synthesizers](#Speech_synthesizers)
        *   [7.3.2 Speech recognition](#Speech_recognition)
        *   [7.3.3 Screen magnifiers](#Screen_magnifiers)
        *   [7.3.4 Mouse](#Mouse)
    *   [7.4 Display managers](#Display_managers)
    *   [7.5 Desktop environments](#Desktop_environments)
        *   [7.5.1 Window managers](#Window_managers)
            *   [7.5.1.1 Console](#Console_28)
            *   [7.5.1.2 Graphical](#Graphical_28)
            *   [7.5.1.3 Composite managers](#Composite_managers)
        *   [7.5.2 Window tilers](#Window_tilers)
        *   [7.5.3 Taskbars](#Taskbars)
        *   [7.5.4 System tray](#System_tray)
        *   [7.5.5 Application launchers](#Application_launchers)
        *   [7.5.6 Application menu editors](#Application_menu_editors)
        *   [7.5.7 Wallpaper setters](#Wallpaper_setters)
        *   [7.5.8 Virtual desktop pagers](#Virtual_desktop_pagers)
        *   [7.5.9 Desktop widgets](#Desktop_widgets)
        *   [7.5.10 Desktop notifications](#Desktop_notifications)
        *   [7.5.11 Clipboard managers](#Clipboard_managers)
        *   [7.5.12 Logout UI](#Logout_UI)
*   [8 See also](#See_also)

## Internet

### Network connection

#### Network managers

*   **[ConnMan](/index.php/ConnMan "ConnMan")** — Daemon for managing internet connections within embedded devices running the Linux operating system. Comes with a command-line client, plus Enlightenment, ncurses, GTK and Dmenu clients are available.

	[https://01.org/connman](https://01.org/connman) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **dhclient** — DHCP client from the Internet Systems Consortium.

	[https://www.isc.org/downloads/dhcp/](https://www.isc.org/downloads/dhcp/) || [dhclient](https://www.archlinux.org/packages/?name=dhclient)

*   **[dhcpcd](/index.php/Dhcpcd "Dhcpcd")** — RFC2131 compliant DHCP client daemon.

	[https://roy.marples.name/projects/dhcpcd](https://roy.marples.name/projects/dhcpcd) || [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)

*   **[netctl](/index.php/Netctl "Netctl")** — Simple and robust tool to manage network connections via profiles. Intended for use with [systemd](/index.php/Systemd "Systemd").

	[https://projects.archlinux.org/netctl.git/](https://projects.archlinux.org/netctl.git/) || [netctl](https://www.archlinux.org/packages/?name=netctl)

*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** — Manager that provides wired, wireless, mobile broadband and OpenVPN detection with configuration and automatic connection.

	[https://wiki.gnome.org/Projects/NetworkManager](https://wiki.gnome.org/Projects/NetworkManager) || CLI: [networkmanager](https://www.archlinux.org/packages/?name=networkmanager), GUI: [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)

*   **[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")** — Native [systemd](/index.php/Systemd "Systemd") daemon that manages network configuration. It includes support for basic network configuration through [udev](/index.php/Udev "Udev").

	[https://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html](https://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[Wicd](/index.php/Wicd "Wicd")** — Wireless and wired connection manager with few dependencies. Comes with ncurses and GTK interfaces.

	[https://launchpad.net/wicd](https://launchpad.net/wicd) || CLI: [wicd](https://www.archlinux.org/packages/?name=wicd), GUI: [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk)

*   **[Wifi Radar](/index.php/Wifi_Radar "Wifi Radar")** — *WiFi Radar* is a PyGTK (Python 2) utility for managing wireless (and **only** wireless) profiles. It enables you to scan for available networks and create profiles for your preferred networks.

	[http://wifi-radar.tuxfamily.org/](http://wifi-radar.tuxfamily.org/) || [wifi-radar](https://www.archlinux.org/packages/?name=wifi-radar)

*   **wpa-cute** — Is a graphical Qt [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") front end to manage your wireless profiles *only*. It offer to change and add profiles or scan for networks and connect to them by [WPS](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Setup "wikipedia:Wi-Fi Protected Setup").

	[https://github.com/loh-tar/wpa-cute](https://github.com/loh-tar/wpa-cute) || [wpa-cute](https://aur.archlinux.org/packages/wpa-cute/)

See also [Network configuration#Network managers](/index.php/Network_configuration#Network_managers "Network configuration").

#### VPN clients

*   **Bitmask** — Secured and encrypted communication using various service providers

	[https://bitmask.net/](https://bitmask.net/) || [bitmask](https://aur.archlinux.org/packages/bitmask/)

*   **Libreswan** — A free software implementation of the most widely supported and standarized VPN protocol based on ("IPsec") and the Internet Key Exchange ("IKE").

	[https://libreswan.org/](https://libreswan.org/) || [libreswan](https://aur.archlinux.org/packages/libreswan/)

*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** — Supports a variety of protocols (e.g. MS, Cisco, Fortinet) via a plugin system.

	[https://wiki.gnome.org/Projects/NetworkManager/VPN](https://wiki.gnome.org/Projects/NetworkManager/VPN) || [networkmanager](https://www.archlinux.org/packages/?name=networkmanager)

*   **[OpenConnect](/index.php/OpenConnect "OpenConnect")** — Supports Cisco and Juniper VPNs.

	[http://www.infradead.org/openconnect/](http://www.infradead.org/openconnect/) || [openconnect](https://www.archlinux.org/packages/?name=openconnect)

*   **[Openswan](/index.php/Openswan "Openswan")** — IPsec-based VPN Solution.

	[https://www.openswan.org/](https://www.openswan.org/) || [openswan](https://aur.archlinux.org/packages/openswan/)

*   **[OpenVPN](/index.php/OpenVPN "OpenVPN")** — To connect to OpenVPN VPNs.

	[https://openvpn.net/](https://openvpn.net/) || [openvpn](https://www.archlinux.org/packages/?name=openvpn)

*   **[PPTP Client](/index.php/PPTP_Client "PPTP Client")** — To connect to PPTP VPNs, like Microsoft VPNs (MPPE). (insecure)

	[http://pptpclient.sourceforge.net/](http://pptpclient.sourceforge.net/) || [pptpclient](https://www.archlinux.org/packages/?name=pptpclient)

*   **[strongSwan](/index.php/StrongSwan "StrongSwan")** — IPsec-based VPN Solution.

	[https://www.strongswan.org/](https://www.strongswan.org/) || [strongswan](https://www.archlinux.org/packages/?name=strongswan)

*   **[tinc](/index.php/Tinc "Tinc")** — tinc is a free VPN daemon.

	[https://www.tinc-vpn.org/](https://www.tinc-vpn.org/) || [tinc](https://www.archlinux.org/packages/?name=tinc)

*   **[Vpnc](/index.php/Vpnc "Vpnc")** — To connect to Cisco 3000 VPN Concentrators.

	[https://www.unix-ag.uni-kl.de/~massar/vpnc/](https://www.unix-ag.uni-kl.de/~massar/vpnc/) || [vpnc](https://www.archlinux.org/packages/?name=vpnc)

*   **[WireGuard](/index.php/WireGuard "WireGuard")** — Next generation secure network tunnel.

	[https://www.wireguard.com/](https://www.wireguard.com/) || [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools)

#### Proxy servers

*   **Dante** — SOCKS server and SOCKS client, implementing RFC 1928 and related standards.

	[https://www.inet.no/dante/](https://www.inet.no/dante/) || [dante](https://www.archlinux.org/packages/?name=dante)

*   **[Privoxy](/index.php/Privoxy "Privoxy")** — Non-caching web proxy with advanced filtering capabilities for enhancing privacy, modifying web page data and HTTP headers, controlling access, and removing ads and other obnoxious Internet junk.

	[https://www.privoxy.org/](https://www.privoxy.org/) || [privoxy](https://www.archlinux.org/packages/?name=privoxy)

*   **Project V** — Project V is a set of tools to help you build your own privacy network over internet.

	[https://www.v2fly.org/en/](https://www.v2fly.org/en/) || [v2ray](https://www.archlinux.org/packages/?name=v2ray)

*   **[Shadowsocks](/index.php/Shadowsocks "Shadowsocks")** — Secure socks5 proxy, designed to protect your Internet traffic.

	[https://www.shadowsocks.org/en/index.html](https://www.shadowsocks.org/en/index.html) || Python: [shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks), C: [shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev), Qt: [shadowsocks-qt5](https://www.archlinux.org/packages/?name=shadowsocks-qt5)

*   **[Squid](/index.php/Squid "Squid")** — Caching proxy for the Web supporting HTTP, HTTPS, FTP, and more.

	[http://www.squid-cache.org/](http://www.squid-cache.org/) || [squid](https://www.archlinux.org/packages/?name=squid)

*   **[Stunnel](/index.php/Stunnel "Stunnel")** — A server and client to add and remove TLS encryption to TCP data flow.

	[https://www.stunnel.org/](https://www.stunnel.org/) || [stunnel](https://www.archlinux.org/packages/?name=stunnel)

*   **Tinyproxy** — Lightweight HTTP/HTTPS proxy daemon.

	[https://tinyproxy.github.io/](https://tinyproxy.github.io/) || [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy)

*   **[Trojan](/index.php/Trojan "Trojan")** — An unidentifiable mechanism that helps you bypass GFW.

	[https://trojan-gfw.github.io/trojan/](https://trojan-gfw.github.io/trojan/) || [trojan](https://www.archlinux.org/packages/?name=trojan)

*   **[Varnish](/index.php/Varnish "Varnish")** — High-performance HTTP accelerator.

	[https://varnish-cache.org/](https://varnish-cache.org/) || [varnish](https://www.archlinux.org/packages/?name=varnish)

*   **Ziproxy** — Forwarding (non-caching) compressing HTTP proxy server.

	[http://ziproxy.sourceforge.net/](http://ziproxy.sourceforge.net/) || [ziproxy](https://www.archlinux.org/packages/?name=ziproxy)

#### Anonymizing networks

*   **[Freenet](/index.php/Freenet "Freenet")** — An encrypted network without censorship.

	[https://freenetproject.org/](https://freenetproject.org/) || [freenet](https://aur.archlinux.org/packages/freenet/)

*   **[GNUnet](/index.php/GNUnet "GNUnet")** — Framework for secure peer-to-peer networking.

	[https://gnunet.org/](https://gnunet.org/) || CLI: [gnunet](https://www.archlinux.org/packages/?name=gnunet), GUI: [gnunet-gtk](https://www.archlinux.org/packages/?name=gnunet-gtk)

*   **[I2P](/index.php/I2P "I2P")** — Distributed anonymous network.

	[https://geti2p.net/](https://geti2p.net/) || [i2p](https://aur.archlinux.org/packages/i2p/), [i2p-bin](https://aur.archlinux.org/packages/i2p-bin/)

*   **[Lantern](/index.php/Lantern "Lantern")** — Peer-to-peer internet censorship circumvention software.

	[https://getlantern.org/](https://getlantern.org/) || [lantern-bin](https://aur.archlinux.org/packages/lantern-bin/)

*   **[Tor](/index.php/Tor "Tor")** — Anonymizing overlay network.

	[https://www.torproject.org/](https://www.torproject.org/) || [tor](https://www.archlinux.org/packages/?name=tor)

### Web browsers

See also [Wikipedia:Comparison of web browsers](https://en.wikipedia.org/wiki/Comparison_of_web_browsers "wikipedia:Comparison of web browsers").

#### Console

*   **[ELinks](/index.php/ELinks "ELinks")** — Advanced and well-established feature-rich text mode web browser with mouse wheel scroll support (links fork, barely supported since 2009).

	[http://elinks.or.cz/](http://elinks.or.cz/) || [elinks](https://www.archlinux.org/packages/?name=elinks)

*   **[Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")** — Graphics and text mode web browser. Includes a console version similar to Lynx.

	[http://links.twibright.com/](http://links.twibright.com/) || [links](https://www.archlinux.org/packages/?name=links)

*   **[Lynx](https://en.wikipedia.org/wiki/Lynx_(web_browser) "wikipedia:Lynx (web browser)")** — Text browser for the World Wide Web.

	[https://lynx.invisible-island.net/](https://lynx.invisible-island.net/) || [lynx](https://www.archlinux.org/packages/?name=lynx)

*   **[w3m](https://en.wikipedia.org/wiki/W3m "wikipedia:W3m")** — Pager/text-based web browser. It has vim-like keybindings, and is able to display images.

	[http://w3m.sourceforge.net/](http://w3m.sourceforge.net/) || [w3m](https://www.archlinux.org/packages/?name=w3m)

#### Graphical

##### Gecko-based

See also [Wikipedia:Gecko (software)](https://en.wikipedia.org/wiki/Gecko_(software) "wikipedia:Gecko (software)").

*   **[Firefox](/index.php/Firefox "Firefox")** — Extensible browser from Mozilla based on Gecko with fast rendering.

	[https://mozilla.com/firefox](https://mozilla.com/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

*   **[SeaMonkey](https://en.wikipedia.org/wiki/SeaMonkey "wikipedia:SeaMonkey")** — Continuation of the Mozilla Internet Suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

###### Firefox spin-offs

*   **[Cliqz](https://en.wikipedia.org/wiki/Cliqz "wikipedia:Cliqz")** — Firefox-based privacy aware web browser.

	[https://cliqz.com/](https://cliqz.com/) || [cliqz](https://aur.archlinux.org/packages/cliqz/) or [cliqz-bin](https://aur.archlinux.org/packages/cliqz-bin/)

*   **Cyberfox** — Fast and privacy oriented fork of Mozilla Firefox.

	[https://cyberfox.8pecxstudios.com/](https://cyberfox.8pecxstudios.com/) || [cyberfox-bin](https://aur.archlinux.org/packages/cyberfox-bin/)

*   **[GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat")** — A customized build of Firefox ESR distributed by the GNU Project, stripped of non-free components and with additional privacy extensions. Release cycle may be delayed compared to Mozilla Firefox.

	[https://www.gnu.org/software/gnuzilla/](https://www.gnu.org/software/gnuzilla/) || [icecat](https://aur.archlinux.org/packages/icecat/) or [icecat-bin](https://aur.archlinux.org/packages/icecat-bin/)

*   **LibreWolf** — A fork of Firefox, focused on privacy, security and freedom.

	[https://librewolf-community.gitlab.io/](https://librewolf-community.gitlab.io/) || [librewolf](https://aur.archlinux.org/packages/librewolf/) or [librewolf-bin](https://aur.archlinux.org/packages/librewolf-bin/)

*   **Waterfox Classic** — Optimized fork of Mozilla Firefox, without data collection and allowing unsigned extensions and NPAPI plugins.

	[https://www.waterfox.net/](https://www.waterfox.net/) || [waterfox-classic-bin](https://aur.archlinux.org/packages/waterfox-classic-bin/)

*   **Waterfox Current** — Optimized fork of Mozilla Firefox, updated feature-rich branch of Waterfox.

	[https://www.waterfox.net/](https://www.waterfox.net/) || [waterfox-current-bin](https://aur.archlinux.org/packages/waterfox-current-bin/)

##### Blink-based

See also [Wikipedia:Blink (web engine)](https://en.wikipedia.org/wiki/Blink_(web_engine) "wikipedia:Blink (web engine)").

*   **[Chromium](/index.php/Chromium "Chromium")** — Web browser developed by Google, the open source project behind Google Chrome.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

###### Privacy-focused chromium spin-offs

*   **[Brave](https://en.wikipedia.org/wiki/Brave_(web_browser) "wikipedia:Brave (web browser)")** — Web browser that blocks ads and trackers by default.

	[https://www.brave.com/](https://www.brave.com/) || [brave-bin](https://aur.archlinux.org/packages/brave-bin/)

*   **Iridium** — A privacy-focused [patchset](https://git.iridiumbrowser.de/cgit.cgi/iridium-browser/tree/?h=patchview) for Chromium. See [differences from Chromium](https://github.com/iridium-browser/tracker/wiki/Differences-between-Iridium-and-Chromium).

	[https://iridiumbrowser.de/](https://iridiumbrowser.de/) || [iridium-deb](https://aur.archlinux.org/packages/iridium-deb/)

*   **Ungoogled Chromium** — Modifications to Google Chromium for removing Google integration and enhancing privacy, control, and transparency

	[https://github.com/Eloston/ungoogled-chromium](https://github.com/Eloston/ungoogled-chromium) || [ungoogled-chromium](https://aur.archlinux.org/packages/ungoogled-chromium/)

###### Proprietary chromium spin-offs

*   **[Google Chrome](/index.php/Google_Chrome "Google Chrome")** — Proprietary web browser developed by Google.

	[https://www.google.com/chrome/](https://www.google.com/chrome/) || [google-chrome](https://aur.archlinux.org/packages/google-chrome/)

*   **[Opera](/index.php/Opera "Opera")** — Proprietary browser developed by Opera Software.

	[https://opera.com](https://opera.com) || [opera](https://www.archlinux.org/packages/?name=opera)

*   **[Slimjet](https://en.wikipedia.org/wiki/SlimBrowser "wikipedia:SlimBrowser")** — Fast, smart and powerful proprietary browser based on Chromium.

	[https://www.slimjet.com/](https://www.slimjet.com/) || [slimjet](https://aur.archlinux.org/packages/slimjet/)

*   **[Vivaldi](/index.php/Vivaldi "Vivaldi")** — An advanced proprietary browser made with the power user in mind.

	[https://vivaldi.com/](https://vivaldi.com/) || [vivaldi](https://aur.archlinux.org/packages/vivaldi/)

*   **[Yandex Browser](https://en.wikipedia.org/wiki/Yandex_Browser "wikipedia:Yandex Browser")** — Proprietary browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.

	[https://browser.yandex.com/](https://browser.yandex.com/) || [yandex-browser-beta](https://aur.archlinux.org/packages/yandex-browser-beta/)

###### Browsers based on qt5-webengine

*   **Crusta** — Blazingly fast full feature web browser with unique features.

	[https://github.com/Crusta/CrustaBrowser/](https://github.com/Crusta/CrustaBrowser/) || [crusta](https://aur.archlinux.org/packages/crusta/)

*   **[Dooble](https://en.wikipedia.org/wiki/Dooble "wikipedia:Dooble")** — Colorful Web browser.

	[https://textbrowser.github.io/dooble/](https://textbrowser.github.io/dooble/) || [dooble](https://aur.archlinux.org/packages/dooble/)

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — QtWebEngine-based HTML browser, part of the eric6 development toolset, can be launched with the `eric6_browser` command.

	[https://eric-ide.python-projects.org/](https://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric)

*   **[Falkon](https://en.wikipedia.org/wiki/Falkon "wikipedia:Falkon")** — Web browser based on QtWebEngine, written in Qt framework.

	[https://falkon.org/](https://falkon.org/) || [falkon](https://www.archlinux.org/packages/?name=falkon)

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Web browser based on Qt toolkit and Qt WebEngine (or KHTML layout engine), part of [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/).

	[https://kde.org/applications/internet/org.kde.konqueror](https://kde.org/applications/internet/org.kde.konqueror) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **Liri Browser** — A minimalistic material design web browser written for Liri.

	[https://github.com/lirios/browser](https://github.com/lirios/browser) || [liri-browser-git](https://aur.archlinux.org/packages/liri-browser-git/)

*   **[Otter Browser](/index.php/Otter_Browser "Otter Browser")** — Browser aiming to recreate classic Opera (12.x) UI using Qt5\. It can use Qt WebEngine as an alternative backend.

	[https://otter-browser.org/](https://otter-browser.org/) || [otter-browser](https://www.archlinux.org/packages/?name=otter-browser)

*   **Qt WebBrowser** — Browser for embedded devices developed using the capabilities of Qt and Qt WebEngine.

	[https://doc.qt.io/QtWebBrowser/](https://doc.qt.io/QtWebBrowser/) || [qtwebbrowser](https://aur.archlinux.org/packages/qtwebbrowser/)

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, [vim](/index.php/Vim "Vim")-like browser based on PyQt5 and QtWebEngine.

	[https://qutebrowser.org/](https://qutebrowser.org/) || [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser)

###### Browsers based on electron

*   **Beaker** — Peer-to-peer web browser with tools to create and host websites. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/beakerbrowser/beaker](https://github.com/beakerbrowser/beaker) || [beaker](https://aur.archlinux.org/packages/beaker/)

*   **Min** — A smarter, faster web browser based on the [Electron](https://electronjs.org/) platform.

	[https://minbrowser.github.io/min/](https://minbrowser.github.io/min/) || [min](https://www.archlinux.org/packages/?name=min)

##### WebKit-based

See also [Wikipedia:WebKit](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit").

**Note:** webkitgtk, webkitgtk2 and qtwebkit-based browsers were removed from the list, because these are today considered insecure and outdated. More info [here](https://blogs.gnome.org/mcatanzaro/2016/02/01/on-webkit-security-updates/).

###### Browsers based on webkit2gtk

*   **Eolie** — Simple web browser for GNOME.

	[https://wiki.gnome.org/Apps/Eolie](https://wiki.gnome.org/Apps/Eolie) || [eolie](https://www.archlinux.org/packages/?name=eolie)

*   **[GNOME Web](/index.php/GNOME_Web "GNOME Web")** — Browser which uses the WebKitGTK rendering engine, part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Apps/Web/](https://wiki.gnome.org/Apps/Web/) || [epiphany](https://www.archlinux.org/packages/?name=epiphany)

*   **[Lariza](/index.php/Lariza "Lariza")** — A simple, experimental web browser using GTK 3, GLib and WebKit2GTK.

	[https://www.uninformativ.de/git/lariza/](https://www.uninformativ.de/git/lariza/) || [lariza](https://aur.archlinux.org/packages/lariza/)

*   **[Luakit](/index.php/Luakit "Luakit")** — Fast, small, webkit based browser framework extensible by Lua.

	[https://luakit.github.io/](https://luakit.github.io/) || [luakit](https://www.archlinux.org/packages/?name=luakit)

*   **[Midori](/index.php/Midori "Midori")** — Lightweight web browser based on GTK and WebKit.

	[https://www.midori-browser.org/](https://www.midori-browser.org/) || [midori](https://www.archlinux.org/packages/?name=midori)

*   **Next** — Keyboard-oriented, infinitely extensible browser.

	[https://next.atlas.engineer/](https://next.atlas.engineer/) || [next-browser-git](https://aur.archlinux.org/packages/next-browser-git/)

*   **[surf](/index.php/Surf "Surf")** — Lightweight WebKit-based browser, which follows the [suckless ideology](https://suckless.org/philosophy) (basically, the browser itself is a single C source file).

	[https://surf.suckless.org/](https://surf.suckless.org/) || [surf](https://www.archlinux.org/packages/?name=surf)

*   **Surfer** — Simple keyboard based web browser, written in C.

	[https://github.com/nihilowy/surfer](https://github.com/nihilowy/surfer) || [surfer-git](https://aur.archlinux.org/packages/surfer-git/)

*   **Vimb** — A Vim-like web browser that is inspired by Pentadactyl and Vimprobable.

	[https://fanglingsu.github.io/vimb/](https://fanglingsu.github.io/vimb/) || [vimb](https://www.archlinux.org/packages/?name=vimb)

###### Browsers based on qt5-webkit

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — QtWebKit-based HTML browser, part of the eric6 development toolset, can be launched with the `eric6_webbrowser` command.

	[https://eric-ide.python-projects.org/](https://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric)

*   **OSPKit** — Webkit based html browser for printing.

	[http://osp.kitchen/tools/ospkit/](http://osp.kitchen/tools/ospkit/) || [ospkit-git](https://aur.archlinux.org/packages/ospkit-git/)

*   **[Otter Browser](/index.php/Otter_Browser "Otter Browser")** — Browser aiming to recreate classic Opera (12.x) UI using Qt5.

	[https://otter-browser.org/](https://otter-browser.org/) || [otter-browser](https://www.archlinux.org/packages/?name=otter-browser) or [otter-browser-nowebengine](https://www.archlinux.org/packages/?name=otter-browser-nowebengine)

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, [vim](/index.php/Vim "Vim")-like browser based on PyQt5 with QtWebKit as an available backend.

	[https://github.com/qutebrowser/qutebrowser](https://github.com/qutebrowser/qutebrowser) || [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser)

*   **smtube** — Application that allows to browse, search and play YouTube videos.

	[https://www.smtube.org/](https://www.smtube.org/) || [smtube](https://www.archlinux.org/packages/?name=smtube)

*   **WCGBrowser** — A web browser for kiosk systems.

	[http://www.alandmoore.com/wcgbrowser/wcgbrowser.html](http://www.alandmoore.com/wcgbrowser/wcgbrowser.html) || [wcgbrowser-git](https://aur.archlinux.org/packages/wcgbrowser-git/)

##### Other

*   **[Dillo](https://en.wikipedia.org/wiki/Dillo "wikipedia:Dillo")** — Small, fast graphical web browser built on [FLTK](https://en.wikipedia.org/wiki/Fltk "wikipedia:Fltk"). Uses its own layout engine.

	[https://www.dillo.org/](https://www.dillo.org/) || [dillo](https://www.archlinux.org/packages/?name=dillo)

*   **[Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")** — Graphics and text mode web browser. Includes a graphical X-window/framebuffer version with CSS, image rendering, pull-down menus. It can be launched with the `xlinks -g` command.

	[http://links.twibright.com/](http://links.twibright.com/) || [links](https://www.archlinux.org/packages/?name=links)

*   **[NetSurf](https://en.wikipedia.org/wiki/NetSurf "wikipedia:NetSurf")** — Featherweight browser written in C, notable for its slowly developing JavaScript support and fast rendering through its own layout engine.

	[http://www.netsurf-browser.org/](http://www.netsurf-browser.org/) || [netsurf](https://www.archlinux.org/packages/?name=netsurf)

*   **[Pale Moon](https://en.wikipedia.org/wiki/Pale_Moon_(web_browser) layout engine, a fork of Gecko. Firefox add-ons may not be compatible. [[1]](https://addons.palemoon.org/firefox/incompatible/) Without support for newer Firefox features such as cache2, e10s, and OTMC.

	[http://www.palemoon.org/](http://www.palemoon.org/) || [palemoon](https://aur.archlinux.org/packages/palemoon/) or [palemoon-bin](https://aur.archlinux.org/packages/palemoon-bin/)

### Web servers

A [web server](https://en.wikipedia.org/wiki/Web_server "wikipedia:Web server") serves HTML web pages and other files via HTTP to clients like [web browsers](/index.php/Category:Web_browser "Category:Web browser"). The major web servers can be interfaced with programs to serve dynamic content ([web applications](/index.php/Web_applications "Web applications")).

See also [Category:Web server](/index.php/Category:Web_server "Category:Web server") and [Wikipedia:Comparison of web server software](https://en.wikipedia.org/wiki/Comparison_of_web_server_software "wikipedia:Comparison of web server software").

*   **[Apache](/index.php/Apache "Apache")** — A high performance Unix-based HTTP server.

	[http://www.apache.org/dist/httpd/](http://www.apache.org/dist/httpd/) || [apache](https://www.archlinux.org/packages/?name=apache)

*   **[Caddy](/index.php/Caddy "Caddy")** — HTTP/2 web server with automatic HTTPS.

	[https://caddyserver.com/](https://caddyserver.com/) || [caddy](https://aur.archlinux.org/packages/caddy/)

*   **[Hiawatha](/index.php/Hiawatha "Hiawatha")** — Secure and advanced web server.

	[https://www.hiawatha-webserver.org/](https://www.hiawatha-webserver.org/) || [hiawatha](https://www.archlinux.org/packages/?name=hiawatha)

*   **[Lighttpd](/index.php/Lighttpd "Lighttpd")** — A secure, fast, compliant and very flexible web-server.

	[http://www.lighttpd.net/](http://www.lighttpd.net/) || [lighttpd](https://www.archlinux.org/packages/?name=lighttpd)

*   **[nginx](/index.php/Nginx "Nginx")** — Lightweight HTTP server and IMAP/POP3 proxy server.

	[https://nginx.org/](https://nginx.org/) || [nginx](https://www.archlinux.org/packages/?name=nginx)

*   **sthttpd** — Supported fork of the thttpd web server.

	[https://github.com/blueness/sthttpd](https://github.com/blueness/sthttpd) || [sthttpd](https://www.archlinux.org/packages/?name=sthttpd)

*   **yaws** — Web server/framework written in Erlang.

	[http://yaws.hyber.org/](http://yaws.hyber.org/) || [yaws](https://www.archlinux.org/packages/?name=yaws)

#### Static web servers

*   **darkhttpd** — A small and secure static web server, written in C, does not support HTTPS or Auth.

	[https://unix4lyfe.org/darkhttpd/](https://unix4lyfe.org/darkhttpd/) || [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd)

*   **KatWeb** — A lightweight static web server and reverse proxy, written in Go, designed for the modern web.

	[https://github.com/kittyhacker101/KatWeb](https://github.com/kittyhacker101/KatWeb) || [katweb](https://aur.archlinux.org/packages/katweb/)

*   **quark** — An extremly small and simple http get-only web server. It only serves static pages on a single host.

	[http://tools.suckless.org/quark/](http://tools.suckless.org/quark/) || [quark-git](https://aur.archlinux.org/packages/quark-git/)

*   **serve** — Static file serving and directory listing.

	[https://github.com/zeit/serve](https://github.com/zeit/serve) || [nodejs-serve](https://aur.archlinux.org/packages/nodejs-serve/)

*   **servy** — A tiny little web server, single binary, written in Rust.

	[https://github.com/zethra/servy](https://github.com/zethra/servy) || [servy](https://aur.archlinux.org/packages/servy/)

*   **Webfs** — Simple and instant web server for mostly static content.

	[http://linux.bytesex.org/misc/webfs.html](http://linux.bytesex.org/misc/webfs.html) || [webfs](https://www.archlinux.org/packages/?name=webfs)

The [Python](/index.php/Python "Python") standard library module [http.server](https://docs.python.org/library/http.server.html) can also be used from the command-line.

#### Specialized web servers

*   **Mongoose** — Embedded web server library, supports WebSocket and MQTT.

	[https://github.com/cesanta/mongoose](https://github.com/cesanta/mongoose) || [mongoose](https://aur.archlinux.org/packages/mongoose/)

*   **webhook** — Small server for creating HTTP endpoints (hooks)

	[https://github.com/adnanh/webhook](https://github.com/adnanh/webhook) || [webhook](https://www.archlinux.org/packages/?name=webhook)

*   **Woof** — An ad-hoc single file webserver; Web Offer One File.

	[http://www.home.unix-ag.org/simon/woof.html](http://www.home.unix-ag.org/simon/woof.html) || [woof](https://aur.archlinux.org/packages/woof/)

#### WSGI servers

*   **Gunicorn** — A Python WSGI HTTP Server for UNIX.

	[https://gunicorn.org/](https://gunicorn.org/) || [gunicorn](https://www.archlinux.org/packages/?name=gunicorn), [python2-gunicorn](https://aur.archlinux.org/packages/python2-gunicorn/)

*   **[uWSGI](/index.php/UWSGI "UWSGI")** — A fast, self-healing and developer/sysadmin-friendly application container server written in C.

	[https://uwsgi-docs.readthedocs.io/](https://uwsgi-docs.readthedocs.io/) || [uwsgi](https://www.archlinux.org/packages/?name=uwsgi)

*   **Waitress** — A WSGI server for Python 2 and 3.

	[https://github.com/Pylons/waitress](https://github.com/Pylons/waitress) || [python-waitress](https://www.archlinux.org/packages/?name=python-waitress), [python2-waitress](https://www.archlinux.org/packages/?name=python2-waitress)

Apache also supports WSGI with [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi").

#### Performance testing

*   **http_load** — A webserver performance testing tool, runs in a single process.

	[http://www.acme.com/software/http_load/](http://www.acme.com/software/http_load/) || [http_load](https://aur.archlinux.org/packages/http_load/)

*   **httperf** — Can generate various HTTP workloads, written in C.

	[https://github.com/httperf/httperf](https://github.com/httperf/httperf) || [httperf](https://aur.archlinux.org/packages/httperf/)

*   **vegeta** — HTTP load testing tool, written in Go.

	[https://github.com/tsenart/vegeta](https://github.com/tsenart/vegeta) || [vegeta](https://www.archlinux.org/packages/?name=vegeta)

*   **Web Bench** — Benchmarking tool, uses fork() for simulating multiple clients.

	[http://home.tiscali.cz/~cz210552/webbench.html](http://home.tiscali.cz/~cz210552/webbench.html) || [webbench](https://aur.archlinux.org/packages/webbench/)

### File sharing

#### Download managers

See also [Wikipedia:Comparison of download managers](https://en.wikipedia.org/wiki/Comparison_of_download_managers "wikipedia:Comparison of download managers").

##### Console

*   **[aria2](/index.php/Aria2 "Aria2")** — Lightweight download utility that supports HTTP, FTP, SFTP, BitTorrent and Metalink. It can run as a daemon controlled via a built-in JSON-RPC or XML-RPC interface.

	[https://aria2.github.io/](https://aria2.github.io/) || [aria2](https://www.archlinux.org/packages/?name=aria2)

*   **Axel** — Light command line download accelerator. Supports HTTP and FTP.

	[https://github.com/eribertomota/axel](https://github.com/eribertomota/axel) || [axel](https://www.archlinux.org/packages/?name=axel)

*   **[cURL](https://en.wikipedia.org/wiki/cURL "wikipedia:cURL")** — An URL retrieval utility and library. Supports HTTP, FTP and SFTP.

	[https://curl.haxx.se/](https://curl.haxx.se/) || [curl](https://www.archlinux.org/packages/?name=curl)

*   **[LFTP](https://en.wikipedia.org/wiki/Lftp "wikipedia:Lftp")** — Sophisticated file transfer program. Supports HTTP, FTP, SFTP, FISH, and BitTorrent.

	[http://lftp.yar.ru/](http://lftp.yar.ru/) || [lftp](https://www.archlinux.org/packages/?name=lftp)

*   **mps-youtube** — Terminal based YouTube jukebox with playlist management. Plays audio/video through mplayer/mpv.

	[https://github.com/mps-youtube/mps-youtube](https://github.com/mps-youtube/mps-youtube) || [mps-youtube](https://www.archlinux.org/packages/?name=mps-youtube)

*   **Plowshare** — A set of command-line tools designed for managing file-sharing websites (aka Hosters).

	[https://github.com/mcrapet/plowshare](https://github.com/mcrapet/plowshare) || [plowshare](https://www.archlinux.org/packages/?name=plowshare)

*   **[RTMPDump](https://en.wikipedia.org/wiki/RTMPDump "wikipedia:RTMPDump")** — Download FLV videos through RTMP (Adobe's proprietary protocol for Flash video players)

	[http://rtmpdump.mplayerhq.hu/](http://rtmpdump.mplayerhq.hu/) || [rtmpdump](https://www.archlinux.org/packages/?name=rtmpdump)

*   **snarf** — Command-line URL retrieval tool. Supports HTTP and FTP.

	[https://www.xach.com/snarf/](https://www.xach.com/snarf/) || [snarf](https://www.archlinux.org/packages/?name=snarf)

*   **[Streamlink](/index.php/Streamlink "Streamlink")** — Launch streams from various streaming services in a custom video player or save them to a file.

	[https://streamlink.github.io/](https://streamlink.github.io/) || [streamlink](https://www.archlinux.org/packages/?name=streamlink)

*   **[Streamripper](https://en.wikipedia.org/wiki/Streamripper "wikipedia:Streamripper")** — Records and splits streaming mp3 into tracks.

	[http://streamripper.sourceforge.net/](http://streamripper.sourceforge.net/) || [streamripper](https://aur.archlinux.org/packages/streamripper/)

*   **You-Get** — Download media contents (videos, audios, images) from the Web.

	[https://you-get.org/](https://you-get.org/) || [you-get](https://www.archlinux.org/packages/?name=you-get)

*   **[youtube-dl](/index.php/Youtube-dl "Youtube-dl")** — Download videos from YouTube and many other web sites.

	[https://rg3.github.io/youtube-dl/](https://rg3.github.io/youtube-dl/) || [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl)

*   **youtube-viewer** — Command line utility for viewing YouTube videos.

	[https://github.com/trizen/youtube-viewer](https://github.com/trizen/youtube-viewer) || [youtube-viewer](https://www.archlinux.org/packages/?name=youtube-viewer)

*   **[Wget](https://en.wikipedia.org/wiki/Wget "wikipedia:Wget")** — A network utility to retrieve files from the Web. Supports HTTP and FTP.

	[https://www.gnu.org/software/wget/](https://www.gnu.org/software/wget/) || [wget](https://www.archlinux.org/packages/?name=wget)

##### Graphical

*   **ClipGrab** — Downloader and converter for YouTube, Vimeo and many other online video sites.

	[https://clipgrab.org/](https://clipgrab.org/) || [clipgrab](https://www.archlinux.org/packages/?name=clipgrab)

*   **FatRat** — Qt based download manager with support for HTTP, FTP, SFTP, BitTorrent and Metalink.

	[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)

*   **FreeRapid** — Java-based downloader that supports downloading from file-sharing services.

	[http://wordrider.net/freerapid/](http://wordrider.net/freerapid/) || [freerapid](https://aur.archlinux.org/packages/freerapid/)

*   **[FrostWire](https://en.wikipedia.org/wiki/FrostWire "wikipedia:FrostWire")** — Easy to use cloud downloader, BitTorrent client and media player.

	[https://www.frostwire.com/](https://www.frostwire.com/) || [frostwire](https://aur.archlinux.org/packages/frostwire/)

*   **gtk-youtube-viewer** — GTK utility for viewing YouTube videos.

	[https://github.com/trizen/youtube-viewer](https://github.com/trizen/youtube-viewer) || [youtube-viewer](https://www.archlinux.org/packages/?name=youtube-viewer) + [gtk2-perl](https://www.archlinux.org/packages/?name=gtk2-perl) + [perl-file-sharedir](https://www.archlinux.org/packages/?name=perl-file-sharedir)

*   **[Gwget](https://en.wikipedia.org/wiki/Wget#GWget "wikipedia:Wget")** — Download manager for GNOME. Supports HTTP and FTP.

	[https://projects.gnome.org/gwget/](https://projects.gnome.org/gwget/) || [gwget](https://www.archlinux.org/packages/?name=gwget)

*   **Gydl** — GUI wrapper around the already existing youtube-dl program to download content from sites like YouTube.

	[https://github.com/JannikHv/gydl](https://github.com/JannikHv/gydl) || [gydl-git](https://aur.archlinux.org/packages/gydl-git/)

*   **[JDownloader](/index.php/JDownloader "JDownloader")** — Java-based downloader for one-click hosting sites.

	[http://jdownloader.org/](http://jdownloader.org/) || [jdownloader2](https://aur.archlinux.org/packages/jdownloader2/)

*   **[KGet](https://en.wikipedia.org/wiki/KGet "wikipedia:KGet")** — Download manager for KDE. Supports HTTP, FTP, BitTorrent and Metalink. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[https://www.kde.org/applications/internet/kget/](https://www.kde.org/applications/internet/kget/) || [kget](https://www.archlinux.org/packages/?name=kget)

*   **Persepolis** — Graphical front-end for aria2 download manager with lots of features. Supports HTTP and FTP.

	[https://persepolisdm.github.io/](https://persepolisdm.github.io/) || [persepolis](https://aur.archlinux.org/packages/persepolis/)

*   **[pyLoad](/index.php/PyLoad "PyLoad")** — Downloader written in Python and designed to be extremely lightweight, easily extensible and fully manageable via web.

	[https://pyload.net/](https://pyload.net/) || [pyload](https://aur.archlinux.org/packages/pyload/)

*   **Steadyflow** — Simple download manager for GNOME. Supports HTTP and FTP.

	[https://launchpad.net/steadyflow](https://launchpad.net/steadyflow) || [steadyflow](https://www.archlinux.org/packages/?name=steadyflow)

*   **Streamtuner2** — Internet radio station and video browser. It simply lists stations in categories from different directories and launches your preferred media apps for playback.

	[https://sourceforge.net/projects/streamtuner2/](https://sourceforge.net/projects/streamtuner2/) || [streamtuner2](https://aur.archlinux.org/packages/streamtuner2/)

*   **uGet** — GTK download manager featuring download classification and HTML import. Supports HTTP, FTP, BitTorrent, Metalink, YouTube and Mega.

	[https://ugetdm.com/](https://ugetdm.com/) || [uget](https://www.archlinux.org/packages/?name=uget)

*   **Xtreme Download Manager** — Powerful tool to increase download speed up-to 500%. Supports HTTP and FTP. Video grabber works in a general way and is not limited to certain websites.

	[http://xdman.sourceforge.net/](http://xdman.sourceforge.net/) || [xdman](https://aur.archlinux.org/packages/xdman/)

#### Cloud storage servers

*   **[Cozy](/index.php/Cozy "Cozy")** — A personal cloud you can hack, host and delete.

	[https://cozy.io/](https://cozy.io/) || [cozy-stack](https://www.archlinux.org/packages/?name=cozy-stack)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud")** — A cloud server to store your files centrally on a hardware controlled by you.

	[https://nextcloud.com](https://nextcloud.com) || [nextcloud](https://www.archlinux.org/packages/?name=nextcloud)

*   **[Pydio](/index.php/Pydio "Pydio")** — Mature open source web application for file sharing and synchronization.

	[https://pydio.com/](https://pydio.com/) || [pydio](https://aur.archlinux.org/packages/pydio/)

*   **[Seafile](/index.php/Seafile "Seafile")** — An online file storage and collaboration tool with advanced support for file syncing, privacy protection and teamwork.

	[https://www.seafile.com/](https://www.seafile.com/) || [seafile-server](https://aur.archlinux.org/packages/seafile-server/)

#### Cloud synchronization clients

**Tip:**

*   Some [synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") provide direct support for some cloud-storage services.
*   Some [FUSE filesystems](/index.php/FUSE#List_of_FUSE_filesystems "FUSE") provide a way to mount cloud-storage as a filesystem. Google Drive can be accessed also by [gvfs-google](https://www.archlinux.org/packages/?name=gvfs-google) for GVFS-based applications (like [Nautilus](/index.php/Nautilus "Nautilus")), and by [kio-gdrive](https://www.archlinux.org/packages/?name=kio-gdrive) for KIO-based applications (like [Dolphin](/index.php/Dolphin "Dolphin")).
*   See [Disk encryption#Cloud-storage optimized](/index.php/Disk_encryption#Cloud-storage_optimized "Disk encryption") to achieve zero-knowledge (client-side transparent encryption) storage on any third-party cloud service.

*   **aws-cli** — CLI for Amazon Web Services, including efficient file transfers to and from Amazon S3.

	[https://aws.amazon.com/cli/](https://aws.amazon.com/cli/) || [aws-cli](https://www.archlinux.org/packages/?name=aws-cli)

*   **Backblaze B2** — Backblaze B2 open-source command-line client.

	[https://www.backblaze.com/b2/cloud-storage.html](https://www.backblaze.com/b2/cloud-storage.html) || [backblaze-b2](https://aur.archlinux.org/packages/backblaze-b2/)

*   **CloudCross** — Synchronize local files and folders with many cloud providers. Mail.ru Cloud, Yandex Disk, Google Drive, OneDrive and Dropbox support is available.

	[https://cloudcross.mastersoft24.ru/](https://cloudcross.mastersoft24.ru/) || [cloudcross](https://aur.archlinux.org/packages/cloudcross/)

*   **[Cozy](/index.php/Cozy "Cozy") Drive** — Desktop client for Cozy.

	[https://cozy-labs.github.io/cozy-desktop/](https://cozy-labs.github.io/cozy-desktop/) || [cozy-desktop](https://www.archlinux.org/packages/?name=cozy-desktop)

*   **drive** — Tiny program to pull or push Google Drive files.

	[https://github.com/odeke-em/drive](https://github.com/odeke-em/drive) || [drive-bin](https://aur.archlinux.org/packages/drive-bin/), [drive-git](https://aur.archlinux.org/packages/drive-git/)

*   **DriveSync** — Command line utility that synchronizes your Google Drive files with a local folder on your machine.

	[https://github.com/MStadlmeier/drivesync](https://github.com/MStadlmeier/drivesync) || [drivesync](https://aur.archlinux.org/packages/drivesync/)

*   **[Dropbox](/index.php/Dropbox "Dropbox")** — Proprietary desktop client for Dropbox.

	[https://www.dropbox.com/](https://www.dropbox.com/) || [dropbox](https://aur.archlinux.org/packages/dropbox/)

*   **gdrive** — Command line utility for interacting with Google Drive.

	[https://github.com/prasmussen/gdrive](https://github.com/prasmussen/gdrive) || [gdrive](https://aur.archlinux.org/packages/gdrive/)

*   **Grive** — Google Drive client with support for new Drive REST API and partial sync.

	[https://github.com/vitalif/grive2](https://github.com/vitalif/grive2) || [grive](https://aur.archlinux.org/packages/grive/)

*   **ODrive** — Google Drive GUI for Windows / Mac / Linux.

	[https://github.com/liberodark/ODrive](https://github.com/liberodark/ODrive) || [odrive-bin](https://aur.archlinux.org/packages/odrive-bin/)

*   **hubiC** — Proprietary synchronization client service and command line tools for hubiC.

	[https://hubic.com/en/downloads](https://hubic.com/en/downloads) || [hubic](https://aur.archlinux.org/packages/hubic/)

*   **[Insync](/index.php/Insync "Insync")** — Unofficial proprietary Google Drive desktop client.

	[https://www.insynchq.com/](https://www.insynchq.com/) || [insync](https://aur.archlinux.org/packages/insync/)

*   **[Mail.ru](https://en.wikipedia.org/wiki/Mail.Ru "wikipedia:Mail.Ru") Cloud** — Proprietary client for Mail.ru Cloud storage service.

	[https://cloud.mail.ru/](https://cloud.mail.ru/) || [mailru-cloud](https://aur.archlinux.org/packages/mailru-cloud/)

*   **[Mega](https://en.wikipedia.org/wiki/Mega_(service) Sync Client** — Desktop client to sync files with Mega.

	[https://mega.nz/](https://mega.nz/) || [megasync](https://aur.archlinux.org/packages/megasync/)

*   **Megatools** — Unofficial CLI for Mega.

	[https://megatools.megous.com/](https://megatools.megous.com/) || [megatools](https://aur.archlinux.org/packages/megatools/)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") Client** — Desktop client for Nextcloud.

	[https://nextcloud.com/](https://nextcloud.com/) || [nextcloud-client](https://www.archlinux.org/packages/?name=nextcloud-client)

*   **Nutstore** — Desktop client for Nutstore.

	[https://www.jianguoyun.com/](https://www.jianguoyun.com/) || [nutstore](https://aur.archlinux.org/packages/nutstore/)

*   **OneDrive** — Unofficial CLI for [OneDrive](https://onedrive.live.com/about/).

	[https://github.com/skilion/onedrive](https://github.com/skilion/onedrive) || [onedrive](https://aur.archlinux.org/packages/onedrive/)

*   **[ownCloud](https://en.wikipedia.org/wiki/ownCloud "wikipedia:ownCloud") Desktop Client** — Desktop syncing client for ownCloud.

	[https://owncloud.com/client/](https://owncloud.com/client/) || [owncloud-client](https://www.archlinux.org/packages/?name=owncloud-client)

*   **pCloud Drive** — Proprietary desktop syncing client for pCloud. Based on the [Electron](https://electronjs.org/) platform.

	[https://www.pcloud.com/download-free-online-cloud-file-storage.html](https://www.pcloud.com/download-free-online-cloud-file-storage.html) || [pcloud-drive](https://aur.archlinux.org/packages/pcloud-drive/)

*   **[Pydio](/index.php/Pydio "Pydio")Sync** — Desktop client for Pydio.

	[https://pydio.com/](https://pydio.com/) || [pydio-sync](https://aur.archlinux.org/packages/pydio-sync/)

*   **Rclone** — Multi-provider sync, copy, and mount client.

	[https://rclone.org/](https://rclone.org/) || [rclone](https://www.archlinux.org/packages/?name=rclone)

*   **Rclone Browser** — GUI client for Rclone.

	[https://github.com/kapitainsky/RcloneBrowser](https://github.com/kapitainsky/RcloneBrowser) || [rclone-browser](https://aur.archlinux.org/packages/rclone-browser/)

*   **S3cmd** — Unofficial CLI for Amazon S3.

	[https://s3tools.org/s3cmd](https://s3tools.org/s3cmd) || [s3cmd](https://www.archlinux.org/packages/?name=s3cmd)

*   **[Seafile](/index.php/Seafile "Seafile") Client** — GUI client for Seafile.

	[https://www.seafile.com/](https://www.seafile.com/) || [seafile-client](https://aur.archlinux.org/packages/seafile-client/)

*   **[SpiderOak](https://en.wikipedia.org/wiki/SpiderOak "wikipedia:SpiderOak") One** — Proprietary client for SpiderOak One.

	[https://spideroak.com/](https://spideroak.com/) || [spideroak-one](https://aur.archlinux.org/packages/spideroak-one/)

*   **[Tresorit](https://en.wikipedia.org/wiki/Tresorit "wikipedia:Tresorit")** — Proprietary desktop syncing client for Tresorit.

	[https://tresorit.com/download](https://tresorit.com/download) || [tresorit](https://aur.archlinux.org/packages/tresorit/)

*   **[Yandex Disk](/index.php/Yandex_Disk "Yandex Disk")** — Proprietary CLI for Yandex Disk.

	[https://disk.yandex.ru/](https://disk.yandex.ru/) || [yandex-disk](https://aur.archlinux.org/packages/yandex-disk/)

#### FTP

##### FTP clients

See also [Wikipedia:Comparison of FTP client software](https://en.wikipedia.org/wiki/Comparison_of_FTP_client_software "wikipedia:Comparison of FTP client software").

*   **[FileZilla](https://en.wikipedia.org/wiki/FileZilla "wikipedia:FileZilla")** — Fast and reliable FTP, FTPS and SFTP client.

	[https://filezilla-project.org/](https://filezilla-project.org/) || [filezilla](https://www.archlinux.org/packages/?name=filezilla)

*   **[gFTP](https://en.wikipedia.org/wiki/gFTP "wikipedia:gFTP")** — Multithreaded FTP client for Linux.

	[https://www.gftp.org/](https://www.gftp.org/) || [gftp](https://www.archlinux.org/packages/?name=gftp)

*   **ftp** — Simple ftp client provided by GNU Inetutils

	[https://www.gnu.org/software/inetutils/manual/inetutils.html#ftp-invocation](https://www.gnu.org/software/inetutils/manual/inetutils.html#ftp-invocation) || [inetutils](https://www.archlinux.org/packages/?name=inetutils)

*   **ncftp** — A set of free application programs implementing FTP.

	[https://www.ncftp.com/](https://www.ncftp.com/) || [ncftp](https://www.archlinux.org/packages/?name=ncftp)

*   **[tnftp](https://en.wikipedia.org/wiki/tnftp "wikipedia:tnftp")** — FTP client with several advanced features for [NetBSD](https://en.wikipedia.org/wiki/NetBSD "wikipedia:NetBSD").

	[http://freshmeat.sourceforge.net/projects/tnftp](http://freshmeat.sourceforge.net/projects/tnftp) || [tnftp](https://www.archlinux.org/packages/?name=tnftp)

Some file managers like [Dolphin](/index.php/Dolphin "Dolphin"), [GNOME Files](/index.php/GNOME_Files "GNOME Files") and [Thunar](/index.php/Thunar "Thunar") also provide FTP functionality.

##### FTP servers

See also [Wikipedia:List of FTP server software](https://en.wikipedia.org/wiki/List_of_FTP_server_software "wikipedia:List of FTP server software").

*   **[bftpd](/index.php/Bftpd "Bftpd")** — Small, easy-to-configure FTP server

	[http://bftpd.sourceforge.net/](http://bftpd.sourceforge.net/) || [bftpd](https://www.archlinux.org/packages/?name=bftpd)

*   **chezdav** — WebDAV server that allows to share a particular directory.

	[https://wiki.gnome.org/phodav](https://wiki.gnome.org/phodav) || [phodav](https://www.archlinux.org/packages/?name=phodav)

*   **ftpd** — Simple ftp server provided by GNU Inetutils

	[https://www.gnu.org/software/inetutils/manual/inetutils.html#ftpd-invocation](https://www.gnu.org/software/inetutils/manual/inetutils.html#ftpd-invocation) || [inetutils](https://www.archlinux.org/packages/?name=inetutils)

*   **[proFTPd](/index.php/Proftpd "Proftpd")** — A secure and configurable FTP server

	[http://www.proftpd.org/](http://www.proftpd.org/) || [proftpd](https://aur.archlinux.org/packages/proftpd/)

*   **[Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")** — Free (BSD-licensed), secure, production-quality and standard-compliant FTP server.

	[https://www.pureftpd.org/project/pure-ftpd/](https://www.pureftpd.org/project/pure-ftpd/) || [pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)

*   **[SSH](/index.php/SSH "SSH")** — SFTP is a network protocol that provides file access, file transfer, and file management over any reliable data stream.

	[https://www.openssh.com](https://www.openssh.com) || [openssh](https://www.archlinux.org/packages/?name=openssh)

*   **[vsftpd](/index.php/Vsftpd "Vsftpd")** — Lightweight, stable and secure FTP server for UNIX-like systems.

	[https://security.appspot.com/vsftpd.html](https://security.appspot.com/vsftpd.html) || [vsftpd](https://www.archlinux.org/packages/?name=vsftpd)

#### BitTorrent clients

Some [download managers](#Download_managers) are also able to connect to the BitTorrent network: [Aria2](/index.php/Aria2 "Aria2"), [LFTP](https://en.wikipedia.org/wiki/Lftp "wikipedia:Lftp"), FatRat, [FrostWire](https://en.wikipedia.org/wiki/FrostWire "wikipedia:FrostWire"), [KGet](https://en.wikipedia.org/wiki/KGet "wikipedia:KGet"), [MLDonkey](https://en.wikipedia.org/wiki/MLDonkey "wikipedia:MLDonkey"), uGet.

See also [Wikipedia:Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients").

##### Console

*   **btpd** — The BitTorrent Protocol Daemon.

	[https://github.com/btpd/btpd](https://github.com/btpd/btpd) || [btpd](https://aur.archlinux.org/packages/btpd/)

*   **Ctorrent** — CTorrent is a BitTorrent client implemented in C++ to be lightweight and quick.

	[http://www.rahul.net/dholmes/ctorrent/](http://www.rahul.net/dholmes/ctorrent/) || [enhanced-ctorrent](https://aur.archlinux.org/packages/enhanced-ctorrent/)

*   **peerflix** — Streaming torrent client for node.js.

	[https://github.com/mafintosh/peerflix](https://github.com/mafintosh/peerflix) || [peerflix](https://aur.archlinux.org/packages/peerflix/)

*   **[rTorrent](/index.php/RTorrent "RTorrent")** — Simple and lightweight ncurses BitTorrent client. Requires [libtorrent](https://www.archlinux.org/packages/?name=libtorrent) backend.

	[https://rakshasa.github.io/rtorrent/](https://rakshasa.github.io/rtorrent/) || [rtorrent](https://www.archlinux.org/packages/?name=rtorrent)

*   **[Transmission](/index.php/Transmission "Transmission") CLI** — Simple and easy-to-use BitTorrent client with a daemon version and multiple front-ends. This package includes backend, daemon, command-line interface, and a Web UI interface.

	[https://transmissionbt.com/](https://transmissionbt.com/) || [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli)

##### Graphical

*   **[Deluge](/index.php/Deluge "Deluge")** — User-friendly BitTorrent client written in Python using GTK that can run as a daemon.

	[https://deluge-torrent.org/](https://deluge-torrent.org/) || [deluge](https://www.archlinux.org/packages/?name=deluge)

*   **Fragments** — Easy to use BitTorrent client which follows the GNOME HIG and includes well thought-out features.

	[https://gitlab.gnome.org/World/Fragments](https://gitlab.gnome.org/World/Fragments) || [fragments](https://www.archlinux.org/packages/?name=fragments)

*   **[Ktorrent](/index.php/Ktorrent "Ktorrent")** — Feature-rich BitTorrent client for KDE.

	[https://www.kde.org/applications/internet/ktorrent/](https://www.kde.org/applications/internet/ktorrent/) || [ktorrent](https://www.archlinux.org/packages/?name=ktorrent)

*   **Powder Player** — Hybrid between a streaming BitTorrent client and a player. Based on the [Electron](https://electronjs.org/) platform.

	[https://powder.media/](https://powder.media/) || [powder-player-bin](https://aur.archlinux.org/packages/powder-player-bin/)

*   **[qBittorrent](https://en.wikipedia.org/wiki/qBittorrent "wikipedia:qBittorrent")** — Open source (GPLv2) BitTorrent client that strongly resembles µtorrent.

	[https://www.qbittorrent.org/](https://www.qbittorrent.org/) || [qbittorrent](https://www.archlinux.org/packages/?name=qbittorrent) or [qbittorrent-nox](https://www.archlinux.org/packages/?name=qbittorrent-nox)

*   **[Tixati](https://en.wikipedia.org/wiki/Tixati "wikipedia:Tixati")** — Proprietary peer-to-peer file sharing program that uses the popular BitTorrent protocol.

	[https://tixati.com/](https://tixati.com/) || [tixati](https://aur.archlinux.org/packages/tixati/)

*   **Torrential** — Simple torrent client for elementary OS.

	[https://github.com/davidmhewitt/torrential](https://github.com/davidmhewitt/torrential) || [torrential](https://aur.archlinux.org/packages/torrential/)

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with a daemon version and multiple front-ends.

	[https://transmissionbt.com/](https://transmissionbt.com/) || GTK: [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk), Qt: [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt)

*   **[Transmission](/index.php/Transmission "Transmission") Remote** — GTK client for remote management of the Transmission BitTorrent client, using its HTTP RPC protocol.

	[https://github.com/transmission-remote-gtk/transmission-remote-gtk](https://github.com/transmission-remote-gtk/transmission-remote-gtk) || [transmission-remote-gtk](https://www.archlinux.org/packages/?name=transmission-remote-gtk)

*   **[Tribler](https://en.wikipedia.org/wiki/Tribler "wikipedia:Tribler")** — 4th generation file sharing system BitTorrent client.

	[https://www.tribler.org](https://www.tribler.org) || [tribler](https://www.archlinux.org/packages/?name=tribler)

*   **[Vuze](https://en.wikipedia.org/wiki/Vuze "wikipedia:Vuze")** — Feature-rich BitTorrent client written in Java (formerly Azureus).

	[https://www.vuze.com/](https://www.vuze.com/) || [vuze](https://aur.archlinux.org/packages/vuze/)

*   **WebTorrent Desktop** — Streaming BitTorrent application. Based on the [Electron](https://electronjs.org/) platform.

	[https://webtorrent.io/desktop/](https://webtorrent.io/desktop/) || [webtorrent-desktop](https://aur.archlinux.org/packages/webtorrent-desktop/)

#### Other P2P networks

See also [Wikipedia:Comparison of file-sharing applications](https://en.wikipedia.org/wiki/Comparison_of_file-sharing_applications "wikipedia:Comparison of file-sharing applications").

*   **[aMule](/index.php/AMule "AMule")** — Well-known eDonkey/Kad client with a daemon version and GTK, web, and CLI front-ends.

	[http://www.amule.org/](http://www.amule.org/) || [amule](https://www.archlinux.org/packages/?name=amule)

*   **EiskaltDC++** — Direct Connect and ADC client.

	[https://github.com/eiskaltdcpp/eiskaltdcpp](https://github.com/eiskaltdcpp/eiskaltdcpp) || GTK: [eiskaltdcpp-gtk](https://aur.archlinux.org/packages/eiskaltdcpp-gtk/), Qt: [eiskaltdcpp-qt](https://aur.archlinux.org/packages/eiskaltdcpp-qt/)

*   **[gtk-gnutella](https://en.wikipedia.org/wiki/gtk-gnutella "wikipedia:gtk-gnutella")** — GTK server/client for the Gnutella peer-to-peer network.

	[http://gtk-gnutella.sourceforge.net/](http://gtk-gnutella.sourceforge.net/) || [gtk-gnutella](https://aur.archlinux.org/packages/gtk-gnutella/)

*   **KaMule** — KDE graphical front-end for aMule.

	[https://www.linux-apps.com/content/show.php?content=150270](https://www.linux-apps.com/content/show.php?content=150270) || [kamule](https://aur.archlinux.org/packages/kamule/)

*   **LBRY** — Browser and wallet for LBRY, the decentralized, user-controlled content marketplace. Based on the [Electron](https://electronjs.org/) platform.

	[https://lbry.io/](https://lbry.io/) || [lbry-app-bin](https://aur.archlinux.org/packages/lbry-app-bin/)

*   **[MLDonkey](https://en.wikipedia.org/wiki/MLDonkey "wikipedia:MLDonkey")** — Multi-protocol P2P client that supports HTTP, FTP, BitTorrent, Direct Connect, eDonkey and FastTrack.

	[http://mldonkey.sourceforge.net/](http://mldonkey.sourceforge.net/) || [mldonkey](https://www.archlinux.org/packages/?name=mldonkey)

*   **ncdc** — Modern and lightweight Direct Connect and ADC client with a friendly ncurses interface.

	[https://dev.yorhel.nl/ncdc](https://dev.yorhel.nl/ncdc) || [ncdc](https://aur.archlinux.org/packages/ncdc/)

*   **Nicotine+** — A graphical client for the Soulseek P2P network.

	[https://www.nicotine-plus.org/](https://www.nicotine-plus.org/) || [nicotine+](https://www.archlinux.org/packages/?name=nicotine%2B)

*   **Valknut** — Direct Connect client (like DC++) with segmented downloading.

	[http://wxdcgui.sourceforge.net/](http://wxdcgui.sourceforge.net/) || [valknut](https://aur.archlinux.org/packages/valknut/)

#### Pastebin clients

See also [Wikipedia:Pastebin](https://en.wikipedia.org/wiki/Pastebin "wikipedia:Pastebin").

Pastebin services are often used to quote text or images while collaborating and troubleshooting. Pastebin clients provide a convenient way to post from the command line.

**Tip:** You can access the [ix.io](http://ix.io/) pastebin using curl. For example pipe the output of a command to ix.io: `*command* | curl -F 'f:1=<-' ix.io ` or upload a file: `curl -F 'f:1=<-' ix.io < *file*` 

**Note:** [pastebin.com](http://pastebin.com/) is blocked for some people and has a history of annoying issues (javascript, adverts, poor formatting, etc). Do *not* use it.

*   **Elmer** — Pastebin client similar to wgetpaste and curlpaste, except written in Perl and usable with wget or curl. Servers: [codepad.org](http://codepad.org/), [rafb.me](http://rafb.me/), [sprunge.us](http://sprunge.us/).

	[https://github.com/sudokode/elmer](https://github.com/sudokode/elmer) || [elmer](https://aur.archlinux.org/packages/elmer/)

*   **Fb-client** — Client for the [paste.xinu.at](http://paste.xinu.at/) pastebin.

	[http://paste.xinu.at](http://paste.xinu.at) || [fb-client](https://www.archlinux.org/packages/?name=fb-client)

*   **Gist** — Command-line interface for the [gist.github.com](https://gist.github.com/) pastebin service.

	[https://github.com/defunkt/gist](https://github.com/defunkt/gist) || [gist](https://www.archlinux.org/packages/?name=gist)

*   **imgur** — A CLI client which can upload image to [imgur.com](https://imgur.com) image sharing service.

	[https://github.com/tremby/imgur.sh](https://github.com/tremby/imgur.sh) || [imgur.sh](https://aur.archlinux.org/packages/imgur.sh/)

*   **Ix** — Client for the ix.io pastebin.

	[http://ix.io](http://ix.io) || [ix](https://aur.archlinux.org/packages/ix/)

*   **Pastebinit** — Really small Python script that acts as a Pastebin client. Servers: [pastie.org](http://pastie.org/), [paste.kde.org](https://paste.kde.org/), [paste.debian.net](http://paste.debian.net/), [paste.ubuntu.com](http://paste.ubuntu.com/) and others (for a full list see `pastebinit -l`).

	[https://launchpad.net/pastebinit](https://launchpad.net/pastebinit) || [pastebinit](https://www.archlinux.org/packages/?name=pastebinit)

*   **ruby-haste** — Client for [hastebin.com](http://hastebin.com/).

	[https://github.com/seejohnrun/haste-client](https://github.com/seejohnrun/haste-client) || [ruby-haste](https://aur.archlinux.org/packages/ruby-haste/)

*   **Uppity** — The pastebin client with an attitude.

	[https://github.com/Kiwi/Uppity](https://github.com/Kiwi/Uppity) || [uppity-git](https://aur.archlinux.org/packages/uppity-git/)

*   **Wgetpaste** — Bash script that automates pasting to a number of pastebin services. Servers: [pastebin.ca](http://pastebin.ca/), [codepad.org](http://codepad.org/), [dpaste.com](http://dpaste.com/) and [pastebin.osuosl.org](http://pastebin.osuosl.org/).

	[http://wgetpaste.zlin.dk/](http://wgetpaste.zlin.dk/) || [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste)

### Communication

#### Email clients

See also [Wikipedia:Comparison of email clients](https://en.wikipedia.org/wiki/Comparison_of_email_clients "wikipedia:Comparison of email clients")

##### Console

*   **aerc** — Work in progress asynchronous email client.

	[https://git.sr.ht/~sircmpwn/aerc](https://git.sr.ht/~sircmpwn/aerc) || [aerc-git](https://aur.archlinux.org/packages/aerc-git/)

*   **alot** — An experimental terminal MUA based on [notmuch mail](https://notmuchmail.org/). It is written in python using the [urwid](http://urwid.org/) toolkit.

	[https://github.com/pazz/alot](https://github.com/pazz/alot) || [alot](https://www.archlinux.org/packages/?name=alot)

*   **[Alpine](/index.php/Alpine "Alpine")** — Fast, easy-to-use and Apache-licensed email client based on [Pine](https://en.wikipedia.org/wiki/Pine_(email_client) "wikipedia:Pine (email client)").

	[http://www.washington.edu/alpine/](http://www.washington.edu/alpine/) || [alpine-git](https://aur.archlinux.org/packages/alpine-git/)

*   **[S-nail](/index.php/S-nail "S-nail")** — a mail processing system with a command syntax reminiscent of *ed* with lines replaced by messages. Provides the functionality of [mailx](https://en.wikipedia.org/wiki/mailx "wikipedia:mailx").

	[https://www.sdaoden.eu/code.html#s-mailx](https://www.sdaoden.eu/code.html#s-mailx) || [s-nail](https://www.archlinux.org/packages/?name=s-nail)

*   **mu/mu4e** — Email indexer (mu) and client for emacs (mu4e). Xapian based for fast searches.

	[http://www.djcbsoftware.nl/code/mu/mu4e.html](http://www.djcbsoftware.nl/code/mu/mu4e.html) || [mu](https://aur.archlinux.org/packages/mu/)

*   **[Mutt](/index.php/Mutt "Mutt")** — Small but very powerful text-based mail client.

	[http://www.mutt.org/](http://www.mutt.org/) || [mutt](https://www.archlinux.org/packages/?name=mutt)

*   **[NeoMutt](/index.php/Mutt#NeoMutt "Mutt")** — Command line mail reader (or MUA). It's a fork of Mutt with added features.

	[https://www.neomutt.org/](https://www.neomutt.org/) || [neomutt](https://www.archlinux.org/packages/?name=neomutt)

*   **[nmh](/index.php/Nmh "Nmh")** — A modular mail handling system.

	[http://www.nongnu.org/nmh/](http://www.nongnu.org/nmh/) || [nmh](https://aur.archlinux.org/packages/nmh/)

*   **[notmuch](/index.php/Notmuch "Notmuch")** — A fast mail indexer built on top of *xapian*.

	[https://notmuchmail.org/](https://notmuchmail.org/) || [notmuch](https://www.archlinux.org/packages/?name=notmuch)

*   **[Sup](/index.php/Sup "Sup")** — CLI mail client with very fast searching, tagging, threading and GMail like operation.

	[https://sup-heliotrope.github.io/](https://sup-heliotrope.github.io/) || [sup](https://aur.archlinux.org/packages/sup/)

*   **Wanderlust** — Email client and news reader for Emacs.

	[http://www.gohome.org/wl/](http://www.gohome.org/wl/) || [wanderlust](https://www.archlinux.org/packages/?name=wanderlust)

##### Graphical

*   **Balsa** — Simple and light email client for GNOME.

	[https://pawsa.fedorapeople.org/balsa/](https://pawsa.fedorapeople.org/balsa/) || [balsa](https://www.archlinux.org/packages/?name=balsa)

*   **[Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail")** — Lightweight GTK-based email client and news reader.

	[https://www.claws-mail.org/](https://www.claws-mail.org/) || [claws-mail](https://www.archlinux.org/packages/?name=claws-mail)

*   **ElectronMail** — Unofficial desktop app for several end-to-end encrypted email providers (like ProtonMail, Tutanota). Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/vladimiry/ElectronMail](https://github.com/vladimiry/ElectronMail) || [electronmail-bin](https://aur.archlinux.org/packages/electronmail-bin/)

*   **[Evolution](/index.php/Evolution "Evolution")** — Mature and feature-rich e-mail client that is part of the GNOME project. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution](https://www.archlinux.org/packages/?name=evolution)

*   **Geary** — Simple desktop mail client built in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

	[https://wiki.gnome.org/Apps/Geary](https://wiki.gnome.org/Apps/Geary) || [geary](https://www.archlinux.org/packages/?name=geary)

*   **Gnubiff** — Mail notification program that checks for mail and displays headers when new mail has arrived.

	[http://gnubiff.sourceforge.net/](http://gnubiff.sourceforge.net/) || [gnubiff](https://www.archlinux.org/packages/?name=gnubiff)

*   **Inboxer** — Unofficial, free and open-source Google Inbox desktop app. Based on the [Electron](https://electronjs.org/) platform.

	[https://denysdovhan.com/inboxer/](https://denysdovhan.com/inboxer/) || [inboxer](https://aur.archlinux.org/packages/inboxer/)

*   **[Kmail](https://en.wikipedia.org/wiki/Kmail "wikipedia:Kmail")** — Mature and feature-rich email client. Part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/internet/kmail/](https://www.kde.org/applications/internet/kmail/) || [kmail](https://www.archlinux.org/packages/?name=kmail)

*   **Kube** — Modern communication and collaboration client built with QtQuick.

	[https://kube.kde.org/](https://kube.kde.org/) || [kube](https://www.archlinux.org/packages/?name=kube)

*   **Mailnag** — Extensible mail notification daemon.

	[https://github.com/pulb/mailnag](https://github.com/pulb/mailnag) || [mailnag](https://www.archlinux.org/packages/?name=mailnag)

*   **Mailspring** — [Proprietary](https://github.com/Foundry376/Mailspring/issues/24) fork of Nylas Mail by one of the original authors.

	[https://getmailspring.com/](https://getmailspring.com/) || [mailspring](https://aur.archlinux.org/packages/mailspring/)

*   **Nylas Mail** — Extensible desktop mail app. Based on the [Electron](https://electronjs.org/) platform.

	[https://www.nylas.com/nylas-mail/](https://www.nylas.com/nylas-mail/) || [nylas-mail-lives-bin](https://aur.archlinux.org/packages/nylas-mail-lives-bin/)

*   **openWMail** — The missing desktop client for Gmail & Google Inbox. Based on the [Electron](https://electronjs.org/) platform.

	[https://openwmail.github.io/](https://openwmail.github.io/) || [openwmail](https://aur.archlinux.org/packages/openwmail/)

*   **QGmailNotifier** — Portable Qt5 based GMail notifier.

	[https://github.com/eteran/qgmailnotifier](https://github.com/eteran/qgmailnotifier) || [qgmailnotifier](https://aur.archlinux.org/packages/qgmailnotifier/)

*   **Protonmail Desktop** — Unofficial app that emulates a native client for the ProtonMail e-mail service. Based on the [Electron](https://electronjs.org/) platform.

	[http://protondesktop.com/](http://protondesktop.com/) || [protonmail-desktop](https://aur.archlinux.org/packages/protonmail-desktop/)

*   **[SeaMonkey Mail & Newsgroups](https://en.wikipedia.org/wiki/SeaMonkey#Mail "wikipedia:SeaMonkey")** — Email client included in the SeaMonkey suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

*   **[Sylpheed](https://en.wikipedia.org/wiki/Sylpheed "wikipedia:Sylpheed")** — Lightweight and user-friendly GTK email client.

	[https://sylpheed.sraoss.jp/en/](https://sylpheed.sraoss.jp/en/) || [sylpheed](https://www.archlinux.org/packages/?name=sylpheed)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Feature-rich email client from Mozilla written in GTK.

	[https://www.thunderbird.net/](https://www.thunderbird.net/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Trojitá** — Qt IMAP email client. Only supports [one IMAP account](https://bugs.kde.org/show_bug.cgi?id=321374).

	[http://trojita.flaska.net/](http://trojita.flaska.net/) || [trojita](https://www.archlinux.org/packages/?name=trojita)

##### Web-based

*   **[Mailpile](https://en.wikipedia.org/wiki/Mailpile "wikipedia:Mailpile")** — A modern, fast web-mail client with user-friendly encryption and privacy features.

	[https://www.mailpile.is/](https://www.mailpile.is/) || [mailpile](https://aur.archlinux.org/packages/mailpile/)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") Mail** — An email webapp for NextCloud.

	[https://github.com/nextcloud/mail](https://github.com/nextcloud/mail) || [nextcloud-app-mail](https://www.archlinux.org/packages/?name=nextcloud-app-mail)

*   **Roundcubemail** — Browser-based multilingual IMAP client webapp with a native application-like user interface.

	[https://roundcube.net/](https://roundcube.net/) || [roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail)

*   **[SquirrelMail](/index.php/Squirrelmail "Squirrelmail")** — Webmail for Nuts!

	[https://squirrelmail.org/](https://squirrelmail.org/) || [squirrelmail](https://aur.archlinux.org/packages/squirrelmail/)

#### Mail servers

See [Mail server](/index.php/Mail_server "Mail server").

*   **Modoboa** — A modular mail hosting and management platform, written in Python.

	[https://modoboa.org/](https://modoboa.org/) || [modoboa](https://aur.archlinux.org/packages/modoboa/)

#### Mail retrieval agents

See also [Wikipedia:Mail retrieval agent](https://en.wikipedia.org/wiki/Mail_retrieval_agent "wikipedia:Mail retrieval agent").

*   **[fdm](/index.php/Fdm "Fdm")** — Program to fetch and deliver mail.

	[https://github.com/nicm/fdm](https://github.com/nicm/fdm) || [fdm](https://www.archlinux.org/packages/?name=fdm)

*   **[Fetchmail](https://en.wikipedia.org/wiki/Fetchmail "wikipedia:Fetchmail")** — A remote-mail retrieval utility.

	[https://www.fetchmail.info/](https://www.fetchmail.info/) || [fetchmail](https://aur.archlinux.org/packages/fetchmail/)

*   **[getmail](/index.php/Getmail "Getmail")** — A POP3/IMAP4 mail retriever with reliable Maildir and command delivery.

	[http://pyropus.ca/software/getmail/](http://pyropus.ca/software/getmail/) || [getmail](https://www.archlinux.org/packages/?name=getmail)

*   **imapsync** — IMAP synchronisation, sync, copy or migration tool

	[http://imapsync.lamiral.info/](http://imapsync.lamiral.info/) || [imapsync](https://aur.archlinux.org/packages/imapsync/)

*   **[isync](/index.php/Isync "Isync")** — IMAP and MailDir mailbox synchronizer

	[http://isync.sourceforge.net/](http://isync.sourceforge.net/) || [isync](https://www.archlinux.org/packages/?name=isync)

*   **mpop** — A small, fast POP3 client suitable as a fetchmail replacement

	[https://marlam.de/mpop/](https://marlam.de/mpop/) || [mpop](https://www.archlinux.org/packages/?name=mpop)

*   **[OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP")** — Synchronizes emails between two repositories.

	[http://www.offlineimap.org/](http://www.offlineimap.org/) || [offlineimap](https://www.archlinux.org/packages/?name=offlineimap)

#### Instant messaging clients

See also [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients") and [Wikipedia:Comparison of VoIP software](https://en.wikipedia.org/wiki/Comparison_of_VoIP_software "wikipedia:Comparison of VoIP software").

This section lists all client software with [instant messaging](https://en.wikipedia.org/wiki/Instant_messaging "wikipedia:Instant messaging") support.

##### Multi-protocol clients

**Note:** All messengers, that support several networks by means of direct connections to them, belong to this section.

The number of networks supported by these clients is very large but they (like any multi-protocol clients) usually have very limited or no support for network-specific features.

###### Console

*   **BarnOwl** — Ncurses-based chat client with support for the Zephyr, XMPP, IRC and Twitter protocols.

	[https://barnowl.mit.edu/](https://barnowl.mit.edu/) || [barnowl](https://aur.archlinux.org/packages/barnowl/)

*   **[BitlBee](/index.php/Bitlbee "Bitlbee")** — IRC gateway to popular chat networks (XMPP, ICQ and Twitter).

	[https://bitlbee.org/](https://bitlbee.org/) || [bitlbee](https://www.archlinux.org/packages/?name=bitlbee)

*   **[CenterIM](https://en.wikipedia.org/wiki/Centericq "wikipedia:Centericq")** — Text mode menu- and window-driven IM interface. Supports most of widely used IM protocols, including ICQ, IRC, XMPP.

	[http://centerim.org/](http://centerim.org/) || [centerim](https://aur.archlinux.org/packages/centerim/)

*   **EKG2** — Ncurses based XMPP, Gadu-Gadu, ICQ and IRC client.

	[http://en.ekg2.org/](http://en.ekg2.org/) || [ekg2](https://aur.archlinux.org/packages/ekg2/)

*   **Finch** — Ncurses-based chat client that uses libpurple and supports all its protocols (Bonjour, Gadu-Gadu, Groupwise, ICQ, IRC, SIMPLE, XMPP, Zephyr).

	[https://developer.pidgin.im/wiki/Using%20Finch](https://developer.pidgin.im/wiki/Using%20Finch) || [finch](https://www.archlinux.org/packages/?name=finch)

*   **Minbif** — IRC gateway to IM networks that uses libpurple.

	[https://symlink.me/projects/minbif/wiki](https://symlink.me/projects/minbif/wiki) || [minbif](https://www.archlinux.org/packages/?name=minbif)

###### Graphical

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) framework.

	[https://wiki.gnome.org/Apps/Empathy](https://wiki.gnome.org/Apps/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **Franz** — [Electron](https://en.wikipedia.org/wiki/Electron_(software_framework) application. Supports Discord, Facebook Messenger, Google Hangouts, Skype, Slack, Telegram, WhatsApp, Zulip and many more.

	[https://meetfranz.com/](https://meetfranz.com/) || [franz](https://aur.archlinux.org/packages/franz/)

*   **[Jitsi](https://en.wikipedia.org/wiki/Jitsi "wikipedia:Jitsi")** — Audio/video VoIP phone and instant messenger written in Java that supports protocols such as SIP, XMPP, ICQ, IRC and many other useful features.

	[https://jitsi.org/](https://jitsi.org/) || [jitsi](https://aur.archlinux.org/packages/jitsi/)

*   **[Kopete](https://en.wikipedia.org/wiki/Kopete "wikipedia:Kopete")** — User-friendly IM supporting Bonjour, Gadu-Gadu, GroupWise, ICQ, XMPP.

	[https://userbase.kde.org/Kopete](https://userbase.kde.org/Kopete) || [kopete](https://www.archlinux.org/packages/?name=kopete)

*   **[KDE Telepathy](/index.php/KDE#KDE_Telepathy "KDE")** — KDE instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) framework. Meant as a replacement for Kopete.

	[https://userbase.kde.org/Telepathy](https://userbase.kde.org/Telepathy) || [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta)

*   **[Pidgin](/index.php/Pidgin "Pidgin")** — Multi-protocol instant messaging client with audio support that uses libpurple and supports all its protocols (Bonjour, Gadu-Gadu, Groupwise, ICQ, IRC, SIMPLE, XMPP, Zephyr).

	[http://pidgin.im/](http://pidgin.im/) || [pidgin](https://www.archlinux.org/packages/?name=pidgin)

*   **qutIM** — Simple and user-friendly IM supporting ICQ, XMPP, Mail.Ru, IRC and VKontakte messaging.

	[http://qutim.org/](http://qutim.org/) || [qutim](https://aur.archlinux.org/packages/qutim/)

*   **[Smuxi](https://en.wikipedia.org/wiki/Smuxi "wikipedia:Smuxi")** — Cross-platform IRC client that also supports Twitter and XMPP.

	[https://smuxi.im/](https://smuxi.im/) || [smuxi](https://aur.archlinux.org/packages/smuxi/)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Feature-rich email client supports instant messaging and chat using IRC, XMPP and Twitter.

	[https://www.thunderbird.net/](https://www.thunderbird.net/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Volt** — Proprietary native desktop client for Skype, Telegram, Slack, XMPP, Discord, IRC and more.

	[https://volt-app.com/](https://volt-app.com/) || [volt](https://aur.archlinux.org/packages/volt/)

##### IRC clients

See also [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients").

###### Console

*   **[BitchX](https://en.wikipedia.org/wiki/BitchX "wikipedia:BitchX")** — Console-based IRC client developed from the popular [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[http://www.bitchx.org/](http://www.bitchx.org/) || [bitchx-git](https://aur.archlinux.org/packages/bitchx-git/)

*   **ERC** — Powerful, modular and extensible IRC client for [Emacs](/index.php/Emacs "Emacs").

	[https://savannah.gnu.org/projects/erc/](https://savannah.gnu.org/projects/erc/) || included with [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)")** — Featherweight IRC client, literally `tail -f` the conversation and `echo` back your replies to a file.

	[https://tools.suckless.org/ii/](https://tools.suckless.org/ii/) || [ii](https://aur.archlinux.org/packages/ii/)

*   **[Irssi](/index.php/Irssi "Irssi")** — Highly-configurable ncurses-based IRC client.

	[https://irssi.org/](https://irssi.org/) || [irssi](https://www.archlinux.org/packages/?name=irssi)

*   **pork** — Programmable, ncurses-based IRC client that mostly looks and feels like ircII.

	[http://dev.ojnk.net/](http://dev.ojnk.net/) || [pork](https://www.archlinux.org/packages/?name=pork)

*   **ScrollZ** — Advanced IRC client based on [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[https://www.scrollz.info/](https://www.scrollz.info/) || [scrollz](https://aur.archlinux.org/packages/scrollz/)

*   **sic** — Extremely simple IRC client, similar to [ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)").

	[https://tools.suckless.org/sic/](https://tools.suckless.org/sic/) || [sic](https://aur.archlinux.org/packages/sic/)

*   **[WeeChat](/index.php/WeeChat "WeeChat")** — Modular, lightweight ncurses-based IRC client.

	[https://weechat.org/](https://weechat.org/) || [weechat](https://www.archlinux.org/packages/?name=weechat)

*   **tiny** — an IRC client written in Rust with a clutter-free interface

	[https://github.com/osa1/tiny](https://github.com/osa1/tiny) || [tiny-irc-client-git](https://aur.archlinux.org/packages/tiny-irc-client-git/)

**Comparison**

| Name | Package | Written in | Extensible | [SASL](https://en.wikipedia.org/wiki/Simple_Authentication_and_Security_Layer "wikipedia:Simple Authentication and Security Layer") |
| [BitchX](https://en.wikipedia.org/wiki/BitchX "wikipedia:BitchX") | [bitchx-git](https://aur.archlinux.org/packages/bitchx-git/) | C | ? | ? |
| [ERC](https://savannah.gnu.org/projects/erc/) | [emacs](https://www.archlinux.org/packages/?name=emacs) | ELisp | in ELisp | [via script](https://www.emacswiki.org/emacs/ErcSASL) |
| [ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) | [ii](https://aur.archlinux.org/packages/ii/) | C | stdin/stdout | No |
| [Irssi](/index.php/Irssi "Irssi") | [irssi](https://www.archlinux.org/packages/?name=irssi) | C | in Perl | Yes |
| [pork](http://dev.ojnk.net/) | [pork](https://www.archlinux.org/packages/?name=pork) | C | in Perl | No |
| [ScrollZ](https://www.scrollz.info/) | [scrollz](https://aur.archlinux.org/packages/scrollz/) | C | ? | No |
| [sic](https://tools.suckless.org/sic/) | [sic](https://aur.archlinux.org/packages/sic/) | C | stdin/stdout | No |
| [WeeChat](/index.php/WeeChat "WeeChat") | [weechat](https://www.archlinux.org/packages/?name=weechat) | C | [multiple languages](https://weechat.org/files/doc/stable/weechat_scripting.en.html) | Yes |
| [tiny](https://github.com/osa1/tiny) | [tiny-irc-client-git](https://aur.archlinux.org/packages/tiny-irc-client-git/) | Rust | No | Yes |

###### Graphical

*   **HexChat** — Fork of XChat for Linux and Windows.

	[https://hexchat.github.io/](https://hexchat.github.io/) || [hexchat](https://www.archlinux.org/packages/?name=hexchat)

*   **[Konversation](https://en.wikipedia.org/wiki/Konversation "wikipedia:Konversation")** — Qt-based IRC client for the KDE desktop.

	[https://konversation.kde.org/](https://konversation.kde.org/) || [konversation](https://www.archlinux.org/packages/?name=konversation)

*   **[KVIrc](https://en.wikipedia.org/wiki/KVIrc "wikipedia:KVIrc")** — Qt-based IRC client featuring extensive themes support.

	[http://kvirc.net/](http://kvirc.net/) || [kvirc-git](https://aur.archlinux.org/packages/kvirc-git/)

*   **Loqui** — GTK IRC client.

	[https://launchpad.net/loqui](https://launchpad.net/loqui) || [loqui](https://aur.archlinux.org/packages/loqui/)

*   **LostIRC** — Simple GTK IRC client with tab-autocompletion, multiple server support, logging and others.

	[http://lostirc.sourceforge.net](http://lostirc.sourceforge.net) || [lostirc](https://aur.archlinux.org/packages/lostirc/)

*   **Polari** — Simple IRC client by the GNOME project.

	[https://wiki.gnome.org/Apps/Polari](https://wiki.gnome.org/Apps/Polari) || [polari](https://www.archlinux.org/packages/?name=polari)

*   **[Quassel](/index.php/Quassel "Quassel")** — Modern, cross-platform, distributed IRC client.

	[https://quassel-irc.org/](https://quassel-irc.org/) || [quassel-monolithic](https://www.archlinux.org/packages/?name=quassel-monolithic)

*   **Srain** — Modern, beautiful IRC client written in GTK 3.

	[https://srain.im/](https://srain.im/) || [srain](https://aur.archlinux.org/packages/srain/)

##### XMPP clients

See also [Wikipedia:XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP") and [Wikipedia:Comparison of instant messaging clients#XMPP-related features](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients#XMPP-related_features "wikipedia:Comparison of instant messaging clients").

###### Console

*   **Freetalk** — Console-based XMPP client.

	[https://www.gnu.org/software/freetalk/](https://www.gnu.org/software/freetalk/) || [freetalk](https://aur.archlinux.org/packages/freetalk/)

*   **jabber.el** — Minimal XMPP client for [Emacs](/index.php/Emacs "Emacs").

	[http://emacs-jabber.sourceforge.net/](http://emacs-jabber.sourceforge.net/) || [emacs-jabber](https://aur.archlinux.org/packages/emacs-jabber/)

*   **jp (Salut à Toi)** — CLI frontend for Salut à Toi, multi-purpose XMPP client

	[https://salut-a-toi.org/](https://salut-a-toi.org/) || [sat-jp](https://aur.archlinux.org/packages/sat-jp/)

*   **[MCabber](https://en.wikipedia.org/wiki/MCabber "wikipedia:MCabber")** — Small XMPP console client, includes features: SSL, PGP, MUC, OTR and UTF8.

	[https://mcabber.com/](https://mcabber.com/) || [mcabber](https://www.archlinux.org/packages/?name=mcabber)

*   **Poezio** — XMPP client with IRC feeling

	[https://poez.io/](https://poez.io/) || [poezio](https://aur.archlinux.org/packages/poezio/)

*   **Primitivus (Salut à Toi)** — Console frontend for Salut à Toi, multi-purpose XMPP client

	[https://salut-a-toi.org/](https://salut-a-toi.org/) || [sat-primitivus](https://aur.archlinux.org/packages/sat-primitivus/)

*   **Profanity** — A console based XMPP client inspired by Irssi.

	[http://profanity.im/](http://profanity.im/) || [profanity](https://www.archlinux.org/packages/?name=profanity)

*   **xmpp-client** — A minimalist XMPP client with OTR support.

	[https://github.com/agl/xmpp-client](https://github.com/agl/xmpp-client) || [go-xmpp-client](https://aur.archlinux.org/packages/go-xmpp-client/)

###### Graphical

*   **Cagou (Salut à Toi)** — Desktop/mobiles frontend for Salut à Toi, multi-purpose XMPP client

	[https://salut-a-toi.org/](https://salut-a-toi.org/) || [sat-cagou-hg](https://aur.archlinux.org/packages/sat-cagou-hg/)

*   **Converse.js** — Web-based XMPP chat client written in JavaScript.

	[https://conversejs.org/](https://conversejs.org/) || [conversejs-git](https://aur.archlinux.org/packages/conversejs-git/)

*   **Dino** — A modern, easy to use XMPP client, with PGP and OMEMO support.

	[https://dino.im/](https://dino.im/) || [dino-git](https://aur.archlinux.org/packages/dino-git/)

*   **[Gajim](/index.php/Gajim "Gajim")** — XMPP client with audio support written in Python using GTK.

	[https://gajim.org/](https://gajim.org/) || [gajim](https://www.archlinux.org/packages/?name=gajim)

*   **[Kadu](https://en.wikipedia.org/wiki/Kadu_(software) "wikipedia:Kadu (software)")** — Qt-based XMPP and Gadu-Gadu client.

	[http://www.kadu.im/](http://www.kadu.im/) || [kadu](https://aur.archlinux.org/packages/kadu/)

*   **Libervia (Salut à Toi)** — Web frontend for Salut à Toi, multi-purpose XMPP client

	[https://salut-a-toi.org/](https://salut-a-toi.org/) || [sat-libervia-hg](https://aur.archlinux.org/packages/sat-libervia-hg/)

*   **Nextcloud JavaScript XMPP Client** — Chat app for Nextcloud with XMPP, end-to-end encryption, video calls, file transfer & group chat.

	[https://github.com/nextcloud/jsxc.nextcloud](https://github.com/nextcloud/jsxc.nextcloud) || [nextcloud-app-jsxc](https://aur.archlinux.org/packages/nextcloud-app-jsxc/)

*   **[Psi](https://en.wikipedia.org/wiki/Psi_(instant_messaging_client) "wikipedia:Psi (instant messaging client)")** — Qt-based XMPP client.

	[https://psi-im.org/](https://psi-im.org/) || [psi](https://www.archlinux.org/packages/?name=psi) or [psi-nowebengine](https://www.archlinux.org/packages/?name=psi-nowebengine)

*   **[Spark](https://en.wikipedia.org/wiki/Spark_(XMPP_client) "wikipedia:Spark (XMPP client)")** — Cross-platform real-time XMPP collaboration client optimized for business and organizations.

	[https://www.igniterealtime.org/projects/spark/](https://www.igniterealtime.org/projects/spark/) || [spark](https://aur.archlinux.org/packages/spark/)

*   **Swift** — XMPP client written in C++ with Qt and Swiften.

	[https://swift.im/](https://swift.im/) || [swift-im](https://aur.archlinux.org/packages/swift-im/)

*   **[Tkabber](https://en.wikipedia.org/wiki/Tkabber "wikipedia:Tkabber")** — Easy to hack feature-rich XMPP client by the author of the ejabberd XMPP server.

	[http://tkabber.jabber.ru/](http://tkabber.jabber.ru/) || [tkabber](https://aur.archlinux.org/packages/tkabber/)

*   **Vacuum IM** — Full-featured crossplatform XMPP client.

	[https://github.com/Vacuum-IM/vacuum-im](https://github.com/Vacuum-IM/vacuum-im) || [vacuum-im](https://aur.archlinux.org/packages/vacuum-im/)

##### SIP clients

See also [Wikipedia:List of SIP software#Clients](https://en.wikipedia.org/wiki/List_of_SIP_software#Clients "wikipedia:List of SIP software").

*   **[Banji](/index.php/Jami "Jami")** — SIP-compatible softphone and instant messenger for the decentralized Jami network. KDE client, formerly known as Ring KDE.

	[https://kde.org/applications/internet/org.kde.ring-kde](https://kde.org/applications/internet/org.kde.ring-kde) || [ring-kde](https://aur.archlinux.org/packages/ring-kde/)

*   **[Blink](https://en.wikipedia.org/wiki/Blink_(SIP_client) "wikipedia:Blink (SIP client)")** — State of the art, easy to use SIP client.

	[http://icanblink.com/](http://icanblink.com/) || [blink](https://aur.archlinux.org/packages/blink/)

*   **[Ekiga](https://en.wikipedia.org/wiki/Ekiga "wikipedia:Ekiga")** — VoIP and video conferencing application with full SIP and H.323 support (formerly known as GNOME Meeting).

	[https://www.ekiga.org/](https://www.ekiga.org/) || [ekiga](https://www.archlinux.org/packages/?name=ekiga)

*   **[Jami](/index.php/Jami "Jami")** — SIP-compatible softphone and instant messenger for the decentralized Jami network. Formerly known as Ring and SFLphone.

	[https://jami.net/](https://jami.net/) || [jami-gnome](https://www.archlinux.org/packages/?name=jami-gnome)

*   **[Linphone](https://en.wikipedia.org/wiki/Linphone "wikipedia:Linphone")** — VoIP phone application (SIP client) for communicating freely with people over the internet, with voice, video, and text instant messaging.

	[http://www.linphone.org/](http://www.linphone.org/) || [linphone](https://aur.archlinux.org/packages/linphone/)

*   **[Twinkle](https://en.wikipedia.org/wiki/Twinkle_(software) "wikipedia:Twinkle (software)")** — Qt softphone for VoIP and IM communication using SIP.

	[http://twinkle.dolezel.info/](http://twinkle.dolezel.info/) || [twinkle-qt5](https://aur.archlinux.org/packages/twinkle-qt5/)

##### Matrix clients

See also [Matrix](/index.php/Matrix "Matrix").

*   **Fractal** — Matrix client for GNOME written in Rust.

	[https://wiki.gnome.org/Apps/Fractal](https://wiki.gnome.org/Apps/Fractal) || [fractal](https://www.archlinux.org/packages/?name=fractal)

*   **nheko** — Desktop client for the Matrix protocol.

	[https://github.com/Nheko-Reborn/nheko](https://github.com/Nheko-Reborn/nheko) || [nheko](https://aur.archlinux.org/packages/nheko/), [nheko-git](https://aur.archlinux.org/packages/nheko-git/)

*   **Quaternion** — Qt5-based IM client for the Matrix protocol.

	[https://github.com/QMatrixClient/Quaternion](https://github.com/QMatrixClient/Quaternion) || [quaternion](https://aur.archlinux.org/packages/quaternion/)

*   **Riot** — Glossy Matrix client with an emphasis on performance and usability. Web application and desktop application based on the [Electron](https://electronjs.org/) platform.

	[https://about.riot.im/](https://about.riot.im/) || [riot-web](https://www.archlinux.org/packages/?name=riot-web), [riot-desktop](https://www.archlinux.org/packages/?name=riot-desktop)

*   **Tensor** — Qt5/QML-based Matrix client.

	[https://github.com/davidar/tensor](https://github.com/davidar/tensor) || [tensor-git](https://aur.archlinux.org/packages/tensor-git/)

##### Tox clients

See also [Tox](/index.php/Tox "Tox").

*   **qTox** — Powerful Tox client written in C++/Qt that follows the Tox design guidelines.

	[https://qtox.github.io/](https://qtox.github.io/) || [qtox](https://www.archlinux.org/packages/?name=qtox)

*   **ratox** — FIFO based tox client.

	[https://ratox.2f30.org/](https://ratox.2f30.org/) || [ratox-git](https://aur.archlinux.org/packages/ratox-git/)

*   **Ricin** — Dead-simple but powerful Tox client.

	[https://github.com/RicinApp/Ricin](https://github.com/RicinApp/Ricin) || [ricin](https://aur.archlinux.org/packages/ricin/)

*   **Toxic** — ncurses-based Tox client

	[https://github.com/Jfreegman/toxic](https://github.com/Jfreegman/toxic) || [toxic](https://www.archlinux.org/packages/?name=toxic)

*   **Toxygen** — Tox client written in pure Python3.

	[https://github.com/toxygen-project/toxygen](https://github.com/toxygen-project/toxygen) || [toxygen-git](https://aur.archlinux.org/packages/toxygen-git/)

*   **Venom** — a modern Tox client for the GNU/Linux desktop

	[https://github.com/naxuroqa/Venom](https://github.com/naxuroqa/Venom) || [venom](https://aur.archlinux.org/packages/venom/)

*   **µTox** — Lightweight Tox client.

	[https://utox.io/](https://utox.io/) || [utox](https://www.archlinux.org/packages/?name=utox)

##### Serverless (decentralized) clients

See also [Bonjour](/index.php/Avahi#Link-Local_(Bonjour/Zeroconf)_chat "Avahi"), [Ring](/index.php/Ring "Ring"), [Tox](/index.php/Tox "Tox") and [Wikipedia:Comparison of LAN messengers](https://en.wikipedia.org/wiki/Comparison_of_LAN_messengers "wikipedia:Comparison of LAN messengers").

*   **BeeBEEP** — Secure LAN Messenger.

	[http://beebeep.sourceforge.net/](http://beebeep.sourceforge.net/) || [beebeep](https://aur.archlinux.org/packages/beebeep/)

*   **Bit Chat** — Secure, peer-to-peer instant messenger.

	[https://bitchat.im/](https://bitchat.im/) || [bitchat](https://aur.archlinux.org/packages/bitchat/)

*   **[Bitmessage](/index.php/Bitmessage "Bitmessage")** — Decentralized and trustless P2P communications protocol for sending encrypted messages to another person or to many subscribers.

	[https://bitmessage.org/](https://bitmessage.org/) || [pybitmessage](https://aur.archlinux.org/packages/pybitmessage/)

*   **iptux** — LAN communication software, compatible with IP Messenger.

	[https://github.com/iptux-src/iptux](https://github.com/iptux-src/iptux) || [iptux](https://aur.archlinux.org/packages/iptux/)

*   **LAN Messenger** — P2P chat application for intranet communication and does not require a server. A variety of handy features are supported including notifications, personal and group messaging with encryption, file transfer and message logging.

	[https://lanmessenger.github.io/](https://lanmessenger.github.io/) || [lmc](https://aur.archlinux.org/packages/lmc/)

*   **Patchwork** — Decentralized messaging and sharing app built on top of Secure Scuttlebutt (SSB). Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/ssbc/patchwork](https://github.com/ssbc/patchwork) || [ssb-patchwork](https://aur.archlinux.org/packages/ssb-patchwork/)

*   **[RetroShare](/index.php/RetroShare "RetroShare")** — Serverless encrypted instant messenger with filesharing, chatgroups, mail.

	[http://retroshare.net/](http://retroshare.net/) || [retroshare](https://aur.archlinux.org/packages/retroshare/)

*   **[Ricochet](https://en.wikipedia.org/wiki/Ricochet_(software) "wikipedia:Ricochet (software)")** — Anonymous peer-to-peer instant messaging system built on [Tor](/index.php/Tor "Tor") hidden services.

	[https://ricochet.im/](https://ricochet.im/) || [ricochet](https://aur.archlinux.org/packages/ricochet/)

##### Other IM clients

*   **Caprine** — Unofficial Facebook Messenger app. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/sindresorhus/caprine](https://github.com/sindresorhus/caprine) || [caprine](https://www.archlinux.org/packages/?name=caprine)

*   **[Discord](/index.php/Discord "Discord")** — Proprietary all-in-one voice and text chat application for gamers that’s free and works on both your desktop and phone.

	[https://discordapp.com/](https://discordapp.com/) || [discord](https://www.archlinux.org/packages/?name=discord)

*   **Esmska** — Program for sending SMS over the Internet.

	[https://github.com/kparal/esmska](https://github.com/kparal/esmska) || [esmska](https://www.archlinux.org/packages/?name=esmska)

*   **[Gitter](https://en.wikipedia.org/wiki/Gitter "wikipedia:Gitter")** — Communication product for communities and teams on GitHub.

	[https://gitter.im/](https://gitter.im/) || [gitter](https://aur.archlinux.org/packages/gitter/)

*   **Hangups** — Third-party instant messaging client for Google Hangouts.

	[https://github.com/tdryer/hangups](https://github.com/tdryer/hangups) || [hangups](https://aur.archlinux.org/packages/hangups/)

*   **[ICQ](/index.php/ICQ "ICQ")** — Official ICQ client for Linux.

	[https://icq.com/linux/](https://icq.com/linux/) || [icqdesktop-bin](https://aur.archlinux.org/packages/icqdesktop-bin/)

*   **Licq** — Instant messaging client for UNIX supporting ICQ.

	[http://licq.org/](http://licq.org/) || [licq](https://www.archlinux.org/packages/?name=licq)

*   **Matterhorn** — Console client for the Mattermost chat system.

	[https://github.com/matterhorn-chat/matterhorn](https://github.com/matterhorn-chat/matterhorn) || [matterhorn](https://aur.archlinux.org/packages/matterhorn/)

*   **[Mattermost](/index.php/Mattermost "Mattermost") Desktop** — Desktop application for Mattermost. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/mattermost/desktop](https://github.com/mattermost/desktop) || [mattermost-desktop](https://aur.archlinux.org/packages/mattermost-desktop/)

*   **[Mumble](/index.php/Mumble "Mumble")** — Voice chat application similar to TeamSpeak.

	[https://www.mumble.info/](https://www.mumble.info/) || [mumble](https://www.archlinux.org/packages/?name=mumble)

*   **QHangups** — Alternative client for Google Hangouts written in PyQt.

	[https://github.com/xmikos/qhangups](https://github.com/xmikos/qhangups) || [qhangups](https://aur.archlinux.org/packages/qhangups/)

*   **Rocket.Chat Desktop** — Desktop application for Rocket.Chat. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/RocketChat/Rocket.Chat.Electron](https://github.com/RocketChat/Rocket.Chat.Electron) || [rocketchat-desktop](https://aur.archlinux.org/packages/rocketchat-desktop/)

*   **[Signal](https://en.wikipedia.org/wiki/Signal_(software) "wikipedia:Signal (software)")** — Signal Private Messenger for the Desktop. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/signalapp/Signal-Desktop](https://github.com/signalapp/Signal-Desktop) || [signal](https://aur.archlinux.org/packages/signal/)

*   **[Skype](https://en.wikipedia.org/wiki/Skype "wikipedia:Skype")** — Popular but proprietary application for voice and video communication. Based on the [Electron](https://electronjs.org/) platform.

	[https://www.skype.com/](https://www.skype.com/) || [skypeforlinux-stable-bin](https://aur.archlinux.org/packages/skypeforlinux-stable-bin/)

*   **[Slack](https://en.wikipedia.org/wiki/Slack_(software) "wikipedia:Slack (software)")** — Proprietary Slack client for desktop. Based on the [Electron](https://electronjs.org/) platform.

	[https://slack.com/downloads/linux](https://slack.com/downloads/linux) || [slack-desktop](https://aur.archlinux.org/packages/slack-desktop/)

*   **[TeamSpeak](/index.php/TeamSpeak "TeamSpeak")** — Proprietary VoIP application with gamers as its target audience.

	[https://www.teamspeak.com/](https://www.teamspeak.com/) || [teamspeak3](https://www.archlinux.org/packages/?name=teamspeak3)

*   **[TeamTalk](/index.php/TeamTalk "TeamTalk")** — Proprietary VoIP application with video chat, file and desktop sharing. Desktop sharing doesn't appear to be working in Linux though. AUR package is server only, but client is built in the make process.

	[https://bearware.dk](https://bearware.dk) || [teamtalk](https://aur.archlinux.org/packages/teamtalk/)

*   **[Telegram](/index.php/Telegram "Telegram") Desktop** — Official Telegram desktop client.

	[https://desktop.telegram.org/](https://desktop.telegram.org/) || [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop)

*   **[Viber](https://en.wikipedia.org/wiki/Viber "wikipedia:Viber")** — Proprietary cross-platform IM and VoIP software.

	[https://www.viber.com/products/linux/](https://www.viber.com/products/linux/) || [viber](https://aur.archlinux.org/packages/viber/)

*   **[Wire](https://en.wikipedia.org/wiki/Wire_(software) "wikipedia:Wire (software)")** — Modern, private messenger. Based on the [Electron](https://electronjs.org/) platform.

	[https://wire.com/](https://wire.com/) || [wire-desktop](https://www.archlinux.org/packages/?name=wire-desktop)

*   **YakYak** — Unofficial desktop client for Google Hangouts. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/yakyak/yakyak](https://github.com/yakyak/yakyak) || [yakyak](https://aur.archlinux.org/packages/yakyak/)

*   **[Zoom](https://en.wikipedia.org/wiki/Zoom_Video_Communications "wikipedia:Zoom Video Communications")** — Proprietary video conferencing, online meetings and group messaging application.

	[https://zoom.us/](https://zoom.us/) || [zoom](https://aur.archlinux.org/packages/zoom/)

*   **[Zulip](https://en.wikipedia.org/wiki/Zulip "wikipedia:Zulip")** — Desktop client for Zulip group chat. Based on the [Electron](https://electronjs.org/) platform.

	[https://zulipchat.com/apps/linux](https://zulipchat.com/apps/linux) || [zulip-electron-bin](https://aur.archlinux.org/packages/zulip-electron-bin/)

#### Instant messaging servers

See also [Wikipedia:Comparison of instant messaging protocols](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_protocols "wikipedia:Comparison of instant messaging protocols").

##### IRC servers

See also [Wikipedia:Comparison of Internet Relay Chat daemons](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_daemons "wikipedia:Comparison of Internet Relay Chat daemons").

*   **[InspIRCd](/index.php/InspIRCd "InspIRCd")** — A stable, modern and lightweight IRC daemon.

	[https://www.inspircd.org/](https://www.inspircd.org/) || [inspircd](https://aur.archlinux.org/packages/inspircd/)

*   **IRCD-Hybrid** — A lightweight, high-performance internet relay chat daemon.

	[http://www.ircd-hybrid.org/](http://www.ircd-hybrid.org/) || [ircd-hybrid](https://aur.archlinux.org/packages/ircd-hybrid/)

*   **miniircd** — A small and configuration free IRC server, suitable for private use.

	[https://github.com/jrosdahl/miniircd](https://github.com/jrosdahl/miniircd) || [miniircd-git](https://aur.archlinux.org/packages/miniircd-git/)

*   **[UnrealIRCd](/index.php/UnrealIRCd "UnrealIRCd")** — Open Source IRC Server.

	[https://www.unrealircd.org/](https://www.unrealircd.org/) || [unrealircd](https://www.archlinux.org/packages/?name=unrealircd)

*   **ngIRCd** — A free, portable and lightweight Internet Relay Chat server for small or private networks.

	[https://ngircd.barton.de/](https://ngircd.barton.de/) || [ngircd](https://www.archlinux.org/packages/?name=ngircd)

##### XMPP servers

See also [Wikipedia:Comparison of XMPP server software](https://en.wikipedia.org/wiki/Comparison_of_XMPP_server_software "wikipedia:Comparison of XMPP server software").

*   **[Prosody](/index.php/Prosody "Prosody")** — An XMPP server written in the [Lua](http://www.lua.org/) programming language. Prosody is designed to be lightweight and highly extensible. It is licensed under a permissive [MIT license](http://prosody.im/source/mit).

	[http://prosody.im/](http://prosody.im/) || [prosody](https://www.archlinux.org/packages/?name=prosody)

*   **Ejabberd** — Robust, scalable and extensible XMPP Server written in Erlang

	[https://www.ejabberd.im/](https://www.ejabberd.im/) || [ejabberd](https://www.archlinux.org/packages/?name=ejabberd)

*   **[Jabberd2](/index.php/Jabberd2 "Jabberd2")** — An XMPP server written in the C language and licensed under the GNU General Public License. It was inspired by jabberd14.

	[https://jabberd2.org/](https://jabberd2.org/) || [jabberd2](https://aur.archlinux.org/packages/jabberd2/)

*   **[Openfire](/index.php/Openfire "Openfire")** — An XMPP IM multiplatform server written in Java

	[http://www.igniterealtime.org/projects/openfire/](http://www.igniterealtime.org/projects/openfire/) || [openfire](https://www.archlinux.org/packages/?name=openfire)

##### SIP servers

See also [Wikipedia:List of SIP software#Servers](https://en.wikipedia.org/wiki/List_of_SIP_software#Servers "wikipedia:List of SIP software").

*   **[Asterisk](/index.php/Asterisk "Asterisk")** — A complete PBX solution.

	[https://www.asterisk.org/](https://www.asterisk.org/) || [asterisk](https://aur.archlinux.org/packages/asterisk/)

*   **Kamailio** — Rock solid SIP server.

	[https://www.kamailio.org/](https://www.kamailio.org/) || [kamailio](https://aur.archlinux.org/packages/kamailio/)

*   **openSIPS** — SIP proxy/server for voice, video, IM, presence and any other SIP extensions.

	[https://opensips.org/](https://opensips.org/) || [opensips](https://www.archlinux.org/packages/?name=opensips)

*   **Repro** — An open-source, free SIP server.

	[https://www.resiprocate.org/About_Repro](https://www.resiprocate.org/About_Repro) || [repro](https://aur.archlinux.org/packages/repro/)

*   **[Yate](https://en.wikipedia.org/wiki/Yate_(telephony_engine) "wikipedia:Yate (telephony engine)")** — Advanced, mature, flexible telephony server that is used for VoIP and fixed networks, and for traditional mobile operators and MVNOs.

	[http://yate.ro/](http://yate.ro/) || [yate](https://www.archlinux.org/packages/?name=yate)

##### Other IM servers

*   **[Mattermost](/index.php/Mattermost "Mattermost")** — Open source private cloud server, Slack-alternative.

	[https://github.com/mattermost/mattermost-server](https://github.com/mattermost/mattermost-server) || [mattermost](https://aur.archlinux.org/packages/mattermost/)

*   **[Murmur](/index.php/Murmur "Murmur")** — The voice chat application server for Mumble.

	[https://www.mumble.info/](https://www.mumble.info/) || [murmur](https://www.archlinux.org/packages/?name=murmur)

*   **Nextcloud Talk** — Video- and audio-conferencing app for Nextcloud.

	[https://github.com/nextcloud/spreed](https://github.com/nextcloud/spreed) || [nextcloud-app-spreed](https://www.archlinux.org/packages/?name=nextcloud-app-spreed)

*   **Rocket.Chat** — Web chat server, developed in JavaScript, using the Meteor fullstack framework.

	[https://github.com/RocketChat/Rocket.Chat](https://github.com/RocketChat/Rocket.Chat) || [rocketchat-server](https://aur.archlinux.org/packages/rocketchat-server/)

*   **Spreed WebRTC** — WebRTC audio/video call and conferencing server.

	[https://github.com/strukturag/spreed-webrtc](https://github.com/strukturag/spreed-webrtc) || [spreed-webrtc-server](https://aur.archlinux.org/packages/spreed-webrtc-server/)

*   **[Synapse](/index.php/Matrix "Matrix")** — Reference homeserver for the Matrix protocol.

	[https://github.com/matrix-org/synapse](https://github.com/matrix-org/synapse) || [matrix-synapse](https://www.archlinux.org/packages/?name=matrix-synapse)

*   **[TeamSpeak](/index.php/TeamSpeak "TeamSpeak") Server** — Proprietary VoIP conference server.

	[https://teamspeak.com/](https://teamspeak.com/) || [teamspeak3-server](https://www.archlinux.org/packages/?name=teamspeak3-server)

*   **uMurmur** — Minimalistic Mumble server.

	[https://umurmur.net/](https://umurmur.net/) || [umurmur](https://www.archlinux.org/packages/?name=umurmur)

#### Collaborative software

See also [Wikipedia:Collaborative software](https://en.wikipedia.org/wiki/Collaborative_software "wikipedia:Collaborative software").

*   **[Citadel/UX](https://en.wikipedia.org/wiki/Citadel/UX "wikipedia:Citadel/UX")** — Includes an email & mailing list server, instant messaging, address books, calendar/scheduling, bulletin boards, and wiki and blog engines.

	[http://www.citadel.org/](http://www.citadel.org/) || [webcit](https://aur.archlinux.org/packages/webcit/)

*   **[Kolab](/index.php/Kolab "Kolab")** — Kolab Groupware solution consisting of a server and various clients.

	[https://kolab.org/](https://kolab.org/) || [kolab](https://aur.archlinux.org/packages/kolab/)

*   **[Open-xchange](/index.php/Open-xchange "Open-xchange")** — A groupware solution providing mail facilities, calendaring, shared contacts and Google-Docs-like text editing

	[http://www.ox.io/](http://www.ox.io/) || [open-xchange](https://aur.archlinux.org/packages/open-xchange/)

*   **[SOGo](/index.php/SOGo "SOGo")** — Groupware server built around OpenGroupware.org (OGo) and the SOPE application server.

	[https://sogo.nu/](https://sogo.nu/) || [sogo](https://aur.archlinux.org/packages/sogo/)

### News, RSS, and blogs

#### News aggregators

[RSS](https://en.wikipedia.org/wiki/RSS aggregators. Some [email clients](#Email_clients) are also able to act as news aggregator: [Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail") RSSyl plugin, [Evolution](/index.php/Evolution "Evolution") RSS plugin, [SeaMonkey Mail & Newsgroups](https://en.wikipedia.org/wiki/SeaMonkey#Mail "wikipedia:SeaMonkey"), [Thunderbird](/index.php/Thunderbird "Thunderbird").

See also [Wikipedia:Comparison of feed aggregators](https://en.wikipedia.org/wiki/Comparison_of_feed_aggregators "wikipedia:Comparison of feed aggregators").

##### Console

*   **[Canto](https://en.wikipedia.org/wiki/Canto_(news_aggregator) "wikipedia:Canto (news aggregator)")** — Ncurses RSS aggregator.

	[https://codezen.org/canto/](https://codezen.org/canto/) || [canto-curses](https://www.archlinux.org/packages/?name=canto-curses)

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

	[http://gnus.org/](http://gnus.org/) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[Newsboat](/index.php/Newsboat "Newsboat")** — Ncurses RSS aggregator with layout and keybinding similar to the [Mutt](/index.php/Mutt "Mutt") email client.

	[https://newsboat.org/](https://newsboat.org/) || [newsboat](https://www.archlinux.org/packages/?name=newsboat)

*   **Rawdog** — "RSS Aggregator Without Delusions Of Grandeur" that parses RSS/CDF/Atom feeds into a static HTML page of articles in chronological order.

	[http://offog.org/code/rawdog/](http://offog.org/code/rawdog/) || [rawdog](https://www.archlinux.org/packages/?name=rawdog)

*   **Snownews** — Text mode RSS news reader.

	[https://github.com/kouya/snownews](https://github.com/kouya/snownews) || [snownews](https://aur.archlinux.org/packages/snownews/)

*   **sfeed** — Lightweight RSS and Atom parser.

	[https://codemadness.org/sfeed-simple-feed-parser.html](https://codemadness.org/sfeed-simple-feed-parser.html) || [sfeed-git](https://aur.archlinux.org/packages/sfeed-git/)

##### Graphical

*   **[Akregator](https://en.wikipedia.org/wiki/Kontact#News_Feed_Aggregator "wikipedia:Kontact")** — News aggregator for KDE, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/internet/akregator/](https://www.kde.org/applications/internet/akregator/) || [akregator](https://www.archlinux.org/packages/?name=akregator)

*   **Alduin** — RSS, Atom and JSON feed aggregator. Based on the [Electron](https://electronjs.org/) platform.

	[https://alduinapp.github.io/](https://alduinapp.github.io/) || [alduin](https://aur.archlinux.org/packages/alduin/)

*   **FeedReader** — Modern desktop application designed to complement existing web-based RSS accounts.

	[https://jangernert.github.io/FeedReader/](https://jangernert.github.io/FeedReader/) || [feedreader](https://www.archlinux.org/packages/?name=feedreader)

*   **[Liferea](https://en.wikipedia.org/wiki/Liferea "wikipedia:Liferea")** — GTK news aggregator for online news feeds and weblogs.

	[https://lzone.de/liferea/](https://lzone.de/liferea/) || [liferea](https://www.archlinux.org/packages/?name=liferea)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") News** — RSS/Atom feed reader for Nextcloud.

	[https://github.com/nextcloud/news](https://github.com/nextcloud/news) || [nextcloud-app-news](https://www.archlinux.org/packages/?name=nextcloud-app-news)

*   **QuiteRSS** — RSS/Atom feed reader written on Qt/С++.

	[http://quiterss.org/](http://quiterss.org/) || [quiterss](https://www.archlinux.org/packages/?name=quiterss)

*   **RSS Guard** — Very tiny RSS and ATOM news reader developed using Qt framework.

	[https://github.com/martinrotter/rssguard](https://github.com/martinrotter/rssguard) || [rssguard](https://www.archlinux.org/packages/?name=rssguard) or [rssguard-nowebengine](https://www.archlinux.org/packages/?name=rssguard-nowebengine)

*   **selfoss** — The new multipurpose RSS reader, live stream, mashup, aggregation web application.

	[https://selfoss.aditu.de/](https://selfoss.aditu.de/) || [selfoss](https://aur.archlinux.org/packages/selfoss/)

*   **Tickr** — GTK-based RSS Reader that displays feeds as a smooth scrolling line on your desktop, as known from TV stations.

	[https://www.open-tickr.net/](https://www.open-tickr.net/) || [tickr](https://aur.archlinux.org/packages/tickr/)

*   **[Tiny Tiny RSS](https://en.wikipedia.org/wiki/Tiny_Tiny_RSS "wikipedia:Tiny Tiny RSS")** — Web-based news feed (RSS/Atom) aggregator.

	[https://tt-rss.org/](https://tt-rss.org/) || [tt-rss](https://www.archlinux.org/packages/?name=tt-rss)

#### Podcast clients

Some media players are also able to act as podcast client: [Amarok](/index.php/Amarok "Amarok"), [Banshee](https://en.wikipedia.org/wiki/Banshee_(media_player) "wikipedia:Banshee (media player)"), Cantata, [Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)"), Goggles Music Manager, [Rhythmbox](https://en.wikipedia.org/wiki/Rhythmbox "wikipedia:Rhythmbox"), [VLC media player](/index.php/VLC_media_player "VLC media player"). [git-annex](https://en.wikipedia.org/wiki/git-annex "wikipedia:git-annex") can also [function as podcatcher](https://git-annex.branchable.com/tips/downloading_podcasts/).

See also [Wikipedia:List of podcatchers](https://en.wikipedia.org/wiki/List_of_podcatchers "wikipedia:List of podcatchers").

##### Console

*   **castget** — Simple, command-line RSS enclosure downloader, primarily intended for automatic, unattended downloading of podcasts.

	[https://castget.johndal.com/](https://castget.johndal.com/) || [castget](https://www.archlinux.org/packages/?name=castget)

*   **gpo** — Text mode interface of gPodder.

	[https://gpodder.github.io/](https://gpodder.github.io/) || [gpodder](https://www.archlinux.org/packages/?name=gpodder)

*   **Greg** — A command-line podcast aggregator.

	[https://github.com/manolomartinez/greg](https://github.com/manolomartinez/greg) || [greg-git](https://aur.archlinux.org/packages/greg-git/)

*   **Marrie** — A simple podcast client that runs on the Command Line Interface.

	[https://github.com/rafaelmartins/marrie/](https://github.com/rafaelmartins/marrie/) || [marrie-git](https://aur.archlinux.org/packages/marrie-git/)

*   **pcd** — A minimal podcast client written in go

	[https://github.com/kvannotten/pcd](https://github.com/kvannotten/pcd) || [pcd](https://aur.archlinux.org/packages/pcd/)

##### Graphical

*   **CPod** — Simple, beautiful podcast app. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/z-------------/cumulonimbus](https://github.com/z-------------/cumulonimbus) || [cpod-bin](https://aur.archlinux.org/packages/cpod-bin/)

*   **GNOME Podcasts** — Podcast client for the GNOME Desktop written in Rust.

	[https://gitlab.gnome.org/World/podcasts](https://gitlab.gnome.org/World/podcasts) || [gnome-podcasts](https://www.archlinux.org/packages/?name=gnome-podcasts)

*   **gPodder** — Podcast client and media aggregator (GTK interface).

	[https://gpodder.github.io/](https://gpodder.github.io/) || [gpodder](https://www.archlinux.org/packages/?name=gpodder)

*   **Vocal** — Simple podcast client for the Modern Desktop (GTK).

	[https://vocalproject.net/](https://vocalproject.net/) || [vocal](https://www.archlinux.org/packages/?name=vocal)

#### Usenet newsreaders

Some [email clients](#Email_clients) are also able to act as Usenet newsreader: [Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail"), [Evolution](/index.php/Evolution "Evolution"), [NeoMutt](/index.php/Mutt#NeoMutt "Mutt"), [SeaMonkey Mail & Newsgroups](https://en.wikipedia.org/wiki/SeaMonkey#Mail "wikipedia:SeaMonkey"), [Sylpheed](https://en.wikipedia.org/wiki/Sylpheed "wikipedia:Sylpheed"), [Thunderbird](/index.php/Thunderbird "Thunderbird").

See also: [Wikipedia:List of Usenet newsreaders](https://en.wikipedia.org/wiki/List_of_Usenet_newsreaders "wikipedia:List of Usenet newsreaders"), [Wikipedia:Comparison of Usenet newsreaders](https://en.wikipedia.org/wiki/Comparison_of_Usenet_newsreaders "wikipedia:Comparison of Usenet newsreaders").

##### Console

*   **[nn](https://en.wikipedia.org/wiki/nn_(newsreader) "wikipedia:nn (newsreader)")** — Alternative more user-friendly (curses-based) Usenet newsreader for UNIX.

	[http://www.nndev.org/](http://www.nndev.org/) || [nn](https://aur.archlinux.org/packages/nn/)

*   **[slrn](https://en.wikipedia.org/wiki/slrn "wikipedia:slrn")** — Text-based news client.

	[http://www.slrn.org/](http://www.slrn.org/) || [slrn](https://aur.archlinux.org/packages/slrn/)

*   **[tin](https://en.wikipedia.org/wiki/Tin_(newsreader) "wikipedia:Tin (newsreader)")** — A cross-platform threaded NNTP and spool based UseNet newsreader.

	[http://tin.org/](http://tin.org/) || [tin](https://aur.archlinux.org/packages/tin/)

*   **trn** — A text-based Threaded Usenet newsreader.

	[http://trn.sourceforge.net/](http://trn.sourceforge.net/) || [trn](https://aur.archlinux.org/packages/trn/)

##### Graphical

*   **LottaNZB** — A *SABnzbd* (Usenet binary downloader) GUI front-end written in PyGTK (Python 2)

	[https://launchpad.net/lottanzb/](https://launchpad.net/lottanzb/) || [lottanzb](https://aur.archlinux.org/packages/lottanzb/)

*   **[NZBGet](/index.php/NZBGet "NZBGet")** — Usenet binary downloader for .nzb files with web and CLI interface.

	[https://nzbget.net/](https://nzbget.net/) || [nzbget](https://www.archlinux.org/packages/?name=nzbget)

*   **[Pan](https://en.wikipedia.org/wiki/Pan_(newsreader) "wikipedia:Pan (newsreader)")** — GTK Usenet newsreader that's good at both text and binaries.

	[http://pan.rebelbase.com/](http://pan.rebelbase.com/) || [pan](https://www.archlinux.org/packages/?name=pan)

*   **[SABnzbd](/index.php/SABnzbd "SABnzbd")** — An open-source binary newsreader webapp written in Python.

	[https://sabnzbd.org/](https://sabnzbd.org/) || [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/)

*   **XRN** — Usenet newsreader for X Window System.

	[http://www.mit.edu/people/jik/software/xrn.html](http://www.mit.edu/people/jik/software/xrn.html) || [xrn](https://aur.archlinux.org/packages/xrn/)

#### Microblogging clients

See also [Wikipedia:List of Twitter services and applications](https://en.wikipedia.org/wiki/List_of_Twitter_services_and_applications "wikipedia:List of Twitter services and applications").

##### Console

*   **oysttyer** — (official fork of ttytter) An interactive console text-based command-line Twitter client written in Perl.

	[https://github.com/oysttyer/oysttyer](https://github.com/oysttyer/oysttyer) || [oysttyer-git](https://aur.archlinux.org/packages/oysttyer-git/)

*   **Rainbowstream** — A powerful and fully-featured console Twitter client written in Python.

	[https://github.com/orakaro/rainbowstream](https://github.com/orakaro/rainbowstream) || [rainbowstream](https://aur.archlinux.org/packages/rainbowstream/)

*   **toot** — CLI and TUI tool for interacting with Mastodon instances

	[https://github.com/ihabunek/toot](https://github.com/ihabunek/toot) || [toot](https://aur.archlinux.org/packages/toot/)

*   **turses** — Twitter client for the console based off *tyrs* with major improvements.

	[https://github.com/louipc/turses](https://github.com/louipc/turses) || [turses-git](https://aur.archlinux.org/packages/turses-git/)

##### Graphical

*   **Birdie** — Beautiful Twitter client designed for elementary OS.

	[https://www.amuza.uk/birdie](https://www.amuza.uk/birdie) || [birdie-git](https://aur.archlinux.org/packages/birdie-git/)

*   **Choqok** — Microblogging client for KDE that supports Twitter.com, Pump.io, GNU social and opendesktop.org services.

	[http://choqok.gnufolks.org/](http://choqok.gnufolks.org/) || [choqok](https://www.archlinux.org/packages/?name=choqok)

*   **Corebird** — Native GTK Twitter client for the Linux desktop.

	[https://corebird.baedert.org//](https://corebird.baedert.org//) || [corebird](https://aur.archlinux.org/packages/corebird/)

*   **Mikutter** — Simple, powerful Twitter client using [GTK](/index.php/GTK "GTK") and Ruby.

	[https://mikutter.hachune.net/](https://mikutter.hachune.net/) || [mikutter](https://aur.archlinux.org/packages/mikutter/)

*   **Polly** — Linux Twitter client designed for multiple columns of multiple accounts.

	[https://launchpad.net/polly/](https://launchpad.net/polly/) || [polly](https://aur.archlinux.org/packages/polly/)

*   **Pumpa** — Pump.io client written in C++ and Qt.

	[https://pumpa.branchable.com/](https://pumpa.branchable.com/) || [pumpa-git](https://aur.archlinux.org/packages/pumpa-git/)

*   **Turpial** — Multi-interface Twitter client written in Python.

	[http://turpial.org.ve/](http://turpial.org.ve/) || [turpial-git](https://aur.archlinux.org/packages/turpial-git/)

*   **Whalebird** — Mastodon client application. Based on the [Electron](https://electronjs.org/) platform.

	[https://whalebird.org/](https://whalebird.org/) || [whalebird-bin](https://aur.archlinux.org/packages/whalebird-bin/)

#### Blog engines

See also [Wikipedia:Blog software](https://en.wikipedia.org/wiki/Blog_software "wikipedia:Blog software") and [Wikipedia:List of content management systems](https://en.wikipedia.org/wiki/List_of_content_management_systems "wikipedia:List of content management systems").

**Note:** Content managers, social networks, and blog publishers overlap in many functions.

*   **[Diaspora](/index.php/Diaspora "Diaspora")** — A distributed privacy aware social network.

	[https://diasporafoundation.org](https://diasporafoundation.org) || [diaspora-mysql](https://aur.archlinux.org/packages/diaspora-mysql/) or [diaspora-postgresql](https://aur.archlinux.org/packages/diaspora-postgresql/)

*   **[Drupal](/index.php/Drupal "Drupal")** — A PHP-based content management platform.

	[https://www.drupal.org/](https://www.drupal.org/) || [drupal](https://www.archlinux.org/packages/?name=drupal)

*   **[Ghost](/index.php/Ghost "Ghost")** — Blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications.

	[https://ghost.org/](https://ghost.org/) || [ghost-web](https://aur.archlinux.org/packages/ghost-web/)

*   **[Joomla](/index.php/Joomla "Joomla")** — A php Content Management System (CMS) which enables you to build websites and powerful online applications.

	[https://www.joomla.org/](https://www.joomla.org/) || [joomla](https://aur.archlinux.org/packages/joomla/)

*   **[Wordpress](/index.php/Wordpress "Wordpress")** — Blog tool and publishing platform.

	[https://wordpress.org/](https://wordpress.org/) || [wordpress](https://www.archlinux.org/packages/?name=wordpress)

#### Static site generators

*   **Hexo** — Fast, simple and powerful blog framework.

	[https://hexo.io/](https://hexo.io/) || [nodejs-hexo-cli](https://aur.archlinux.org/packages/nodejs-hexo-cli/)

*   **Hugo** — Hugo is a static HTML and CSS website generator written in Go. It is optimized for speed, ease of use, and configurability.

	[https://gohugo.io/](https://gohugo.io/) || [hugo](https://www.archlinux.org/packages/?name=hugo)

*   **[Jekyll](/index.php/Jekyll "Jekyll")** — Static blog engine, written in Ruby, which supports Markdown, textile and other formats.

	[https://jekyllrb.com/](https://jekyllrb.com/) || [jekyll](https://aur.archlinux.org/packages/jekyll/)

*   **Nanoblogger** — A small weblog engine written in Bash for the command line. It uses common UNIX tools such as cat, grep, and sed to create static HTML content. It is not maintained anymore.

	[http://nanoblogger.sourceforge.net/](http://nanoblogger.sourceforge.net/) || [nanoblogger](https://aur.archlinux.org/packages/nanoblogger/)

*   **Nikola** — Static site generator written in Python, with incremental rebuilds and multiple markup formats.

	[https://getnikola.com/](https://getnikola.com/) || [nikola](https://www.archlinux.org/packages/?name=nikola)

*   **Pelican** — Static site generator, powered by Python.

	[http://docs.getpelican.com/](http://docs.getpelican.com/) || [pelican](https://www.archlinux.org/packages/?name=pelican)

### Remote desktop

See also [Wikipedia:Remote desktop software](https://en.wikipedia.org/wiki/Remote_desktop_software "wikipedia:Remote desktop software") and [Wikipedia:Comparison of remote desktop software](https://en.wikipedia.org/wiki/Comparison_of_remote_desktop_software "wikipedia:Comparison of remote desktop software").

#### Remote desktop clients

*   **[AnyDesk](https://en.wikipedia.org/wiki/AnyDesk "wikipedia:AnyDesk")** — Proprietary remote desktop software.

	[https://anydesk.com/](https://anydesk.com/) || [anydesk](https://aur.archlinux.org/packages/anydesk/)

*   **[GNOME Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — A simple GNOME 3 application to access remote or virtual systems. Supports VNC and SPICE.

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **GVncViewer** — Simple VNC Client on Gtk-VNC. Run with `gvncviewer`.

	[https://wiki.gnome.org/Projects/gtk-vnc](https://wiki.gnome.org/Projects/gtk-vnc) || [gtk-vnc](https://www.archlinux.org/packages/?name=gtk-vnc)

*   **[KRDC](https://en.wikipedia.org/wiki/KRDC "wikipedia:KRDC")** — Remote Desktop Client for KDE. Supports RDP and VNC. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[https://www.kde.org/applications/internet/krdc/](https://www.kde.org/applications/internet/krdc/) || [krdc](https://www.archlinux.org/packages/?name=krdc)

*   **[Remmina](/index.php/Remmina "Remmina")** — Remote desktop client written in GTK. Supports RDP, VNC, NX, XDMCP and SSH.

	[https://remmina.org/](https://remmina.org/) || [remmina](https://www.archlinux.org/packages/?name=remmina)

*   **Remote Viewer** — Simple remote display client. Supports SPICE and VNC.

	[https://virt-manager.org/](https://virt-manager.org/) || [virt-viewer](https://www.archlinux.org/packages/?name=virt-viewer)

*   **[TeamViewer](https://en.wikipedia.org/wiki/TeamViewer "wikipedia:TeamViewer")** — Proprietary remote desktop client. It uses its own proprietary protocol.

	[https://www.teamviewer.com/](https://www.teamviewer.com/) || [teamviewer](https://aur.archlinux.org/packages/teamviewer/)

*   **[vncviewer (TigerVNC)](/index.php/TigerVNC "TigerVNC")** — VNC viewer for X.

	[https://tigervnc.org/](https://tigervnc.org/) || [tigervnc](https://www.archlinux.org/packages/?name=tigervnc)

*   **[Vinagre](https://en.wikipedia.org/wiki/Vinagre "wikipedia:Vinagre")** — Remote desktop viewer for GNOME. Supports RDP, VNC, SPICE and SSH. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Vinagre](https://wiki.gnome.org/Apps/Vinagre) || [vinagre](https://www.archlinux.org/packages/?name=vinagre)

*   **xfreerdp** — FreeRDP X11 client. Run with `xfreerdp`.

	[http://www.freerdp.com/](http://www.freerdp.com/) || [freerdp](https://www.archlinux.org/packages/?name=freerdp)

*   **[X2Go](/index.php/X2Go "X2Go") Client** — A graphical client (Qt4) for the X2Go system that uses the [NX technology](https://en.wikipedia.org/wiki/NX_technology "w:NX technology") protocol.

	[https://wiki.x2go.org/doku.php](https://wiki.x2go.org/doku.php) || [x2goclient](https://www.archlinux.org/packages/?name=x2goclient)

#### Remote desktop servers

*   **Krfb** — VNC server for KDE. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[https://www.kde.org/applications/system/krfb](https://www.kde.org/applications/system/krfb) || [krfb](https://www.archlinux.org/packages/?name=krfb)

*   **[Vino](/index.php/Vino "Vino")** — VNC server for GNOME. Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Projects/Vino](https://wiki.gnome.org/Projects/Vino) || [vino](https://www.archlinux.org/packages/?name=vino)

*   **[x0vncserver (TigerVNC)](/index.php/TigerVNC "TigerVNC")** — VNC Server for X displays.

	[https://tigervnc.org/](https://tigervnc.org/) || [tigervnc](https://www.archlinux.org/packages/?name=tigervnc)

*   **[x11vnc](/index.php/X11vnc "X11vnc")** — VNC server for real X displays.

	[http://www.karlrunge.com/x11vnc/](http://www.karlrunge.com/x11vnc/) || [x11vnc](https://www.archlinux.org/packages/?name=x11vnc)

*   **[X2Go](/index.php/X2Go "X2Go") Server** — An open source remote desktop software that uses the [NX technology](https://en.wikipedia.org/wiki/NX_technology "w:NX technology") protocol.

	[https://wiki.x2go.org/doku.php](https://wiki.x2go.org/doku.php) || [x2goserver](https://www.archlinux.org/packages/?name=x2goserver)

*   **[Xrdp](/index.php/Xrdp "Xrdp")** — A daemon that supports RDP. It uses Xvnc, X11rdp or xorgxrdp as a backend.

	[http://xrdp.org/](http://xrdp.org/) || [xrdp](https://aur.archlinux.org/packages/xrdp/)

## Multimedia

### Codecs

See the main article: [Codecs](/index.php/Codecs "Codecs").

### Image

#### Image viewers

See also [Wikipedia:Comparison of image viewers](https://en.wikipedia.org/wiki/Comparison_of_image_viewers "wikipedia:Comparison of image viewers").

##### Framebuffer image viewers

*   **fbi** — Image viewer for the linux framebuffer console.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **fbv** — Very simple graphic file viewer for the framebuffer console.

	[http://s-tech.elsat.net.pl/fbv/](http://s-tech.elsat.net.pl/fbv/) || [fbv](https://www.archlinux.org/packages/?name=fbv)

*   **fim** — Highly customizable and scriptable framebuffer image viewer based on fbi.

	[http://www.nongnu.org/fbi-improved/](http://www.nongnu.org/fbi-improved/) || [fim](https://aur.archlinux.org/packages/fim/)

*   **jfbview** — Framebuffer PDF and image viewer based on Imlib2\. Features include Vim-like controls, rotation and zoom, zoom-to-fit, and fast multi-threaded rendering.

	[https://github.com/jichu4n/jfbview](https://github.com/jichu4n/jfbview) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

##### Graphical image viewers

*   **Ephoto** — A light image viewer based on EFL.

	[https://www.enlightenment.org/about-ephoto](https://www.enlightenment.org/about-ephoto) || [ephoto](https://aur.archlinux.org/packages/ephoto/)

*   **[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")** — Image viewing and cataloging program, which is a part of the GNOME desktop environment.

	[https://wiki.gnome.org/Apps/EyeOfGnome](https://wiki.gnome.org/Apps/EyeOfGnome) || [eog](https://www.archlinux.org/packages/?name=eog)

*   **Eye of MATE** — Simple graphics viewer for the MATE desktop.

	[https://github.com/mate-desktop/eom](https://github.com/mate-desktop/eom) || [eom](https://www.archlinux.org/packages/?name=eom)

*   **EyeSight** — Image viewer for the Hawaii desktop environment.

	[https://github.com/hawaii-desktop/eyesight](https://github.com/hawaii-desktop/eyesight) || [eyesight](https://aur.archlinux.org/packages/eyesight/)

*   **[feh](/index.php/Feh "Feh")** — Fast, lightweight image viewer that uses imlib2.

	[https://feh.finalrewind.org/](https://feh.finalrewind.org/) || [feh](https://www.archlinux.org/packages/?name=feh)

*   **GalaPix** — OpenGL-based image viewer for simultaneously viewing and zooming large collections of image files,

	[https://github.com/Galapix/galapix](https://github.com/Galapix/galapix) || [galapix](https://aur.archlinux.org/packages/galapix/)

*   **[Geeqie](https://en.wikipedia.org/wiki/Geeqie "wikipedia:Geeqie")** — Image browser and viewer (fork of GQview) that adds additional functionality such as support for RAW files.

	[http://geeqie.org/](http://geeqie.org/) || [geeqie](https://www.archlinux.org/packages/?name=geeqie)

*   **GPicView** — Simple and fast image viewer for X, which is part of the [LXDE](/index.php/LXDE "LXDE") desktop.

	[http://lxde.sourceforge.net/gpicview/](http://lxde.sourceforge.net/gpicview/) || GTK 2: [gpicview](https://www.archlinux.org/packages/?name=gpicview), GTK 3: [gpicview-gtk3](https://www.archlinux.org/packages/?name=gpicview-gtk3)

*   **[Gwenview](https://en.wikipedia.org/wiki/Gwenview "wikipedia:Gwenview")** — Fast and easy to use image viewer for the KDE desktop.

	[https://userbase.kde.org/Gwenview](https://userbase.kde.org/Gwenview) || [gwenview](https://www.archlinux.org/packages/?name=gwenview)

*   **ida** — X11 application (Motif based) for viewing images.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **imv** — Lightweight image viewer with support for Wayland and animated GIFs which uses FreeImage.

	[https://www.github.com/eXeC64/imv/](https://www.github.com/eXeC64/imv/) || [imv](https://www.archlinux.org/packages/?name=imv)

*   **LxImage-Qt** — The LXQt image viewer.

	[https://github.com/lxde/lximage-qt](https://github.com/lxde/lximage-qt) || [lximage-qt](https://www.archlinux.org/packages/?name=lximage-qt)

*   **meh** — meh is a small, simple, super fast image viewer using raw XLib.

	[https://www.johnhawthorn.com/meh/](https://www.johnhawthorn.com/meh/) || [meh-git](https://aur.archlinux.org/packages/meh-git/)

*   **Mirage** — PyGTK image viewer featuring support for crop and resize, custom actions and a thumbnail panel.

	[https://sourceforge.net/projects/mirageiv.berlios/](https://sourceforge.net/projects/mirageiv.berlios/) || [mirage](https://aur.archlinux.org/packages/mirage/)

*   **nomacs** — Qt image viewer. It is feature-rich but starts fast and can be configured to show additional widgets or only the image.

	[https://nomacs.org/](https://nomacs.org/) || [nomacs](https://www.archlinux.org/packages/?name=nomacs)

*   **Phototonic** — Fast and functional image viewer and browser (Qt).

	[https://github.com/oferkv/phototonic/](https://github.com/oferkv/phototonic/) || [phototonic](https://aur.archlinux.org/packages/phototonic/)

*   **PhotoQt** — Fast and highly configurable image viewer with a simple and nice interface.

	[https://photoqt.org/](https://photoqt.org/) || [photoqt](https://aur.archlinux.org/packages/photoqt/)

*   **pix** — Image viewer and browser based on gthumb. X-Apps Project.

	[https://github.com/linuxmint/pix](https://github.com/linuxmint/pix) || [pix](https://aur.archlinux.org/packages/pix/)

*   **pqiv** — GTK 3 based command-line image viewer with a minimal UI supporting images in compressed archives, rewrite of qiv.

	[https://github.com/phillipberndt/pqiv/](https://github.com/phillipberndt/pqiv/) || [pqiv](https://aur.archlinux.org/packages/pqiv/)

*   **qimgv** — Fast and easy to use Qt5 image viewer. Supports webm/mp4 playback via mpv.

	[https://github.com/easymodo/qimgv/](https://github.com/easymodo/qimgv/) || [qimgv](https://aur.archlinux.org/packages/qimgv/)

*   **Quick Image Viewer** — Very small and fast image viewer based on GTK and imlib2.

	[http://spiegl.de/qiv/](http://spiegl.de/qiv/) || [qiv](https://www.archlinux.org/packages/?name=qiv)

*   **qView** — Qt image viewer designed with minimalism and usability in mind.

	[https://interversehq.com/qview/](https://interversehq.com/qview/) || [qview](https://aur.archlinux.org/packages/qview/)

*   **Ristretto** — Fast and lightweight image viewer for the Xfce desktop environment.

	[https://docs.xfce.org/apps/ristretto/start](https://docs.xfce.org/apps/ristretto/start) || [ristretto](https://www.archlinux.org/packages/?name=ristretto)

*   **shufti** — shufti non-destructively saves and restores the zoom level, rotation, window size, desktop location and viewing area on a per-image/file location basis

	[https://github.com/danboid/shufti](https://github.com/danboid/shufti) || [shufti](https://aur.archlinux.org/packages/shufti/)

*   **[sxiv](/index.php/Sxiv "Sxiv")** — Simple image viewer based on imlib2 that works well with tiling window managers.

	[https://github.com/muennich/sxiv](https://github.com/muennich/sxiv) || [sxiv](https://www.archlinux.org/packages/?name=sxiv)

*   **Viewnior** — Minimalistic GTK image viewer featuring support for flipping, rotating, animations and configurable mouse actions.

	[http://siyanpanayotov.com/project/viewnior](http://siyanpanayotov.com/project/viewnior) || [viewnior](https://www.archlinux.org/packages/?name=viewnior)

*   **Vimiv** — An image viewer with vim-like keybindings. It is written in python3 using the Gtk3 toolkit.

	[http://karlch.github.io/vimiv/](http://karlch.github.io/vimiv/) || [vimiv](https://www.archlinux.org/packages/?name=vimiv)

*   **Xloadimage** — Classic X image viewer.

	[https://sioseis.ucsd.edu/xloadimage.html](https://sioseis.ucsd.edu/xloadimage.html) || [xloadimage](https://www.archlinux.org/packages/?name=xloadimage)

#### Image organizers

See also [Wikipedia:Image organizer](https://en.wikipedia.org/wiki/Image_organizer "wikipedia:Image organizer").

*   **Deepin Image Viewer** — Image viewer and organizer for Deepin desktop.

	[https://www.deepin.org/en/original/deepin-image-viewer/](https://www.deepin.org/en/original/deepin-image-viewer/) || [deepin-image-viewer](https://www.archlinux.org/packages/?name=deepin-image-viewer)

*   **[digiKam](https://en.wikipedia.org/wiki/digiKam "wikipedia:digiKam")** — KDE-based image organizer with built-in editing features via a plugin architecture. digiKam asserts it is more full featured than similar applications with a larger set of image manipulation features including RAW image import and manipulation.

	[https://www.digikam.org/](https://www.digikam.org/) || [digikam](https://www.archlinux.org/packages/?name=digikam)

*   **Frogr** — Small application for the GNOME desktop that allows users to manage their accounts in the Flickr image hosting website.

	[https://wiki.gnome.org/Apps/Frogr](https://wiki.gnome.org/Apps/Frogr) || [frogr](https://aur.archlinux.org/packages/frogr/)

*   **GNOME Photos** — Access, organize, and share your photos on GNOME.

	[https://wiki.gnome.org/Apps/Photos](https://wiki.gnome.org/Apps/Photos) || [gnome-photos](https://www.archlinux.org/packages/?name=gnome-photos)

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — Image viewer and browser for the GNOME desktop.

	[https://wiki.gnome.org/Apps/Gthumb](https://wiki.gnome.org/Apps/Gthumb) || [gthumb](https://www.archlinux.org/packages/?name=gthumb)

*   **[KPhotoAlbum](https://en.wikipedia.org/wiki/KPhotoAlbum "wikipedia:KPhotoAlbum")** — Digital image cataloging software that supports annotation, browsing, searching and viewing of digital images and videos.

	[https://www.kphotoalbum.org/](https://www.kphotoalbum.org/) || [kphotoalbum](https://www.archlinux.org/packages/?name=kphotoalbum)

*   **Pantheon Photos** — Photo organizer for Pantheon.

	[https://launchpad.net/pantheon-photos](https://launchpad.net/pantheon-photos) || [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos)

*   **Rapid Photo Downloader** — Download photos and videos from cameras, memory cards and portable storage devices.

	[https://www.damonlynch.net/rapid/](https://www.damonlynch.net/rapid/) || [rapid-photo-downloader](https://www.archlinux.org/packages/?name=rapid-photo-downloader)

*   **[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")** — A digital photo organizer designed for the GNOME desktop environment

	[https://wiki.gnome.org/Apps/Shotwell](https://wiki.gnome.org/Apps/Shotwell) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

#### Image processing

*   **CairoSVG** — SVG to PNG, PDF, PS converter.

	[https://cairosvg.org/](https://cairosvg.org/) || [python-cairosvg](https://www.archlinux.org/packages/?name=python-cairosvg)

*   **Converseen** — Batch image converter and resizer.

	[http://converseen.fasterland.net/](http://converseen.fasterland.net/) || [converseen](https://www.archlinux.org/packages/?name=converseen)

*   **[dcraw](https://en.wikipedia.org/wiki/dcraw "wikipedia:dcraw")** — Converts many camera RAW formats.

	[http://www.cybercom.net/~dcoffin/dcraw/](http://www.cybercom.net/~dcoffin/dcraw/) || [dcraw](https://www.archlinux.org/packages/?name=dcraw)

*   **Fyre** — Tool for producing computational artwork based on histograms of iterated chaotic functions.

	[http://fyre.navi.cx/](http://fyre.navi.cx/) || [fyre](https://aur.archlinux.org/packages/fyre/)

*   **[G'MIC](https://en.wikipedia.org/wiki/G%27MIC "wikipedia:G'MIC")** — Full-featured open-source framework for image processing, providing several different user interfaces to convert/manipulate/filter/visualize generic image datasets, ranging from 1d scalar signals to 3d+t sequences of multi-spectral volumetric images, including 2d color images.

	[http://www.gmic.eu/](http://www.gmic.eu/) || [gmic](https://www.archlinux.org/packages/?name=gmic)

*   **[GraphicsMagick](https://en.wikipedia.org/wiki/GraphicsMagick "wikipedia:GraphicsMagick")** — Fork of ImageMagick designed to have API and command-line stability. It also supports multi-CPU for enhanced performance and thus is used by some large commercial sites (Flickr, etsy) for its performance.

	[http://www.graphicsmagick.org/](http://www.graphicsmagick.org/) || [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick)

*   **[ImageMagick](/index.php/ImageMagick "ImageMagick")** — Command-line image manipulation program. It is known for its accurate format conversions with support for over 100 formats. Its API enables it to be scripted and it is usually used as a backend processor.

	[http://www.imagemagick.org/script/index.php](http://www.imagemagick.org/script/index.php) || [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

##### Image compression

*   **[Guetzli](https://en.wikipedia.org/wiki/Guetzli "wikipedia:Guetzli")** — A perceptual JPEG encoder, aiming for excellent compression density at high visual quality.

	[https://github.com/google/guetzli](https://github.com/google/guetzli) || [guetzli](https://www.archlinux.org/packages/?name=guetzli)

*   **ImCompressor** — Simple and lossless image compressor. (GUI for optipng)

	[https://github.com/Huluti/ImCompressor](https://github.com/Huluti/ImCompressor) || [imcompressor](https://aur.archlinux.org/packages/imcompressor/)

*   **jpegoptim** — JPEG optimization utility providing lossless and lossy compression.

	[https://www.kokkonen.net/tjko/projects.html#jpegoptim](https://www.kokkonen.net/tjko/projects.html#jpegoptim) || [jpegoptim](https://www.archlinux.org/packages/?name=jpegoptim)

*   **optipng** — Lossless PNG compressor.

	[http://optipng.sourceforge.net/](http://optipng.sourceforge.net/) || [optipng](https://www.archlinux.org/packages/?name=optipng)

*   **zopflipng** — Highly efficient PNG optimisation tool using Google's zopfli library

	[https://github.com/google/zopfli](https://github.com/google/zopfli) || [zopflipng-git](https://aur.archlinux.org/packages/zopflipng-git/)

#### Raster graphics editors

See also [Wikipedia:Comparison of raster graphics editors](https://en.wikipedia.org/wiki/Comparison_of_raster_graphics_editors "wikipedia:Comparison of raster graphics editors").

*   **AzPainter** — Painting software for illustration drawing.

	[https://github.com/Symbian9/azpainter](https://github.com/Symbian9/azpainter) || [azpainter](https://aur.archlinux.org/packages/azpainter/)

*   **Deepin Draw** — Lightweight drawing tool for Deepin desktop.

	[https://github.com/linuxdeepin/deepin-draw](https://github.com/linuxdeepin/deepin-draw) || [deepin-draw](https://www.archlinux.org/packages/?name=deepin-draw)

*   **Drawing** — Drawing application for the GNOME desktop, using Cairo and GdkPixbuf for basic drawing operations.

	[https://github.com/maoschanz/drawing](https://github.com/maoschanz/drawing) || [drawing](https://www.archlinux.org/packages/?name=drawing)

*   **[GIMP](/index.php/GIMP "GIMP")** — Image editing suite in the vein of proprietary editors such as [Adobe Photoshop](https://en.wikipedia.org/wiki/Adobe_Photoshop "wikipedia:Adobe Photoshop"). GIMP ([GNU](/index.php/GNU "GNU") Image Manipulation Program) has been started in the mid 1990s and has acquired a large number of [plugins](/index.php/CMYK_support_in_The_GIMP "CMYK support in The GIMP") and additional tools.

	[https://www.gimp.org/](https://www.gimp.org/) || [gimp](https://www.archlinux.org/packages/?name=gimp)

*   **[Gpaint](https://en.wikipedia.org/wiki/GNU_Paint "wikipedia:GNU Paint")** — [Paintbrush](https://en.wikipedia.org/wiki/PC_Paintbrush "wikipedia:PC Paintbrush") clone for GNOME.

	[https://www.gnu.org/software/gpaint/](https://www.gnu.org/software/gpaint/) || [gpaint](https://aur.archlinux.org/packages/gpaint/)

*   **[GrafX2](https://en.wikipedia.org/wiki/GrafX2 "wikipedia:GrafX2")** — Bitmap paint program specialized in 256 color drawing.

	[http://grafx2.chez.com/](http://grafx2.chez.com/) || [grafx2](https://www.archlinux.org/packages/?name=grafx2)

*   **[KolourPaint](https://en.wikipedia.org/wiki/KolourPaint "wikipedia:KolourPaint")** — Free raster graphics editor for KDE, similar to Microsoft's Paint application before Windows 7, but with some additional features such as support for transparency. Part of [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) and [kdegraphics](https://www.archlinux.org/groups/x86_64/kdegraphics/) groups.

	[http://kolourpaint.org](http://kolourpaint.org) || [kolourpaint](https://www.archlinux.org/packages/?name=kolourpaint)

*   **[Krita](https://en.wikipedia.org/wiki/Krita "wikipedia:Krita")** — Digital painting and illustration software included based on the KDE platform.

	[https://krita.org/](https://krita.org/) || [krita](https://www.archlinux.org/packages/?name=krita)

*   **Milton** — Infinite-canvas paint program.

	[https://www.miltonpaint.com/](https://www.miltonpaint.com/) || [milton](https://aur.archlinux.org/packages/milton/), [milton-git](https://aur.archlinux.org/packages/milton-git/)

*   **mtPaint** — Graphics editing program geared towards creating indexed palette images and pixel art.

	[http://mtpaint.sourceforge.net/](http://mtpaint.sourceforge.net/) || [mtpaint](https://www.archlinux.org/packages/?name=mtpaint)

*   **[MyPaint](https://en.wikipedia.org/wiki/MyPaint "wikipedia:MyPaint")** — Free software graphics application for digital painters.

	[http://mypaint.org](http://mypaint.org) || [mypaint](https://www.archlinux.org/packages/?name=mypaint)

*   **PhotoFlare** — Simple but powerful image editor originally inspired by PhotoFiltre.

	[https://photoflare.io/](https://photoflare.io/) || [photoflare](https://www.archlinux.org/packages/?name=photoflare)

*   **[Pinta](https://en.wikipedia.org/wiki/Pinta_(software) "wikipedia:Pinta (software)")** — Drawing and editing program modeled after [Paint.NET](https://en.wikipedia.org/wiki/Paint.net "wikipedia:Paint.net"). Its goal is to provide a simplified alternative to GIMP for casual users.

	[https://pinta-project.com/](https://pinta-project.com/) || [pinta](https://www.archlinux.org/packages/?name=pinta)

*   **[XPaint](https://en.wikipedia.org/wiki/XPaint "wikipedia:XPaint")** — Color image editing tool which features most standard paint program options.

	[https://sourceforge.net/projects/sf-xpaint/](https://sourceforge.net/projects/sf-xpaint/) || [xpaint](https://aur.archlinux.org/packages/xpaint/)

Some image viewers and organizers like [digiKam](https://en.wikipedia.org/wiki/digiKam also provide some basic image manipulation functionality.

#### Photo editors

*   **[darktable](https://en.wikipedia.org/wiki/darktable "wikipedia:darktable")** — Photography workflow and RAW development application.

	[http://www.darktable.org/](http://www.darktable.org/) || [darktable](https://www.archlinux.org/packages/?name=darktable)

*   **[Hugin](https://en.wikipedia.org/wiki/Hugin_(software) "wikipedia:Hugin (software)")** — Panorama photo stitcher.

	[http://hugin.sourceforge.net/](http://hugin.sourceforge.net/) || [hugin](https://www.archlinux.org/packages/?name=hugin)

*   **[LightZone](https://en.wikipedia.org/wiki/LightZone "wikipedia:LightZone")** — Professional-level digital darkroom and photo editor comparable to Photoshop Lightroom.

	[http://lightzoneproject.org/](http://lightzoneproject.org/) || [lightzone](https://aur.archlinux.org/packages/lightzone/)

*   **[Luminance HDR](https://en.wikipedia.org/wiki/Luminance_HDR "wikipedia:Luminance HDR")** — Open source graphical user interface application that aims to provide a workflow for HDR imaging.

	[http://qtpfsgui.sourceforge.net/](http://qtpfsgui.sourceforge.net/) || [luminancehdr](https://www.archlinux.org/packages/?name=luminancehdr)

*   **[nUFRaw](https://en.wikipedia.org/wiki/UFRaw "wikipedia:UFRaw")** — Utility to read and manipulate raw images from digital cameras using DCRaw.

	[https://sourceforge.net/projects/nufraw/](https://sourceforge.net/projects/nufraw/) || [gimp-nufraw](https://www.archlinux.org/packages/?name=gimp-nufraw)

*   **Oqapy** — Photographic workflow application.

	[https://oqapy.eu/](https://oqapy.eu/) || [oqapy](https://aur.archlinux.org/packages/oqapy/)

*   **[Rawstudio](https://en.wikipedia.org/wiki/Rawstudio "wikipedia:Rawstudio")** — Raw-image converter written in GTK.

	[https://rawstudio.org/](https://rawstudio.org/) || [rawstudio](https://aur.archlinux.org/packages/rawstudio/)

*   **[RawTherapee](https://en.wikipedia.org/wiki/RawTherapee "wikipedia:RawTherapee")** — A powerful cross-platform raw image processing program.

	[http://www.rawtherapee.com/](http://www.rawtherapee.com/) || [rawtherapee](https://www.archlinux.org/packages/?name=rawtherapee)

#### Vector graphics editors

See also [Wikipedia:Comparison of vector graphics editors](https://en.wikipedia.org/wiki/Comparison_of_vector_graphics_editors "wikipedia:Comparison of vector graphics editors").

*   **[Dia](https://en.wikipedia.org/wiki/Dia_(software) "wikipedia:Dia (software)")** — GTK-based diagram creation program.

	[https://wiki.gnome.org/Apps/Dia](https://wiki.gnome.org/Apps/Dia) || [dia](https://www.archlinux.org/packages/?name=dia)

*   **draw.io desktop** — Diagram drawing application built on web technology. Based on the [Electron](https://electronjs.org/) platform.

	[https://about.draw.io/](https://about.draw.io/) || [drawio-desktop](https://aur.archlinux.org/packages/drawio-desktop/)

*   **Gravit Designer** — Proprietary vector design application. Based on the [Electron](https://electronjs.org/) platform.

	[https://designer.io/](https://designer.io/) || [gravit-designer-bin](https://aur.archlinux.org/packages/gravit-designer-bin/)

*   **[Inkscape](/index.php/Inkscape "Inkscape")** — Vector graphics editor, with capabilities similar to [Illustrator](https://en.wikipedia.org/wiki/Adobe_Illustrator "wikipedia:Adobe Illustrator"), [CorelDraw](https://en.wikipedia.org/wiki/CorelDRAW "wikipedia:CorelDRAW"), or [Xara X](https://en.wikipedia.org/wiki/Xara_X "wikipedia:Xara X"), using the SVG (Scalable Vector Graphics) file format. Inkscape supports many advanced SVG features (markers, clones, alpha blending, etc.) and great care is taken in designing a streamlined interface. It is very easy to edit nodes, perform complex path operations, trace bitmaps and much more. It's developers also aim to maintain a thriving user and developer community by using open, community-oriented development.

	[https://inkscape.org/](https://inkscape.org/) || [inkscape](https://www.archlinux.org/packages/?name=inkscape)

*   **[Karbon](https://en.wikipedia.org/wiki/Karbon_(software) "wikipedia:Karbon (software)")** — Vector graphics editor, part of the Calligra Suite.

	[https://www.calligra.org/karbon/](https://www.calligra.org/karbon/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[LibreOffice Draw](/index.php/LibreOffice "LibreOffice")** — Vector graphics editor and diagramming tool included in the LibreOffice suite similar to Microsoft Visio.

	[https://www.libreoffice.org/discover/draw/](https://www.libreoffice.org/discover/draw/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **Mockingbot** — Proprietary prototyping & collaboration design tool. Based on the [Electron](https://electronjs.org/) platform.

	[https://mockingbot.com/](https://mockingbot.com/) || [mockingbot](https://aur.archlinux.org/packages/mockingbot/)

*   **[OpenOffice Draw](/index.php/OpenOffice "OpenOffice")** — Vector graphics editor and diagramming tool included in the OpenOffice suite.

	[http://www.openoffice.org/product/draw.html](http://www.openoffice.org/product/draw.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[Pencil Project](https://en.wikipedia.org/wiki/Pencil2D "wikipedia:Pencil2D")** — GUI prototyping and mockup tool. Based on the [Electron](https://electronjs.org/) platform.

	[http://pencil.evolus.vn/](http://pencil.evolus.vn/) || [pencil](https://aur.archlinux.org/packages/pencil/)

*   **[sK1](https://en.wikipedia.org/wiki/SK1_(program) "wikipedia:SK1 (program)")** — Replacement for Adobe Illustrator or CorelDraw, oriented for "prepress ready" PostScript & PDF output.

	[https://sk1project.net/](https://sk1project.net/) || [sk1](https://www.archlinux.org/packages/?name=sk1)

*   **[yEd](https://en.wikipedia.org/wiki/yEd "wikipedia:yEd")** — General-purpose proprietary diagramming program for flowcharts, network diagrams, UML diagrams, BPMN diagrams, mind maps, organization charts, and Entity Relationship diagrams.

	[https://www.yworks.com/products/yed](https://www.yworks.com/products/yed) || [yed](https://aur.archlinux.org/packages/yed/)

*   **[Xfig](https://en.wikipedia.org/wiki/Xfig "wikipedia:Xfig")** — Interactive drawing tool.

	[http://mcj.sourceforge.net/](http://mcj.sourceforge.net/) || [xfig](https://aur.archlinux.org/packages/xfig/)

#### Font editors

See also [Wikipedia:Comparison of font editors](https://en.wikipedia.org/wiki/Comparison_of_font_editors "wikipedia:Comparison of font editors").

*   **Birdfont** — Font editor which lets you create vector graphics and export TTF, EOT and SVG fonts.

	[https://birdfont.org/](https://birdfont.org/) || [birdfont](https://aur.archlinux.org/packages/birdfont/)

*   **[FontForge](https://en.wikipedia.org/wiki/FontForge "wikipedia:FontForge")** — Outline font editor.

	[https://fontforge.github.io/](https://fontforge.github.io/) || [fontforge](https://www.archlinux.org/packages/?name=fontforge)

*   **TruFont** — Font-editing application.

	[http://trufont.github.io/](http://trufont.github.io/) || [trufont-git](https://aur.archlinux.org/packages/trufont-git/)

#### 2D animation

*   **OpenStopMotion** — Capture program for creating stopmotion video clips.

	[http://qstopmotion.org/](http://qstopmotion.org/) || [openstopmotion](https://aur.archlinux.org/packages/openstopmotion/)

*   **[OpenToonz](https://en.wikipedia.org/wiki/Toonz "wikipedia:Toonz")** — 2D animation creation software.

	[https://opentoonz.github.io/e/](https://opentoonz.github.io/e/) || [opentoonz](https://aur.archlinux.org/packages/opentoonz/)

*   **[Pencil2D](https://en.wikipedia.org/wiki/Pencil2D "wikipedia:Pencil2D")** — Easy, intuitive tool to make 2D hand-drawn animations.

	[https://www.pencil2d.org/](https://www.pencil2d.org/) || [pencil2d](https://aur.archlinux.org/packages/pencil2d/)

*   **qStopMotion** — Application for creating stop-motion animation movies. The users will be able to create stop-motions from pictures imported from a camera or from the harddrive and export the animation to different video formats such as mpeg or avi.

	[http://qstopmotion.org/](http://qstopmotion.org/) || [qstopmotion](https://aur.archlinux.org/packages/qstopmotion/)

*   **Stopmotion** — Application to create stop-motion animations. It helps you capture and edit the frames of your animation and export them as a single file.

	[http://linuxstopmotion.org/](http://linuxstopmotion.org/) || [stopmotion](https://aur.archlinux.org/packages/stopmotion/)

*   **[Synfig Studio](https://en.wikipedia.org/wiki/Synfig "wikipedia:Synfig")** — 2D animation software, designed as powerful industrial-strength solution for creating film-quality animation using a vector and bitmap artwork.

	[https://www.synfig.org/](https://www.synfig.org/) || [synfigstudio](https://aur.archlinux.org/packages/synfigstudio/)

*   **[TupiTube Desk](https://en.wikipedia.org/wiki/Tupi_(software) "wikipedia:Tupi (software)")** — Desktop application to create and share 2D animations, focused on kids and teenagers.

	[https://www.maefloresta.com/](https://www.maefloresta.com/) || [tupitube.desk](https://aur.archlinux.org/packages/tupitube.desk/)

#### 3D computer graphics

See also [Wikipedia:Comparison of 3D computer graphics software](https://en.wikipedia.org/wiki/Comparison_of_3D_computer_graphics_software "wikipedia:Comparison of 3D computer graphics software").

*   **Art of Illusion** — 3D modeling and rendering studio written in Java.

	[http://www.artofillusion.org/](http://www.artofillusion.org/) || [aoi](https://aur.archlinux.org/packages/aoi/)

*   **[Blender](/index.php/Blender "Blender")** — Fully integrated 3D graphics creation suite capable of 3D modeling, texturing, and animation, among other things.

	[https://www.blender.org/](https://www.blender.org/) || [blender](https://www.archlinux.org/packages/?name=blender)

*   **Goxel** — Open Source 3D voxel editor.

	[https://guillaumechereau.github.io/goxel/](https://guillaumechereau.github.io/goxel/) || [goxel](https://aur.archlinux.org/packages/goxel/)

*   **LuxRender** — Rendering system for physically correct, unbiased image synthesis.

	[http://luxrender.net/](http://luxrender.net/) || [luxrender-hg](https://aur.archlinux.org/packages/luxrender-hg/)

*   **[MakeHuman™](https://en.wikipedia.org/wiki/MakeHuman "wikipedia:MakeHuman")** — Parametrical modeling program for creating human bodies.

	[http://www.makehumancommunity.org/](http://www.makehumancommunity.org/) || [makehuman](https://aur.archlinux.org/packages/makehuman/)

*   **[Sweet Home 3D](https://en.wikipedia.org/wiki/Sweet_Home_3D "wikipedia:Sweet Home 3D")** — Interior design software application for the planning and development of floor plans

	[http://sweethome3d.com/](http://sweethome3d.com/) || [sweethome3d](https://www.archlinux.org/packages/?name=sweethome3d)

*   **[POV-Ray](https://en.wikipedia.org/wiki/POV-Ray "wikipedia:POV-Ray")** — Script-based raytracer for creating 3D graphics.

	[http://www.povray.org/](http://www.povray.org/) || [povray](https://www.archlinux.org/packages/?name=povray)

*   **VoxelShop** — Extremely intuitive and powerful software to modify and create voxel objects.

	[https://blackflux.com/node/11](https://blackflux.com/node/11) || [voxelshop](https://aur.archlinux.org/packages/voxelshop/)

*   **[Wings 3D](https://en.wikipedia.org/wiki/Wings3d "wikipedia:Wings3d")** — Advanced subdivision modeler that is both powerful and easy to use.

	[http://www.wings3d.com/](http://www.wings3d.com/) || [wings3d](https://www.archlinux.org/packages/?name=wings3d)

#### Color pickers

*   **Agave** — Colorscheme designer tool for GNOME.

	[https://web.archive.org/web/20170327063642/http://home.gna.org/colorscheme/](https://web.archive.org/web/20170327063642/http://home.gna.org/colorscheme/) || [agave](https://aur.archlinux.org/packages/agave/)

*   **Chameleon** — Simple color picker for X11 which outputs colors to stdout.

	[https://github.com/seebye/chameleon](https://github.com/seebye/chameleon) || [chameleon-git](https://aur.archlinux.org/packages/chameleon-git/)

*   **ColorGrab** — Cross-platform color picker.

	[https://github.com/nielssp/colorgrab](https://github.com/nielssp/colorgrab) || [colorgrab](https://aur.archlinux.org/packages/colorgrab/)

*   **Color Picker** — Simplistic color picker for the Pantheon desktop.

	[https://github.com/RonnyDo/ColorPicker](https://github.com/RonnyDo/ColorPicker) || [color-picker-git](https://aur.archlinux.org/packages/color-picker-git/)

*   **Deepin Picker** — Color picker tool for Deepin desktop.

	[https://www.deepin.org/en/original/deepin-picker/](https://www.deepin.org/en/original/deepin-picker/) || [deepin-picker](https://www.archlinux.org/packages/?name=deepin-picker)

*   **delicolour** — Lightweight GTK 3 color finder.

	[https://github.com/eepp/delicolour](https://github.com/eepp/delicolour) || [delicolour](https://aur.archlinux.org/packages/delicolour/)

*   **gcolor2** — Simple GTK 2 color selector.

	[http://gcolor2.sourceforge.net/](http://gcolor2.sourceforge.net/) || [gcolor2](https://www.archlinux.org/packages/?name=gcolor2)

*   **Gcolor3** — Simple GTK 3 color selector.

	[https://www.hjdskes.nl/projects/gcolor3/](https://www.hjdskes.nl/projects/gcolor3/) || [gcolor3](https://www.archlinux.org/packages/?name=gcolor3)

*   **GPick** — Advanced color picker tool.

	[http://www.gpick.org/](http://www.gpick.org/) || [gpick](https://www.archlinux.org/packages/?name=gpick)

*   **KColorChooser** — Simple application to select the color from the screen or from a pallete. Part of [kdegraphics](https://www.archlinux.org/groups/x86_64/kdegraphics/).

	[https://www.kde.org/applications/graphics/kcolorchooser/](https://www.kde.org/applications/graphics/kcolorchooser/) || [kcolorchooser](https://www.archlinux.org/packages/?name=kcolorchooser)

*   **MATE Color Selection** — Choose colors from the palette or the screen. Run with `mate-color-select`.

	[https://mate-desktop.org/](https://mate-desktop.org/) || [mate-desktop](https://www.archlinux.org/packages/?name=mate-desktop)

*   **Pick** — Simple color picker tool for the Linux desktop.

	[https://www.kryogenix.org/code/pick](https://www.kryogenix.org/code/pick) || [pick-colour-picker](https://aur.archlinux.org/packages/pick-colour-picker/)

*   **xcolor** — Lightweight color picker for X11.

	[https://soft.github.io/xcolor/](https://soft.github.io/xcolor/) || [xcolor](https://aur.archlinux.org/packages/xcolor/)

#### Screenshot

See [Screen capture#Screenshot software](/index.php/Screen_capture#Screenshot_software "Screen capture").

#### Digital camera managers

See [Libgphoto2#Installation](/index.php/Libgphoto2#Installation "Libgphoto2").

### Audio

#### Audio systems

See also the main article [Sound system](/index.php/Sound_system "Sound system") and [Wikipedia:Sound server](https://en.wikipedia.org/wiki/Sound_server "wikipedia:Sound server").

#### Audio players

See also [Music Player Daemon#Clients](/index.php/Music_Player_Daemon#Clients "Music Player Daemon") and [Wikipedia:Comparison of audio player software](https://en.wikipedia.org/wiki/Comparison_of_audio_player_software "wikipedia:Comparison of audio player software").

##### Console

*   **[cmus](/index.php/Cmus "Cmus")** — Very feature-rich ncurses-based music player.

	[https://cmus.github.io/](https://cmus.github.io/) || [cmus](https://www.archlinux.org/packages/?name=cmus)

*   **Cplay** — Curses front-end for various audio players (ogg123, mpg123, mpg321, splay, madplay, and mikmod, xmp, and sox).

	[https://directory.fsf.org/wiki/Cplay](https://directory.fsf.org/wiki/Cplay) || [cplay](https://aur.archlinux.org/packages/cplay/)

*   **Herrie** — Minimalistic console-based music player with native AudioScrobbler support.

	[https://github.com/EdSchouten/herrie](https://github.com/EdSchouten/herrie) || [herrie](https://aur.archlinux.org/packages/herrie/)

*   **[MOC](/index.php/MOC "MOC")** — Ncurses console audio player with support for the MP3, OGG, and WAV formats.

	[https://moc.daper.net/](https://moc.daper.net/) || [moc](https://www.archlinux.org/packages/?name=moc)

*   **MPFC** — Gstreamer-based audio player with curses interface.

	[https://code.google.com/archive/p/mpfc/](https://code.google.com/archive/p/mpfc/) || [mpfc](https://aur.archlinux.org/packages/mpfc/)

*   **[mpg123](https://en.wikipedia.org/wiki/Mpg123 "wikipedia:Mpg123")** — Fast free MP3 console audio player for Linux, FreeBSD, Solaris, HP-UX and nearly all other UNIX systems (also decodes MP1 and MP2 files).

	[https://www.mpg123.org/](https://www.mpg123.org/) || [mpg123](https://www.archlinux.org/packages/?name=mpg123)

*   **[pianobar](/index.php/Pianobar "Pianobar")** — Console-based frontend for the online radio Pandora.

	[https://6xq.net/projects/pianobar/](https://6xq.net/projects/pianobar/) || [pianobar](https://www.archlinux.org/packages/?name=pianobar)

*   **vitunes** — Curses-based music player and playlist manager with vim-like keybindings.

	[http://vitunes.org/](http://vitunes.org/) || [vitunes](https://aur.archlinux.org/packages/vitunes/)

*   **whistle** — Curses-based commandline audio player.

	[https://github.com/ap0calypse/whistle/](https://github.com/ap0calypse/whistle/) || [whistle-git](https://aur.archlinux.org/packages/whistle-git/)

*   **[XMMS2](https://en.wikipedia.org/wiki/XMMS2 "wikipedia:XMMS2")** — Complete rewrite of the popular music player.

	[https://xmms2.org](https://xmms2.org) || [xmms2](https://www.archlinux.org/packages/?name=xmms2)

##### Graphical

###### GStreamer-based

*   **[Banshee](https://en.wikipedia.org/wiki/Banshee_(media_player) "wikipedia:Banshee (media player)")** — [iTunes](https://en.wikipedia.org/wiki/iTunes "wikipedia:iTunes") clone, built with GTK and [Mono](/index.php/Mono "Mono"), feature-rich.

	[http://banshee.fm/](http://banshee.fm/) || [banshee](https://aur.archlinux.org/packages/banshee/)

*   **[Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)")** — Amarok 1.4 clone, ported to Qt 4.

	[https://www.clementine-player.org/](https://www.clementine-player.org/) || [clementine](https://www.archlinux.org/packages/?name=clementine)

*   **Cozy** — Modern audio book player for Linux using GTK 3.

	[https://github.com/geigi/cozy](https://github.com/geigi/cozy) || [cozy-audiobooks](https://aur.archlinux.org/packages/cozy-audiobooks/)

*   **[Exaile](/index.php/Exaile "Exaile")** — GTK clone of Amarok.

	[https://www.exaile.org/](https://www.exaile.org/) || [exaile](https://aur.archlinux.org/packages/exaile/)

*   **GNOME Internet Radio Locator** — Easily find live radio programs based on geographical location of radio broadcasters on the Internet.

	[https://wiki.gnome.org/Apps/InternetRadioLocator](https://wiki.gnome.org/Apps/InternetRadioLocator) || [gnome-internet-radio-locator](https://aur.archlinux.org/packages/gnome-internet-radio-locator/)

*   **GNOME Music** — Music is the new GNOME music playing application. It aims to combine an elegant and immersive browsing experience with simple and straightforward controls.

	[https://wiki.gnome.org/Apps/Music](https://wiki.gnome.org/Apps/Music) || [gnome-music](https://www.archlinux.org/packages/?name=gnome-music)

*   **Gradio** — GTK 3 application for finding and listening to internet radio stations.

	[https://github.com/haecker-felix/gradio](https://github.com/haecker-felix/gradio) || [gradio](https://aur.archlinux.org/packages/gradio/)

*   **Guayadeque** — Full featured media player that can easily manage large collections and uses the GStreamer media framework.

	[https://www.guayadeque.org/](https://www.guayadeque.org/) || [guayadeque](https://aur.archlinux.org/packages/guayadeque/)

*   **Lollypop** — A GNOME music player.

	[https://wiki.gnome.org/Apps/Lollypop](https://wiki.gnome.org/Apps/Lollypop) || [lollypop](https://www.archlinux.org/packages/?name=lollypop)

*   **[Muine](https://en.wikipedia.org/wiki/Muine "wikipedia:Muine")** — A music player written in C Sharp.

	[https://muine.gooeylinux.org/](https://muine.gooeylinux.org/) || [muine](https://aur.archlinux.org/packages/muine/)

*   **Pantheon Music** — Simple, fast, and good looking music player. The official elementary music player.

	[https://github.com/elementary/music](https://github.com/elementary/music) || [pantheon-music](https://www.archlinux.org/packages/?name=pantheon-music)

*   **Parlatype** — Minimal audio player for manual speech transcription, for GNOME. It plays audio sources to transcribe them in your favorite text application.

	[https://gkarsay.github.io/parlatype/](https://gkarsay.github.io/parlatype/) || [parlatype](https://aur.archlinux.org/packages/parlatype/)

*   **Pithos** — Python/GTK Pandora Radio desktop client.

	[https://pithos.github.io/](https://pithos.github.io/) || [pithos](https://aur.archlinux.org/packages/pithos/)

*   **Pragha** — GTK music manager. (fork of the Consonance Music Manager)

	[https://pragha-music-player.github.io/](https://pragha-music-player.github.io/) || [pragha](https://www.archlinux.org/packages/?name=pragha)

*   **[Quod Libet](https://en.wikipedia.org/wiki/Quod_Libet_(software) "wikipedia:Quod Libet (software)")** — Audio player written with PyGTK and GStreamer with support for regular expressions in playlists.

	[https://github.com/quodlibet/quodlibet/](https://github.com/quodlibet/quodlibet/) || [quodlibet](https://www.archlinux.org/packages/?name=quodlibet)

*   **Radiotray-NG** — Internet radio player systray applet.

	[https://github.com/ebruck/radiotray-ng](https://github.com/ebruck/radiotray-ng) || [radiotray-ng](https://aur.archlinux.org/packages/radiotray-ng/)

*   **[Rhythmbox](/index.php/Rhythmbox "Rhythmbox")** — GTK clone of iTunes, used by default in GNOME.

	[https://wiki.gnome.org/Apps/Rhythmbox](https://wiki.gnome.org/Apps/Rhythmbox) || [rhythmbox](https://www.archlinux.org/packages/?name=rhythmbox)

*   **Sayonara** — Small, clear and fast audio player for Linux written in C++, uses the Qt framework.

	[https://sayonara-player.com/](https://sayonara-player.com/) || [sayonara-player](https://aur.archlinux.org/packages/sayonara-player/)

*   **Strawberry** — Fork of Clementine aimed at audio enthusiasts and music collectors.

	[https://strawbs.org/](https://strawbs.org/) || [strawberry](https://www.archlinux.org/packages/?name=strawberry)

###### Phonon-based

*   **[Amarok](/index.php/Amarok "Amarok")** — Mature Qt-based player known for its plethora of features.

	[https://amarok.kde.org/](https://amarok.kde.org/) || [amarok](https://aur.archlinux.org/packages/amarok/)

*   **[JuK](https://en.wikipedia.org/wiki/JuK "wikipedia:JuK")** — JuK is an audio jukebox application, supporting collections of MP3, Ogg Vorbis, and FLAC audio files.

	[https://www.kde.org/applications/multimedia/juk/](https://www.kde.org/applications/multimedia/juk/) || [juk](https://www.archlinux.org/packages/?name=juk)

*   **Musique** — Just another music player, only better.

	[https://flavio.tordini.org/musique](https://flavio.tordini.org/musique) || [musique](https://aur.archlinux.org/packages/musique/)

*   **[Tomahawk](https://en.wikipedia.org/wiki/Tomahawk_(software) "wikipedia:Tomahawk (software)")** — Not actively developed anymore. Music player application written in C++/Qt. It decouples the name of the song from the source it was shared from - and fulfills the request using all of your available sources.

	[https://www.tomahawk-player.org/](https://www.tomahawk-player.org/) || [tomahawk](https://aur.archlinux.org/packages/tomahawk/)

*   **Yarock** — Modern looking music player, packed with features, that doesn’t depend on any specific desktop environment. Yarock is designed to provide an easy and pretty music browser based on cover art.

	[https://seb-apps.github.io/yarock/](https://seb-apps.github.io/yarock/) || [yarock-qt5](https://aur.archlinux.org/packages/yarock-qt5/)

###### Qt Multimedia-based

*   **Babe** — Tiny Qt music player to keep your favorite songs at hand.

	[https://milohr.github.io/BabeIt/](https://milohr.github.io/BabeIt/) || [babe](https://www.archlinux.org/packages/?name=babe)

*   **Deepin Music** — Awesome music player with brilliant and tweakful UI Deepin-UI based.

	[https://www.deepin.org/en/original/deepin-music/](https://www.deepin.org/en/original/deepin-music/) || [deepin-music](https://www.archlinux.org/packages/?name=deepin-music)

*   **Elisa** — Simple music player by the KDE community aiming to provide a nice experience for its users.

	[https://community.kde.org/Elisa](https://community.kde.org/Elisa) || [elisa](https://www.archlinux.org/packages/?name=elisa)

###### Other

*   **[Aqualung](https://en.wikipedia.org/wiki/Aqualung_(software) "wikipedia:Aqualung (software)")** — Advanced music player, which plays audio CDs, internet radio streams and podcasts as well as soundfiles in just about any audio format and has the feature of inserting no gaps between adjacent tracks.

	[https://aqualung.jeremyevans.net/](https://aqualung.jeremyevans.net/) || [aqualung](https://aur.archlinux.org/packages/aqualung/)

*   **ArchSimian** — Graphical Qt-based playlist creator that mines data from the user's MediaMonkey database.

	[https://github.com/Harpo3/archsimian](https://github.com/Harpo3/archsimian) || [archsimian-git](https://aur.archlinux.org/packages/archsimian-git/)

*   **[Audacious](/index.php/Audacious "Audacious")** — [Winamp](https://en.wikipedia.org/wiki/Winamp "wikipedia:Winamp") clone like Beep and old XMMS versions.

	[https://audacious-media-player.org/](https://audacious-media-player.org/) || [audacious](https://www.archlinux.org/packages/?name=audacious)

*   **[DeaDBeeF](https://en.wikipedia.org/wiki/DeaDBeeF "wikipedia:DeaDBeeF")** — Light and fast music player with many features, no GNOME or KDE dependencies, supports console-only, as well as a GTK GUI, comes with many plugins, and has a metadata editor.

	[https://deadbeef.sourceforge.io/](https://deadbeef.sourceforge.io/) || [deadbeef](https://www.archlinux.org/packages/?name=deadbeef)

*   **gmusicbrowser** — Open-source jukebox for large collections of MP3/OGG/FLAC files.

	[https://gmusicbrowser.org/](https://gmusicbrowser.org/) || [gmusicbrowser](https://aur.archlinux.org/packages/gmusicbrowser/)

*   **Goggles Music Manager** — Music collection manager and player that automatically categorizes your music, supports gapless playback, features easy tag editing, and internet radio support. Uses the [Fox toolkit](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit").

	[https://gogglesmm.github.io/](https://gogglesmm.github.io/) || [gogglesmm](https://www.archlinux.org/packages/?name=gogglesmm)

*   **Google Play Music Desktop Player** — Beautiful cross platform desktop player for Google Play Music. Based on the [Electron](https://electronjs.org/) platform.

	[https://googleplaymusicdesktopplayer.com/](https://googleplaymusicdesktopplayer.com/) || [gpmdp](https://aur.archlinux.org/packages/gpmdp/)

*   **LXMusic** — A minimalist xmms2-based music player.

	[https://wiki.lxde.org/en/LXMusic](https://wiki.lxde.org/en/LXMusic) || GTK 2: [lxmusic](https://www.archlinux.org/packages/?name=lxmusic), GTK 3: [lxmusic-gtk3](https://www.archlinux.org/packages/?name=lxmusic-gtk3)

*   **museeks** — Minimalistic and easy to use music player. Based on the [Electron](https://electronjs.org/) platform.

	[https://museeks.io/](https://museeks.io/) || [museeks-bin](https://aur.archlinux.org/packages/museeks-bin/)

*   **Noson** — Fast and smart controller for SONOS devices.

	[https://janbar.github.io/noson-app/](https://janbar.github.io/noson-app/) || [noson-app](https://aur.archlinux.org/packages/noson-app/)

*   **Nuclear** — Modern music player focused on streaming from free sources. Based on the [Electron](https://electronjs.org/) platform.

	[https://nuclear.gumblert.tech/](https://nuclear.gumblert.tech/) || [nuclear-player](https://aur.archlinux.org/packages/nuclear-player/)

*   **Nuvola Player** — Integrated Google Music, 8tracks and Hype Machine player.

	[https://tiliado.eu/nuvolaplayer/](https://tiliado.eu/nuvolaplayer/) || [nuvolaplayer-git](https://aur.archlinux.org/packages/nuvolaplayer-git/)

*   **[Qmmp](https://en.wikipedia.org/wiki/qmmp "wikipedia:qmmp")** — Qt-based multimedia player with a user interface that is similar to Winamp or XMMS.

	[http://qmmp.ylsoftware.com/](http://qmmp.ylsoftware.com/) || [qmmp](https://www.archlinux.org/packages/?name=qmmp)

*   **SpotCommander** — A remote control for Spotify, optimized for mobile devices. It works on any device with a modern browser, and it's free and open source.

	[https://olejon.github.io/spotcommander/](https://olejon.github.io/spotcommander/) || [spotcommander](https://aur.archlinux.org/packages/spotcommander/)

*   **[Spotify](/index.php/Spotify "Spotify")** — Proprietary music streaming service. It supports local playback and streaming from Spotify's vast library (requires a free account).

	[https://www.spotify.com/](https://www.spotify.com/) || [spotify](https://aur.archlinux.org/packages/spotify/)

*   **Upplay** — Qt-based UPnP audio control point.

	[https://lesbonscomptes.com/upplay/](https://lesbonscomptes.com/upplay/) || [upplay](https://aur.archlinux.org/packages/upplay/)

#### Audio tag editors

##### Console

*   **[Beets](/index.php/Beets "Beets")** — Music library organizer, tagger and more.

	[http://beets.io/](http://beets.io/) || [beets](https://www.archlinux.org/packages/?name=beets)

*   **Demlo** — Batch music tagger, encoder, renamer and more.

	[https://ambrevar.bitbucket.io/demlo/](https://ambrevar.bitbucket.io/demlo/) || [demlo](https://aur.archlinux.org/packages/demlo/)

*   **id3** — Command-line utility to edit ID3 1.x and 2.x tags.

	[https://squell.github.io/id3/](https://squell.github.io/id3/) || [id3](https://aur.archlinux.org/packages/id3/)

*   **id3ted** — Command line id3 tag editor.

	[https://muennich.github.io/id3ted/](https://muennich.github.io/id3ted/) || [id3ted](https://aur.archlinux.org/packages/id3ted/)

*   **id3v2** — Command line editor for id3v2 tags.

	[http://id3v2.sourceforge.net/](http://id3v2.sourceforge.net/) || [id3v2](https://www.archlinux.org/packages/?name=id3v2)

*   **MP3Info** — MP3 technical info viewer and ID3 1.x tag editor.

	[https://ibiblio.org/mp3info/](https://ibiblio.org/mp3info/) || [mp3info](https://www.archlinux.org/packages/?name=mp3info)

*   **MP3Unicode** — Command line utility to convert ID3 tags in mp3 files between different encodings.

	[http://mp3unicode.sourceforge.net/](http://mp3unicode.sourceforge.net/) || [mp3unicode](https://www.archlinux.org/packages/?name=mp3unicode)

*   **Taffy** — Simple command-line tag editor for many audio formats.

	[https://github.com/jangler/taffy](https://github.com/jangler/taffy) || [taffy](https://aur.archlinux.org/packages/taffy/)

*   **Tagutil** — CLI tool to edit music file's tag. It aims to provide both an easy-to-script interface and ease of use interactively.

	[https://github.com/kAworu/tagutil](https://github.com/kAworu/tagutil) || [tagutil](https://aur.archlinux.org/packages/tagutil/)

##### Graphical

*   **Audio Tag Tool** — Tool to edit tags in MP3 and Ogg Vorbis files.

	[https://github.com/impegoraro/tagtool](https://github.com/impegoraro/tagtool) || [tagtool](https://aur.archlinux.org/packages/tagtool/)

*   **Coquillo** — Metadata editor for various audio formats.

	[https://github.com/sjuvonen/coquillo](https://github.com/sjuvonen/coquillo) || [coquillo](https://aur.archlinux.org/packages/coquillo/)

*   **[EasyTag](https://en.wikipedia.org/wiki/EasyTag "wikipedia:EasyTag")** — Utility for viewing, editing and writing ID3 tags of music files, supports many audio formats.

	[https://wiki.gnome.org/Apps/EasyTAG](https://wiki.gnome.org/Apps/EasyTAG) || [easytag](https://www.archlinux.org/packages/?name=easytag)

*   **[Ex Falso](https://en.wikipedia.org/wiki/Ex_Falso_(software) "wikipedia:Ex Falso (software)")** — Cross-platform free and open source audio tag editor and library organizer. Run with `exfalso`.

	[https://github.com/quodlibet/quodlibet/](https://github.com/quodlibet/quodlibet/) || [quodlibet](https://www.archlinux.org/packages/?name=quodlibet)

*   **Kid3** — MP3, Ogg/Vorbis, FLAC, MPC, MP4/AAC, MP2, Speex, TrueAudio, WavPack, WMA, WAV and AIFF files tag editor.

	[https://kid3.sourceforge.io/](https://kid3.sourceforge.io/) || KDE: [kid3](https://www.archlinux.org/packages/?name=kid3), Qt: [kid3-qt](https://www.archlinux.org/packages/?name=kid3-qt)

*   **KTag Editor** — ID3v tag editor developed in Qt5 framework. Supported files are mp3, wav, ogg, wma, flac, asf.

	[http://karoljkocmaros.blogspot.com/p/ktag-editor.html](http://karoljkocmaros.blogspot.com/p/ktag-editor.html) || [ktageditor](https://aur.archlinux.org/packages/ktageditor/)

*   **MP3Info GUI** — MP3 technical info viewer and ID3 1.x tag editor. The graphical interface can be launched with the `gmp3info` command.

	[https://ibiblio.org/mp3info/](https://ibiblio.org/mp3info/) || [mp3info](https://www.archlinux.org/packages/?name=mp3info)

*   **[Picard](https://en.wikipedia.org/wiki/MusicBrainz_Picard "wikipedia:MusicBrainz Picard")** — Cross-platform audio tag editor written in Python (the official [MusicBrainz](https://en.wikipedia.org/wiki/MusicBrainz "wikipedia:MusicBrainz") tagger).

	[https://picard.musicbrainz.org/](https://picard.musicbrainz.org/) || [picard](https://www.archlinux.org/packages/?name=picard)

*   **[Puddletag](https://en.wikipedia.org/wiki/Puddletag "wikipedia:Puddletag")** — Replacement for the famous MP3tag for Windows.

	[http://docs.puddletag.net/](http://docs.puddletag.net/) || [puddletag](https://aur.archlinux.org/packages/puddletag/)

*   **Qoobar** — Universal Qt-based audio tagger (specialized for classical music).

	[http://qoobar.sourceforge.net/en/index.htm](http://qoobar.sourceforge.net/en/index.htm) || [qoobar](https://aur.archlinux.org/packages/qoobar/)

*   **Tag Editor** — A tag editor with Qt GUI and command-line interface supporting MP4/M4A/AAC (iTunes), ID3v1/ID3v2, Vorbis, Opus, FLAC and Matroska.

	[https://github.com/Martchus/tageditor](https://github.com/Martchus/tageditor) || [tageditor](https://aur.archlinux.org/packages/tageditor/)

*   **Thunar Media Tags Plugin** — Adds special features for media files to the Thunar File Manager, including the ability to edit tags.

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin](https://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) || [thunar-media-tags-plugin](https://www.archlinux.org/packages/?name=thunar-media-tags-plugin)

#### Lyrics

*   **clyrics** — Extensible lyrics fetcher, with daemon support for cmus and mocp.

	[https://github.com/trizen/clyrics](https://github.com/trizen/clyrics) || [clyrics](https://aur.archlinux.org/packages/clyrics/)

*   **LyricsX** — Lyrics editor.

	[https://github.com/timxx/lyricsx](https://github.com/timxx/lyricsx) || [lyricsx](https://aur.archlinux.org/packages/lyricsx/)

*   **OSD Lyrics** — Lyric show compatible with various media players.

	[https://github.com/osdlyrics/osdlyrics](https://github.com/osdlyrics/osdlyrics) || [osdlyrics](https://www.archlinux.org/packages/?name=osdlyrics)

#### Audio converters

*   **[Ecasound](https://en.wikipedia.org/wiki/Ecasound "wikipedia:Ecasound")** — Command line tools designed for multitrack audio processing. It can be used for simple tasks like audio playback, recording and format conversions, as well as for multitrack effect processing, mixing, recording and signal recycling.

	[https://nosignal.fi/ecasound/](https://nosignal.fi/ecasound/) || [ecasound](https://www.archlinux.org/packages/?name=ecasound)

*   **[free:ac](https://en.wikipedia.org/wiki/Fre:ac "wikipedia:Fre:ac")** — Audio converter and CD ripper with support for various popular formats and encoders.

	[https://freac.org/](https://freac.org/) || [freac](https://aur.archlinux.org/packages/freac/)

*   **Gnac** — Audio converter for GNOME.

	[http://gnac.sourceforge.net/](http://gnac.sourceforge.net/) || [gnac](https://www.archlinux.org/packages/?name=gnac)

*   **SoundConverter** — A graphical application to convert audio files into different formats.

	[https://soundconverter.org/](https://soundconverter.org/) || [soundconverter](https://www.archlinux.org/packages/?name=soundconverter)

*   **soundKonverter** — Qt-based GUI front-end to various audio converters.

	[https://github.com/dfaust/soundkonverter](https://github.com/dfaust/soundkonverter) || [soundkonverter](https://www.archlinux.org/packages/?name=soundkonverter)

*   **[SoX](https://en.wikipedia.org/wiki/SoX "wikipedia:SoX")** — Command line utility that can convert various formats of computer audio files into other formats.

	[http://sox.sourceforge.net/](http://sox.sourceforge.net/) || [sox](https://www.archlinux.org/packages/?name=sox)

*   **XCFA** — Tool to extract the content of audio CDs and convert files to various formats.

	[http://www.xcfa.tuxfamily.org/](http://www.xcfa.tuxfamily.org/) || [xcfa](https://aur.archlinux.org/packages/xcfa/)

#### Audio editors

See also [Wikipedia:Comparison of digital audio editors](https://en.wikipedia.org/wiki/Comparison_of_digital_audio_editors "wikipedia:Comparison of digital audio editors").

*   **[Audacity](https://en.wikipedia.org/wiki/Audacity_(audio_editor) "wikipedia:Audacity (audio editor)")** — Program that lets you manipulate digital audio waveforms.

	[https://www.audacityteam.org/](https://www.audacityteam.org/) || [audacity](https://www.archlinux.org/packages/?name=audacity)

*   **Deepin Voice Recorder** — Voice recorder application for Deepin desktop.

	[https://www.deepin.org/en/original/deepin-voice-recorder/](https://www.deepin.org/en/original/deepin-voice-recorder/) || [deepin-voice-recorder](https://www.archlinux.org/packages/?name=deepin-voice-recorder)

*   **GNOME Sound Recorder** — The Sound Recorder application enables you to record and play .flac, .ogg (OGG audio, or .oga), and .wav sound files.

	[https://wiki.gnome.org/Apps/SoundRecorder](https://wiki.gnome.org/Apps/SoundRecorder) || [gnome-sound-recorder](https://www.archlinux.org/packages/?name=gnome-sound-recorder)

*   **[Gnome Wave Cleaner](https://en.wikipedia.org/wiki/Gnome_Wave_Cleaner "wikipedia:Gnome Wave Cleaner")** — Digital audio editor to denoise, dehiss and amplify audio files.

	[http://gwc.sourceforge.net/](http://gwc.sourceforge.net/) || [gwc](https://aur.archlinux.org/packages/gwc/)

*   **Kwave** — Sound editor for KDE.

	[http://kwave.sourceforge.net/](http://kwave.sourceforge.net/) || [kwave](https://www.archlinux.org/packages/?name=kwave)

*   **mhWaveEdit** — Graphical program for editing, playing and recording sound files.

	[https://github.com/magnush/mhwaveedit/](https://github.com/magnush/mhwaveedit/) || [mhwaveedit](https://aur.archlinux.org/packages/mhwaveedit/)

*   **[Mp3splt](https://en.wikipedia.org/wiki/Mp3splt "wikipedia:Mp3splt")** — Utility to split mp3, ogg vorbis and native FLAC files selecting a begin and an end time position, without decoding.

	[http://mp3splt.sourceforge.net/](http://mp3splt.sourceforge.net/) || CLI: [mp3splt](https://www.archlinux.org/packages/?name=mp3splt), GUI: [mp3splt-gtk](https://www.archlinux.org/packages/?name=mp3splt-gtk)

*   **ocenaudio** — Proprietary cross-platform, easy to use, fast and functional audio editor.

	[https://www.ocenaudio.com/en/](https://www.ocenaudio.com/en/) || [ocenaudio-bin](https://aur.archlinux.org/packages/ocenaudio-bin/) or [ocenaudio](https://aur.archlinux.org/packages/ocenaudio/)

*   **Play it Slowly** — Play back audio files at a different speed or pitch.

	[https://29a.ch/playitslowly](https://29a.ch/playitslowly) || [playitslowly](https://aur.archlinux.org/packages/playitslowly/)

*   **[Sweep](https://en.wikipedia.org/wiki/Sweep_(software) "wikipedia:Sweep (software)")** — Audio editor and live playback tool.

	[http://www.metadecks.org/software/sweep/](http://www.metadecks.org/software/sweep/) || [sweep](https://www.archlinux.org/packages/?name=sweep)

*   **[WaveSurfer](https://en.wikipedia.org/wiki/WaveSurfer "wikipedia:WaveSurfer")** — Tool for sound visualization and manipulation. Typical applications are speech/sound analysis and sound annotation/transcription.

	[https://www.speech.kth.se/wavesurfer/](https://www.speech.kth.se/wavesurfer/) || [wavesurfer](https://aur.archlinux.org/packages/wavesurfer/)

#### Digital audio workstations

See also [Professional audio](/index.php/Professional_audio "Professional audio").

*   **[Ardour](https://en.wikipedia.org/wiki/Ardour_(software) "wikipedia:Ardour (software)")** — Multichannel hard disk recorder and digital audio workstation.

	[http://ardour.org/](http://ardour.org/) || [ardour](https://www.archlinux.org/packages/?name=ardour)

*   **Bitwig Studio** — Proprietary professional digital audio workstation.

	[https://www.bitwig.com/](https://www.bitwig.com/) || [bitwig-studio](https://aur.archlinux.org/packages/bitwig-studio/)

*   **Frinika** — Digital audio workstation, features sequencer, soft-synths, realtime effects and audio recording.

	[http://www.frinika.com/](http://www.frinika.com/) || [frinika](https://aur.archlinux.org/packages/frinika/)

*   **[LMMS](/index.php/LMMS "LMMS")** — Digital audio workstation which allows you to produce music with your computer.

	[https://lmms.io/](https://lmms.io/) || [lmms](https://www.archlinux.org/packages/?name=lmms)

*   **[MusE](https://en.wikipedia.org/wiki/MusE "wikipedia:MusE")** — MIDI/Audio sequencer (digital audio workstation) with recording and editing capabilities, aims to be a complete multitrack virtual studio for Linux.

	[http://muse-sequencer.org/](http://muse-sequencer.org/) || [muse](https://aur.archlinux.org/packages/muse/)

*   **Non** — Modular digital audio workstation composed of four main parts: Timeline, Mixer, Sequencer and Session Manager.

	[http://non.tuxfamily.org/](http://non.tuxfamily.org/) || [non-daw](https://www.archlinux.org/groups/x86_64/non-daw/)

*   **[Qtractor](https://en.wikipedia.org/wiki/Qtractor "wikipedia:Qtractor")** — Qt-based hard disk recorder and digital audio workstation application that aims to provide digital audio workstation software simple enough for the average home user, and yet powerful enough for the professional user.

	[https://qtractor.sourceforge.io/qtractor-index.html](https://qtractor.sourceforge.io/qtractor-index.html) || [qtractor](https://www.archlinux.org/packages/?name=qtractor)

*   **[REAPER](https://en.wikipedia.org/wiki/REAPER "wikipedia:REAPER")** — Proprietary digital audio workstation, offering a full multitrack audio and MIDI recording, editing, processing, mixing and mastering toolset.

	[https://www.reaper.fm/](https://www.reaper.fm/) || [reaper-bin](https://aur.archlinux.org/packages/reaper-bin/)

*   **[Rosegarden](https://en.wikipedia.org/wiki/Rosegarden "wikipedia:Rosegarden")** — Digital audio workstation program developed with ALSA and Qt that acts as an audio and MIDI sequencer, scorewriter and musical composition and editing tool.

	[https://www.rosegardenmusic.com/](https://www.rosegardenmusic.com/) || [rosegarden](https://www.archlinux.org/packages/?name=rosegarden)

*   **[Tracktion](https://en.wikipedia.org/wiki/Tracktion "wikipedia:Tracktion")** — Proprietary digital audio workstation, specifically designed for the needs of modern music producers.

	[https://www.tracktion.com/](https://www.tracktion.com/) || [tracktion-waveform](https://aur.archlinux.org/packages/tracktion-waveform/)

*   **[Traverso](https://en.wikipedia.org/wiki/Traverso_DAW "wikipedia:Traverso DAW")** — Multitrack audio recorder and editor with a very clean and intuitive interface which supports ALSA and Jack as the sound driver.

	[https://traverso-daw.org/](https://traverso-daw.org/) || [traverso](https://aur.archlinux.org/packages/traverso/)

#### Audio analyzers

*   **audioprism** — Spectrogram tool for PulseAudio input and WAV files.

	[https://github.com/vsergeev/audioprism](https://github.com/vsergeev/audioprism) || [audioprism](https://aur.archlinux.org/packages/audioprism/)

*   **[BRP-PACU](https://en.wikipedia.org/wiki/BRP-PACU "wikipedia:BRP-PACU")** — Dual channel FFT based acoustic analysis tool to help engineers analyze live professional sound systems using the transfer function.

	[https://sourceforge.net/projects/brp-pacu/](https://sourceforge.net/projects/brp-pacu/) || [brp-pacu](https://aur.archlinux.org/packages/brp-pacu/)

*   **Baudline** — Time-frequency and spectrogram analyzer

	[http://www.baudline.com/index.html](http://www.baudline.com/index.html) || [baudline-bin](https://aur.archlinux.org/packages/baudline-bin/)

*   **FMIT** — Graphical utility for tuning your musical instruments, with error and volume history and advanced features.

	[http://gillesdegottex.github.io/fmit/](http://gillesdegottex.github.io/fmit/) || [fmit](https://aur.archlinux.org/packages/fmit/)

*   **Friture** — Real-time audio analyzer.

	[http://friture.org/](http://friture.org/) || [friture](https://aur.archlinux.org/packages/friture/)

*   **rtspeccy** — Real time audio spectrum analyzer.

	[https://www.uninformativ.de/projects/rtspeccy/](https://www.uninformativ.de/projects/rtspeccy/) || [rtspeccy-git](https://aur.archlinux.org/packages/rtspeccy-git/)

*   **sndpeek** — Real-time audio visualization tool.

	[https://soundlab.cs.princeton.edu/software/sndpeek/](https://soundlab.cs.princeton.edu/software/sndpeek/) || ALSA: [sndpeek-alsa](https://aur.archlinux.org/packages/sndpeek-alsa/), JACK: [sndpeek-jack](https://aur.archlinux.org/packages/sndpeek-jack/)

*   **[Sonic Visualiser](https://en.wikipedia.org/wiki/Sonic_Visualiser "wikipedia:Sonic Visualiser")** — Viewing and analyzing the contents of music audio files.

	[https://www.sonicvisualiser.org/](https://www.sonicvisualiser.org/) || [sonic-visualiser](https://www.archlinux.org/packages/?name=sonic-visualiser)

*   **Spectrum3d** — Displays a 3D audio spectrogram in real time from the microphone or an audio file.

	[http://spectrum3d.sourceforge.net/](http://spectrum3d.sourceforge.net/) || [spectrum3d](https://aur.archlinux.org/packages/spectrum3d/)

*   **Spek** — Helps to analyse your audio files by showing their spectrogram.

	[http://spek.cc/](http://spek.cc/) || [spek](https://aur.archlinux.org/packages/spek/)

#### Scorewriters

See also [LilyPond#Front-ends](/index.php/LilyPond#Front-ends "LilyPond") and [Wikipedia:Comparison of scorewriters](https://en.wikipedia.org/wiki/Comparison_of_scorewriters "wikipedia:Comparison of scorewriters").

*   **[Aria Maestosa](https://en.wikipedia.org/wiki/Aria_Maestosa "wikipedia:Aria Maestosa")** — MIDI sequencer/editor. It lets you compose, edit and play MIDI files with a few clicks in a user-friendly interface offering score, keyboard, guitar, drum and controller views.

	[http://ariamaestosa.sourceforge.net/](http://ariamaestosa.sourceforge.net/) || [ariamaestosa](https://aur.archlinux.org/packages/ariamaestosa/)

*   **[Canorus](https://en.wikipedia.org/wiki/Canorus "wikipedia:Canorus")** — Music score editor. It supports an unlimited number and length of staffs, polyphony, a MIDI playback of notes, chord markings, lyrics, import/export filters to formats like MIDI, MusicXML, ABC Music, MusiXTeX and LilyPond.

	[https://sourceforge.net/projects/canorus/](https://sourceforge.net/projects/canorus/) || [canorus](https://www.archlinux.org/packages/?name=canorus)

*   **[GNU Denemo](https://en.wikipedia.org/wiki/Denemo "wikipedia:Denemo")** — Denemo is a free music notation program for GNU/Linux, Mac OSX and Windows that lets you rapidly enter notation which it typesets using the [LilyPond](/index.php/LilyPond "LilyPond") music engraver. Music can be typed in at the PC-Keyboard [(watch demo)](https://vimeo.com/65174334), or played in via MIDI controller [(watch demo)](https://vimeo.com/61994482), or input acoustically into a microphone plugged into your computer's soundcard.

	[http://www.denemo.org/](http://www.denemo.org/) || [denemo](https://aur.archlinux.org/packages/denemo/)

*   **[Impro-Visor](https://en.wikipedia.org/wiki/Impro-Visor "wikipedia:Impro-Visor")** — Music notation program designed to help jazz musicians compose and hear solos similar to ones that might be improvised.

	[https://www.cs.hmc.edu/~keller/jazz/improvisor/](https://www.cs.hmc.edu/~keller/jazz/improvisor/) || [impro-visor](https://aur.archlinux.org/packages/impro-visor/)

*   **[LilyPond](/index.php/LilyPond "LilyPond")** — Music engraving program, devoted to producing the highest-quality sheet music possible.

	[http://lilypond.org/](http://lilypond.org/) || [lilypond](https://www.archlinux.org/packages/?name=lilypond)

*   **[MuseScore](https://en.wikipedia.org/wiki/MuseScore "wikipedia:MuseScore")** — Create, playback, and print sheet music.

	[https://musescore.org/](https://musescore.org/) || [musescore](https://www.archlinux.org/packages/?name=musescore)

*   **[TuxGuitar](https://en.wikipedia.org/wiki/TuxGuitar "wikipedia:TuxGuitar")** — Multitrack guitar tablature editor and player.

	[http://tuxguitar.com.ar/](http://tuxguitar.com.ar/) || [tuxguitar](https://aur.archlinux.org/packages/tuxguitar/)

#### Audio synthesis environments

See also [Wikipedia:Comparison of audio synthesis environments](https://en.wikipedia.org/wiki/Comparison_of_audio_synthesis_environments "wikipedia:Comparison of audio synthesis environments").

*   **Blue** — Music composition environment for Csound, written in Java.

	[https://blue.kunstmusik.com/](https://blue.kunstmusik.com/) || [csound-blue](https://aur.archlinux.org/packages/csound-blue/)

*   **Cabbage** — Framework for audio software development using simple markup text and the Csound audio synthesis language.

	[https://cabbageaudio.com/](https://cabbageaudio.com/) || [cabbage](https://aur.archlinux.org/packages/cabbage/)

*   **[ChucK](https://en.wikipedia.org/wiki/ChucK "wikipedia:ChucK")** — Strongly-timed, concurrent, and on-the-fly music programming language.

	[https://chuck.cs.princeton.edu/](https://chuck.cs.princeton.edu/) || [chuck](https://www.archlinux.org/packages/?name=chuck)

*   **[Csound](https://en.wikipedia.org/wiki/Csound "wikipedia:Csound")** — Sound and music computing system.

	[https://csound.com/](https://csound.com/) || [csound](https://www.archlinux.org/packages/?name=csound)

*   **CsoundQt** — Frontend for Csound featuring a highlighting editor with autocomplete, interactive widgets and integrated help.

	[https://csoundqt.github.io/](https://csoundqt.github.io/) || [csoundqt](https://www.archlinux.org/packages/?name=csoundqt)

*   **[Pure Data](https://en.wikipedia.org/wiki/Pure_Data "wikipedia:Pure Data")** — Real-time music and multimedia environment.

	[http://msp.ucsd.edu/software.html](http://msp.ucsd.edu/software.html) || [pd](https://www.archlinux.org/packages/?name=pd)

*   **[SuperCollider](https://en.wikipedia.org/wiki/SuperCollider "wikipedia:SuperCollider")** — Platform for audio synthesis and algorithmic composition, used by musicians, artists, and researchers working with sound.

	[https://supercollider.github.io/](https://supercollider.github.io/) || [supercollider](https://www.archlinux.org/packages/?name=supercollider)

#### Sound generators

This section contains [drum machines](https://en.wikipedia.org/wiki/Drum_machine "wikipedia:Drum machine"), [software samplers](https://en.wikipedia.org/wiki/Software_sampler "wikipedia:Software sampler") and [software synthesizers](https://en.wikipedia.org/wiki/Software_synthesizer "wikipedia:Software synthesizer").

*   **ams** — Alsa Modular Synth. Realtime modular synthesizer and effect processor.

	[http://alsamodular.sourceforge.net/](http://alsamodular.sourceforge.net/) || [ams](https://www.archlinux.org/packages/?name=ams)

*   **[amsynth](https://en.wikipedia.org/wiki/Amsynth "wikipedia:Amsynth")** — Analog Modelling SYNTHesizer. Easy-to-use software synthesizer with a classic subtractive synthesizer topology.

	[https://amsynth.github.io/](https://amsynth.github.io/) || [amsynth](https://www.archlinux.org/packages/?name=amsynth)

*   **[DIN](https://en.wikipedia.org/wiki/Din_(din_is_noise) "wikipedia:Din (din is noise)")** — Sound synthesizer and musical instrument.

	[https://dinisnoise.org/](https://dinisnoise.org/) || [din](https://www.archlinux.org/packages/?name=din)

*   **Drumstick** — Set of MIDI tools: drum grid, MIDI player, virtual piano.

	[http://drumstick.sourceforge.net/](http://drumstick.sourceforge.net/) || [drumstick](https://www.archlinux.org/packages/?name=drumstick)

*   **[FluidSynth](/index.php/FluidSynth "FluidSynth")** — Real-time software synthesizer based on the SoundFont 2 specifications.

	[http://www.fluidsynth.org/](http://www.fluidsynth.org/) || [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth)

*   **Gigedit** — Graphical instrument editor for sample based virtual instruments, based on the GigaStudio/Gigasampler file format.

	[http://doc.linuxsampler.org/Gigedit/](http://doc.linuxsampler.org/Gigedit/) || [gigedit](https://www.archlinux.org/packages/?name=gigedit)

*   **Helm** — Software synthesizer to create electronic music on your computer.

	[https://tytel.org/helm/](https://tytel.org/helm/) || [helm](https://www.archlinux.org/packages/?name=helm)

*   **[Hydrogen](https://en.wikipedia.org/wiki/Hydrogen_(software) "wikipedia:Hydrogen (software)")** — Advanced drum machine to create drum sequences.

	[https://github.com/hydrogen-music/hydrogen](https://github.com/hydrogen-music/hydrogen) || [hydrogen](https://www.archlinux.org/packages/?name=hydrogen)

*   **JSampler** — Java GUI for [LinuxSampler](/index.php/LinuxSampler "LinuxSampler") software audio sampler.

	[http://jsampler.sourceforge.net/](http://jsampler.sourceforge.net/) || [jsampler](https://www.archlinux.org/packages/?name=jsampler)

*   **[PySynth](https://en.wikipedia.org/wiki/PySynth "wikipedia:PySynth")** — Suite of simple music synthesizers and helper scripts written in Python 3.

	[https://mdoege.github.io/PySynth/](https://mdoege.github.io/PySynth/) || [python-pysynth-git](https://aur.archlinux.org/packages/python-pysynth-git/)

*   **QMidiArp** — Advanced MIDI arpeggiator, programmable step sequencer and LFO.

	[http://qmidiarp.sourceforge.net/](http://qmidiarp.sourceforge.net/) || [qmidiarp](https://www.archlinux.org/packages/?name=qmidiarp)

*   **QMidiRoute** — MIDI router and processor for ALSA.

	[http://alsamodular.sourceforge.net/](http://alsamodular.sourceforge.net/) || [qmidiroute](https://www.archlinux.org/packages/?name=qmidiroute)

*   **Qsampler** — Qt GUI for [LinuxSampler](/index.php/LinuxSampler "LinuxSampler") software audio sampler.

	[https://qsampler.sourceforge.io/](https://qsampler.sourceforge.io/) || [qsampler](https://www.archlinux.org/packages/?name=qsampler)

*   **Qsynth** — Qt GUI for Fluidsynth.

	[https://qsynth.sourceforge.io/](https://qsynth.sourceforge.io/) || [qsynth](https://www.archlinux.org/packages/?name=qsynth)

*   **[TiMidity++](/index.php/Timidity "Timidity")** — Software synthesizer, which can play MIDI files by converting them into PCM waveform data.

	[http://timidity.sourceforge.net/](http://timidity.sourceforge.net/) || [timidity++](https://www.archlinux.org/packages/?name=timidity%2B%2B)

*   **Vee One Suite** — Old-school software instruments: synthv1, a polyphonic subtractive synthesizer; samplv1, a polyphonic sampler synthesizer; drumkv1, yet another drum-kit sampler; padthv1, a polyphonic additive synthesizer.

	[https://www.rncbc.org/](https://www.rncbc.org/) || [vee-one](https://www.archlinux.org/groups/x86_64/vee-one/)

*   **VMPK** — Virtual MIDI Piano Keyboard. MIDI events generator and receiver. It doesn't produce any sound by itself, but can be used to drive a MIDI synthesizer.

	[http://vmpk.sourceforge.net/](http://vmpk.sourceforge.net/) || [vmpk](https://www.archlinux.org/packages/?name=vmpk)

*   **[Yoshimi](https://en.wikipedia.org/wiki/Yoshimi_(synthesizer) "wikipedia:Yoshimi (synthesizer)")** — Software synthesizer, a fork of ZynAddSubFX.

	[http://yoshimi.sourceforge.net/](http://yoshimi.sourceforge.net/) || [yoshimi](https://www.archlinux.org/packages/?name=yoshimi)

*   **[ZynAddSubFX](https://en.wikipedia.org/wiki/ZynAddSubFX "wikipedia:ZynAddSubFX")** — Fully featured software synthesizer capable of making a countless number of instruments, from some common heard from expensive hardware to interesting sounds that you'll boost to an amazing universe of sounds.

	[http://zynaddsubfx.sourceforge.net/](http://zynaddsubfx.sourceforge.net/) || [zynaddsubfx](https://www.archlinux.org/packages/?name=zynaddsubfx)

#### Music trackers

*   **[Buzztrax](https://en.wikipedia.org/wiki/Buzztrax "wikipedia:Buzztrax")** — Music studio to compose songs using only a computer with a soundcard.

	[https://news.buzztrax.org/](https://news.buzztrax.org/) || [buzztrax](https://aur.archlinux.org/packages/buzztrax/)

*   **klystrack** — Tracker for making C64/NES/Amiga-style chiptunes on a modern platform.

	[https://kometbomb.github.io/klystrack/](https://kometbomb.github.io/klystrack/) || [klystrack-git](https://aur.archlinux.org/packages/klystrack-git/)

*   **[MilkyTracker](https://en.wikipedia.org/wiki/MilkyTracker "wikipedia:MilkyTracker")** — Music application for creating .MOD and .XM module files.

	[https://milkytracker.titandemo.org/](https://milkytracker.titandemo.org/) || [milkytracker](https://www.archlinux.org/packages/?name=milkytracker)

*   **[OpenMPT](https://en.wikipedia.org/wiki/OpenMPT "wikipedia:OpenMPT")** — Tracker software to create and play back some great music on your computer.

	[https://openmpt.org/](https://openmpt.org/) || [openmpt](https://aur.archlinux.org/packages/openmpt/)

*   **Radium** — Music editor with a new type of interface.

	[https://users.notam02.no/~kjetism/radium/](https://users.notam02.no/~kjetism/radium/) || [radium](https://aur.archlinux.org/packages/radium/)

*   **Schism Tracker** — Create high quality music without the requirements of specialized, expensive equipment, and with a unique "finger feel" that is difficult to replicate in part.

	[http://schismtracker.org/](http://schismtracker.org/) || [schismtracker](https://aur.archlinux.org/packages/schismtracker/)

#### DJ

*   **Giada** — Minimal, hardcore audio tool for DJs, live performers and electronic musicians.

	[https://giadamusic.com/](https://giadamusic.com/) || [giada](https://www.archlinux.org/packages/?name=giada)

*   **IDJC** — Powerful yet easy to use source-client for individuals interested in streaming live radio shows over the Internet using Shoutcast or Icecast servers.

	[http://idjc.sourceforge.net/](http://idjc.sourceforge.net/) || [idjc](https://aur.archlinux.org/packages/idjc/)

*   **Luppp** — Music creation tool, intended for live use. The focus is on real time processing and a fast and intuitive workflow.

	[http://openavproductions.com/luppp/](http://openavproductions.com/luppp/) || [luppp](https://www.archlinux.org/packages/?name=luppp)

*   **[Mixxx](https://en.wikipedia.org/wiki/Mixxx "wikipedia:Mixxx")** — Integrates the tools DJs need to perform creative live mixes with digital music files.

	[https://mixxx.org/](https://mixxx.org/) || [mixxx](https://www.archlinux.org/packages/?name=mixxx)

*   **[Seq24](/index.php/Seq24 "Seq24")** — Minimal loop based MIDI sequencer for a live performance with a very simple interface for editing and playing MIDI 'loops'.

	[http://filter24.org/seq24/](http://filter24.org/seq24/) || [seq24-bzr](https://aur.archlinux.org/packages/seq24-bzr/)

*   **[xwax](https://en.wikipedia.org/wiki/xwax "wikipedia:xwax")** — Digital Vinyl System (DVS) for Linux. It allows DJs and turntablists to playback digital audio files (MP3, Ogg Vorbis, FLAC, AAC and more), controlled using a normal pair of turntables via timecoded vinyls.

	[http://xwax.org/](http://xwax.org/) || [xwax](https://www.archlinux.org/packages/?name=xwax)

#### Audio effects

*   **Calf Plugin Pack for JACK** — Process and produce sounds using a set of plugins with JACK interface. (`calfjackhost`)

	[https://calf-studio-gear.org/](https://calf-studio-gear.org/) || [calf](https://www.archlinux.org/packages/?name=calf)

*   **Carla** — Audio plugin host, with support for many audio drivers and plugin formats.

	[https://kxstudio.linuxaudio.org/Applications:Carla](https://kxstudio.linuxaudio.org/Applications:Carla) || [carla](https://www.archlinux.org/packages/?name=carla)

*   **guitarix** — Virtual guitar amplifier for JACK.

	[https://guitarix.org/](https://guitarix.org/) || [guitarix2](https://www.archlinux.org/packages/?name=guitarix2)

*   **Rakarrack** — Richly featured multi-effects processor emulating a guitar effects pedalboard.

	[http://rakarrack.sourceforge.net/](http://rakarrack.sourceforge.net/) || [rakarrack](https://aur.archlinux.org/packages/rakarrack/)

#### Audio visualizers

*   **C.A.V.A.** — Console-based audio visualizer for ALSA, MPD and PulseAudio.

	[https://karlstav.github.io/cava/](https://karlstav.github.io/cava/) || [cava](https://aur.archlinux.org/packages/cava/)

*   **Cavalcade** — GTK GUI for C.A.V.A.

	[https://github.com/worron/cavalcade/](https://github.com/worron/cavalcade/) || [cavalcade](https://aur.archlinux.org/packages/cavalcade/)

*   **cli-visualizer** — Highly configurable CLI-based audio visualizer.

	[https://github.com/dpayne/cli-visualizer](https://github.com/dpayne/cli-visualizer) || [cli-visualizer](https://aur.archlinux.org/packages/cli-visualizer/)

*   **GLava** — OpenGL audio spectrum visualizer. Its primary use case is for desktop windows or backgrounds.

	[https://github.com/wacossusca34/glava](https://github.com/wacossusca34/glava) || [glava-git](https://aur.archlinux.org/packages/glava-git/)

*   **GLMViz** — Fully configurable OpenGL music visualizer.

	[https://github.com/hannesha/GLMViz](https://github.com/hannesha/GLMViz) || [glmviz-git](https://aur.archlinux.org/packages/glmviz-git/)

*   **[projectM](/index.php/ProjectM "ProjectM")** — Music visualizer which uses 3D accelerated iterative image-based rendering.

	[https://github.com/projectM-visualizer/projectm](https://github.com/projectM-visualizer/projectm) || JACK: [projectm-jack](https://www.archlinux.org/packages/?name=projectm-jack), PulseAudio: [projectm-pulseaudio](https://www.archlinux.org/packages/?name=projectm-pulseaudio)

*   **[VSXu](https://en.wikipedia.org/wiki/VSXu "wikipedia:VSXu")** — OpenGL-based (hardware-accelerated), modular programming environment with its main purpose to visualize music and create graphic effects in real-time.

	[http://www.vsxu.com/](http://www.vsxu.com/) || [vsxu](https://aur.archlinux.org/packages/vsxu/)

#### Volume control

See also [PulseAudio#Front-ends](/index.php/PulseAudio#Front-ends "PulseAudio").

*   **[alsamixer](https://en.wikipedia.org/wiki/alsamixer "wikipedia:alsamixer")** — Soundcard mixer for ALSA soundcard driver, with ncurses interface.

	[https://alsa-project.org/](https://alsa-project.org/) || [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)

*   **ALSA Tray** — Provides a systray icon and a command line interface for setting the volume of the ALSA Mixers.

	[https://projects.flogisoft.com/alsa-tray/](https://projects.flogisoft.com/alsa-tray/) || [alsa-tray](https://aur.archlinux.org/packages/alsa-tray/)

*   **AlsaVolume** — Tray ALSA volume changer written using gtkmm.

	[https://github.com/Vitozz/cppAlsaVolume](https://github.com/Vitozz/cppAlsaVolume) || [cpp-alsa-volume](https://aur.archlinux.org/packages/cpp-alsa-volume/)

*   **AMixST** — Volume wheel using ALSA and Qt5.

	[https://github.com/FenixFyreX/amixst](https://github.com/FenixFyreX/amixst) || [amixst](https://aur.archlinux.org/packages/amixst/)

*   **GNOME ALSA Mixer** — ALSA mixer for GNOME.

	[https://launchpad.net/gnome-alsamixer](https://launchpad.net/gnome-alsamixer) || [gnome-alsamixer](https://aur.archlinux.org/packages/gnome-alsamixer/)

*   **GVolWheel** — Audio mixer which lets you control the volume through a tray icon.

	[https://sourceforge.net/projects/gvolwheel/](https://sourceforge.net/projects/gvolwheel/) || [gvolwheel](https://aur.archlinux.org/packages/gvolwheel/)

*   **KMix** — KDE volume control program.

	[https://kde.org/applications/multimedia/kmix/](https://kde.org/applications/multimedia/kmix/) || [kmix](https://www.archlinux.org/packages/?name=kmix)

*   **MATE Volume Control** — Audio mixer application and system tray applet for MATE to mix audio and adjust volume levels of various audio mixer devices.

	[https://github.com/mate-desktop/mate-media](https://github.com/mate-desktop/mate-media) || [mate-media](https://www.archlinux.org/packages/?name=mate-media)

*   **PNMixer** — A fork of Obmixer. It has many new features such as ALSA channel selection, connect/disconnect detection, shortcuts, etc.

	[https://github.com/nicklan/pnmixer/wiki](https://github.com/nicklan/pnmixer/wiki) || [pnmixer](https://aur.archlinux.org/packages/pnmixer/)

*   **QasTools** — Collection of desktop applications for the Linux sound system ALSA. It provides QasMixer (mixer), QasHctl (HCTL mixer) and QasConfig (configuration browser).

	[http://xwmw.org/qastools/](http://xwmw.org/qastools/) || [qastools](https://www.archlinux.org/packages/?name=qastools)

*   **Retrovol** — Retro-looking volume setting tray applet.

	[https://github.com/pizzasgood/retrovol](https://github.com/pizzasgood/retrovol) || [retrovol](https://aur.archlinux.org/packages/retrovol/)

*   **[Volnoti](/index.php/Volnoti "Volnoti")** — A lightweight volume notification daemon for GNU/Linux and other POSIX operating systems.

	[https://github.com/davidbrazdil/volnoti](https://github.com/davidbrazdil/volnoti) || [volnoti](https://aur.archlinux.org/packages/volnoti/)

*   **Volti** — A GTK application for controlling audio volume from system tray with an internal mixer and support for multimedia keys that uses only ALSA.

	[https://github.com/gen2brain/volti](https://github.com/gen2brain/volti) || [volti](https://aur.archlinux.org/packages/volti/)

*   **Volume Icon** — Another volume control for your system tray with channel selection, themes and an external mixer.

	[http://nullwise.com/volumeicon.html](http://nullwise.com/volumeicon.html) || [volumeicon](https://www.archlinux.org/packages/?name=volumeicon)

*   **VolWheel** — A little application which lets you control the sound volume easily through a tray icon you can scroll on.

	[https://oliwer.net/b/volwheel.html](https://oliwer.net/b/volwheel.html) || [volwheel](https://www.archlinux.org/packages/?name=volwheel)

*   **Xfce ALSA Panel Plugin** — Simple ALSA volume control plugin for [Xfce](/index.php/Xfce "Xfce")4 panel.

	[https://github.com/equeim/xfce4-alsa-plugin](https://github.com/equeim/xfce4-alsa-plugin) || [xfce4-alsa-plugin](https://aur.archlinux.org/packages/xfce4-alsa-plugin/)

#### CD ripping

See [Optical disc drive#Audio CD](/index.php/Optical_disc_drive#Audio_CD "Optical disc drive").

### Video

#### Video players

See also [Wikipedia:Comparison of video player software](https://en.wikipedia.org/wiki/Comparison_of_video_player_software "wikipedia:Comparison of video player software").

##### Console

*   **[FFplay](/index.php/FFmpeg "FFmpeg")** — Very simple and portable media player using the FFmpeg libraries and the SDL library.

	[http://ffmpeg.org/](http://ffmpeg.org/) || [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)

*   **[gst-play-1.0](/index.php/GStreamer "GStreamer")** — Simple command line playback testing tool for GStreamer.

	[https://gstreamer.freedesktop.org/](https://gstreamer.freedesktop.org/) || [gst-plugins-base-libs](https://www.archlinux.org/packages/?name=gst-plugins-base-libs)

*   **[MPlayer](/index.php/MPlayer "MPlayer")** — Video player that supports a complete and versatile array of video and audio formats.

	[http://www.mplayerhq.hu/design7/news.html](http://www.mplayerhq.hu/design7/news.html) || [mplayer](https://www.archlinux.org/packages/?name=mplayer)

*   **[mpv](/index.php/Mpv "Mpv")** — Movie player based on MPlayer and mplayer2.

	[https://mpv.io/](https://mpv.io/) || [mpv](https://www.archlinux.org/packages/?name=mpv)

*   **[VLC media player](/index.php/VLC_media_player "VLC media player")** — Command-line version of the famous video player that can play smoothly high definition videos in the TTY. The rc interface can be launched with `vlc -I rc`, and the ncurses interface can be launched with `vlc -I ncurses`.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

##### Graphical

###### GStreamer-based

*   **GNOME Twitch** — Twitch client for GNOME using [GStreamer](/index.php/GStreamer "GStreamer").

	[http://gnome-twitch.vinszent.com/](http://gnome-twitch.vinszent.com/) || [gnome-twitch](https://www.archlinux.org/packages/?name=gnome-twitch)

*   **[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")** — Media player (audio and video) for the GNOME desktop that uses [GStreamer](/index.php/GStreamer "GStreamer"). Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Apps/Videos](https://wiki.gnome.org/Apps/Videos) || [totem](https://www.archlinux.org/packages/?name=totem)

*   **Movie Monad** — Free and simple to use video player made with Haskell using [GStreamer](/index.php/GStreamer "GStreamer") and GTK. Precompiled and no Haskell dependency in run-time.

	[https://lettier.github.io/movie-monad/](https://lettier.github.io/movie-monad/) || [movie-monad](https://aur.archlinux.org/packages/movie-monad/)

*   **Pantheon Videos** — Video player and library app designed for elementary OS using [GStreamer](/index.php/GStreamer "GStreamer").

	[https://github.com/elementary/videos](https://github.com/elementary/videos) || [pantheon-videos](https://www.archlinux.org/packages/?name=pantheon-videos)

*   **Parole** — Modern media player based on the [GStreamer](/index.php/GStreamer "GStreamer") framework.

	[https://docs.xfce.org/apps/parole/start](https://docs.xfce.org/apps/parole/start) || [parole](https://www.archlinux.org/packages/?name=parole)

*   **Rage** — Video and audio player written with Enlightenment Foundation Libraries with some extra bells and whistles. Uses [GStreamer](/index.php/GStreamer "GStreamer")

	[https://www.enlightenment.org/about-rage](https://www.enlightenment.org/about-rage) || [rage](https://aur.archlinux.org/packages/rage/)

*   **Snappy** — Powerful media player with a minimalistic interface that uses [GStreamer](/index.php/GStreamer "GStreamer").

	[https://wiki.gnome.org/Apps/Snappy](https://wiki.gnome.org/Apps/Snappy) || [snappy-player](https://www.archlinux.org/packages/?name=snappy-player)

*   **Spivak** — Karaoke player based on [GStreamer](/index.php/GStreamer "GStreamer") and Qt5.

	[https://github.com/gyunaev/spivak](https://github.com/gyunaev/spivak) || [spivak](https://aur.archlinux.org/packages/spivak/)

*   **Xnoise** — GTK and [GStreamer](/index.php/GStreamer "GStreamer")-based media player for both audio and video with "a slick GUI, great speed and lots of features." (development ceased)

	[http://xnoise-media-player.com/](http://xnoise-media-player.com/) || [xnoise](https://www.archlinux.org/packages/?name=xnoise)

###### mpv-based

*   **Baka MPlayer** — Free and open source, cross-platform, [mpv](/index.php/Mpv "Mpv") based multimedia player (Qt 5).

	[http://bakamplayer.u8sand.net/](http://bakamplayer.u8sand.net/) || [baka-mplayer](https://www.archlinux.org/packages/?name=baka-mplayer)

*   **Celluloid** — Simple GTK frontend for [mpv](/index.php/Mpv "Mpv"), formerly GNOME MPV.

	[https://gnome-mpv.github.io/](https://gnome-mpv.github.io/) || [celluloid](https://www.archlinux.org/packages/?name=celluloid)

*   **Deepin Movie** — Movie player for Deepin desktop based on [mpv](/index.php/Mpv "Mpv").

	[https://www.deepin.org/en/original/deepin-movie/](https://www.deepin.org/en/original/deepin-movie/) || [deepin-movie](https://www.archlinux.org/packages/?name=deepin-movie)

*   **Kawaii-Player** — Audio/video manager and multimedia player (based on [mpv](/index.php/Mpv "Mpv")) with PC-to-PC casting feature, along with functionalities of portable media server and torrent streaming server.

	[https://github.com/kanishka-linux/kawaii-player](https://github.com/kanishka-linux/kawaii-player) || [kawaii-player](https://aur.archlinux.org/packages/kawaii-player/)

*   **KittehPlayer** — A YouTube-like video player based on Qt, QML and [mpv](/index.php/Mpv "Mpv").

	[https://github.com/NamedKitten/KittehPlayer](https://github.com/NamedKitten/KittehPlayer) || [kittehplayer](https://aur.archlinux.org/packages/kittehplayer/)

*   **Media Player Classic Qute Theater** — Clone of [Media Player Classic](https://en.wikipedia.org/wiki/Media_Player_Classic "wikipedia:Media Player Classic") reimplimented in Qt and based on [mpv](/index.php/Mpv "Mpv").

	[https://gitlab.com/mpc-qt/mpc-qt](https://gitlab.com/mpc-qt/mpc-qt) || [mpc-qt](https://aur.archlinux.org/packages/mpc-qt/), [mpc-qt-git](https://aur.archlinux.org/packages/mpc-qt-git/)

*   **[mpv](/index.php/Mpv "Mpv")** — Very basic GUI for mpv. Can be launched with `mpv --player-operation-mode=pseudo-gui`.

	[https://mpv.io/](https://mpv.io/) || [mpv](https://www.archlinux.org/packages/?name=mpv)

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Qt multimedia player with extra features (CSS themes, YouTube integration, etc.) based on [mpv](/index.php/Mpv "Mpv"). It can use [MPlayer](/index.php/MPlayer "MPlayer") as alternative backend.

	[https://www.smplayer.info/](https://www.smplayer.info/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **xt7-player-mpv** — Qt/Gambas GUI to [mpv](/index.php/Mpv "Mpv") with a rich set of configurable options including filters and drivers, ladspa plugins support as well as library/playlist managment, YouTube, online radios, podcasts, DVB-T and more.

	[https://github.com/kokoko3k/xt7-player-mpv](https://github.com/kokoko3k/xt7-player-mpv) || [xt7-player-mpv](https://aur.archlinux.org/packages/xt7-player-mpv/)

###### MPlayer-based

*   **GNOME MPlayer** — Simple GTK-based GUI for [MPlayer](/index.php/MPlayer "MPlayer").

	[https://sites.google.com/site/kdekorte2/gnomemplayer](https://sites.google.com/site/kdekorte2/gnomemplayer) || [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **[KMPlayer](https://en.wikipedia.org/wiki/KMPlayer "wikipedia:KMPlayer")** — Simple KDE frontend for [MPlayer](/index.php/MPlayer "MPlayer") and video player plugin for Konqueror. It can use [Phonon](/index.php/Phonon "Phonon") as alternative backend.

	[https://kmplayer.kde.org/](https://kmplayer.kde.org/) || [kmplayer](https://www.archlinux.org/packages/?name=kmplayer)

*   **KPlayer** — Multimedia player for KDE4 using [MPlayer](/index.php/MPlayer "MPlayer") as a backend.

	[http://kplayer.sourceforge.net/](http://kplayer.sourceforge.net/) || [kplayer](https://aur.archlinux.org/packages/kplayer/)

###### Other

*   **[Dragon Player](https://en.wikipedia.org/wiki/Dragon_Player "wikipedia:Dragon Player")** — Simple video player for KDE based on [Phonon](/index.php/Phonon "Phonon"). Part of the [kdemultimedia](https://www.archlinux.org/groups/x86_64/kdemultimedia/) group.

	[https://www.kde.org/applications/multimedia/dragonplayer/](https://www.kde.org/applications/multimedia/dragonplayer/) || [dragon](https://www.archlinux.org/packages/?name=dragon)

*   **[Kaffeine](https://en.wikipedia.org/wiki/Kaffeine "wikipedia:Kaffeine")** — Very versatile KDE media player that, by default, utilizes [VLC](/index.php/VLC "VLC") as its backend and has excellent support of digital TV ([DVB-T](/index.php/DVB-T "DVB-T"), DVB-C, [DVB-S](/index.php/DVB-S "DVB-S")).

	[https://www.kde.org/applications/multimedia/kaffeine/](https://www.kde.org/applications/multimedia/kaffeine/) || [kaffeine](https://www.archlinux.org/packages/?name=kaffeine)

*   **Kaku** — Highly integrated music player supports different online platform like YouTube, SoundCloud, Vimeo and more. Based on the [Electron](https://electronjs.org/) platform.

	[https://kaku.rocks/](https://kaku.rocks/) || [kaku-bin](https://aur.archlinux.org/packages/kaku-bin/)

*   **[Kodi](/index.php/Kodi "Kodi")** — Media player and entertainment hub for digital media.

	[https://kodi.tv/](https://kodi.tv/) || [kodi](https://www.archlinux.org/packages/?name=kodi)

*   **Minitube** — YouTube desktop application written in C++ using [Phonon](/index.php/Phonon "Phonon") and Qt.

	[https://flavio.tordini.org/minitube](https://flavio.tordini.org/minitube) || [minitube](https://www.archlinux.org/packages/?name=minitube)

*   **QMPlay2** — Qt based video player. It can play and stream all formats supported by [FFmpeg](/index.php/FFmpeg "FFmpeg") and libmodplug. It has on integrated module system, which includes a YouTube browser.

	[http://zaps166.sourceforge.net/?app=QMPlay2](http://zaps166.sourceforge.net/?app=QMPlay2) || [qmplay2](https://aur.archlinux.org/packages/qmplay2/)

*   **QtAV Player** — Simple media player based on QtAV and [FFmpeg](/index.php/FFmpeg "FFmpeg"). Run with `Player` or `QMLPlayer`.

	[http://www.qtav.org/](http://www.qtav.org/) || [qtav](https://www.archlinux.org/packages/?name=qtav)

*   **[tvtime](https://en.wikipedia.org/wiki/tvtime "wikipedia:tvtime")** — High quality television application for use with video capture cards.

	[https://linuxtv.org/](https://linuxtv.org/) || [tvtime](https://www.archlinux.org/packages/?name=tvtime)

*   **[VLC media player](/index.php/VLC_media_player "VLC media player")** — Middleweight video player with support for a wide variety of audio and video formats.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **[xine](https://en.wikipedia.org/wiki/xine "wikipedia:xine")** — Free multimedia player.

	[http://www.xine-project.org/](http://www.xine-project.org/) || [xine-ui](https://www.archlinux.org/packages/?name=xine-ui)

#### Video converters

See also [Wikipedia:Comparison of video converters](https://en.wikipedia.org/wiki/Comparison_of_video_converters "wikipedia:Comparison of video converters") and [Codecs and containers#Container format tools](/index.php/Codecs_and_containers#Container_format_tools "Codecs and containers").

##### Console

*   **[Avidemux CLI](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — Free video editor designed for simple cutting, filtering and encoding tasks.

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-cli](https://www.archlinux.org/packages/?name=avidemux-cli)

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Complete, cross-platform solution to record, convert and stream audio and video.

	[http://ffmpeg.org/](http://ffmpeg.org/) || [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)

*   **[HandBrake CLI](https://en.wikipedia.org/wiki/HandBrake "wikipedia:HandBrake")** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping.

	[https://handbrake.fr/](https://handbrake.fr/) || [handbrake-cli](https://www.archlinux.org/packages/?name=handbrake-cli)

*   **[MEncoder](https://en.wikipedia.org/wiki/MEncoder "wikipedia:MEncoder")** — Free command line video decoding, encoding and filtering tool.

	[http://mplayerhq.hu/](http://mplayerhq.hu/) || [mencoder](https://www.archlinux.org/packages/?name=mencoder)

*   **Transcode** — Command line tool for video stream processing.

	[https://bitbucket.org/france/transcode-tcforge](https://bitbucket.org/france/transcode-tcforge) || [transcode](https://www.archlinux.org/packages/?name=transcode)

##### Graphical

*   **Ciano** — Simple multimedia file converter using FFmpeg and ImageMagick.

	[https://robertsanseries.github.io/ciano/](https://robertsanseries.github.io/ciano/) || [ciano](https://www.archlinux.org/packages/?name=ciano)

*   **Curlew** — Easy to use multimedia converter written in Python and GTK3 and uses FFmpeg.

	[https://curlew.sourceforge.io/](https://curlew.sourceforge.io/) || [curlew](https://aur.archlinux.org/packages/curlew/)

*   **FFmpegYAG** — Advanced GUI for the popular FFmpeg audio/video encoding tool.

	[https://sourceforge.net/projects/ffmpegyag/](https://sourceforge.net/projects/ffmpegyag/) || [ffmpegyag](https://aur.archlinux.org/packages/ffmpegyag/)

*   **FF Multi Converter** — Simple graphical application which enables you to convert audio, video, image and document files between all popular formats, by utilizing other command-line tools.

	[https://sites.google.com/site/ffmulticonverter/](https://sites.google.com/site/ffmulticonverter/) || [ffmulticonverter](https://aur.archlinux.org/packages/ffmulticonverter/)

*   **[HandBrake](https://en.wikipedia.org/wiki/HandBrake "wikipedia:HandBrake")** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping. GTK version.

	[https://handbrake.fr/](https://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **QWinFF** — Qt5 GUI for FFmpeg that can read audio and video files in various formats and convert them into other formats.

	[http://qwinff.github.io/](http://qwinff.github.io/) || [qwinff](https://aur.archlinux.org/packages/qwinff/)

*   **traGtor** — Convert all your audio and video files through FFmpeg without using a terminal.

	[http://mein-neues-blog.de/tragtor-gui-for-ffmpeg/](http://mein-neues-blog.de/tragtor-gui-for-ffmpeg/) || [tragtor](https://aur.archlinux.org/packages/tragtor/)

*   **Transmageddon** — Simple python application for transcoding video into formats supported by GStreamer.

	[http://www.linuxrising.org/](http://www.linuxrising.org/) || [transmageddon](https://www.archlinux.org/packages/?name=transmageddon)

*   **WinFF** — Graphical video and audio batch converter using FFmpeg.

	[https://www.biggmatt.com/winff/](https://www.biggmatt.com/winff/) || [winff](https://aur.archlinux.org/packages/winff/)

#### Video editors

See also [Wikipedia:Comparison of video editing software](https://en.wikipedia.org/wiki/Comparison_of_video_editing_software "wikipedia:Comparison of video editing software").

*   **[Avidemux](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — Free video editor designed for simple cutting, filtering and encoding tasks.

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-qt](https://www.archlinux.org/packages/?name=avidemux-qt)

*   **[Blender](https://en.wikipedia.org/wiki/Blender_(software)#Video_editing "wikipedia:Blender (software)")** — Fully integrated 3D graphics creation suite with a built-in non-linear video editor.

	[https://www.blender.org/](https://www.blender.org/) || [blender](https://www.archlinux.org/packages/?name=blender)

*   **[Cinelerra (Community Version)](https://en.wikipedia.org/wiki/Cinelerra "wikipedia:Cinelerra")** — Professional video editing and compositing environment.

	[https://www.cinelerra-gg.org/](https://www.cinelerra-gg.org/) || [cinelerra-cv](https://aur.archlinux.org/packages/cinelerra-cv/)

*   **[DaVinci Resolve](/index.php/DaVinci_Resolve "DaVinci Resolve")** — Proprietary A/V post-production software suite.

	[https://www.blackmagicdesign.com/products/davinciresolve/](https://www.blackmagicdesign.com/products/davinciresolve/) || [davinci-resolve](https://aur.archlinux.org/packages/davinci-resolve/)

*   **[Flowblade](https://en.wikipedia.org/wiki/Flowblade "wikipedia:Flowblade")** — Multitrack non-linear video editor for Linux, designed to provide a fast, robust editing experience.

	[https://github.com/jliljebl/flowblade](https://github.com/jliljebl/flowblade) || [flowblade](https://aur.archlinux.org/packages/flowblade/)

*   **[Kdenlive](https://en.wikipedia.org/wiki/Kdenlive "wikipedia:Kdenlive")** — Non-linear video editor designed for basic to semi-professional work.

	[https://kdenlive.org/](https://kdenlive.org/) || [kdenlive](https://www.archlinux.org/packages/?name=kdenlive)

*   **[Lightworks](https://en.wikipedia.org/wiki/Lightworks "wikipedia:Lightworks")** — Professional proprietary non-linear editing system for editing and mastering digital video in various formats.

	[http://www.lwks.com/](http://www.lwks.com/) || [lwks](https://aur.archlinux.org/packages/lwks/)

*   **[LiVES](https://en.wikipedia.org/wiki/LiVES "wikipedia:LiVES")** — Video editor and VJ (live performance) platform.

	[http://lives-video.com/](http://lives-video.com/) || [lives](https://aur.archlinux.org/packages/lives/)

*   **[Natron](https://en.wikipedia.org/wiki/Natron_(software) "wikipedia:Natron (software)")** — Open-source compositing software. Node-graph based. Similar in functionalities to Adobe After Effects and Nuke by The Foundry.

	[https://natrongithub.github.io/](https://natrongithub.github.io/) || [natron](https://aur.archlinux.org/packages/natron/)

*   **[OpenShot](https://en.wikipedia.org/wiki/OpenShot_Video_Editor "wikipedia:OpenShot Video Editor")** — Non-linear video editor based on MLT framework.

	[https://www.openshot.org/](https://www.openshot.org/) || [openshot](https://www.archlinux.org/packages/?name=openshot)

*   **[Pitivi](https://en.wikipedia.org/wiki/Pitivi "wikipedia:Pitivi")** — Video editor designed to be intuitive and integrate well in the GNOME desktop.

	[http://www.pitivi.org/](http://www.pitivi.org/) || [pitivi](https://www.archlinux.org/packages/?name=pitivi)

*   **[Shotcut](https://en.wikipedia.org/wiki/Shotcut "wikipedia:Shotcut")** — Shotcut is a free, open source, cross-platform video editor.

	[https://www.shotcut.org/](https://www.shotcut.org/) || [shotcut](https://www.archlinux.org/packages/?name=shotcut)

*   **VidCutter** — Fast lossless media cutter + joiner w/ frame-accurate SmartCut options powered by mpv, FFmpeg via a sleek Qt5 GUI.

	[https://vidcutter.ozmartians.com/](https://vidcutter.ozmartians.com/) || [vidcutter](https://aur.archlinux.org/packages/vidcutter/)

*   **Olive** — Olive is a free non-linear video editor aiming to provide a fully-featured alternative to high-end professional video editing software.

	[https://www.olivevideoeditor.org/](https://www.olivevideoeditor.org/) || [olive](https://aur.archlinux.org/packages/olive/)

#### Subtitles

*   **Penguin Subtitle Player** — Standalone subtitle player that provides a translucent window which always stays on the top so subtitles can be shown on top of the video without blocking anything.

	[https://github.com/carsonip/Penguin-Subtitle-Player](https://github.com/carsonip/Penguin-Subtitle-Player) || [penguin-subtitle-player-git](https://aur.archlinux.org/packages/penguin-subtitle-player-git/)

*   **subdl** — Command-line tool for downloading subtitles from opensubtitles.org.

	[https://github.com/akexakex/subdl](https://github.com/akexakex/subdl) || [subdl](https://www.archlinux.org/packages/?name=subdl)

*   **SubDownloader** — Automatic download/upload of subtitles using fast hashing.

	[https://github.com/subdownloader/subdownloader](https://github.com/subdownloader/subdownloader) || [subdownloader](https://www.archlinux.org/packages/?name=subdownloader)

*   **SubtitlesPrinter** — Print subtitles above a X-screen, independently of the video player.

	[https://github.com/OlivierMarty/SubtitlesPrinter](https://github.com/OlivierMarty/SubtitlesPrinter) || [subtitles-printer-git](https://aur.archlinux.org/packages/subtitles-printer-git/)

#### Subtitle editors

See also [Wikipedia:Comparison of subtitle editors](https://en.wikipedia.org/wiki/Comparison_of_subtitle_editors "wikipedia:Comparison of subtitle editors").

*   **[Aegisub](https://en.wikipedia.org/wiki/Aegisub "wikipedia:Aegisub")** — Subtitle editor.

	[https://github.com/Aegisub/Aegisub](https://github.com/Aegisub/Aegisub) || [aegisub](https://www.archlinux.org/packages/?name=aegisub)

*   **Gaupol** — Full-featured subtitle editor.

	[https://otsaloma.io/gaupol/](https://otsaloma.io/gaupol/) || [gaupol](https://www.archlinux.org/packages/?name=gaupol)

*   **[Gnome Subtitles](https://en.wikipedia.org/wiki/Gnome_Subtitles "wikipedia:Gnome Subtitles")** — Video subtitle editor for GNOME.

	[http://www.gnomesubtitles.org/](http://www.gnomesubtitles.org/) || [gnome-subtitles](https://www.archlinux.org/packages/?name=gnome-subtitles)

*   **Jubler** — Open-source multiplatform subtitle editor written in Java.

	[https://www.jubler.org/](https://www.jubler.org/) || [jubler](https://aur.archlinux.org/packages/jubler/)

*   **Subtitle Composer** — Subtitle editor with Qt 5 based GUI supporting various formats, features different player backends, able to display wave form.

	[https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer) || [subtitlecomposer](https://aur.archlinux.org/packages/subtitlecomposer/)

*   **[Subtitle Edit](https://en.wikipedia.org/wiki/Subtitle_Edit "wikipedia:Subtitle Edit")** — Subtitle editing program. Written in C# using mono.

	[https://github.com/SubtitleEdit/subtitleedit](https://github.com/SubtitleEdit/subtitleedit) || [subtitleedit](https://aur.archlinux.org/packages/subtitleedit/)

*   **Subtitle Editor** — GTK 3 tool to edit subtitles for GNU/Linux/*BSD.

	[http://kitone.github.io/subtitleeditor/](http://kitone.github.io/subtitleeditor/) || [subtitleeditor](https://www.archlinux.org/packages/?name=subtitleeditor)

#### Screencast

See [Screen capture#Screencast software](/index.php/Screen_capture#Screencast_software "Screen capture").

#### Webcam

See also [FFmpeg#Recording webcam](/index.php/FFmpeg#Recording_webcam "FFmpeg") and [Wikipedia:Comparison of webcam software](https://en.wikipedia.org/wiki/Comparison_of_webcam_software "wikipedia:Comparison of webcam software").

*   **[Cheese](https://en.wikipedia.org/wiki/Cheese_(software) "wikipedia:Cheese (software)")** — Take photos and videos with your webcam, with fun graphical effects.

	[https://wiki.gnome.org/Apps/Cheese](https://wiki.gnome.org/Apps/Cheese) || [cheese](https://www.archlinux.org/packages/?name=cheese)

*   **fswebcam** — Small and simple command line webcam software that generates images for a webcam.

	[https://www.sanslogic.co.uk/fswebcam/](https://www.sanslogic.co.uk/fswebcam/) || [fswebcam](https://aur.archlinux.org/packages/fswebcam/)

*   **[Guvcview](https://en.wikipedia.org/wiki/Guvcview "wikipedia:Guvcview")** — Simple interface for capturing and viewing video from v4l2 devices.

	[http://guvcview.sourceforge.net/](http://guvcview.sourceforge.net/) || GTK: [guvcview](https://www.archlinux.org/packages/?name=guvcview), Qt: [guvcview-qt](https://www.archlinux.org/packages/?name=guvcview-qt)

*   **Kamoso** — Webcam recorder from KDE community.

	[https://userbase.kde.org/Kamoso](https://userbase.kde.org/Kamoso) || [kamoso](https://www.archlinux.org/packages/?name=kamoso)

*   **MJPG-streamer** — Command line application which can be used to stream M-JPEG over an IP-based network from a webcam to various types of viewers.

	[https://github.com/jacksonliam/mjpg-streamer](https://github.com/jacksonliam/mjpg-streamer) || [mjpg-streamer](https://aur.archlinux.org/packages/mjpg-streamer/)

*   **[Motion](/index.php/Motion "Motion")** — Highly configurable program that monitors video signals from many types of cameras. It is able to detect if a significant part of the picture has changed; in other words, it can detect motion.

	[https://motion-project.github.io/](https://motion-project.github.io/) || [motion](https://www.archlinux.org/packages/?name=motion)

*   **Pantheon Camera** — Camera app designed for elementary OS.

	[https://github.com/elementary/camera](https://github.com/elementary/camera) || [pantheon-camera-git](https://aur.archlinux.org/packages/pantheon-camera-git/)

*   **QtCAM** — Webcam software with more than 10 image control settings, extension settings and color space switching.

	[https://www.e-consystems.com/opensource-linux-webcam-software-application.asp](https://www.e-consystems.com/opensource-linux-webcam-software-application.asp) || [qtcam-git](https://aur.archlinux.org/packages/qtcam-git/)

*   **v4l2ucp** — Universal control panel for V4L2 devices.

	[http://v4l2ucp.sourceforge.net/](http://v4l2ucp.sourceforge.net/) || [v4l2ucp](https://aur.archlinux.org/packages/v4l2ucp/)

*   **v4l-utils** — Provides a series of utilities for media devices.

	[https://linuxtv.org/](https://linuxtv.org/) || [v4l-utils](https://www.archlinux.org/packages/?name=v4l-utils)

*   **Webcamoid** — Full featured webcam suite.

	[https://webcamoid.github.io/](https://webcamoid.github.io/) || [webcamoid](https://aur.archlinux.org/packages/webcamoid/)

*   **ZArt** — GUI for G'MIC real-time manipulations on the output of a webcam.

	[https://gmic.eu/](https://gmic.eu/) || [zart](https://www.archlinux.org/packages/?name=zart)

#### DVD authoring

See also [Wikipedia:List of DVD authoring applications](https://en.wikipedia.org/wiki/List_of_DVD_authoring_applications "wikipedia:List of DVD authoring applications").

*   **Bombono DVD** — DVD authoring program with nice and clean GUI.

	[http://www.bombono.org/](http://www.bombono.org/) || [bombono-dvd](https://aur.archlinux.org/packages/bombono-dvd/)

*   **[Devede](https://en.wikipedia.org/wiki/DeVeDe "wikipedia:DeVeDe")** — Program to create VideoDVDs and CDs.

	[http://www.rastersoft.com/programas/devede.html](http://www.rastersoft.com/programas/devede.html) || [devede](https://www.archlinux.org/packages/?name=devede)

*   **[DVDStyler](https://en.wikipedia.org/wiki/DVDStyler "wikipedia:DVDStyler")** — DVD authoring application for the creation of professional-looking DVDs.

	[https://www.dvdstyler.org/](https://www.dvdstyler.org/) || [dvdstyler](https://aur.archlinux.org/packages/dvdstyler/)

#### DVD ripping

See [Optical disc drive#DVD-Video](/index.php/Optical_disc_drive#DVD-Video "Optical disc drive").

#### Video thumbnails

*   **vcsi** — Create video contact sheets. A video contact sheet is an image composed of video capture thumbnails arranged on a grid.

	[https://github.com/amietn/vcsi](https://github.com/amietn/vcsi) || [vcsi-git](https://aur.archlinux.org/packages/vcsi-git/)

### Collection managers

*   **Data Crow** — Media cataloger and media organizer.

	[http://datacrow.net/](http://datacrow.net/) || [datacrow](https://aur.archlinux.org/packages/datacrow/)

*   **FileBot** — The ultimate tool for organizing and renaming your movies, tv shows or anime, and music well as downloading subtitles and artwork.

	[https://github.com/filebot/filebot](https://github.com/filebot/filebot) || [filebot](https://aur.archlinux.org/packages/filebot/)

*   **[GCstar](https://en.wikipedia.org/wiki/GCstar "wikipedia:GCstar")** — GNOME application for organizing various collections (board games, comic books, movies, stamps, etc.).

	[http://www.gcstar.org/](http://www.gcstar.org/) || [gcstar](https://aur.archlinux.org/packages/gcstar/)

*   **Griffith** — Movie collection manager application.

	[https://gitlab.com/Strit/griffith](https://gitlab.com/Strit/griffith) || [griffith](https://aur.archlinux.org/packages/griffith/)

*   **MediaElch** — Media manager for Kodi. Information about movies, TV shows, concerts and music are stored as nfo files.

	[https://www.kvibes.de/en/mediaelch/](https://www.kvibes.de/en/mediaelch/) || [mediaelch](https://www.archlinux.org/packages/?name=mediaelch)

*   **[Tellico](https://en.wikipedia.org/wiki/Tellico_(software) "wikipedia:Tellico (software)")** — KDE application for organizing various collections (books, video, music, coins, etc.).

	[http://tellico-project.org/](http://tellico-project.org/) || [tellico](https://www.archlinux.org/packages/?name=tellico)

*   **tinyMediaManager** — Media management tool to provide metadata for Kodi.

	[https://tinymediamanager.org/](https://tinymediamanager.org/) || [tiny-media-manager](https://aur.archlinux.org/packages/tiny-media-manager/)

*   **vMovieDB** — Movie collection manager for the Gnome desktop.

	[https://sourceforge.net/projects/vmoviedb/](https://sourceforge.net/projects/vmoviedb/) || [vmoviedb](https://aur.archlinux.org/packages/vmoviedb/)

### Media servers

*   **Airsonic** — Web-based media streamer, providing ubiquitous access to your music. (Fork of Subsonic.)

	[https://airsonic.github.io/](https://airsonic.github.io/) || [airsonic](https://aur.archlinux.org/packages/airsonic/)

*   **[Emby](/index.php/Emby "Emby")** — Proprietary media server, which automatically converts and streams your media on-the-fly to play on any device.

	[https://emby.media/](https://emby.media/) || [emby-server](https://www.archlinux.org/packages/?name=emby-server)

*   **forked-daapd** — DAAP (iTunes) and MPD media server with support for AirPlay devices, Apple Remote, Chromecast, Spotify and internet radio.

	[http://ejurgensen.github.io/forked-daapd/](http://ejurgensen.github.io/forked-daapd/) || [forked-daapd](https://aur.archlinux.org/packages/forked-daapd/)

*   **Gerbera** — UPnP Media Server to stream your media to devices on your home network. (Fork of MediaTomb.)

	[https://gerbera.io/](https://gerbera.io/) || [gerbera](https://aur.archlinux.org/packages/gerbera/)

*   **[Icecast](/index.php/Icecast "Icecast")** — Streaming media (audio/video) server which currently supports Ogg (Vorbis and Theora), Opus, WebM and MP3 streams.

	[https://icecast.org/](https://icecast.org/) || [icecast](https://www.archlinux.org/packages/?name=icecast)

*   **Jellyfin** — Jellyfin is a Free Software Media System that puts you in control of managing and streaming your media.

	[https://jellyfin.github.io/](https://jellyfin.github.io/) || [jellyfin](https://aur.archlinux.org/packages/jellyfin/)

*   **[Plex](/index.php/Plex "Plex")** — Proprietary media server, which organizes your personal video, music, and photo collections and streams them to all of your devices.

	[https://www.plex.tv/](https://www.plex.tv/) || [plex-media-server](https://aur.archlinux.org/packages/plex-media-server/)

*   **[ReadyMedia](/index.php/ReadyMedia "ReadyMedia")** — Simple media server software, with the aim of being fully compliant with DLNA/UPnP-AV clients.

	[https://sourceforge.net/projects/minidlna/](https://sourceforge.net/projects/minidlna/) || [minidlna](https://www.archlinux.org/packages/?name=minidlna)

*   **[Rygel](/index.php/Rygel "Rygel")** — UPnP AV MediaServer and MediaRenderer that allows you to easily share audio, video and pictures, and control of media player on your home network.

	[https://wiki.gnome.org/Projects/Rygel](https://wiki.gnome.org/Projects/Rygel) || [rygel](https://www.archlinux.org/packages/?name=rygel)

*   **Serviio** — Proprietary media server, which allows you to stream your media files (music, video or images) to renderer devices (e.g. a TV set, Bluray player, games console or mobile phone) on your connected home network.

	[https://serviio.org/](https://serviio.org/) || [serviio](https://aur.archlinux.org/packages/serviio/)

*   **[Subsonic](/index.php/Subsonic "Subsonic")** — Proprietary media server to stream from your own computer.

	[http://www.subsonic.org/](http://www.subsonic.org/) || [subsonic](https://aur.archlinux.org/packages/subsonic/)

*   **[Tvheadend](/index.php/Tvheadend "Tvheadend")** — TV streaming server and recorder supporting DVB-S, DVB-S2, DVB-C, DVB-T, ATSC, ISDB-T, IPTV, SAT>IP and HDHomeRun as input sources.

	[https://tvheadend.org/](https://tvheadend.org/) || [tvheadend](https://aur.archlinux.org/packages/tvheadend/)

*   **[Universal Media Server](/index.php/Universal_Media_Server "Universal Media Server")** — UPnP media server, which is capable of sharing video, audio and images between most modern devices. (Fork of PS3 Media Server.)

	[https://www.universalmediaserver.com/](https://www.universalmediaserver.com/) || [ums](https://aur.archlinux.org/packages/ums/)

### Metadata

*   **[ExifTool](https://en.wikipedia.org/wiki/ExifTool "wikipedia:ExifTool")** — Command-line application for reading, writing and editing meta information in a wide variety of files.

	[https://sno.phy.queensu.ca/~phil/exiftool/](https://sno.phy.queensu.ca/~phil/exiftool/) || [perl-image-exiftool](https://www.archlinux.org/packages/?name=perl-image-exiftool)

*   **Exiv2** — Command line utility to manage image metadata. It provides fast and easy read and write access to the Exif, IPTC and XMP metadata and the ICC Profile embedded within digital images in various formats.

	[https://exiv2.org/](https://exiv2.org/) || [exiv2](https://www.archlinux.org/packages/?name=exiv2)

*   **[ffprobe](https://en.wikipedia.org/wiki/FFmpeg "wikipedia:FFmpeg")** — Gather information from multimedia streams and print it in human- and machine-readable fashion.

	[https://ffmpeg.org/ffprobe.html](https://ffmpeg.org/ffprobe.html) || [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)

*   **jhead** — Exif jpeg header manipulation tool.

	[http://sentex.net/~mwandel/jhead/](http://sentex.net/~mwandel/jhead/) || [jhead](https://www.archlinux.org/packages/?name=jhead)

*   **MediaConch** — Implementation checker, policy checker, reporter, and fixer.

	[https://mediaarea.net/MediaConch](https://mediaarea.net/MediaConch) || CLI: [mediaconch](https://aur.archlinux.org/packages/mediaconch/), GUI: [mediaconch-gui](https://aur.archlinux.org/packages/mediaconch-gui/)

*   **[MediaInfo](https://en.wikipedia.org/wiki/MediaInfo "wikipedia:MediaInfo")** — Convenient unified display of the most relevant technical and tag data for video and audio files.

	[https://mediaarea.net/en/MediaInfo](https://mediaarea.net/en/MediaInfo) || CLI: [mediainfo](https://www.archlinux.org/packages/?name=mediainfo), GUI: [mediainfo-gui](https://www.archlinux.org/packages/?name=mediainfo-gui)

*   **pyExifToolGUI** — Graphical frontend for ExifTool, which reads and writes all kind of metadata tags from/to image files.

	[https://hvdwolf.github.io/pyExifToolGUI/](https://hvdwolf.github.io/pyExifToolGUI/) || [pyexiftoolgui-git](https://aur.archlinux.org/packages/pyexiftoolgui-git/)

*   **[sndfile-info](https://en.wikipedia.org/wiki/libsndfile "wikipedia:libsndfile")** — Obtaining information about the contents of an audio file.

	[http://mega-nerd.com/libsndfile/](http://mega-nerd.com/libsndfile/) || [libsndfile](https://www.archlinux.org/packages/?name=libsndfile)

### Mobile device managers

*   **Android File Transfer** — Interactive [Media Transfer Protocol](/index.php/Media_Transfer_Protocol "Media Transfer Protocol") client with Qt5 GUI.

	[https://whoozle.github.io/android-file-transfer-linux/](https://whoozle.github.io/android-file-transfer-linux/) || [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer)

*   **[gnokii](https://en.wikipedia.org/wiki/Gnokii "wikipedia:Gnokii")** — Tools and user space driver for use with mobile phones.

	[https://www.gnokii.org/](https://www.gnokii.org/) || [gnokii](https://www.archlinux.org/packages/?name=gnokii)

*   **gMTP** — Simple MP3 and media player client for [Media Transfer Protocol](/index.php/Media_Transfer_Protocol "Media Transfer Protocol").

	[https://gmtp.sourceforge.io/](https://gmtp.sourceforge.io/) || [gmtp](https://www.archlinux.org/packages/?name=gmtp)

*   **GNOME Phone Manager** — Control your mobile phone from your GNOME desktop.

	[https://wiki.gnome.org/PhoneManager](https://wiki.gnome.org/PhoneManager) || [gnome-phone-manager](https://www.archlinux.org/packages/?name=gnome-phone-manager)

*   **[gtkpod](https://en.wikipedia.org/wiki/gtkpod "wikipedia:gtkpod")** — GUI for Apple's iPod using GTK. It allows you to import your existing iTunes database, add songs, podcasts, videos and cover art, and to edit ID3 tags.

	[https://sourceforge.net/projects/gtkpod/](https://sourceforge.net/projects/gtkpod/) || [gtkpod](https://aur.archlinux.org/packages/gtkpod/)

*   **KDE Connect** — Aims to communicate all your devices.

	[https://community.kde.org/KDEConnect](https://community.kde.org/KDEConnect) || [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect)

*   **Modem Manager GUI** — Control EDGE/3G/4G broadband modem specific functions.

	[https://linuxonly.ru/page/modem-manager-gui](https://linuxonly.ru/page/modem-manager-gui) || [modem-manager-gui](https://www.archlinux.org/packages/?name=modem-manager-gui)

*   **Wammu** — Manage data in your cell phone such as contacts, calendar or messages.

	[https://wammu.eu/](https://wammu.eu/) || [wammu](https://www.archlinux.org/packages/?name=wammu)

### Optical disc burning

See [Optical disc drive#Burning CD/DVD/BD with a GUI](/index.php/Optical_disc_drive#Burning_CD/DVD/BD_with_a_GUI "Optical disc drive").

## Utilities

### Terminal

#### Command shells

See the main article: [Command-line shell](/index.php/Command-line_shell "Command-line shell").

See also [Wikipedia:Comparison of command shells](https://en.wikipedia.org/wiki/Comparison_of_command_shells "wikipedia:Comparison of command shells").

#### Terminal emulators

Terminal emulators show a GUI Window that contains a terminal. Most emulate Xterm, which in turn emulates VT102, which emulates typewriter. For further background information, see [Wikipedia:Terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator").

For a comprehensive list, see [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

*   **Alacritty** — A cross-platform, GPU-accelerated terminal emulator.

	[https://github.com/jwilm/alacritty](https://github.com/jwilm/alacritty) || [alacritty](https://www.archlinux.org/packages/?name=alacritty)

*   **aterm** — Xterm replacement with transparency support. It has been deprecated in favour of urxvt since 2008.

	[http://www.afterstep.org/aterm.php](http://www.afterstep.org/aterm.php) || [aterm](https://aur.archlinux.org/packages/aterm/)

*   **Cool Retro Term** — A good looking terminal emulator which mimics the old cathode display.

	[https://github.com/Swordfish90/cool-retro-term](https://github.com/Swordfish90/cool-retro-term) || [cool-retro-term](https://www.archlinux.org/packages/?name=cool-retro-term)

*   **CuteCom** — A graphical serial terminal.

	[https://gitlab.com/cutecom/cutecom](https://gitlab.com/cutecom/cutecom) || [cutecom](https://aur.archlinux.org/packages/cutecom/)

*   **Eterm** — Terminal emulator intended as a replacement for xterm and designed for the [Enlightenment](/index.php/Enlightenment "Enlightenment") desktop.

	[http://eterm.org](http://eterm.org) || [eterm](https://aur.archlinux.org/packages/eterm/)

*   **Gate One** — Web-based terminal emulator and SSH client.

	[https://github.com/liftoff/GateOne](https://github.com/liftoff/GateOne) || [gateone-git](https://aur.archlinux.org/packages/gateone-git/)

*   **Hyper** — A terminal with JS/CSS support.

	[https://github.com/zeit/hyper](https://github.com/zeit/hyper) || [hyper](https://aur.archlinux.org/packages/hyper/)

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — Terminal emulator included in the [KDE](/index.php/KDE "KDE") desktop.

	[https://www.kde.org/applications/system/konsole/](https://www.kde.org/applications/system/konsole/) || [konsole](https://www.archlinux.org/packages/?name=konsole)

*   **[kitty](/index.php/Kitty "Kitty")** — A modern, hackable, featureful, OpenGL based terminal emulator

	[https://github.com/kovidgoyal/kitty](https://github.com/kovidgoyal/kitty) || [kitty](https://www.archlinux.org/packages/?name=kitty)

*   **mlterm** — A multi-lingual terminal emulator supporting various character sets and encodings in the world.

	[https://sourceforge.net/projects/mlterm/](https://sourceforge.net/projects/mlterm/) || [mlterm](https://aur.archlinux.org/packages/mlterm/)

*   **[PuTTY](/index.php/PuTTY "PuTTY")** — Highly configurable ssh/telnet/serial console program.

	[https://www.chiark.greenend.org.uk/~sgtatham/putty/](https://www.chiark.greenend.org.uk/~sgtatham/putty/) || [putty](https://www.archlinux.org/packages/?name=putty)

*   **QTerminal** — Lightweight Qt-based terminal emulator.

	[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal](https://www.archlinux.org/packages/?name=qterminal)

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — Popular replacement for xterm.

	[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://aur.archlinux.org/packages/rxvt/)

*   **shellinabox** — A web-based SSH Terminal

	[https://github.com/shellinabox/shellinabox](https://github.com/shellinabox/shellinabox) || [shellinabox-git](https://aur.archlinux.org/packages/shellinabox-git/)

*   **[st](/index.php/St "St")** — Simple terminal implementation for X.

	[http://st.suckless.org](http://st.suckless.org) || [st](https://aur.archlinux.org/packages/st/)

*   **Terminology** — Terminal emulator by the Enlightenment project team with innovative features: file thumbnails and media play like a media player.

	[https://www.enlightenment.org/about-terminology](https://www.enlightenment.org/about-terminology) || [terminology](https://www.archlinux.org/packages/?name=terminology)

*   **[urxvt](/index.php/Urxvt "Urxvt")** — Highly extendable (with Perl) unicode enabled rxvt-clone terminal emulator featuring tabbing, url launching, a Quake style drop-down mode and pseudo-transparency.

	[http://software.schmorp.de/pkg/rxvt-unicode.html](http://software.schmorp.de/pkg/rxvt-unicode.html) || [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode)

*   **[xterm](/index.php/Xterm "Xterm")** — Simple terminal emulator for the X Window System. It provides DEC VT102 and Tektronix 4014 compatible terminals for programs that can't use the window system directly.

	[https://invisible-island.net/xterm/](https://invisible-island.net/xterm/) || [xterm](https://www.archlinux.org/packages/?name=xterm)

*   **[Yakuake](/index.php/Yakuake "Yakuake")** — Drop-down terminal (Quake style) emulator based on Konsole.

	[https://yakuake.kde.org/](https://yakuake.kde.org/) || [yakuake](https://www.archlinux.org/packages/?name=yakuake)

##### VTE-based

[VTE](https://developer.gnome.org/vte/unstable/) (Virtual Terminal Emulator) is a widget developed during early GNOME days for use in the GNOME Terminal. It has since given birth to many terminals with similar capabilities.

*   **Deepin Terminal** — Terminal emulation application for Deepin desktop.

	[https://www.deepin.org/en/original/deepin-terminal/](https://www.deepin.org/en/original/deepin-terminal/) || [deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal)

*   **evilvte** — Very lightweight and highly customizable terminal emulator with support for tabs, auto-hiding and different encodings.

	[http://calno.com/evilvte/](http://calno.com/evilvte/) || [evilvte-git](https://aur.archlinux.org/packages/evilvte-git/)

*   **Germinal** — Minimalist terminal emulator which provides a borderless maximized terminal, attached to a tmux session by default, hence providing tabs and panels.

	[http://www.imagination-land.org/tags/germinal.html](http://www.imagination-land.org/tags/germinal.html) || [germinal](https://aur.archlinux.org/packages/germinal/)

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — A terminal emulator included in the [GNOME](/index.php/GNOME "GNOME") desktop with support for Unicode and pseudo-transparency.

	[https://wiki.gnome.org/Apps/Terminal](https://wiki.gnome.org/Apps/Terminal) || [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)

*   **[Guake](/index.php/Guake "Guake")** — Drop-down terminal for the GNOME desktop.

	[http://guake-project.org/](http://guake-project.org/) || [guake](https://www.archlinux.org/packages/?name=guake)

*   **k3rmit** — A VTE-based terminal emulator that aims to be simple, fast and effective.

	[https://github.com/orhun/k3rmit](https://github.com/orhun/k3rmit) || [k3rmit-git](https://aur.archlinux.org/packages/k3rmit-git/)

*   **LXTerminal** — Desktop independent terminal emulator for [LXDE](/index.php/LXDE "LXDE").

	[https://wiki.lxde.org/en/LXTerminal](https://wiki.lxde.org/en/LXTerminal) || [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)

*   **MATE terminal** — A fork of [Wikipedia:GNOME terminal](https://en.wikipedia.org/wiki/GNOME_terminal "wikipedia:GNOME terminal") for the [MATE](/index.php/MATE "MATE") desktop.

	[https://www.mate-desktop.org/](https://www.mate-desktop.org/) || [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)

*   **Pantheon Terminal** — A super lightweight, beautiful, and simple terminal emulator. It's designed to be setup with sane defaults and little to no configuration.

	[https://github.com/elementary/terminal](https://github.com/elementary/terminal) || [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal)

*   **ROXTerm** — Tabbed terminal emulator with a small footprint.

	[http://roxterm.sourceforge.net/](http://roxterm.sourceforge.net/) || [roxterm](https://aur.archlinux.org/packages/roxterm/)

*   **sakura** — Terminal emulator based on GTK and VTE.

	[http://www.pleyades.net/david/projects/sakura](http://www.pleyades.net/david/projects/sakura) || [sakura](https://www.archlinux.org/packages/?name=sakura)

*   **[Terminator](/index.php/Terminator "Terminator")** — Terminal emulator supporting multiple resizable terminal panels.

	[https://gnometerminator.blogspot.com/](https://gnometerminator.blogspot.com/) || [terminator](https://www.archlinux.org/packages/?name=terminator)

*   **[Termite](/index.php/Termite "Termite")** — Keyboard-centric VTE-based terminal, aimed at use within a window manager with tiling and/or tabbing support.

	[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

*   **[Tilda](/index.php/Tilda "Tilda")** — Configurable drop down terminal emulator.

	[https://github.com/lanoxx/tilda/](https://github.com/lanoxx/tilda/) || [tilda](https://www.archlinux.org/packages/?name=tilda)

*   **Tilix** — Tiling terminal emulator for GNOME.

	[https://gnunn1.github.io/tilix-web/](https://gnunn1.github.io/tilix-web/) || [tilix](https://www.archlinux.org/packages/?name=tilix)

*   **tinyterm** — Very lightweight terminal emulator based on VTE.

	[https://github.com/lahwaacz/tinyterm](https://github.com/lahwaacz/tinyterm) || [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/)

*   **[Xfce Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — Terminal emulator included in the [Xfce](/index.php/Xfce "Xfce") desktop with support for a colorized prompt and a tabbed interface.

	[https://docs.xfce.org/apps/terminal/start](https://docs.xfce.org/apps/terminal/start) || [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

##### KMS-based

The following terminal emulators are based on the [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") that could be invoked without X.

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — A KMS/DRM-based system console(getty) with an integrated terminal emulator for Linux operating systems.

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

##### framebuffer-based

In the GNU/Linux world, the [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") can refer to a virtual device in the Linux kernel (**fbdev**) or the virtual framebuffer system for X (**xvfb**). This section mainly lists the terminal emulators based on the in-kernel virtual device, i.e. **fbdev**.

*   **yaft** — A simple terminal emulator for living without X, with UCS2 glyphs, wallpaper and 256color support.

	[https://github.com/uobikiemukot/yaft](https://github.com/uobikiemukot/yaft) || [yaft](https://aur.archlinux.org/packages/yaft/)

#### Terminal pagers

See also [Wikipedia:Terminal pager](https://en.wikipedia.org/wiki/Terminal_pager "wikipedia:Terminal pager").

*   **[more](https://en.wikipedia.org/wiki/More_(command) "wikipedia:More (command)")** — A simple and feature-light pager. It is a part of util-linux.

	[https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/about/](https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/about/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[less](/index.php/Core_utilities#Essentials "Core utilities")** — A program similar to more, but with support for both forward and backward scrolling, as well as partial loading of files.

	[https://www.gnu.org/software/less/](https://www.gnu.org/software/less/) || [less](https://www.archlinux.org/packages/?name=less)

*   **[most](https://en.wikipedia.org/wiki/Most_(Unix) "wikipedia:Most (Unix)")** — A pager with support for multiple windows, left and right scrolling, and built-in colour support

	[http://www.jedsoft.org/most/](http://www.jedsoft.org/most/) || [most](https://www.archlinux.org/packages/?name=most)

*   **mcview** — A pager with mouse and colour support. It is bundled with midnight commander.

	[http://midnight-commander.org/](http://midnight-commander.org/) || [mc](https://www.archlinux.org/packages/?name=mc)

*   [Vim](/index.php/Vim "Vim") can [also be used as a pager](/index.php/Vim#Vim_as_a_pager "Vim").

#### Terminal multiplexers

See also [Wikipedia:Terminal multiplexer](https://en.wikipedia.org/wiki/Terminal_multiplexer "wikipedia:Terminal multiplexer").

*   **abduco** — Tool for session attach and detach support which allows a process to run independently from its controlling terminal.

	[http://www.brain-dump.org/projects/abduco/](http://www.brain-dump.org/projects/abduco/) || [abduco](https://www.archlinux.org/packages/?name=abduco)

*   **[byobu](https://en.wikipedia.org/wiki/Byobu_(software) "wikipedia:Byobu (software)")** — An GPLv3 licensed addon for tmux or screen. It requires a terminal multiplexer installed.

	[http://byobu.co/](http://byobu.co/) || [byobu](https://aur.archlinux.org/packages/byobu/)

*   **[dtach](/index.php/Dtach "Dtach")** — Program that emulates the detach feature of [GNU Screen](/index.php/GNU_Screen "GNU Screen").

	[http://dtach.sourceforge.net/](http://dtach.sourceforge.net/) || [dtach](https://aur.archlinux.org/packages/dtach/)

*   **dvtm** — [dwm](/index.php/Dwm "Dwm")-style window manager in the console.

	[http://brain-dump.org/projects/dvtm/](http://brain-dump.org/projects/dvtm/) || [dvtm](https://www.archlinux.org/packages/?name=dvtm)

*   **[GNU Screen](/index.php/GNU_Screen "GNU Screen")** — Full-screen window manager that multiplexes a physical terminal.

	[https://www.gnu.org/software/screen/](https://www.gnu.org/software/screen/) || [screen](https://www.archlinux.org/packages/?name=screen)

*   **mtm** — Simple terminal multiplexer with just four commands: change focus, split, close, and screen redraw.

	[https://github.com/deadpixi/mtm](https://github.com/deadpixi/mtm) || [mtm-git](https://aur.archlinux.org/packages/mtm-git/)

*   **[tmux](/index.php/Tmux "Tmux")** — BSD licensed terminal multiplexer.

	[https://tmux.github.io/](https://tmux.github.io/) || [tmux](https://www.archlinux.org/packages/?name=tmux)

### Files

#### File managers

See also [Wikipedia:Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "wikipedia:Comparison of file managers").

##### Console

*   **Clex** — File manager with full-screen user interface

	[http://www.clex.sk/](http://www.clex.sk/) || [clex](https://aur.archlinux.org/packages/clex/)

*   **ded** — directory editor, file manager similar to Emacs dired

	[https://invisible-island.net/ded/ded.html](https://invisible-island.net/ded/ded.html) || [ded](https://aur.archlinux.org/packages/ded/)

*   **[Dired](https://en.wikipedia.org/wiki/Dired "wikipedia:Dired")** — Directory editor integrated with [Emacs](/index.php/Emacs "Emacs").

	[https://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html](https://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **Last File Manager** — Powerful file manager written in Python 3 with a curses interface.

	[https://inigo.katxi.org/devel/lfm/](https://inigo.katxi.org/devel/lfm/) || [lfm](https://aur.archlinux.org/packages/lfm/)

*   **lf** — Terminal file manager written in Go using server/client architecture.

	[https://github.com/gokcehan/lf](https://github.com/gokcehan/lf) || [lf-git](https://aur.archlinux.org/packages/lf-git/)

*   **[Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")** — Console-based, dual-paneled file manager.

	[http://midnight-commander.org](http://midnight-commander.org) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **nffm** — "Nothing Fancy File Manager", a mouseless ncurses file manager written in C.

	[https://github.com/mariostg/nffm](https://github.com/mariostg/nffm) || [nffm-git](https://aur.archlinux.org/packages/nffm-git/)

*   **[nnn](/index.php/Nnn "Nnn")** — Tiny, lightning fast, feature-packed file manager.

	[https://github.com/jarun/nnn](https://github.com/jarun/nnn) || [nnn](https://www.archlinux.org/packages/?name=nnn)

*   **fff** — A simple file manager written in Bash.

	[https://github.com/dylanaraps/fff](https://github.com/dylanaraps/fff) || [fff](https://www.archlinux.org/packages/?name=fff)

*   **Pilot** — File manager that comes with the [Alpine](/index.php/Alpine "Alpine") email client.

	[https://www.washington.edu/alpine/](https://www.washington.edu/alpine/) || [alpine-git](https://aur.archlinux.org/packages/alpine-git/)

*   **[Ranger](/index.php/Ranger "Ranger")** — Console-based file manager with vi bindings, customizability, and lots of features.

	[https://ranger.github.io/](https://ranger.github.io/) || [ranger](https://www.archlinux.org/packages/?name=ranger)

*   **[Vifm](/index.php/Vifm "Vifm")** — Ncurses-based two-panel file manager with vi-like keybindings.

	[https://vifm.info](https://vifm.info) || [vifm](https://www.archlinux.org/packages/?name=vifm)

##### Graphical

*   **Caja** — The file manager for the MATE desktop.

	[https://github.com/mate-desktop/caja](https://github.com/mate-desktop/caja) || [caja](https://www.archlinux.org/packages/?name=caja)

*   **Deepin File Manager** — File manager developed for [Deepin](/index.php/Deepin "Deepin").

	[https://www.deepin.org/en/original/dde-file-manager/](https://www.deepin.org/en/original/dde-file-manager/) || [deepin-file-manager](https://www.archlinux.org/packages/?name=deepin-file-manager)

*   **[Dolphin](/index.php/Dolphin "Dolphin")** — File manager included in the KDE desktop.

	[https://userbase.kde.org/Dolphin](https://userbase.kde.org/Dolphin) || [dolphin](https://www.archlinux.org/packages/?name=dolphin)

*   **Gentoo** — A lightweight file manager for GTK.

	[https://sourceforge.net/projects/gentoo/](https://sourceforge.net/projects/gentoo/) || [gentoo](https://aur.archlinux.org/packages/gentoo/)

*   **[GNOME Files](/index.php/GNOME_Files "GNOME Files")** — Extensible, heavyweight file manager used by default in GNOME with support for custom scripts.

	[https://wiki.gnome.org/Apps/Files](https://wiki.gnome.org/Apps/Files) || [nautilus](https://www.archlinux.org/packages/?name=nautilus)

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — File manager and web browser for the KDE desktop.

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **Liri Files** — The file manager for Liri.

	[https://github.com/lirios/files](https://github.com/lirios/files) || [liri-files](https://www.archlinux.org/packages/?name=liri-files)

*   **[Nemo](/index.php/Nemo "Nemo")** — Nemo is the file manager of the Cinnamon desktop. A fork of Nautilus.

	[https://cinnamon.linuxmint.com/](https://cinnamon.linuxmint.com/) || [nemo](https://www.archlinux.org/packages/?name=nemo)

*   **Pantheon Files** — File browser designed for elementary OS.

	[https://github.com/elementary/files](https://github.com/elementary/files) || [pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files)

*   **PathFinder** — File browser that comes with the [FOX toolkit](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit").

	[http://fox-toolkit.org/](http://fox-toolkit.org/) || [fox](https://www.archlinux.org/packages/?name=fox)

*   **[PCManFM](/index.php/PCManFM "PCManFM")** — Very fast and lightweight file manager which can also optionally manage the desktop icons and background.

	[https://wiki.lxde.org/en/PCManFM](https://wiki.lxde.org/en/PCManFM) || [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)

*   **qtFM** — Small, lightweight filemanager for Linux desktops based on pure Qt.

	[https://qtfm.eu/](https://qtfm.eu/) || [qtfm](https://aur.archlinux.org/packages/qtfm/)

*   **ROX** — Small and fast file manager which can optionally manage the desktop background and panels.

	[http://rox.sourceforge.net/](http://rox.sourceforge.net/) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[Thunar](/index.php/Thunar "Thunar")** — File manager that can be run as a daemon with excellent start up and directory load times.

	[https://docs.xfce.org/xfce/thunar/start](https://docs.xfce.org/xfce/thunar/start) || [thunar](https://www.archlinux.org/packages/?name=thunar)

###### Twin-panel

Note that some of these twin-panel file managers can also be set to have only one pane.

*   **Double Commander** — File manager with two panels side by side. It is inspired by Total Commander and features some new ideas.

	[https://doublecmd.sourceforge.net//](https://doublecmd.sourceforge.net//) || GTK: [doublecmd-gtk2](https://www.archlinux.org/packages/?name=doublecmd-gtk2), Qt5: [doublecmd-qt5](https://www.archlinux.org/packages/?name=doublecmd-qt5)

*   **[emelFM2](https://en.wikipedia.org/wiki/emelFM2 "wikipedia:emelFM2")** — File manager that implements the popular two-panel design.

	[http://emelfm2.net/](http://emelfm2.net/) || [emelfm2](https://www.archlinux.org/packages/?name=emelfm2)

*   **[GNOME Commander](https://en.wikipedia.org/wiki/GNOME_Commander "wikipedia:GNOME Commander")** — A dual-paned file manager for the GNOME Desktop.

	[https://gcmd.github.io/](https://gcmd.github.io/) || [gnome-commander](https://aur.archlinux.org/packages/gnome-commander/)

*   **[Krusader](https://en.wikipedia.org/wiki/Krusader "wikipedia:Krusader")** — Advanced twin panel (Midnight Commander style) file manager for the KDE desktop.

	[https://krusader.org/](https://krusader.org/) || [krusader](https://www.archlinux.org/packages/?name=krusader)

*   **muCommander** — A lightweight, cross-platform file manager with a dual-pane interface written in Java.

	[http://www.mucommander.com/](http://www.mucommander.com/) || [mucommander](https://aur.archlinux.org/packages/mucommander/)

*   **[SpaceFM](/index.php/SpaceFM "SpaceFM")** — GTK multi-panel tabbed file manager.

	[http://ignorantguru.github.io/spacefm/](http://ignorantguru.github.io/spacefm/) || [spacefm](https://aur.archlinux.org/packages/spacefm/)

*   **Sunflower** — Small and highly customizable twin-panel file manager for Linux with support for plugins.

	[http://sunflower-fm.org/](http://sunflower-fm.org/) || [sunflower](https://aur.archlinux.org/packages/sunflower/)

*   **trolCommander** — Lightweight, dual-pane file manager written in Java. Fork of muCommander.

	[https://github.com/trol73/mucommander](https://github.com/trol73/mucommander) || [trolcommander](https://aur.archlinux.org/packages/trolcommander/)

*   **Tux Commander** — Windowed file manager with two panels side by side similar to popular Total Commander or Midnight Commander file managers.

	[http://tuxcmd.sourceforge.net/description.php](http://tuxcmd.sourceforge.net/description.php) || [tuxcmd](https://www.archlinux.org/packages/?name=tuxcmd)

*   **Worker** — Fast, lightweight and feature-rich file manager for the X Window System.

	[http://www.boomerangsworld.de/cms/worker/](http://www.boomerangsworld.de/cms/worker/) || [worker](https://aur.archlinux.org/packages/worker/)

*   **[Xfe](https://en.wikipedia.org/wiki/Xfe "wikipedia:Xfe")** — Microsoft Explorer-like file manager for X (X File Explorer).

	[http://roland65.free.fr/xfe/](http://roland65.free.fr/xfe/) || [xfe](https://aur.archlinux.org/packages/xfe/)

#### Trash management

*   **trash-cli** — A command-line interface implementing [FreeDesktop.org's Trash specification](https://specifications.freedesktop.org/trash-spec/trashspec-latest.html).

	[https://github.com/andreafrancia/trash-cli](https://github.com/andreafrancia/trash-cli) || [trash-cli](https://www.archlinux.org/packages/?name=trash-cli)

#### File synchronization

See also [Synchronization and backup programs#Data synchronization](/index.php/Synchronization_and_backup_programs#Data_synchronization "Synchronization and backup programs") and [Wikipedia:Comparison of file synchronization software](https://en.wikipedia.org/wiki/Comparison_of_file_synchronization_software "wikipedia:Comparison of file synchronization software").

*   **[DirSync Pro](https://en.wikipedia.org/wiki/DirSync_Pro "wikipedia:DirSync Pro")** — Small, but powerful utility for file and folder synchronization.

	[https://dirsyncpro.org/](https://dirsyncpro.org/) || [dirsyncpro](https://aur.archlinux.org/packages/dirsyncpro/)

*   **[FreeFileSync](https://en.wikipedia.org/wiki/FreeFileSync "wikipedia:FreeFileSync")** — Folder comparison and synchronization software that creates and manages backup copies of all your important files.

	[https://www.freefilesync.org/](https://www.freefilesync.org/) || [freefilesync](https://aur.archlinux.org/packages/freefilesync/)

*   **[git-annex](https://en.wikipedia.org/wiki/git-annex "wikipedia:git-annex")** — Manage files with git, without checking the file contents into git.

	[https://git-annex.branchable.com/](https://git-annex.branchable.com/) || [git-annex](https://www.archlinux.org/packages/?name=git-annex)

*   **hsync** — Command line program to sync only those files that have been renamed/moved but otherwise unchanged. It works by issuing simple move operations at the destination without actually transferring the files, and is meant to be used in conjunction with other synchronization programs that lack this capability.

	[https://ambrevar.bitbucket.io/hsync/](https://ambrevar.bitbucket.io/hsync/) || [hsync](https://aur.archlinux.org/packages/hsync/)

*   **rclone** — Command line program to sync files and directories to and from Amazon S3, Dropbox, Google Drive, Microsoft OneDrive, Yandex Disk and many other cloud storage services as well as between local paths.

	[https://rclone.org/](https://rclone.org/) || [rclone](https://www.archlinux.org/packages/?name=rclone)

*   **[rsync](/index.php/Rsync "Rsync")** — File transfer program that uses the "rsync algorithm" which provides a very fast method for bringing remote files into sync. It does this by sending just the differences in the files across the link, without requiring that both sets of files are present at one of the ends of the link beforehand.

	[https://rsync.samba.org/](https://rsync.samba.org/) || [rsync](https://www.archlinux.org/packages/?name=rsync)

*   **[SparkleShare](https://en.wikipedia.org/wiki/SparkleShare "wikipedia:SparkleShare")** — File sharing and collaboration application written in C#. It can sync with any Git server over SSH.

	[http://www.sparkleshare.org/](http://www.sparkleshare.org/) || [sparkleshare](https://www.archlinux.org/packages/?name=sparkleshare)

*   **[Syncthing](/index.php/Syncthing "Syncthing")** — Continuous file synchronization program. It synchronizes files between two or more computers in a simple way without advanced configuration.

	[https://syncthing.net/](https://syncthing.net/) || Web: [syncthing](https://www.archlinux.org/packages/?name=syncthing), GTK: [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk)

*   **Syncany** — Cloud storage and filesharing application with a focus on security and abstraction of storage.

	[https://www.syncany.org/](https://www.syncany.org/) || [syncany](https://aur.archlinux.org/packages/syncany/)

*   **[Synkron](https://en.wikipedia.org/wiki/Synkron "wikipedia:Synkron")** — Application that helps you keep your files and folders always updated. You can easily sync your documents, music or pictures to have their latest versions everywhere.

	[http://synkron.sourceforge.net/](http://synkron.sourceforge.net/) || [synkron](https://aur.archlinux.org/packages/synkron/)

*   **[Unison](/index.php/Unison "Unison")** — File synchronization tool that allows two replicas of a collection of files and directories to be stored on different hosts (or different disks on the same host), modified separately, and then brought up to date by propagating the changes in each replica to the other.

	[https://www.cis.upenn.edu/~bcpierce/unison/](https://www.cis.upenn.edu/~bcpierce/unison/) || [unison](https://www.archlinux.org/packages/?name=unison)

#### Archiving and compression tools

For archiving and compression command-line tools, see [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression").

##### Archive managers

*   **[Ark](https://en.wikipedia.org/wiki/Ark_(software) "wikipedia:Ark (software)")** — Archiving tool included in the KDE desktop.

	[https://www.kde.org/applications/utilities/ark/](https://www.kde.org/applications/utilities/ark/) || [ark](https://www.archlinux.org/packages/?name=ark)

*   **Engrampa** — Archive manager for [MATE](/index.php/MATE "MATE")

	[https://github.com/mate-desktop/engrampa](https://github.com/mate-desktop/engrampa) || [engrampa](https://www.archlinux.org/packages/?name=engrampa)

*   **[GNOME Archive Manager](https://en.wikipedia.org/wiki/GNOME_Archive_Manager "wikipedia:GNOME Archive Manager")** — Archive manager included in the GNOME desktop (previously File Roller).

	[https://wiki.gnome.org/Apps/FileRoller](https://wiki.gnome.org/Apps/FileRoller) || [file-roller](https://www.archlinux.org/packages/?name=file-roller)

*   **p7zip-gui** — The GUI belonging to the p7zip software.

	[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip-gui](https://aur.archlinux.org/packages/p7zip-gui/)

*   **[PeaZip](https://en.wikipedia.org/wiki/PeaZip "wikipedia:PeaZip")** — Open source file and archive manager.

	[https://www.peazip.org/peazip-linux.html](https://www.peazip.org/peazip-linux.html) || GTK: [peazip-gtk2](https://aur.archlinux.org/packages/peazip-gtk2/), Qt: [peazip-qt](https://aur.archlinux.org/packages/peazip-qt/)

*   **Squeeze** — Featherweight front-end for commandline archiving tools.

	[http://squeeze.xfce.org](http://squeeze.xfce.org) || [squeeze-git](https://aur.archlinux.org/packages/squeeze-git/)

*   **[Xarchiver](https://en.wikipedia.org/wiki/Xarchiver "wikipedia:Xarchiver")** — Lightweight desktop independent archive manager built with GTK.

	[https://github.com/ib/xarchiver](https://github.com/ib/xarchiver) || GTK 3: [xarchiver](https://www.archlinux.org/packages/?name=xarchiver), GTK 2: [xarchiver-gtk2](https://www.archlinux.org/packages/?name=xarchiver-gtk2)

#### Comparison, diff, merge

See also [Wikipedia:Comparison of file comparison tools](https://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools "wikipedia:Comparison of file comparison tools").

For managing *pacnew*/*pacsave* files, specialised tools exist. See [Pacnew and Pacsave files#Managing .pac* files](/index.php/Pacnew_and_Pacsave_files#Managing_.pac*_files "Pacnew and Pacsave files").

*   **colordiff** — A Perl script wrapper for 'diff' that produces the same output but with pretty 'syntax' highlighting.

	[https://www.colordiff.org/](https://www.colordiff.org/) || [colordiff](https://www.archlinux.org/packages/?name=colordiff)

*   **Diffuse** — Small and simple text merge tool written in Python.

	[http://diffuse.sourceforge.net/](http://diffuse.sourceforge.net/) || [diffuse](https://www.archlinux.org/packages/?name=diffuse)

*   **KDiff3** — File and directory diff and merge tool for the KDE desktop.

	[http://kdiff3.sourceforge.net/](http://kdiff3.sourceforge.net/) || [kdiff3](https://www.archlinux.org/packages/?name=kdiff3)

*   **[Kompare](https://en.wikipedia.org/wiki/Kompare "wikipedia:Kompare")** — GUI front-end program for viewing and merging differences between source files. It supports a variety of diff formats and provides many options to customize the information level displayed.

	[https://www.kde.org/applications/development/kompare/](https://www.kde.org/applications/development/kompare/) || [kompare](https://www.archlinux.org/packages/?name=kompare)

*   **[Meld](https://en.wikipedia.org/wiki/Meld_(software) "wikipedia:Meld (software)")** — Visual diff and merge tool that can compare files, directories, and version controlled projects.

	[http://meldmerge.org/](http://meldmerge.org/) || [meld](https://www.archlinux.org/packages/?name=meld)

*   **xxdiff** — A graphical browser for file and directory differences.

	[http://furius.ca/xxdiff/](http://furius.ca/xxdiff/) || [xxdiff](https://aur.archlinux.org/packages/xxdiff/)

*   **ydiff** — A Python wrapper to get highlighted output from GNU diff's output or vcs-tracked file/dirs, in either unfied or side-by-side view.

	[https://github.com/ymattw/ydiff](https://github.com/ymattw/ydiff) || [ydiff](https://aur.archlinux.org/packages/ydiff/)

[Vim](/index.php/Vim "Vim") and [Emacs](/index.php/Emacs "Emacs") provide merge functionality with [vimdiff](/index.php/Vim#Merging_files "Vim") and `ediff`.

#### Batch renamers

*   **[GPRename](https://en.wikipedia.org/wiki/GPRename "wikipedia:GPRename")** — GTK batch renamer for files and directories.

	[http://gprename.sourceforge.net](http://gprename.sourceforge.net) || [gprename](https://www.archlinux.org/packages/?name=gprename)

*   **[KRename](https://en.wikipedia.org/wiki/KRename "wikipedia:KRename")** — Very powerful batch file renamer for the KDE desktop.

	[http://www.krename.net](http://www.krename.net) || [krename](https://www.archlinux.org/packages/?name=krename)

*   **metamorphose2** — wxPython based batch renamer with support for regular expressions, renaming multimedia files according to their metadata, etc.

	[http://file-folder-ren.sourceforge.net](http://file-folder-ren.sourceforge.net) || [metamorphose2](https://aur.archlinux.org/packages/metamorphose2/)

*   **pyRenamer** — Application for the mass renaming of files.

	[https://github.com/SteveRyherd/pyRenamer](https://github.com/SteveRyherd/pyRenamer) || [pyrenamer](https://aur.archlinux.org/packages/pyrenamer/)

*   **rename.pl** — Batch renamer based on perl regex.

	[http://search.cpan.org/~pederst/rename/bin/rename.PL](http://search.cpan.org/~pederst/rename/bin/rename.PL) || [perl-rename](https://www.archlinux.org/packages/?name=perl-rename)

*   **[Thunar](/index.php/Thunar "Thunar") Bulk Rename** — Change the name of multiple files at once using some criterion that applies to at least one of the files. Run with `thunar -B`.

	[https://docs.xfce.org/xfce/thunar/bulk-renamer/start](https://docs.xfce.org/xfce/thunar/bulk-renamer/start) || [thunar](https://www.archlinux.org/packages/?name=thunar)

#### File searching

This section lists utilities for file searching based on filename, file path or metadata. For full-text searching, see the next section.

See also [Wikipedia:List of search engines#Desktop search engines](https://en.wikipedia.org/wiki/List_of_search_engines#Desktop_search_engines "wikipedia:List of search engines").

##### Console

See [find](/index.php/Find "Find") and its alternatives.

##### Graphical

*   **Catfish** — Versatile file searching tool by Xfce, can be powered by find, locate and Zeitgeist.

	[https://launchpad.net/catfish-search](https://launchpad.net/catfish-search) || [catfish](https://www.archlinux.org/packages/?name=catfish)

*   **GNOME Search Tool** — GNOME utility to search for files, depends on [GNOME/Files](/index.php/GNOME/Files "GNOME/Files").

	[https://gitlab.gnome.org/GNOME/gnome-search-tool](https://gitlab.gnome.org/GNOME/gnome-search-tool) || [gnome-search-tool](https://www.archlinux.org/packages/?name=gnome-search-tool)

*   **KFind** — Search tool for KDE to find files by name, type or content. Has internal search and supports locate.

	[https://www.kde.org/applications/utilities/kfind/](https://www.kde.org/applications/utilities/kfind/) || [kfind](https://www.archlinux.org/packages/?name=kfind)

*   **MATE Search Tool** — MATE utility to search for files.

	[https://github.com/mate-desktop/mate-utils](https://github.com/mate-desktop/mate-utils) || [mate-utils](https://www.archlinux.org/packages/?name=mate-utils)

*   **regexxer** — Interactive search and replace tool featuring Perl-style regular expressions.

	[http://regexxer.sourceforge.net/](http://regexxer.sourceforge.net/) || [regexxer](https://www.archlinux.org/packages/?name=regexxer)

*   **Searchmonkey** — Powerful GUI search utility for matching regex patterns.

	[http://searchmonkey.embeddediq.com/](http://searchmonkey.embeddediq.com/) || [searchmonkey](https://aur.archlinux.org/packages/searchmonkey/)

###### File indexers

These programs index your files to allow for quick searching.

*   **Basenji** — Volume indexing tool designed for easy and fast indexing of CD/DVD and other type of volume collections.

	[https://github.com/pulb/basenji](https://github.com/pulb/basenji) || [basenji](https://aur.archlinux.org/packages/basenji/)

*   **fsearch** — A fast file search utility for Unix-like systems based on GTK 3.

	[https://github.com/cboxdoerfer/fsearch](https://github.com/cboxdoerfer/fsearch) || [fsearch-git](https://aur.archlinux.org/packages/fsearch-git/)

#### Full-text searching

[Grep](/index.php/Grep "Grep") and its alternatives provide non-indexed [full-text search](https://en.wikipedia.org/wiki/Full-text_search "wikipedia:Full-text search").

##### Full-text indexers

*   **[Baloo](/index.php/Baloo "Baloo")** — KDE's file indexing and search solution, has a CLI and is used by [KRunner](/index.php/KRunner "KRunner").

	[https://community.kde.org/Baloo](https://community.kde.org/Baloo) || [baloo](https://www.archlinux.org/packages/?name=baloo)

*   **[DocFetcher](https://en.wikipedia.org/wiki/DocFetcher "wikipedia:DocFetcher")** — Graphical Java desktop search application.

	[http://docfetcher.sourceforge.net](http://docfetcher.sourceforge.net) || [docfetcher](https://aur.archlinux.org/packages/docfetcher/)

*   **[Recoll](https://en.wikipedia.org/wiki/Recoll "wikipedia:Recoll")** — Full text search tool based on Xapian, has CLI and GUI.

	[https://lesbonscomptes.com/recoll/](https://lesbonscomptes.com/recoll/) || [recoll](https://www.archlinux.org/packages/?name=recoll)

*   **[Tracker](https://en.wikipedia.org/wiki/Tracker_(search_software) "wikipedia:Tracker (search software)")** — All-in-one indexer, search tool and metadata database, used by [GNOME](/index.php/GNOME "GNOME") Documents, Music, Photos and Videos.

	[https://wiki.gnome.org/Projects/Tracker](https://wiki.gnome.org/Projects/Tracker) || [tracker](https://www.archlinux.org/packages/?name=tracker)

*   **[Zeitgeist](/index.php/Zeitgeist "Zeitgeist")** — Event aggregation framework for the user's activities and notifications (files opened, websites visited, conversations had, etc.), has several third-party front-ends.

	[https://launchpad.net/zeitgeist-project](https://launchpad.net/zeitgeist-project) || [zeitgeist](https://www.archlinux.org/packages/?name=zeitgeist)

### Development

#### Code forges

*   **[GitLab](/index.php/GitLab "GitLab")** — Project management and code hosting application.

	[https://gitlab.com/gitlab-org/gitlab-ce](https://gitlab.com/gitlab-org/gitlab-ce) || [gitlab](https://www.archlinux.org/packages/?name=gitlab)

*   **[Gitea](/index.php/Gitea "Gitea")** — Painless self-hosted Git service. Community managed fork of Gogs.

	[https://gitea.io](https://gitea.io) || [gitea](https://www.archlinux.org/packages/?name=gitea)

##### Code forge clients

*   **git-open** — Open a repo website (GitHub, GitLab, Bitbucket) in your browser

	[https://github.com/paulirish/git-open](https://github.com/paulirish/git-open) || [git-open](https://aur.archlinux.org/packages/git-open/)

*   **hub** — cli interface for Github.

	[https://hub.github.com](https://hub.github.com) || [hub](https://www.archlinux.org/packages/?name=hub)

*   **lab** — A hub-like tool for GitLab

	[https://zaquestion.github.io/lab/](https://zaquestion.github.io/lab/) || [lab-bin](https://aur.archlinux.org/packages/lab-bin/)

*   **snippet** — A terminal based interface to create a new GitLab snippet

	[https://gitlab.com/zj/snippet](https://gitlab.com/zj/snippet) || [snippet](https://aur.archlinux.org/packages/snippet/)

#### Version control systems

See also [Wikipedia:Comparison of revision control software](https://en.wikipedia.org/wiki/Comparison_of_revision_control_software "wikipedia:Comparison of revision control software").

*   **[Bazaar](/index.php/Bazaar "Bazaar")** — Distributed version control system that helps you track project history over time and to collaborate easily with others.

	[https://bazaar.canonical.com/](https://bazaar.canonical.com/) || [bzr](https://www.archlinux.org/packages/?name=bzr)

*   **[CVS](/index.php/CVS "CVS")** — Concurrent Versions System, a client-server revision control system.

	[http://cvs.nongnu.org/](http://cvs.nongnu.org/) || [cvs](https://www.archlinux.org/packages/?name=cvs)

*   **[Darcs](https://en.wikipedia.org/wiki/Darcs "wikipedia:Darcs")** — Distributed revision control system that was designed to replace traditional, centralized source control systems such as CVS and Subversion.

	[http://darcs.net/](http://darcs.net/) || [darcs](https://www.archlinux.org/packages/?name=darcs)

*   **[Fossil](https://en.wikipedia.org/wiki/Fossil_(software) "wikipedia:Fossil (software)")** — Distributed VCS with bug tracking, wiki, forum, and technotes.

	[https://www.fossil-scm.org/](https://www.fossil-scm.org/) || [fossil](https://www.archlinux.org/packages/?name=fossil)

*   **[Git](/index.php/Git "Git")** — Distributed revision control and source code management system with an emphasis on speed.

	[https://git-scm.com/](https://git-scm.com/) || [git](https://www.archlinux.org/packages/?name=git)

*   **[Mercurial](/index.php/Mercurial "Mercurial")** — Distributed version control system written in Python and similar in many ways to Git.

	[https://www.mercurial-scm.org/](https://www.mercurial-scm.org/) || [mercurial](https://www.archlinux.org/packages/?name=mercurial)

*   **[Subversion](/index.php/Subversion "Subversion")** — Full-featured centralized version control system originally designed to be a better CVS.

	[https://subversion.apache.org/](https://subversion.apache.org/) || [subversion](https://www.archlinux.org/packages/?name=subversion)

#### Build automation

See also [Wikipedia:List of build automation software](https://en.wikipedia.org/wiki/List_of_build_automation_software "wikipedia:List of build automation software").

*   **[Apache Ant](https://en.wikipedia.org/wiki/Apache_Ant "wikipedia:Apache Ant")** — Java library and command-line tool whose mission is to drive processes described in build files as targets and extension points dependent upon each other.

	[http://ant.apache.org/](http://ant.apache.org/) || [ant](https://www.archlinux.org/packages/?name=ant)

*   **[Apache Maven](https://en.wikipedia.org/wiki/Apache_Maven "wikipedia:Apache Maven")** — Build automation tool used primarily for Java.

	[http://maven.apache.org/](http://maven.apache.org/) || [maven](https://www.archlinux.org/packages/?name=maven)

*   **[CMake](https://en.wikipedia.org/wiki/CMake "wikipedia:CMake")** — Family of tools designed to build, test and package software.

	[https://cmake.org/](https://cmake.org/) || [cmake](https://www.archlinux.org/packages/?name=cmake)

*   **[GNU make](https://en.wikipedia.org/wiki/Make_(software) "wikipedia:Make (software)")** — GNU make utility to maintain groups of programs.

	[http://www.gnu.org/software/make/](http://www.gnu.org/software/make/) || [make](https://www.archlinux.org/packages/?name=make) (part of [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/))

*   **[Gradle](https://en.wikipedia.org/wiki/Gradle "wikipedia:Gradle")** — Powerful build system for the JVM.

	[https://gradle.org/](https://gradle.org/) || [gradle](https://www.archlinux.org/packages/?name=gradle)

*   **Phing** — PHP program designed to automate tasks of all kinds.

	[https://www.phing.info/](https://www.phing.info/) || [phing](https://aur.archlinux.org/packages/phing/)

#### Integrated development environments

See also [Wikipedia:Comparison of integrated development environments](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments "wikipedia:Comparison of integrated development environments").

*   **[Anjuta](https://en.wikipedia.org/wiki/Anjuta "wikipedia:Anjuta")** — Versatile IDE with project management, an application wizard, an interactive debugger, a source editor, version control support and many more tools.

	[http://anjuta.org/](http://anjuta.org/) || [anjuta](https://www.archlinux.org/packages/?name=anjuta)

*   **[Aptana Studio](https://en.wikipedia.org/wiki/Aptana#Aptana_Studio "wikipedia:Aptana")** — IDE based on Eclipse, but geared towards web development, with support for HTML, CSS, Javascript, Ruby on Rails, PHP, Adobe AIR and others.

	[http://www.aptana.com/](http://www.aptana.com/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **[Bluefish](https://en.wikipedia.org/wiki/Bluefish_(software) "wikipedia:Bluefish (software)")** — Powerful editor targeted towards programmers and webdevelopers, with many options to write websites, scripts and programming code. It supports many programming and markup languages.

	[http://bluefish.openoffice.nl/](http://bluefish.openoffice.nl/) || [bluefish](https://www.archlinux.org/packages/?name=bluefish)

*   **[Code::Blocks](https://en.wikipedia.org/wiki/Code::Blocks "wikipedia:Code::Blocks")** — C, C++ and Fortran IDE built to meet the most demanding needs of its users. It is designed to be very extensible and fully configurable.

	[http://codeblocks.org/](http://codeblocks.org/) || [codeblocks](https://www.archlinux.org/packages/?name=codeblocks)

*   **[CLion](https://en.wikipedia.org/wiki/JetBrains#CLion "wikipedia:JetBrains")** — A cross-platform IDE for C and C++.

	[http://www.jetbrains.com/clion](http://www.jetbrains.com/clion) || [clion](https://aur.archlinux.org/packages/clion/)

*   **[CodeLite](https://en.wikipedia.org/wiki/CodeLite "wikipedia:CodeLite")** — Open source and cross-platform C/C++/PHP and Node.js IDE written in C++ .

	[https://codelite.org/](https://codelite.org/) || [codelite](https://aur.archlinux.org/packages/codelite/)

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

	[https://c9.io/](https://c9.io/) || [c9.core](https://aur.archlinux.org/packages/c9.core/)

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — IDE for Java, C/C++, PHP, Perl and Python with subversion support and task management.

	[https://www.eclipse.org/](https://www.eclipse.org/) || Java EE: [eclipse-jee](https://www.archlinux.org/packages/?name=eclipse-jee), Java: [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java), C/C++: [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp), PHP: [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php), JavaScript and Web: [eclipse-javascript](https://www.archlinux.org/packages/?name=eclipse-javascript)

*   **[Eric](https://en.wikipedia.org/wiki/Eric_(software) "wikipedia:Eric (software)")** — Full-featured Python and Ruby IDE written in PyQt5.

	[https://eric-ide.python-projects.org/](https://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric)

*   **[Gambas](/index.php/Gambas "Gambas")** — IDE based on a Basic interpreter with object extensions.

	[http://gambas.sourceforge.net/en/main.html](http://gambas.sourceforge.net/en/main.html) || [gambas3-ide](https://www.archlinux.org/packages/?name=gambas3-ide)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — Small and lightweight IDE with many supported many programming and markup languages including C, Java, PHP, HTML, Python, Perl, Pascal.

	[https://geany.org/](https://geany.org/) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **[GNOME Builder](https://en.wikipedia.org/wiki/GNOME_Builder "wikipedia:GNOME Builder")** — Tool to write and contribute to great GNOME-based applications.

	[https://wiki.gnome.org/Apps/Builder](https://wiki.gnome.org/Apps/Builder) || [gnome-builder](https://www.archlinux.org/packages/?name=gnome-builder)

*   **[KDevelop](https://en.wikipedia.org/wiki/KDevelop "wikipedia:KDevelop")** — Feature-full, plugin extensible IDE for C/C++ and other programming languages.

	[https://www.kdevelop.org/](https://www.kdevelop.org/) || [kdevelop](https://www.archlinux.org/packages/?name=kdevelop)

*   **[Komodo Edit](https://en.wikipedia.org/wiki/Komodo_Edit "wikipedia:Komodo Edit")** — A free, multi-language editor.

	[https://www.activestate.com/products/komodo-edit/](https://www.activestate.com/products/komodo-edit/) || [komodo-edit](https://aur.archlinux.org/packages/komodo-edit/)

*   **[Lazarus](https://en.wikipedia.org/wiki/Lazarus_(IDE) "wikipedia:Lazarus (IDE)")** — Delphi (Object Pascal) compatible IDE for Rapid Application Development. It has variety of components ready for use and a graphical form designer to easily create complex graphical user interfaces.

	[https://www.lazarus-ide.org/](https://www.lazarus-ide.org/) || [lazarus](https://www.archlinux.org/packages/?name=lazarus)

*   **LiteIDE** — Simple Go IDE.

	[https://github.com/visualfc/liteide](https://github.com/visualfc/liteide) || [liteide](https://www.archlinux.org/packages/?name=liteide)

*   **[MonoDevelop](https://en.wikipedia.org/wiki/MonoDevelop "wikipedia:MonoDevelop")** — Cross-platform IDE targeted for the Mono and .NET frameworks.

	[https://www.monodevelop.com/](https://www.monodevelop.com/) || [monodevelop-git](https://aur.archlinux.org/packages/monodevelop-git/)

*   **[MPLAB](https://en.wikipedia.org/wiki/MPLAB "wikipedia:MPLAB")** — IDE for Microchip PIC and dsPIC development.

	[https://www.microchip.com/mplabx](https://www.microchip.com/mplabx) || [microchip-mplabx-bin](https://aur.archlinux.org/packages/microchip-mplabx-bin/)

*   **[Netbeans](/index.php/Netbeans "Netbeans")** — IDE for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

	[https://netbeans.org/](https://netbeans.org/) || [netbeans](https://www.archlinux.org/packages/?name=netbeans)

*   **[PHPStorm](/index.php/PHPStorm "PHPStorm")** — JetBrains PhpStorm is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform, providing an editor for PHP, HTML and JavaScript with on-the-fly code analysis, error prevention and automated refactorings for PHP and JavaScript code.

	[https://www.jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/) || [phpstorm](https://aur.archlinux.org/packages/phpstorm/) [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/)

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — Lightweight, cross-platform C++ integrated development environment with a focus on Qt.

	[https://www.qt.io/ide/](https://www.qt.io/ide/) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

##### Java IDEs

*   **[BlueJ](https://en.wikipedia.org/wiki/BlueJ "wikipedia:BlueJ")** — Fully featured Java IDE used mainly for educational and beginner purposes.

	[https://bluej.org/](https://bluej.org/) || [bluej](https://aur.archlinux.org/packages/bluej/)

*   **[IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA "wikipedia:IntelliJ IDEA")** — IDE for Java, Groovy and other programming languages with advanced refactoring features.

	[http://www.jetbrains.com/idea/](http://www.jetbrains.com/idea/) || [intellij-idea-community-edition](https://www.archlinux.org/packages/?name=intellij-idea-community-edition)

##### Python IDEs

*   **[Ninja-IDE](https://en.wikipedia.org/wiki/Ninja-IDE "wikipedia:Ninja-IDE")** — IDE for Python development.

	[http://ninja-ide.org/](http://ninja-ide.org/) || [ninja-ide](https://aur.archlinux.org/packages/ninja-ide/)

*   **[PyCharm](https://en.wikipedia.org/wiki/PyCharm "wikipedia:PyCharm")** — Python IDE with support for code analysis, debugging, unit testing, version control and web development with Django.

	[http://www.jetbrains.com/pycharm/](http://www.jetbrains.com/pycharm/) || [pycharm-community-edition](https://www.archlinux.org/packages/?name=pycharm-community-edition)

*   **[Spyder](https://en.wikipedia.org/wiki/Spyder_(software) "wikipedia:Spyder (software)")** — Scientific Python Development Environment providing MATLAB-like features.

	[https://github.com/spyder-ide/spyder](https://github.com/spyder-ide/spyder) || [spyder](https://www.archlinux.org/packages/?name=spyder)

*   **[Thonny](https://en.wikipedia.org/wiki/Thonny "wikipedia:Thonny")** — Python IDE for beginners.

	[https://thonny.org/](https://thonny.org/) || [thonny](https://aur.archlinux.org/packages/thonny/)

*   **[WingIDE](https://en.wikipedia.org/wiki/Wing_IDE "wikipedia:Wing IDE")** — Proprietary Python development environment. It is fully featured and meant for professional use.

	[http://www.wingware.com](http://www.wingware.com) || [wingide](https://aur.archlinux.org/packages/wingide/)

##### Educational IDEs

*   **[Etoys](https://en.wikipedia.org/wiki/Etoys_(programming_language) "wikipedia:Etoys (programming language)")** — Educational tool and media-rich authoring environment for teaching children.

	[http://squeakland.org/](http://squeakland.org/) || [etoys](https://aur.archlinux.org/packages/etoys/)

*   **[KTurtle](https://en.wikipedia.org/wiki/KTurtle "wikipedia:KTurtle")** — Educational programming environment that aims to make learning how to program as easily as possible. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/kturtle/](https://www.kde.org/applications/education/kturtle/) || [kturtle](https://www.archlinux.org/packages/?name=kturtle)

*   **[Processing](https://en.wikipedia.org/wiki/Processing_(programming_language) "wikipedia:Processing (programming language)")** — Playground for teaching non-programmers the fundamentals of computer programming in a visual context.

	[https://processing.org/](https://processing.org/) || [processing](https://www.archlinux.org/packages/?name=processing)

*   **[Scratch](https://en.wikipedia.org/wiki/Scratch_(programming_language) "wikipedia:Scratch (programming language)")** — Programming system and content development tool for educational and entertainment purposes, such as creating interactive projects and simple sprite-based games. It is used primarly by unskilled users (such as children) as an entry to [event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming "wikipedia:Event-driven programming").

	[https://scratch.mit.edu/](https://scratch.mit.edu/) || [scratch](https://www.archlinux.org/packages/?name=scratch)

#### Debuggers

*   **Accerciser** — Interactive Python accessibility explorer. It uses the AT-SPI library to inspect, examine, and interact with widgets, allowing you to check if an application is providing correct information to assistive technologies and automated testing frameworks.

	[https://wiki.gnome.org/Apps/Accerciser](https://wiki.gnome.org/Apps/Accerciser) || [accerciser](https://www.archlinux.org/packages/?name=accerciser)

*   **Alleyoop** — Find memory-management problems in your programs using the valgrind tool.

	[http://alleyoop.sourceforge.net/](http://alleyoop.sourceforge.net/) || [alleyoop](https://aur.archlinux.org/packages/alleyoop/)

*   **Bustle** — Draws sequence diagrams of D-Bus activity. It shows signal emissions, method calls and their corresponding returns, with time stamps for each individual event and the duration of each method call.

	[https://www.freedesktop.org/wiki/Software/Bustle/](https://www.freedesktop.org/wiki/Software/Bustle/) || [bustle-git](https://aur.archlinux.org/packages/bustle-git/)

*   **[Data Display Debugger](https://en.wikipedia.org/wiki/Data_Display_Debugger "wikipedia:Data Display Debugger")** — Graphical front-end for command-line debuggers such as GDB.

	[https://www.gnu.org/software/ddd/](https://www.gnu.org/software/ddd/) || [ddd](https://aur.archlinux.org/packages/ddd/)

*   **D-Feet** — Easy to use D-Bus debugger to inspect D-Bus interfaces of running programs and invoke methods on those interfaces.

	[https://wiki.gnome.org/Apps/DFeet](https://wiki.gnome.org/Apps/DFeet) || [d-feet](https://www.archlinux.org/packages/?name=d-feet)

*   **GammaRay** — Qt-application inspection and manipulation tool.

	[https://www.kdab.com/development-resources/qt-tools/gammaray/](https://www.kdab.com/development-resources/qt-tools/gammaray/) || [gammaray](https://www.archlinux.org/packages/?name=gammaray)

*   **KCachegrind** — Profile data visualization tool, used to determine the most time consuming execution parts of program.

	[https://www.kde.org/applications/development/kcachegrind/](https://www.kde.org/applications/development/kcachegrind/) || KDE: [kcachegrind](https://www.archlinux.org/packages/?name=kcachegrind), Qt: [qcachegrind](https://www.archlinux.org/packages/?name=qcachegrind)

*   **[KDbg](https://en.wikipedia.org/wiki/KDbg "wikipedia:KDbg")** — Graphical user interface to GDB, the GNU debugger. It provides an intuitive interface for setting breakpoints, inspecting variables, and stepping through code.

	[http://kdbg.org/](http://kdbg.org/) || [kdbg](https://www.archlinux.org/packages/?name=kdbg)

*   **Massif-Visualizer** — Visualizer for Valgrind Massif data files.

	[https://phabricator.kde.org/source/massif-visualizer/](https://phabricator.kde.org/source/massif-visualizer/) || [massif-visualizer](https://www.archlinux.org/packages/?name=massif-visualizer)

*   **[Nemiver](https://en.wikipedia.org/wiki/Nemiver "wikipedia:Nemiver")** — Easy to use standalone C/C++ debugger (GDB front-end) that integrates well in the GNOME environment.

	[https://wiki.gnome.org/Apps/Nemiver](https://wiki.gnome.org/Apps/Nemiver) || [nemiver](https://www.archlinux.org/packages/?name=nemiver)

*   **Qt QDbusViewer** — Tool to introspect D-Bus objects and messages.

	[https://doc.qt.io/qt-5/qdbusviewer.html](https://doc.qt.io/qt-5/qdbusviewer.html) || [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools)

*   **scanmem** — Debugging utility designed to isolate the address of an arbitrary variable in an executing process.

	[https://github.com/scanmem/scanmem](https://github.com/scanmem/scanmem) || CLI: [scanmem](https://www.archlinux.org/packages/?name=scanmem), GUI: [gameconqueror](https://www.archlinux.org/packages/?name=gameconqueror)

*   **Sysprof** — Profiling tool that helps in finding the functions in which a program uses most of its time.

	[https://wiki.gnome.org/Apps/Sysprof](https://wiki.gnome.org/Apps/Sysprof) || [sysprof](https://www.archlinux.org/packages/?name=sysprof)

#### Lexing and parsing

[Lex](https://en.wikipedia.org/wiki/Lex_(software) and [Yacc](https://en.wikipedia.org/wiki/Yacc "wikipedia:Yacc") are part of POSIX.

*   **[flex](https://en.wikipedia.org/wiki/Flex_(lexical_analyser_generator) "wikipedia:Flex (lexical analyser generator)")** — A tool for generating text-scanning programs, alternative to Lex.

	[https://github.com/westes/flex](https://github.com/westes/flex) || [flex](https://www.archlinux.org/packages/?name=flex)

*   **[Berkeley Yacc](https://en.wikipedia.org/wiki/Berkeley_Yacc "wikipedia:Berkeley Yacc")** — Berkeley reimplementation of the Unix parser generator Yacc.

	[https://invisible-island.net/byacc/](https://invisible-island.net/byacc/) || [byacc](https://www.archlinux.org/packages/?name=byacc)

*   **[GNU Bison](https://en.wikipedia.org/wiki/GNU_bison "wikipedia:GNU bison")** — The GNU general-purpose parser generator, alternative to *byacc*.

	[https://www.gnu.org/software/bison/](https://www.gnu.org/software/bison/) || [bison](https://www.archlinux.org/packages/?name=bison)

And then there are also:

*   **[ANTLR](https://en.wikipedia.org/wiki/ANTLR "wikipedia:ANTLR")** — Parser generator, written in Java, for parsing structured text or binary files.

	[https://www.antlr.org/](https://www.antlr.org/) || [antlr4](https://www.archlinux.org/packages/?name=antlr4)

*   **LPeg** — Pattern-matching library, based on PEGs, for Lua.

	[http://www.inf.puc-rio.br/~roberto/lpeg/](http://www.inf.puc-rio.br/~roberto/lpeg/) || [lua-lpeg](https://www.archlinux.org/packages/?name=lua-lpeg), [lua52-lpeg](https://www.archlinux.org/packages/?name=lua52-lpeg), [lua51-lpeg](https://www.archlinux.org/packages/?name=lua51-lpeg)

*   **peg/leg** — Recursive-descent parser generators for C.

	[https://www.piumarta.com/software/peg/](https://www.piumarta.com/software/peg/) || [peg](https://www.archlinux.org/packages/?name=peg)

*   **Ragel** — Compiles finite state machines from regular languages into executable C, C++, Objective-C, or D code.

	[http://www.colm.net/open-source/ragel/](http://www.colm.net/open-source/ragel/) || [ragel](https://www.archlinux.org/packages/?name=ragel)

#### GUI builders

*   **[FLUID](https://en.wikipedia.org/wiki/FLUID "wikipedia:FLUID")** — FLTK GUI designer.

	[https://www.fltk.org/](https://www.fltk.org/) || [fltk](https://www.archlinux.org/packages/?name=fltk)

*   **[Glade](https://en.wikipedia.org/wiki/Glade_Interface_Designer "wikipedia:Glade Interface Designer")** — Create or open user interface designs for GTK applications.

	[https://glade.gnome.org/](https://glade.gnome.org/) || [glade](https://www.archlinux.org/packages/?name=glade)

*   **KUIViewer** — Quick viewer for Qt Designer UI File.

	[https://userbase.kde.org/KUIViewer](https://userbase.kde.org/KUIViewer) || [kde-dev-utils](https://www.archlinux.org/packages/?name=kde-dev-utils)

*   **Qt Designer** — Tool for designing and building graphical user interfaces (GUIs) with Qt Widgets.

	[https://doc.qt.io/qt-5/qtdesigner-manual.html](https://doc.qt.io/qt-5/qtdesigner-manual.html) || [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools)

#### Hex editors

See also [Wikipedia:Comparison of hex editors](https://en.wikipedia.org/wiki/Comparison_of_hex_editors "wikipedia:Comparison of hex editors").

*   **Bless** — High quality, full featured hex editor.

	[https://web.archive.org/web/20170503150524/http://home.gna.org/bless/](https://web.archive.org/web/20170503150524/http://home.gna.org/bless/) || [bless](https://aur.archlinux.org/packages/bless/)

*   **GHex** — Hex editor for GNOME, which allows the user to load data from any file, view and edit it in either hex or ascii.

	[https://wiki.gnome.org/Apps/Ghex](https://wiki.gnome.org/Apps/Ghex) || [ghex](https://www.archlinux.org/packages/?name=ghex)

*   **hyx** — Minimalistic but powerful console hex editor.

	[https://yx7.cc/code/](https://yx7.cc/code/) || [hyx](https://aur.archlinux.org/packages/hyx/)

*   **Okteta** — KDE hex editor for viewing and editing the raw data of files.

	[https://www.kde.org/applications/utilities/okteta/](https://www.kde.org/applications/utilities/okteta/) || [okteta](https://www.archlinux.org/packages/?name=okteta)

#### JSON tools

*   **gron** — gron transforms JSON into discrete assignments to make it easier to grep.

	[https://github.com/tomnomnom/gron](https://github.com/tomnomnom/gron) || [gron-bin](https://aur.archlinux.org/packages/gron-bin/)

*   **jid** — JSON incremental digger

	[https://github.com/simeji/jid](https://github.com/simeji/jid) || [jid](https://aur.archlinux.org/packages/jid/)

*   **jo** — A command to create JSON.

	[https://github.com/jpmens/jo](https://github.com/jpmens/jo) || [jo-git](https://aur.archlinux.org/packages/jo-git/)

*   **jq** — Command-line JSON processor

	[https://stedolan.github.io/jq/](https://stedolan.github.io/jq/) || [jq](https://www.archlinux.org/packages/?name=jq)

*   **jsawk** — Like awk, but for JSON.

	[https://github.com/micha/jsawk](https://github.com/micha/jsawk) || [jsawk-git](https://aur.archlinux.org/packages/jsawk-git/)

*   **jshon** — A JSON parser for the shell.

	[http://kmkeen.com/jshon/](http://kmkeen.com/jshon/) || [jshon](https://www.archlinux.org/packages/?name=jshon)

*   the [Elvish](/index.php/Elvish "Elvish") shell has built-in support for JSON

#### Literate programming

See also [Wikipedia:Literate programming](https://en.wikipedia.org/wiki/Literate_programming "wikipedia:Literate programming").

*   **Noweb** — A Simple, Extensible Tool for Literate Programming build against ICON libs and texlive

	[https://www.cs.tufts.edu/~nr/noweb/](https://www.cs.tufts.edu/~nr/noweb/) || [noweb](https://aur.archlinux.org/packages/noweb/)

*   **nuweb** — A Simple Literate Programming Tool

	[http://nuweb.sourceforge.net/](http://nuweb.sourceforge.net/) || [nuweb](https://aur.archlinux.org/packages/nuweb/)

#### UML modelers

See also [Wikipedia:List of Unified Modeling Language tools](https://en.wikipedia.org/wiki/List_of_Unified_Modeling_Language_tools "wikipedia:List of Unified Modeling Language tools").

*   **[ArgoUML](https://en.wikipedia.org/wiki/ArgoUML "wikipedia:ArgoUML")** — UML modeling tool with support for all standard UML 1.4 diagrams.

	[http://argouml.tigris.org/](http://argouml.tigris.org/) || [argouml](https://aur.archlinux.org/packages/argouml/)

*   **[Eclipse](/index.php/Eclipse "Eclipse") Modeling Tools** — Tools and runtimes for building model-based applications.

	[https://www.eclipse.org/](https://www.eclipse.org/) || [eclipse-modeling-tools](https://aur.archlinux.org/packages/eclipse-modeling-tools/)

*   **[Modelio](https://en.wikipedia.org/wiki/Modelio "wikipedia:Modelio")** — Modeling environment supporting the main standards: UML, BPMN, MDA, SysML.

	[https://www.modelio.org/](https://www.modelio.org/) || [modelio-bin](https://aur.archlinux.org/packages/modelio-bin/)

*   **[Papyrus](https://en.wikipedia.org/wiki/Papyrus_(software) "wikipedia:Papyrus (software)")** — Model-based engineering tool based on Eclipse.

	[https://www.eclipse.org/papyrus/](https://www.eclipse.org/papyrus/) || [papyrus](https://aur.archlinux.org/packages/papyrus/)

*   **[PlantUML](https://en.wikipedia.org/wiki/PlantUML "wikipedia:PlantUML")** — Tool to create UML diagrams from a plain text language.

	[http://plantuml.com/](http://plantuml.com/) || [plantuml](https://www.archlinux.org/packages/?name=plantuml)

*   **PlantUML QEditor** — PlantUML editor written in Qt.

	[https://github.com/borco/plantumlqeditor](https://github.com/borco/plantumlqeditor) || [plantumlqeditor-git](https://aur.archlinux.org/packages/plantumlqeditor-git/)

*   **[Umbrello](https://en.wikipedia.org/wiki/Umbrello_UML_Modeller "wikipedia:Umbrello UML Modeller")** — Unified Modelling Language (UML) diagram program based on KDE Technology.

	[https://umbrello.kde.org/](https://umbrello.kde.org/) || [umbrello](https://www.archlinux.org/packages/?name=umbrello)

*   **[UML Designer](https://en.wikipedia.org/wiki/UML_Designer "wikipedia:UML Designer")** — Graphical tool based on Eclipse to edit and visualize UML models.

	[http://www.umldesigner.org/](http://www.umldesigner.org/) || [umldesigner](https://aur.archlinux.org/packages/umldesigner/)

*   **[UMLet](https://en.wikipedia.org/wiki/UMLet "wikipedia:UMLet")** — UML tool with a simple user interface: draw UML diagrams fast, build sequence and activity diagrams from plain text, export diagrams to eps, pdf, jpg, svg, and clipboard, share diagrams using Eclipse, and create new, custom UML elements.

	[http://umlet.com/](http://umlet.com/) || [umlet](https://aur.archlinux.org/packages/umlet/)

*   **UML/INTERLIS-editor** — Facilitate the application of the model driven approach to a greater number of users.

	[http://www.umleditor.org/](http://www.umleditor.org/) || [umleditor](https://aur.archlinux.org/packages/umleditor/)

*   **Violet** — Very easy to learn and use UML editor that draws nice-looking diagrams.

	[https://sourceforge.net/projects/violet/](https://sourceforge.net/projects/violet/) || [violetumleditor](https://aur.archlinux.org/packages/violetumleditor/)

#### API documentation browsers

*   **[Devhelp](https://en.wikipedia.org/wiki/GNOME_Devhelp "wikipedia:GNOME Devhelp")** — Developer tool for browsing and searching API documentation.

	[https://wiki.gnome.org/Apps/Devhelp](https://wiki.gnome.org/Apps/Devhelp) || [devhelp](https://www.archlinux.org/packages/?name=devhelp)

*   **Doc Browser** — API documentation browser with support for DevDocs and Hoogle.

	[https://github.com/qwfy/doc-browser](https://github.com/qwfy/doc-browser) || [doc-browser-git](https://aur.archlinux.org/packages/doc-browser-git/)

*   **Qt Assistant** — Tool for viewing on-line documentation in Qt help file format.

	[https://doc.qt.io/qt-5/qtassistant-index.html](https://doc.qt.io/qt-5/qtassistant-index.html) || [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools)

*   **quickDocs** — Fast developer docs reader for reading Valadoc and DevDocs.

	[https://github.com/mdh34/quickDocs](https://github.com/mdh34/quickDocs) || [quickdocs](https://aur.archlinux.org/packages/quickdocs/)

*   **Zeal** — Offline API documentation browser for software developers.

	[https://zealdocs.org/](https://zealdocs.org/) || [zeal](https://www.archlinux.org/packages/?name=zeal)

#### Issue tracking systems

*   **[Bugzilla](/index.php/Bugzilla "Bugzilla")** — Bug tracker from Mozilla.

	[https://www.bugzilla.org](https://www.bugzilla.org) || [bugzilla](https://www.archlinux.org/packages/?name=bugzilla)

*   **[Flyspray](/index.php/Flyspray "Flyspray")** — Lightweight, web-based bug tracking system written in PHP

	[https://www.flyspray.org/](https://www.flyspray.org/) || [flyspray](https://www.archlinux.org/packages/?name=flyspray)

*   **[MantisBT](/index.php/MantisBT "MantisBT")** — Web-based issue tracking system

	[https://www.mantisbt.org/](https://www.mantisbt.org/) || [mantisbt](https://aur.archlinux.org/packages/mantisbt/)

*   **[Redmine](/index.php/Redmine "Redmine")** — A flexible project management web application. Written using the Ruby on Rails, it is cross-platform and cross-database.

	[https://www.redmine.org](https://www.redmine.org) || [redmine](https://www.archlinux.org/packages/?name=redmine)

*   **[Request Tracker](/index.php/Request_Tracker "Request Tracker") (RT)** — The leading open-source issue tracking system.

	[https://bestpractical.com/rt/](https://bestpractical.com/rt/) || [rt](https://aur.archlinux.org/packages/rt/)

*   **[Trac](/index.php/Trac "Trac")** — Trac Integrated SCM & Project Management using Apache & Subversion.

	[https://trac.edgewall.org/](https://trac.edgewall.org/) || [trac](https://aur.archlinux.org/packages/trac/)

See also [Git server#Advanced web applications](/index.php/Git_server#Advanced_web_applications "Git server").

#### Code review

*   **Gerrit** — A web-based code review tool built on top of the Git version control system

	[https://www.gerritcodereview.com/](https://www.gerritcodereview.com/) || [gerrit](https://aur.archlinux.org/packages/gerrit/)

*   [GitLab](/index.php/GitLab "GitLab") also supports code reviews.

See also [Wikipedia:List of tools for code review](https://en.wikipedia.org/wiki/List_of_tools_for_code_review "wikipedia:List of tools for code review").

#### Game development

See also [Wikipedia:List of game engines](https://en.wikipedia.org/wiki/List_of_game_engines "wikipedia:List of game engines").

*   **GDevelop** — Game creator designed to be used by everyone - no programming skills required.

	[https://gdevelop-app.com/](https://gdevelop-app.com/) || [gdevelop](https://aur.archlinux.org/packages/gdevelop/)

*   **[Godot](/index.php/Godot_Engine "Godot Engine")** — Advanced, feature-packed, multi-platform 2D and 3D game engine. Create games with ease, using Godot's unique approach to game development.

	[https://godotengine.org/](https://godotengine.org/) || [godot](https://aur.archlinux.org/packages/godot/)

*   **LibreSprite** — Animated sprite editor and pixel art tool lets you create 2D animations for videogames.

	[https://github.com/LibreSprite/LibreSprite](https://github.com/LibreSprite/LibreSprite) || [libresprite](https://aur.archlinux.org/packages/libresprite/)

*   **Tiled** — General purpose 2D level editor with powerful tile map editing features. It’s built to be easy to use and is suitable for many type of games.

	[https://www.mapeditor.org/](https://www.mapeditor.org/) || [tiled](https://www.archlinux.org/packages/?name=tiled)

#### Repository managers

*   **Nexus 2** — Nexus 2 Repository Manager (OSS)

	[https://www.sonatype.com/nexus-repository-oss](https://www.sonatype.com/nexus-repository-oss) || [nexus](https://aur.archlinux.org/packages/nexus/)

*   **Nexus 3** — Nexus 3 Repository OSS

	[https://www.sonatype.com/nexus-repository-oss](https://www.sonatype.com/nexus-repository-oss) || [nexus-oss](https://aur.archlinux.org/packages/nexus-oss/)

*   **Artifactory** — Artifactory is an advanced Binary Repository Manager for use by build tools, dependency management tools and build servers

	[https://bintray.com/jfrog/product/JFrog-Artifactory-Oss/view](https://bintray.com/jfrog/product/JFrog-Artifactory-Oss/view) || [artifactory-oss](https://aur.archlinux.org/packages/artifactory-oss/)

### Text input

#### Character selectors

*   **GNOME Characters** — Character map application for GNOME.

	[https://gitlab.gnome.org/GNOME/gnome-characters](https://gitlab.gnome.org/GNOME/gnome-characters) || [gnome-characters](https://www.archlinux.org/packages/?name=gnome-characters)

*   **[gucharmap](https://en.wikipedia.org/wiki/GNOME_Character_Map "wikipedia:GNOME Character Map")** — GTK 3 character selector for GNOME.

	[https://wiki.gnome.org/Apps/Gucharmap](https://wiki.gnome.org/Apps/Gucharmap) || [gucharmap](https://www.archlinux.org/packages/?name=gucharmap)

*   **KCharSelect** — Tool to select special characters from all installed fonts and copy them into the clipboard. Part of [kdeutils](https://www.archlinux.org/groups/x86_64/kdeutils/).

	[https://utils.kde.org/projects/kcharselect/](https://utils.kde.org/projects/kcharselect/) || [kcharselect](https://www.archlinux.org/packages/?name=kcharselect)

#### On-screen keyboards

*   **CellWriter** — Grid-entry handwriting recognition input panel.

	[https://github.com/risujin/cellwriter](https://github.com/risujin/cellwriter) || [cellwriter](https://www.archlinux.org/packages/?name=cellwriter)

*   **eekboard** — Easy to use virtual keyboard toolkit.

	[https://github.com/ueno/eekboard](https://github.com/ueno/eekboard) || [eekboard](https://aur.archlinux.org/packages/eekboard/)

*   **Florence** — Extensible scalable on-screen virtual keyboard for GNOME that stays out of your way when not needed.

	[https://sourceforge.net/projects/florence/](https://sourceforge.net/projects/florence/) || [florence](https://aur.archlinux.org/packages/florence/)

*   **Onboard** — Onscreen keyboard useful for tablet PC users and for mobility impaired users.

	[https://launchpad.net/onboard](https://launchpad.net/onboard) || [onboard](https://www.archlinux.org/packages/?name=onboard)

*   **qtvkbd** — Virtual keyboard written in Qt, a fork of kvkbd.

	[https://github.com/Alexander-r/qtvkbd](https://github.com/Alexander-r/qtvkbd) || [qtvkbd](https://aur.archlinux.org/packages/qtvkbd/)

*   **QVKbd** — Virtual keyboard written in Qt.

	[https://github.com/KivApple/qvkbd](https://github.com/KivApple/qvkbd) || [qvkbd](https://www.archlinux.org/packages/?name=qvkbd)

*   **theShell On Screen Keyboard** — Touchscreen keyboard for theShell.

	[https://github.com/vicr123/ts-kbd](https://github.com/vicr123/ts-kbd) || [ts-kbd](https://aur.archlinux.org/packages/ts-kbd/)

*   **xvkbd** — Virtual keyboard for X window system.

	[http://t-sato.in.coocan.jp/xvkbd/](http://t-sato.in.coocan.jp/xvkbd/) || [xvkbd](https://aur.archlinux.org/packages/xvkbd/)

#### Keyboard layout switchers

*   **fbxkb** — A NETWM compliant keyboard indicator and switcher. It shows a flag of current keyboard in a systray area and allows you to switch to another one.

	[http://fbxkb.sourceforge.net/](http://fbxkb.sourceforge.net/) || [fbxkb](https://aur.archlinux.org/packages/fbxkb/)

*   **xxkb** — A lightweight keyboard layout indicator and switcher.

	[https://sourceforge.net/projects/xxkb/](https://sourceforge.net/projects/xxkb/) || [xxkb](https://www.archlinux.org/packages/?name=xxkb)

*   **qxkb** — A keyboard switcher written in Qt.

	[https://github.com/disels/qxkb](https://github.com/disels/qxkb) || [qxkb](https://aur.archlinux.org/packages/qxkb/)

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — A text analyser, it detects the language of the input and corrects the keyboard layout if needed.

	[https://xneur.ru/](https://xneur.ru/) || [xneur](https://aur.archlinux.org/packages/xneur/), [gxneur](https://aur.archlinux.org/packages/gxneur/) (GUI)

#### Keybinding managers

See [Keyboard shortcuts#Xorg](/index.php/Keyboard_shortcuts#Xorg "Keyboard shortcuts").

#### Input methods

See the main article: [Internationalization#Input methods](/index.php/Internationalization#Input_methods "Internationalization").

### Disks

#### Partitioning tools

See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

#### Formatting tools

See [File systems#Types of file systems](/index.php/File_systems#Types_of_file_systems "File systems").

#### Cloning tools

See [Disk cloning#Disk cloning software](/index.php/Disk_cloning#Disk_cloning_software "Disk cloning").

#### Mount tools

See also [udisks#Mount helpers](/index.php/Udisks#Mount_helpers "Udisks").

*   **9mount** — Mount 9p filesystems.

	[http://sqweek.net/code/9mount/](http://sqweek.net/code/9mount/) || [9mount](https://aur.archlinux.org/packages/9mount/)

*   **cryptmount** — Mount an encrypted file system as a regular user.

	[https://sourceforge.net/projects/cryptmount/](https://sourceforge.net/projects/cryptmount/) || [cryptmount](https://aur.archlinux.org/packages/cryptmount/)

*   **KDiskFree** — Displays information about hard disks and other storage devices. It also allows to mount and unmount drives and view them in a file manager.

	[https://www.kde.org/applications/system/kdiskfree/](https://www.kde.org/applications/system/kdiskfree/) || [kdf](https://www.archlinux.org/packages/?name=kdf)

*   **ldm** — A lightweight daemon that mounts drives automagically using *udev*

	[https://github.com/LemonBoy/ldm](https://github.com/LemonBoy/ldm) || [ldm](https://aur.archlinux.org/packages/ldm/)

*   **pmount** — Mount *source* as a regular user to an automatically created destination `/media/*source_name*`.

	[https://pmount.alioth.debian.org/](https://pmount.alioth.debian.org/) || [pmount](https://aur.archlinux.org/packages/pmount/)

*   **pmount-safe-removal** — Mount removable devices as regular user with safe removal

	[https://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device](https://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device) || [pmount-safe-removal](https://aur.archlinux.org/packages/pmount-safe-removal/)

*   **udevil** — Mounts removable devices as a regular user, show device info, and monitor device changes. Only depends on *udev* and glib.

	[https://ignorantguru.github.io/udevil](https://ignorantguru.github.io/udevil) || [udevil](https://www.archlinux.org/packages/?name=udevil)

*   **ws** — Mount Windows network shares ([CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") and [VFS](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system")).

	[https://sourceforge.net/projects/winshares/](https://sourceforge.net/projects/winshares/) || [ws](https://aur.archlinux.org/packages/ws/)

*   **zulucrypt** — A GUI frontend for cryptsetup to create, manage and mount encrypted volumes; supports encfs as well

	[https://mhogomchungu.github.io/zuluCrypt/](https://mhogomchungu.github.io/zuluCrypt/) || [zulucrypt](https://aur.archlinux.org/packages/zulucrypt/)

#### Disk usage display

*   **duc** — A library and suite of tools for inspecting disk usage.

	[https://duc.zevv.nl/](https://duc.zevv.nl/) || [duc](https://aur.archlinux.org/packages/duc/)

*   **[Filelight](https://en.wikipedia.org/wiki/Filelight "wikipedia:Filelight")** — Disk usage analyzer that creates an interactive map of concentric, segmented rings that help visualise disk usage on your computer.

	[https://www.kde.org/applications/utilities/filelight](https://www.kde.org/applications/utilities/filelight) || [filelight](https://www.archlinux.org/packages/?name=filelight)

*   **[GNOME Disk Usage Analyzer](https://en.wikipedia.org/wiki/Disk_Usage_Analyzer "wikipedia:Disk Usage Analyzer")** — Disk usage analyzer for the [GNOME](/index.php/GNOME "GNOME") desktop to check folder sizes and available disk space.

	[https://wiki.gnome.org/Apps/DiskUsageAnalyzer](https://wiki.gnome.org/Apps/DiskUsageAnalyzer) || [baobab](https://www.archlinux.org/packages/?name=baobab)

*   **Graphical Disk Map** — Disk usage analyzer that draws a map of rectangles sized according to file or dir sizes.

	[http://gdmap.sourceforge.net/](http://gdmap.sourceforge.net/) || [gdmap](https://www.archlinux.org/packages/?name=gdmap)

*   **gt5** — Diff-capable "du-browser".

	[http://gt5.sourceforge.net](http://gt5.sourceforge.net) || [gt5](https://aur.archlinux.org/packages/gt5/)

*   **MATE Disk Usage Analyzer** — Disk usage analyzing tool for MATE Desktop.

	[https://github.com/mate-desktop/mate-utils](https://github.com/mate-desktop/mate-utils) || [mate-utils](https://www.archlinux.org/packages/?name=mate-utils)

*   **ncdu** — Simple ncurses disk usage analyzer.

	[https://dev.yorhel.nl/ncdu](https://dev.yorhel.nl/ncdu) || [ncdu](https://www.archlinux.org/packages/?name=ncdu)

*   **qdirstat** — Qt-based directory statistics (KDirStat/K4DirStat without any KDE - from the original KDirStat author).

	[https://github.com/shundhammer/qdirstat](https://github.com/shundhammer/qdirstat) || [qdirstat](https://aur.archlinux.org/packages/qdirstat/)

#### Disk health status

See [S.M.A.R.T.#GUI Applications](/index.php/S.M.A.R.T.#GUI_Applications "S.M.A.R.T.").

#### File recovery tools

See [File recovery#List of utilities](/index.php/File_recovery#List_of_utilities "File recovery").

#### Disk cleaning

*   **[BleachBit](https://en.wikipedia.org/wiki/BleachBit "wikipedia:BleachBit")** — Frees disk space and guards your privacy; frees cache, deletes cookies, clears Internet history, shreds temporary files, deletes logs, and discards junk you didn't know was there.

	[https://www.bleachbit.org/](https://www.bleachbit.org/) || [bleachbit](https://www.archlinux.org/packages/?name=bleachbit)

*   **[fdupes](https://en.wikipedia.org/wiki/fdupes "wikipedia:fdupes")** — Program for identifying or deleting duplicate files residing within specified directories.

	[https://github.com/adrianlopezroche/fdupes](https://github.com/adrianlopezroche/fdupes) || [fdupes](https://www.archlinux.org/packages/?name=fdupes)

*   **fslint** — A utility to find and clean various forms of lint on a filesystem.

	[https://www.pixelbeat.org/fslint/](https://www.pixelbeat.org/fslint/) || [fslint](https://aur.archlinux.org/packages/fslint/)

*   **gconf-cleaner** — cleans up the unknown/invalid GConf keys that still sitting down on your GConf database.

	[https://code.google.com/archive/p/gconf-cleaner/](https://code.google.com/archive/p/gconf-cleaner/) || [gconf-cleaner](https://aur.archlinux.org/packages/gconf-cleaner/)

*   **rmlint** — Tool to quickly find (and optionally remove) duplicate files and other lint.

	[https://github.com/sahib/rmlint](https://github.com/sahib/rmlint) || CLI: [rmlint](https://www.archlinux.org/packages/?name=rmlint), GUI: [rmlint-shredder](https://www.archlinux.org/packages/?name=rmlint-shredder)

*   **Sweeper** — System cleaning utility for KDE.

	[https://utils.kde.org/projects/sweeper/](https://utils.kde.org/projects/sweeper/) || [sweeper](https://www.archlinux.org/packages/?name=sweeper)

#### Disk image writing

See also [Wikipedia:List of tools to create Live USB systems](https://en.wikipedia.org/wiki/List_of_tools_to_create_Live_USB_systems "wikipedia:List of tools to create Live USB systems").

*   **Deepin Boot Maker** — Tool to make boot disk for Deepin OS.

	[https://www.deepin.org/en/original/deepin-boot-maker/](https://www.deepin.org/en/original/deepin-boot-maker/) || [deepin-boot-maker](https://www.archlinux.org/packages/?name=deepin-boot-maker)

*   **Etcher** — Flash OS images to SD cards & USB drives, safely and easily. Based on the [Electron](https://electronjs.org/) platform.

	[https://etcher.io/](https://etcher.io/) || [balena-etcher](https://aur.archlinux.org/packages/balena-etcher/)

*   **[Fedora Media Writer](https://en.wikipedia.org/wiki/Fedora_Media_Writer "wikipedia:Fedora Media Writer")** — Tool that helps users put Fedora images on their portable drives such as flash disks.

	[https://github.com/FedoraQt/MediaWriter](https://github.com/FedoraQt/MediaWriter) || [mediawriter](https://aur.archlinux.org/packages/mediawriter/)

*   **GNOME MultiWriter** — Write an ISO file to multiple USB devices at once.

	[https://wiki.gnome.org/Apps/MultiWriter](https://wiki.gnome.org/Apps/MultiWriter) || [gnome-multi-writer](https://www.archlinux.org/packages/?name=gnome-multi-writer)

*   **ISOImageWriter** — Tool to write a .iso file to a USB disk.

	[https://community.kde.org/ISOImageWriter](https://community.kde.org/ISOImageWriter) || [isoimagewriter](https://aur.archlinux.org/packages/isoimagewriter/)

*   **LiveUSB Install** — Install various Linux distributions and operating systems on removable flash drive or external disk drive.

	[http://live.learnfree.eu/](http://live.learnfree.eu/) || [live-usb-install](https://aur.archlinux.org/packages/live-usb-install/)

*   **MultiBootUSB** — Install multiple live Linux on a USB disk non destructively and option to uninstall distros.

	[http://multibootusb.org/](http://multibootusb.org/) || [multibootusb](https://aur.archlinux.org/packages/multibootusb/)

*   **MultiSystem** — GUI tool to create a USB system that can boot multiple distro's.

	[http://liveusb.info/](http://liveusb.info/) || [multisystem](https://aur.archlinux.org/packages/multisystem/)

*   **[SUSE Studio ImageWriter](https://en.wikipedia.org/wiki/SUSE_Studio_ImageWriter "wikipedia:SUSE Studio ImageWriter")** — Utility for writing raw disk images & hybrid isos to USB keys.

	[https://github.com/openSUSE/imagewriter](https://github.com/openSUSE/imagewriter) || [imagewriter](https://aur.archlinux.org/packages/imagewriter/)

*   **[UNetbootin](https://en.wikipedia.org/wiki/UNetbootin "wikipedia:UNetbootin")** — Installs Linux/BSD distributions to a partition or USB drive.

	[https://unetbootin.github.io/](https://unetbootin.github.io/) || [unetbootin](https://aur.archlinux.org/packages/unetbootin/)

*   **WoeUSB** — Simple tool to create USB stick windows installer from an ISO image or a real DVD. (Fork of WinUSB).

	[https://github.com/WoeUSB/WoeUSB-frontend-wxgtk](https://github.com/WoeUSB/WoeUSB-frontend-wxgtk) || [woeusb-git](https://aur.archlinux.org/packages/woeusb-git/)

*   **windows2usb** — Windows 7/8/8.1/10 ISO to Flash Drive burning utility for Linux with MBR/GPT, BIOS/UEFI, FAT32/NTFS support

	[https://github.com/ValdikSS/windows2usb](https://github.com/ValdikSS/windows2usb) || [windows2usb-git](https://aur.archlinux.org/packages/windows2usb-git/)

### System

#### Task managers

*   **Deepin System Monitor** — Monitor system process status for Deepin desktop.

	[https://www.deepin.org/en/original/deepin-system-monitor/](https://www.deepin.org/en/original/deepin-system-monitor/) || [deepin-system-monitor](https://www.archlinux.org/packages/?name=deepin-system-monitor)

*   **GNOME System Monitor** — System monitor for [GNOME](/index.php/GNOME "GNOME") to view and manage system resources.

	[https://wiki.gnome.org/Apps/SystemMonitor](https://wiki.gnome.org/Apps/SystemMonitor) || [gnome-system-monitor](https://www.archlinux.org/packages/?name=gnome-system-monitor)

*   **GNOME Usage** — View information about use of system resources, like memory and disk space.

	[https://wiki.gnome.org/Apps/Usage](https://wiki.gnome.org/Apps/Usage) || [gnome-usage](https://www.archlinux.org/packages/?name=gnome-usage)

*   **[htop](https://en.wikipedia.org/wiki/Htop "wikipedia:Htop")** — Simple, ncurses interactive process viewer.

	[http://htop.sourceforge.net/](http://htop.sourceforge.net/) || [htop](https://www.archlinux.org/packages/?name=htop)

*   **[KSysGuard](https://en.wikipedia.org/wiki/KDE_System_Guard "wikipedia:KDE System Guard")** — System monitor for [KDE](/index.php/KDE "KDE") to monitor running processes and system performance.

	[https://userbase.kde.org/KSysGuard](https://userbase.kde.org/KSysGuard) || [ksysguard](https://www.archlinux.org/packages/?name=ksysguard)

*   **Linux Process Explorer** — Graphical process explorer for Linux.

	[https://sourceforge.net/projects/procexp/](https://sourceforge.net/projects/procexp/) || [procexp](https://aur.archlinux.org/packages/procexp/)

*   **LXTask** — Lightweight task manager for [LXDE](/index.php/LXDE "LXDE").

	[https://wiki.lxde.org/en/LXTask](https://wiki.lxde.org/en/LXTask) || [lxtask](https://www.archlinux.org/packages/?name=lxtask)

*   **MATE System Monitor** — System monitor for [MATE](/index.php/MATE "MATE").

	[https://github.com/mate-desktop/mate-system-monitor](https://github.com/mate-desktop/mate-system-monitor) || [mate-system-monitor](https://www.archlinux.org/packages/?name=mate-system-monitor)

*   **Task Manager** — GTK2 process management application for [Xfce](/index.php/Xfce "Xfce").

	[https://goodies.xfce.org/projects/applications/xfce4-taskmanager](https://goodies.xfce.org/projects/applications/xfce4-taskmanager) || [xfce4-taskmanager](https://www.archlinux.org/packages/?name=xfce4-taskmanager)

#### System monitors

See also [Category:Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification")

*   **[Conky](/index.php/Conky "Conky")** — Lightweight, scriptable system monitor.

	[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **Collectd** — Simple, extensible system monitoring daemon based on [rrdtool](http://oss.oetiker.ch/rrdtool/). It has a small footprint and can be set up either stand-alone or as a server/client application.

	[https://collectd.org/](https://collectd.org/) || [collectd](https://www.archlinux.org/packages/?name=collectd)

*   **collectl** — Collectl is a light-weight performance monitoring tool capable of reporting interactively as well as logging to disk. It reports statistics on cpu, disk, infiniband, lustre, memory, network, nfs, process, quadrics, slabs and more in easy to read format.

	[http://collectl.sourceforge.net/](http://collectl.sourceforge.net/) || [collectl](https://aur.archlinux.org/packages/collectl/)

*   **dstat** — Versatile resource statistics tool.

	[http://dag.wiee.rs/home-made/dstat/](http://dag.wiee.rs/home-made/dstat/) || [dstat](https://www.archlinux.org/packages/?name=dstat)

*   **Fsniper** — Daemon to run scripts based on changes in files monitored by inotify.

	[http://projects.l3ib.org/fsniper/](http://projects.l3ib.org/fsniper/) || [fsniper](https://aur.archlinux.org/packages/fsniper/)

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — Simple, flexible system monitor package for [GTK](/index.php/GTK "GTK") with many plug-ins.

	[http://billw2.github.io/gkrellm/gkrellm.html](http://billw2.github.io/gkrellm/gkrellm.html) || [gkrellm](https://www.archlinux.org/packages/?name=gkrellm)

*   **glances** — CLI curses-based monitoring tool in Python.

	[https://nicolargo.github.io/glances/](https://nicolargo.github.io/glances/) || [glances](https://www.archlinux.org/packages/?name=glances)

*   **netdata** — Web-based real-time performance monitor.

	[https://github.com/firehol/netdata/wiki](https://github.com/firehol/netdata/wiki) || [netdata](https://www.archlinux.org/packages/?name=netdata)

*   **[Telegraf](/index.php/Telegraf "Telegraf")** — Agent written in Go for collecting, processing, aggregating, and writing metrics.

	[https://docs.influxdata.com/telegraf/latest/](https://docs.influxdata.com/telegraf/latest/) || [telegraf](https://aur.archlinux.org/packages/telegraf/)

*   **[Paramano](/index.php/Paramano "Paramano")** — Light battery monitor and a CPU frequency scaler. Forked from [trayfreq](http://trayfreq.sourceforge.net/)

	[https://github.com/phillid/paramano](https://github.com/phillid/paramano) || [paramano](https://aur.archlinux.org/packages/paramano/)

*   **Sysstat** — Collection of resource monitoring tools: iostat, isag, mpstat, pidstat, sadf, sar.

	[http://sebastien.godard.pagesperso-orange.fr/](http://sebastien.godard.pagesperso-orange.fr/) || [sysstat](https://www.archlinux.org/packages/?name=sysstat)

*   **xosview** — System monitor that resembles gr_osview from SGI IRIX.

	[http://www.pogo.org.uk/~mark/xosview/](http://www.pogo.org.uk/~mark/xosview/) || [xosview](https://aur.archlinux.org/packages/xosview/)

*   **zps** — A small utility for listing and reaping zombie processes on GNU/Linux.

	[https://github.com/orhun/zps](https://github.com/orhun/zps) || [zps](https://aur.archlinux.org/packages/zps/)

#### Hardware sensor monitoring

See [lm_sensors#Graphical front-ends](/index.php/Lm_sensors#Graphical_front-ends "Lm sensors").

#### System information viewers

##### Console

*   **alsi** — A system information tool for Arch Linux. It can be configured for every other system without even touching the source code of the script.

	[https://trizenx.blogspot.com/2012/08/alsi.html](https://trizenx.blogspot.com/2012/08/alsi.html) || [alsi](https://aur.archlinux.org/packages/alsi/)

*   **[archey3](/index.php/Archey3 "Archey3")** — Python script to display system infomation alongside the Arch Linux logo.

	[https://lclarkmichalek.github.io/archey3](https://lclarkmichalek.github.io/archey3) || [archey3](https://www.archlinux.org/packages/?name=archey3)

*   **dmidecode** — It reports information about your system's hardware as described in your system BIOS according to the SMBIOS/DMI standard.

	[http://www.nongnu.org/dmidecode/](http://www.nongnu.org/dmidecode/) || [dmidecode](https://www.archlinux.org/packages/?name=dmidecode)

*   **hwdetect** — Simple script to list modules that are exported in `/sys/`.

	[https://projects.archlinux.org/](https://projects.archlinux.org/) || [hwdetect](https://www.archlinux.org/packages/?name=hwdetect)

*   **hwinfo** — Powerful hardware detection tool come from openSUSE.

	[https://github.com/openSUSE/hwinfo](https://github.com/openSUSE/hwinfo) || [hwinfo](https://www.archlinux.org/packages/?name=hwinfo)

*   **inxi** — A script to get system information.

	[https://github.com/smxi/inxi](https://github.com/smxi/inxi) || [inxi](https://aur.archlinux.org/packages/inxi/)

*   **neofetch** — A fast, highly customizable system info script that supports displaying images with w3m.

	[https://github.com/dylanaraps/neofetch](https://github.com/dylanaraps/neofetch) || [neofetch](https://www.archlinux.org/packages/?name=neofetch)

*   **screenfetch** — Similar to archey but has an option to take a screenshot. Written in bash.

	[https://github.com/KittyKatt/screenFetch](https://github.com/KittyKatt/screenFetch) || [screenfetch](https://www.archlinux.org/packages/?name=screenfetch)

*   **nmon** — Console based application for monitoring various system components.

	[http://nmon.sourceforge.net/](http://nmon.sourceforge.net/) || [nmon](https://www.archlinux.org/packages/?name=nmon)

##### Graphical

*   **hardinfo** — A small application that displays information about your hardware and operating system, it looks like the Device Manager in Windows.

	[https://www.berlios.de/software/hardinfo/](https://www.berlios.de/software/hardinfo/) || [hardinfo](https://www.archlinux.org/packages/?name=hardinfo)

*   **i-Nex** — An application that gathers information for hardware components available on your system and displays it using an user interface similar to the popular Windows tool CPU-Z.

	[http://i-nex.linux.pl/](http://i-nex.linux.pl/) || [i-nex-git](https://aur.archlinux.org/packages/i-nex-git/)

*   **lshw** — A small tool to provide detailed information on the hardware configuration of the machine with CLI and GTK interfaces.

	[https://ezix.org/project/wiki/HardwareLiSter](https://ezix.org/project/wiki/HardwareLiSter) || [lshw](https://www.archlinux.org/packages/?name=lshw)

*   **KDE Info Center** — Centralized and convenient overview of system information for KDE.

	[https://www.kde.org/applications/system/kinfocenter/](https://www.kde.org/applications/system/kinfocenter/) || [kinfocenter](https://www.archlinux.org/packages/?name=kinfocenter)

*   **USBView** — Display the topology of devices on the USB bus.

	[http://www.kroah.com/linux/usb/](http://www.kroah.com/linux/usb/) || [usbview](https://www.archlinux.org/packages/?name=usbview)

#### System log viewers

*   **GNOME Logs** — Viewer for the systemd journal. Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Apps/Logs](https://wiki.gnome.org/Apps/Logs) || [gnome-logs](https://www.archlinux.org/packages/?name=gnome-logs)

*   **GNOME System Log** — System log viewer for GNOME.

	[https://gitlab.gnome.org/GNOME/gnome-system-log](https://gitlab.gnome.org/GNOME/gnome-system-log) || [gnome-system-log](https://www.archlinux.org/packages/?name=gnome-system-log)

*   **KSystemLog** — System log viewer tool for KDE.

	[https://www.kde.org/applications/system/ksystemlog/](https://www.kde.org/applications/system/ksystemlog/) || [ksystemlog](https://www.archlinux.org/packages/?name=ksystemlog)

*   **MATE System Log** — System log viewer for MATE.

	[https://github.com/mate-desktop/mate-utils](https://github.com/mate-desktop/mate-utils) || [mate-utils](https://www.archlinux.org/packages/?name=mate-utils)

*   **Pacman Log Viewer** — Tool used to inspect pacman log file, in particular it lists installed, removed and upgraded packages letting you to filter by package's name and/or date.

	[https://www.opendesktop.org/content/show.php?content=150484](https://www.opendesktop.org/content/show.php?content=150484) || [pacmanlogviewer](https://www.archlinux.org/packages/?name=pacmanlogviewer)

#### Font viewers

See also [Wikipedia:Font management software](https://en.wikipedia.org/wiki/Font_management_software "wikipedia:Font management software").

*   **Font Manager** — Simple font management for GTK desktop environments.

	[https://fontmanager.github.io/](https://fontmanager.github.io/) || [font-manager](https://aur.archlinux.org/packages/font-manager/)

*   **Fonty Python** — Manage, view and find your fonts.

	[https://savannah.nongnu.org/projects/fontypython](https://savannah.nongnu.org/projects/fontypython) || [fontypython](https://aur.archlinux.org/packages/fontypython/)

*   **GNOME Fonts** — Font viewer for GNOME.

	[https://gitlab.gnome.org/GNOME/gnome-font-viewer](https://gitlab.gnome.org/GNOME/gnome-font-viewer) || [gnome-font-viewer](https://www.archlinux.org/packages/?name=gnome-font-viewer)

*   **KFontview** — KDE application to view and install different types of fonts.

	[https://docs.kde.org/trunk5/en/kde-workspace/kfontview/index.html](https://docs.kde.org/trunk5/en/kde-workspace/kfontview/index.html) || [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop)

*   **MATE Font Viewer** — Font viewer for MATE.

	[https://github.com/mate-desktop/mate-control-center](https://github.com/mate-desktop/mate-control-center) || [mate-utils](https://www.archlinux.org/packages/?name=mate-utils)

*   **Waterfall** — GTK application to view all characters of font in all sizes.

	[https://keithp.com/cgit/gwaterfall.git](https://keithp.com/cgit/gwaterfall.git) || [gwaterfall](https://www.archlinux.org/packages/?name=gwaterfall)

#### Help viewers

See [man page#Viewer applications](/index.php/Man_page#Viewer_applications "Man page").

#### Command schedulers

See also [Cron](/index.php/Cron "Cron").

*   **FcronQ** — Fcron GUI, an advanced periodic command scheduler.

	[http://fcronq.xavion.name/](http://fcronq.xavion.name/) || [fcronq](https://aur.archlinux.org/packages/fcronq/)

*   **GNOME Schedule** — Graphical interface to crontab and at for GNOME.

	[http://gnome-schedule.sourceforge.net/](http://gnome-schedule.sourceforge.net/) || [gnome-schedule](https://aur.archlinux.org/packages/gnome-schedule/)

*   **KCron** — Tool for KDE to run applications in the background at regular intervals. It's a graphical interface to the Cron command.

	[https://userbase.kde.org/KCron](https://userbase.kde.org/KCron) || [kcron](https://www.archlinux.org/packages/?name=kcron)

*   **KTimer** — Little tool for KDE to execute programs after some time. It allows you to enter several tasks and to set a timer for each of them. The timers for each task can be started, stopped, changed, or looped.

	[https://www.kde.org/applications/utilities/ktimer/](https://www.kde.org/applications/utilities/ktimer/) || [ktimer](https://www.archlinux.org/packages/?name=ktimer)

#### Shutdown timers

*   **GShutdown** — Advanced shutdown utility which allows you to schedule the shutdown or the restart of your computer, or logout your actual session.

	[https://gshutdown.tuxfamily.org/](https://gshutdown.tuxfamily.org/) || [gshutdown](https://aur.archlinux.org/packages/gshutdown/)

*   **Hsiu-Ming's Timer** — Graphical shutdown timer, which enables you to shutdown, turn off monitor, reboot or play sound after a period of time.

	[https://cges30901.github.io/hmtimer-website/](https://cges30901.github.io/hmtimer-website/) || [hmtimer](https://aur.archlinux.org/packages/hmtimer/)

*   **KShutdown** — Graphical shutdown utility, which allows you to turn off or suspend a computer at a specified time. It features various time and delay options, command-line support, and notifications.

	[https://kshutdown.sourceforge.io/](https://kshutdown.sourceforge.io/) || [kshutdown](https://www.archlinux.org/packages/?name=kshutdown)

#### Clock synchronization

See [Time synchronization](/index.php/Time_synchronization "Time synchronization").

#### Screen management

See [Xrandr#Graphical front-ends](/index.php/Xrandr#Graphical_front-ends "Xrandr").

#### Backlight management

See [Backlight#Backlight utilities](/index.php/Backlight#Backlight_utilities "Backlight").

#### Color management

See [ICC profiles#Utilities](/index.php/ICC_profiles#Utilities "ICC profiles") and [Backlight#Color correction](/index.php/Backlight#Color_correction "Backlight").

#### Printer management

See [CUPS#GUI applications](/index.php/CUPS#GUI_applications "CUPS").

#### Bluetooth management

See [Bluetooth#Front-ends](/index.php/Bluetooth#Front-ends "Bluetooth").

#### Power management

See [Power management#Userspace tools](/index.php/Power_management#Userspace_tools "Power management").

#### Package management

See [pacman tips#Utilities](/index.php/Pacman_tips#Utilities "Pacman tips").

## Documents and texts

### Text editors

See also [Wikipedia:Comparison of text editors](https://en.wikipedia.org/wiki/Comparison_of_text_editors "wikipedia:Comparison of text editors").

Some of the lighter-weight [Integrated development environments](/index.php/List_of_applications/Utilities#Integrated_development_environments "List of applications/Utilities") can also serve as text editors.

#### Console

*   **dte** — Small, easy to use editor with multi-tabbed interface, syntax highlighting, ctags navigation, etc.

	[https://craigbarnes.gitlab.io/dte/](https://craigbarnes.gitlab.io/dte/) || [dte](https://aur.archlinux.org/packages/dte/)

*   **e3** — Tiny editor without dependencies, written in assembly.

	[https://sites.google.com/site/e3editor/](https://sites.google.com/site/e3editor/) || [e3](https://www.archlinux.org/packages/?name=e3)

*   **ee** — Classic curse-based text editor. Born in HP-UX, used in FreeBSD.

	[https://web.archive.org/web/20160719002816/http://www.users.qwest.net/~hmahon/](https://web.archive.org/web/20160719002816/http://www.users.qwest.net/~hmahon/) || [ee-editor](https://aur.archlinux.org/packages/ee-editor/)

*   **[JED](https://en.wikipedia.org/wiki/JED_(text_editor) "wikipedia:JED (text editor)")** — Text editor that makes extensive use of the [S-Lang library](https://en.wikipedia.org/wiki/S-Lang "wikipedia:S-Lang"). Includes a console version (jed) and an X-window version (xjed).

	[http://jedsoft.org/jed/](http://jedsoft.org/jed/) || [jed](https://aur.archlinux.org/packages/jed/)

*   **[JOE (Joe's Own Editor)](https://en.wikipedia.org/wiki/Joe%27s_Own_Editor "wikipedia:Joe's Own Editor")** — Terminal-based text editor designed to be easy to use.

	[https://joe-editor.sourceforge.io/](https://joe-editor.sourceforge.io/) || [joe](https://www.archlinux.org/packages/?name=joe)

*   **[mcedit](https://en.wikipedia.org/wiki/Midnight_Commander "wikipedia:Midnight Commander")** — Useful text editor that comes with Midnight Commander file manager.

	[http://www.ibiblio.org/mc/](http://www.ibiblio.org/mc/) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **micro** — Modern and intuitive terminal-based text editor, written in go and extensible through plugins.

	[https://micro-editor.github.io/](https://micro-editor.github.io/) || [micro](https://aur.archlinux.org/packages/micro/)

*   **Minimum Profit** — Text editor for programmers.

	[https://triptico.com/software/mp.html](https://triptico.com/software/mp.html) || [mp](https://aur.archlinux.org/packages/mp/)

*   **[nano](/index.php/Nano "Nano")** — Console text editor based on pico with on-screen key bindings help.

	[https://nano-editor.org/](https://nano-editor.org/) || [nano](https://www.archlinux.org/packages/?name=nano)

*   **ne** — Minimalist text editor with Windows-like key-bindings.

	[http://ne.di.unimi.it/](http://ne.di.unimi.it/) || [ne](https://aur.archlinux.org/packages/ne/)

*   **slap** — Sublime-like terminal-based text editor.

	[https://github.com/slap-editor/slap](https://github.com/slap-editor/slap) || [slap](https://aur.archlinux.org/packages/slap/)

*   **Tilde** — Intuitive text editor with Windows-like key bindings.

	[https://os.ghalkes.nl/tilde/](https://os.ghalkes.nl/tilde/) || [tilde](https://aur.archlinux.org/packages/tilde/)

#### Graphical

*   **[Acme](https://en.wikipedia.org/wiki/Acme_(text_editor) "wikipedia:Acme (text editor)")** — Minimalist and flexible programming environment developed by Rob Pike for the Plan 9 operating system.

	[http://acme.cat-v.org/](http://acme.cat-v.org/) || [plan9port](https://www.archlinux.org/packages/?name=plan9port)

*   **Adie** — Fast and convenient programming text editor.

	[http://fox-toolkit.org/](http://fox-toolkit.org/) || [fox](https://www.archlinux.org/packages/?name=fox)

*   **[Atom](/index.php/Atom "Atom")** — Promising text editor developed by GitHub. With support for plug-ins written in Node.js and embedded [Git](/index.php/Git "Git") Control.

	[https://atom.io/](https://atom.io/) || [atom](https://www.archlinux.org/packages/?name=atom)

*   **Beaver** — GTK editor designed to be modular, lightweight and stylish.

	[http://beaver-editor.sourceforge.net/](http://beaver-editor.sourceforge.net/) || [beaver](https://www.archlinux.org/packages/?name=beaver)

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "w:Brackets (text editor)")** — Code editor for the web, written in JavaScript, HTML and CSS.

	[http://brackets.io/](http://brackets.io/) || [brackets](https://aur.archlinux.org/packages/brackets/)

*   **Deepin Editor** — Simple text editor for Deepin desktop.

	[https://github.com/linuxdeepin/deepin-editor](https://github.com/linuxdeepin/deepin-editor) || [deepin-editor](https://www.archlinux.org/packages/?name=deepin-editor)

*   **Ecrire** — Simple text editor based on EFL.

	[https://git.enlightenment.org/apps/ecrire.git/](https://git.enlightenment.org/apps/ecrire.git/) || [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/)

*   **[Editra](https://en.wikipedia.org/wiki/Editra "wikipedia:Editra")** — Text editor with an implementation that focuses on creating an easy to use interface and features that aid in code development.

	[http://editra.org/](http://editra.org/) || [editra](https://aur.archlinux.org/packages/editra/)

*   **Enki** — Text editor for programmers.

	[http://enki-editor.org/](http://enki-editor.org/) || [enki-editor-git](https://aur.archlinux.org/packages/enki-editor-git/)

*   **FeatherPad** — Minimal Qt5 plain text editor featuring a native dark theme and support for tabs, printing and syntax highlighting.

	[https://github.com/tsujan/FeatherPad](https://github.com/tsujan/FeatherPad) || [featherpad](https://aur.archlinux.org/packages/featherpad/)

*   **FLTK Editor** — Simple text editor application for FLTK.

	[https://www.fltk.org/](https://www.fltk.org/) || [fltk-editor](https://aur.archlinux.org/packages/fltk-editor/)

*   **[gedit](https://en.wikipedia.org/wiki/gedit "wikipedia:gedit")** — GTK editor for the GNOME desktop with syntax highlighting, automatic indentation, matching brackets, etc., and a number of add-ons to increase functionality.

	[https://wiki.gnome.org/Apps/Gedit](https://wiki.gnome.org/Apps/Gedit) || [gedit](https://www.archlinux.org/packages/?name=gedit)

*   **Gobby** — Collaborative editor supporting multiple documents in one session and a multi-user chat.

	[https://gobby.github.io/](https://gobby.github.io/) || [gobby](https://www.archlinux.org/packages/?name=gobby)

*   **Howl** — General purpose, fast and lightweight editor with a keyboard-centric minimalistic user interface.

	[https://howl.io/](https://howl.io/) || [howl](https://www.archlinux.org/packages/?name=howl)

*   **[jEdit](https://en.wikipedia.org/wiki/jEdit "wikipedia:jEdit")** — Text editor for programmers, written in Java.

	[http://www.jedit.org/](http://www.jedit.org/) || [jedit](https://www.archlinux.org/packages/?name=jedit)

*   **[JuffEd](https://en.wikipedia.org/wiki/JuffEd "wikipedia:JuffEd")** — Simple tabbed text editor with syntax highlighting, written in Qt.

	[http://juffed.com/en/index.html](http://juffed.com/en/index.html) || [juffed](https://aur.archlinux.org/packages/juffed/)

*   **[Kate](https://en.wikipedia.org/wiki/Kate_(text_editor) "wikipedia:Kate (text editor)")** — Full-featured programmer's editor for the KDE desktop with MDI and a filesystem browser.

	[https://kate-editor.org](https://kate-editor.org) || [kate](https://www.archlinux.org/packages/?name=kate)

*   **[KWrite](https://en.wikipedia.org/wiki/KWrite "wikipedia:KWrite")** — Lightweight text editor for the KDE desktop that uses the same editor widget as Kate.

	[https://www.kde.org/applications/utilities/kwrite](https://www.kde.org/applications/utilities/kwrite) || [kwrite](https://www.archlinux.org/packages/?name=kwrite)

*   **L3afpad** — Simple text editor forked from Leafpad, supports GTK 3.

	[https://github.com/stevenhoneyman/l3afpad](https://github.com/stevenhoneyman/l3afpad) || [l3afpad](https://www.archlinux.org/packages/?name=l3afpad)

*   **[Leafpad](https://en.wikipedia.org/wiki/Leafpad "wikipedia:Leafpad")** — Notepad clone for GTK that emphasizes simplicity.

	[http://tarot.freeshell.org/leafpad/](http://tarot.freeshell.org/leafpad/) || [leafpad](https://www.archlinux.org/packages/?name=leafpad)

*   **[Light Table](https://en.wikipedia.org/wiki/Light_Table_(software) "w:Light Table (software)")** — Next generation code editor that connects you to your creation with instant feedback.

	[http://lighttable.com/](http://lighttable.com/) || [lighttable-bin](https://aur.archlinux.org/packages/lighttable-bin/) or [lighttable-git](https://aur.archlinux.org/packages/lighttable-git/)

*   **Liri Text** — Text editor for Liri.

	[https://github.com/lirios/text](https://github.com/lirios/text) || [liri-text](https://www.archlinux.org/packages/?name=liri-text)

*   **medit** — Programming and around-programming text editor.

	[http://mooedit.sourceforge.net](http://mooedit.sourceforge.net) || [medit](https://aur.archlinux.org/packages/medit/)

*   **[Mousepad](https://en.wikipedia.org/wiki/Xfce#Mousepad "wikipedia:Xfce")** — Fast text editor for the Xfce Desktop Environment.

	[https://www.xfce.org](https://www.xfce.org) || [mousepad](https://www.archlinux.org/packages/?name=mousepad)

*   **[NEdit](https://en.wikipedia.org/wiki/NEdit "wikipedia:NEdit")** — Text editor for the Motif environment.

	[https://sourceforge.net/projects/nedit/](https://sourceforge.net/projects/nedit/) || [nedit](https://www.archlinux.org/packages/?name=nedit)

*   **NFO Viewer** — Simple viewer for NFO files.

	[https://otsaloma.io/nfoview/](https://otsaloma.io/nfoview/) || [nfoview](https://www.archlinux.org/packages/?name=nfoview)

*   **Notepadqq** — Qt-based, Notepad++-like text editor with support for syntax highlighting for more than 100 languages.

	[https://notepadqq.com/s/](https://notepadqq.com/s/) || [notepadqq](https://www.archlinux.org/packages/?name=notepadqq)

*   **Pantheon Code** — Code editor for elementaryOS. It auto-saves your files, meaning they're always up-to-date. Plus it remembers your tabs so you never lose your spot, even in between sessions.

	[https://github.com/elementary/code](https://github.com/elementary/code) || [pantheon-code](https://www.archlinux.org/packages/?name=pantheon-code)

*   **[Pluma](/index.php/MATE "MATE")** — Powerful text editor for MATE.

	[https://mate-desktop.org/](https://mate-desktop.org/) || [pluma](https://www.archlinux.org/packages/?name=pluma)

*   **QSciTE** — Qt clone of the SciTE text and code editor.

	[https://code.google.com/archive/p/qscite/](https://code.google.com/archive/p/qscite/) || [qscite](https://aur.archlinux.org/packages/qscite/)

*   **[Sam](https://en.wikipedia.org/wiki/Sam_(text_editor) "wikipedia:Sam (text editor)")** — Minimalist text editor with a graphical user interface, a very powerful command language and remote editing capabilities, developed by Rob Pike.

	[http://sam.cat-v.org](http://sam.cat-v.org) || [plan9port](https://www.archlinux.org/packages/?name=plan9port) or [9base](https://www.archlinux.org/packages/?name=9base)

*   **[SciTE](https://en.wikipedia.org/wiki/SciTE "wikipedia:SciTE")** — Generally useful editor with facilities for building and running programs.

	[https://scintilla.org/SciTE.html](https://scintilla.org/SciTE.html) || [scite](https://aur.archlinux.org/packages/scite/)

*   **Scribes** — Ultra minimalist text editor that combines simplicity with power.

	[http://scribes.sourceforge.net](http://scribes.sourceforge.net) || [scribes](https://aur.archlinux.org/packages/scribes/)

*   **[Sublime Text](https://en.wikipedia.org/wiki/Sublime_Text "wikipedia:Sublime Text")** — Proprietary C++ and Python-based editor with many advanced features and plugins while staying lightweight and pretty.

	[https://www.sublimetext.com/](https://www.sublimetext.com/) || version 3: [sublime-text-dev](https://aur.archlinux.org/packages/sublime-text-dev/), version 2: [sublime-text2](https://aur.archlinux.org/packages/sublime-text2/)

*   **[TEA](https://en.wikipedia.org/wiki/TEA_(text_editor) "wikipedia:TEA (text editor)")** — Qt-based feature rich text editor.

	[http://semiletov.org/tea/](http://semiletov.org/tea/) || [tea](https://aur.archlinux.org/packages/tea/)

*   **[Textadept](/index.php/Textadept "Textadept")** — Lua-extensible feature rich text editor based on Scintilla and written in C.

	[https://foicica.com/textadept/](https://foicica.com/textadept/) || [textadept](https://aur.archlinux.org/packages/textadept/)

*   **Textosaurus** — Simple cross-platform text editor based on Qt and QScintilla.

	[https://github.com/martinrotter/textosaurus](https://github.com/martinrotter/textosaurus) || [textosaurus](https://aur.archlinux.org/packages/textosaurus/)

*   **[Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code")** — Editor for building and debugging modern web and cloud applications.

	[https://code.visualstudio.com](https://code.visualstudio.com) || [code](https://www.archlinux.org/packages/?name=code)

*   **xed** — Text editor based on Pluma developed for Linux Mint.

	[https://github.com/linuxmint/xed](https://github.com/linuxmint/xed) || [xed](https://www.archlinux.org/packages/?name=xed)

*   **XEdit** — Simple text editor for the X Window System.

	[https://www.x.org/wiki](https://www.x.org/wiki) || [xorg-xedit](https://www.archlinux.org/packages/?name=xorg-xedit)

*   **wxMEdit** — Text/Hex editor written in C++ and wxWidgets.

	[https://wxmedit.github.io/](https://wxmedit.github.io/) || [wxmedit](https://aur.archlinux.org/packages/wxmedit/)

#### Emacs-style text editors

*   **[Emacs](/index.php/Emacs "Emacs")** — The extensible, customizable, self-documenting real-time display editor by GNU.

	[https://www.gnu.org/software/emacs/emacs.html](https://www.gnu.org/software/emacs/emacs.html) || with GUI: [emacs](https://www.archlinux.org/packages/?name=emacs), without GUI: [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox)

*   **[mg](https://en.wikipedia.org/wiki/mg_(editor) "wikipedia:mg (editor)")** — Small, fast, and portable Emacs-like editor.

	[https://github.com/hboetes/mg](https://github.com/hboetes/mg) || [mg](https://www.archlinux.org/packages/?name=mg)

*   **[MicroEmacs](https://en.wikipedia.org/wiki/MicroEMACS "wikipedia:MicroEMACS")** — Ncurses-based text editor.

	[http://www.jasspa.com/](http://www.jasspa.com/) || [jasspa-me](https://aur.archlinux.org/packages/jasspa-me/)

*   **[vile](https://en.wikipedia.org/wiki/Vile_(editor) "wikipedia:Vile (editor)")** — Lightweight Emacs clone with *vi*-like key bindings.

	[https://invisible-island.net/vile/vile.html](https://invisible-island.net/vile/vile.html) || [vile](https://aur.archlinux.org/packages/vile/)

*   **[Zile](https://en.wikipedia.org/wiki/GNU_Zile "wikipedia:GNU Zile")** — Lightweight Emacs clone.

	[https://www.gnu.org/software/zile/](https://www.gnu.org/software/zile/) || [zile](https://www.archlinux.org/packages/?name=zile)

#### Vi-style text editors

*   **Amp** — Text editor written in Rust, that aims to take the core interaction model of Vim, simplify it, and bundle in the essential features required for a modern text editor.

	[https://amp.rs/](https://amp.rs/) || [amp](https://aur.archlinux.org/packages/amp/)

*   **[Kakoune](/index.php/Kakoune "Kakoune")** — Modal editor. Fewer keystrokes. Selection based, multi-cursor editing. Orthogonal design.

	[https://github.com/mawww/kakoune](https://github.com/mawww/kakoune) || [kakoune](https://www.archlinux.org/packages/?name=kakoune)

*   **[Neovim](/index.php/Neovim "Neovim")** — Vim's rebirth for the 21st century.

	[https://neovim.io/](https://neovim.io/) || [neovim](https://www.archlinux.org/packages/?name=neovim)

*   **[vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi")** — The original ex/vi text editor.

	[http://ex-vi.sourceforge.net/](http://ex-vi.sourceforge.net/) || [vi](https://www.archlinux.org/packages/?name=vi)

*   **[Vim](/index.php/Vim "Vim") (Vi IMproved)** — Advanced text editor that seeks to provide the power of the de-facto Unix editor 'vi', with a more complete feature set.

	[https://www.vim.org/](https://www.vim.org/) || with GUI: [gvim](https://www.archlinux.org/packages/?name=gvim), without GUI: [vim](https://www.archlinux.org/packages/?name=vim)

*   **Vis** — Modern, legacy free, simple yet efficient vim-like editor.

	[https://github.com/martanne/vis](https://github.com/martanne/vis) || [vis](https://www.archlinux.org/packages/?name=vis)

### Office

#### Office suites

See also [Wikipedia:Comparison of office suites](https://en.wikipedia.org/wiki/Comparison_of_office_suites "wikipedia:Comparison of office suites").

*   **[Calligra](https://en.wikipedia.org/wiki/Calligra_Suite "wikipedia:Calligra Suite")** — Actively developed fork of KOffice, the [KDE](/index.php/KDE "KDE") office suite. It offers most of the features of OpenOffice while also having versions for smartphones (Calligra Mobile) and tablets (Calligra Active).

	[https://www.calligra.org/](https://www.calligra.org/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[LibreOffice](/index.php/LibreOffice "LibreOffice")** — The office productivity suite compatible to the open and standardized ODF document format. Fork of OpenOffice, supported by The Document Foundation.

	[https://www.libreoffice.org/](https://www.libreoffice.org/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OnlyOffice](https://en.wikipedia.org/wiki/OnlyOffice "wikipedia:OnlyOffice")** — Office suite that combines text, spreadsheet and presentation editors.

	[https://www.onlyoffice.com/](https://www.onlyoffice.com/) || [onlyoffice-bin](https://aur.archlinux.org/packages/onlyoffice-bin/)

*   **[OpenOffice](/index.php/OpenOffice "OpenOffice")** — Open-source office software suite for word processing, spreadsheets, presentations, graphics, databases and more, under the Apache Licence.

	[https://www.openoffice.org/](https://www.openoffice.org/) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[SoftMaker Office](https://en.wikipedia.org/wiki/SoftMaker_Office "wikipedia:SoftMaker Office")** — Complete, reliable, lightning-fast and Microsoft Office-compatible proprietary office suite with a word processor, spreadsheet, and presentation graphics software.

	[https://www.freeoffice.com/](https://www.freeoffice.com/) || [freeoffice](https://aur.archlinux.org/packages/freeoffice/)

*   **[WPS Office](https://en.wikipedia.org/wiki/Kingsoft_Office "wikipedia:Kingsoft Office")** — Proprietary office productivity suite, previously known as Kingsoft Office.

	[https://www.wps.com/](https://www.wps.com/) || [wps-office](https://aur.archlinux.org/packages/wps-office/)

#### Word processors

See also [Wikipedia:Comparison of word processors](https://en.wikipedia.org/wiki/Comparison_of_word_processors "wikipedia:Comparison of word processors").

*   **[AbiWord](/index.php/AbiWord "AbiWord")** — Full-featured word processor.

	[https://www.abisource.com/](https://www.abisource.com/) || [abiword](https://www.archlinux.org/packages/?name=abiword)

*   **[Calligra Words](https://en.wikipedia.org/wiki/Calligra_Words "wikipedia:Calligra Words")** — Powerful word processor included in the Calligra Suite.

	[https://www.calligra.org/words/](https://www.calligra.org/words/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[LibreOffice Writer](/index.php/LibreOffice "LibreOffice")** — Full-featured word processor included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/writer](https://www.libreoffice.org/discover/writer) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice Writer](/index.php/OpenOffice "OpenOffice")** — Full-featured word processor included in the OpenOffice suite.

	[http://www.openoffice.org/product/writer.html](http://www.openoffice.org/product/writer.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[Ted](https://en.wikipedia.org/wiki/Ted_(word_processor) "wikipedia:Ted (word processor)")** — Easy to use GTK-based rich text processor (with footnote support).

	[https://nllgg.nl/Ted/](https://nllgg.nl/Ted/) || [ted](https://aur.archlinux.org/packages/ted/)

*   **[WordGrinder](https://en.wikipedia.org/wiki/WordGrinder "wikipedia:WordGrinder")** — Word processor for the console.

	[http://cowlark.com/wordgrinder/](http://cowlark.com/wordgrinder/) || [wordgrinder](https://aur.archlinux.org/packages/wordgrinder/)

##### WYSIWYG HTML editors

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — WYSIWYG content editor for the World Wide Web.

	[http://www.bluegriffon.com/](http://www.bluegriffon.com/) || [bluegriffon](https://www.archlinux.org/packages/?name=bluegriffon)

*   **[SeaMonkey Composer](https://en.wikipedia.org/wiki/SeaMonkey#Composer "wikipedia:SeaMonkey")** — Powerful yet simple HTML editor included in the SeaMonkey suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

##### Desktop publishing

*   **gLabels** — Program for creating labels, business cards and media covers.

	[http://glabels.org/](http://glabels.org/) || [glabels](https://www.archlinux.org/packages/?name=glabels)

*   **[Scribus](https://en.wikipedia.org/wiki/Scribus "wikipedia:Scribus")** — Desktop publishing program.

	[https://www.scribus.net/](https://www.scribus.net/) || [scribus](https://www.archlinux.org/packages/?name=scribus)

#### Presentations

*   **[Calligra Stage](https://en.wikipedia.org/wiki/Calligra_Stage "wikipedia:Calligra Stage")** — Easy to use yet still flexible presentation application included in the Calligra Suite.

	[https://www.calligra.org/stage/](https://www.calligra.org/stage/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[LibreOffice Impress](/index.php/LibreOffice "LibreOffice")** — Presentation program included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/writer](https://www.libreoffice.org/discover/writer) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice Impress](/index.php/OpenOffice "OpenOffice")** — Presentation program included in the OpenOffice suite.

	[http://www.openoffice.org/product/impress.html](http://www.openoffice.org/product/impress.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **Sozi** — Zooming presentation editor and player. Based on the [Electron](https://electronjs.org/) platform.

	[https://sozi.baierouge.fr/](https://sozi.baierouge.fr/) || [sozi](https://aur.archlinux.org/packages/sozi/)

*   **Spice-Up** — Create simple and beautiful presentations.

	[https://github.com/Philip-Scott/Spice-up](https://github.com/Philip-Scott/Spice-up) || [spice-up](https://aur.archlinux.org/packages/spice-up/)

*   **sent** — Simple plaintext presentation tool.

	[https://git.suckless.org/sent/](https://git.suckless.org/sent/) || [sent](https://aur.archlinux.org/packages/sent/)

#### Spreadsheets

See also [Wikipedia:Comparison of spreadsheet software](https://en.wikipedia.org/wiki/Comparison_of_spreadsheet_software "wikipedia:Comparison of spreadsheet software").

*   **[Calligra Sheets](https://en.wikipedia.org/wiki/Calligra_Sheets "wikipedia:Calligra Sheets")** — Powerful spreadsheet application included in the Calligra Suite.

	[https://www.calligra.org/sheets/](https://www.calligra.org/sheets/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[Gnumeric](/index.php/Gnumeric "Gnumeric")** — Spreadsheet program for the GNOME desktop.

	[http://www.gnumeric.org/](http://www.gnumeric.org/) || [gnumeric](https://www.archlinux.org/packages/?name=gnumeric)

*   **[LibreOffice Calc](/index.php/LibreOffice "LibreOffice")** — Full-featured spreadsheet application included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/calc/](https://www.libreoffice.org/discover/calc/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice Calc](/index.php/OpenOffice "OpenOffice")** — Full-featured spreadsheet application included in the OpenOffice suite.

	[http://www.openoffice.org/product/calc.html](http://www.openoffice.org/product/calc.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[Pyspread](https://en.wikipedia.org/wiki/Pyspread "wikipedia:Pyspread")** — Pyspread is a non-traditional spreadsheet application that is based on and written in the programming language Python.

	[https://manns.github.io/pyspread/index.html](https://manns.github.io/pyspread/index.html) || [pyspread](https://aur.archlinux.org/packages/pyspread/)

*   **[sc](https://en.wikipedia.org/wiki/sc_(spreadsheet_calculator) "wikipedia:sc (spreadsheet calculator)")** — Curses-based lightweight spreadsheet.

	[http://ibiblio.org/pub/linux/apps/financial/spreadsheet/!INDEX.html](http://ibiblio.org/pub/linux/apps/financial/spreadsheet/!INDEX.html) || [sc](https://www.archlinux.org/packages/?name=sc)

*   **sc-im** — Spreadsheet program based on sc.

	[https://github.com/andmarti1424/sc-im/](https://github.com/andmarti1424/sc-im/) || [sc-im](https://aur.archlinux.org/packages/sc-im/)

#### Database tools

For DBMS-specific tools, see:

*   [MySQL#Graphical tools](/index.php/MySQL#Graphical_tools "MySQL")
*   [PostgreSQL#Graphical tools](/index.php/PostgreSQL#Graphical_tools "PostgreSQL")
*   [SQLite#Graphical tools](/index.php/SQLite#Graphical_tools "SQLite")

See also [Wikipedia:Comparison of database tools](https://en.wikipedia.org/wiki/Comparison_of_database_tools "wikipedia:Comparison of database tools").

*   **[Adminer](/index.php/Adminer "Adminer")** — Full-featured database management webapp with support for many database types.

	[https://www.adminer.org/](https://www.adminer.org/) || [adminer](https://aur.archlinux.org/packages/adminer/)

*   **[DBeaver](https://en.wikipedia.org/wiki/DBeaver "wikipedia:DBeaver")** — Java-based graphical database editor with support for many database types.

	[https://dbeaver.jkiss.org/](https://dbeaver.jkiss.org/) || [dbeaver](https://www.archlinux.org/packages/?name=dbeaver)

*   **GdaBrowser** — Graphical tool to get a quick access to a database's structure and contents.

	[https://www.gnome-db.org/GdaBrowser](https://www.gnome-db.org/GdaBrowser) || [libgda](https://www.archlinux.org/packages/?name=libgda)

*   **GSQL** — Integrated database development tool for GNOME. Last release 2010.

	[http://gsql.org/](http://gsql.org/) || [gsql](https://aur.archlinux.org/packages/gsql/)

*   **[Kexi](https://en.wikipedia.org/wiki/Kexi "wikipedia:Kexi")** — Visual database applications creator tool by KDE, designed to fill the gap between spreadsheets and database solutions requiring more sophisticated development.

	[http://www.kexi-project.org/](http://www.kexi-project.org/) || [kexi](https://www.archlinux.org/packages/?name=kexi)

*   **[LibreOffice Base](/index.php/LibreOffice "LibreOffice")** — Full-featured desktop database front end included in the LibreOffice suite, designed to meet the needs of a broad array of users.

	[https://www.libreoffice.org/discover/base/](https://www.libreoffice.org/discover/base/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice Base](/index.php/OpenOffice "OpenOffice")** — Full-featured desktop database front end included in the OpenOffice suite, designed to meet the needs of a broad array of users.

	[http://www.openoffice.org/product/base.html](http://www.openoffice.org/product/base.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[Orbada](https://en.wikipedia.org/wiki/Orbada "wikipedia:Orbada")** — Excellent tool for database developers, SQL developers, DBA administrators, as well as for users who wish to broaden their knowledge and skills in SQL.

	[https://orbada.sourceforge.io/](https://orbada.sourceforge.io/) || [orbada](https://aur.archlinux.org/packages/orbada/)

*   **Sequeler** — SQL client built in Vala and Gtk. It allows you to connect to your local and remote databases, write SQL in a handy text editor with language recognition, and visualize SELECT results in a Gtk.Grid Widget.

	[https://github.com/Alecaddd/sequeler](https://github.com/Alecaddd/sequeler) || [sequeler-git](https://aur.archlinux.org/packages/sequeler-git/)

*   **[SQuirreL SQL Client](https://en.wikipedia.org/wiki/SQuirreL_SQL_Client "wikipedia:SQuirreL SQL Client")** — Graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc.

	[http://www.squirrelsql.org/](http://www.squirrelsql.org/) || [squirrel-sql](https://aur.archlinux.org/packages/squirrel-sql/)

*   **[TOra](https://en.wikipedia.org/wiki/TOra "wikipedia:TOra")** — Database management GUI that supports accessing most of the common database platforms in use, including Oracle, MySQL, and PostgreSQL, as well as limited support for any target that can be accessed through Qt's ODBC support.

	[https://github.com/tora-tool/tora/wiki](https://github.com/tora-tool/tora/wiki) || [tora](https://aur.archlinux.org/packages/tora/)

##### Simplified database software

*   **Glom** — Easy-to-use database designer and user interface.

	[https://www.glom.org/](https://www.glom.org/) || [glom](https://www.archlinux.org/packages/?name=glom)

*   **Symphytum** — Personal database software for everyone who desires to manage and organize data in an easy and intuitive way, without having to study complex database languages and software user interfaces.

	[https://giowck.github.io/symphytum/](https://giowck.github.io/symphytum/) || [symphytum](https://aur.archlinux.org/packages/symphytum/)

#### Formula editors

See also [#TeX formula editors](#TeX_formula_editors) and [Wikipedia:Formula editor](https://en.wikipedia.org/wiki/Formula_editor "wikipedia:Formula editor").

*   **[LibreOffice Math](/index.php/LibreOffice "LibreOffice")** — Create and edit scientific formulas and equations. Included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/math/](https://www.libreoffice.org/discover/math/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice Math](/index.php/OpenOffice "OpenOffice")** — Create equations and formulas for your documents. Included in the OpenOffice suite.

	[http://www.openoffice.org/product/math.html](http://www.openoffice.org/product/math.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

### Markup languages

See also [Wikipedia:Comparison of document markup languages](https://en.wikipedia.org/wiki/Comparison_of_document_markup_languages "wikipedia:Comparison of document markup languages").

*   **[Sphinx](https://en.wikipedia.org/wiki/Sphinx_(documentation_generator) "wikipedia:Sphinx (documentation generator)")** — A documentation generation system using [reStructuredText](https://en.wikipedia.org/wiki/ReStructuredText "wikipedia:ReStructuredText") to generate output in multiple formats (primary documentation system for the Python project).

	[http://sphinx-doc.org](http://sphinx-doc.org) || [python-sphinx](https://www.archlinux.org/packages/?name=python-sphinx)

*   **[txt2tags](https://en.wikipedia.org/wiki/Txt2tags "wikipedia:Txt2tags")** — Dead-simple, KISS-compliant lightweight, human-readable markup language to produce rich format content out of plain text files.

	[https://txt2tags.org/](https://txt2tags.org/) || [txt2tags](https://www.archlinux.org/packages/?name=txt2tags)

#### AsciiDoc

See also [Wikipedia:AsciiDoc](https://en.wikipedia.org/wiki/AsciiDoc "wikipedia:AsciiDoc").

*   **AsciiDoc** — The original implementation, written in Python. Used by Arch for generating *pacman*'s man pages.[[2]](https://www.archlinux.org/pacman/pacman.8.html).

	[http://asciidoc.org/](http://asciidoc.org/) || [asciidoc](https://www.archlinux.org/packages/?name=asciidoc)

*   **Asciidoctor** — An implementation written in Ruby, with [many extra features](https://asciidoctor.org/docs/asciidoc-asciidoctor-diffs/).

	[https://asciidoctor.org/](https://asciidoctor.org/) || [asciidoctor](https://www.archlinux.org/packages/?name=asciidoctor)

#### Markdown

See also the [official website](https://daringfireball.net/projects/markdown/) and [Wikipedia:Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown").

*   **Discount** — A Markdown implementation written in C.

	[https://www.pell.portland.or.us/~orc/Code/discount/](https://www.pell.portland.or.us/~orc/Code/discount/) || [discount](https://www.archlinux.org/packages/?name=discount), Ruby wrapper library: [ruby-rdiscount](https://www.archlinux.org/packages/?name=ruby-rdiscount)

*   **lowdown** — Markdown translator producing HTML5 and roff documents in the ms and man formats.

	[https://kristaps.bsd.lv/lowdown/](https://kristaps.bsd.lv/lowdown/) || [lowdown](https://aur.archlinux.org/packages/lowdown/)

*   **Marked** — Markdown parser and compiler built for speed.

	[https://marked.js.org/](https://marked.js.org/) || [marked](https://www.archlinux.org/packages/?name=marked)

*   [Pandoc](/index.php/Pandoc "Pandoc") also supports Markdown.

##### Python implementations

*   **CommonMark-py** — Python parser for the CommonMark Markdown specification.

	[https://github.com/rtfd/CommonMark-py](https://github.com/rtfd/CommonMark-py) || [python-commonmark](https://www.archlinux.org/packages/?name=python-commonmark), [python2-commonmark](https://www.archlinux.org/packages/?name=python2-commonmark)

*   **M2R** — Markdown to reStructuredText converter.

	[https://github.com/miyakogi/m2r](https://github.com/miyakogi/m2r) || [m2r](https://www.archlinux.org/packages/?name=m2r), [python2-m2r](https://www.archlinux.org/packages/?name=python2-m2r)

*   **Mistune** — The fastest markdown parser in pure Python with renderer feature.

	[https://github.com/lepture/mistune](https://github.com/lepture/mistune) || [python-mistune](https://www.archlinux.org/packages/?name=python-mistune), [python2-mistune](https://www.archlinux.org/packages/?name=python2-mistune)

*   **Python-Markdown** — Extensible Python implementation of John Gruber's Markdown.

	[https://github.com/Python-Markdown/markdown](https://github.com/Python-Markdown/markdown) || [python-markdown](https://www.archlinux.org/packages/?name=python-markdown), [python2-markdown](https://www.archlinux.org/packages/?name=python2-markdown)

##### Ruby implementations

*   **kramdown** — Fast, pure Ruby Markdown superset converter, using a strict syntax definition.

	[https://kramdown.gettalong.org/](https://kramdown.gettalong.org/) || [ruby-kramdown](https://www.archlinux.org/packages/?name=ruby-kramdown)

*   **Maruku** — Pure Ruby Markdown-superset interpreter.

	[https://github.com/bhollis/maruku](https://github.com/bhollis/maruku) || [ruby-maruku](https://www.archlinux.org/packages/?name=ruby-maruku)

##### Markdown editors

*   **Abricotine** — Markdown editor built for desktop. Based on the [Electron](https://electronjs.org/) platform.

	[https://abricotine.brrd.fr/](https://abricotine.brrd.fr/) || [abricotine](https://aur.archlinux.org/packages/abricotine/)

*   **CuteMarkEd** — Qt-based Markdown editor with live HTML preview, math expressions, code and markdown syntax highlighting.

	[https://cloose.github.io/CuteMarkEd/](https://cloose.github.io/CuteMarkEd/) || [cutemarked](https://aur.archlinux.org/packages/cutemarked/)

*   **EME** — Elegant Markdown Editor. Based on the [Electron](https://electronjs.org/) platform.

	[https://github.com/egoist/eme](https://github.com/egoist/eme) || [eme](https://aur.archlinux.org/packages/eme/)

*   **ghostwriter** — Distraction-free Markdown editor.

	[https://wereturtle.github.io/ghostwriter/](https://wereturtle.github.io/ghostwriter/) || [ghostwriter](https://aur.archlinux.org/packages/ghostwriter/)

*   **Marker** — Simple yet robust Markdown editor.

	[https://fabiocolacio.github.io/Marker/](https://fabiocolacio.github.io/Marker/) || [marker](https://aur.archlinux.org/packages/marker/)

*   **MarkMyWords** — Minimal markdown editor.

	[https://github.com/voldyman/MarkMyWords](https://github.com/voldyman/MarkMyWords) || [markmywords-git](https://aur.archlinux.org/packages/markmywords-git/)

*   **Mark Text** — Next generation markdown editor. Based on the [Electron](https://electronjs.org/) platform.

	[https://marktext.github.io/website/](https://marktext.github.io/website/) || [marktext](https://aur.archlinux.org/packages/marktext/)

*   **Moeditor** — Your all-purpose markdown editor. Based on the [Electron](https://electronjs.org/) platform.

	[https://moeditor.js.org/](https://moeditor.js.org/) || [moeditor-bin](https://aur.archlinux.org/packages/moeditor-bin/)

*   **Remarkable** — Fully featured Markdown editor.

	[https://remarkableapp.github.io/](https://remarkableapp.github.io/) || [remarkable](https://aur.archlinux.org/packages/remarkable/)

*   **ReText** — Simple text editor for Markdown and reStructuredText.

	[https://github.com/retext-project/retext](https://github.com/retext-project/retext) || [retext](https://www.archlinux.org/packages/?name=retext)

*   **[UberWriter](https://en.wikipedia.org/wiki/UberWriter "wikipedia:UberWriter")** — Elegant, free distraction GTK Markdown editor.

	[http://uberwriter.github.io/uberwriter/](http://uberwriter.github.io/uberwriter/) || [uberwriter](https://aur.archlinux.org/packages/uberwriter/)

#### Typesetting systems

*   **[groff](https://en.wikipedia.org/wiki/groff_(software) "wikipedia:groff (software)")** — [GNU](/index.php/GNU "GNU") implementation of troff, a heirloom Unix document processing system and the default formatter for [man pages](/index.php/Man_page "Man page").

	[https://www.gnu.org/software/groff/groff.html](https://www.gnu.org/software/groff/groff.html) || [groff](https://www.archlinux.org/packages/?name=groff)

*   **[Lout](/index.php/Lout "Lout")** — A lightware document formatting system. Reads a high-level description of a document similar in style to LaTeX and produces a PostScript.

	[http://savannah.nongnu.org/projects/lout](http://savannah.nongnu.org/projects/lout) || [lout](https://www.archlinux.org/packages/?name=lout)

*   **SILE** — Modern typesetting system inspired by TeX.

	[https://sile-typesetter.org/](https://sile-typesetter.org/) || [sile](https://aur.archlinux.org/packages/sile/)

*   **[TeX](/index.php/TeX "TeX")** — A high-quality typesetting system popular in academia.

	[https://tug.org/](https://tug.org/) || [texlive-core](https://www.archlinux.org/packages/?name=texlive-core)

*   **[Texinfo](/index.php/Texinfo "Texinfo")** — Typesetting syntax for software manuals used by the [GNU Project](/index.php/GNU_Project "GNU Project").

	[https://www.gnu.org/software/texinfo/](https://www.gnu.org/software/texinfo/) || [texinfo](https://www.archlinux.org/packages/?name=texinfo)

#### TeX editors

With [TeX, LaTeX and friends](/index.php/TeX_Live "TeX Live"), creation of any scientific document, article, journal, etc. is made commonplace.

See also [Wikipedia:Comparison of TeX editors](https://en.wikipedia.org/wiki/Comparison_of_TeX_editors "wikipedia:Comparison of TeX editors") and [the LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Editors).

*   **[AUCTeX](https://en.wikipedia.org/wiki/AUCTeX "wikipedia:AUCTeX")** — Together with RefTex, AUCTeX provices an extensible environment for writing and formatting TeX files in [Emacs](/index.php/Emacs "Emacs").

	[https://www.gnu.org/software/auctex/](https://www.gnu.org/software/auctex/) || [auctex](https://aur.archlinux.org/packages/auctex/)

*   **[gedit](/index.php/Gedit "Gedit") LaTeX Plugin** — Add code-completion to gedit and allows for compiling LaTeX documents and managing BibTeX bibliographies.

	[https://wiki.gnome.org/Apps/Gedit/LaTeXPlugin](https://wiki.gnome.org/Apps/Gedit/LaTeXPlugin) || [gedit-latex](https://aur.archlinux.org/packages/gedit-latex/)

*   **[GNOME LaTeX](https://en.wikipedia.org/wiki/GNOME-LaTeX "wikipedia:GNOME-LaTeX")** — LaTeX editor for the GNOME Desktop including support for code completion, compiling and project management.

	[https://wiki.gnome.org/Apps/GNOME-LaTeX](https://wiki.gnome.org/Apps/GNOME-LaTeX) || [gnome-latex](https://www.archlinux.org/packages/?name=gnome-latex)

*   **[Gummi](https://en.wikipedia.org/wiki/Gummi_(software) "wikipedia:Gummi (software)")** — Lightweight TeX/LaTeX GTK-based editor. It features a continuous preview mode, integrated BibTeX support, extendable snippet interface and multi-document support.

	[https://github.com/alexandervdm/gummi/](https://github.com/alexandervdm/gummi/) || [gummi](https://www.archlinux.org/packages/?name=gummi)

*   **[Kile](https://en.wikipedia.org/wiki/Kile "wikipedia:Kile")** — User-friendly TeX/LaTeX editor for the KDE desktop with many features.

	[https://kile.sourceforge.io/](https://kile.sourceforge.io/) || [kile](https://www.archlinux.org/packages/?name=kile)

*   **Ktikz** — Small application helping you to create [PGF/TikZ](https://en.wikipedia.org/wiki/PGF/TikZ "wikipedia:PGF/TikZ") diagrams for your publications.

	[http://www.hackenberger.at/blog/ktikz-editor-for-the-tikz-language/](http://www.hackenberger.at/blog/ktikz-editor-for-the-tikz-language/) || KDE: [ktikz](https://www.archlinux.org/packages/?name=ktikz), Qt: [qtikz](https://www.archlinux.org/packages/?name=qtikz)

*   **[LyX](https://en.wikipedia.org/wiki/LyX "wikipedia:LyX")** — Document processor that encourages an approach to writing based on the structure of your documents (WYSIWYM) and not simply their appearance (WYSIWYG).

	[https://www.lyx.org/](https://www.lyx.org/) || [lyx](https://www.archlinux.org/packages/?name=lyx)

*   **[TeXmacs](https://en.wikipedia.org/wiki/GNU_TeXmacs "wikipedia:GNU TeXmacs")** — WYSIWYW (what you see is what you want) editing platform with special features for scientists.

	[http://www.texmacs.org/](http://www.texmacs.org/) || [texmacs](https://www.archlinux.org/packages/?name=texmacs)

*   **[Texmaker](https://en.wikipedia.org/wiki/Texmaker "wikipedia:Texmaker")** — Cross-platform, light and easy-to-use LaTeX IDE. It integrates many tools needed to develop documents with LaTeX, in just one application

	[https://www.xm1math.net/texmaker/](https://www.xm1math.net/texmaker/) || [texmaker](https://www.archlinux.org/packages/?name=texmaker)

*   **[TeXstudio](https://en.wikipedia.org/wiki/TeXstudio "wikipedia:TeXstudio")** — Fork of TeXMaker including support for code completion of bibtex items, grammar check and automatic detection of the need for multiple LaTeX runs.

	[http://texstudio.sourceforge.net/](http://texstudio.sourceforge.net/) || [texstudio](https://www.archlinux.org/packages/?name=texstudio)

*   **[TeXworks](https://en.wikipedia.org/wiki/TeXworks "wikipedia:TeXworks")** — Simple TeX front-end program modeled after TeXShop.

	[https://tug.org/texworks/](https://tug.org/texworks/) || [texworks](https://www.archlinux.org/packages/?name=texworks)

*   **TikZiT** — Graphical tool for rapidly creating graphs and diagrams using [PGF/TikZ](https://en.wikipedia.org/wiki/PGF/TikZ "wikipedia:PGF/TikZ").

	[https://tikzit.github.io/](https://tikzit.github.io/) || [tikzit](https://aur.archlinux.org/packages/tikzit/)

*   **[Vim-LaTeX-suite](/index.php/Vim "Vim")** — Customizable LaTeX environment for Vim.

	[http://vim-latex.sourceforge.net/](http://vim-latex.sourceforge.net/) || [vim-latexsuite](https://www.archlinux.org/packages/?name=vim-latexsuite)

#### TeX formula editors

*   **EqualX** — LaTeX equation editor with real time preview.

	[http://equalx.sourceforge.net/](http://equalx.sourceforge.net/) || [equalx](https://aur.archlinux.org/packages/equalx/)

*   **KLatexFormula** — GUI for generating images from LaTeX equations.

	[https://klatexformula.sourceforge.io/](https://klatexformula.sourceforge.io/) || [klatexformula](https://aur.archlinux.org/packages/klatexformula/)

*   **[LibreOffice](/index.php/LibreOffice "LibreOffice") TexMaths extension** — LaTeX equation editor for LibreOffice.

	[http://roland65.free.fr/texmaths/](http://roland65.free.fr/texmaths/) || [libreoffice-extension-texmaths](https://www.archlinux.org/packages/?name=libreoffice-extension-texmaths)

#### XML editors

See also [Wikipedia:Comparison of XML editors](https://en.wikipedia.org/wiki/Comparison_of_XML_editors "wikipedia:Comparison of XML editors").

*   **QXmlEdit** — Simple Qt XML editor and XSD viewer.

	[http://qxmledit.org/](http://qxmledit.org/) || [qxmledit](https://aur.archlinux.org/packages/qxmledit/)

*   **XML Copy Editor** — Fast, validating XML editor.

	[http://xml-copy-editor.sourceforge.net/](http://xml-copy-editor.sourceforge.net/) || [xmlcopyeditor](https://aur.archlinux.org/packages/xmlcopyeditor/)

*   **XML Tree Editor** — Displays XML files as tree views and allows basic operations: adding, editing and deleting text nodes and their attributes.

	[https://sourceforge.net/projects/xmltreeeditor/](https://sourceforge.net/projects/xmltreeeditor/) || [xmltreeedit-bin](https://aur.archlinux.org/packages/xmltreeedit-bin/)

### Document converters

See also [#Markup languages](#Markup_languages) and [PDF, PS and DjVu](/index.php/PDF,_PS_and_DjVu "PDF, PS and DjVu").

*   **[Antiword](https://en.wikipedia.org/wiki/Antiword "wikipedia:Antiword")** — MS Word to text converter.

	[http://www.winfield.demon.nl/](http://www.winfield.demon.nl/) || [antiword](https://www.archlinux.org/packages/?name=antiword)

*   **catdoc** — Converter for Microsoft Word, Excel, PowerPoint and RTF files to text.

	[https://wagner.pp.ru/~vitus/software/catdoc/](https://wagner.pp.ru/~vitus/software/catdoc/) || [catdoc](https://www.archlinux.org/packages/?name=catdoc)

*   **[mutool](/index.php/MuPDF "MuPDF")** — All purpose tool based on MuPDF for dealing with document files in various manners.

	[https://mupdf.com/](https://mupdf.com/) || [mupdf-tools](https://www.archlinux.org/packages/?name=mupdf-tools)

*   **[Pandoc](https://en.wikipedia.org/wiki/Pandoc "wikipedia:Pandoc")** — Swiss-army knife for converting markup and document formats.

	[https://pandoc.org/](https://pandoc.org/) || [pandoc](https://www.archlinux.org/packages/?name=pandoc), [pandoc-bin](https://aur.archlinux.org/packages/pandoc-bin/)

*   **unoconv** — Libreoffice-based document converter.

	[http://dag.wiee.rs/home-made/unoconv/](http://dag.wiee.rs/home-made/unoconv/) || [unoconv](https://www.archlinux.org/packages/?name=unoconv)

*   **UnRTF** — Command-line program which converts RTF documents to other formats.

	[https://www.gnu.org/software/unrtf/unrtf.html](https://www.gnu.org/software/unrtf/unrtf.html) || [unrtf](https://www.archlinux.org/packages/?name=unrtf)

### Bibliographic reference managers

See also [Wikipedia:Comparison of reference management software](https://en.wikipedia.org/wiki/Comparison_of_reference_management_software "wikipedia:Comparison of reference management software").

*   **[Bibus](https://en.wikipedia.org/wiki/Bibus "wikipedia:Bibus")** — A bibliographic database that can directly insert references in OpenOffice.org/LibreOffice and generate the bibliographic index.

	[https://sourceforge.net/projects/bibus-biblio/](https://sourceforge.net/projects/bibus-biblio/) || [bibus](https://aur.archlinux.org/packages/bibus/)

*   **DocEar** — Docear is an academic literature suite for searching, organizing and creating academic literature, built upon the mind mapping software Freeplane and the reference manager JabRef.

	[https://www.docear.org](https://www.docear.org) || [docear](https://aur.archlinux.org/packages/docear/)

*   **[JabRef](https://en.wikipedia.org/wiki/JabRef "wikipedia:JabRef")** — Java GUI frontend for managing BibTeX and other bibliographies.

	[https://www.jabref.org/](https://www.jabref.org/) || [jabref](https://aur.archlinux.org/packages/jabref/)

*   **[KBibTeX](https://en.wikipedia.org/wiki/KBibTeX "wikipedia:KBibTeX")** — BibTeX editor by KDE to edit bibliographies used with LaTeX.

	[https://userbase.kde.org/KBibTeX](https://userbase.kde.org/KBibTeX) || [kbibtex](https://www.archlinux.org/packages/?name=kbibtex)

*   **[Mendeley Desktop](https://en.wikipedia.org/wiki/Mendeley "wikipedia:Mendeley")** — Proprietary reference manager and academic social network.

	[https://www.mendeley.com/](https://www.mendeley.com/) || [mendeleydesktop](https://aur.archlinux.org/packages/mendeleydesktop/)

*   **[Pybliographer](https://en.wikipedia.org/wiki/Pybliographer "wikipedia:Pybliographer")** — Tool for managing bibliographic databases.

	[https://pybliographer.org/](https://pybliographer.org/) || [pybliographer](https://aur.archlinux.org/packages/pybliographer/)

*   **[Referencer](https://en.wikipedia.org/wiki/Referencer "wikipedia:Referencer")** — GNOME application to organize documents or references, and ultimately generate a BibTeX bibliography file.

	[https://launchpad.net/referencer/](https://launchpad.net/referencer/) || [referencer](https://aur.archlinux.org/packages/referencer/)

*   **[Zotero](https://en.wikipedia.org/wiki/Zotero "wikipedia:Zotero")** — An easy-to-use tool to help you collect, organize, cite, and share your research sources. Can import and export BibTeX and has browser extensions.

	[https://www.zotero.org/](https://www.zotero.org/) || [zotero](https://aur.archlinux.org/packages/zotero/)

### Readers and viewers

#### PDF and DjVu

See [PDF, PS and DjVu](/index.php/PDF,_PS_and_DjVu "PDF, PS and DjVu").

#### E-book

**Note:** Some [PDF and DjVu viewers](/index.php/PDF,_PS_and_DjVu#Viewers "PDF, PS and DjVu") also support other e-book formats.

*   **Bookworm** — Simple, focused e-book reader for Elementary OS with EPUB, PDF, Mobipocket and Comicbook support.

	[https://babluboy.github.io/bookworm/](https://babluboy.github.io/bookworm/) || [bookworm](https://www.archlinux.org/packages/?name=bookworm)

*   **[Calibre](https://en.wikipedia.org/wiki/Calibre_(software) "wikipedia:Calibre (software)")** — E-book library management application that can also edit EPUB files, convert between different formats and sync with a variety of e-book readers. Supported formats include CHM, Comicbook, DjVu, DOCX, EPUB, FictionBook, HTML, HTMLZ, Kindle, LIT, LRF, Mobipocket, ODT, PDF, PRC, PDB, PML, RB, RTF, SNB, TCR, TXT and TXTZ.

	[https://calibre-ebook.com/](https://calibre-ebook.com/) || [calibre](https://www.archlinux.org/packages/?name=calibre)

*   **Cool Reader** — E-book viewer with many supported formats such as EPUB (non-DRM), FictionBook, TXT, RTF, HTML, CHM and TCR.

	[https://sourceforge.net/projects/crengine/](https://sourceforge.net/projects/crengine/) || [coolreader](https://aur.archlinux.org/packages/coolreader/)

*   **[FBReader](https://en.wikipedia.org/wiki/FBReader "wikipedia:FBReader")** — E-book viewer with many supported formats such as EPUB, FictionBook, HTML, plucker, PalmDoc, zTxt, TCR, CHM, RTF, OEB, Mobipocket (non-DRM) and TXT.

	[https://fbreader.org/](https://fbreader.org/) || [fbreader](https://www.archlinux.org/packages/?name=fbreader)

*   **Foliate** — Simple and modern GTK eBook reader.

	[https://johnfactotum.github.io/foliate/](https://johnfactotum.github.io/foliate/) || [foliate](https://www.archlinux.org/packages/?name=foliate)

*   **GNOME Books** — E-book manager application for GNOME with EPUB, Mobipocket, FictionBook, DjVu and Comicbook support.

	[https://wiki.gnome.org/Apps/Books](https://wiki.gnome.org/Apps/Books) || [gnome-books](https://www.archlinux.org/packages/?name=gnome-books)

*   **Lector** — Qt based e-book reader with PDF, EPUB, Kindle, Mobipocket and Comicbook support.

	[https://github.com/BasioMeusPuga/Lector](https://github.com/BasioMeusPuga/Lector) || [lector-git](https://aur.archlinux.org/packages/lector-git/)

*   **[Sigil](https://en.wikipedia.org/wiki/Sigil_(application) "wikipedia:Sigil (application)")** — WYSIWYG EPUB e-book editor.

	[https://sigil-ebook.com/](https://sigil-ebook.com/) || [sigil](https://www.archlinux.org/packages/?name=sigil)

#### Comic book

*   **Buoh** — Online strips comics reader for GNOME.

	[http://buoh.steve-o.org/](http://buoh.steve-o.org/) || [buoh](https://www.archlinux.org/packages/?name=buoh)

*   **MComix** — GTK2 image viewer specifically designed to handle comic book archives (fork of Comix). Also includes library manager.

	[https://sourceforge.net/projects/mcomix/](https://sourceforge.net/projects/mcomix/) || [mcomix](https://www.archlinux.org/packages/?name=mcomix)

*   **MComix-GTK3** — GTK3 image viewer specifically designed to handle comic book archives (unmerged patch for MComix). Works well on hidpi screens. Also includes library manager.

	[https://github.com/multiSnow/mcomix3](https://github.com/multiSnow/mcomix3) || [mcomix-gtk3-git](https://aur.archlinux.org/packages/mcomix-gtk3-git/)

*   **Peruse** — Comic book reader by KDE.

	[https://peruse.kde.org/](https://peruse.kde.org/) || [peruse-git](https://aur.archlinux.org/packages/peruse-git/)

*   **QComicBook** — Viewer for comic book archives that aims at convenience and simplicity.

	[https://github.com/stolowski/QComicBook](https://github.com/stolowski/QComicBook) || [qcomicbook](https://aur.archlinux.org/packages/qcomicbook/)

*   **YACReader** — Comic book viewer written in C++ and Qt5\. Comes with YACReaderLibrary for managing comics.

	[https://yacreader.com/](https://yacreader.com/) || [yacreader](https://aur.archlinux.org/packages/yacreader/)

#### CHM

See also [Wikipedia:Microsoft Compiled HTML Help](https://en.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help "wikipedia:Microsoft Compiled HTML Help").

*   **Archmage** — Extensible reader and decompiler for files in the CHM format.

	[https://github.com/dottedmag/archmage](https://github.com/dottedmag/archmage) || [archmage](https://aur.archlinux.org/packages/archmage/)

*   **Kchmviewer** — Qt-based CHM viewer that uses chmlib and borrows some ideas from xchm. It does not depend on [KDE](/index.php/KDE "KDE"), but it can be compiled to integrate with it.

	[http://www.ulduzsoft.com/linux/kchmviewer/](http://www.ulduzsoft.com/linux/kchmviewer/) || [kchmviewer](https://www.archlinux.org/packages/?name=kchmviewer)

*   **[xCHM](https://en.wikipedia.org/wiki/xCHM "wikipedia:xCHM")** — Lightweight CHM viewer, based on chmlib.

	[http://xchm.sourceforge.net/](http://xchm.sourceforge.net/) || [xchm](https://www.archlinux.org/packages/?name=xchm)

### Document managers

*   **GNOME Documents** — Document manager application for GNOME with PDF, DVI, XPS, PostScript, Microsoft Office, LibreOffice and Google Docs support.

	[https://wiki.gnome.org/Apps/Documents](https://wiki.gnome.org/Apps/Documents) || [gnome-documents](https://www.archlinux.org/packages/?name=gnome-documents)

*   **Paperwork** — Personal document manager. It manages scanned documents and PDFs.

	[https://openpaper.work/](https://openpaper.work/) || [paperwork](https://www.archlinux.org/packages/?name=paperwork)

### Scanning software

See [SANE#Install a frontend](/index.php/SANE#Install_a_frontend "SANE").

*   **Scan Tailor** — Interactive post-processing tool for scanned pages.

	[http://scantailor.org/](http://scantailor.org/) || [scantailor](https://www.archlinux.org/packages/?name=scantailor)

### OCR software

#### Console

See also [Wikipedia:Comparison of optical character recognition software](https://en.wikipedia.org/wiki/Comparison_of_optical_character_recognition_software "wikipedia:Comparison of optical character recognition software").

*   **[CuneiForm](https://en.wikipedia.org/wiki/CuneiForm_(software) "wikipedia:CuneiForm (software)")** — Command line OCR system originally developed and open sourced by Cognitive technologies. Supported languages: eng, ger, fra, rus, swe, spa, ita, ruseng, ukr, srp, hrv, pol, dan, por, dut, cze, rum, hun, bul, slo, lav, lit, est, tur.

	[https://launchpad.net/cuneiform-linux](https://launchpad.net/cuneiform-linux) || [cuneiform](https://www.archlinux.org/packages/?name=cuneiform)

*   **[GOCR](https://en.wikipedia.org/wiki/GOCR "wikipedia:GOCR")** — OCR engine which also supports barcode recognition.

	[https://www-e.uni-magdeburg.de/jschulen/ocr/](https://www-e.uni-magdeburg.de/jschulen/ocr/) || [gocr](https://www.archlinux.org/packages/?name=gocr)

*   **[Ocrad](https://en.wikipedia.org/wiki/Ocrad "wikipedia:Ocrad")** — OCR program based on a feature extraction method.

	[https://www.gnu.org/software/ocrad/](https://www.gnu.org/software/ocrad/) || [ocrad](https://www.archlinux.org/packages/?name=ocrad)

*   **[OCRopus](https://en.wikipedia.org/wiki/OCRopus "wikipedia:OCRopus")** — OCR *platform*, modules exist for document layout analysis, OCR engines (it can use Tesseract or its own engine), natural language modeling, etc.

	[https://github.com/tmbdev/ocropy](https://github.com/tmbdev/ocropy) || [ocropy](https://aur.archlinux.org/packages/ocropy/)

*   **[Tesseract](https://en.wikipedia.org/wiki/Tesseract_(software) "wikipedia:Tesseract (software)")** — Accurate open source OCR engine. Package splitted, you need install some datafiles for each language ([tesseract-data-eng](https://www.archlinux.org/packages/?name=tesseract-data-eng) for example).

	[https://github.com/tesseract-ocr](https://github.com/tesseract-ocr) || [tesseract](https://www.archlinux.org/packages/?name=tesseract)

#### Graphical

*   **gImageReader** — Graphical GTK/Qt frontend to Tesseract.

	[https://github.com/manisandro/gImageReader](https://github.com/manisandro/gImageReader) || GTK: [gimagereader-gtk](https://www.archlinux.org/packages/?name=gimagereader-gtk), Qt: [gimagereader-qt](https://www.archlinux.org/packages/?name=gimagereader-qt)

*   **[gscan2pdf](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#gscan2pdf "wikipedia:Scanner Access Now Easy")** — Scans, runs an OCR engine, minor post-processing, creates a document.

	[http://gscan2pdf.sourceforge.net/](http://gscan2pdf.sourceforge.net/) || [gscan2pdf](https://www.archlinux.org/packages/?name=gscan2pdf)

*   **Linux-Intelligent-Ocr-Solution** — Easy-OCR solution and Tesseract trainer for converting print into text using either scanner or a camera.

	[https://sourceforge.net/projects/lios/](https://sourceforge.net/projects/lios/) || [lios-git](https://aur.archlinux.org/packages/lios-git/)

*   **[OCRFeeder](https://en.wikipedia.org/wiki/OCRFeeder "wikipedia:OCRFeeder")** — Python GUI for Gnome which performs document analysis and rendition, and can use either CuneiForm, GOCR, Ocrad or Tesseract as OCR engines. It can import from PDF or image files, and export to HTML or OpenDocument.

	[https://wiki.gnome.org/Apps/OCRFeeder](https://wiki.gnome.org/Apps/OCRFeeder) || [ocrfeeder](https://www.archlinux.org/packages/?name=ocrfeeder)

*   **Paperwork** — Personal document manager. It manages scanned documents and PDFs.

	[https://openpaper.work/](https://openpaper.work/) || [paperwork](https://www.archlinux.org/packages/?name=paperwork)

*   **[YAGF](/index.php/YAGF "YAGF")** — Graphical interface for the CuneiForm text recognition program on the Linux platform.

	[https://sourceforge.net/projects/yagf-ocr/](https://sourceforge.net/projects/yagf-ocr/) || [yagf](https://aur.archlinux.org/packages/yagf/)

### Notes

#### Note-taking software

See also [Wikipedia:Comparison of notetaking software](https://en.wikipedia.org/wiki/Comparison_of_notetaking_software "wikipedia:Comparison of notetaking software").

##### Console

*   **Geeknote** — Command line client for Evernote.

	[http://geeknote.me/](http://geeknote.me/) || [geeknote-git](https://aur.archlinux.org/packages/geeknote-git/)

*   **hierarchical notebook** — Program to organize many kinds of data (addresses, to-do lists, ideas, book reviews, etc.) in one place using the XML format.

	[http://hnb.sourceforge.net/](http://hnb.sourceforge.net/) || [hnb](https://aur.archlinux.org/packages/hnb/)

*   **[Org mode](https://en.wikipedia.org/wiki/org-mode "wikipedia:org-mode")** — [Emacs](/index.php/Emacs "Emacs") mode for notes, project planning and authoring.

	[https://orgmode.org/](https://orgmode.org/) || [emacs-org-mode](https://aur.archlinux.org/packages/emacs-org-mode/)

*   **pynote** — Manage notes on the commandline.

	[https://github.com/rumpelsepp/pynote](https://github.com/rumpelsepp/pynote) || [pynote](https://aur.archlinux.org/packages/pynote/)

*   **tnote** — Small note taking program for the terminal.

	[https://sourceforge.net/projects/tnote/](https://sourceforge.net/projects/tnote/) || [tnote](https://aur.archlinux.org/packages/tnote/)

*   **Vimwiki** — Personal wiki for [Vim](/index.php/Vim "Vim") – interlinked, plain text files written in a markup language.

	[https://vimwiki.github.io/](https://vimwiki.github.io/) || [vim-vimwiki](https://aur.archlinux.org/packages/vim-vimwiki/)

##### Graphical

*   **[BasKet](https://en.wikipedia.org/wiki/BasKet_Note_Pads "wikipedia:BasKet Note Pads")** — Application for organizing, sharing, and taking notes. It can manage various types of information such as to-do lists, links, pictures, and other types, similar to a scrapbook.

	[https://basket-notepads.github.io/](https://basket-notepads.github.io/) || [basket](https://www.archlinux.org/packages/?name=basket)

*   **Boostnote** — Note-taking application for programmers that focuses on markdown, snippets, and customizability. Based on the [Electron](https://electronjs.org/) platform.

	[https://boostnote.io/](https://boostnote.io/) || [boostnote](https://aur.archlinux.org/packages/boostnote/)

*   **Cherrytree** — Hierarchical note taking application, featuring rich text and syntax highlighting, storing data in a single xml or sqlite file.

	[https://www.giuspen.com/cherrytree/](https://www.giuspen.com/cherrytree/) || [cherrytree](https://aur.archlinux.org/packages/cherrytree/)

*   **Elephant** — Notetaker with a classic interface.

	[http://elephant.mine.nu/](http://elephant.mine.nu/) || [elephant](https://aur.archlinux.org/packages/elephant/)

*   **FromScratch** — Simple but smart note-taking application that you can use as a quick note taking or todo app. Based on the [Electron](https://electronjs.org/) platform.

	[https://fromscratch.rocks/](https://fromscratch.rocks/) || [fromscratch-bin](https://aur.archlinux.org/packages/fromscratch-bin/)

*   **GNOME Notes** — Note editor for GNOME designed to remain simple to use.

	[https://wiki.gnome.org/Apps/Notes](https://wiki.gnome.org/Apps/Notes) || [gnome-notes](https://www.archlinux.org/packages/?name=gnome-notes)

*   **[Gnote](https://en.wikipedia.org/wiki/Gnote "wikipedia:Gnote")** — Port of Tomboy to C++. It is the same note taking application, including most of the add-ins.

	[https://wiki.gnome.org/Apps/Gnote](https://wiki.gnome.org/Apps/Gnote) || [gnote](https://www.archlinux.org/packages/?name=gnote)

*   **Joplin** — Note taking and to-do application, which can handle a large number of notes organized into notebooks. Based on the [Electron](https://electronjs.org/) platform.

	[https://joplin.cozic.net/](https://joplin.cozic.net/) || [joplin](https://aur.archlinux.org/packages/joplin/)

*   **KeepNote** — Cross-platform GTK note-taking application with rich text formatting.

	[http://keepnote.org](http://keepnote.org) || [keepnote](https://aur.archlinux.org/packages/keepnote/)

*   **KJots** — Note taking application for KDE.

	[https://userbase.kde.org/KJots](https://userbase.kde.org/KJots) || [kjots](https://www.archlinux.org/packages/?name=kjots)

*   **Laverna** — JavaScript note taking application with Markdown editor and encryption support. Based on the [Electron](https://electronjs.org/) platform.

	[https://laverna.cc/](https://laverna.cc/) || [laverna](https://aur.archlinux.org/packages/laverna/)

*   **Mikidown** — Note taking application featuring markdown syntax.

	[https://shadowkyogre.github.io/mikidown/](https://shadowkyogre.github.io/mikidown/) || [mikidown](https://aur.archlinux.org/packages/mikidown/)

*   **[MyNotex](https://en.wikipedia.org/wiki/MyNotex "wikipedia:MyNotex")** — Note-taking, document file and activity manager.

	[https://sites.google.com/site/mynotex/](https://sites.google.com/site/mynotex/) || [mynotex](https://aur.archlinux.org/packages/mynotex/)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") Notes** — Simple notes app for Nextcloud.

	[https://github.com/nextcloud/notes](https://github.com/nextcloud/notes) || [nextcloud-app-notes](https://www.archlinux.org/packages/?name=nextcloud-app-notes)

*   **NixNote** — Helps you take notes and stay organized. Create text notes, attach files or images, and even synchronize with Evernote. Formerly called Nevernote.

	[http://nixnote.org/](http://nixnote.org/) || [nixnote2](https://aur.archlinux.org/packages/nixnote2/)

*   **Notes** — Note-taking application, write down your thoughts.

	[https://github.com/nuttyartist/notes](https://github.com/nuttyartist/notes) || [notes](https://aur.archlinux.org/packages/notes/)

*   **NotesTree** — Note taking application, which organizes notes in a hierarchical (tree like) structure.

	[https://bitbucket.org/baltic/notestree/overview](https://bitbucket.org/baltic/notestree/overview) || [notes-tree](https://aur.archlinux.org/packages/notes-tree/)

*   **Notes-Up** — Markdown notes editor and manager for elementaryOS.

	[https://github.com/Philip-Scott/Notes-up](https://github.com/Philip-Scott/Notes-up) || [notes-up](https://aur.archlinux.org/packages/notes-up/)

*   **nvPY** — Simplenote syncing note-taking application, inspired by Notational Velocity and ResophNotes, but uglier and cross-platformerer.

	[https://github.com/cpbotha/nvpy](https://github.com/cpbotha/nvpy) || [nvpy-git](https://aur.archlinux.org/packages/nvpy-git/)

*   **OutWiker** — Store notes in a tree.

	[https://jenyay.net/Outwiker/English](https://jenyay.net/Outwiker/English) || [outwiker](https://aur.archlinux.org/packages/outwiker/)

*   **[QOwnNotes](https://en.wikipedia.org/wiki/QOwnNotes "wikipedia:QOwnNotes")** — Notepad and todo list manager with markdown support and optional ownCloud integration built on Qt5.

	[https://www.qownnotes.org/](https://www.qownnotes.org/) || [qownnotes](https://aur.archlinux.org/packages/qownnotes/)

*   **Renku** — Note taking application based on Akonadi.

	[https://zanshin.kde.org/](https://zanshin.kde.org/) || [zanshin](https://www.archlinux.org/packages/?name=zanshin)

*   **[Simplenote](https://en.wikipedia.org/wiki/Simplenote "wikipedia:Simplenote")** — The simplest way to keep notes. Based on the [Electron](https://electronjs.org/) platform.

	[https://simplenote.com/](https://simplenote.com/) || [simplenote-electron-bin](https://aur.archlinux.org/packages/simplenote-electron-bin/)

*   **Standard Notes** — Simple and private notes application which focuses on simplicity, and encrypts data locally before it ever touches a cloud. Based on the [Electron](https://electronjs.org/) platform.

	[https://standardnotes.org/](https://standardnotes.org/) || [standardnotes-desktop](https://aur.archlinux.org/packages/standardnotes-desktop/) [sn-bin](https://aur.archlinux.org/packages/sn-bin/)

*   **[TagSpaces](https://en.wikipedia.org/wiki/TagSpaces "wikipedia:TagSpaces")** — Offline personal data manager for managing of your local files. Based on the [Electron](https://electronjs.org/) platform.

	[https://www.tagspaces.org/](https://www.tagspaces.org/) || [tagspaces](https://aur.archlinux.org/packages/tagspaces/) [tagspaces-bin](https://aur.archlinux.org/packages/tagspaces-bin/)

*   **[TiddlyWiki](https://en.wikipedia.org/wiki/TiddlyWiki "wikipedia:TiddlyWiki")** — Unique non-linear notebook for capturing, organizing and sharing complex information.

	[https://tiddlywiki.com/](https://tiddlywiki.com/) || [tiddlywiki](https://aur.archlinux.org/packages/tiddlywiki/)

*   **[Tomboy](https://en.wikipedia.org/wiki/Tomboy_(software) "wikipedia:Tomboy (software)")** — Desktop note-taking application for Linux and Unix with a wiki-like linking system to connect notes together.

	[https://wiki.gnome.org/Apps/Tomboy](https://wiki.gnome.org/Apps/Tomboy) || [tomboy](https://www.archlinux.org/packages/?name=tomboy)

*   **TreeLine** — Store almost any kind of information in a tree structure, which makes it easy to keep things organized.

	[http://treeline.bellz.org/](http://treeline.bellz.org/) || [treeline-unstable](https://aur.archlinux.org/packages/treeline-unstable/)

*   **TuxCards** — Hierarchical notebook to enter and manage ever every kind of notes and ideas in a structured manner.

	[http://tuxcards.de/](http://tuxcards.de/) || [tuxcards](https://www.archlinux.org/packages/?name=tuxcards)

*   **VNote** — Vim-inspired note-taking application that knows programmers and Markdown better.

	[https://tamlok.github.io/vnote/](https://tamlok.github.io/vnote/) || [vnote](https://aur.archlinux.org/packages/vnote/)

*   **[WikidPad](https://en.wikipedia.org/wiki/WikidPad "wikipedia:WikidPad")** — Wiki-like notebook for storing your thoughts, ideas, todo lists, contacts, or anything else you can think of to write down.

	[http://wikidpad.sourceforge.net/](http://wikidpad.sourceforge.net/) || [wikidpad](https://aur.archlinux.org/packages/wikidpad/)

*   **WizNote** — Cloud based note-taking client.

	[https://github.com/WizTeam/WizQTClient](https://github.com/WizTeam/WizQTClient) || [wiznote](https://www.archlinux.org/packages/?name=wiznote)

*   **[Zim](/index.php/Zim "Zim")** — WYSIWYG text editor that aims at bringing the concept of a wiki to the desktop.

	[https://zim-wiki.org/](https://zim-wiki.org/) || [zim](https://www.archlinux.org/packages/?name=zim)

*   **zNotes** — Lightweight application for notes management with simple interface.

	[https://sourceforge.net/projects/znotes/](https://sourceforge.net/projects/znotes/) || [znotes](https://aur.archlinux.org/packages/znotes/)

#### Stylus note-taking

*   **Cournal** — Collaborative note taking and journal application using a stylus. It allows multiple users to annotate PDF files in real-time.

	[https://github.com/flyser/cournal](https://github.com/flyser/cournal) || [cournal](https://aur.archlinux.org/packages/cournal/)

*   **Write** — A proprietary word processor for handwriting.

	[http://www.styluslabs.com/](http://www.styluslabs.com/) || [write_stylus](https://aur.archlinux.org/packages/write_stylus/)

*   **Xournal** — Application for notetaking, sketching and keeping a journal using a stylus. Capable of annotating existing PDF files as well.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://aur.archlinux.org/packages/xournal/)

*   **Xournal++** — Notetaking software designed around a tablet. C++ rewrite of Xournal with PDF annotation support.

	[https://github.com/xournalpp/xournalpp](https://github.com/xournalpp/xournalpp) || [xournalpp](https://www.archlinux.org/packages/?name=xournalpp)

#### Diary

*   **Almanah** — Small GTK application to allow you to keep a diary of your life.

	[https://wiki.gnome.org/Apps/Almanah_Diary](https://wiki.gnome.org/Apps/Almanah_Diary) || [almanah](https://www.archlinux.org/packages/?name=almanah)

*   **Hazama** — Simple and highly customizable application for keeping diary. There is no calendar but a big list that contains preview of diaries.

	[https://hazama.cc/](https://hazama.cc/) || [hazama](https://aur.archlinux.org/packages/hazama/)

*   **Lifeograph** — Off-line and private journal and note taking application. It offers a rich feature set presented in a clean and simple user interface.

	[http://lifeograph.sourceforge.net/](http://lifeograph.sourceforge.net/) || [lifeograph](https://aur.archlinux.org/packages/lifeograph/)

*   **RedNotebook** — Modern journal, which lets you format, tag and search your entries.

	[https://rednotebook.sourceforge.io/](https://rednotebook.sourceforge.io/) || [rednotebook](https://aur.archlinux.org/packages/rednotebook/)

#### Mind-mapping

See also [Wikipedia:List of concept- and mind-mapping software](https://en.wikipedia.org/wiki/List_of_concept-_and_mind-mapping_software "wikipedia:List of concept- and mind-mapping software").

*   **[FreeMind](https://en.wikipedia.org/wiki/FreeMind "wikipedia:FreeMind")** — Mind-mapping software written in Java.

	[http://freemind.sourceforge.net](http://freemind.sourceforge.net) || [freemind](https://www.archlinux.org/packages/?name=freemind)

*   **[Freeplane](https://en.wikipedia.org/wiki/Freeplane "wikipedia:Freeplane")** — Fork of FreeMind, supports thinking, sharing information and getting things done at work. The software can be used for mind mapping and analyzing the information contained in mind maps.

	[https://www.freeplane.org/](https://www.freeplane.org/) || [freeplane](https://aur.archlinux.org/packages/freeplane/)

*   **Labyrinth** — Lightweight mind-mapping tool, written in Python using GTK, with support for image import and drawing.

	[https://github.com/labyrinth-team/labyrinth](https://github.com/labyrinth-team/labyrinth) || [labyrinth](https://aur.archlinux.org/packages/labyrinth/)

*   **Semantik** — Mind-mapping application for KDE.

	[https://waf.io/semantik.html](https://waf.io/semantik.html) || [semantik](https://aur.archlinux.org/packages/semantik/)

*   **TreeSheets** — The ultimate replacement for spreadsheets, mind mappers, outliners, PIMs, text editors and small databases.

	[http://strlen.com/treesheets/](http://strlen.com/treesheets/) || [treesheets-git](https://aur.archlinux.org/packages/treesheets-git/)

*   **View Your Mind** — Tool to generate and manipulate maps which show your thoughts. Such maps can help you to improve your creativity and effectivity. You can use them for time management, to organize tasks, to get an overview over complex contexts, to sort your ideas etc.

	[http://www.insilmaril.de/vym/](http://www.insilmaril.de/vym/) || [vym](https://www.archlinux.org/packages/?name=vym)

*   **[Visual Understanding Environment](https://en.wikipedia.org/wiki/Visual_Understanding_Environment "wikipedia:Visual Understanding Environment")** — Flexible tools for managing and integrating digital resources in support of teaching, learning and research.

	[http://vue.tufts.edu](http://vue.tufts.edu) || [vue](https://aur.archlinux.org/packages/vue/)

*   **[XMind](https://en.wikipedia.org/wiki/XMind "wikipedia:XMind")** — Brainstorming and mind mapping application. It provides a rich set of different visualization styles, and allows sharing of created mind maps via their website.

	[https://www.xmind.net/](https://www.xmind.net/) || [xmind](https://aur.archlinux.org/packages/xmind/)

*   **MindMaster** — commercial mindmap and brainstorm software with modern UI and beautiful template.It also provides online mindmap service and cross-platform sharing.

	[https://www.edrawsoft.com/mindmaster/](https://www.edrawsoft.com/mindmaster/) || [mindmaster](https://aur.archlinux.org/packages/mindmaster/)

#### Sticky notes

*   **GloboNote** — Easy to use desktop note taking application. You can use it to create sticky notes, to-do lists, personal journals, reminders and other notes all in one application.

	[https://globonote.info/](https://globonote.info/) || [globonote](https://aur.archlinux.org/packages/globonote/)

*   **KNotes** — Program that lets you write the computer equivalent of sticky notes. Part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/utilities/knotes/](https://www.kde.org/applications/utilities/knotes/) || [knotes](https://www.archlinux.org/packages/?name=knotes)

*   **MyNotes** — Sticky note application. An icon appears in the system tray and from it you can create and manage your sticky notes.

	[https://github.com/j4321/MyNotes](https://github.com/j4321/MyNotes) || [mynotes](https://aur.archlinux.org/packages/mynotes/)

*   **Notejot** — Stupidly simple sticky notes applet for elementaryOS.

	[https://github.com/lainsce/notejot](https://github.com/lainsce/notejot) || [notejot](https://aur.archlinux.org/packages/notejot/)

*   **Notes** — Provides you a quick way to paste text, to write down a list of things, to leave a note to your friend, or whatever you had do with Post-It's.

	[https://goodies.xfce.org/projects/panel-plugins/xfce4-notes-plugin](https://goodies.xfce.org/projects/panel-plugins/xfce4-notes-plugin) || [xfce4-notes-plugin](https://www.archlinux.org/packages/?name=xfce4-notes-plugin)

*   **qtPad** — Modern and customizable sticky note application written in PyQt5.

	[https://gitlab.com/william.belanger/qtpad](https://gitlab.com/william.belanger/qtpad) || [qtpad-git](https://aur.archlinux.org/packages/qtpad-git/)

*   **xNots** — Desktop post-it/sticky note system for the Unix geek.

	[https://github.com/thePalindrome/xnots](https://github.com/thePalindrome/xnots) || [xnots-git](https://aur.archlinux.org/packages/xnots-git/)

*   **Xpad** — Sticky note application for jotting down things to remember.

	[https://launchpad.net/xpad](https://launchpad.net/xpad) || [xpad](https://www.archlinux.org/packages/?name=xpad)

### Special writing environments

#### Distraction-free writing

See also [#Markdown editors](#Markdown_editors) and [Wikipedia:Full-screen writing program](https://en.wikipedia.org/wiki/Full-screen_writing_program "wikipedia:Full-screen writing program").

*   **FocusWriter** — Simple, distraction-free writing environment. It utilizes a hide-away interface that you access by moving your mouse to the edges of the screen, allowing the program to have a familiar look and feel to it while still getting out of the way so that you can immerse yourself in your work.

	[https://gottcode.org/focuswriter/](https://gottcode.org/focuswriter/) || [focuswriter](https://aur.archlinux.org/packages/focuswriter/)

*   **[PyRoom](https://en.wikipedia.org/wiki/PyRoom "wikipedia:PyRoom")** — Fullscreen editor without buttons, widgets, formatting options, menus and with only the minimum of required dialog windows, it doesn't have any distractions and lets you focus on writing and only writing.

	[https://pyroom.org/](https://pyroom.org/) || [pyroom](https://aur.archlinux.org/packages/pyroom/)

*   **Quilter** — Focus on your writing.

	[https://github.com/lainsce/quilter](https://github.com/lainsce/quilter) || [quilter](https://aur.archlinux.org/packages/quilter/)

*   **TextRoom** — Fullscreen text editor for writers.

	[https://github.com/dbuksbaum/TextRoom](https://github.com/dbuksbaum/TextRoom) || [textroom](https://aur.archlinux.org/packages/textroom/)

#### Story writing

*   **Manuskript** — Provides a rich environment to help writers create their first draft and then further refine and edit their masterpiece.

	[http://www.theologeek.ch/manuskript/](http://www.theologeek.ch/manuskript/) || [manuskript-git](https://aur.archlinux.org/packages/manuskript-git/)

*   **NovProg** — Tool to graph your progress in writing a NaNoWriMo style novel.

	[https://gottcode.org/novprog/](https://gottcode.org/novprog/) || [novprog](https://aur.archlinux.org/packages/novprog/)

*   **oStorybook** — Tool for writers, essayists, authors from the draft to the final work.

	[https://ostorybook.tuxfamily.org/?lng=en](https://ostorybook.tuxfamily.org/?lng=en) || [ostorybook](https://aur.archlinux.org/packages/ostorybook/)

#### Screenwriting

*   **KIT Scenarist** — Simple and powerful application for creating screenplays.

	[https://kitscenarist.ru/en/](https://kitscenarist.ru/en/) || [scenarist](https://aur.archlinux.org/packages/scenarist/)

*   **Magic Fountain** — Fountain syntax editor and viewer for writing screenplays.

	[https://aztorius.github.io/magicfountain/](https://aztorius.github.io/magicfountain/) || [magicfountain](https://aur.archlinux.org/packages/magicfountain/)

*   **[Trelby](https://en.wikipedia.org/wiki/Trelby "wikipedia:Trelby")** — Simple, fast and elegantly laid out to make screenwriting simple.

	[https://www.trelby.org/](https://www.trelby.org/) || [trelby-git](https://aur.archlinux.org/packages/trelby-git/)

### Language

#### Dictionary and thesaurus

*   **Artha** — English thesaurus that works completely off-line and is based on WordNet.

	[http://artha.sourceforge.net/](http://artha.sourceforge.net/) || [artha](https://aur.archlinux.org/packages/artha/)

*   **Gjiten Kai** — Rewrite of Gjiten, a GTK Japanese dictionary.

	[http://odrevet.github.io/gjitenkai/](http://odrevet.github.io/gjitenkai/) || [gjitenkai-git](https://aur.archlinux.org/packages/gjitenkai-git/)

*   **GNOME Dictionary** — GNOME application to check word definitions and spellings in an online dictionary.

	[https://wiki.gnome.org/Apps/Dictionary](https://wiki.gnome.org/Apps/Dictionary) || [gnome-dictionary](https://www.archlinux.org/packages/?name=gnome-dictionary)

*   **GoldenDict** — Feature-rich dictionary lookup program.

	[http://www.goldendict.org/](http://www.goldendict.org/) || [goldendict](https://www.archlinux.org/packages/?name=goldendict)

*   **Kiten** — Japanese reference and study tool. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/kiten/](https://www.kde.org/applications/education/kiten/) || [kiten](https://www.archlinux.org/packages/?name=kiten)

*   **MATE Dictionary** — MATE application to look up words in dictionary sources.

	[https://github.com/mate-desktop/mate-utils](https://github.com/mate-desktop/mate-utils) || [mate-utils](https://www.archlinux.org/packages/?name=mate-utils)

*   **OpenDict** — Computer dictionary, which supports popular computer dictionary formats including Slowo and Mova. It also acts as a client for DICT servers.

	[http://opendict.sourceforge.net/](http://opendict.sourceforge.net/) || [opendict](https://aur.archlinux.org/packages/opendict/)

*   **QStarDict** — Dictionary program written using Qt. The user interface is similar to StarDict.

	[http://qstardict.ylsoftware.com/](http://qstardict.ylsoftware.com/) || [qstardict](https://www.archlinux.org/packages/?name=qstardict)

*   **[sdcv](/index.php/Sdcv "Sdcv")** — Command line dictionary. It provides access to dictionaries in StarDict's format.

	[http://dushistov.github.io/sdcv/](http://dushistov.github.io/sdcv/) || [sdcv](https://www.archlinux.org/packages/?name=sdcv)

*   **StarDict** — International dictionary software.

	[http://stardict-4.sourceforge.net/](http://stardict-4.sourceforge.net/) || [stardict](https://www.archlinux.org/packages/?name=stardict)

*   **Xfce4 Dictionary** — Search different kinds of dictionary services for words or phrases.

	[https://goodies.xfce.org/projects/applications/xfce4-dict](https://goodies.xfce.org/projects/applications/xfce4-dict) || [xfce4-dict](https://www.archlinux.org/packages/?name=xfce4-dict)

#### Spell checkers

See [Language checking](/index.php/Language_checking "Language checking").

#### Translation and localization

See also [Wikipedia:Comparison of computer-assisted translation tools](https://en.wikipedia.org/wiki/Comparison_of_computer-assisted_translation_tools "wikipedia:Comparison of computer-assisted translation tools").

*   **[Apertium](https://en.wikipedia.org/wiki/Apertium "wikipedia:Apertium")** — Free and open source rule-based machine translation platform with available language data. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, TMX, MediaWiki and others.

	[https://www.apertium.org/](https://www.apertium.org/) || [apertium](https://aur.archlinux.org/packages/apertium/)

*   **Crow Translate** — Simple and lightweight translator that allows to translate and speak text using Google, Yandex and Bing.

	[https://crow-translate.github.io/](https://crow-translate.github.io/) || [crow-translate](https://aur.archlinux.org/packages/crow-translate/)

*   **[Gtranslator](https://en.wikipedia.org/wiki/Gtranslator "wikipedia:Gtranslator")** — Enhanced gettext po file editor for the GNOME. It handles all forms of gettext po files and includes very useful features.

	[https://wiki.gnome.org/Apps/Gtranslator](https://wiki.gnome.org/Apps/Gtranslator) || [gtranslator](https://www.archlinux.org/packages/?name=gtranslator)

*   **Lokalize** — Standard [KDE](/index.php/KDE "KDE") tool for software translation. It includes basic editing of PO files, support for glossary, translation memory, project managing, etc. It belongs to [kdesdk](https://www.archlinux.org/groups/x86_64/kdesdk/)

	[https://userbase.kde.org/Lokalize](https://userbase.kde.org/Lokalize) || [lokalize](https://www.archlinux.org/packages/?name=lokalize)

*   **[Moses](https://en.wikipedia.org/wiki/Moses_(machine_translation) "wikipedia:Moses (machine translation)")** — Statistical machine translation tool (language data not included).

	[http://statmt.org/moses/](http://statmt.org/moses/) || [mosesdecoder](https://aur.archlinux.org/packages/mosesdecoder/)

*   **[OmegaT](https://en.wikipedia.org/wiki/OmegaT "wikipedia:OmegaT")** — General translator's tool which contains a lot of translation memory features and can give suggestions from Google Translate. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, XLIFF/Okapi, MediaWiki, plain text, TMX and others.

	[https://omegat.org/](https://omegat.org/) || [omegat](https://aur.archlinux.org/packages/omegat/)

*   **[Poedit](https://en.wikipedia.org/wiki/Poedit "wikipedia:Poedit")** — Simple translation editor for gettext (PO, POT) and XLIFF.

	[https://poedit.net](https://poedit.net) || [poedit](https://www.archlinux.org/packages/?name=poedit)

*   **Pology** — Set of Python tools for dealing with gettext/po-files.

	[https://techbase.kde.org/Localization/Tools/Pology](https://techbase.kde.org/Localization/Tools/Pology) || [pology](https://aur.archlinux.org/packages/pology/)

*   **[Qt](/index.php/Qt "Qt") Linguist** — Translating Qt C++ and Qt Quick applications into local languages.

	[https://doc.qt.io/qt-5/qtlinguist-index.html](https://doc.qt.io/qt-5/qtlinguist-index.html) || [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools)

*   **Translate Shell** — Command-line interface and interactive shell for Google Translate.

	[https://www.soimort.org/translate-shell/](https://www.soimort.org/translate-shell/) || [translate-shell](https://www.archlinux.org/packages/?name=translate-shell)

*   **[Translate Toolkit](https://en.wikipedia.org/wiki/Translate_Toolkit "wikipedia:Translate Toolkit")** — Localization and translation toolkit, which provides a set of tools for working with localization file formats and files that might need localization.

	[https://toolkit.translatehouse.org/](https://toolkit.translatehouse.org/) || [translate-toolkit](https://www.archlinux.org/packages/?name=translate-toolkit)

*   **[Virtaal](https://en.wikipedia.org/wiki/Virtaal and others.

	[http://virtaal.translatehouse.org/](http://virtaal.translatehouse.org/) || [virtaal](https://aur.archlinux.org/packages/virtaal/)

### Barcode generators and readers

#### Console

*   **barcode** — A tool to convert text strings to printed bars.

	[https://www.gnu.org/software/barcode/](https://www.gnu.org/software/barcode/) || [barcode](https://www.archlinux.org/packages/?name=barcode)

*   **iec16022** — Produce 2D barcodes often also referenced as DataMatrix.

	[https://datenfreihafen.org/projects/iec16022.html](https://datenfreihafen.org/projects/iec16022.html) || [iec16022](https://www.archlinux.org/packages/?name=iec16022)

*   **qrencode** — C library and command line tool for encoding data in a QR Code symbol.

	[https://fukuchi.org/works/qrencode/](https://fukuchi.org/works/qrencode/) || [qrencode](https://www.archlinux.org/packages/?name=qrencode)

*   **ZBar** — Application and library for reading bar codes from various sources.

	[http://zbar.sourceforge.net/](http://zbar.sourceforge.net/) || [zbar](https://www.archlinux.org/packages/?name=zbar)

*   **Zint** — Barcode encoding library and command line tool supporting over 50 symbologies.

	[http://zint.org.uk/](http://zint.org.uk/) || [zint](https://www.archlinux.org/packages/?name=zint)

#### Graphical

*   **gLabels** — Program for creating labels and business cards. It also supports creating barcodes.

	[http://glabels.org/](http://glabels.org/) || [glabels](https://www.archlinux.org/packages/?name=glabels)

*   **QRab** — Simply grabs QR code from screen and copies decoded text into clipboard.

	[https://qrab.sourceforge.io/](https://qrab.sourceforge.io/) || [qrab](https://aur.archlinux.org/packages/qrab/)

*   **Qreator** — Graphical utility for creating QR codes.

	[https://davidplanella.org/qreator/](https://davidplanella.org/qreator/) || [qreator](https://www.archlinux.org/packages/?name=qreator)

*   **QtQR** — QR Code generator and decoder.

	[https://launchpad.net/qr-tools](https://launchpad.net/qr-tools) || [qtqr](https://aur.archlinux.org/packages/qtqr/)

*   **ZBarCam GUI** — Simple GUI for ZBar to read bar codes from various sources.

	[http://zbar.sourceforge.net/](http://zbar.sourceforge.net/) || GTK: [zbar-gtk](https://www.archlinux.org/packages/?name=zbar-gtk), Qt: [zbar-qt](https://www.archlinux.org/packages/?name=zbar-qt)

*   **Zint Barcode Studio** — Barcode generator GUI.

	[http://zint.org.uk/](http://zint.org.uk/) || [zint-qt](https://www.archlinux.org/packages/?name=zint-qt)

## Security

For detailed guides, see the main ArchWiki page, [Security](/index.php/Security "Security").

#### Network security

See also [Wikipedia:Comparison of packet analyzers](https://en.wikipedia.org/wiki/Comparison_of_packet_analyzers "wikipedia:Comparison of packet analyzers").

*   **airgeddon** — Multi-use bash script to audit wireless networks

	[https://github.com/v1s1t0r1sh3r3/airgeddon](https://github.com/v1s1t0r1sh3r3/airgeddon) || [airgeddon-git](https://aur.archlinux.org/packages/airgeddon-git/)

*   **[Arpwatch](https://en.wikipedia.org/wiki/Arpwatch "wikipedia:Arpwatch")** — Tool that monitors ethernet activity and keeps a database of Ethernet/IP address pairings.

	[https://ee.lbl.gov/](https://ee.lbl.gov/) || [arpwatch](https://www.archlinux.org/packages/?name=arpwatch)

*   **bettercap** — Swiss army knife for network attacks and monitoring.

	[https://www.bettercap.org/](https://www.bettercap.org/) || [bettercap](https://www.archlinux.org/packages/?name=bettercap)

*   **Bro** — Powerful network analysis framework that is much different from the typical IDS you may know.

	[https://www.bro.org/](https://www.bro.org/) || [bro-git](https://aur.archlinux.org/packages/bro-git/)

*   **darkstat** — Captures network traffic, calculates statistics about usage, and serves reports over HTTP.

	[https://unix4lyfe.org/darkstat/](https://unix4lyfe.org/darkstat/) || [darkstat](https://www.archlinux.org/packages/?name=darkstat)

*   **[dsniff](https://en.wikipedia.org/wiki/dSniff "wikipedia:dSniff")** — Collection of tools for network auditing and penetration testing.

	[https://www.monkey.org/~dugsong/dsniff/](https://www.monkey.org/~dugsong/dsniff/) || [dsniff](https://www.archlinux.org/packages/?name=dsniff)

*   **[EtherApe](https://en.wikipedia.org/wiki/EtherApe "wikipedia:EtherApe")** — Graphical network monitor for Unix modeled after etherman. Featuring link layer, IP and TCP modes, it displays network activity graphically. Hosts and links change in size with traffic. Color coded protocols display.

	[https://etherape.sourceforge.io/](https://etherape.sourceforge.io/) || [etherape](https://www.archlinux.org/packages/?name=etherape)

*   **[Ettercap](https://en.wikipedia.org/wiki/Ettercap_(software) "wikipedia:Ettercap (software)")** — Multipurpose Network sniffer/analyser/interceptor/logger.

	[https://ettercap.github.io/ettercap/](https://ettercap.github.io/ettercap/) || CLI: [ettercap](https://www.archlinux.org/packages/?name=ettercap), GUI: [ettercap-gtk](https://www.archlinux.org/packages/?name=ettercap-gtk)

*   **GNOME Network Tools** — GNOME interface for various networking tools.

	[https://gitlab.gnome.org/GNOME/gnome-nettool](https://gitlab.gnome.org/GNOME/gnome-nettool) || [gnome-nettool](https://www.archlinux.org/packages/?name=gnome-nettool)

*   **[Honeyd](/index.php/Honeyd "Honeyd")** — Tool that allows the user to set up and run multiple virtual hosts on a computer network.

	[http://www.honeyd.org/](http://www.honeyd.org/) || [honeyd](https://aur.archlinux.org/packages/honeyd/)

*   **hping** — Command-line oriented TCP/IP packet assembler/analyzer.

	[http://hping.org/](http://hping.org/) || [hping](https://www.archlinux.org/packages/?name=hping)

*   **IPTraf** — Console-based network monitoring utility.

	[https://sourceforge.net/projects/iptraf-ng/](https://sourceforge.net/projects/iptraf-ng/) || [iptraf-ng](https://www.archlinux.org/packages/?name=iptraf-ng)

*   **jnettop** — top-like console network traffic visualizer.

	[https://sourceforge.net/projects/jnettop/](https://sourceforge.net/projects/jnettop/) || [jnettop](https://www.archlinux.org/packages/?name=jnettop)

*   **[justniffer](https://en.wikipedia.org/wiki/justniffer "wikipedia:justniffer")** — Network protocol analyzer that captures network traffic and produces logs in a customized way, can emulate Apache web server log files, track response times and extract all "intercepted" files from the HTTP traffic.

	[http://justniffer.sourceforge.net/](http://justniffer.sourceforge.net/) || [justniffer](https://aur.archlinux.org/packages/justniffer/)

*   **Kismet** — 802.11 layer2 wireless network detector, sniffer, and intrusion detection system.

	[https://www.kismetwireless.net/](https://www.kismetwireless.net/) || [kismet](https://www.archlinux.org/packages/?name=kismet)

*   **LinSSID** — Graphical wireless scanner.

	[https://sourceforge.net/projects/linssid/](https://sourceforge.net/projects/linssid/) || [linssid](https://www.archlinux.org/packages/?name=linssid)

*   **Nemesis** — Command-line network packet crafting and injection utility.

	[http://nemesis.sourceforge.net/](http://nemesis.sourceforge.net/) || [nemesis](https://aur.archlinux.org/packages/nemesis/)

*   **Net Activity Viewer** — Graphical network connections viewer, similar in functionality with Netstat.

	[http://netactview.sourceforge.net/](http://netactview.sourceforge.net/) || [netactview](https://aur.archlinux.org/packages/netactview/)

*   **[netsniff-ng](https://en.wikipedia.org/wiki/netsniff-ng "wikipedia:netsniff-ng")** — High performance Linux network sniffer for packet inspection.

	[http://netsniff-ng.org/](http://netsniff-ng.org/) || [netsniff-ng](https://www.archlinux.org/packages/?name=netsniff-ng)

*   **[ngrep](https://en.wikipedia.org/wiki/ngrep "wikipedia:ngrep")** — grep-like utility that allows you to search for network packets on an interface.

	[https://github.com/jpr5/ngrep](https://github.com/jpr5/ngrep) || [ngrep](https://www.archlinux.org/packages/?name=ngrep)

*   **[Nmap](/index.php/Nmap "Nmap")** — Security scanner used to discover hosts and services on a computer network, thus creating a "map" of the network.

	[https://nmap.org/](https://nmap.org/) || [nmap](https://www.archlinux.org/packages/?name=nmap)

*   **[Ntop](/index.php/Ntop "Ntop")** — Network probe that shows network usage in a way similar to what top does for processes.

	[https://www.ntop.org/](https://www.ntop.org/) || [ntop](https://www.archlinux.org/packages/?name=ntop)

*   **pyNeighborhood** — GTK-based SMB/CIFS browsing utility.

	[https://launchpad.net/pyneighborhood](https://launchpad.net/pyneighborhood) || [pyneighborhood](https://www.archlinux.org/packages/?name=pyneighborhood)

*   **Smb4K** — Advanced network neighborhood browser and Samba share mounting utility for KDE.

	[https://smb4k.sourceforge.io/](https://smb4k.sourceforge.io/) || [smb4k](https://www.archlinux.org/packages/?name=smb4k)

*   **[Snort](/index.php/Snort "Snort")** — Network intrusion prevention and detection system.

	[https://www.snort.org/](https://www.snort.org/) || [snort](https://aur.archlinux.org/packages/snort/)

*   **Spectools** — A set of utilities for spectrum analyzer hardware including Wi-Spy devices.

	[https://www.kismetwireless.net/spectools/](https://www.kismetwireless.net/spectools/) || [spectools](https://aur.archlinux.org/packages/spectools/)

*   **[Sshguard](/index.php/Sshguard "Sshguard")** — Daemon that protects SSH and other services against brute-force attacts, similar to Fail2ban.

	[https://www.sshguard.net/](https://www.sshguard.net/) || [sshguard](https://www.archlinux.org/packages/?name=sshguard)

*   **[Suricata](/index.php/Suricata "Suricata")** — High performance Network IDS, IPS and Network Security Monitoring engine.

	[https://suricata-ids.org/](https://suricata-ids.org/) || [suricata](https://aur.archlinux.org/packages/suricata/)

*   **[Tcpdump](https://en.wikipedia.org/wiki/tcpdump "wikipedia:tcpdump")** — Common console-based packet analyzer that allows the user to intercept and display TCP/IP and other packets being transmitted or received over a network.

	[http://www.tcpdump.org/](http://www.tcpdump.org/) || [tcpdump](https://www.archlinux.org/packages/?name=tcpdump)

*   **[tcptrace](https://en.wikipedia.org/wiki/tcptrace "wikipedia:tcptrace")** — TCP dump file analysis tool.

	[http://tcptrace.org/](http://tcptrace.org/) || [tcptrace](https://www.archlinux.org/packages/?name=tcptrace)

*   **[vnStat](/index.php/VnStat "VnStat")** — Console-based network traffic monitor that keeps a log of network traffic for the selected interfaces.

	[https://humdi.net/vnstat/](https://humdi.net/vnstat/) || [vnstat](https://www.archlinux.org/packages/?name=vnstat)

*   **wifiphisher** — Fast automated phishing attacks against WPA networks.

	[https://github.com/wifiphisher/wifiphisher](https://github.com/wifiphisher/wifiphisher) || [wifiphisher](https://aur.archlinux.org/packages/wifiphisher/)

*   **[Wireshark](/index.php/Wireshark "Wireshark")** — Network protocol analyzer that lets you capture and interactively browse the traffic running on a computer network.

	[https://www.wireshark.org/](https://www.wireshark.org/) || CLI: [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli), GUI: [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt)

*   **[Xplico](https://en.wikipedia.org/wiki/Xplico "wikipedia:Xplico")** — Network forensics analysis tool (NFAT), which is a software that reconstructs the contents of acquisitions performed with a packet sniffer.

	[https://www.xplico.org/](https://www.xplico.org/) || [xplico](https://aur.archlinux.org/packages/xplico/)

#### Firewall management

See [iptables#Front-ends](/index.php/Iptables#Front-ends "Iptables").

#### Threat and vulnerability detection

*   **AFICK** — Security tool that allows to monitor the changes on your files systems, and so can detect intrusions.

	[http://afick.sourceforge.net/](http://afick.sourceforge.net/) || [afick](https://aur.archlinux.org/packages/afick/)

*   **[Lynis](https://en.wikipedia.org/wiki/Lynis "wikipedia:Lynis")** — Security and system auditing tool to harden Unix/Linux systems.

	[https://cisofy.com/lynis/](https://cisofy.com/lynis/) || [lynis](https://www.archlinux.org/packages/?name=lynis)

*   **[Metasploit Framework](/index.php/Metasploit_Framework "Metasploit Framework")** — An advanced open-source platform for developing, testing, and using exploit code.

	[https://www.metasploit.com/](https://www.metasploit.com/) || [metasploit](https://www.archlinux.org/packages/?name=metasploit)

*   **[Nessus](/index.php/Nessus "Nessus")** — Comprehensive vulnerability scanning program.

	[https://www.tenable.com/products/nessus](https://www.tenable.com/products/nessus) || [nessus](https://aur.archlinux.org/packages/nessus/)

*   **[OpenVAS](/index.php/OpenVAS "OpenVAS")** — Framework of several services and tools offering a comprehensive and powerful vulnerability scanning and vulnerability management solution. FOSS Nessus fork.

	[http://www.openvas.org/](http://www.openvas.org/) || [openvas](https://www.archlinux.org/packages/?name=openvas)

*   **OSSEC** — Open Source Host-based Intrusion Detection System that performs log analysis, file integrity checking, policy monitoring, rootkit detection, real-time alerting and active response.

	[https://ossec.github.io/](https://ossec.github.io/) || [ossec-agent](https://aur.archlinux.org/packages/ossec-agent/) [ossec-local](https://aur.archlinux.org/packages/ossec-local/) [ossec-server](https://aur.archlinux.org/packages/ossec-server/)

*   **Samhain** — Host-based intrusion detection system (HIDS) provides file integrity checking and log file monitoring/analysis, as well as rootkit detection, port monitoring, detection of rogue SUID executables, and hidden processes.

	[https://www.la-samhna.de/samhain/index.html](https://www.la-samhna.de/samhain/index.html) || [samhain](https://aur.archlinux.org/packages/samhain/)

*   **[Tiger](https://en.wikipedia.org/wiki/Tiger_(security_software) "wikipedia:Tiger (security software)")** — Security tool that can be use both as a security audit and intrusion detection system.

	[http://www.nongnu.org/tiger/](http://www.nongnu.org/tiger/) || [tiger](https://aur.archlinux.org/packages/tiger/)

*   **[Tripwire](https://en.wikipedia.org/wiki/Open_Source_Tripwire "wikipedia:Open Source Tripwire")** — Intrusion detection system.

	[https://github.com/Tripwire/tripwire-open-source](https://github.com/Tripwire/tripwire-open-source) || [tripwire-git](https://aur.archlinux.org/packages/tripwire-git/)

#### File security

*   **[AIDE](/index.php/AIDE "AIDE")** — File and directory integrity checker.

	[https://aide.github.io](https://aide.github.io) || [aide](https://www.archlinux.org/packages/?name=aide)

*   **Logcheck** — Simple utility which is designed to allow a system administrator to view the logfiles which are produced upon hosts under their control.

	[https://logcheck.alioth.debian.org/](https://logcheck.alioth.debian.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Logwatch](/index.php/Logwatch "Logwatch")** — Customizable log analysis system.

	[https://sourceforge.net/projects/logwatch/](https://sourceforge.net/projects/logwatch/) || [logwatch](https://www.archlinux.org/packages/?name=logwatch)

*   **OpenDLP** — OpenDLP is a free and open source, agent- and agentless-based, centrally-managed, massively distributable data loss prevention tool.

	[https://code.google.com/archive/p/opendlp/](https://code.google.com/archive/p/opendlp/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

#### Anti malware

*   **[ClamAV](/index.php/ClamAV "ClamAV")** — Open source antivirus engine for detecting trojans, viruses, malware & other malicious threats.

	[http://www.clamav.net/](http://www.clamav.net/) || [clamav](https://www.archlinux.org/packages/?name=clamav)

*   **ClamTk** — Graphical front-end for ClamAV using Perl and Gtk libraries. It is designed to be an easy-to-use, lightweight, on-demand antivirus scanner for Linux systems.

	[https://dave-theunsub.github.io/clamtk/](https://dave-theunsub.github.io/clamtk/) || [clamtk](https://www.archlinux.org/packages/?name=clamtk), Nautilus plugin: [clamtk-gnome](https://aur.archlinux.org/packages/clamtk-gnome/), MATE plugin: [clamtk-mate](https://aur.archlinux.org/packages/clamtk-mate/), Thunar plugin: [thunar-sendto-clamtk](https://aur.archlinux.org/packages/thunar-sendto-clamtk/)

*   **Linux Malware Detect** — Malware scanner designed around the threats faced in shared hosted environments.

	[https://www.rfxn.com/projects/linux-malware-detect/](https://www.rfxn.com/projects/linux-malware-detect/) || [maldet](https://aur.archlinux.org/packages/maldet/)

*   **Rootkit Hunter** — Checks machines for the presence of rootkits and other unwanted tools.

	[http://rkhunter.sourceforge.net/](http://rkhunter.sourceforge.net/) || [rkhunter](https://www.archlinux.org/packages/?name=rkhunter)

*   **Hostsblock** — A script that downloads, sorts, and compiles multiple ad- and malware-blocking hosts files.

	[http://gaenserich.github.io/hostsblock/](http://gaenserich.github.io/hostsblock/) || [hostsblock](https://aur.archlinux.org/packages/hostsblock/)

#### Backup programs

See also [Synchronization and backup programs#Incremental backups](/index.php/Synchronization_and_backup_programs#Incremental_backups "Synchronization and backup programs") and [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software").

*   **Déjà Dup** — Simple GTK backup program. It hides the complexity of doing backups the 'right way' (encrypted, off-site, and regular) and uses [duplicity](/index.php/Duplicity "Duplicity") as the backend.

	[https://launchpad.net/deja-dup](https://launchpad.net/deja-dup) || [deja-dup](https://www.archlinux.org/packages/?name=deja-dup)

*   **[Duplicati](https://en.wikipedia.org/wiki/Duplicati "wikipedia:Duplicati")** — Backup client that securely stores encrypted, incremental, compressed backups on cloud storage services and remote file servers.

	[https://www.duplicati.com/](https://www.duplicati.com/) || [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/)

*   **[duplicity](/index.php/Duplicity "Duplicity")** — Simple command-line utility which allows encrypted compressed incremental backup to nearly any storage.

	[http://www.nongnu.org/duplicity/](http://www.nongnu.org/duplicity/) || [duplicity](https://www.archlinux.org/packages/?name=duplicity)

*   **[Duply](/index.php/Duply "Duply")** — Command-line front-end for [duplicity](/index.php/Duplicity "Duplicity") which simplifies running it. It manages backup job settings in profiles and allows to batch execute commands.

	[http://www.duply.net/](http://www.duply.net/) || [duply](https://aur.archlinux.org/packages/duply/)

*   **restic** — Fast, secure, efficient backup program that supports backing up to many cloud services.

	[https://restic.net/](https://restic.net/) || [restic](https://www.archlinux.org/packages/?name=restic)

*   **[Tarsnap](https://en.wikipedia.org/wiki/Tarsnap "wikipedia:Tarsnap")** — Secure, efficient proprietary online backup service.

	[http://www.tarsnap.com/](http://www.tarsnap.com/) || [tarsnap](https://www.archlinux.org/packages/?name=tarsnap)

#### Screen lockers

See also [Session lock](/index.php/Session_lock "Session lock").

**Warning:** Only *sflock*, *physlock*, *Cinnamon Screensaver*, *MATE Screensaver* and *GNOME Screensaver* are able to block tty access. See [Xorg#Block TTY access](/index.php/Xorg#Block_TTY_access "Xorg") on how to manually block tty access.

*   **Cinnamon Screensaver** — Screen locker for the Cinnamon desktop.

	[https://github.com/linuxmint/cinnamon-screensaver](https://github.com/linuxmint/cinnamon-screensaver) || [cinnamon-screensaver](https://www.archlinux.org/packages/?name=cinnamon-screensaver)

*   **Deepin Screensaver** — A lightweight Qt5 based screensaver.

	[https://github.com/linuxdeepin/deepin-screensaver](https://github.com/linuxdeepin/deepin-screensaver) || [deepin-screensaver](https://www.archlinux.org/packages/?name=deepin-screensaver)

*   **GNOME Screensaver** — Screen locker for the GNOME Flashback desktop.

	[https://wiki.gnome.org/Projects/GnomeScreensaver](https://wiki.gnome.org/Projects/GnomeScreensaver) || [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver)

*   **i3lock** — A simple screen locker. Provides user feedback, uses PAM authentication, supports DPMS. The background can be set to an image or solid color.

	[https://i3wm.org/i3lock/](https://i3wm.org/i3lock/) || [i3lock](https://www.archlinux.org/packages/?name=i3lock)

*   **i3lock-blur** — Fork of *i3lock* which can use your desktop with the blur effect applied as a background.

	[https://github.com/karulont/i3lock-blur](https://github.com/karulont/i3lock-blur) || [i3lock-blur](https://aur.archlinux.org/packages/i3lock-blur/)

*   **i3lock-color** — Fork of *i3lock* with color and positioning configuration support and can use your desktop with the blur effect applied as a background.

	[https://github.com/PandorasFox/i3lock-color](https://github.com/PandorasFox/i3lock-color) || [i3lock-color](https://www.archlinux.org/packages/?name=i3lock-color)

*   **i3lock-wrapper** — A simple wrapper around *i3lock* which sets up a blurred screenshot of the desktop as a background image.

	[https://github.com/ashinkarov/i3-extras](https://github.com/ashinkarov/i3-extras) || [i3lock-wrapper](https://aur.archlinux.org/packages/i3lock-wrapper/)

*   **Light-locker** — A simple locker (forked from *gnome-screensaver*) that aims to have simple, sane, secure defaults and be well integrated with the desktop while not carrying any desktop-specific dependencies. It relies on [LightDM](/index.php/LightDM "LightDM") for locking and unlocking your session via ConsoleKit/UPower or *logind/systemd*.

	[https://github.com/the-cavalry/light-locker](https://github.com/the-cavalry/light-locker) || [light-locker](https://www.archlinux.org/packages/?name=light-locker)

*   **MATE Screensaver** — Screensaver and locker for MATE Desktop Environment.

	[https://github.com/mate-desktop/mate-screensaver](https://github.com/mate-desktop/mate-screensaver) || [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver)

*   **physlock** — Screen and console locker.

	[https://github.com/muennich/physlock](https://github.com/muennich/physlock) || [physlock](https://www.archlinux.org/packages/?name=physlock)

*   **sflock** — Simple screen locker utility for X, based on slock. Provides a very basic user feedback.

	[https://github.com/benruijl/sflock](https://github.com/benruijl/sflock) || [sflock-git](https://aur.archlinux.org/packages/sflock-git/)

*   **[slock](/index.php/Slock "Slock")** — Very simple and lightweight X screen locker. Offers only a black background when locked, there are no animations or text fields.

	[https://tools.suckless.org/slock/](https://tools.suckless.org/slock/) || [slock](https://www.archlinux.org/packages/?name=slock)

*   **sxlock** — Fork of sflock with a few enhancements. Provides basic user feedback, uses PAM authentication, supports DPMS and RandR. Supports `sxlock.service` to lock the screen on suspend/hibernation. See the [README](https://github.com/lahwaacz/sxlock/blob/master/README.md) for more information.

	[https://github.com/lahwaacz/sxlock](https://github.com/lahwaacz/sxlock) || [sxlock-git](https://aur.archlinux.org/packages/sxlock-git/)

*   **tsscreenlock** — Screen locker used in theShell. Shows music controls, and if used with theShell, also shows desktop notifications.

	[https://github.com/vicr123/tsscreenlock](https://github.com/vicr123/tsscreenlock) || [tsscreenlock](https://aur.archlinux.org/packages/tsscreenlock/)

*   **vlock** — TTY locker. A mirror of the [original vlock](https://lists.archlinux.org/pipermail/aur-general/2013-July/024662.html) is available at [github](https://github.com/WorMzy/vlock).

	[http://kbd-project.org/](http://kbd-project.org/) || [kbd](https://www.archlinux.org/packages/?name=kbd)

*   **xfce4-screensaver** — A screen saver and locker that aims to have simple, sane, secure defaults and be well integrated with the xfce desktop.

	[https://git.xfce.org/apps/xfce4-screensaver/about/](https://git.xfce.org/apps/xfce4-screensaver/about/) || [xfce4-screensaver](https://www.archlinux.org/packages/?name=xfce4-screensaver)

*   **xlockmore** — Simple X11 screen lock with PAM support.

	[http://sillycycle.com/xlockmore.html](http://sillycycle.com/xlockmore.html) || [xlockmore](https://www.archlinux.org/packages/?name=xlockmore)

*   **[XScreenSaver](/index.php/XScreenSaver "XScreenSaver")** — Screen saver and locker for the X Window System.

	[https://www.jwz.org/xscreensaver/](https://www.jwz.org/xscreensaver/) || [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)

*   **XSecureLock** — X11 screen lock utility designed with the primary goal of security.

	[https://github.com/google/xsecurelock](https://github.com/google/xsecurelock) || [xsecurelock](https://www.archlinux.org/packages/?name=xsecurelock)

*   **xtrlock** — Very lightweight X display locker. Keeps windows visible and displays lock icon instead of mouse cursor. Typing password followed by enter unlocks the screen.

	[https://packages.debian.org/sid/xtrlock](https://packages.debian.org/sid/xtrlock) || [xtrlock](https://www.archlinux.org/packages/?name=xtrlock)

#### Password auditing

*   **[John](https://en.wikipedia.org/wiki/John "wikipedia:John")** — John the Ripper password cracker.

	[https://www.openwall.com/john](https://www.openwall.com/john) || [john](https://www.archlinux.org/packages/?name=john)

*   **[Hashcat](/index.php/Hashcat "Hashcat")** — Multithreaded advanced password recovery utility.

	[https://hashcat.net/hashcat](https://hashcat.net/hashcat) || [hashcat](https://www.archlinux.org/packages/?name=hashcat)

#### Password managers

##### Console

*   **gopass** — Advanced console based password manager, supporting GnuPG and other backends.

	[https://github.com/justwatchcom/gopass](https://github.com/justwatchcom/gopass) || [gopass](https://www.archlinux.org/packages/?name=gopass)

*   **KeePassC** — Curses-based password manager compatible to KeePass v.1.x.

	[https://outerhaven.de/keepassc/](https://outerhaven.de/keepassc/) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **LastPass** — Hosted password manager.

	[https://www.lastpass.com/](https://www.lastpass.com/) || [lastpass-cli](https://www.archlinux.org/packages/?name=lastpass-cli)

*   **[pass](/index.php/Pass "Pass")** — Simple console based password manager, using GnuPG encryption.

	[https://www.passwordstore.org/](https://www.passwordstore.org/) || [pass](https://www.archlinux.org/packages/?name=pass)

*   **pwsafe** — Unix command-line program that manages encrypted password databases.

	[http://nsd.dyndns.org/pwsafe/](http://nsd.dyndns.org/pwsafe/) || [pwsafe](https://aur.archlinux.org/packages/pwsafe/)

*   **spm** — Simple Password Manager written entirely in POSIX shell using PGP. Fast, lightweight and easily scriptable.

	[https://notabug.org/kl3/spm/](https://notabug.org/kl3/spm/) || [spm](https://aur.archlinux.org/packages/spm/)

*   **tpm** — tiny password manager, inspired by pass, written entirely in POSIX shell.

	[https://github.com/nmeum/tpm](https://github.com/nmeum/tpm) || [tpm](https://aur.archlinux.org/packages/tpm/)

*   **Ylva** — Command-line password manager, written in C, uses OpenSSL.

	[https://www.ylvapasswordmanager.com/](https://www.ylvapasswordmanager.com/) || [ylva](https://aur.archlinux.org/packages/ylva/)

##### Graphical

*   **Bitwarden** — Open source password manager with desktop, mobile, browser, and CLI versions. Cloud or self-hosted.

	[https://bitwarden.com/](https://bitwarden.com/) || [bitwarden-bin](https://aur.archlinux.org/packages/bitwarden-bin/), [bitwarden-cli](https://aur.archlinux.org/packages/bitwarden-cli/)

*   **Encryptr** — Zero-knowledge, cloud-based password manager.

	[https://spideroak.com/encryptr/](https://spideroak.com/encryptr/) || [encryptr](https://aur.archlinux.org/packages/encryptr/)

*   **Enpass** — A multiplatform password manager

	[https://www.enpass.io/](https://www.enpass.io/) || [enpass-bin](https://aur.archlinux.org/packages/enpass-bin/)

*   **Figaro's Password Manager 2** — GTK2 port of [Figaro's Password Manager](http://fpm.sourceforge.net/) with some new enhancements.

	[https://als.regnet.cz/fpm2/](https://als.regnet.cz/fpm2/) || [fpm2](https://aur.archlinux.org/packages/fpm2/)

*   **GNOME Password Safe** — Password manager for GNOME which makes use of the KeePass v.4 format.

	[https://gitlab.gnome.org/World/PasswordSafe](https://gitlab.gnome.org/World/PasswordSafe) || [gnome-passwordsafe](https://www.archlinux.org/packages/?name=gnome-passwordsafe)

*   **Ked Password Manager** — A password manager that helps to manage large numbers of passwords.

	[http://kedpm.sourceforge.net](http://kedpm.sourceforge.net) || [kedpm](https://aur.archlinux.org/packages/kedpm/)

*   **[KeePass Password Safe](/index.php/KeePass "KeePass")** — Mono-based password manager, which helps you to manage your passwords in a secure way.

	[https://keepass.info/](https://keepass.info/) || [keepass](https://www.archlinux.org/packages/?name=keepass)

*   **KeePassX** — Qt-based password manager. Compatible with KeePass v.1.x and KeePass v.2.x.

	[https://www.keepassx.org/](https://www.keepassx.org/) || version 1: [keepassx](https://aur.archlinux.org/packages/keepassx/), version 2: [keepassx2](https://aur.archlinux.org/packages/keepassx2/)

*   **KeePassXC** — Community fork of KeePassX with more active development. Compatible with KeePass v.1.x (import only) and KeePass v.2.x.

	[https://keepassxc.org/](https://keepassxc.org/) || [keepassxc](https://www.archlinux.org/packages/?name=keepassxc)

*   **[KDE Wallet Manager](/index.php/KDE_Wallet "KDE Wallet")** — Tool to manage the passwords on your system. By using the KDE wallet subsystem it not only allows you to keep your own secrets but also to access and manage the passwords of every application that integrates with the wallet.

	[https://www.kde.org/applications/system/kwalletmanager/](https://www.kde.org/applications/system/kwalletmanager/) || [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager)

*   **OTPClient** — Highly secure and easy to use GTK software for two-factor authentication that supports both Time-based One-time Passwords (TOTP) and HMAC-Based One-Time Passwords (HOTP).

	[https://github.com/paolostivanin/OTPClient](https://github.com/paolostivanin/OTPClient) || [otpclient](https://aur.archlinux.org/packages/otpclient/)

*   **Passbook** — Modern password manager for GNOME.

	[https://wiki.gnome.org/Apps/Passbook](https://wiki.gnome.org/Apps/Passbook) || [passbook](https://aur.archlinux.org/packages/passbook/)

*   **Password Gorilla** — A cross-platform password manager.

	[https://github.com/zdia/gorilla/wiki](https://github.com/zdia/gorilla/wiki) || [password-gorilla](https://aur.archlinux.org/packages/password-gorilla/)

*   **Password Safe** — Simple and secure password manager.

	[https://pwsafe.org/](https://pwsafe.org/) || [passwordsafe](https://aur.archlinux.org/packages/passwordsafe/)

*   **QPass** — Easy to use password manager with built-in password generator.

	[http://qpass.sourceforge.net/](http://qpass.sourceforge.net/) || [qpass](https://aur.archlinux.org/packages/qpass/)

*   **QtPass** — GUI for pass, the standard unix password manager.

	[https://qtpass.org/](https://qtpass.org/) || [qtpass](https://www.archlinux.org/packages/?name=qtpass)

*   **Revelation** — Password manager for the GNOME desktop.

	[https://revelation.olasagasti.info/](https://revelation.olasagasti.info/) || [revelation](https://aur.archlinux.org/packages/revelation/)

*   **[Seahorse](https://en.wikipedia.org/wiki/Seahorse_(software) "wikipedia:Seahorse (software)")** — GNOME application for managing encryption keys and passwords in the GNOME Keyring.

	[https://wiki.gnome.org/Apps/Seahorse](https://wiki.gnome.org/Apps/Seahorse) || [seahorse](https://www.archlinux.org/packages/?name=seahorse)

*   **Universal Password Manager** — Allows you to store usernames, passwords, URLs and generic notes in an encrypted database protected by one master password.

	[http://upm.sourceforge.net/](http://upm.sourceforge.net/) || [upm](https://aur.archlinux.org/packages/upm/)

#### Cryptography

##### Hash checkers

*   **cfv** — Tiny utility to both test and create checksum files, support `.sfv`, `.csv`, `.crc`, `.md5`, `md5sum`, `sha1sum`, `.torrent`, `par`, and `.par2` files.

	[http://cfv.sourceforge.net/](http://cfv.sourceforge.net/) || [cfv](https://aur.archlinux.org/packages/cfv/)

*   **GtkHash** — A GTK utility for computing message digests or checksums

	[https://github.com/tristanheaven/gtkhash](https://github.com/tristanheaven/gtkhash) || [gtkhash](https://aur.archlinux.org/packages/gtkhash/)

*   **hashdeep** — A cross-platform tools to computer hashes, or message digests, for any number of files

	[http://md5deep.sourceforge.net/](http://md5deep.sourceforge.net/) || [hashdeep](https://www.archlinux.org/packages/?name=hashdeep)

*   **Parano** — A GNOME frontend for creating/editing/checking MD5 and SFV files

	[https://sourceforge.net/projects/parano.berlios/](https://sourceforge.net/projects/parano.berlios/) || [parano](https://aur.archlinux.org/packages/parano/)

*   **Quick Hash GUI** — A GUI to enable the rapid selection and subsequent hashing of files (individually or recursively throughout a folder structure) text and (on Linux) disks.

	[https://www.quickhash-gui.org/](https://www.quickhash-gui.org/) || [quickhash-gui-bin](https://aur.archlinux.org/packages/quickhash-gui-bin/)

*   **RHash** — Utility for verifying hash sums (SFV, CRC, etc). Supports lots of algorithms.

	[https://github.com/rhash/RHash/](https://github.com/rhash/RHash/) || [rhash](https://www.archlinux.org/packages/?name=rhash)

*   **MassHash** — A set of file hashing tools (both CLI and GTK GUI) written in Python. Supported algorithms include MD5, SHA-1, SHA-224, SHA-256, SHA-384, SHA-512.

	[http://jdleicher.github.io/MassHash/](http://jdleicher.github.io/MassHash/) || [masshash](https://aur.archlinux.org/packages/masshash/)

*   **Parchive** — Utility which creates and uses PAR2 files to detect damage in data files and repair them if necessary.

	[https://github.com/Parchive/par2cmdline](https://github.com/Parchive/par2cmdline) || [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline)

##### Encryption, signing, steganography

*   **ccrypt** — A command-line utility for encrypting and decrypting files and streams.

	[http://ccrypt.sourceforge.net/](http://ccrypt.sourceforge.net/) || [ccrypt](https://aur.archlinux.org/packages/ccrypt/)

*   **[Enigmail](https://en.wikipedia.org/wiki/Enigmail "wikipedia:Enigmail")** — A security extension to Mozilla Thunderbird and Seamonkey. It enables you to write and receive email messages signed and/or encrypted with the OpenPGP standard.

	[https://enigmail.net](https://enigmail.net) || [thunderbird-extension-enigmail](https://www.archlinux.org/packages/?name=thunderbird-extension-enigmail)

*   **GNOME Keysign** — GTK/GNOME application to use GnuPG for signing other people's keys. Quickly, easily, and securely.

	[https://wiki.gnome.org/Apps/Keysign](https://wiki.gnome.org/Apps/Keysign) || [gnome-keysign](https://aur.archlinux.org/packages/gnome-keysign/)

*   **[GnuPG](/index.php/GnuPG "GnuPG")** — The GNU project's complete and free implementation of the OpenPGP standard as defined by RFC4880\. Free and Open Source replacement of PGP, mostly used for digital signing of packages.

	[https://gnupg.org/](https://gnupg.org/) || [gnupg](https://www.archlinux.org/packages/?name=gnupg)

*   **GPG-Crypter** — Graphical front-end to GnuPG(GPG) using the GTK3 toolkit and GPGME library.

	[https://sourceforge.net/projects/gpg-crypter/](https://sourceforge.net/projects/gpg-crypter/) || [gpg-crypter](https://www.archlinux.org/packages/?name=gpg-crypter)

*   **gzsteg** — Utility that can hide data in gzip compressed files

	[http://www.nic.funet.fi/pub/crypt/steganography/](http://www.nic.funet.fi/pub/crypt/steganography/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Keybase](/index.php/Keybase "Keybase")** — Key directory mapping social media identities, with cross platform encrypted chat, cloud storage, and git repositories.

	[https://keybase.io/](https://keybase.io/) || [keybase](https://www.archlinux.org/packages/?name=keybase)

*   **[KGpg](https://en.wikipedia.org/wiki/KGPG "wikipedia:KGPG")** — Simple interface for GnuPG, for KDE.

	[https://www.kde.org/applications/utilities/kgpg/](https://www.kde.org/applications/utilities/kgpg/) || [kgpg](https://www.archlinux.org/packages/?name=kgpg)

*   **Kleopatra** — Certificate Manager and Unified Crypto GUI for KDE. It supports managing X.509 and OpenPGP certificates in the GpgSM keybox and retrieving certificates from LDAP servers.

	[https://www.kde.org/applications/utilities/kleopatra/](https://www.kde.org/applications/utilities/kleopatra/) || [kleopatra](https://www.archlinux.org/packages/?name=kleopatra)

*   **minisign** — Simple program that only inplements key signing

	[https://github.com/jedisct1/minisign](https://github.com/jedisct1/minisign) || [minisign](https://www.archlinux.org/packages/?name=minisign)

*   **[Seahorse](https://en.wikipedia.org/wiki/Seahorse_(software) "wikipedia:Seahorse (software)")** — GNOME application for managing encryption keys and passwords in the GNOME Keyring.

	[https://wiki.gnome.org/Apps/Seahorse](https://wiki.gnome.org/Apps/Seahorse) || [seahorse](https://www.archlinux.org/packages/?name=seahorse)

*   **steghide** — A steganography utility that is able to hide data in various kinds of image and audio files.

	[http://steghide.sourceforge.net](http://steghide.sourceforge.net) || [steghide](https://www.archlinux.org/packages/?name=steghide)

##### Disk encryption

See [Disk encryption](/index.php/Disk_encryption "Disk encryption").

## Science

**Note:** For possibly more up to date selection of scientific applications, try checking the [AUR 'science' category](https://aur.archlinux.org/packages.php?O=0&do_Search=Go&detail=1&C=15&SeB=nd&SB=v&SO=d&PP=50)

### Mathematics

#### Calculator

See also [Wikipedia:Comparison of software calculators](https://en.wikipedia.org/wiki/Comparison_of_software_calculators "wikipedia:Comparison of software calculators").

*   **[bc](https://en.wikipedia.org/wiki/bc_programming_language "wikipedia:bc programming language")** — Arbitrary precision calculator language.

	[https://www.gnu.org/software/bc/](https://www.gnu.org/software/bc/) || [bc](https://www.archlinux.org/packages/?name=bc)

*   **calc** — Arbitrary precision console calculator.

	[http://www.isthe.com/chongo/tech/comp/calc/](http://www.isthe.com/chongo/tech/comp/calc/) || [calc](https://www.archlinux.org/packages/?name=calc)

*   **clac** — Command-line, stack-based calculator with postfix notation.

	[https://github.com/soveran/clac](https://github.com/soveran/clac) || [clac](https://aur.archlinux.org/packages/clac/)

*   **Deepin Calculator** — Easy to use calculator for Deepin desktop.

	[https://www.deepin.org/en/original/deepin-calculator/](https://www.deepin.org/en/original/deepin-calculator/) || [deepin-calculator](https://www.archlinux.org/packages/?name=deepin-calculator)

*   **Extcalc** — Qt-based scientific graphical calculator.

	[http://extcalc-linux.sourceforge.net/](http://extcalc-linux.sourceforge.net/) || [extcalc](https://aur.archlinux.org/packages/extcalc/)

*   **FOX Calculator** — Simple desktop calculator.

	[http://fox-toolkit.org/](http://fox-toolkit.org/) || [fox](https://www.archlinux.org/packages/?name=fox)

*   **galculator** — GTK-based scientific calculator.

	[http://galculator.mnim.org/](http://galculator.mnim.org/) || GTK 3: [galculator](https://www.archlinux.org/packages/?name=galculator), GTK 2: [galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)

*   **[Genius](https://en.wikipedia.org/wiki/Genius_(mathematics_software) "wikipedia:Genius (mathematics software)")** — Advanced calculator including a mathematical programming language.

	[https://www.jirka.org/genius.html](https://www.jirka.org/genius.html) || [genius](https://www.archlinux.org/packages/?name=genius)

*   **[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")** — Scientific calculator included in the GNOME desktop.

	[https://wiki.gnome.org/Apps/Calculator](https://wiki.gnome.org/Apps/Calculator) || [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)

*   **[KAlgebra](https://en.wikipedia.org/wiki/KAlgebra "wikipedia:KAlgebra")** — Calculator and 3D plotter. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/kalgebra/](https://www.kde.org/applications/education/kalgebra/) || [kalgebra](https://www.archlinux.org/packages/?name=kalgebra)

*   **[KCalc](https://en.wikipedia.org/wiki/KCalc "wikipedia:KCalc")** — Scientific calculator included in the KDE desktop.

	[https://www.kde.org/applications/utilities/kcalc/](https://www.kde.org/applications/utilities/kcalc/) || [kcalc](https://www.archlinux.org/packages/?name=kcalc)

*   **Liri Calculator** — Calculator for Liri.

	[https://github.com/lirios/calculator](https://github.com/lirios/calculator) || [liri-calculator](https://www.archlinux.org/packages/?name=liri-calculator)

*   **MATE Calc** — Calculator for the MATE desktop environment.

	[https://mate-desktop.org/](https://mate-desktop.org/) || [mate-calc](https://www.archlinux.org/packages/?name=mate-calc)

*   **Qalculate!** — Calculator and equation solver with fault-tolerant parsing, constant recognition and units.

	[https://qalculate.github.io/](https://qalculate.github.io/) || [qalculate-gtk](https://www.archlinux.org/packages/?name=qalculate-gtk)

*   **SpeedCrunch** — Fast, high precision and powerful cross-platform calculator.

	[http://speedcrunch.org](http://speedcrunch.org) || [speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch)

*   **[xcalc](https://en.wikipedia.org/wiki/xcalc "wikipedia:xcalc")** — Scientific calculator for X with algebraic and reverse polish notation modes.

	[https://www.x.org/](https://www.x.org/) || [xorg-xcalc](https://www.archlinux.org/packages/?name=xorg-xcalc)

#### Computer algebra system

See also [Wikipedia:Comparison of computer algebra systems](https://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems "wikipedia:Comparison of computer algebra systems").

*   **[AXIOM](https://en.wikipedia.org/wiki/Axiom_(computer_algebra_system) "wikipedia:Axiom (computer algebra system)")** — FriCAS: derivative of the powerful AXIOM-CAS

	[http://fricas.sourceforge.net](http://fricas.sourceforge.net) || [fricas](https://aur.archlinux.org/packages/fricas/)

*   **[GAP](https://en.wikipedia.org/wiki/GAP_(computer_algebra_system) "wikipedia:GAP (computer algebra system)")** — Computer algebra system for computational discrete algebra with particular emphasis on computational group theory.

	[http://www.gap-system.org](http://www.gap-system.org) || [gap](https://www.archlinux.org/packages/?name=gap)

*   **[Maple](/index.php/Maple "Maple")** — Famous commercial CAS. Often used in education.

	[https://www.maplesoft.com/products/maple/](https://www.maplesoft.com/products/maple/) ||

*   **Mathics** — A free CAS for symbolic mathematical computations which uses [Python](/index.php/Python "Python") as its main language. It aims at achieving a Mathematica-compatible syntax and functions. It relies mostly on Sympy for most mathematical tasks and, optionally, Sage for more advanced functionality.

	[http://www.mathics.org/](http://www.mathics.org/) || [mathics](https://aur.archlinux.org/packages/mathics/)

*   **[Mathomatic](https://en.wikipedia.org/wiki/Mathomatic "wikipedia:Mathomatic")** — General purpose Computer Algebra System written in C.

	[http://www.mathomatic.org/](http://www.mathomatic.org/) || [mathomatic](https://www.archlinux.org/packages/?name=mathomatic)

*   **[Maxima](https://en.wikipedia.org/wiki/Maxima_(software) "wikipedia:Maxima (software)")** — [Maple](https://en.wikipedia.org/wiki/Maple_(software) "wikipedia:Maple (software)")/[Mathematica](https://en.wikipedia.org/wiki/Wolfram_Mathematica "wikipedia:Wolfram Mathematica")-like computer algebra system.

	[http://maxima.sourceforge.net/](http://maxima.sourceforge.net/) || [maxima](https://www.archlinux.org/packages/?name=maxima)

*   **[PARI/GP](https://en.wikipedia.org/wiki/PARI/GP "wikipedia:PARI/GP")** — Computer algebra system designed for fast computations in number theory.

	[http://pari.math.u-bordeaux.fr/](http://pari.math.u-bordeaux.fr/) || [pari](https://www.archlinux.org/packages/?name=pari)

*   **[Singular](https://en.wikipedia.org/wiki/Singular_(software) "wikipedia:Singular (software)")** — Computer algebra system for polynomial computations, with special emphasis on commutative and non-commutative algebra, algebraic geometry, and singularity theory.

	[https://www.singular.uni-kl.de/](https://www.singular.uni-kl.de/) || [singular](https://www.archlinux.org/packages/?name=singular)

*   **wxMaxima** — Graphical user interface for Maxima being a powerful computer algebra system.

	[https://andrejv.github.io/wxmaxima/](https://andrejv.github.io/wxmaxima/) || [wxmaxima](https://www.archlinux.org/packages/?name=wxmaxima)

*   **[Xcas](https://en.wikipedia.org/wiki/Xcas "wikipedia:Xcas")** — User interface to Giac, a free, basic computer algebra system.

	[http://www-fourier.ujf-grenoble.fr/~parisse/giac.html](http://www-fourier.ujf-grenoble.fr/~parisse/giac.html) || [xcas](https://www.archlinux.org/packages/?name=xcas)

#### Scientific or technical computing

See also [Wikipedia:Comparison of numerical analysis software](https://en.wikipedia.org/wiki/Comparison_of_numerical_analysis_software "wikipedia:Comparison of numerical analysis software").

*   **[Cantor](https://en.wikipedia.org/wiki/Cantor_(software) "wikipedia:Cantor (software)")** — Application that lets you use your favorite mathematical applications from within a nice KDE-integrated Worksheet Interface. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/cantor/](https://www.kde.org/applications/education/cantor/) || [cantor](https://www.archlinux.org/packages/?name=cantor)

*   **EngLab** — Cross-compile mathematical platform with a C like syntax.

	[http://englab.bugfest.net](http://englab.bugfest.net) || [englab](https://aur.archlinux.org/packages/englab/)

*   **[FFTW](https://en.wikipedia.org/wiki/FFTW "wikipedia:FFTW")** — A [Fast Fourier Transform](https://en.wikipedia.org/wiki/Fast_Fourier_transform "wikipedia:Fast Fourier transform") library for computing discrete Fourier transforms. Used for a wide variety of numerical applications, which includes spectral methods.

	[https://www.fftw.org/](https://www.fftw.org/) || [fftw](https://www.archlinux.org/packages/?name=fftw) [fftw-mpi](https://aur.archlinux.org/packages/fftw-mpi/) [fftw-mpich](https://aur.archlinux.org/packages/fftw-mpich/)

*   **[FreeMat](https://en.wikipedia.org/wiki/FreeMat "wikipedia:FreeMat")** — Matlab-like program that supports many of its functions and features a codeless interface to external C, C++, and Fortran code, further parallel distributed algorithm development (via MPI), and 3D visualization capabilities.

	[http://freemat.sourceforge.net/](http://freemat.sourceforge.net/) || [freemat](https://aur.archlinux.org/packages/freemat/)

*   **[GeoGebra](https://en.wikipedia.org/wiki/GeoGebra "wikipedia:GeoGebra")** — Dynamic mathematics software with interactive graphics, algebra and spreadsheet

	[https://www.geogebra.org/](https://www.geogebra.org/) || [geogebra](https://www.archlinux.org/packages/?name=geogebra)

*   **[Julia](https://en.wikipedia.org/wiki/Julia_(programming_language) "wikipedia:Julia (programming language)")** — High-level, high-performance dynamic language for technical computing.

	[https://julialang.org/](https://julialang.org/) || [julia](https://www.archlinux.org/packages/?name=julia)

*   **[Kig](https://en.wikipedia.org/wiki/Kig_(software) "wikipedia:Kig (software)")** — Application for Interactive Geometry. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/kig/](https://www.kde.org/applications/education/kig/) || [kig](https://www.archlinux.org/packages/?name=kig)

*   **[matplotlib (PyLab)](https://en.wikipedia.org/wiki/matplotlib "wikipedia:matplotlib")** — Collection of Python modules (pyplot, numpy, etc.) used for scientific calculations.

	[https://www.scipy.org/](https://www.scipy.org/) || [python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib)

*   **[Octave](/index.php/Octave "Octave")** — [MATLAB](/index.php/MATLAB "MATLAB")-like language and interface for numerical computations.

	[https://www.gnu.org/software/octave/](https://www.gnu.org/software/octave/) || [octave](https://www.archlinux.org/packages/?name=octave)

*   **[SageMath](/index.php/SageMath "SageMath")** — Mathematics software system, that combines many existing open-source packages into a common Python interface. Alternative to Magma, Maple, Mathematica and Matlab.

	[http://www.sagemath.org](http://www.sagemath.org) || [sagemath](https://www.archlinux.org/packages/?name=sagemath)

*   **[Scilab](https://en.wikipedia.org/wiki/Scilab "wikipedia:Scilab")** — Matlab alternative used for numerical computations. Its syntax is not equivalent to that of Matlab, but it can be easily converted.

	[https://www.scilab.org/](https://www.scilab.org/) || [scilab](https://aur.archlinux.org/packages/scilab/), [scilab-bin](https://aur.archlinux.org/packages/scilab-bin/), [scilab-git](https://aur.archlinux.org/packages/scilab-git/)

#### Statistics

See also [Wikipedia:Comparison of statistical packages](https://en.wikipedia.org/wiki/Comparison_of_statistical_packages "wikipedia:Comparison of statistical packages").

*   **[JAGS](https://en.wikipedia.org/wiki/Just_another_Gibbs_sampler "wikipedia:Just another Gibbs sampler") (Just another Gibbs sampler)** — Cross-platform program for analysis of Bayesian hierarchical models using Markov Chain Monte Carlo (MCMC) simulation.

	[http://mcmc-jags.sourceforge.net/](http://mcmc-jags.sourceforge.net/) || [jags](https://aur.archlinux.org/packages/jags/)

*   **jamovi** — Statistics package, which is easy to use, and designed to be familiar to users of SPSS. Based on the [Electron](https://electronjs.org/) platform.

	[https://www.jamovi.org/](https://www.jamovi.org/) || [jamovi-git](https://aur.archlinux.org/packages/jamovi-git/)

*   **[Python Data Analysis Library (pandas)](https://en.wikipedia.org/wiki/Pandas_(software) "wikipedia:Pandas (software)")** — Providing high-performance, easy-to-use data structures and data analysis tools with Python programming language.

	[https://pandas.pydata.org/](https://pandas.pydata.org/) || [python-pandas](https://www.archlinux.org/packages/?name=python-pandas)

*   **[PSPP](https://en.wikipedia.org/wiki/PSPP "wikipedia:PSPP")** — Free SPSS implementation.

	[https://www.gnu.org/software/pspp/](https://www.gnu.org/software/pspp/) || [pspp](https://aur.archlinux.org/packages/pspp/)

*   **[R](/index.php/R "R")** — Software environment for statistical computing and graphics.

	[https://cran.r-project.org/](https://cran.r-project.org/) || [r](https://www.archlinux.org/packages/?name=r)

*   **[RKWard](https://en.wikipedia.org/wiki/RKWard "wikipedia:RKWard")** — Frontend for the statistical language R.

	[https://rkward.kde.org/](https://rkward.kde.org/) || [rkward](https://aur.archlinux.org/packages/rkward/)

*   **[RStudio](https://en.wikipedia.org/wiki/RStudio "wikipedia:RStudio")** — A powerful and productive IDE for R written in Qt.

	[https://www.rstudio.com/](https://www.rstudio.com/) || [rstudio-desktop-bin](https://aur.archlinux.org/packages/rstudio-desktop-bin/)

#### Data analysis and plotting

See also [Wikipedia:List of information graphics software](https://en.wikipedia.org/wiki/List_of_information_graphics_software "wikipedia:List of information graphics software").

*   **Engauge Digitizer** — Extracts data points from images of graphs.

	[https://markummitchell.github.io/engauge-digitizer/](https://markummitchell.github.io/engauge-digitizer/) || [engauge](https://aur.archlinux.org/packages/engauge/)

*   **[Fityk](https://en.wikipedia.org/wiki/Fityk "wikipedia:Fityk")** — Curve fitting and data analysis application, predominantly used to fit analytical, bell-shaped functions to experimental data.

	[http://fityk.nieto.pl/](http://fityk.nieto.pl/) || [fityk](https://aur.archlinux.org/packages/fityk/)

*   **[Gnuplot](https://en.wikipedia.org/wiki/gnuplot "wikipedia:gnuplot")** — Command-line program that can generate 2D and 3D plots of functions, data, and data fits.

	[http://www.gnuplot.info/](http://www.gnuplot.info/) || [gnuplot](https://www.archlinux.org/packages/?name=gnuplot)

*   **[Grace](https://en.wikipedia.org/wiki/Grace_(plotting_tool) "wikipedia:Grace (plotting tool)")** — WYSIWYG 2D graph plotting tool.

	[http://plasma-gate.weizmann.ac.il/Grace/](http://plasma-gate.weizmann.ac.il/Grace/) || [grace](https://aur.archlinux.org/packages/grace/) [qtgrace](https://aur.archlinux.org/packages/qtgrace/) [gracegtk](https://aur.archlinux.org/packages/gracegtk/)

*   **[KmPlot](https://en.wikipedia.org/wiki/KmPlot "wikipedia:KmPlot")** — Program to draw graphs, their integrals or derivatives. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/kmplot/](https://www.kde.org/applications/education/kmplot/) || [kmplot](https://www.archlinux.org/packages/?name=kmplot)

*   **[LabPlot](https://en.wikipedia.org/wiki/LabPlot "wikipedia:LabPlot")** — Free software data analysis and visualization application, similar to SciDAVis.

	[https://labplot.kde.org/](https://labplot.kde.org/) || [labplot](https://www.archlinux.org/packages/?name=labplot)

*   **[QtiPlot](https://en.wikipedia.org/wiki/QtiPlot or [SigmaPlot](https://en.wikipedia.org/wiki/SigmaPlot "wikipedia:SigmaPlot").

	[https://www.qtiplot.com/](https://www.qtiplot.com/) || [qtiplot-git](https://aur.archlinux.org/packages/qtiplot-git/)

*   **Rocs** — Graph Theory IDE for everybody interested in designing and analyzing graph algorithms (e.g., lecturers, students, researchers). Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/rocs/](https://www.kde.org/applications/education/rocs/) || [rocs](https://www.archlinux.org/packages/?name=rocs)

*   **[ROOT](https://en.wikipedia.org/wiki/ROOT "wikipedia:ROOT")** — Data analysis program and library (originally for particle physics) developed by CERN.

	[https://root.cern.ch/](https://root.cern.ch/) || [root](https://www.archlinux.org/packages/?name=root)

*   **[SciDAVis](https://en.wikipedia.org/wiki/SciDAVis "wikipedia:SciDAVis")** — Fork of QtiPlot with the goal of being better documented and more user friendly.

	[http://scidavis.sourceforge.net/](http://scidavis.sourceforge.net/) || [scidavis](https://aur.archlinux.org/packages/scidavis/)

See also [List of applications/Documents#Spreadsheets](/index.php/List_of_applications/Documents#Spreadsheets "List of applications/Documents")

#### Proof assistants

See also [Wikipedia:Proof assistant](https://en.wikipedia.org/wiki/Proof_assistant "wikipedia:Proof assistant").

*   **[Agda](https://en.wikipedia.org/wiki/Agda_(programming_language) "wikipedia:Agda (programming language)")** — Dependently typed functional programming language and proof assistant. It is an interactive system for writing and checking proofs.

	[http://wiki.portal.chalmers.se/agda/](http://wiki.portal.chalmers.se/agda/) || [agda](https://www.archlinux.org/packages/?name=agda)

*   **[Coq](https://en.wikipedia.org/wiki/Coq "wikipedia:Coq")** — Formal proof management system. It provides a formal language to write mathematical definitions, executable algorithms and theorems together with an environment for semi-interactive development of machine-checked proofs.

	[https://coq.inria.fr/](https://coq.inria.fr/) || CLI: [coq](https://www.archlinux.org/packages/?name=coq), GUI: [coqide](https://www.archlinux.org/packages/?name=coqide)

*   **[Isabelle](https://en.wikipedia.org/wiki/Isabelle_(proof_assistant) "wikipedia:Isabelle (proof assistant)")** — Generic proof assistant that allows mathematical formulas to be expressed in a formal language and provides tools for proving those formulas in a logical calculus.

	[https://www.cl.cam.ac.uk/research/hvg/Isabelle/](https://www.cl.cam.ac.uk/research/hvg/Isabelle/) || [isabelle](https://aur.archlinux.org/packages/isabelle/)

### Physics

#### Physics simulation

*   **[Code_Aster](https://en.wikipedia.org/wiki/Code_Aster "wikipedia:Code Aster")** — Software package for Civil and Structural Engineering finite element analysis and numeric simulation in structural mechanics.

	[https://www.code-aster.org/V2/spip.php?rubrique2](https://www.code-aster.org/V2/spip.php?rubrique2) || [aster](https://aur.archlinux.org/packages/aster/)

*   **[EPANET](https://en.wikipedia.org/wiki/EPANET "wikipedia:EPANET")** — EPANET performs extended period simulation of the water movement and quality behavior within pressurized pipe networks.

	[https://www.epa.gov/](https://www.epa.gov/) || [epanet2-git](https://aur.archlinux.org/packages/epanet2-git/)

*   **[Step](https://en.wikipedia.org/wiki/Step_(software) "wikipedia:Step (software)")** — Two-dimensional physics simulation engine. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/step/](https://www.kde.org/applications/education/step/) || [step](https://www.archlinux.org/packages/?name=step)

*   **[SWMM](https://en.wikipedia.org/wiki/SWMM "wikipedia:SWMM")** — Storm Water Management Model is a dynamic rainfall-runoff-subsurface runoff simulation model used for simulation of the surface/subsurface hydrology quantity and quality.

	[https://www.epa.gov/](https://www.epa.gov/) || [swmm5-git](https://aur.archlinux.org/packages/swmm5-git/)

#### Unit conversion

*   **ConvertAll** — Unit conversion application that allows one to combine units in any way (e.g. inches per decade), even if it does not make sense.

	[http://convertall.bellz.org/](http://convertall.bellz.org/) || [convertall](https://aur.archlinux.org/packages/convertall/)

*   **Gonvert** — Conversion utility that allows conversion between many units like CGS, Ancient, Imperial with many categories like length, mass, numbers, etc.

	[http://www.unihedron.com/projects/gonvert/](http://www.unihedron.com/projects/gonvert/) || [gonvert](https://aur.archlinux.org/packages/gonvert/)

*   **[Units](https://en.wikipedia.org/wiki/GNU_Units "wikipedia:GNU Units")** — Command-line unit converter and calculator that can handle multiplicative scale changes, nonlinear conversions such as Fahrenheit to Celsius or wire gauge and others.

	[https://www.gnu.org/software/units/](https://www.gnu.org/software/units/) || [units](https://www.archlinux.org/packages/?name=units)

### Chemistry

#### Molecules

##### Viewers

See also [Wikipedia:List of molecular graphics systems](https://en.wikipedia.org/wiki/List_of_molecular_graphics_systems "wikipedia:List of molecular graphics systems").

*   **[Avogadro](https://en.wikipedia.org/wiki/Avogadro_(software) "wikipedia:Avogadro (software)")** — Editor, viewer and simulator for 3D molecule structures (also supports downloading files from the [Protein Data Bank](https://en.wikipedia.org/wiki/Protein_Data_Bank "wikipedia:Protein Data Bank")).

	[http://avogadro.cc/](http://avogadro.cc/) || [avogadro](https://aur.archlinux.org/packages/avogadro/)

*   **BALLView** — Standalone molecular modeling and visualization application, part of the [BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") framework.

	[https://ball-project.org/](https://ball-project.org/) || [ball](https://aur.archlinux.org/packages/ball/)

*   **[Ghemical](https://en.wikipedia.org/wiki/Ghemical "wikipedia:Ghemical")** — Computational chemistry software package used to edit, view and simulate molecular structures.

	[http://bioinformatics.org/ghemical/ghemical/index.html](http://bioinformatics.org/ghemical/ghemical/index.html) || [ghemical](https://aur.archlinux.org/packages/ghemical/)

*   **[PyMOL](https://en.wikipedia.org/wiki/PyMOL "wikipedia:PyMOL")** — Open-source molecular visualization system that can produce high quality 3D images of small molecules and biological macromolecules, such as proteins.

	[https://pymol.org/](https://pymol.org/) || [pymol](https://www.archlinux.org/packages/?name=pymol)

*   **VMD** — VMD is a molecular visualization program for displaying, animating, and analyzing large biomolecular systems using 3-D graphics and built-in scripting.

	[http://www.ks.uiuc.edu/Research/vmd/](http://www.ks.uiuc.edu/Research/vmd/) || [vmd](https://aur.archlinux.org/packages/vmd/)

##### Drawing

*   **[BKChem](https://en.wikipedia.org/wiki/BKchem "wikipedia:BKchem")** — Practical and goodlooking skeletal formula molecule drawing program.

	[http://bkchem.zirael.org/](http://bkchem.zirael.org/) || [bkchem](https://aur.archlinux.org/packages/bkchem/)

*   **[Chemtool](https://en.wikipedia.org/wiki/Chemtool "wikipedia:Chemtool")** — GTK-based program for drawing chemical structural formulas.

	[http://ruby.chemie.uni-freiburg.de/~martin/chemtool/chemtool.html](http://ruby.chemie.uni-freiburg.de/~martin/chemtool/chemtool.html) || [chemtool](https://www.archlinux.org/packages/?name=chemtool)

*   **EasyChem** — Simple skeletal formula molecule drawing program with a focus on producing press-quality figures.

	[http://easychem.sourceforge.net/](http://easychem.sourceforge.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Gabedit](https://en.wikipedia.org/wiki/Gabedit "wikipedia:Gabedit")** — Graphical user interface to computational chemistry packages like [GAMESS](https://en.wikipedia.org/wiki/GAMESS_(US) "wikipedia:GAMESS (US)"), [Gaussian](https://en.wikipedia.org/wiki/Gaussian_(software) "wikipedia:Gaussian (software)"), [MOLCAS](https://en.wikipedia.org/wiki/MOLCAS "wikipedia:MOLCAS"), [MOLPRO](https://en.wikipedia.org/wiki/MOLPRO "wikipedia:MOLPRO"), [MPQC](https://en.wikipedia.org/wiki/MPQC "wikipedia:MPQC"), [OpenMopac](https://en.wikipedia.org/wiki/MOPAC "wikipedia:MOPAC"), [Firefly](https://en.wikipedia.org/wiki/PC_GAMESS "wikipedia:PC GAMESS") (previously PC GAMESS) and [Q-Chem](https://en.wikipedia.org/wiki/Q-Chem "wikipedia:Q-Chem").

	[http://gabedit.sourceforge.net/](http://gabedit.sourceforge.net/) || [gabedit](https://aur.archlinux.org/packages/gabedit/)

##### Modeling

*   **APBS** — Electrostatic and solvation properties for complex molecules.

	[http://www.poissonboltzmann.org/](http://www.poissonboltzmann.org/) || [apbs](https://aur.archlinux.org/packages/apbs/)

*   **CP2K** — A quantum chemistry and solid state physics software package.

	[https://www.cp2k.org/](https://www.cp2k.org/) || [cp2k](https://aur.archlinux.org/packages/cp2k/)

*   **Fpocket** — Fpocket is a very fast open source protein pocket detection algorithm based on Voronoi tessellation.

	[https://github.com/Discngine/fpocket](https://github.com/Discngine/fpocket) || [fpocket-git](https://aur.archlinux.org/packages/fpocket-git/)

*   **[GROMACS](/index.php/GROMACS "GROMACS") (GROningen MAchine for Chemical Simulations)** — Versatile package to perform molecular dynamics, i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

	[http://www.gromacs.org](http://www.gromacs.org) || [gromacs](https://aur.archlinux.org/packages/gromacs/)

*   **AmberTools** — AmberTools consists of several independently developed packages that work well by themselves, and with Amber18 itself. The suite can also be used to carry out complete molecular dynamics simulations, with either explicit water or generalized Born solvent models.

	[http://ambermd.org/AmberTools.php](http://ambermd.org/AmberTools.php) || [ambertools](https://aur.archlinux.org/packages/ambertools/)

*   **NAMD** — NAMD is a parallel molecular dynamics code designed for high-performance simulation of large biomolecular systems.

	[http://www.ks.uiuc.edu/Research/namd/](http://www.ks.uiuc.edu/Research/namd/) || [namd](https://aur.archlinux.org/packages/namd/)

*   **ORCA** — ORCA is an ab initio, DFT, and semi-empirical SCF-MO package.

	[https://orcaforum.kofo.mpg.de/app.php/portal](https://orcaforum.kofo.mpg.de/app.php/portal) || [orcaqm](https://aur.archlinux.org/packages/orcaqm/)

*   **PDB2PQR** — Electrostatic and solvation properties for complex molecules.

	[http://www.poissonboltzmann.org/](http://www.poissonboltzmann.org/) || [pdb2pqr](https://aur.archlinux.org/packages/pdb2pqr/)

*   **PMEMD** — PMEMD module of AMBER software package.

	[http://ambermd.org/AmberMD.php](http://ambermd.org/AmberMD.php) || [pmemd](https://aur.archlinux.org/packages/pmemd/), [pmemd-cuda](https://aur.archlinux.org/packages/pmemd-cuda/)

*   **[Quantum ESPRESSO](https://en.wikipedia.org/wiki/Quantum_ESPRESSO "wikipedia:Quantum ESPRESSO")** — Integrated suite of applications for electronic-structure calculations and materials modeling at nanoscale. It is based on density-functional theory, plane waves, and pseudopotentials (both norm-conserving and ultrasoft).

	[http://www.quantum-espresso.org/](http://www.quantum-espresso.org/) || [quantum-espresso](https://aur.archlinux.org/packages/quantum-espresso/)

*   **smina** — Smina is a fork of Autodock Vina that focuses on improving scoring and minimization.

	[https://sourceforge.net/projects/smina/](https://sourceforge.net/projects/smina/) || [smina-bin](https://aur.archlinux.org/packages/smina-bin/)

#### Periodic table

*   **eperiodique** — A simple Periodic Table Of Elements viewer using the EFL.

	[http://eperiodique.sourceforge.net/](http://eperiodique.sourceforge.net/) || [eperiodique](https://aur.archlinux.org/packages/eperiodique/)

*   **gElemental** — Periodic table of the elements with additional information.

	[http://freshmeat.sourceforge.net/projects/gelemental](http://freshmeat.sourceforge.net/projects/gelemental) || [gelemental](https://aur.archlinux.org/packages/gelemental/)

*   **Kalzium** — Periodic table of the elements with molecule editor and equation solver. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/kalzium/](https://www.kde.org/applications/education/kalzium/) || [kalzium](https://www.archlinux.org/packages/?name=kalzium)

### Earth science

#### Geography

*   **BT747** — The swiss army knife for MTK GPS dataloggers.

	[https://sourceforge.net/projects/bt747/](https://sourceforge.net/projects/bt747/) || [bt747](https://www.archlinux.org/packages/?name=bt747)

*   **FoxtrotGPS** — Lightweight and fast mapping application.

	[https://www.foxtrotgps.org/](https://www.foxtrotgps.org/) || [foxtrotgps](https://aur.archlinux.org/packages/foxtrotgps/)

*   **Gebabbel** — Alternative GUI for GPSBabel.

	[http://gebabbel.sourceforge.net/](http://gebabbel.sourceforge.net/) || [gebabbel](https://aur.archlinux.org/packages/gebabbel/)

*   **Geotag** — Match date/time information from photos with location information from a GPS unit or from a map.

	[http://geotag.sourceforge.net/](http://geotag.sourceforge.net/) || [geotag](https://www.archlinux.org/packages/?name=geotag)

*   **GNOME Maps** — A simple map client for GNOME. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Maps](https://wiki.gnome.org/Apps/Maps) || [gnome-maps](https://www.archlinux.org/packages/?name=gnome-maps)

*   **GottenGeography** — Easy to use photo geotagging application for the GNOME desktop.

	[https://launchpad.net/gottengeography](https://launchpad.net/gottengeography) || [gottengeography](https://www.archlinux.org/packages/?name=gottengeography)

*   **Gpredict** — Real-time satellite tracking and orbit prediction application.

	[http://gpredict.oz9aec.net/](http://gpredict.oz9aec.net/) || [gpredict](https://aur.archlinux.org/packages/gpredict/)

*   **GPSBabel** — Reads, writes, and manipulates GPS waypoints, tracks, routes in a variety of formats.

	[https://www.gpsbabel.org/](https://www.gpsbabel.org/) || [gpsbabel](https://www.archlinux.org/packages/?name=gpsbabel)

*   **GPSCorrelate** — Correlate (geotagging) digital camera photos with GPS data in GPX format.

	[https://github.com/freefoote/gpscorrelate](https://github.com/freefoote/gpscorrelate) || [gpscorrelate](https://www.archlinux.org/packages/?name=gpscorrelate)

*   **[gpsd](https://en.wikipedia.org/wiki/gpsd "wikipedia:gpsd")** — Service daemon that monitors one or more GPSes or AIS receivers attached to a host computer through serial or USB ports, making all data on the location/course/velocity of the sensors available to be queried on TCP port 2947 of the host computer.

	[http://catb.org/gpsd/](http://catb.org/gpsd/) || [gpsd](https://www.archlinux.org/packages/?name=gpsd)

*   **GpsPrune** — View, edit and convert coordinate data from GPS systems.

	[https://activityworkshop.net/software/gpsprune/](https://activityworkshop.net/software/gpsprune/) || [gpsprune](https://www.archlinux.org/packages/?name=gpsprune)

*   **GPXSee** — GPS log file viewer and analyzer.

	[http://www.gpxsee.org/](http://www.gpxsee.org/) || [gpxsee](https://www.archlinux.org/packages/?name=gpxsee)

*   **GPX Viewer** — Simple tool to visualize tracks and waypoints stored in a gpx file.

	[https://blog.sarine.nl/tag/gpxviewer/](https://blog.sarine.nl/tag/gpxviewer/) || [gpx-viewer](https://www.archlinux.org/packages/?name=gpx-viewer)

*   **[GRASS GIS](https://en.wikipedia.org/wiki/GRASS_GIS "wikipedia:GRASS GIS")** — Geospatial data management and analysis, image processing, graphics/maps production, spatial modeling and visualization.

	[https://grass.osgeo.org/](https://grass.osgeo.org/) || [grass](https://aur.archlinux.org/packages/grass/)

*   **[gvSIG](https://en.wikipedia.org/wiki/gvSIG "wikipedia:gvSIG")** — vSIG is a geographic information system (GIS), that is, a desktop application designed for capturing, storing, handling, analyzing and deploying any kind of referenced geographic information in order to solve complex management and planning problems.

	[http://www.gvsig.com/en](http://www.gvsig.com/en) || [gvsig-desktop-bin](https://aur.archlinux.org/packages/gvsig-desktop-bin/)

*   **JOSM** — Main editor for OpenStreetMap written in Java.

	[https://josm.openstreetmap.de/](https://josm.openstreetmap.de/) || [josm](https://www.archlinux.org/packages/?name=josm)

*   **Mapton** — Extensible desktop map and globe application written in Java.

	[https://mapton.org/](https://mapton.org/) || [mapton](https://aur.archlinux.org/packages/mapton/)

*   **[Marble](https://en.wikipedia.org/wiki/Marble_(software) "wikipedia:Marble (software)")** — Virtual Globe and World Atlas that can be used to learn more about the Earth. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://marble.kde.org/](https://marble.kde.org/) || KDE: [marble](https://www.archlinux.org/packages/?name=marble), Qt: [marble-qt](https://www.archlinux.org/packages/?name=marble-qt)

*   **Merkaartor** — OpenStreetMap editor.

	[http://merkaartor.be/](http://merkaartor.be/) || [merkaartor](https://www.archlinux.org/packages/?name=merkaartor)

*   **Navit** — Modular turn-by-turn car navigation system.

	[https://www.navit-project.org/](https://www.navit-project.org/) || [navit](https://www.archlinux.org/packages/?name=navit)

*   **OffRoad** — Offline vector map display ported from OsmAnd.

	[https://sourceforge.net/projects/offroadosm/](https://sourceforge.net/projects/offroadosm/) || [offroad](https://www.archlinux.org/packages/?name=offroad)

*   **OpenOrienteering Mapper** — Orienteering mapmaking program.

	[https://www.openorienteering.org/apps/mapper/](https://www.openorienteering.org/apps/mapper/) || [openorienteering-mapper](https://aur.archlinux.org/packages/openorienteering-mapper/)

*   **QMapShack** — Plan your next outdoor trip.

	[https://bitbucket.org/maproom/qmapshack](https://bitbucket.org/maproom/qmapshack) || [qmapshack](https://www.archlinux.org/packages/?name=qmapshack)

*   **QGIS** — Geographic Information System (GIS) that supports vector, raster & database formats.

	[https://qgis.org/](https://qgis.org/) || [qgis](https://www.archlinux.org/packages/?name=qgis)

*   **[Subsurface](https://en.wikipedia.org/wiki/Subsurface_(software) "wikipedia:Subsurface (software)")** — Diving logbook to keep track of your dives by logging dive locations (with GPS coordinates), weights and exposure protection used, divemasters and dive buddies, etc.

	[https://subsurface-divelog.org/](https://subsurface-divelog.org/) || [subsurface](https://www.archlinux.org/packages/?name=subsurface)

*   **Viking** — GTK 2 application to manage GPS data.

	[https://sourceforge.net/projects/viking/](https://sourceforge.net/projects/viking/) || [viking](https://www.archlinux.org/packages/?name=viking)

#### Meteorology

*   **Gis Weather** — Customizable weather forecast desktop widget.

	[https://sourceforge.net/projects/gis-weather/](https://sourceforge.net/projects/gis-weather/) || [gis-weather](https://aur.archlinux.org/packages/gis-weather/)

*   **GNOME Weather** — Small application for GNOME that allows you to monitor the current weather conditions for your city, or anywhere in the world, and to access updated forecasts provided by various internet services.

	[https://wiki.gnome.org/Apps/Weather](https://wiki.gnome.org/Apps/Weather) || [gnome-weather](https://www.archlinux.org/packages/?name=gnome-weather)

*   **meteo-qt** — System tray application for weather status information.

	[https://github.com/dglent/meteo-qt](https://github.com/dglent/meteo-qt) || [meteo-qt](https://aur.archlinux.org/packages/meteo-qt/)

*   **wttr** — A simple console application to check the weather, using data from [http://wttr.in](http://wttr.in)

	[https://github.com/AmirrezaFiroozi/wttr](https://github.com/AmirrezaFiroozi/wttr) || [wttr](https://aur.archlinux.org/packages/wttr/)

*   **Xfce Weather Panel Plugin** — Weather forecast plugin for the Xfce4 panel.

	[https://goodies.xfce.org/projects/panel-plugins/xfce4-weather-plugin](https://goodies.xfce.org/projects/panel-plugins/xfce4-weather-plugin) || [xfce4-weather-plugin](https://www.archlinux.org/packages/?name=xfce4-weather-plugin)

### Astronomy

*   **[Celestia](https://en.wikipedia.org/wiki/Celestia "wikipedia:Celestia")** — 3D astronomy simulation program that allows users to travel through an extensive universe, modeled after reality, at any speed, in any direction and at any time in history.

	[https://celestiaproject.net/](https://celestiaproject.net/) || [celestia](https://www.archlinux.org/packages/?name=celestia)

*   **GIMP Astronomy Plugins** — Set of GIMP plugins for astronomical image processing.

	[http://hennigbuam.de/georg/gimp.html](http://hennigbuam.de/georg/gimp.html) || [gimp-plugin-astronomy](https://aur.archlinux.org/packages/gimp-plugin-astronomy/)

*   **GoQat** — Camera acquisition software, especially for QSI cameras, that provides other features such as autoguiding, focusing help and others.

	[http://canburytech.net/GoQat/](http://canburytech.net/GoQat/) || [goqat](https://aur.archlinux.org/packages/goqat/)

*   **[KStars](https://en.wikipedia.org/wiki/KStars "wikipedia:KStars")** — Planetarium application that provides an accurate graphical simulation of the night sky, from any location on Earth, at any date and time. It is included in KDE Edu.

	[https://edu.kde.org/kstars/](https://edu.kde.org/kstars/) || [kstars](https://www.archlinux.org/packages/?name=kstars)

*   **Qastrocam-g2** — Webcam acquisition software for planetary imaging.

	[https://sourceforge.net/projects/qastrocam-g2/](https://sourceforge.net/projects/qastrocam-g2/) || [qastrocam-g2](https://aur.archlinux.org/packages/qastrocam-g2/)

*   **[Skychart / Cartes du Ciel](https://en.wikipedia.org/wiki/Cartes_du_Ciel "wikipedia:Cartes du Ciel")** — Planetarium that maps out and labels most of the constellations, planets, and objects you can see with a telescope. It can also download Digitized Sky Survey Charts and superimpose images over these charts.

	[https://www.ap-i.net/skychart/](https://www.ap-i.net/skychart/) || [skychart](https://aur.archlinux.org/packages/skychart/)

*   **StarPlot** — 3-dimensional star chart viewer.

	[http://starplot.org/](http://starplot.org/) || [starplot](https://aur.archlinux.org/packages/starplot/)

*   **[Stellarium](https://en.wikipedia.org/wiki/Stellarium_(computer_program) "wikipedia:Stellarium (computer program)")** — Beautiful 3D planetarium that uses OpenGL to render a realistic sky in real time.

	[http://stellarium.org/](http://stellarium.org/) || [stellarium](https://www.archlinux.org/packages/?name=stellarium)

*   **Where Is M13** — Application to visualize the locations and physical properties of deep sky objects.

	[http://www.thinkastronomy.com/M13/](http://www.thinkastronomy.com/M13/) || [where-is-m13](https://aur.archlinux.org/packages/where-is-m13/)

*   **[XEphem](https://en.wikipedia.org/wiki/XEphem "wikipedia:XEphem")** — Motif-based ephemeris and planetarium program.

	[http://www.clearskyinstitute.com/xephem/xephem.html](http://www.clearskyinstitute.com/xephem/xephem.html) || [xephem](https://aur.archlinux.org/packages/xephem/)

### Biology

*   **[Gramps](https://en.wikipedia.org/wiki/Gramps "wikipedia:Gramps")** — Genealogy program, which helps you track your family tree.

	[https://gramps-project.org/](https://gramps-project.org/) || [gramps](https://www.archlinux.org/packages/?name=gramps)

#### Computational biology and bioinformatics

See also [Wikipedia:List of open source bioinformatics software](https://en.wikipedia.org/wiki/List_of_open_source_bioinformatics_software "wikipedia:List of open source bioinformatics software").

*   **[BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") (Biochemical Algorithms Library)** — Application framework in C++ that provides an extensive set of data structures as well as classes for molecular mechanics, advanced solvation methods, comparison and analysis of protein structures, file import/export, and visualization.

	[https://ball-project.org/](https://ball-project.org/) || [ball](https://aur.archlinux.org/packages/ball/)

*   **[BioJava](https://en.wikipedia.org/wiki/BioJava "wikipedia:BioJava")** — Set of Java tools for computational biology, as well as bioinformatics.

	[https://biojava.org/](https://biojava.org/) || [biojava](https://aur.archlinux.org/packages/biojava/)

*   **[Biopython](https://en.wikipedia.org/wiki/Biopython "wikipedia:Biopython")** — Python package with tools for computational biology, as well as bioinformatics.

	[https://biopython.org/wiki/Biopython](https://biopython.org/wiki/Biopython) || [python-biopython](https://www.archlinux.org/packages/?name=python-biopython) [python2-biopython](https://www.archlinux.org/packages/?name=python2-biopython)

*   **[EMBOSS](https://en.wikipedia.org/wiki/EMBOSS "wikipedia:EMBOSS") (European Molecular Biology Open Software Suite)** — Open source software analysis package specially developed for the needs of the molecular biology and bioinformatics user community.

	[http://emboss.sourceforge.net/](http://emboss.sourceforge.net/) || [emboss](https://aur.archlinux.org/packages/emboss/)

*   **[MEGA](https://en.wikipedia.org/wiki/MEGA,_Molecular_Evolutionary_Genetics_Analysis "wikipedia:MEGA, Molecular Evolutionary Genetics Analysis") (Molecular Evolutionary Genetics Analysis)** — Integrated tool for conducting automatic and manual sequence alignment, inferring phylogenetic trees, mining web-based databases, estimating rates of molecular evolution, inferring ancestral sequences, and testing evolutionary hypotheses.

	[https://www.megasoftware.net/](https://www.megasoftware.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[MUMmer](https://en.wikipedia.org/wiki/MUMmer "wikipedia:MUMmer")** — Bioinformatics software system for sequence alignment based on suffix trees.

	[http://mummer.sourceforge.net/](http://mummer.sourceforge.net/) || [mummer](https://aur.archlinux.org/packages/mummer/)

*   **[Snapgene](https://en.wikipedia.org/wiki/Snapgene "wikipedia:Snapgene")** — Closed source molecular cloning application that offers a fast and easy way to plan, visualize, and document molecular biology procedures. Supports a wide range of cloning and PCR manipulations. The free version allows most common visualizations of a molecular biology workflow.

	[https://www.snapgene.com/](https://www.snapgene.com/) || [snapgene-viewer](https://aur.archlinux.org/packages/snapgene-viewer/)

*   **[UGENE](https://en.wikipedia.org/wiki/UGENE "wikipedia:UGENE")** — Application that integrates dozens of well-known biological tools and algorithms, providing both graphical user and command-line interfaces.

	[http://ugene.net/](http://ugene.net/) || [ugene-bin](https://aur.archlinux.org/packages/ugene-bin/)

#### Biochemistry

*   **[Bioclipse](https://en.wikipedia.org/wiki/Bioclipse "wikipedia:Bioclipse")** — Java-based visual platform for biochemistry that uses the Eclipse Rich Client Platform (RCP).

	[http://www.bioclipse.net/](http://www.bioclipse.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

#### Image manipulation

*   **[ImageJ](https://en.wikipedia.org/wiki/ImageJ "wikipedia:ImageJ")** — Java-based image processing and analysing program that provides extensibility via plugins and macros. It is widely used in microscopy (e.g. for cell counting).

	[https://imagej.nih.gov/ij/](https://imagej.nih.gov/ij/) || [imagej](https://aur.archlinux.org/packages/imagej/)

*   **[Fiji](https://en.wikipedia.org/wiki/FIJI_(software) "wikipedia:FIJI (software)")** — ImageJ distribution (and soon ImageJ2) with a lot of plugins organized into a coherent menu structure.

	[http://fiji.sc](http://fiji.sc) || [fiji-binary](https://aur.archlinux.org/packages/fiji-binary/)

#### DICOM viewers and volume rendering

*   **aeskulap** — Simple DICOM data viewer

	[http://www.nongnu.org/aeskulap/](http://www.nongnu.org/aeskulap/) || [aeskulap](https://aur.archlinux.org/packages/aeskulap/)

*   **weasis** — Multipurpose DICOM viewer with a highly modular architecture

	[https://nroduit.github.io/en/](https://nroduit.github.io/en/) || [weasis-bin](https://aur.archlinux.org/packages/weasis-bin/)

*   **aliza** — Open 2D, 3D and 4D images in DICOM, MetaIO, Nifti, Nrrd and other formats, meshes in DICOM, VTK, STL and OBJ formats

	[https://www.aliza-dicom-viewer.com/](https://www.aliza-dicom-viewer.com/) || [aliza](https://aur.archlinux.org/packages/aliza/)

*   **[Ginkgo CADx](https://en.wikipedia.org/wiki/Ginkgo_CADx "wikipedia:Ginkgo CADx")** — Advanced DICOM viewer and dicomizer. Continuation of the now abandoned free version developed by MetaEmotion

	[https://github.com/gerddie/ginkgocadx](https://github.com/gerddie/ginkgocadx) || [ginkgo-cadx](https://aur.archlinux.org/packages/ginkgo-cadx/)

*   **[3DSlicer](https://en.wikipedia.org/wiki/3DSlicer "wikipedia:3DSlicer")** — Comprehensive [MRI](https://en.wikipedia.org/wiki/Magnetic_resonance_imaging "wikipedia:Magnetic resonance imaging"), [CT](https://en.wikipedia.org/wiki/CT_scan "wikipedia:CT scan"), [LSCM microscopy](https://en.wikipedia.org/wiki/Laser_scanning_confocal_microscopy "wikipedia:Laser scanning confocal microscopy") volume processing, segmentation and 3D-reconstruction

	[https://www.slicer.org/](https://www.slicer.org/) || [3dslicer](https://aur.archlinux.org/packages/3dslicer/)

### Engineering

#### Computer-aided design

See also [Wikipedia:List of computer-aided design editors](https://en.wikipedia.org/wiki/List_of_computer-aided_design_editors "wikipedia:List of computer-aided design editors").

*   **[BRL-CAD](https://en.wikipedia.org/wiki/BRL-CAD "wikipedia:BRL-CAD")** — Constructive solid geometry (CSG) solid modeling computer-aided design (CAD) system that includes an interactive geometry editor, ray tracing support for graphics rendering and geometric analysis, computer network distributed framebuffer support, scripting, image-processing and signal-processing tools.

	[http://brlcad.org/](http://brlcad.org/) || [brlcad](https://aur.archlinux.org/packages/brlcad/)

*   **DraftSight** — Dassault Systemes' freeware 2D CAD application. DraftSight allows users to access DWG/DXF files, regardless of which CAD software was originally used to create them.

	[https://www.3ds.com/products-services/draftsight-cad-software/](https://www.3ds.com/products-services/draftsight-cad-software/) || [draftsight](https://aur.archlinux.org/packages/draftsight/)

*   **[FreeCAD](https://en.wikipedia.org/wiki/FreeCAD "wikipedia:FreeCAD")** — CAD/CAE program, based on OpenCascade, Qt and Python with features such as macro recording, workbenches and the ability to run as server.

	[https://github.com/FreeCAD/FreeCAD](https://github.com/FreeCAD/FreeCAD) || [freecad](https://aur.archlinux.org/packages/freecad/)

*   **LeoCAD** — CAD program for creating virtual LEGO models. It has an easy to use interface and currently includes over 6000 different pieces created by the LDraw community.

	[https://www.leocad.org/](https://www.leocad.org/) || [leocad](https://aur.archlinux.org/packages/leocad/)

*   **[LibreCAD](https://en.wikipedia.org/wiki/LibreCAD "wikipedia:LibreCAD")** — Powerful 2D CAD application based on Qt. It has been forked from QCad Community Edition.

	[https://www.librecad.org/](https://www.librecad.org/) || [librecad](https://www.archlinux.org/packages/?name=librecad)

*   **[OpenSCAD](https://en.wikipedia.org/wiki/OpenSCAD "wikipedia:OpenSCAD")** — Open source 2D/3D CAD using programmers approach.

	[http://www.openscad.org](http://www.openscad.org) || [openscad](https://www.archlinux.org/packages/?name=openscad)

*   **[QCAD](https://en.wikipedia.org/wiki/QCad "wikipedia:QCad")** — Powerful 2D CAD application that began in 1999\. QCaD includes DFX standard file format and supports HPGL format.

	[https://www.qcad.org/](https://www.qcad.org/) || [qcad](https://www.archlinux.org/packages/?name=qcad)

#### Electronics

See also [Wikipedia:Comparison of EDA software](https://en.wikipedia.org/wiki/Comparison_of_EDA_software "wikipedia:Comparison of EDA software").

##### Digital logic

Digital logic software are mainly simple educational tools that intended for only designing and simulating logic circuits.

*   **glogic** — An educational graphical logic circuit simulator, written in Python.

	[https://launchpad.net/glogic](https://launchpad.net/glogic) || [glogic](https://aur.archlinux.org/packages/glogic/)

*   **GTKWave** — Fully featured GTK-based wave viewer which reads LXT, LXT2, VZT, FST, and GHW files as well as standard Verilog VCD/EVCD files and allows their viewing.

	[http://gtkwave.sourceforge.net/](http://gtkwave.sourceforge.net/) || [gtkwave](https://www.archlinux.org/packages/?name=gtkwave)

*   **Logisim** — Educational digital logic design and simulation software, written in Java, officially its development has stopped.

	[https://sourceforge.net/projects/circuit/](https://sourceforge.net/projects/circuit/) || [logisim](https://aur.archlinux.org/packages/logisim/)

*   **Logisim Evolution** — Project which continue the development of the original Logisim with new features, written in Java.

	[https://github.com/reds-heig/logisim-evolution](https://github.com/reds-heig/logisim-evolution) || [logisim-evolution-git](https://aur.archlinux.org/packages/logisim-evolution-git/)

*   **PulseView** — Logic analyzer, oscilloscope and MSO GUI.

	[https://sigrok.org/wiki/PulseView](https://sigrok.org/wiki/PulseView) || [pulseview](https://www.archlinux.org/packages/?name=pulseview)

*   **SmartSim** — Simple and beautiful digital logic circuit design and simulation software, mainly target teachers and students, very lightweight and cross platform, GPL licensed, written in Vala.

	[https://smartsim.org.uk](https://smartsim.org.uk) || [smartsim-git](https://aur.archlinux.org/packages/smartsim-git/)

##### HDL

Also see [Wikipedia:Hardware description language](https://en.wikipedia.org/wiki/Hardware_description_language "wikipedia:Hardware description language").

*   **[Altera Design Software](/index.php/Altera_Design_Software "Altera Design Software")** — A set of design tools for Altera's FPGA chips that includes Quartus II and ModelSim-Altera.

	[https://www.altera.com/products/design-software/overview.html](https://www.altera.com/products/design-software/overview.html) || see [Altera Design Software](/index.php/Altera_Design_Software "Altera Design Software")

*   **[Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")** — FPGA programmable logic design suit.

	[https://www.xilinx.com/products/design-tools/ise-design-suite/ise-webpack.html](https://www.xilinx.com/products/design-tools/ise-design-suite/ise-webpack.html) || see [Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")

##### MCU IDE and programmers

*   **[Arduino](/index.php/Arduino "Arduino")** — Arduino prototyping platform SDK.

	[https://www.arduino.cc/en/Main/Software](https://www.arduino.cc/en/Main/Software) || [arduino](https://www.archlinux.org/packages/?name=arduino)

*   **avrcalc** — Calculator to speed development of Atmel AVRs.

	[https://sourceforge.net/projects/avrcalc](https://sourceforge.net/projects/avrcalc) || [avrcalc](https://aur.archlinux.org/packages/avrcalc/)

*   **AVRDUDE** — Download/upload/manipulate the ROM and EEPROM contents of AVR microcontrollers.

	[http://www.nongnu.org/avrdude/](http://www.nongnu.org/avrdude/) || [avrdude](https://www.archlinux.org/packages/?name=avrdude)

*   **SPIPGM** — Tool for programming serial SPI FlashROM memories attached to PC via parallel port cable.

	[http://rayer.g6.cz/programm/programe.htm](http://rayer.g6.cz/programm/programe.htm) || [spipgm-bin](https://aur.archlinux.org/packages/spipgm-bin/)

##### Schematic capture editor

*   **freeroute** — Automatic PCB track router for KiCad written by Alfons Wirtz.

	[http://www.freerouting.net/](http://www.freerouting.net/) || [freeroute-bin](https://aur.archlinux.org/packages/freeroute-bin/)

*   **[gEDA](/index.php/GEDA "GEDA")** — Full suite and toolkit of Electronic Design Automation tools that are used for electrical circuit design, schematic capture, simulation, prototyping, and production.

	[http://www.geda-project.org/](http://www.geda-project.org/) || [geda-gaf](https://www.archlinux.org/packages/?name=geda-gaf)

*   **[gEDA](/index.php/GEDA "GEDA") PCB** — Interactive printed circuit board editor.

	[http://pcb.geda-project.org/](http://pcb.geda-project.org/) || [pcb](https://www.archlinux.org/packages/?name=pcb)

*   **[KiCad](https://en.wikipedia.org/wiki/KiCad "wikipedia:KiCad")** — Software suite for electronic design automation (EDA) that facilitates the design of schematics for electronic circuits and their conversion to PCB (printed circuit board).

	[http://kicad-pcb.org/](http://kicad-pcb.org/) || [kicad](https://www.archlinux.org/packages/?name=kicad)

*   **[Oregano](https://en.wikipedia.org/wiki/Oregano_(software) "wikipedia:Oregano (software)")** — Graphical software application for schematic capture and simulation of electrical circuits. The actual simulation is done by the [ngspice](https://en.wikipedia.org/wiki/Ngspice "wikipedia:Ngspice") or [Gnucap](https://en.wikipedia.org/wiki/GNU_Circuit_Analysis_Package "wikipedia:GNU Circuit Analysis Package") engines.

	[https://github.com/drahnr/oregano](https://github.com/drahnr/oregano) || [oregano](https://aur.archlinux.org/packages/oregano/)

*   **QElectroTech** — Application used to draw advanced electrical circuits.

	[https://qelectrotech.org/](https://qelectrotech.org/) || [qelectrotech](https://aur.archlinux.org/packages/qelectrotech/)

*   **[Qucs](https://en.wikipedia.org/wiki/Quite_Universal_Circuit_Simulator "wikipedia:Quite Universal Circuit Simulator")** — Electronics circuit simulator application that gives you the ability to set up a circuit with a graphical user interface and simulate its large-signal, small-signal and noise behaviour.

	[http://qucs.sourceforge.net/](http://qucs.sourceforge.net/) || [qucs](https://aur.archlinux.org/packages/qucs/)

*   **[ngspice](https://en.wikipedia.org/wiki/ngspice "wikipedia:ngspice")** — Application used to simulate circuits. Open source successor of [spice3f5](https://en.wikipedia.org/wiki/SPICE "wikipedia:SPICE")

	[http://ngspice.sourceforge.net/](http://ngspice.sourceforge.net/) || [ngspice](https://www.archlinux.org/packages/?name=ngspice)

### Telecommunication

*   **CupCarbon** — A Smart City & IoT Wireless Sensor Network Simulator.

	[http://cupcarbon.com/](http://cupcarbon.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[GNU Radio](/index.php/GNU_Radio "GNU Radio")** — Software development toolkit that provides signal processing blocks to implement software radios.

	[https://www.gnuradio.org/](https://www.gnuradio.org/) || [gnuradio](https://www.archlinux.org/packages/?name=gnuradio)

*   **Gqrx** — Software defined radio receiver implemented using GNU Radio and the Qt GUI toolkit.

	[http://gqrx.dk/](http://gqrx.dk/) || [gqrx](https://www.archlinux.org/packages/?name=gqrx)

*   **Pothos** — The Pothos project is a complete data-flow framework for creating topologies of interconnected processing blocks.

	[https://github.com/pothosware/PothosCore/wiki](https://github.com/pothosware/PothosCore/wiki) || [pothos](https://aur.archlinux.org/packages/pothos/), [pothos-git](https://aur.archlinux.org/packages/pothos-git/)

*   **SDR#** — The most popular SDR program.

	[https://airspy.com/](https://airspy.com/) || [sdrsharp](https://aur.archlinux.org/packages/sdrsharp/)

*   **SigDigger** — Qt-based digital signal analyzer, using Suscan core and Sigutils DSP library.

	[https://github.com/BatchDrake/SigDigger](https://github.com/BatchDrake/SigDigger) || [sigdigger-git](https://aur.archlinux.org/packages/sigdigger-git/)

#### Amateur radio

See the main article: [Amateur radio#Software list](/index.php/Amateur_radio#Software_list "Amateur radio").

See also [Wikipedia:List of software-defined radios](https://en.wikipedia.org/wiki/List_of_software-defined_radios "wikipedia:List of software-defined radios").

### Simulation modeling

*   **[gephi](https://en.wikipedia.org/wiki/Gephi "wikipedia:Gephi")** — Gephi is an open-source network analysis and visualization software package written in Java.

	[https://gephi.org/](https://gephi.org/) || [gephi](https://www.archlinux.org/packages/?name=gephi)

*   **golly** — Golly is an open source, cross-platform application for exploring Conway's Game of Life and many other types of cellular automata.

	[http://golly.sourceforge.net/](http://golly.sourceforge.net/) || [golly](https://aur.archlinux.org/packages/golly/)

*   **Netlogo** — NetLogo is a multi-agent programmable modeling environment.

	[http://ccl.northwestern.edu/netlogo/](http://ccl.northwestern.edu/netlogo/) || [netlogo](https://aur.archlinux.org/packages/netlogo/)

*   **[AnyLogic](https://en.wikipedia.org/wiki/AnyLogic "wikipedia:AnyLogic")** — AnyLogic is a cross-platform proprietary multimethod simulation modeling tool, which is also available for personal use.

	[https://www.anylogic.com/](https://www.anylogic.com/) || [anylogic-ple](https://aur.archlinux.org/packages/anylogic-ple/), [anylogic-university](https://aur.archlinux.org/packages/anylogic-university/), [anylogic-professional](https://aur.archlinux.org/packages/anylogic-professional/)

### Computer science

#### Artificial intelligence

See also [Wikipedia:Comparison of deep learning software](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software "wikipedia:Comparison of deep learning software").

*   **[Fast Artificial Neural Network](https://en.wikipedia.org/wiki/Fast_Artificial_Neural_Network "wikipedia:Fast Artificial Neural Network")** — Library for developing feedforward Artificial Neural Networks.

	[http://leenissen.dk/fann/wp/](http://leenissen.dk/fann/wp/) || [fann](https://aur.archlinux.org/packages/fann/)

*   **[Mycroft](https://en.wikipedia.org/wiki/Mycroft_(software) "wikipedia:Mycroft (software)")** — Intelligent personal assistant and knowledge navigator with speech recognition.

	[https://mycroft.ai/](https://mycroft.ai/) || [mycroft-core](https://aur.archlinux.org/packages/mycroft-core/)

*   **[Orange](https://en.wikipedia.org/wiki/Orange_(software) "wikipedia:Orange (software)")** — Data visualization, machine learning and data mining toolkit, accessible via visual programming and Python.

	[https://orange.biolab.si/](https://orange.biolab.si/) || [python-orange](https://aur.archlinux.org/packages/python-orange/)

*   **[Torch](https://en.wikipedia.org/wiki/Torch_(machine_learning) "wikipedia:Torch (machine learning)")** — Machine learning library, scientific computing framework, and script language based on LuaJIT.

	[http://torch.ch/](http://torch.ch/) || [torch7-git](https://aur.archlinux.org/packages/torch7-git/)

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — Automatic (intelligent) keyboard layout adaption.

	[https://xneur.ru/](https://xneur.ru/) || [xneur](https://aur.archlinux.org/packages/xneur/), [gxneur](https://aur.archlinux.org/packages/gxneur/)

*   **[Tensorflow](https://en.wikipedia.org/wiki/Tensorflow "wikipedia:Tensorflow")** — An end-to-end open source machine learning platform.

	[https://www.tensorflow.org/](https://www.tensorflow.org/) || [python-tensorflow](https://www.archlinux.org/packages/?name=python-tensorflow), with non x86-64 CPU optimization [python-tensorflow-opt](https://www.archlinux.org/packages/?name=python-tensorflow-opt), with CUDA [python-tensorflow-cuda](https://www.archlinux.org/packages/?name=python-tensorflow-cuda), with CUDA and with non x86-64 CPU optimizations [python-tensorflow-opt-cuda](https://www.archlinux.org/packages/?name=python-tensorflow-opt-cuda)

*   **[PyTorch](https://en.wikipedia.org/wiki/PyTorch "wikipedia:PyTorch")** — An open source machine learning framework that accelerates the path from research prototyping to production deployment.

	[https://pytorch.org/](https://pytorch.org/) || [python-pytorch](https://www.archlinux.org/packages/?name=python-pytorch), with non x86-64 CPU optimization [python-pytorch-opt](https://www.archlinux.org/packages/?name=python-pytorch-opt), with CUDA [python-pytorch-cuda](https://www.archlinux.org/packages/?name=python-pytorch-cuda), with CUDA and with non x86-64 CPU optimizations [python-pytorch-opt-cuda](https://www.archlinux.org/packages/?name=python-pytorch-opt-cuda)

## Others

### Organization

#### Personal information managers

These applications support time, task and contacts management.

*   **[Evolution](/index.php/Evolution "Evolution")** — Personal information management application that provides integrated mail, calendaring and address book functionality. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution](https://www.archlinux.org/packages/?name=evolution)

*   **[Kontact](https://en.wikipedia.org/wiki/Kontact "wikipedia:Kontact")** — Integrated solution to your personal information management.

	[https://kontact.kde.org/](https://kontact.kde.org/) || [kontact](https://www.archlinux.org/packages/?name=kontact)

*   **Osmo** — GTK personal organizer, which includes calendar, tasks manager and address book modules.

	[http://clayo.org/osmo/](http://clayo.org/osmo/) || [osmo](https://www.archlinux.org/packages/?name=osmo)

*   **[SeaMonkey Mail & Newsgroups](https://en.wikipedia.org/wiki/SeaMonkey#Mail "wikipedia:SeaMonkey") with [Lightning](https://en.wikipedia.org/wiki/Lightning_(software) "wikipedia:Lightning (software)")** — Extension to SeaMonkey that provides calendar and task support.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird") with [Lightning](https://en.wikipedia.org/wiki/Lightning_(software) "wikipedia:Lightning (software)")** — Extension to Mozilla Thunderbird that provides calendar and task support.

	[https://www.thunderbird.net/calendar/](https://www.thunderbird.net/calendar/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

#### Time management

##### Console

*   **Calcurse** — Text-based ncurses calendar and scheduling system (supports CalDAV)

	[https://calcurse.org](https://calcurse.org) || [calcurse](https://www.archlinux.org/packages/?name=calcurse)

*   **ccal** — A console program which writes a calendar together with Chinese calendar to standard output.

	[http://ccal.chinesebay.com/ccal/ccal.htm](http://ccal.chinesebay.com/ccal/ccal.htm) || [ccal](https://aur.archlinux.org/packages/ccal/)

*   **khal** — Command-line (non-interactive) and ncurses (interactive) calendar system (supports CalDAV)

	[https://github.com/pimutils/khal](https://github.com/pimutils/khal) || [khal](https://www.archlinux.org/packages/?name=khal)

*   **mail2rem** — Small script for importing *.ics calendars from Maildir to Remind calendar.

	[https://github.com/esovetkin/mail2rem](https://github.com/esovetkin/mail2rem) || [mail2rem-git](https://aur.archlinux.org/packages/mail2rem-git/)

*   **Pal** — Very lightweight calendar with both interactive and non-interactive interfaces.

	[http://palcal.sourceforge.net/](http://palcal.sourceforge.net/) || [pal](https://aur.archlinux.org/packages/pal/)

*   **pcal** — A tool to create pdf calendars from pcal input which can be exported by some calendar programs.

	[https://sourceforge.net/projects/pcal/](https://sourceforge.net/projects/pcal/) || [pcal](https://aur.archlinux.org/packages/pcal/)

*   **[Remind](/index.php/Remind "Remind")** — Highly sophisticated text-based calendaring and notification system.

	[https://www.roaringpenguin.com/products/remind](https://www.roaringpenguin.com/products/remind) || [remind](https://www.archlinux.org/packages/?name=remind)

*   **When** — Simple personal calendar program.

	[http://lightandmatter.com/when/when.html](http://lightandmatter.com/when/when.html) || [when](https://www.archlinux.org/packages/?name=when)

##### Graphical

*   **chinese-calendar** — Chinese traditional calendar for Ubuntu Kylin.

	[https://launchpad.net/chinese-calendar/](https://launchpad.net/chinese-calendar/) || [chinese-calendar](https://www.archlinux.org/packages/?name=chinese-calendar)

*   **Day Planner** — Program designed to help you easily plan and manage your time. It can manage appointments, birthdays and more.

	[http://www.day-planner.org/](http://www.day-planner.org/) || [dayplanner](https://aur.archlinux.org/packages/dayplanner/)

*   **Deepin Calendar** — Calendar application for Deepin.

	[https://www.deepin.org/en/original/dde-calendar/](https://www.deepin.org/en/original/dde-calendar/) || [deepin-calendar](https://www.archlinux.org/packages/?name=deepin-calendar)

*   **etmtk (Event and Task Manager)** — Simple application with a "Getting Things Done!" approach to handling events, tasks, activities, reminders and projects.

	[http://people.duke.edu/~dgraham/ETMtk/](http://people.duke.edu/~dgraham/ETMtk/) || [etmtk](https://aur.archlinux.org/packages/etmtk/)

*   **GNOME Calendar** — Calendar application for GNOME.

	[https://wiki.gnome.org/Apps/Calendar](https://wiki.gnome.org/Apps/Calendar) || [gnome-calendar](https://www.archlinux.org/packages/?name=gnome-calendar)

*   **[KAlarm](https://en.wikipedia.org/wiki/KAlarm "wikipedia:KAlarm")** — Personal alarm message, command and email scheduler, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/utilities/kalarm/](https://www.kde.org/applications/utilities/kalarm/) || [kalarm](https://www.archlinux.org/packages/?name=kalarm)

*   **[KOrganizer](https://en.wikipedia.org/wiki/Kontact#Organizer "wikipedia:Kontact")** — Calendar and scheduling program, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/office/korganizer/](https://www.kde.org/applications/office/korganizer/) || [korganizer](https://www.archlinux.org/packages/?name=korganizer)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") Calendar** — Calendar app for Nextcloud.

	[https://github.com/nextcloud/calendar](https://github.com/nextcloud/calendar) || [nextcloud-app-calendar](https://www.archlinux.org/packages/?name=nextcloud-app-calendar)

*   **Orage** — GTK calendar and task manager often seen integrated with Xfce.

	[https://www.xfce.org/projects](https://www.xfce.org/projects) || [orage](https://www.archlinux.org/packages/?name=orage)

*   **Outspline** — Extensible outliner with advanced time management features, supporting events with complex recurrence schemes.

	[https://kynikos.github.io/outspline/](https://kynikos.github.io/outspline/) || [outspline](https://aur.archlinux.org/packages/outspline/)

*   **Pantheon Calendar** — Desktop calendar app designed for elementary OS.

	[https://github.com/elementary/calendar](https://github.com/elementary/calendar) || [pantheon-calendar](https://www.archlinux.org/packages/?name=pantheon-calendar)

*   **TkRemind** — Sophisticated calendar and alarm program.

	[https://www.roaringpenguin.com/products/remind](https://www.roaringpenguin.com/products/remind) || [remind](https://www.archlinux.org/packages/?name=remind)

#### Time trackers

*   **flow** — Pomodoro app that blocks distractions while you work.

	[https://github.com/iamsergio/flow-pomodoro](https://github.com/iamsergio/flow-pomodoro) || [flow-pomodoro](https://aur.archlinux.org/packages/flow-pomodoro/)

*   **Gnomato** — Timer for the [Pomodoro Technique](https://en.wikipedia.org/wiki/Pomodoro_Technique "wikipedia:Pomodoro Technique").

	[https://github.com/diegorubin/gnomato](https://github.com/diegorubin/gnomato) || [gnomato](https://aur.archlinux.org/packages/gnomato/)

*   **GNOME Break Timer** — Keeps track of how much you are using the computer, and it reminds you to take regular breaks.

	[https://wiki.gnome.org/Apps/GnomeBreakTimer](https://wiki.gnome.org/Apps/GnomeBreakTimer) || [gnome-break-timer](https://www.archlinux.org/packages/?name=gnome-break-timer)

*   **GNOME Clocks** — Clocks application for GNOME, including alarm, stopwatch and timer functionality.

	[https://wiki.gnome.org/Apps/Clocks](https://wiki.gnome.org/Apps/Clocks) || [gnome-clocks](https://www.archlinux.org/packages/?name=gnome-clocks)

*   **GNOME Pomodoro** — Time management utility for GNOME based on the [Pomodoro Technique](https://en.wikipedia.org/wiki/Pomodoro_Technique "wikipedia:Pomodoro Technique").

	[https://gnomepomodoro.org/](https://gnomepomodoro.org/) || [gnome-shell-pomodoro](https://aur.archlinux.org/packages/gnome-shell-pomodoro/)

*   **Hamster** — Time tracking application that helps you to keep track on how much time you have spent during the day on activities you choose to track.

	[http://projecthamster.org/](http://projecthamster.org/) || [hamster-time-tracker](https://aur.archlinux.org/packages/hamster-time-tracker/)

*   **Kapow** — Punch clock to track time spent on projects.

	[https://gottcode.org/kapow/](https://gottcode.org/kapow/) || [kapow](https://aur.archlinux.org/packages/kapow/)

*   **Kronometer** — Stopwatch application for KDE.

	[https://www.kde.org/applications/utilities/kronometer/](https://www.kde.org/applications/utilities/kronometer/) || [kronometer](https://www.archlinux.org/packages/?name=kronometer)

*   **KTeaTime** — Handy timer for steeping tea.

	[https://www.kde.org/applications/games/kteatime/](https://www.kde.org/applications/games/kteatime/) || [kteatime](https://www.archlinux.org/packages/?name=kteatime)

*   **Orage Globaltime** — Show clocks from different countries.

	[https://xfce.org/projects](https://xfce.org/projects) || [orage](https://www.archlinux.org/packages/?name=orage)

*   **RSIBreak** — Takes care of your health and regularly breaks your work to avoid repetitive strain injury (RSI).

	[https://userbase.kde.org/RSIBreak](https://userbase.kde.org/RSIBreak) || [rsibreak](https://www.archlinux.org/packages/?name=rsibreak)

*   **Safe Eyes** — Tool to reduce and prevent repetitive strain injury (RSI).

	[https://slgobinath.github.io/SafeEyes/](https://slgobinath.github.io/SafeEyes/) || [safeeyes](https://aur.archlinux.org/packages/safeeyes/)

*   **Tider** — Lightweight time tracking application (GTK)

	[https://pusto.org/en/tider/](https://pusto.org/en/tider/) || [tider-git](https://aur.archlinux.org/packages/tider-git/)

*   **Tomate** — Timer for the [Pomodoro Technique](https://en.wikipedia.org/wiki/Pomodoro_Technique "wikipedia:Pomodoro Technique").

	[https://github.com/eliostvs/tomate-gtk](https://github.com/eliostvs/tomate-gtk) || [tomate-gtk](https://aur.archlinux.org/packages/tomate-gtk/)

*   **Tomato** — Simple, usable and efficient pomodoro app designed for elementaryOS.

	[https://github.com/luizaugustomm/tomato](https://github.com/luizaugustomm/tomato) || [tomatoapp-bzr](https://aur.archlinux.org/packages/tomatoapp-bzr/)

*   **Tomighty** — Desktop timer for the [Pomodoro Technique](https://en.wikipedia.org/wiki/Pomodoro_Technique "wikipedia:Pomodoro Technique").

	[http://tomighty.org/](http://tomighty.org/) || [tomighty](https://aur.archlinux.org/packages/tomighty/)

*   **[Workrave](https://en.wikipedia.org/wiki/Workrave "wikipedia:Workrave")** — Program that assists in the recovery and prevention of RSI.

	[http://www.workrave.org/](http://www.workrave.org/) || [workrave](https://www.archlinux.org/packages/?name=workrave)

#### Task management

##### Console

*   **DevTodo** — Small command line application for maintaining lists of tasks.

	[https://swapoff.org/devtodo1.html](https://swapoff.org/devtodo1.html) || [devtodo](https://aur.archlinux.org/packages/devtodo/)

*   **Taskbook** — Tasks, boards & notes for the command-line habitat.

	[https://github.com/klauscfhq/taskbook](https://github.com/klauscfhq/taskbook) || [taskbook](https://aur.archlinux.org/packages/taskbook/)

*   **[Taskwarrior](https://en.wikipedia.org/wiki/Taskwarrior "wikipedia:Taskwarrior")** — Command-line To-do list application with support for lua customization and more.

	[https://taskwarrior.org/](https://taskwarrior.org/) || [task](https://www.archlinux.org/packages/?name=task)

*   **todoman** — Command-line To-do list manager (supports CalDAV)

	[https://github.com/pimutils/todoman](https://github.com/pimutils/todoman) || [todoman](https://www.archlinux.org/packages/?name=todoman)

*   **Todo.txt** — Small command-line To-do manager.

	[https://github.com/todotxt/todo.txt-cli/](https://github.com/todotxt/todo.txt-cli/) || [todotxt](https://aur.archlinux.org/packages/todotxt/)

*   **TuDu** — Ncurses-based hierarchical To-do list manager with vim-like keybindings.

	[https://code.meskio.net/tudu/](https://code.meskio.net/tudu/) || [tudu](https://aur.archlinux.org/packages/tudu/)

##### Graphical

*   **Effitask** — Graphical task manager, based on the [Todo.txt](http://todotxt.com/) format.

	[https://github.com/sanpii/effitask](https://github.com/sanpii/effitask) || [effitask](https://aur.archlinux.org/packages/effitask/)

*   **Getting Things GNOME!** — Personal tasks and TODO list items organizer for GNOME inspired by the [Getting Things Done (GTD)](https://en.wikipedia.org/wiki/Getting_Things_Done "wikipedia:Getting Things Done") methodology.

	[https://github.com/getting-things-gnome/gtg](https://github.com/getting-things-gnome/gtg) || [gtg-git](https://aur.archlinux.org/packages/gtg-git/)

*   **Go For It!** — Simple and stylish productivity app, featuring a to-do list, merged with a timer that keeps your focus on the current task. To-do lists are stored in the [Todo.txt](http://todotxt.com/) format.

	[http://manuel-kehl.de/projects/go-for-it/](http://manuel-kehl.de/projects/go-for-it/) || [go-for-it-git](https://aur.archlinux.org/packages/go-for-it-git/)

*   **GNOME To Do** — Personal task manager for GNOME.

	[https://wiki.gnome.org/Apps/Todo](https://wiki.gnome.org/Apps/Todo) || [gnome-todo](https://www.archlinux.org/packages/?name=gnome-todo)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") Tasks** — Tasks app for Nextcloud.

	[https://github.com/nextcloud/tasks](https://github.com/nextcloud/tasks) || [nextcloud-app-tasks](https://www.archlinux.org/packages/?name=nextcloud-app-tasks)

*   **ptask** — GTK task manager based on [Taskwarrior](https://en.wikipedia.org/wiki/Taskwarrior "wikipedia:Taskwarrior").

	[https://wpitchoune.net/ptask/](https://wpitchoune.net/ptask/) || [ptask](https://aur.archlinux.org/packages/ptask/)

*   **QTodoTxt** — UI client for [todo.txt](http://todotxt.com/) files.

	[https://github.com/mNantern/QTodoTxt](https://github.com/mNantern/QTodoTxt) || [qtodotxt](https://aur.archlinux.org/packages/qtodotxt/)

*   **Task Coach** — Simple todo manager to manage personal tasks and todo lists.

	[https://www.taskcoach.org](https://www.taskcoach.org) || [taskcoach](https://aur.archlinux.org/packages/taskcoach/)

*   **TaskUnifier** — Task management application which enables you to create and organize your tasks.

	[https://www.taskunifier.app](https://www.taskunifier.app) || [taskunifier](https://aur.archlinux.org/packages/taskunifier/)

*   **[Tasque](https://en.wikipedia.org/wiki/Tasque_(software) "wikipedia:Tasque (software)")** — Easy quick task management app written in C#.

	[https://wiki.gnome.org/Apps/Tasque](https://wiki.gnome.org/Apps/Tasque) || [tasque](https://aur.archlinux.org/packages/tasque/)

*   **Zanshin** — To-do management application based on Akonadi.

	[https://zanshin.kde.org/](https://zanshin.kde.org/) || [zanshin](https://www.archlinux.org/packages/?name=zanshin)

#### Contacts management

##### Console

*   **Abook** — Text-based contacts manager designed for use with mutt.

	[http://abook.sourceforge.net/](http://abook.sourceforge.net/) || [abook](https://www.archlinux.org/packages/?name=abook)

*   **Khard** — Command-line addressbook that is able to sync with CardDAV-servers.

	[https://github.com/scheibler/khard](https://github.com/scheibler/khard) || [khard](https://www.archlinux.org/packages/?name=khard)

##### Graphical

*   **GNOME Contacts** — Contacts manager for GNOME.

	[https://wiki.gnome.org/Apps/Contacts](https://wiki.gnome.org/Apps/Contacts) || [gnome-contacts](https://www.archlinux.org/packages/?name=gnome-contacts)

*   **KAddressBook** — Address book manager for KDE.

	[https://www.kde.org/applications/office/kaddressbook/](https://www.kde.org/applications/office/kaddressbook/) || [kaddressbook](https://www.archlinux.org/packages/?name=kaddressbook)

*   **LDAP Administration Tool** — Browse LDAP-based directories and add/edit/delete entries contained within.

	[https://sourceforge.net/projects/ldap-at/](https://sourceforge.net/projects/ldap-at/) || [lat](https://aur.archlinux.org/packages/lat/)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") Contacts** — Contacts app for Nextcloud.

	[https://github.com/nextcloud/contacts](https://github.com/nextcloud/contacts) || [nextcloud-app-contacts](https://www.archlinux.org/packages/?name=nextcloud-app-contacts)

*   **[phpLDAPadmin](/index.php/PhpLDAPadmin "PhpLDAPadmin")** — LDAP client webapp. Its hierarchical tree-viewer and advanced search functionality make it intuitive to browse and administer your LDAP directory.

	[http://phpldapadmin.sourceforge.net/](http://phpldapadmin.sourceforge.net/) || [phpldapadmin](https://www.archlinux.org/packages/?name=phpldapadmin)

#### Financial management

See also [Wikipedia:Comparison of accounting software](https://en.wikipedia.org/wiki/Comparison_of_accounting_software "wikipedia:Comparison of accounting software").

*   **Beancount** — A double-entry bookkeeping computer language that lets you define financial transaction records in a text file, read them in memory, generate a variety of reports from them, and provides a web interface.

	[http://furius.ca/beancount/](http://furius.ca/beancount/) || [beancount-hg](https://aur.archlinux.org/packages/beancount-hg/)

*   **BillReminder** — Small and quick accounting application designed to allow for easy tracking of bills.

	[https://gitlab.gnome.org/Archive/billreminder](https://gitlab.gnome.org/Archive/billreminder) || [billreminder](https://aur.archlinux.org/packages/billreminder/)

*   **Eqonomize!** — Cross-platform personal accounting software, with focus on efficiency and ease of use for the small household economy.

	[https://eqonomize.github.io/](https://eqonomize.github.io/) || [eqonomize-bin](https://aur.archlinux.org/packages/eqonomize-bin/)

*   **esniper** — Simple, lightweight tool for [sniping](https://en.wikipedia.org/wiki/Auction_sniping "wikipedia:Auction sniping") eBay auctions.

	[http://esniper.sourceforge.net/](http://esniper.sourceforge.net/) || [esniper](https://aur.archlinux.org/packages/esniper/)

*   **[GnuCash](https://en.wikipedia.org/wiki/GnuCash "wikipedia:GnuCash")** — Financial application that implements a double-entry book-keeping system with features for small business accounting.

	[http://www.gnucash.org/](http://www.gnucash.org/) || [gnucash](https://www.archlinux.org/packages/?name=gnucash)

*   **Grisbi** — Personal finance system which manages third party, expenditure and receipt categories, as well as budgetary lines, financial years, and other information that makes it suitable for associations.

	[http://www.grisbi.org/](http://www.grisbi.org/) || [grisbi](https://aur.archlinux.org/packages/grisbi/)

*   **[HomeBank](https://en.wikipedia.org/wiki/HomeBank "wikipedia:HomeBank")** — Easy to use finance manager that can analyse your personal finance in detail using powerful filtering tools and graphs.

	[http://homebank.free.fr/](http://homebank.free.fr/) || [homebank](https://www.archlinux.org/packages/?name=homebank)

*   **[KMyMoney](https://en.wikipedia.org/wiki/KMyMoney "wikipedia:KMyMoney")** — Personal finance manager that operates in a similar way to [Microsoft Money](https://en.wikipedia.org/wiki/Microsoft_Money "wikipedia:Microsoft Money"). It supports different account types, categorisation of expenses and incomes, reconciliation of bank accounts and import/export to the “QIF” file format.

	[http://kmymoney2.sourceforge.net/index-home.html](http://kmymoney2.sourceforge.net/index-home.html) || [kmymoney](https://www.archlinux.org/packages/?name=kmymoney)

*   **[Ledger](/index.php/Ledger "Ledger")** — Ledger is a powerful, double-entry accounting system that is accessed from the UNIX command-line.

	[http://ledger-cli.org/](http://ledger-cli.org/) || [ledger](https://www.archlinux.org/packages/?name=ledger)

*   **hledger** — An accounting program for tracking money, time, or any other commodity, using double-entry accounting and a simple, editable file format. hledger is inspired by and largely compatible with ledger.

	[https://hledger.org/](https://hledger.org/) || [hledger-git](https://aur.archlinux.org/packages/hledger-git/)

*   **Manager Accounting** — Manager is free accounting software for small business.

	[https://www.manager.io/](https://www.manager.io/) || [manager-accounting](https://aur.archlinux.org/packages/manager-accounting/)

*   **Money Manager EX** — An easy-to-use personal finance suite

	[https://www.moneymanagerex.org/](https://www.moneymanagerex.org/) || [moneymanagerex](https://www.archlinux.org/packages/?name=moneymanagerex)

*   **Skrooge** — Personal finances manager for the KDE desktop.

	[https://skrooge.org/](https://skrooge.org/) || [skrooge](https://www.archlinux.org/packages/?name=skrooge)

*   **[Odoo](/index.php/Odoo "Odoo")** — Open source ERP system purely in Python. Previously known as OpenERP.

	[https://www.odoo.com/](https://www.odoo.com/) || [odoo](https://aur.archlinux.org/packages/odoo/)

#### Cryptocurrency

*   **ARK Desktop Wallet** — Wallet for ARK.

	[https://github.com/ArkEcosystem/desktop-wallet](https://github.com/ArkEcosystem/desktop-wallet) || [ark-desktop](https://aur.archlinux.org/packages/ark-desktop/)

*   **Bitcoin Core** — Connect to the [Bitcoin](/index.php/Bitcoin "Bitcoin") P2P Network.

	[https://bitcoincore.org/](https://bitcoincore.org/) || [bitcoin-qt](https://www.archlinux.org/packages/?name=bitcoin-qt)

*   **Cointop** — Terminal based application for tracking cryptocurrencies.

	[https://cointop.sh/](https://cointop.sh/) || [cointop](https://aur.archlinux.org/packages/cointop/)

*   **Electrum** — Lightweight [Bitcoin](/index.php/Bitcoin "Bitcoin") client.

	[https://electrum.org/](https://electrum.org/) || [electrum](https://www.archlinux.org/packages/?name=electrum)

*   **Etherwall** — [Ethereum](/index.php/Ethereum "Ethereum") wallet.

	[https://www.etherwall.com/](https://www.etherwall.com/) || [etherwall](https://www.archlinux.org/packages/?name=etherwall)

*   **Exodus** — All-in-one proprietary application to secure, manage, and exchange blockchain assets. Based on the [Electron](https://electronjs.org/) platform.

	[https://www.exodus.io/](https://www.exodus.io/) || [exodus](https://aur.archlinux.org/packages/exodus/)

*   **Mist** — [Ethereum](/index.php/Ethereum "Ethereum") Dapp browser.

	[https://github.com/ethereum/mist](https://github.com/ethereum/mist) || [mist](https://aur.archlinux.org/packages/mist/)

#### Project management

See also [Wikipedia:Comparison of project management software](https://en.wikipedia.org/wiki/Comparison_of_project_management_software "wikipedia:Comparison of project management software").

*   **[Calligra Plan](https://en.wikipedia.org/wiki/Calligra_Plan "wikipedia:Calligra Plan")** — Project management application, which is intended for managing moderately large projects with multiple resources.

	[https://www.calligra.org/plan/](https://www.calligra.org/plan/) || [calligra-plan](https://www.archlinux.org/packages/?name=calligra-plan)

*   **[GanttProject](https://en.wikipedia.org/wiki/GanttProject "wikipedia:GanttProject")** — Project scheduling application featuring gantt chart, resource management, calendaring.

	[https://www.ganttproject.biz/](https://www.ganttproject.biz/) || [ganttproject](https://aur.archlinux.org/packages/ganttproject/)

*   **Planner** — Project management application for GNOME.

	[https://wiki.gnome.org/Apps/Planner](https://wiki.gnome.org/Apps/Planner) || [planner](https://aur.archlinux.org/packages/planner/)

*   **[ProjectLibre](https://en.wikipedia.org/wiki/ProjectLibre "wikipedia:ProjectLibre")** — Project management software alternative to [Microsoft Project](https://en.wikipedia.org/wiki/Microsoft_Project "wikipedia:Microsoft Project").

	[https://www.projectlibre.com/product/projectlibre-open-source](https://www.projectlibre.com/product/projectlibre-open-source) || [projectlibre](https://aur.archlinux.org/packages/projectlibre/)

*   **[TaskJuggler](https://en.wikipedia.org/wiki/TaskJuggler "wikipedia:TaskJuggler")** — Modern and powerful project management tool. Its new approach to project planning and tracking is more flexible and superior to the commonly used Gantt chart editing tools.

	[http://taskjuggler.org/](http://taskjuggler.org/) || [taskjuggler](https://aur.archlinux.org/packages/taskjuggler/)

#### Recipe management

*   **GNOME Recipes** — Recipe management application for GNOME.

	[https://wiki.gnome.org/Apps/Recipes](https://wiki.gnome.org/Apps/Recipes) || [gnome-recipes](https://www.archlinux.org/packages/?name=gnome-recipes)

*   **Gourmet** — Simple but powerful recipe-managing application.

	[http://thinkle.github.io/gourmet/](http://thinkle.github.io/gourmet/) || [gourmet](https://aur.archlinux.org/packages/gourmet/)

*   **KRecipes** — KDE application designed to make organizing your personal recipes collection fast and easy.

	[https://www.kde.org/applications/utilities/krecipes/](https://www.kde.org/applications/utilities/krecipes/) || [krecipes](https://aur.archlinux.org/packages/krecipes/)

### Education

See also [List of games#Education](/index.php/List_of_games#Education "List of games").

*   **[Moodle](/index.php/Moodle "Moodle")** — Open-source software learning management system.

	[https://moodle.org/](https://moodle.org/) || [moodle](https://aur.archlinux.org/packages/moodle/)

*   **[OpenBoard](https://en.wikipedia.org/wiki/OpenBoard "wikipedia:OpenBoard")** — Interactive whiteboard software for schools and universities.

	[http://openboard.ch/index.en.html](http://openboard.ch/index.en.html) || [openboard](https://aur.archlinux.org/packages/openboard/)

#### Flashcards

See also [Wikipedia:List of flashcard software](https://en.wikipedia.org/wiki/List_of_flashcard_software "wikipedia:List of flashcard software").

*   **[Anki](/index.php/Anki "Anki")** — Intelligent spaced-repetition memory training program.

	[https://apps.ankiweb.net/](https://apps.ankiweb.net/) || [anki](https://www.archlinux.org/packages/?name=anki)

*   **iGNUit** — Memorization aid based on the [Leitner flashcard system](https://en.wikipedia.org/wiki/Leitner_system "wikipedia:Leitner system").

	[http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit](http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit) || [ignuit](https://aur.archlinux.org/packages/ignuit/)

*   **jVLT** — Vocabulary learning tool.

	[https://www.linuxlinks.com/jVLT/](https://www.linuxlinks.com/jVLT/) || [jvlt](https://aur.archlinux.org/packages/jvlt/)

*   **KWordQuiz** — Tool that gives you a powerful way to master new vocabularies. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/kwordquiz/](https://www.kde.org/applications/education/kwordquiz/) || [kwordquiz](https://www.archlinux.org/packages/?name=kwordquiz)

*   **[Mnemosyne](/index.php/Mnemosyne "Mnemosyne")** — Flash-card tool which optimizes your learning process.

	[https://mnemosyne-proj.org/](https://mnemosyne-proj.org/) || [mnemosyne](https://aur.archlinux.org/packages/mnemosyne/)

*   **Parley** — Program to help you memorize things. It uses the spaced repetition learning method, also known as flash cards. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/parley/](https://www.kde.org/applications/education/parley/) || [parley](https://www.archlinux.org/packages/?name=parley)

*   **Pauker** — Flash card based learning tool using shortterm and longterm memory training.

	[http://pauker.sourceforge.net/](http://pauker.sourceforge.net/) || [pauker](https://aur.archlinux.org/packages/pauker/)

#### Touch typing

##### Console

*   **Dvorak 7min** — Simple ncurses-based typing tutor for those trying to become fluent with the Dvorak keyboard layout.

	[https://github.com/yaychris/dvorak7min](https://github.com/yaychris/dvorak7min) || [dvorak7min](https://aur.archlinux.org/packages/dvorak7min/)

*   **DvorakNG** — Dvorak typing tutor. It's heavily based on Dvorak7min, but adds many improvements.

	[https://gitlab.com/atsb/dvorakng](https://gitlab.com/atsb/dvorakng) || [dvorakng](https://aur.archlinux.org/packages/dvorakng/)

*   **GNU Typist** — Universal typing tutor.

	[https://www.gnu.org/software/gtypist/](https://www.gnu.org/software/gtypist/) || [gtypist](https://aur.archlinux.org/packages/gtypist/)

*   **psani-profi** — Program that will teach you touchtyping (Czech).

	[https://www.sallyx.org/sally/psani-vsemi-deseti/](https://www.sallyx.org/sally/psani-vsemi-deseti/) || [psani-profi](https://aur.archlinux.org/packages/psani-profi/)

*   **Typing Trainer** — ncurses-based typing trainer program that knows the English and Hungarian languages.

	[https://szit.hu/tpgt/](https://szit.hu/tpgt/) || [tpgt](https://aur.archlinux.org/packages/tpgt/)

*   **Typespeed** — Test your typing speed, and get your fingers' CPS.

	[http://typespeed.sourceforge.net/](http://typespeed.sourceforge.net/) || [typespeed](https://www.archlinux.org/packages/?name=typespeed)

##### Graphical

*   **Amphetype** — Layout-agnostic typing program aimed at people who don't need an on-screen keyboard, but would still like to improve their speed and accuracy.

	[https://code.google.com/p/amphetype/](https://code.google.com/p/amphetype/) || [amphetype-svn](https://aur.archlinux.org/packages/amphetype-svn/)

*   **Klavaro** — Teaching touch typing that intends to be keyboard and language independent.

	[https://klavaro.sourceforge.io/](https://klavaro.sourceforge.io/) || [klavaro](https://www.archlinux.org/packages/?name=klavaro)

*   **[KTouch](https://en.wikipedia.org/wiki/KTouch "wikipedia:KTouch")** — Program to learn and practice touch typing. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/ktouch/](https://www.kde.org/applications/education/ktouch/) || [ktouch](https://www.archlinux.org/packages/?name=ktouch)

*   **TIPP10** — Intelligent touch typing tutor.

	[https://www.tipp10.com/](https://www.tipp10.com/) || [tipp10](https://www.archlinux.org/packages/?name=tipp10)

*   **TypingTest** — Typing test desktop program with a large amount of customization.

	[https://github.com/laelath/typingtest](https://github.com/laelath/typingtest) || [typingtest-git](https://aur.archlinux.org/packages/typingtest-git/)

### Accessibility

See [Accessibility](/index.php/Accessibility "Accessibility") for tips on operating the desktop and [Category:Accessibility](/index.php/Category:Accessibility "Category:Accessibility") for all available articles. See also [On-screen keyboards](/index.php/List_of_applications/Utilities#On-screen_keyboards "List of applications/Utilities").

#### Speech synthesizers

See also [Wikipedia:Comparison of speech synthesizers](https://en.wikipedia.org/wiki/Comparison_of_speech_synthesizers "wikipedia:Comparison of speech synthesizers") and [listening comparison of the different engines](https://tools.wmflabs.org/tts-comparison/).

*   **Ekho** — Chinese text-to-speech (TTS) software for Cantonese, Mandarin, Zhaoan Hakka, Tibetan, Ngangien and Korean.

	[https://eguidedog.net/ekho.php](https://eguidedog.net/ekho.php) || [ekho](https://aur.archlinux.org/packages/ekho/)

*   **eSpeak** — Compact speech synthesizer for more than 50 languages.

	[http://espeak.sourceforge.net/](http://espeak.sourceforge.net/) || [espeak](https://www.archlinux.org/packages/?name=espeak)

*   **[eSpeak NG](https://en.wikipedia.org/wiki/eSpeakNG "wikipedia:eSpeakNG")** — Fork of eSpeak (due to inactivity of original maintainer).

	[https://github.com/espeak-ng/espeak-ng](https://github.com/espeak-ng/espeak-ng) || [espeak-ng](https://www.archlinux.org/packages/?name=espeak-ng)

*   **[Festival](/index.php/Festival "Festival")** — General framework for building speech synthesis systems as well as including examples of various modules. As a whole it offers full text to speech.

	[http://www.cstr.ed.ac.uk/projects/festival/](http://www.cstr.ed.ac.uk/projects/festival/) || [festival](https://www.archlinux.org/packages/?name=festival)

*   **Flite** — Lightweight speech synthesis engine.

	[http://festvox.org/flite/](http://festvox.org/flite/) || [flite](https://www.archlinux.org/packages/?name=flite)

*   **Gespeaker** — GTK frontend for espeak. It allows you to play a text in many languages with settings for voice, pitch, volume and speed.

	[https://muflone.com/jekyll/gespeaker/english/](https://muflone.com/jekyll/gespeaker/english/) || [gespeaker](https://aur.archlinux.org/packages/gespeaker/)

*   **KMouth** — Speech synthesizer frontend which enables persons that cannot speak to let their computer speak.

	[https://www.kde.org/applications/utilities/kmouth/](https://www.kde.org/applications/utilities/kmouth/) || [kmouth](https://www.archlinux.org/packages/?name=kmouth)

*   **MaryTTS** — Multilingual text-to-speech synthesis platform written in Java.

	[http://mary.dfki.de/](http://mary.dfki.de/) || [marytts](https://aur.archlinux.org/packages/marytts/)

*   **[MBROLA](/index.php/Mbrola "Mbrola")** — Proprietary phonemes-to-audio program which supports more than 70 languages. Mbrola-voices can also be used with eSpeak.

	[http://tcts.fpms.ac.be/synthesis/mbrola.html](http://tcts.fpms.ac.be/synthesis/mbrola.html) || [mbrola](https://aur.archlinux.org/packages/mbrola/)

*   **Mimic** — Text-to-speech voice synthesis from the Mycroft project (based on Flite).

	[https://mimic.mycroft.ai/](https://mimic.mycroft.ai/) || [mimic](https://aur.archlinux.org/packages/mimic/)

*   **Open JTalk** — Japanese text-to-speech synthesis system.

	[https://sourceforge.net/projects/open-jtalk/](https://sourceforge.net/projects/open-jtalk/) || [open-jtalk](https://aur.archlinux.org/packages/open-jtalk/)

*   **Orca** — Screen reader for individuals who are blind or visually impaired, using eSpeak (via Speech Dispatcher).

	[https://wiki.gnome.org/Projects/Orca](https://wiki.gnome.org/Projects/Orca) || [orca](https://www.archlinux.org/packages/?name=orca)

*   **[SOPS](/index.php/Simple_Orca_Plugin_System "Simple Orca Plugin System")** — Provides a simple way to write custom plugins for screen reader Orca.

	[https://stormdragon.tk/orca-plugins/index.php](https://stormdragon.tk/orca-plugins/index.php) || [simpleorcapluginsystem](https://aur.archlinux.org/packages/simpleorcapluginsystem/)

*   **Speech Dispatcher** — Common interface to speech synthesis. It has backends for eSpeak, Festival, and a few other speech synthesizers.

	[https://freebsoft.org/speechd](https://freebsoft.org/speechd) || [speech-dispatcher](https://www.archlinux.org/packages/?name=speech-dispatcher)

*   **SVOX Pico** — The text-to-speech engine used on Android phones. (Available languages are en-US, en-GB, de-DE, es-ES, fr-FR and it-IT)

	[https://android.googlesource.com/platform/external/svox/+/master](https://android.googlesource.com/platform/external/svox/+/master) || [svox-pico-bin](https://aur.archlinux.org/packages/svox-pico-bin/)

#### Speech recognition

See also [Wikipedia:Speech recognition software for Linux](https://en.wikipedia.org/wiki/Speech_recognition_software_for_Linux "wikipedia:Speech recognition software for Linux").

*   **Blather** — Speech recognizer that will run commands when a user speaks preset commands, uses PocketSphinx.

	[https://gitlab.com/jezra/blather](https://gitlab.com/jezra/blather) || [blather-git](https://aur.archlinux.org/packages/blather-git/)

*   **FreeSpeech** — Desktop application front-end for PocketSphinx dictation, voice transcription, and realtime speech recognition.

	[https://thenerdshow.com/freespeech.html](https://thenerdshow.com/freespeech.html) || [freespeech-vr](https://aur.archlinux.org/packages/freespeech-vr/)

*   **[Julius](https://en.wikipedia.org/wiki/Julius_(software) "wikipedia:Julius (software)")** — Large vocabulary continuous speech recognition engine.

	[https://github.com/julius-speech/julius](https://github.com/julius-speech/julius) || [julius](https://www.archlinux.org/packages/?name=julius)

*   **[Kaldi](https://en.wikipedia.org/wiki/Kaldi_(software) "wikipedia:Kaldi (software)")** — Speech recognition toolkit.

	[https://github.com/kaldi-asr/kaldi](https://github.com/kaldi-asr/kaldi) || [kaldi](https://aur.archlinux.org/packages/kaldi/)

*   **Kalliope** — Modular always-on voice controlled personal assistant designed for home automation.

	[https://kalliope-project.github.io/](https://kalliope-project.github.io/) || [kalliope](https://aur.archlinux.org/packages/kalliope/)

*   **Kaylee** — Somewhat fancy voice command recognition program that performs actions when a user speaks loosely preset sentences.

	[https://git.clayhobbs.com/clay/kaylee](https://git.clayhobbs.com/clay/kaylee) || [kayleevc](https://aur.archlinux.org/packages/kayleevc/)

*   **[Mycroft](https://en.wikipedia.org/wiki/Mycroft_(software) "wikipedia:Mycroft (software)")** — Hackable voice assistant.

	[https://github.com/MycroftAI/mycroft-core](https://github.com/MycroftAI/mycroft-core) || [mycroft-core](https://aur.archlinux.org/packages/mycroft-core/)

*   **Simon** — Speech recognition program that can replace your mouse and keyboard.

	[https://simon.kde.org/](https://simon.kde.org/) || [simon](https://aur.archlinux.org/packages/simon/)

#### Screen magnifiers

*   **KMag** — Small KDE utility to magnify a part of the screen.

	[https://www.kde.org/applications/utilities/kmag/](https://www.kde.org/applications/utilities/kmag/) || [kmag](https://www.archlinux.org/packages/?name=kmag)

*   **Virtual Magnifying Glass** — Simple, customizable and easy-to-use screen magnification tool.

	[http://magnifier.sourceforge.net/](http://magnifier.sourceforge.net/) || [vmg](https://aur.archlinux.org/packages/vmg/)

*   **xzoom** — Zoom, rotate and mirror area of X display.

	[https://www.ibiblio.org/pub/Linux/X11/libs/!INDEX.short.html](https://www.ibiblio.org/pub/Linux/X11/libs/!INDEX.short.html) || [xzoom](https://aur.archlinux.org/packages/xzoom/)

#### Mouse

*   **Easystroke** — Use mouse gestures to initiate commands and hotkeys.

	[https://github.com/thjaeger/easystroke/wiki](https://github.com/thjaeger/easystroke/wiki) || [easystroke](https://www.archlinux.org/packages/?name=easystroke)

*   **KMouseTool** — Clicks the mouse whenever the mouse cursor pauses briefly. It was designed to help those with repetitive strain injuries, for whom pressing buttons hurts.

	[https://userbase.kde.org/KMouseTool](https://userbase.kde.org/KMouseTool) || [kmousetool](https://www.archlinux.org/packages/?name=kmousetool)

*   **Mousetweaks** — Accessibility enhancements for pointing devices.

	[https://wiki.gnome.org/Projects/Mousetweaks](https://wiki.gnome.org/Projects/Mousetweaks) || [mousetweaks](https://www.archlinux.org/packages/?name=mousetweaks)

### Display managers

See the main article: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager").

### Desktop environments

See the main article: [Desktop environment#List of desktop environments](/index.php/Desktop_environment#List_of_desktop_environments "Desktop environment").

#### Window managers

##### Console

See also [List of applications/Utilities#Terminal multiplexers](/index.php/List_of_applications/Utilities#Terminal_multiplexers "List of applications/Utilities"), which offer some of the functions of window managers for the console.

*   **twin** — Text-mode window manager.

	[https://sourceforge.net/projects/twin/](https://sourceforge.net/projects/twin/) || [twin](https://www.archlinux.org/packages/?name=twin)

*   **Wmutils** — A set of tools for X windows manipulation.

	[https://github.com/wmutils/core](https://github.com/wmutils/core) || [wmutils-git](https://aur.archlinux.org/packages/wmutils-git/)

##### Graphical

See the main article: [Window manager#List of window managers](/index.php/Window_manager#List_of_window_managers "Window manager").

##### Composite managers

See the main article: [Xorg#List of composite managers](/index.php/Xorg#List_of_composite_managers "Xorg").

#### Window tilers

*   **PyWO** — Allows you to easily organize windows on the desktop using keyboard shortcuts.

	[https://code.google.com/archive/p/pywo/](https://code.google.com/archive/p/pywo/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **QuickTile** — Lightweight standalone alternative to Compiz Grid plugin.

	[http://ssokolow.com/quicktile/](http://ssokolow.com/quicktile/) || [quicktile-git](https://aur.archlinux.org/packages/quicktile-git/)

*   **wumwum** — The Window Manager manager. It can turn emwh compliant window managers into a tiling window manager while retaining all initial functionalities.

	[http://wumwum.sourceforge.net/](http://wumwum.sourceforge.net/) || [wumwum](https://aur.archlinux.org/packages/wumwum/)

#### Taskbars

See also [Wikipedia:Taskbar](https://en.wikipedia.org/wiki/Taskbar "wikipedia:Taskbar").

*   **[Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")** — Lightweight dock which sits at the bottom of the screen.

	[https://launchpad.net/awn](https://launchpad.net/awn) || [avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/)

*   **[Bmpanel](/index.php/Bmpanel "Bmpanel")** — Lightweight, NETWM compliant panel.

	[https://github.com/nsf/bmpanel2](https://github.com/nsf/bmpanel2) || [bmpanel2](https://aur.archlinux.org/packages/bmpanel2/)

*   **[Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock")** — Highly customizable dock and launcher application.

	[http://www.glx-dock.org/](http://www.glx-dock.org/) || [cairo-dock](https://www.archlinux.org/packages/?name=cairo-dock)

*   **[Docky](https://en.wikipedia.org/wiki/Docky "wikipedia:Docky")** — Full fledged dock application that makes opening common applications and managing windows easier and quicker.

	[http://www.go-docky.com/](http://www.go-docky.com/) || [docky](https://aur.archlinux.org/packages/docky/)

*   **[fbpanel](/index.php/Fbpanel "Fbpanel")** — Lightweight, NETWM compliant desktop panel.

	[https://aanatoly.github.io/fbpanel/](https://aanatoly.github.io/fbpanel/) || [fbpanel](https://aur.archlinux.org/packages/fbpanel/)

*   **[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")** — Panel included in the [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") desktop.

	[https://wiki.gnome.org/Projects/GnomePanel](https://wiki.gnome.org/Projects/GnomePanel) || [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)

*   **Latte** — Dock based on Plasma frameworks that provides an elegant and intuitive experience for your tasks and plasmoids.

	[https://github.com/psifidotos/Latte-Dock](https://github.com/psifidotos/Latte-Dock) || [latte-dock](https://www.archlinux.org/packages/?name=latte-dock)

*   **LXPanel** — Lightweight X11 desktop panel and part of the LXDE desktop.

	[http://lxde.org/lxpanel](http://lxde.org/lxpanel) || [lxpanel](https://www.archlinux.org/packages/?name=lxpanel)

*   **MATE Panel** — Panel included in the [MATE](/index.php/MATE "MATE") desktop.

	[https://github.com/mate-desktop/mate-panel/](https://github.com/mate-desktop/mate-panel/) || [mate-panel](https://www.archlinux.org/packages/?name=mate-panel)

*   **PerlPanel** — The ideal accompaniment to a light-weight Window Manager such as OpenBox, or a desktop-drawing program like iDesk.

	[http://savannah.nongnu.org/projects/perlpanel](http://savannah.nongnu.org/projects/perlpanel) || [perlpanel-git](https://aur.archlinux.org/packages/perlpanel-git/)

*   **[Plank](/index.php/Plank "Plank")** — Elegant, simple, clean dock from [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/plank](https://launchpad.net/plank) || [plank](https://www.archlinux.org/packages/?name=plank)

*   **[PyPanel](/index.php/PyPanel "PyPanel")** — Lightweight panel/taskbar written in Python and C.

	[http://pypanel.sourceforge.net/](http://pypanel.sourceforge.net/) || [pypanel](https://www.archlinux.org/packages/?name=pypanel)

*   **[Tint2](/index.php/Tint2 "Tint2")** — Simple panel/taskbar developed specifically for Openbox.

	[https://gitlab.com/o9000/tint2](https://gitlab.com/o9000/tint2) || [tint2](https://www.archlinux.org/packages/?name=tint2)

*   **Vala Panel** — Gtk3 panel for compositing window managers

	[https://github.com/rilian-la-te/vala-panel](https://github.com/rilian-la-te/vala-panel) || [vala-panel-git](https://aur.archlinux.org/packages/vala-panel-git/)

*   **Xfce Panel** — Panel included in the [Xfce](/index.php/Xfce "Xfce") desktop.

	[https://docs.xfce.org/xfce/xfce4-panel/start](https://docs.xfce.org/xfce/xfce4-panel/start) || [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)

*   **[xmobar](/index.php/Xmobar "Xmobar")** — A lightweight, text-based, status bar written in Haskell.

	[https://archives.haskell.org/projects.haskell.org/xmobar/](https://archives.haskell.org/projects.haskell.org/xmobar/) || [xmobar](https://www.archlinux.org/packages/?name=xmobar), [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/)

#### System tray

*   **AllTray** — Dock other applications into the system tray (notification area).

	[https://github.com/mbt/alltray](https://github.com/mbt/alltray) || [alltray](https://www.archlinux.org/packages/?name=alltray)

*   **Docker** — Docking application which acts as a system tray.

	[http://icculus.org/openbox/2/docker/](http://icculus.org/openbox/2/docker/) || [docker-tray](https://aur.archlinux.org/packages/docker-tray/)

*   **KDocker** — Dock any application in the system tray (notification area).

	[https://github.com/user-none/KDocker](https://github.com/user-none/KDocker) || [kdocker](https://aur.archlinux.org/packages/kdocker/)

*   **[Stalonetray](/index.php/Stalonetray "Stalonetray")** — Stand-alone freedesktop.org and KDE system tray (notification area) for [Xorg](/index.php/Xorg "Xorg"). It has full XEMBED support and minimal dependencies: an X11 lib only. Stalonetray works with virtually any EWMH-compliant window manager.

	[http://stalonetray.sourceforge.net/](http://stalonetray.sourceforge.net/) || [stalonetray](https://www.archlinux.org/packages/?name=stalonetray)

*   **Trayer** — Lightweight GTK-based system tray (notification area).

	[https://gna.org/projects/fvwm-crystal/](https://gna.org/projects/fvwm-crystal/) || [trayer](https://www.archlinux.org/packages/?name=trayer)

#### Application launchers

See also [Wikipedia:Comparison of desktop application launchers](https://en.wikipedia.org/wiki/Comparison_of_desktop_application_launchers "wikipedia:Comparison of desktop application launchers").

*   **Albert** — Sophisticated, plugin based standalone keyboard launcher.

	[https://github.com/manuelschneid3r/albert](https://github.com/manuelschneid3r/albert) || [albert](https://www.archlinux.org/packages/?name=albert)

*   **Application Finder** — Easy-to-use application launcher from Xfce.

	[https://docs.xfce.org/xfce/xfce4-appfinder/start](https://docs.xfce.org/xfce/xfce4-appfinder/start) || [xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder)

*   **Bashrun2** — Provides a different, barebones approach to a run dialog, using a specialized Bash session within a small xterm window.

	[http://henning-bekel.de/bashrun2/](http://henning-bekel.de/bashrun2/) || [bashrun2](https://aur.archlinux.org/packages/bashrun2/)

*   **[dmenu](/index.php/Dmenu "Dmenu")** — Fast and lightweight dynamic menu for X which is also useful as an application launcher.

	[https://tools.suckless.org/dmenu/](https://tools.suckless.org/dmenu/) || [dmenu](https://www.archlinux.org/packages/?name=dmenu)

*   **dmenu-extended** — Extension to *dmenu* for quickly opening files and folders.

	[https://github.com/markjones112358/dmenu-extended](https://github.com/markjones112358/dmenu-extended) || [dmenu-extended-git](https://aur.archlinux.org/packages/dmenu-extended-git/)

*   **dmenu-launch** — Simple *dmenu*-based application launcher. Launches binaries and XDG shortcuts.

	[https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch](https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch) || [dmenu-launch](https://aur.archlinux.org/packages/dmenu-launch/)

*   **dmenu2** — Fork of dmenu with many useful patches applied and additional options like screen select, dim or opacity change.

	[https://bitbucket.org/melek/dmenu2](https://bitbucket.org/melek/dmenu2) || [dmenu2](https://aur.archlinux.org/packages/dmenu2/)

*   **dswitcher** — *dmenu*-based window switcher that works regardless of workspace or minimization.

	[https://github.com/Antithesisx/dswitcher](https://github.com/Antithesisx/dswitcher) || [dswitcher-git](https://aur.archlinux.org/packages/dswitcher-git/)

*   **Fehlstart** — Small GTK-based application launcher.

	[https://gitlab.com/fehlstart/fehlstart](https://gitlab.com/fehlstart/fehlstart) || [fehlstart-git](https://aur.archlinux.org/packages/fehlstart-git/)

*   **[Gmrun](/index.php/Gmrun "Gmrun")** — Lightweight GTK-based application launcher, with the ability to run programs inside a terminal and other handy features.

	[https://sourceforge.net/projects/gmrun/](https://sourceforge.net/projects/gmrun/) || [gmrun](https://www.archlinux.org/packages/?name=gmrun)

*   **[GNOME Do](https://en.wikipedia.org/wiki/GNOME_Do with many plugins, originally developed for the GNOME desktop.

	[https://do.cooperteam.net/](https://do.cooperteam.net/) || [gnome-do](https://aur.archlinux.org/packages/gnome-do/)

*   **Gnome-Pie** — Circular application launcher (pie menu) for Linux. It is made of several pies, each consisting of multiple slices.

	[https://simmesimme.github.io/gnome-pie.html](https://simmesimme.github.io/gnome-pie.html) || [gnome-pie](https://www.archlinux.org/packages/?name=gnome-pie)

*   **j4-dmenu-desktop** — Very fast dmenu application launcher.

	[https://github.com/enkore/j4-dmenu-desktop](https://github.com/enkore/j4-dmenu-desktop) || [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/)

*   **higgins** — Desktop agnostic application launcher, file finder, calculator and more. Plugin based and freely and easily extendable via user-written plugins

	[https://github.com/kokoko3k/higgins](https://github.com/kokoko3k/higgins) || [higgins-git](https://aur.archlinux.org/packages/higgins-git/)

*   **Kupfer** — Convenient command and access tool for the GNOME desktop that can launch applications, open documents and access different types of objects and act on them.

	[https://kupferlauncher.github.io/](https://kupferlauncher.github.io/) || [kupfer](https://www.archlinux.org/packages/?name=kupfer)

*   **launch** — Simple command for launching applications from a terminal emulator.

	[https://github.com/silverhammermba/launch](https://github.com/silverhammermba/launch) || [launch-cmd](https://aur.archlinux.org/packages/launch-cmd/)

*   **[Launchy](https://en.wikipedia.org/wiki/Launchy "wikipedia:Launchy")** — Very popular cross-platform application launcher with a plugin-based system used to provide extra functionality.

	[http://www.launchy.net/](http://www.launchy.net/) || [launchy](https://www.archlinux.org/packages/?name=launchy)

*   **Lighthouse** — Simple scriptable popup dialog to run on X.

	[https://github.com/emgram769/lighthouse](https://github.com/emgram769/lighthouse) || [lighthouse-git](https://aur.archlinux.org/packages/lighthouse-git/)

*   **[rofi](/index.php/Rofi "Rofi")** — Popup window switcher roughly based on superswitcher, requiring only xlib and pango.

	[https://github.com/davatorium/rofi/](https://github.com/davatorium/rofi/) || [rofi](https://www.archlinux.org/packages/?name=rofi)

*   **slingshot** — Application launcher has a clear look, part of [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/slingshot](https://launchpad.net/slingshot) || [slingshot-launcher](https://aur.archlinux.org/packages/slingshot-launcher/)

*   **Runa** — Fast and light dmenu-driven desktop application launcher, suitable for use standalone, integrated into file manager context menus, or as an 'xdg-open' replacement. Favourite applications can also be configured.

	[http://appstogo.mcfadzean.org.uk/linux.html#runa](http://appstogo.mcfadzean.org.uk/linux.html#runa) || [runa](https://aur.archlinux.org/packages/runa/)

*   **Synapse** — Semantic launcher written in Vala that you can use to start applications as well as find and access relevant documents and files by making use of the Zeitgeist engine.

	[https://launchpad.net/synapse-project](https://launchpad.net/synapse-project) || [synapse](https://www.archlinux.org/packages/?name=synapse)

*   **Ulauncher** — Modern and shiny launcher that provides fuzzy search, extensions, and themes

	[https://ulauncher.io/](https://ulauncher.io/) || [ulauncher](https://aur.archlinux.org/packages/ulauncher/)

*   **Whippet** — Launcher and xdg-open replacement for control freaks. Opens files and URLs with applications associated by name and/or mimetype. Applications and associations may be customized using an SQLite database. Uses dmenu to manage its menus.

	[http://appstogo.mcfadzean.org.uk/linux.html#whippet](http://appstogo.mcfadzean.org.uk/linux.html#whippet) || [whippet](https://aur.archlinux.org/packages/whippet/)

#### Application menu editors

*   **[Alacarte](https://en.wikipedia.org/wiki/Alacarte "wikipedia:Alacarte")** — Add or remove applications from the main menu.

	[https://gitlab.gnome.org/GNOME/alacarte](https://gitlab.gnome.org/GNOME/alacarte) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

*   **AppEditor** — Edit application entries in the application menu.

	[https://github.com/donadigo/appeditor](https://github.com/donadigo/appeditor) || [appeditor-git](https://aur.archlinux.org/packages/appeditor-git/)

*   **Ezame** — Desktop and menu file editor.

	[https://github.com/linux-man/ezame](https://github.com/linux-man/ezame) || [ezame](https://aur.archlinux.org/packages/ezame/)

*   **KMenuEdit** — Edit one of the KDE application launchers.

	[https://docs.kde.org/trunk5/en/kde-workspace/kmenuedit/index.html](https://docs.kde.org/trunk5/en/kde-workspace/kmenuedit/index.html) || [kmenuedit](https://www.archlinux.org/packages/?name=kmenuedit)

*   **lxmed** — Application menu editor written in Java.

	[https://sourceforge.net/projects/lxmed/](https://sourceforge.net/projects/lxmed/) || [lxmed](https://aur.archlinux.org/packages/lxmed/)

*   **MenuLibre** — Advanced menu editor that provides modern features in a clean, easy-to-use interface.

	[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/)

*   **Meow** — Application menu editor written in Java.

	[https://pnmougel.github.io/meow/](https://pnmougel.github.io/meow/) || [meow-bin](https://aur.archlinux.org/packages/meow-bin/)

*   **Mozo** — Change which applications are shown on the main menu.

	[https://github.com/mate-desktop/mozo](https://github.com/mate-desktop/mozo) || [mozo](https://www.archlinux.org/packages/?name=mozo)

#### Wallpaper setters

See also [Wikipedia:Wallpaper (computing)](https://en.wikipedia.org/wiki/Wallpaper_(computing) "wikipedia:Wallpaper (computing)").

*   **bgs** — An extremely fast and small background setter for X based on imlib2.

	[https://github.com/Gottox/bgs/](https://github.com/Gottox/bgs/) || [bgs-git](https://aur.archlinux.org/packages/bgs-git/)

*   **esetroot** — Eterm's root background setter, packaged separately.

	[http://www.eterm.org/](http://www.eterm.org/) || [esetroot](https://aur.archlinux.org/packages/esetroot/)

*   **[feh](/index.php/Feh "Feh")** — A lightweight and powerful image viewer that can also be used to manage the desktop wallpaper.

	[https://feh.finalrewind.org/](https://feh.finalrewind.org/) || [feh](https://www.archlinux.org/packages/?name=feh)‎

*   **habak** — A background changing app.

	[https://fvwm-crystal.sourceforge.io/](https://fvwm-crystal.sourceforge.io/) || [habak](https://www.archlinux.org/packages/?name=habak)

*   **hsetroot** — A tool to create compose wallpapers.

	[https://packages.debian.org/sid/hsetroot](https://packages.debian.org/sid/hsetroot) || [hsetroot](https://www.archlinux.org/packages/?name=hsetroot)

*   **HydraPaper** — Gtk utility to set two different backgrounds for each monitor on GNOME.

	[https://gitlab.com/gabmus/hydrapaper](https://gitlab.com/gabmus/hydrapaper) || [hydrapaper-git](https://aur.archlinux.org/packages/hydrapaper-git/)

*   **LiveWallpaper** — Animated 3D wallpapers.

	[https://launchpad.net/livewallpaper](https://launchpad.net/livewallpaper) || [livewallpaper](https://www.archlinux.org/packages/?name=livewallpaper)

*   **[Nitrogen](/index.php/Nitrogen "Nitrogen")** — A fast and lightweight desktop background browser and setter for X windows.

	[http://projects.l3ib.org/nitrogen/](http://projects.l3ib.org/nitrogen/) || [nitrogen](https://www.archlinux.org/packages/?name=nitrogen)

*   **pybgsetter** — Multi-backend (hsetroot, Esetroot, habak, feh) to set desktop wallpaper.

	[https://bbs.archlinux.org/viewtopic.php?id=88997](https://bbs.archlinux.org/viewtopic.php?id=88997) || [pybgsetter](https://aur.archlinux.org/packages/pybgsetter/)

*   **pywal** — Changes the wallpaper and creates matching colorschemes for various applications (rofi, i3, terminals)

	[https://github.com/dylanaraps/pywal](https://github.com/dylanaraps/pywal) || [python-pywal](https://www.archlinux.org/packages/?name=python-pywal)

*   **Variety** — Changes the wallpaper on a regular interval using user-specified or automatically downloaded images.

	[https://peterlevi.com/variety/](https://peterlevi.com/variety/) || [variety](https://www.archlinux.org/packages/?name=variety)

*   **xli** — An image display program for X.

	[https://packages.debian.org/sid/xli](https://packages.debian.org/sid/xli) || [xli](https://aur.archlinux.org/packages/xli/)

**Tip:** In order to avoid installing one more package, you may find convenient to use the `display` utility from [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) or `gm display` from [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick). E.g.: `display -backdrop -background '#3f3f3f' -flatten -window root *image*`.

#### Virtual desktop pagers

See also [Wikipedia:Pager (GUI)](https://en.wikipedia.org/wiki/Pager_(GUI) "wikipedia:Pager (GUI)").

*   **bbpager** — Dockable pager for [blackbox](/index.php/Blackbox "Blackbox") and other window managers.

	[http://bbtools.sourceforge.net/download.php?file=6](http://bbtools.sourceforge.net/download.php?file=6) || [bbpager](https://www.archlinux.org/packages/?name=bbpager)

*   **fbpager** — Virtual desktop pager for fluxbox.

	[http://www.fluxbox.org/fbpager](http://www.fluxbox.org/fbpager) || [fbpager-git](https://aur.archlinux.org/packages/fbpager-git/)

*   **IPager** — A configurable pager with transparency, originally developed for Fluxbox.

	[http://useperl.ru/ipager/index.en.html](http://useperl.ru/ipager/index.en.html) || [ipager](https://aur.archlinux.org/packages/ipager/)

*   **Neap** — An non-intrusive and light pager that runs in the notification area of your panel.

	[https://github.com/vzxwco/neap](https://github.com/vzxwco/neap) || [neap-hotkey](https://aur.archlinux.org/packages/neap-hotkey/)

*   **Netwmpager** — A NetWM/EWMH compatible pager.

	[https://sourceforge.net/projects/sf-xpaint/files/netwmpager/](https://sourceforge.net/projects/sf-xpaint/files/netwmpager/) || [netwmpager](https://aur.archlinux.org/packages/netwmpager/)

#### Desktop widgets

*   **[gDesklets](https://en.wikipedia.org/wiki/gDesklets "wikipedia:gDesklets")** — System for bringing mini programs (desklets) onto your desktop.

	[https://launchpad.net/gdesklets](https://launchpad.net/gdesklets) || [gdesklets](https://aur.archlinux.org/packages/gdesklets/)

*   **GPhotoFrame** — Photo frame gadget for the GNOME Desktop.

	[https://github.com/iblis17/gphotoframe](https://github.com/iblis17/gphotoframe) || [gphotoframe](https://aur.archlinux.org/packages/gphotoframe/)

*   **KRuler** — Displays on screen a ruler measuring pixels. Part of [kdegraphics](https://www.archlinux.org/groups/x86_64/kdegraphics/).

	[https://www.kde.org/applications/graphics/kruler/](https://www.kde.org/applications/graphics/kruler/) || [kruler](https://www.archlinux.org/packages/?name=kruler)

*   **[Screenlets](https://en.wikipedia.org/wiki/Screenlets "wikipedia:Screenlets")** — Widget framework that consists of small owner-drawn applications.

	[https://launchpad.net/screenlets](https://launchpad.net/screenlets) || [screenlets-pack-basic](https://aur.archlinux.org/packages/screenlets-pack-basic/)

#### Desktop notifications

See: [Notification servers](/index.php/Desktop_notifications#Notification_servers "Desktop notifications").

#### Clipboard managers

See [Clipboard#Managers](/index.php/Clipboard#Managers "Clipboard").

#### Logout UI

*   **clearine** — Beautiful Logout UI for X11 window manager

	[https://github.com/okitavera/clearine](https://github.com/okitavera/clearine) || [clearine-git](https://aur.archlinux.org/packages/clearine-git/)

*   **[oblogout](/index.php/Oblogout "Oblogout")** — Openbox logout script

	[https://launchpad.net/oblogout](https://launchpad.net/oblogout) || [oblogout](https://www.archlinux.org/packages/?name=oblogout)

## See also

**Generic software lists**

*   [Wikipedia:Portal:Free and open-source software](https://en.wikipedia.org/wiki/Portal:Free_and_open-source_software "wikipedia:Portal:Free and open-source software")
*   [Wikipedia:List of free and open-source software packages](https://en.wikipedia.org/wiki/List_of_free_and_open-source_software_packages "wikipedia:List of free and open-source software packages")
*   [Wikipedia:List of GNU packages](https://en.wikipedia.org/wiki/List_of_GNU_packages "wikipedia:List of GNU packages")
*   [AlternativeTo](https://alternativeto.net/platform/linux/) - Linux alternatives to popular applications
*   [Awesome Linux Software](https://github.com/luong-komorebi/Awesome-Linux-Software) - Collection of Linux applications and tools
*   [Linux Alternative Project](http://www.linuxalt.com/) - Linux equivalents to Windows software
*   [Linux App Finder](https://linuxappfinder.com/all) - Linux applications directory
*   [Linux Links Directory](https://www.linuxlinks.com/links/Software/) - Linux applications directory
*   [Open Source Alternative](https://www.osalt.com/) - Alternatives to commercial software

**Software lists of other distributions**

*   [AppImageHub](https://appimage.github.io/)
*   [Flathub](https://flathub.org/)
*   [Snapcraft](https://snapcraft.io/)
*   [Debian packages](https://packages.debian.org) and [screenshots](https://screenshots.debian.net)
*   [Fedora packages](https://apps.fedoraproject.org/packages/)
*   [Gentoo packages](https://packages.gentoo.org/)
*   [Ubuntu packages](https://packages.ubuntu.com/)

**Software [forges](https://en.wikipedia.org/wiki/Forge_(software) "wikipedia:Forge (software)")**

*   [GitHub](https://github.com/explore)
*   [GitLab](https://gitlab.com/explore)
*   [Launchpad](https://launchpad.net/)
*   [SourceForge](https://sourceforge.net/)

**Specialized software lists**

*   [GNOME applications](https://wiki.gnome.org/Apps)
*   [KDE's Applications](https://kde.org/applications/)
*   [awesome-linuxaudio](https://github.com/nodiscc/awesome-linuxaudio) - Software for audio/video/live production
*   [awesome-selfhosted](https://github.com/Kickball/awesome-selfhosted) - Network services and web applications
*   [awesome-shell](https://github.com/alebcay/awesome-shell) - Command-line frameworks, toolkits and guides
*   [awesome-sysadmin](https://github.com/n1trux/awesome-sysadmin) - Software for system administrators
*   [Inconsolation](https://inconsolation.wordpress.com/index/) - Lightweight and minimalist applications reviews
*   [K.Mandla's blog](https://kmandla.wordpress.com/software/) - Console applications screenshots and reviews
*   [Libre Projects](https://libreprojects.net/) - Open source hosted web services
*   [LinApp](http://lin-app.com/) - Commercial applications and games for Linux
*   [PRISM Break](https://prism-break.org/en/all/) - Software against mass surveillance
*   [Privacy Tools](https://www.privacytools.io/) - Knowledge and tools to protect your privacy against global mass surveillance

**Arch Linux forum threads**

*   [Arch Linux Forums / LnF Awards 2011](https://bbs.archlinux.org/viewtopic.php?id=111878) - The best Light & Fast apps of 2011
*   [Arch Linux Forums / LnF Awards 2012](https://bbs.archlinux.org/viewtopic.php?id=138281) - The best Light & Fast apps of 2012
*   [Arch Linux Forums / most popular apps of 2013-2014](https://bbs.archlinux.org/viewtopic.php?id=174764)
*   [Arch Linux Forums / most popular apps of 2017+](https://bbs.archlinux.org/viewtopic.php?pid=1702332) (requires login)