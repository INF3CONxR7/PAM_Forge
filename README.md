<p align="center">
  <img src="https://zupimages.net/up/26/46/h7ka.png" alt="Logo de PAM Forge" width="128">
</p>

<h1 align="center">PAM Forge</h1>

<p align="center">
  Fabriquez l’<b>icône animée ICON1.PAM</b> d’un jeu PS3 à partir de n’importe quelle vidéo :<br>découpe en boucle,
  conversion <b>H.264 Main@2.1 en 320 × 176</b> emballée en <b>PAMF</b>, musique <b>SND0.AT3</b>, icône fixe
  <b>ICON0.PNG</b>, vérifications et envoi à la console.
</p>

<p align="center">
  <a href="https://github.com/INF3CONxR7/PAM_Forge/releases/latest"><img src="https://img.shields.io/github/v/release/INF3CONxR7/PAM_Forge?label=t%C3%A9l%C3%A9charger&color=5B9DFF" alt="Télécharger"></a>
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-0078D6?logo=windows&logoColor=white" alt="Windows 10 et 11">
  <a href="https://discord.gg/TbFYvqsh5z"><img src="https://img.shields.io/badge/Discord-rejoindre-5865F2?logo=discord&logoColor=white" alt="Serveur Discord"></a>
</p>

---

## Sommaire

