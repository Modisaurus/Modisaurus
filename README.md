# How to make debian files in a repo

## How It Works
Okay, so now you've downloaded the thing and it's a folder with a bunch of random files in it that make absolutely no sense whatsoever. Now what?! Here's what. You see you unroll it, then you stick it i&mdash; whoops.

Never mind that, the first thing you need to understand is how these debian things work. To start, Cydia, as you probably already know now, is the main program created by /u/saurik for jailbroken iOS devices for easy and quick access to the tweaks and themes that you want. You probably have never thought of how Cydia does this, unless you're into that sort of stuff. Cydia basically to put it into laymon terms, uses Debian packages to download and install these tweaks. Debian packages, more commonly known as the .deb files that Debian uses, are basically advanced .zip files, like Java JARs, also known as .jar files. Debian reads these special .zip files and installs them accordingly with information found in the package's control file. This control file is put into a special location inside the .deb file.

As an example, I have one .deb file in this repository that is already fully packaged and ready to be downloaded in Cydia. If you crack this .deb file with your favourite uncompresser (7-Zip for the win), you will see two folders. A folder marked `DEBIAN`, and a folder marked `var`.

The folder marked `DEBIAN` is the folder that contains the control file, which is called `control`. Bet you didn't see that coming. (I'm so good at jokes! Hehehe... heh....) The control file contains many fields that have specific information that Debian reads when installing the package. We'll get into that in a bit.

The folder marked `var` is where you want your files for your tweak or theme to go. I have no prior experience for tweaking, seeing as I don't own a Mac, but for themers such as myself, the place to put your average theme would be at `/Library/Themes/`. This would mean to make a folder called `Library`, and then a folder called `Themes` inside of that, in your package folder. The reason why the folder in this case is called `var`, is because I'm installing a test file to `/var/mobile/Documents/`. But I'm pretty sure you get the idea.

## The control file
The control file is made up of several fields. I'm going to cover the main ones you will be using. Inside the package folder, which in this case, is called `Package` (I'm no longer inside the example .deb file anymore if you didn't know.), is a `DEBIAN` folder, and inside that is the control file. Crack this puppy open, and you will see several fields. The fields you see should look similar to the ones below.

```markdown
Package: net.winneonsword.package
Name: Test Package
Version: 1.0
Architecture: iphoneos-arm
Description: This is a test package from /u/WinneonSword's tutorial repository!
Depiction: http://repo.winneonsword.net/packages/package.html
Homepage: http://repo.winneonsword.net
Maintainer: Jesse Bryan <winneonsword@gmail.com>
Author: Jesse Bryan <winneonsword@gmail.com>
Section: Themes
```

Let's go down the line and explain what each one means.

* **Package:** This is the name of your package. If you're not familiar with programming, the package name is usually where most of the files the program code relates to goes. The way to name this is like so: `[prefix of your website].[name of your website].[name of package]`. For example, mine says `net.winneonsword.packge`. The `net` is the prefix of my website, the `winneonsword` is the name of my website, which both together puts winneonsword.net, which is my website, and the last part, the `package` is the name of the package. For example's sake, it's just called package in this tutorial.
* **Name:** This is what will show as the name when you are looking at your package in Cydia. You know, the big bold text that is the main attraction.
* **Version:** This is the version of your package. Versioning is something to get into the habit of. The way I do it though, is if it is a initial release, then it obviously is version 1.0. If it is a minor change, then I add a number to the 3rd digit, which in this case would turn into 1.0.1. If it was a major change, then I would add a number to the 2rd digit and remove the 3rd, which would turn into 1.1. Get it?
* **Architecture:** This is the type of the package. **Don't change this.**
* **Description:** This is the description of your package. This text section will appear under entries in Cydia in a list view, or if there is no depiction for the file (below), when viewing the package itself in the dotted-line division area.
* **Depiction:** This is the webpage that pops up when viewing the package itself in Cydia. This part is optional, and should only be used if you know what you are doing around mobile web development. Keep in mind, that if you have a depication specified, the description of the package will *not* show up when viewing the package directly in Cydia.
* **Homepage:** This part is pretty obvious; it's the package's homepage, or mainly your website's homepage.
* **Maintainer:** This is the person who is currently maintaining the package you are making. To put the person's email, enclose it in tag symbols, like so: `<winneonsword@gmail.com>`. This is shown in the above example.
* **Author:** This is the person who originally created the package you are maintaining. This often is the same as the Maintainer.
* **Section:** Last but not least, this is the Section that the package will go under when you view the section view in Cydia. Pretty straightforward, eh?

## Making Your Packages and Sending Them Off
This is reaching the end of this tutorial, so now to conclude the repository making process. Below are step by step instructions on how to make your packages into .deb files, and then send it off to a Git based system, in this case, will be GitHub.

1. Update your packages.sh file. To do so, crack open the packages.sh file, and you should see `dpkg-deb -b Package`. Repeat this pattern for every package that your have in your repository, so if you were to have 3 packages, the packages.sh file should look like so. Keep in mind that the name of the package is the same as the folder name in the repository.

    ```markdown
    dpkg-deb -b Package
    dpkg-deb -b Package2
    dpkg-deb -b Package3
    ```

2. Run the update.sh file in your terminal by typing `./update.sh`. If you get an error mid-way, run this command: `chmod +x packages.sh && chmod +x remove.sh && chmod +x update.sh`. Then, run the file again.
3. Now that you have all of your .debs properly built, you need to send the files along with the Packages.bz2 to the Git repository of your choice. If you are not using GitHub, you are done with these steps. Otherwise, create a GitHub repository on the [GitHub website](https://github.com/) with *this name:* `[your github username].github.com`. Replace the [your github username] part with your actual GitHub username. **This is very important.**
4. Now, in your favourite terminal full of rainbows and sparkles and glitter and ponies and all that neat stuff, type the following set of commands in the repository directory:

    ```markdown
    git init
    git remote add origin https://github.com/[your github username]/[your github username].github.com.git
    git add --all
    git commit -m "[Put a creative name for this commit here.]"
    git push origin master
    ```

5. ????????????
6. Congratulations! You may have your PROFIT you've been waiting for. Your repository should now be up and running at `http://[your github username].github.com/`! Add that web address to your Cydia sources and behold your packages should appear!

## Conclusion
Thank you for listening for my ongoing blabber about Debian and how things work. This method is how you would get an actual repository up and running without using myrepospace or any similar service. This method also allows full control over all of your packages to your hearts content, and it allows a neat and clean way to redirect the web address to your custom domain of your choice, using GitHub's CNAME system. (I will not be going into that in this tutorial. Sorry!) I hope you enjoyed this tutorial, and farewell!

&mdash; /u/WinneonSword
