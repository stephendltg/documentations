# ADB (Android Debug Bridge)

Android Debug Bridge (adb) est un outil de ligne de commande polyvalent qui vous permet de communiquer avec un appareil. La commande adb facilite diverses actions de périphérique, telles que l'installation et le débogage d'applications, et elle permet d'accéder à un shell Unix que vous pouvez utiliser pour exécuter diverses commandes sur un périphérique. C'est un programme client-serveur qui comprend trois composants :

- Un **client** , qui envoie des commandes. Le client s'exécute sur votre machine de développement. Vous pouvez appeler un client à partir d'un terminal de ligne de commande en émettant une commande adb.
- Un **démon** (adbd) , qui exécute des commandes sur un périphérique. Le démon s'exécute en arrière-plan sur chaque périphérique.
- Un **serveur** , qui gère la communication entre le client et le démon. Le serveur s'exécute en arrière-plan sur votre machine de développement.

## INTRODUCTION

Lorsque vous démarrez un client adb, le client vérifie d'abord si un processus de serveur adb est déjà en cours d'exécution. S'il n'y en a pas, il démarre le processus serveur. Lorsque le serveur démarre, il se lie au port TCP local 5037 et écoute les commandes envoyées par les clients adb. Tous les clients adb utilisent le port 5037 pour communiquer avec le serveur adb.

Le serveur établit ensuite les connexions à tous les appareils en cours d'exécution. Il localise les émulateurs en analysant les ports impairs dans la plage 5555 à 5585, la plage utilisée par les 16 premiers émulateurs. Lorsque le serveur trouve un démon adb (adbd), il établit une connexion à ce port. Notez que chaque émulateur utilise une paire de ports séquentiels - un port pair pour les connexions de console et un port impair pour les connexions adb. Par example:

- Emulator 1, console: 5554
- Emulator 1, adb: 5555
- Emulator 2, console: 5556
- Emulator 2, adb: 5557
- et ainsi de suite...

Comme indiqué, l'émulateur connecté à adb sur le port 5555 est le même que l'émulateur dont la console écoute sur le port 5554.

