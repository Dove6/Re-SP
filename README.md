# Re:SP
![Re:SP banner](https://i.imgur.com/sVBS6AO.png)

Starting from the very beginning of the game series, this project targets porting *Reksio i Skarb Piratów* to the most recent version of its 2D engine available: BlooMoo Engine 1.0.8 developed by Aidem Media in 2006. Despite being 14 years old, it should operate way better than its predecessor PiKlib8 (used in the latest official release of the game), not to mention other benefits of unifying all games providing one common exe/dll pair.

Aside from that main task, the repository also provides fixes to various in-game bugs, e.g. missing animations, illogical event sequences and more.

## Download
Soon here: [releases](https://github.com/Dove6/Re-SP/releases)  
Note that the game engine is Windows-only and 32-bit (x86 arch).

## Changelog

### Changes to the scenes
* **MENUGLOWNE** *\[Dane/Intro/MainMenu/menu/MENUGLOWNE.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: variable storing Rex's "position" a.k.a. current scene (POZYCJAREKSIA) was never set to ID of the main menu (100);  
    fixed by adding `POZYCJAREKSIA^SET(100);` inside BEHMAIN procedure
  * cleanup: removed unnecessary comments and leftover code from the script
* **INTRO1** *\[Dane/Intro/MainMenu/intro/intro1/INTRO1.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements
* **INTRO2** *\[Dane/Intro/MainMenu/intro/intro2/INTRO2.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements
* **INTRO3** *\[Dane/Intro/MainMenu/intro/intro3/INTRO3.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements
* **NAWRAKU** *\[Dane/Intro/MainMenu/01nawraku/NAWRAKU.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * cleanup: removed unnecessary comments and leftover code from the script
* **LATAWIEC** *\[Dane/Intro/MainMenu/02latawiec/LATAWIEC.cnv]*  
  *nothing done*
* **3NAWRAKU** *\[Dane/Intro/MainMenu/03nawraku/3NAWRAKU.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * cleanup: removed unnecessary comments and leftover code from the script
* **4PLAZA** *\[Dane/Intro/MainMenu/04plaza/4PLAZA.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: the key to the jungle wasn't disappearing from the inventory after being used;  
    fixed by placing `BKLUCZ_BUTTON^DISABLE();` in `REKSIO:ONFINISHED^DRZWIOTWIERA` callback, removing a typo in ``BKLUCZ_BUTTON:ONINIT and adjusting BKLUCZ_BUTTON behavior in newly introduced BEH_REKSIODODRZWI_ALT procedure,
  * bug: episode progress was being resetted in the event of not passing the ~~vibe~~ game genuineness check;  
    fixed by executing `ROZDZIAL2^RESETINI();` (which restores default values of the saved variables of the second episode) only if the check has been passed before,
  * bug: clicking on the blank map button didn't have any effect;  
    fixed by placing a missing closing bracket back in `4BMAPA:ONFINISHED` callback,
  * cleanup: removed unnecessary comments and leftover code from the script
* **5ROBINSON** *\[Dane/Intro/MainMenu/05robinson/5ROBINSON.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: geese were standing still after being caught (on scene re-entry);  
    fixed by adding `GESZAGx^PLAY("GESx");` in conditionals in `GESZAGx:ONINIT` callbacks (where x stands for numbers 1-6),
  * bug: Robinson's farewell was always interrupted by leaving the scene;  
    fixed by moving `RATUNEK^GOTO("4PLAZA");` (which is switching the current scene) from `REKSIO:ONFINISHED^DOPLANSZY4` to `ROBSEQ:ONFINISHED^PAPA` and thus postponing leaving the scene until the goat is finished talking,
  * bug: Robinson was saying goodbye to Rex everytime the player was leaving the scene;  
    fixed by introducing a condition of finishing both of tasks assigned by Robinson (catching his geese and igniting the campfire) before playing the farewell,
  * feature: introduced an additional hindrance during the geese catching minigame: a black hen randomly appearing among the geese (by adding `KURYSEQ^PLAY("RANDOM");` in BEH_STARTGESI procedure code),
  * cleanup: removed unnecessary comments and leftover code from the script
* **MAPA** *\[Dane/Intro/MainMenu/06mapa/MAPA.cnv]*  
  * porting: replaced some CONDITION objects with @IF conditional statements
* **KONTROLA** *\[Dane/Intro/MainMenu/kontrola/KONTROLA.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * cleanup: removed unnecessary comments and leftover code from the script
* **RZEKA1** *\[Dane/Intro/MainMenu/07rzekaA/RZEKA1.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements
* **RZEKA2** *\[Dane/Intro/MainMenu/08rzekaB/RZEKA2.cnv]*  
  *nothing done*
* **RZEKA3** *\[Dane/Intro/MainMenu/09rzekaC/RZEKA3.cnv]*  
  *nothing done*
* **CUTSTATEK0** *\[Dane/Intro/MainMenu/atakpiratow/statek0/CUTSTATEK0.cnv]*  
  *nothing done*
* **CUTSTATEK1** *\[Dane/Intro/MainMenu/atakpiratow/statek1/CUTSTATEK1.cnv]*  
  *nothing done*
* **CUTSTATEK2** *\[Dane/Intro/MainMenu/atakpiratow/statek2/CUTSTATEK2.cnv]*  
  *nothing done*
* **CUTSTATEK3** *\[Dane/Intro/MainMenu/atakpiratow/statek3/CUTSTATEK3.cnv]*  
  *nothing done*
* **CUTSTATEK4** *\[Dane/Intro/MainMenu/atakpiratow/statek4/CUTSTATEK4.cnv]*  
  *nothing done*
* **CUTSTATEK5** *\[Dane/Intro/MainMenu/atakpiratow/statek5/CUTSTATEK5.cnv]*  
  *nothing done*
* **WIOSKA10** *\[Dane/Intro/MainMenu/10wioska/WIOSKA10.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: an ominous battle music and pirates' background shouts were silenced after re-entering the scene before passing the palisade minigame;  
    fixed by making the conditionals responsible for playing the sounds depend on VARZALICZONAPALISADA (variable storing minigame progress),
  * bug: after completing the episode and attempting to replay it, value of CZYKURCZAKA variable (storing the state of map translation) could remain not resetted
    fixed by resetting it on every scene enter with the palisade minigame not passed,
  * feature: made unneeded buttons disappear accordingly to the plot progress,
  * bug: after the first talk with Kurczaka, he became peaceful and spoke some unrelated phrases;  
    fixed by making his on-click speaking sequences dependent on VARZALICZONAPALISADA state
  * bug: singing hens remained with their beaks open after the end of singing animation;  
    fixed by editing their animation files with the irreplaceable [Anndrzem](https://github.com/mysliwy112/AM-transcoder) and adding `ONFINISHED^PLAY` callback for each one in the script,
  * bug: after completing the episode and attempting to replay it, value of VARROZMSTRURWISKA variable (storing the state of the conduct pass quest introduction dialogue) could remain not resetted
    fixed by resetting it just after the map translation,
  * feature: readded spoken description for the conduct pass and pearls buttons
* **PALISADA13** *\[Dane/Intro/MainMenu/13Palisada/PALISADA13.cnv]*  
  * porting: replaced some CONDITION objects with @IF conditional statements,
  * porting: replaced all ONCOLLISION callbacks with a self-made AABB collision checker,
  * porting: replaced all the EXPRESSION objects with bracket-enclosed in-line expressions,
  * bug: the coconut buttons could become enabled even after the finishing sequence (whether on win or on lose) has been started;  
    fixed by introducing a conditional statement in `ANIMOKOKOSx:ONFINISHED^PEKA` callback enabling the buttons only if the minigame state is not decided yet
  * bug: pirates' animations during the finishing sequence played after losing the minigame seemed to run too quickly;  
    fixed by adjusting FPS count of the animations (ANIMOSZCZUR, ANIMOSZCZUR1 and ANIMOSZCZUR2),
  * bug: sometimes on of the animations of black hens cheering would become stuck on some frame and remain unhidden if interrupted by another one of them
    fixed by adding ONSTARTED callback for each animation that hides all the others
  * cleanup: removed unnecessary comments and leftover code from the script
* **KRETSIAKAPIE** *\[Dane/Intro/MainMenu/kretsiakapie/KRETSIAKAPIE.cnv]*  
  * feature: added sound of hens singing in the background after the completion of the related quest
* **KROLEWNA11** *\[Dane/Intro/MainMenu/11Krolewna/KROLEWNA11.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: map unrolling animation was never played;  
    fixed by removing `RATUNEK^GOTO("MAPAPELNA");` (scene changing procedure call) from `BUTTONMAPA:ONACTION` (on-click callback of the map button),
  * feature: readded spoken description for the conduct pass button,
  * cleanup: removed unnecessary comments and leftover code from the script
* **URWISKO12** *\[Dane/Intro/MainMenu/12urwisko/URWISKO12.cnv]*
  * bug: the bridgekeeper sprite could duplicate;  
    fixed by merging two animation files into one
  * bug: one of the bridgekeeper's utterances wasn't animated;  
    fixed by editing the SEQ file associated with the animation
  * feature: restored the narrator's sequence played after failure in the pearl diving minigame
  * feature: readded spoken description for the pearls buttons
* **TRAMPOLINA** *\[Dane/Intro/MainMenu/trampolina/TRAMPOLINA.cnv]*  
  *nothing done*
* **14PERLY** *\[Dane/Intro/MainMenu/14perly/14PERLY.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * porting: replaced all ONCOLLISION callbacks with checks based on ISNEAR method of ANIMO class,
  * feature: readded the narrator's recordings played after succeeding or failing in the minigame,
  * cleanup: removed unnecessary comments and leftover code from the script
* **15POSAG** *\[Dane/Intro/MainMenu/15posag/15POSAG.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * feature: restored Rex's animation played after giving a wrong answer,
  * feature: rearranged the finishing animation sequence for it to feel more natural,
  * cleanup: removed unnecessary comments and leftover code from the script
* **15BWTWAROGU** *\[Dane/Intro/MainMenu/15bwtwarogu/15BWTWAROGU.cnv]*  
  *nothing done*
* **16BLAWA** *\[Dane/Intro/MainMenu/16blawa/16BLAWA.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: both the maps used to show Rex's position wrongly;  
    fixed by setting variables responsible for holding current Rex's map position (POZYCJAREKSIA, POZYCJAWULKAN) to appropriate values 
* **CIEMNOSC** *\[Dane/Intro/MainMenu/17ciemnosc/CIEMNOSC.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * feature: added a different entrance behavior when entering the scene from the menu or the maps
  * feature: enhanced the torch light behavior (made it stick to the torch if it is not holded by Rex),
  * feature: enhanced animation sequences when switching to/ going back from LAWAA scene
* **LAWAA** *\[Dane/Intro/MainMenu/lawaA/LAWAA.cnv]*  
  * porting: replaced some CONDITION objects with @IF conditional statements,
  * feature: removed the underground map (un)rolling animation
* **LAWAB** *\[Dane/Intro/MainMenu/lawaB/LAWAB.cnv]*  
  *nothing done*
* **LAWAC** *\[Dane/Intro/MainMenu/lawaC/LAWAC.cnv]*  
  *nothing done*
* **21MOST** *\[Dane/Intro/MainMenu/21Most/21MOST.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * porting: replaced all ONCOLLISION callbacks with checks based on ISNEAR method of ANIMO class,
  * feature: removed the underground map (un)rolling animation
* **ZAWAL** *\[Dane/Intro/MainMenu/22Zawal/ZAWAL.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * feature: removed the underground map (un)rolling animation
* **DOUFO** *\[Dane/Intro/MainMenu/Doufo/DOUFO.cnv]*  
  *nothing done*
* **UFO** *\[Dane/Intro/MainMenu/23Wufo/UFO.cnv]*  
  *nothing done*
* **24LASER** *\[Dane/Intro/MainMenu/24laser/24LASER.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * porting: replaced ONFOCUSON/ONFOCUSOFF callbacks with a conditional statement retrieving the mouse position,
  * bug: clicking on the buttons under the laser control screen had effect even with the power cord unplugged;  
    fixed by adding conditional statements inside the buttons ONACTION callbacks,
  * cleanup: removed unnecessary comments and leftover code from the script
* **POUFO** *\[Dane/Intro/MainMenu/22BPoUfo/POUFO.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * feature: removed the underground map (un)rolling animation
* **25PAPUGI** *\[Dane/Intro/MainMenu/25Papugi/25PAPUGI.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: after entering the scene, buttons could remain disabled;  
    fixed by running the button enabling procedure after entering the scene,
  * bug: after entering the scene, a bizarre sound could be heard;  
    fixed by using SETFRAME method instead of PLAY/PAUSE pair in the lift animation ONINIT callback,
  * feature: readded the map (un)rolling animation,
  * feature: added a spoken description for the map button being disabled
* **26SKARB** *\[Dane/Intro/MainMenu/26skarb/26SKARB.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: after finding the treasure it was still possible to enable the treasure chests buttons and "restart" the minigame;  
    fixed by introducing a conditional statement in the button enabling procedure
  * feature: made the episode button from the menu lead to this scene after visiting it (instead of going back to 25PAPUGI)
* **25B** *\[Dane/Intro/MainMenu/25b/25B.cnv]*  
  * bug: the lift animation was partially covering the black bars;  
    fixed by embedding the black bars into start.ann animation and placing it on top of the scene (OZ axis)
* **27STATEK** *\[Dane/Intro/MainMenu/27statek/27STATEK.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * feature: made entering the scene reset the save state variables of the previous episode
* **28ZUKI** *\[Dane/Intro/MainMenu/28zuki/28ZUKI.cnv]*  
  * porting: replaced all the CONDITION objects with @IF conditional statements,
  * bug: an infinite loop could prevent final sequence from proceeding (after the beetles have reached their destination);  
    fixed by pausing the beetles animation on sequence start and thus preventing any further calls of the sequence PLAY method
  * feature: add a sound effect for the seagull,
  * cleanup: removed unnecessary comments and leftover code from the script
* **27BSTATEK** *\[Dane/Intro/MainMenu/27bstatek/27BSTATEK.cnv]*  
  *nothing done*
* **OUTRO_1** *\[Dane/Intro/MainMenu/OUTRO/outro1/OUTRO_1.cnv]*  
  *nothing done*
* **OUTRO_2** *\[Dane/Intro/MainMenu/OUTRO/outro2/OUTRO_2.cnv]*  
  *nothing done*
* **OUTRO_3** *\[Dane/Intro/MainMenu/OUTRO/outro3/OUTRO_3.cnv]*  
  *nothing done*
* **OUTRO_4** *\[Dane/Intro/MainMenu/OUTRO/outro4/OUTRO_4.cnv]*  
  *nothing done*
* **OUTRO_5** *\[Dane/Intro/MainMenu/OUTRO/outro5/OUTRO_5.cnv]*  
  *nothing done*
* **OUTRO_6** *\[Dane/Intro/MainMenu/OUTRO/outro6/OUTRO_6.cnv]*  
  *nothing done*
* **OUTRO_7** *\[Dane/Intro/MainMenu/OUTRO/outro7/OUTRO_7.cnv]*  
  *nothing done*
* **OUTRO_8** *\[Dane/Intro/MainMenu/OUTRO/outro8/OUTRO_8.cnv]*  
  *nothing done*
* **MAPAPUSTA** *\[Dane/Intro/MainMenu/popupmapa/pustakartka/MAPAPUSTA.cnv]*  
  *nothing done*
* **MAPAPELNA** *\[Dane/Intro/MainMenu/popupmapa/pelnamapa/MAPAPELNA.cnv]*  
  * porting: replaced the CONDITION object with @IF conditional statements
* **MAPAPODZIEMI** *\[Dane/Intro/MainMenu/popupmapa/mapapodziemi/MAPAPODZIEMI.cnv]*  
  *nothing done*
* **POKONTROLI** *\[Dane/Intro/MainMenu/pokontroli/POKONTROLI.cnv]*  
  *nothing done*
* **CREDITS** *\[Dane/Intro/MainMenu/credits/CREDITS.cnv]*  
  *nothing done*
* **OFERTA** *\[Dane/Intro/MainMenu/oferta/OFERTA.cnv]*  
  *nothing done*

### Other changes
* adjusted game window sizes (in the windowed mode) removing blank space and the debug menu

[The commit messages](https://github.com/Dove6/Re-SP/commits/master) should be helpful as well.

## Licensing
* game binaries, scripts, other resources and all references to them are licensed under [non-permissive proprietary license](Licencja.txt)
* all the changes and fixes are licensed under [MIT license](LICENSE)
