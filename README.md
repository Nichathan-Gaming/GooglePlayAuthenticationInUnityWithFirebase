# Google Play Authentication In Unity With Firebase *Android*
A detailed tutorial on how to implement Google Play Authentication in Unity with Firebase in 2023 using the new GooglePlayGamesPlugin-0.11.01

## Table of Contents
1. **[Initial Setup and Details](#Initial-Setup-and-Details)**
   1. **[Disclaimer](#Disclaimer)**
   1. **[Details](#Details)**
   2. **[Before continuing you should have](#Before-continuing-you-should-have)**
2. **[Instructions](#Instructions)**
   1. **[Firebase Setup](#Firebase-Setup)**
   2. **[Unity Setup 0](#Unity-Setup-0)**
   3. **[Grabbing Unity's SHA1 key](#Grabbing-Unitys-SHA1-key)**
   4. **[GitHub Privacy Policy](#GitHub-Privacy-Policy)**
   5. **[Google Play Console Setup 0](#Google-Play-Console-Setup-0)**
   6. **[Google Cloud APIs & Services Setup](#Google-Cloud-APIs-&-Services-Setup)**
   7. **[Google Play Console Setup 1](#Google-Play-Console-Setup-1)**
   8. **[Unity Setup 1](#Unity-Setup-1)**
   9. **[Unity Testing](#Unity-Testing)**

## Initial Setup and Details
### Disclaimer
To the best of my knowledge, this walkthrough and all content inside of it has been typed with no errors or misinformation. That being said, neither I, nor Nichathan Gaming owns, has affiliation to, or any form of control over Unity, Google, the Google Console or Google Firebase. All information in this walkthrough is subject to become obsolete at any moment and there are no guarantees that anything inside of this walkthrough will work. By continuing to follow this walkthrough, you understand that neither Johnathan Nichols nor Nichathan Gaming are responsible for whatever may happen. That being said, I put a lot of time and effort into this walkthrough and I sincerely hope that it can help you.
</br>**[Back To Top](#Table-of-Contents)**

### Details
This walkthrough was typed by Johnathan Nichols of [Nichathan Gaming](https://play.google.com/store/apps/dev?id=5505294983591200024) on February 4th 2023. This guide was typed after months of casual intrigue and a week of serious contemplation over the authentication process. The walkthroughs purpose is to supplement the lack of documentation by Google Play Console, Unity and Firebase which all contain frustratingly outdated and useless documentation with nothing current or pointing to depreciated links.
<br>Please note that this tutorial is only for **Android Apps** and does not cover **Apple** or **IOS** apps.
</br>**[Back To Top](#Table-of-Contents)**

### Before continuing you should have
- A [Google Play Account](https://play.google.com/console) which costs around $25 (USD). 
- A [Firebase](https://firebase.google.com/) account with the same Google Account as your Google Play account.
- Download the current [GooglePlayGamesPlugin](https://github.com/playgameservices/play-games-plugin-for-unity/blob/master/current-build/GooglePlayGamesPlugin-0.11.01.unitypackage) which is 0.11.01 as of this posting.
- The latest [Unity](https://unity.com/download) LTS editor with Android modules installed.
- A Console editor such as *Command Prompt*, *Powershell*, *[Hyper](https://hyper.is/)*, etc...
- An Android device to test/run your app on
</br>**[Back To Top](#Table-of-Contents)**

## Instructions
### Firebase Setup
<br>1. From the [Firebase Console](https://console.firebase.google.com/) click *Add Project*.
<br>![Firebase Console](https://user-images.githubusercontent.com/103794085/216764877-9b1d4c02-041b-4b1c-9922-317c03bc224b.png)
<br>2. Give the project any name, *for the purpose of this tutorial, the project will be called GPGS*.
    1. For the purposes of this guide, you may enable or disable Google Analytics.
<br>3. Click **Create Project** and wait for the project to be created.
<br>4. In the project overview, under **Get started by adding Firebase to your app**, click the **Unity** icon.
<br>![Unity Icon](https://user-images.githubusercontent.com/103794085/216765040-ea3eeedf-1b7b-4217-af6f-8505300e3663.png)
<br>5. Under *Register App*, click the *Register as Android app* checkbox then:
    1. Enter a package name for your project. This is com.CompanyName.AppName, if you do not have a company, any name works here.
    2. Save the package name as we will use it in the **Google Play Console** and in the **Unity Editor**
<br>6.  Click **Register app**
<br>![Register App button](https://user-images.githubusercontent.com/103794085/216765336-1ad51e22-3cfe-4738-86fa-0e8812c9dcfe.png)
<br>7. Download the google-services.json config file *It will be added to our **Unity** project later*
<br>![GSJSON Image](https://user-images.githubusercontent.com/103794085/216765401-601befc3-938b-4357-9d46-89ba381bd952.png)
<br>8. Download the Firebase Unity SDK (Zip) then:
    1. Unzip the files anywhere. *We will only use the Auth Unity Package but feel free to add others*
<br>![Firebase SDK Image](https://user-images.githubusercontent.com/103794085/216765481-63ef3dfc-01ee-4a55-9eb0-04910529d79e.png)
<br>![Unzipped SDK](https://user-images.githubusercontent.com/103794085/216765532-23a9f665-6186-4fd2-9a2c-c1545d82bcf5.png)
<br>9. Click *Continue to console*
<br>10. Navigate to Build/Authentication and click *Get started*
<br>![Get Started](https://user-images.githubusercontent.com/103794085/216765954-106db4db-9dd4-49ba-8e56-d470f0750a2c.png)
<br>11. Click the *Google* Sign-in method
<br>![Google Sign in method](https://user-images.githubusercontent.com/103794085/216765995-4fa3db3c-a4f9-4284-bcac-dd2e95d53e56.png)
<br>12. Click Enable then add a public facing name and a support email. (The name is what is shown to users when Firebase sends them emails and the support email is where you receive emails from the user. This interaction is hands free and mediated through Firebase so no one knows the other's information.)
<br>13. Click *Save*
<br>![Google Sign in method](https://user-images.githubusercontent.com/103794085/216766111-446c72cc-5904-4872-89ec-fc81addc8ffe.png)
<br>14. Ignore the *Download latest configuration file* screen by clicking *Done*
<br>![pop up screen](https://user-images.githubusercontent.com/103794085/216766154-f5631fc0-9366-46f4-8798-55c26c69d556.png)
<br>15. Click the *Google* Sign-in method again and expand the *Web SDK configuration* drop-down, then:
    1. Copy the *Web client ID* and *Web client secret* to your *clipboard*, *notepad*, *word*, etc...
    2. Note: You can use the windows key and V to open your clipboard history ![win+V](https://user-images.githubusercontent.com/103794085/216766297-616fe224-7123-41a5-83d7-1bbd9d9d0047.png)
<br>![WhatToCopy](https://user-images.githubusercontent.com/103794085/216766356-ac494fea-f236-4867-a7b4-05ebd1df6e4f.png)
<br>16. Click *Cancel*
<br>17. Click *Add new provider* then click *Play Games*
<br>![Add Play Games](https://user-images.githubusercontent.com/103794085/216766437-832b4cbb-1eb7-4826-8fa0-7468f6f3e57e.png)
<br>18. Click *Enable* and paste your *Client ID* and *Client Secret* from **step 15.1** into the fields.
<br>19. Click *Save*
<br>![PG Add](https://user-images.githubusercontent.com/103794085/216766527-6f80cc34-8c3e-45af-af08-7b49c4d0673b.png)
### Firebase Setup End
</br>**[Back To Top](#Table-of-Contents)**

### Unity Setup 0
Note: This walkthrough uses the Unity Editor 2021.3.16f1 which is the latest LTS version. If you encounter errors, first make sure that you are using the latest LTS version of Unity. You should also have the *Android Build Support* platform modules installed. I read that having *iOS Build Support* may clear some of the issues so I have it as well but I am unsure if it is useful or not.
<br>![Unity Setup](https://user-images.githubusercontent.com/103794085/216766783-53ae893b-d18d-4a82-8bed-e25695ce854c.png)
<br>1. In the *Unity Hub*, click *New Project*
<br>Note: This walkthrough should work in any existing projects but for the purposes of this walkthrough, we will create a vanilla project.
<br>2. Select a project type and a project name, then click *Create project*.
<br>Note: Your project can be any type but for the purposes of this walkthrough, we will use *2D Core* with the name of *GPGS*
<br>![Create Project example](https://user-images.githubusercontent.com/103794085/216767051-6bbf3f48-eed4-492c-a2c2-d26100d0cc6a.png)
<br>3. Once your *Unity Editor* finished building, navigate to and click *File/Build Settings* or press *CTRL-SHIFT-B* all at once.
<br>![Build Settings](https://user-images.githubusercontent.com/103794085/216767223-6659dbbc-66e4-4b87-b49e-4091d468f5af.png)
<br>4. If your project Platform is not already set to *Android*, click *Android* then click *Switch Platform*, otherwise, skip this step.
<br>![Switch Platform](https://user-images.githubusercontent.com/103794085/216767312-18a0d413-85a5-4ca1-a8d3-2dfff80456e1.png)
<br>5. Check *Build App Bundle (Google Play)* and set *Create symbols.zip* to public.
<br>![Settings](https://user-images.githubusercontent.com/103794085/216767379-9481a8ea-aad3-4531-862c-babf1f5fc79e.png)
<br>6. Click *Player Settings* and ensure that you are at *Project Settings/Player* once the new window opens.
<br>![Examples](https://user-images.githubusercontent.com/103794085/216767435-eabf9344-64bd-468b-a503-e2ef2517ff15.png)
<br>7. Under *Player* set your *Company Name* and *Product Name* to fit the package name used in 5.1 of the **[Firebase Setup](Firebase-Setup)** section.
<br>![Company/Product Name example](https://user-images.githubusercontent.com/103794085/216767509-3ae96e40-93cf-4fb3-b8e2-1989e389fd68.png)
<br>8. Navigate to *Other Settings* to *Identification* and either unselect *Override Default Package Name* or type it manually into the *Package Name* input field.
<br>![Package Name IF](https://user-images.githubusercontent.com/103794085/216767610-1a71921f-db2c-42af-88d6-a927330ef4a3.png)
<br>9. Set the *Target API Level* to the highest available unless you are certain that you have the highest installed already. Note: This will install the highest Android API level when you build your app and you can use *Automatic(highest installed)* from here on out.
<br>![image](https://user-images.githubusercontent.com/103794085/216767666-7b22260a-2951-45a9-9596-6740c2bcd8f3.png)
<br>10. Under *Player/OtherSettings/Configuration* set *Scripting Backend* to *IL2CPP* and select *ARM64*.
<br>![Config](https://user-images.githubusercontent.com/103794085/216767796-e182fc48-1262-417d-a1b5-54cbb9615519.png)
<br>11. Now, move from *Player/Other Settings* to *Player/Publishing Settings* and click *Keystore Manager...*
<br>![keystore manager button](https://user-images.githubusercontent.com/103794085/216767851-affefbac-b965-4e9d-80f2-f7965f054d2a.png)
<br>12. In the pop-up window, click *Keystore.../Create New/Anywhere...* then save the keystore under any filename, as long as the file extension is *.keystore* and click *Save*.
<br>![Create new keystore](https://user-images.githubusercontent.com/103794085/216767925-da9b0c27-3b26-405d-9e86-8610301bce43.png)
<br>13. Enter any password, then under *New Key Values* fill out the required fields to click *Add Key* 
<br>![Key manager](https://user-images.githubusercontent.com/103794085/216768046-dd3b396e-128d-4270-b4e1-f6a38d08bbc4.png)
<br>14. At the new pop-up screen *Keystore and Key created* click *Yes*
<br>![pop up keystore](https://user-images.githubusercontent.com/103794085/216768094-df88d352-b91a-48cb-9d7a-b967b4b41da0.png)
### Unity Setup 0 End
</br>**[Back To Top](#Table-of-Contents)**

### Grabbing Unitys SHA1 key
Note: Now, we will grab the SHA1 key which we just created in step 13 of **[Unity Setup 0](Unity-Setup-0)**. To do this, we must work in a console. This may be **Command Prompt**, **PowerShell**, **[Hyper](https://hyper.is/)**, or any other console. Please, be careful with the commands that you type into your console, especially if you are untrained. While you shouldn't be able to seriously damage anything since you have few permissions until you know how to get them, there is still a chance that you can do damage if you deviate from the commands shown in this walkthrough. For the purposes of this walkthrough, we will use **[Hyper](https://hyper.is/)** but the commands should still work in any other console. Please note as well that in console commands, they use the word *directory* instead of folder. Some useful console commands are *ls* (lists all files and directories in the current directory), cd .. (navigates to the directory that holds this directory), cd /path/ (navigates to the directory at the given path). Also, you should not be able to use *CTRL+C* or *CTRL+X* to copy or cut text. Instead, you may need to use the right mouse button to copy in consoles.
<br>1. First, we must identify the directory where we saved our keystore. If you followed along, this should be in our project folder. Although, your *Keystore Manager* should show you the path. From the image below, you can see that my keystore is in my project folder under the file name *user.keystore*.
<br>![path loc](https://user-images.githubusercontent.com/103794085/216768647-f9ee1d56-eb62-4834-b5e6-b1afbe9ba105.png)
<br>2. Now open your console or terminal and navigate to the path of your keystore. To see where you are, use 'ls', to move back use 'cd ..', to move forward use 'cd PATHNAMEHERE'.
<br>![Hyper](https://user-images.githubusercontent.com/103794085/216768846-ed7c2ea3-a163-4335-a0ca-a906e668f7a1.png)
<br>3. Once you are at your *user.keystore* location (or whatever you named your *.keystore* file as), type 'keytool -keystore KEYSTORE FILE NAME -list -v' replacing 'KEYSTORE FILE NAME' with the name of your .keystore file. Then, enter your password that you used to create your .keystore file in step 13 of **[Unity Setup 0](Unity-Setup-0)**.
<br>![GetSHA1](https://user-images.githubusercontent.com/103794085/216768998-f1277d92-1d40-432a-b9a9-b21715c97c6c.png)
<br>4. Finally, highlight and copy your SHA1 certificate fingerprint. Remember, you may need to use the right mouse button to copy in your console.
<br>![CopySHA1](https://user-images.githubusercontent.com/103794085/216769111-405d82f9-3fb0-42a7-9540-a1e0624b7e37.png)
### Grabbing Unitys SHA1 key End
</br>**[Back To Top](#Table-of-Contents)**

### GitHub Privacy Policy
Note: The Google Play Console requires all apps to have a privacy policy. That being said, all a privacy policy is, is pretty much a notice of intent. You can host your privacy policy on GitHub or on your personal website. However, GitHub is free and easy to use. However, if GitHub or your GitHub account are taken offline or deleted, your app may be forcefully unpublished until a new privacy policy is provided.
<br>1. Navigate to the [new repository section of GitHub](https://github.com/new)
<br>2. Enter a repository name such as *GPGSPrivacyPolicy*, check *Add a README file* and click *Create repository*
<br>![image](https://user-images.githubusercontent.com/103794085/216770440-e1d0015c-7dc9-4f0d-8aea-682d750a2f63.png)
<br>3. Inside your new repository, click the pencil next to your README.md file to edit it.
<br>![Repo Edit](https://user-images.githubusercontent.com/103794085/216770500-373b566d-6266-45a6-8d6d-b7be14eec153.png)
<br>4. Add content similar to that shown below and click *Commit changes*
```
I hereby state, to the best of my knowledge and belief, that I have not programmed this app to collect any personally identifiable information. All data created by you (the user) is stored on your device only, and can be erased by clearing the application's data or by uninstalling the application.
```
<br>5. Copy and save the link to your GitHub Repository. For example, mine is `https://github.com/Nichathan-Gaming/GPGSPrivacyPolicy`.
### GitHub Privacy Policy End
</br>**[Back To Top](#Table-of-Contents)**

### Google Play Console Setup 0
Note: Remember, you must purchase a Google Play Console account first which costs around $25 (USD) at the time that this walkthrough was published. Costs are subject to increase or decrease at any time.
<br>1. In the [Google Play Console](https://play.google.com/console/), while logged in, click *Create app*
<br>![GPC](https://user-images.githubusercontent.com/103794085/216769629-0b9aacdb-e9ce-4c77-a67b-c6b4a6c21c39.png)
<br>2. Fill out the App details. I do not believe that *App name*, *Default Language* nor *Free or Paid* matters but to use the *Google Play Games Console* you must select *Game* under *App or game*
<br>![app details](https://user-images.githubusercontent.com/103794085/216769750-dc515163-3c8e-49a8-8b9d-4522107efbb8.png)
<br>3. Then click, *Create app* in the bottom right of the screen.
<br>4. Navigate to *Grow/Store presence/Main store listing* and fill out the app details to the best of your abilities. Then click *Save* Note: You must provide descriptions of at least 1 character, a 512x512 image, a 1024x500 image and at least 2 9x16 images in the *Phone* and *Tablet* sections.
<br>![MSL](https://user-images.githubusercontent.com/103794085/216769984-6cacfbfa-81df-4822-b983-d6ed4573d89c.png)
<br>5. Navigate down to *Store settings* in the same area and fill out the settings to the best of your abilities. Then click *Save*.
<br>![SS](https://user-images.githubusercontent.com/103794085/216770045-4ce6bbc4-8d67-4f50-8231-95debf8d4c34.png)
<br>6. Scroll to the very bottom to App Content and fill out all parts of the *To do* to the best of your abilities. Do this one at a time by clicking *Start*. Ensure that you always save when are done with a field.
<br>![TODO](https://user-images.githubusercontent.com/103794085/216770146-cf031c7e-ac02-4eb5-9606-f4161a1bf1b8.png)
<br>![completed](https://user-images.githubusercontent.com/103794085/216770805-e11aa513-cf3e-4d27-9525-4077be24cdfc.png)
<br>7. After, you're all done with part 6, scroll up to *Grow/Play Games Services/Setup and management/Configuration*, select *Yes, my game already uses Google APIs, select your Firebase project from the *Cloud project* drop-down and click *Use* in the bottom right.
<br>![Config Setup](https://user-images.githubusercontent.com/103794085/216770982-0a02f2a1-3b28-483a-b29a-99e1ddd0e899.png)
<br>8. In the same area, to the right of *Credentials*, click *Add credentials*
<br>![AddCred](https://user-images.githubusercontent.com/103794085/216771041-da09b3fe-aecb-458c-91c5-e071783e305a.png)
<br>9. Click *Create OAuth client* then follow the link to *Create OAuth Client ID*.
<br>![follow link](https://user-images.githubusercontent.com/103794085/216771153-f58c2e77-58f1-49a6-9d47-41f9cbb8eeb6.png)
### Google Play Console Setup 0 End
</br>**[Back To Top](#Table-of-Contents)**

### Google Cloud APIs & Services Setup
Note: Ensure that you are always in the current project. If you ever leave the web page and return, you may need to re-select your project. 
<br>![GCAPI](https://user-images.githubusercontent.com/103794085/216772513-d7175e37-a0af-4743-9256-8a916a093340.png)
<br>1. Click *+ CREATE CREDENTIALS* then *OAuth client ID*
<br>![OAuth](https://user-images.githubusercontent.com/103794085/216772590-0d57fff0-d7d2-4949-8023-fe95f16f42b9.png)
<br>2. Select *Android* for your *Application type*, use the *Package Name* used in Firebase and in your Unity project and add the *SHA-1 certificate fingerprint* from step 4 **[Grabbing Unitys SHA1 key](Grabbing-Unitys-SHA1-key)** then click *CREATE*.
<br>![OAUTH ex](https://user-images.githubusercontent.com/103794085/216772893-2c45c6d3-c369-4b76-8679-85bf4d6cd12c.png)
<br>3. In the popup, download the JSON file and click *OK*
<br>![popup](https://user-images.githubusercontent.com/103794085/216772952-69ea3fb5-9062-4452-9a0f-8091f48ec19b.png)
### Google Cloud APIs & Services Setup End
</br>**[Back To Top](#Table-of-Contents)**

### Google Play Console Setup 1
Note: Make sure that you have done all of the previous steps before reaching this part. We will continue from the last step of **[Google Play Console Setup 0](Google-Play-Console-Setup-0)**.
<br>1. Back in the *Google Play Console/Grow/Play Games Services/Setup and management/Configuration/Add credential* screen, go down to *Authorization*, click *Refresh OAuth clients* and select the newly created client in the drop down. Click *Save changes* and go back to *Configuration* Note: There should only be 1 option. If not, ensure that *Type* is still *Android*.
<br>![Android Cred](https://user-images.githubusercontent.com/103794085/216774502-29f44104-443c-4329-b37d-d3264bb971a9.png)
<br>2. Click Add Credential again, select *Type* as *Game server*, click *Refresh OAuth clients* and in the drop down, select the option that has the same Client ID as your Firebase Google Sign-in method. Then click *Save changes* and go back to *Configuration*.
<br>![FBCID](https://user-images.githubusercontent.com/103794085/216774655-20ee89f3-7880-46c8-958b-64ecb20f4ac7.png)
<br>![CredOption](https://user-images.githubusercontent.com/103794085/216774689-2bb3d4c1-92de-4e02-92e0-cf2d29de4b88.png)
<br>3. Click *Get Resources* and copy the *Android(XML)*. Note: This will not be used until **[Unity Setup 1](Unity-Setup-1)** so save it in a safe space.
<br>![button](https://user-images.githubusercontent.com/103794085/216775829-cff8ccaf-46da-4b1e-b217-adc5582d2d03.png)
<br>![XML](https://user-images.githubusercontent.com/103794085/216775863-484557ef-11ba-433e-8a7d-996ca7ad0dd8.png)
<br>4. Click *Review and publish*.
<br>![RAP](https://user-images.githubusercontent.com/103794085/216799513-e88700be-cdf7-447f-b9df-0061640b191d.png)
<br>5. If you have actions required in your properties, click the arrow and fill out all of the information in the new area. Note: Wait for the images to finish uploading before clicking the *Save changes* button.
<br>![Update](https://user-images.githubusercontent.com/103794085/216799538-9ac2a7d0-749d-4d3a-ad3f-42f2c9ea2f40.png)
<br>![Filled out](https://user-images.githubusercontent.com/103794085/216799569-7ecc8726-84e6-4236-a9fd-9ae99d6cd5e8.png)
<br>6. Return to *Configuration* then click *Review and Publish*. You should now be able to click the *Publish* button. If not then you should see required fields that you neglected to fill out. At the pop-up, confirm the publish.
<br>![publish btn](https://user-images.githubusercontent.com/103794085/216799607-f60e680c-157b-4f1d-a35d-a75f7e79a312.png)
### Google Play Console Setup 1 End
</br>**[Back To Top](#Table-of-Contents)**

### Unity Setup 1
Note: If you closed *Unity* at any time since [Unity Setup 0](Unity-Setup-0), you will need to reenter your *keystore* password in *Project Settings/Player/Publishing Settings*.
<br>1. Go to *Assets/Import package/Custom package* then import the *Firebase Auth unity package* and the *GooglePlayGamesPlugin-0.11.01.unitypackage*. Note: It should be fine if there is a newer version of the *Google Play Games Plugin* package. You should always use the newest stable version. Also, ensure that you import all files when prompted.
<br>![Menu](https://user-images.githubusercontent.com/103794085/216774825-2bc74511-efb5-414f-9219-68554890deba.png)
<br>![GPGP](https://user-images.githubusercontent.com/103794085/216774938-066684b5-5dda-4fd7-bd17-e222cd21fc1d.png)
<br>![FBAUTH](https://user-images.githubusercontent.com/103794085/216774952-5a65a695-8d53-47c5-862d-f89ea56ed347.png)
<br>2. While importing the *Google Play Games Plugin* you may see a screen similar to the picture below. Enable *Anroid Auto Resolution* and *Delete* old files.
<br>![Pop Up GPGP](https://user-images.githubusercontent.com/103794085/216775552-3ac92866-f14c-4336-a495-0deafc3764cd.png)
<br>3. Navigate to *Window/Google Play Games/Setup/Android Setup...* and click on it.
<br>![button](https://user-images.githubusercontent.com/103794085/216775736-318b4ce2-f709-44f1-a7d5-46e11dd8435d.png)
<br>4. In the *Google Play Games - Android Configuration* pop-up screen, paste your XML from step 3 of **[Google Play Console Setup 1](Google-Play-Console-Setup-1)** in the big box, paste your *Firebase Google Client ID* where it says *Client ID* then click *Setup*.
<br>![setup](https://user-images.githubusercontent.com/103794085/216776052-a3e56f30-b672-49bd-a477-1993a27ebf5f.png)
<br>![success](https://user-images.githubusercontent.com/103794085/216776071-fd599496-9564-4452-b6d2-08922895f0c3.png)
<br>5. Now, you need to import the JSON files from step 7 of **[Firebase Setup](Firebase-Setup)** and step 3 of **[Google Cloud APIs & Services Setup](Google-Cloud-APIs-&-Services-Setup)**.
<br>6. Go to *Assets/External Dependency Manager/Android Resolver/Force Resolve* and click to force resolve.
<br>![force resolve](https://user-images.githubusercontent.com/103794085/216776166-a1269398-9cff-4f4f-86a8-79053a59e4a8.png)
<br>Note: We will now setup scripts to test the authentication. You are already setup to use the authentication and no longer have to follow this guide religiously. You can skip to step 12 **[Foundation Code](Foundation-Code)** for the code, or follow along to log results to your device screen. Also, remember that this will not work on your computer. You can only test or run Google Play authentication in Unity with Firebase on your mobile Android device. Because of this, I will add a TMP_Text object to my screen to see results.
<br>7. Right click in the Hierarchy and create a UI/Scroll View. Then delete the Content and both Scrollbars.
<br>![delete](https://user-images.githubusercontent.com/103794085/216776680-04fb2889-4c8b-436e-a9c7-1003102ef58a.png)
<br>8. Right click on Viewport and add a UI/Text(TMP) then import TMP essentials.
<br>![TMPPRO](https://user-images.githubusercontent.com/103794085/216776726-f1d25829-250a-4fb3-92b8-8aafb6d9d4f9.png)
<br>9. Select the Canvas in the Hierarchy and set the Canvas Scalar values to those shown below.
<br>![CanvasScalar](https://user-images.githubusercontent.com/103794085/216776797-b957f4c7-ada0-48a0-8920-e886679d3321.png)
<br>10. On the Text (TMP) object, add a *Content Size Fitter* with a vertical fit to *Preferred Size* and set the *Anchors* and *Pivots* to those shown below. Also, set the *Font Size* very high, we will use 100 to make it more visible.
<br>![TEXTTMP](https://user-images.githubusercontent.com/103794085/216776906-b0191685-5fb1-46bd-b64a-a6329fddad6e.png)
<br>11. Select the Scroll View in the *Hierarchy* and delete the *Image* and *Canvas Renderer* components. Drag *Text (TMP)* to the *Scroll Rect* *Content* area and set the *Anchors* and *Pivots* to those shown below.
<br>![ScrollView](https://user-images.githubusercontent.com/103794085/216777091-32a03182-ffcc-4630-8d91-3ec15bdfed18.png)
<br>12. In *Project/Assets* right click and create a new C# script. Name it whatever you wish but for the purposes of this walkthrough, we will name it 'Auth'.
<br>![Create](https://user-images.githubusercontent.com/103794085/216777152-0466c8de-2dfd-44c5-996c-f61d26fe18a0.png)
<br>13. Open the script in your favorite script editor. For the purposes of this walkthrough, we will use the Unity default *Visual Studio*. Then copy either the *Foundation Code* or the *Debugging Code* below.
</br>**[Back To Top](#Table-of-Contents)**
#### Foundation Code
```
using Firebase.Auth;
using GooglePlayGames;
using GooglePlayGames.BasicApi;
using UnityEngine;

public class Auth : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        PlayGamesPlatform.Instance.Authenticate(status =>
        {
            if (status == SignInStatus.Success)
            {
                PlayGamesPlatform.Instance.RequestServerSideAccess(true, code =>
                {
                    FirebaseAuth auth = FirebaseAuth.DefaultInstance;
                    Credential credential = PlayGamesAuthProvider.GetCredential(code);
                    auth.SignInWithCredentialAsync(credential).ContinueWith(task =>
                    {
                        if (task.IsCanceled)
                        {
                            // canceled
                        }
                        else if (task.IsFaulted)
                        {
                            // error  task.Exception
                        }
                        else
                        {
                            FirebaseUser newUser = task.Result;
                        }
                    });
                });
            }
        });
    }
}
```
</br>**[Back To Top](#Table-of-Contents)**
#### Debugging Code
```
using Firebase.Auth;
using GooglePlayGames;
using GooglePlayGames.BasicApi;
using System;
using System.Collections;
using TMPro;
using UnityEngine;

public class Auth : MonoBehaviour
{
    [SerializeField] TMP_Text textBox;

    // Start is called before the first frame update
    void Start()
    {
        try
        {
            textBox.text += "Authenticate";
            //Auth with Google Play
            PlayGamesPlatform.Instance.Authenticate(status =>
            {
                if (status == SignInStatus.Success)
                {
                    textBox.text += "\nSuccess\nRequestServerSideAccess";

                    try
                    {
                        //Ask for Auth code - This is why we need the Web Server Client ID's and secrets from Firebase
                        PlayGamesPlatform.Instance.RequestServerSideAccess(true, code =>
                        {
                            FirebaseAuth auth = FirebaseAuth.DefaultInstance;
                            Credential credential = PlayGamesAuthProvider.GetCredential(code);

                            //move Firebase get to Coroutine so we can log to our textbox
                            StartCoroutine(AuthGet());

                            IEnumerator AuthGet()
                            {
                                System.Threading.Tasks.Task<FirebaseUser> task = auth.SignInWithCredentialAsync(credential);

                                while (!task.IsCompleted) yield return null;

                                if (task.IsCanceled)
                                {
                                    textBox.text += "\ncanceled";
                                }
                                else if (task.IsFaulted)
                                {
                                    textBox.text += "\nerror " + task.Exception;
                                }
                                else
                                {
                                    FirebaseUser newUser = task.Result;
                                    textBox.text += "\n\nFULLY AUTHENTICATED\n\n";
                                    textBox.text += newUser.ToString();
                                }
                            }
                        });
                    }
                    catch (Exception e)
                    {
                        textBox.text += "RequestServerSideAccess error\n" + e.ToString();
                    }
                }
                else textBox.text += "Failure";
            });
        }
        catch (Exception e)
        {
            textBox.text += "Authenticate error\n" + e.ToString();
        }
    }
}
```
### Unity Setup 1 End
</br>**[Back To Top](#Table-of-Contents)**

### Unity Testing
Note: For the purposes of this walkthrough, we will use the **[Debugging Code](Debugging-Code)**. If you are just here for the code then this tutorial is finished.
<br>1. Back in the Unity Editor, right click on the *Hierarchy* and click *Create Empty* which creates an empty game object. We will name it *Auth* and drag our new *Auth* script onto it.
<br>![emptyAuth](https://user-images.githubusercontent.com/103794085/216778164-705d14cf-3af6-46e6-a6ab-c5a84ba20db9.png)
<br>2. Drag the *Text (TMP)* to *Auth* where it says *Text Box*.
<br>![AuthFinal](https://user-images.githubusercontent.com/103794085/216778216-6a04dbfb-eb62-4c37-9f6d-4fcfabada152.png)
<br>3. Click *File/Build and Run* or press *CTRL+B* at the same time and save the aab file under any name and in any folder. For the purposes of this walkthrough, we will create a new *Builds* folder and save the file as *GPGS.aab* there.
<br>![build&run](https://user-images.githubusercontent.com/103794085/216778363-d1aa0f4f-3634-48bb-84ae-38fd16b1efb7.png)
<br>![SAve](https://user-images.githubusercontent.com/103794085/216778322-2dd6cd70-7165-4248-9c51-da12975caf87.png)
<br>Note: Ensure that you have a mobile Android device with MIDI connection and Unity Remote 5 connected to your computer. You may even need to set the device in your project settings. An alternative is to build the .aab file and then transfer onto your mobile device then install it there.
#### Run Results
![RR](https://user-images.githubusercontent.com/103794085/216800339-755be4a7-40af-4fcd-a750-eef79a34b87a.png)
#### Run Results End
### Unity Testing End