Une fois que le serveur a configuré les connexions à tous les appareils, vous pouvez utiliser les commandes adb pour accéder à ces appareils. Étant donné que le serveur gère les connexions aux appareils et gère les commandes de plusieurs clients adb, vous pouvez contrôler n'importe quel appareil à partir de n'importe quel client (ou à partir d'un script).


## Activer le débogage adb sur votre appareil

Pour utiliser adb avec un appareil connecté via USB, vous devez activer le débogage USB dans les paramètres système de l'appareil, sous Options du développeur . Pour utiliser adb avec un appareil connecté via Wi-Fi, voir Se connecter à un appareil via Wi-Fi .

Sur Android 4.2 et versions ultérieures, l'écran des options du développeur est masqué par défaut. Pour le rendre visible, accédez à Paramètres > À propos du téléphone et appuyez sept fois sur Numéro de build . Revenez à l'écran précédent pour trouver les options de développeur en bas.

Sur certains appareils, l'écran des options du développeur peut être situé ou nommé différemment.

Vous pouvez maintenant connecter votre appareil en USB. Vous pouvez vérifier que votre appareil est connecté en exécutant à **adb devices**. S'il est connecté, vous verrez le nom de l'appareil répertorié comme « appareil ».

::: tip Remarque
Lorsque vous connectez un appareil exécutant Android 4.2.2 ou une version ultérieure, le système affiche une boîte de dialogue vous demandant s'il faut accepter une clé RSA qui permet le débogage via cet ordinateur. Ce mécanisme de sécurité protège les appareils des utilisateurs car il garantit que le débogage USB et d'autres commandes adb ne peuvent pas être exécutés à moins que vous ne puissiez déverrouiller l'appareil et accuser réception de la boîte de dialogue.
:::

## INSTALLATION

``` bash
sudo apt install adb or via android studio
```

## TESTING INTENT SCANLESS -> REFLEX

**Method test reflex (version reflexWeb-14-3-0-3): Intent service Scanless**

``` bash
- Reflex "activer le log"

> adb shell logcat | grep -E "wagon"

- Start fence from scanless & execute - (REFLEX in front app)

> 06-16 10:32:20.829  3016  3016 D MediaScannerReceiver: action: android.intent.action.MEDIA_SCANNER_SCAN_FILE path: /storage/emulated/0/Android/data/hardis.com.wagonandroid/files/wagon0.txt

- Ouvrir fichier dans le terminal: /storage/emulated/0/Android/data/hardis.com.wagonandroid/files/wagon0.txt

- Content: "/storage/emulated/0/Android/data/hardis.com.wagonandroid/files/wagon0.txt":

> Skip data injection - no input field focused or enabled - <fence message>
```

## COMMANDS

### ADB SERVER

``` bash
adb kill-server
adb start-server
```

### DEVICES

``` bash
adb usb
adb devices   //show devices attached
adb devices -l //devices (product/model)
adb connect ip_address_of_device
```

### ADB REBOOT
``` bash
adb reboot
adb reboot recovery 
adb reboot-bootloader
adb root //restarts adb with root permissions
```

### SHELL
```
adb shell    // Open or run commands in a terminal on the host Android device.
```

### LOGCAT
``` bash
adb logcat
adb logcat -c // clear // The parameter -c will clear the current logs on the device.
adb logcat -d > [path_to_file] // Save the logcat output to a file on the local system.
adb bugreport > [path_to_file] // Will dump the whole device information like dumpstate, dumpsys and logcat output.

adb logcat *:V // lowest priority, filter to only show Verbose level
adb logcat *:D // filter to only show Debug level
adb logcat *:I // filter to only show Info level
adb logcat *:W // filter to only show Warning level
adb logcat *:E // filter to only show Error level
adb logcat *:F // filter to only show Fatal level
adb logcat *:S // Silent, highest priority, on which nothing is ever printed

adb logcat -v <format>
adb logcat -v brief // Display priority/tag and PID of the process issuing the message (default format).
adb logcat -v process // Display PID only.)
adb logcat -v tag //Display the priority/tag only.
adb logcat -v raw // Display the raw log message, with no other metadata fields.
adb logcat -v time // Display the date, invocation time, priority/tag, and PID of the process issuing the message.
adb logcat -v threadtime // Display the date, invocation time, priority, tag, and the PID and TID of the thread issuing the message.
adb logcat -v long // Display all metadata fields and separate messages with 

adb logcat -v time *:D
```

### FILES
``` bash
adb push [source] [destination]    // Copy files from your computer to your phone.
adb pull [device file location] [local file location] // Copy files from your phone to your computer.
```

### APP INSTALL
``` bash
adb -e install path/to/app.apk

-d                        - directs command to the only connected USB device...
-e                        - directs command to the only running emulator...
-s <serial number>        ...
-p <product name or path> ...
The flag you decide to use has to come before the actual adb command:

adb devices | tail -n +2 | cut -sf 1 | xargs -IX adb -s X install -r com.myAppPackage // Install the given app on all connected devices.
```

### UNINSTALLING APP FROM DEVICE
``` bash
adb uninstall com.myAppPackage
adb uninstall <app .apk name>
adb uninstall -k <app .apk name> -> "Uninstall .apk withour deleting data"

adb shell pm uninstall com.example.MyApp
adb shell pm clear [package] // Deletes all data associated with a package.

adb devices | tail -n +2 | cut -sf 1 | xargs -IX adb -s X uninstall com.myAppPackage //Uninstall the given app from all connected devices
```

### UPDATE APP
``` bash
adb install -r yourApp.apk  //  -r means re-install the app and keep its data on the device.
adb install –k <.apk file path on computer> 
```

### HOME BUTTON
``` bash
adb shell am start -W -c android.intent.category.HOME -a android.intent.action.MAIN
```

### ACTIVITY MANAGER
``` bash
adb shell am start -a android.intent.action.VIEW
adb shell am broadcast -a 'my_action'

adb shell am start -a android.intent.action.CALL -d tel:+972527300294 // Make a call
```


### PERMISSIONS
``` bash
adb shell pm reset-permissions -p your.app.package 
adb shell pm grant [packageName] [ Permission]  // Grant a permission to an app. 
adb shell pm revoke [packageName] [ Permission]   // Revoke a permission from an app.
```

### PRINT TEXT
``` bash
adb shell input text 'Wow, it so cool feature'
```

### SCREENSHOT
``` bash
adb shell screencap -p /sdcard/screenshot.png

$ adb shell
shell@ $ screencap /sdcard/screen.png
shell@ $ exit
$ adb pull /sdcard/screen.png

---
adb shell screenrecord /sdcard/NotAbleToLogin.mp4

$ adb shell
shell@ $ screenrecord --verbose /sdcard/demo.mp4
(press Control + C to stop)
shell@ $ exit
$ adb pull /sdcard/demo.mp4
```

### KEY EVENT
``` bash
adb shell input keyevent 3 // Home btn
adb shell input keyevent 4 // Back btn
adb shell input keyevent 5 // Call
adb shell input keyevent 6 // End call
adb shell input keyevent 26  // Turn Android device ON and OFF. It will toggle device to on/off status.
adb shell input keyevent 27 // Camera
adb shell input keyevent 64 // Open browser
adb shell input keyevent 66 // Enter
adb shell input keyevent 67 // Delete (backspace)
adb shell input keyevent 207 // Contacts
adb shell input keyevent 220 / 221 // Brightness down/up
adb shell input keyevent 277 / 278 /279 // Cut/Copy/Paste
```

[keycode](https://developer.android.com/reference/android/view/KeyEvent.html)


### DEVICE INFORMATION
``` bash
adb get-statе (print device state)
adb get-serialno (get the serial number)
adb shell dumpsys iphonesybinfo (get the IMEI)
adb shell netstat (list TCP connectivity)
adb shell pwd (print current working directory)
adb shell dumpsys battery (battery status)
adb shell pm list features (list phone features)
adb shell service list (list all services)
adb shell dumpsys activity <package>/<activity> (activity info)
adb shell ps (print process status)
adb shell wm size (displays the current screen resolution)
dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp' (print current app's opened activity)
```

### PROCESSUS
``` bash
adb shell ps // To show information about the currently running processes
adb shell top –m [num] –s [cpu | vss | rss | thr] –t –d [num] // To display top CPU processes
```
- m [num]: Maximum number of processes to display
- s [cpu,vss,rss,thr]: column to sort by <cpu,vss,rss,thr>
- t: Show threads instead of processes
- d: Time interval for information update 

### MEMORY
``` bash
adb shell cat /proc/meminfo // To show memory usage
adb shell procrank -p // To show a quick summary of process memory utilization. By default it shows Vss, Rss, Pss and Uss, and by sorts by Vss
adb shell procmem –p [PID] // To show a quick summary of process memory utilization. By default it shows Vss, Rss, Pss and Uss, and by sorts by Vss
adb shell dumpsys meminfo [PID] // To show memory information in details for the selected process
``` 

### NETWORK
```bash
adb shell tcpdump // To dump traffic on a network
```

### PACKAGE INFO
``` bash
adb shell list packages (list package names)
adb shell list packages -r (list package name + path to apks)
adb shell list packages -3 (list third party package names)
adb shell list packages -s (list only system packages)
adb shell list packages -u (list package names + uninstalled)
adb shell dumpsys package packages (list info on all apps)
adb shell dump <name> (list info on one package)
adb shell path <package> (path to the apk file)
```

[Sources](https://www.automatetheplanet.com/adb-cheat-sheet/)