- [Fonctionnalités](#fonctionnalités)
- [Installation](#installation)
- [Outils de conversion](#outils-de-conversion)
- [Utilisation](#utilisation)
- [Raccourcis clavier](#raccourcis-clavier)
- [Mises à jour et Discord](#mises-à-jour-et-discord)
- [En cas de problème](#en-cas-de-problème)
- [Désinstaller](#désinstaller)
- [Crédits](#crédits)
- [English](#english)

## Fonctionnalités

- **Lire, découper et convertir** : aperçu de la source avec le **cadre de sortie 20:11** (320 × 176 n’est pas du
  16:9 : PAM Forge rogne 12 px en haut et en bas d’une vidéo 1080p), aperçu de l’icône telle qu’elle sortira et vue
  côte à côte ; lecture à l’image près, en boucle, avec le son.

- **Découpe** : entrée et sortie au code temporel ou à la souris, poignées sur la frise, images clés prévues (une
  toutes les 12 images) et **raccord de la boucle** en fondu enchaîné de 0,5 s.

- **La recette éprouvée** : H.264 profil Main, niveau 2.1, CAVLC, 29,97 i/s, une image clé toutes les 12 images,
  délimiteurs d’image, encodage en 2 passes, par **FFmpeg (x264)** ; emballage **PAMF** avec sa table des points
  d’entrée par **PAMFtool**.

- **Budget du menu** : ICON1.PAM + SND0.AT3 ≤ 2 400 000 octets, estimé en direct ; le préréglage recommandé calcule
  le débit (formule du guide, 10 % de marge).

- **Musique SND0.AT3** : coupe (55 s au plus), fondu final, ATRAC3 132 kbit/s stéréo à 48 kHz, par atracdenc (libre,
  avec l’astuce 48 kHz de pop-fe) ou at3tool ; écoute et forme d’onde.

- **Images fixes** : ICON0.PNG tiré de l’image affichée (ou d’un fichier), PIC1.PNG facultatif.

- **Lire le .pam et le vérifier** : en-tête PAMF0040/0041, taille en secteurs de 2 048 octets, vidéo Main@L2.1 en
  320 × 176 CAVLC, table EP map, nom exact et budget ; lecture en boucle avec la musique de SND0.AT3.

- **Envoyer à la PS3** : par le FTP de webMAN MOD (HEN ou CFW), dans le dossier du jeu à côté de son PARAM.SFO,
  avec **sauvegarde préalable des fichiers d’origine** ; ou **essai dans RPCS3**.

- Interface en français ou en anglais, trois thèmes, mises à jour signées, activité Discord.

## Installation

1. Téléchargez `PAMForge-win-x64.zip` dans la [dernière version](https://github.com/INF3CONxR7/PAM_Forge/releases/latest).

2. Décompressez-le dans un dossier à vous (par exemple `Documents\PAM Forge`), puis lancez `PAM Forge.exe`.
   Le runtime .NET et les outils de conversion sont inclus : **rien d’autre à installer**.

Le dossier obtenu contient `PAM Forge.exe`, le dossier `Update` (programme de mise à jour) et le dossier `Tools`
(outils de conversion) : gardez-les ensemble.

## Outils de conversion

PAM Forge pilote des programmes libres, **fournis** dans son dossier **`Tools`** et trouvés sans aucun réglage :

| Outil | Rôle | Dans le paquet |
|---|---|---|
| **FFmpeg** (GPL-3.0, avec x264) | Lecture, découpe, encodage H.264 (libx264) | `Tools\ffmpeg` : `ffmpeg.exe`, `ffprobe.exe` et leurs bibliothèques |
| **PAMFtool** (ravenDS, GPL-3.0) | Emballage PAMF de l’ICON1.PAM | `Tools\PAMFtool\PAMFtool.exe`, autonome (.NET 8 inclus) |
| **atracdenc** (LGPL-2.1) | SND0.AT3 (musique, facultative) | `Tools\atracdenc\atracdenc.exe` |
| **RPCS3** | Aperçu au survol (facultatif) | Non fourni : [rpcs3.net](https://rpcs3.net) |

Chaque outil garde sa propre licence, jointe dans son dossier ; `Tools\LICENCES.txt` donne les versions, les licences
et les adresses de leur code source. Vous pouvez en utiliser une autre version : indiquez-la dans
*Aide > Paramètres > Outils*, ou remplacez ses fichiers dans `Tools`.

at3tool (Sony) n’est pas fourni : il n’est pas redistribuable, et atracdenc le remplace. Les outils fuités du SDK de
Sony (PS3 Stream Composer, at3tool redistribué) ne sont ni fournis ni nécessaires.

## Utilisation

1. **Ouvrir** une vidéo (MP4, MOV, MKV, GIF…) : *Fichier > Ouvrir une vidéo ou un .pam* (`Ctrl+O`), clic dans le
   lecteur vide, ou glisser-déposer.

2. **Découper** 5 à 10 secondes qui bouclent bien : `I` et `O` posent l’entrée et la sortie à l’image affichée.

3. **Régler** : préréglage *Icône animée PS3 (recommandé)*, passage au 20:11, musique (onglet *Musique*), ICON0.PNG
   (*Tirer de l’image affichée*). Le **budget** doit rester vert.

4. **Projet** : cliquez sur la pastille *Projet* pour donner le nom et le **Title ID** du jeu (9 caractères).

5. **Convertir en ICON1.PAM** : les fichiers arrivent dans `Documents\PAM Forge\<projet>`, puis la page du fichier
   montre l’animation, les **6 vérifications** et les fichiers produits.

6. **Envoyer à la PS3** : adresse IP (SELECT + START avec webMAN MOD), dossier du jeu (`/dev_hdd0/game/<TITLE_ID>/`),
   fichiers à envoyer, puis *Envoyer à la PS3*. Redémarrez la console et mettez le jeu en surbrillance.

> Une lecture réussie dans RPCS3 est nécessaire, mais pas suffisante : seule la console valide l’icône. Testez
> d’abord sur un titre de test, et gardez toujours les fichiers d’origine.

## Raccourcis clavier

| Action | Touches |
|---|---|
| Lecture / pause | `Espace` |
| Image précédente / suivante | `←` / `→` |
| Reculer / avancer de 5 s | `Maj+←` / `Maj+→` |
| Entrée / sortie de la découpe | `I` / `O` |
| Boucle | `L` |
| Ouvrir | `Ctrl+O` |
| Choisir une musique | `Ctrl+M` |
| Projet | `Ctrl+P` |
| Convertir | `Ctrl+R` |
| Source / ICON1.PAM / côte à côte | `Ctrl+1` / `Ctrl+2` / `Ctrl+3` |
| Paramètres | `Ctrl+,` |

## Mises à jour et Discord

PAM Forge vérifie au démarrage si une nouvelle version est publiée sur GitHub ; chaque version est **signée** et
vérifiée avant d’être installée par `Update\PAM Forge Update.exe` (lancé seul, il cherche et installe lui-même la
dernière version). L’activité Discord montre ce que fait l’application
(découpe, conversion, vérification, envoi), jamais le nom de vos fichiers ; le bouton à ondes de l’en-tête l’active ou
la masque.

## En cas de problème

| Symptôme | Solution |
|---|---|
| « FFmpeg introuvable », « PAMFtool introuvable » | Le dossier `Tools` doit rester à côté de `PAM Forge.exe` : décompressez de nouveau le paquet, ou indiquez les outils dans *Paramètres > Outils*. |
| « Cette version de FFmpeg n’a pas l’encodeur libx264 » | Vous avez indiqué un autre FFmpeg : videz le champ dans *Paramètres > Outils* pour reprendre celui fourni, ou prenez une version « full » ou « GPL ». |
| « Le programme de mise à jour … est introuvable » | Le dossier `Update` doit rester à côté de `PAM Forge.exe` : décompressez de nouveau le paquet. |
| L’icône reste fixe sur la console | Nom exact `ICON1.PAM`, à côté du PARAM.SFO, budget respecté ; un `ICON1_02.PAM` passe devant sur une console en français ; l’option « No SND0.AT3 » de webMAN doit être décochée. |
| Musique accélérée | Le son doit être à 48 kHz : PAM Forge le prépare ainsi (astuce de pop-fe pour atracdenc). |
| La console ne répond pas | HEN activé, webMAN MOD actif, PC et PS3 sur le même réseau, bonne adresse IP. |

## Désinstaller

Supprimez le dossier de l’application. Les réglages sont dans `HKEY_CURRENT_USER\Software\PAMForge`, l’ouverture des
`.pam` dans `HKEY_CURRENT_USER\Software\Classes\PAMForge.Icon`, les journaux dans `%LocalAppData%\PAM Forge`.

## Crédits

- Format PAMF : d’après le module `cellPamf` de [RPCS3](https://github.com/RPCS3/rpcs3).

- Emballage : [PAMFtool](https://github.com/ravenDS/PAMFtool) de ravenDS ; encodage : [FFmpeg](https://ffmpeg.org) et x264 ;
  ATRAC3 : [atracdenc](https://github.com/dcherednik/atracdenc) ; astuce 48 kHz : [pop-fe](https://github.com/sahlberg/pop-fe).

- Projet non officiel, sans lien avec Sony Interactive Entertainment. PlayStation et PS3 sont des marques de leurs
  propriétaires.

---

## English

**PAM Forge** makes a PS3 game’s **animated ICON1.PAM icon** from any video: looping trim, **H.264 Main@2.1 at
320 × 176** wrapped in **PAMF**, **SND0.AT3** music, **ICON0.PNG** still icon, checks and sending to the console.
The interface is in French or English: choose it in *Help > Settings > General > Interface language*.

**Features**: source preview with the **20:11 output frame**, icon preview and side-by-side view · frame-accurate
looping trim with predicted keyframes and a 0.5 s **crossfaded seam** · the proven recipe (Main, level 2.1, CAVLC,
29.97 fps, one keyframe every 12 frames, 2-pass) by **FFmpeg (x264)**, PAMF wrapping with its EP map by **PAMFtool** ·
live **2,400,000-byte budget** with a recommended bitrate · SND0.AT3 in ATRAC3 132 kbit/s at 48 kHz (atracdenc or
at3tool) · ICON0.PNG from the displayed frame, optional PIC1.PNG · `.pam` reading with six checks (PAMF header,
2,048-byte sectors, Main@L2.1 320 × 176 CAVLC, EP map, exact name, budget) · sending through **webMAN MOD’s FTP** with
a **backup of the original files**, or a **test in RPCS3** · signed updates, Discord activity, three themes.

**Install**: download `PAMForge-win-x64.zip` from the latest release, unzip it and run `PAM Forge.exe`. The .NET
runtime and the conversion tools are included: **nothing else to install**. Keep `PAM Forge.exe`, the `Update` folder
(updater) and the `Tools` folder together.

**Tools**: FFmpeg (GPL-3.0, with x264), PAMFtool (ravenDS, GPL-3.0, self-contained) and atracdenc (LGPL-2.1) are
bundled in the **`Tools`** folder, each with its licence; `Tools\LICENCES.txt` lists versions, licences and source
code. To use another version, choose it in *Settings > Tools* or replace its files. at3tool (Sony, not redistributable)
and RPCS3 (optional, [rpcs3.net](https://rpcs3.net)) are not included.

**Uninstall**: delete the app folder. Settings are in `HKEY_CURRENT_USER\Software\PAMForge`, the `.pam` association in
`HKEY_CURRENT_USER\Software\Classes\PAMForge.Icon`, the logs in `%LocalAppData%\PAM Forge`.

Unofficial project, not affiliated with Sony Interactive Entertainment.
