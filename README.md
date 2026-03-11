## Install the dependencies

1. Install .NET 6.0 Runtime (needed by WiX):

    https://aka.ms/dotnet-core-applaunch?missing_runtime=true&arch=x64&rid=win10-x64&apphost_version=6.0.36

2. Install Java and WiX using Scoop:

    ```shell
    scoop bucket add java
    scoop install temurin-lts-jdk wixtoolset@6.0.2
    ```

3. Install the WiX extensions:

    ```shell
    wix extension add -g WixToolset.Util.wixext/6.0.2
    wix extension add -g WixToolset.Ui.wixext/6.0.2
    ```





## Run with WiX using Scoop

1. Make sure WiX is already install using Scoop:

    ```shell
    scoop install wixtoolset@6.0.2
    ```

2. Run `mvn clean package`

    Either from the Maven wrapper:

    ```shell
    ./mvnw clean package
    ```

    Or from your own system Maven installation:

    ```shell
    mvn clean package
    ```

Expected result: it should produce an installation package in `target/MyApp-0.0.1.exe`.


## Run with WiX using aqua

1. Make sure WiX is uninstalled using Scoop, and installed using aqua:

    ```shell
    scoop uninstall wixtoolset
    scoop install aqua
    Set-Item Env:Path "$Env:LOCALAPPDATA\aquaproj-aqua\bin;$Env:Path"
    aqua install
    ```

2. Run `mvn clean package`

   Either from the Maven wrapper:

    ```shell
    ./mvnw clean package
    ```

   Or from your own system Maven installation:

    ```shell
    mvn clean package
    ```

Expected result: it should fail with a similar message:

```console
[ERROR] Failed to execute goal org.panteleyev:jpackage-maven-plugin:1.7.1:jpackage (default) on project aqua_wix.mwe:
[ERROR] Exit code: 1 - java.io.IOException: Command [wix.exe, build, -nologo, -pdbtype, none, -intermediatefolder, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\wixobj, -ext, WixToolset.Util.wixext, -arch, x64, -b, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config, -loc, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\MsiInstallerStrings_de.wxl, -loc, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\MsiInstallerStrings_en.wxl, -loc, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\MsiInstallerStrings_ja.wxl, -loc, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\MsiInstallerStrings_zh_CN.wxl, -culture, en-us, -d, JpExecutableMinorOSVersion=0, -d, JpAppDescription=MyApp, -d, JpProductCode=6ef946c6-77a6-3007-8d06-920818e23634, -d, JpAppName=MyApp, -d, JpIsSystemWide=yes, -d, JpAllowDowngrades=yes, -d, JpIcon=C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\image\MyApp\MyApp.exe, -d, JpAppSizeKb=125324, -d, JpAppVersion=0.0.1, -d, JpExecutableOSVersion=600, -d, JpAllowUpgrades=yes, -d, JpProductUpgradeCode=5b26eefb-dadd-3cba-a04a-ed833e6157b1, -d, JpExecutableMajorOSVersion=6, -d, JpAppVendor=ACME, -d, JpConfigDir=C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\main.wxs, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\bundle.wxf, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\ui.wxf, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\config\os-condition.wxf, -out, C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\wixobj\a.msi] in C:\Users\vmuser\AppData\Local\Temp\jdk.jpackage14781275708702792597\image\MyApp exited with 1 code
[ERROR]
[ERROR] Command line was: cmd.exe /X /C "C:\Users\vmuser\scoop\apps\temurin-lts-jdk\current\bin\jpackage.exe --name MyApp --dest Z:\aqua-wix-mwe\target --app-version 0.0.1 --input Z:\aqua-wix-mwe\target --vendor ACME --main-class aqua_wix.mwe.MyApp --main-jar aqua_wix.mwe-0.0.1.jar"
```
