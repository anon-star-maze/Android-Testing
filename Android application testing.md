# Android application testing methodology with commands

>	Decompile the apk using __apktool__
-	apktool d <apk file>
-	Application folder will be created in home folder

>	Check __manifest__ file for permissions and __yml__ file 
-	External storage permission
-	Unnecesary permissions
-	<activity android:exported="true" should be false
-	Identify IPC intent-filter
-	android:allowBackup="true" should be false
-	allowdebug shoould be false

>	Use __dex2jar__ to convert
-	d2j-dex2jar /home/anonstar/Downloads/com.application.name/classes.dex

>	Use __jd-gui__ to open the jar file
	
>	Use __ClassNameDeobfuscator_ [https://codeload.github.com/HamiltonianCycle/ClassNameDeobfuscator/zip/master] to deobfuscate smali files
-	python3 /home/anonstar/Downloads/ClassNameDeobfuscator-master/ClassNameDeobfuscator.py -o anyname.txt com
-	If you find .source in output, report it

>	Install __mobsf__:
-	pip3 install -r requirements.txt
-	apt install python3-venv
-	./setup.sh
-	./run.sh


>	Use __Genymotion__ or Android VMs from "Android x86 Boxes"
-	To intercept and modify requests in burpsuite

>	Code tampering check
-	Modify Android Manifest file with changed permission and recompile apktool b <decompiled folder name>
-	Then go to dist folder, inside which is the recompiled apk file
-	Resign apk-
-	In windows, place it in java's java/jdk/bin folder, open admin command prompt there and enter commands:
-	Generate keystore by using command - keytool -genkey -v -keystore <anykeystorname.keystore> -alias sh -keyalg RSA -keysize 2048 -validity 10000
-	Enter any password of 6 digits/characters
-	Answer security questions
-	Key will be created in same bin folder
-	Sign the apk by giving command as - jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore <anykeystorename.keystore> <disfolderapk.apk> sh
-	Install this apk. If it works, report it

>	Sensitive information checks	
-	Browse to root folder
-	Extract and view sqlite databases
-	View shared preference folder for sensitive information in xml files like user credentials, imei in clear text
-	Cache folder for sensitive data


###	Additional checks:
	Code obfuscation check
	Print stack trace should not be present
	Check for hardcoded credentials/keys/encryption algorithm
	Allow all hostname verifier
	Android webkit websettings check
	Javascript value should be false