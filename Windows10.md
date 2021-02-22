All credit for the information here goes to [lambdaheart](https://github.com/lambdaheart) for [the excellent guide](https://github.com/lambdaheart/Haskell-Guide/blob/master/DevelopmentEnvironment.md), of which this is just a condensed and more bare-bones version.

-----------------------------------------------------

# INSTALLER - For if you want to use chocolatey (note: don't use this method of installation until this issue is closed https://github.com/haskell/haskell-language-server/issues/1372):

Follow [the Haskell Platform Windows installation instructions](https://www.haskell.org/platform/windows.html).


# MANUAL - For if you don't want to use chocolatey. Skip this if you followed the step above

Make a new folder called `Haskell` in your `C:\Users\{YourName}` folder.

Create two new folders inside your `Haskell` folder called:
* `GHC`
* `Cabal`

You should now have the folders `.\Haskell\GHC` and `.\Haskell\Cabal`.

Download and extract to your `.\Haskell\GHC` folder: https://www.haskell.org/ghc/download_ghc_8_10_3.html (scroll down until you find the Windows binary package)
Make sure to extract from the folder under the version. So extract the contents of the `ghc-8.10.3` folder, not the `ghc-8.10.3` folder itself.

In your `GHC` folder, you should now have the following folders:
* `bin`
* `doc`
* `lib`
* `man`
* `mingw`

Download and unzip the "[cabal-install tool](https://www.haskell.org/cabal/download.html)" (Binary download for Windows (x86-64)).
Make sure to extract from the folder under the version. So extract the contents of the `Cabal-3.2.0.0` folder, not the `Cabal-3.2.0.0` folder itself.
In your Cabal folder, you should now have `cabal.exe` and `cabal.exe.sig`

Now, add these to your system path. If you don't know how to do this, refer to the section below (note: replace `{YourFullPath}` with the root folder of your Haskell folder, like `C:\Users\Will`):
* `{YourFullPath}\Haskell\Cabal`
* `{YourFullPath}\Haskell\GHC\bin`

To add an item to your system path:
* Type "environment" into your Windows search bar and select "Edit the system environment variables"
* Click the "Environment Variables" button
* Under "System variables", scroll down until you find "Path". Select it and click "Edit"
* Click "New"
* Enter the desired directory (e.g. `C:\Users\Will\Haskell\Cabal`) and hit OK
* Enter the next desired directory (e.g `C:\Users\Will\Haskell\GHC\bin`) and hit OK
* Hit "OK" on the "Environment Variables window"
Note: If you don't hit "OK" on the last step it won't be saved, so our next test won't work


# GHC AND CABAL INSTALL TEST

To test that we were successful, open a new PowerShell or cmd (a new instance is important because the environment variables need to be updated) and type:
* `ghc --version`
* `cabal --version`

You should see version information like:

```
The Glorious Glasgow Haskell Compilation System, version 8.10.3
```

and

```
cabal-install version 3.2.0.0
compiled using version 3.2.0.0 of the Cabal library
```

Run `cabal update`

# MSYS2

Next, we need to install MSYS2 from https://www.msys2.org/ (follow the instructions on that page).

Add the following directories to your system path:
* `C:\msys64\mingw64\bin`
* `C:\msys64\mingw32\bin`
* `C:\msys64\usr\bin`

To add an item to your system path:
* Type "environment" into your Windows search bar and select "Edit the system environment variables"
* Click the "Environment Variables" button
* Under "System variables", scroll down until you find "Path". Select it and click "Edit"
* Click "New"
* Enter the desired directory (i.e. `C:\msys64\mingw64\bin`) and hit OK
* Enter the next desired directory (i.e. `C:\msys64\mingw32\bin`) and hit OK
* Enter the next desired directory (i.e. `C:\msys64\usr\bin`) and hit OK
* Hit "OK" on the "Environment Variables window"
Note: If you don't hit "OK" on the last step it won't be saved, so our next test won't work

You can now access packages via PowerShell.

If you already had PowerShell open, close it and open a new window, then:
* run the following command: `pacman -S mingw-w64-x86_64-toolchain`
* press enter to select the default choice
* enter `y`
* run `pacman -S mingw-w64-x86_64-pkg-config`
* say yes if it asks for confirmation

Now run:
* `which pkg-config`

We should get the output: `/mingw64/bin/pkg-config`

Next, to check that we're all set up, we'll test our ability to install packages. Run the following commands:

* `pacman -S mingw-w64-x86_64-cairo`
* `cabal new-install cairo --lib`

If this succeeds, we're still on track.


# VS CODE AND LANGUAGE SERVER:

Finally, to set up your development environment:
* Download and install Visual Studio Code from https://code.visualstudio.com/download 
* Open Visual Studio Code
* Navigate to the "Extensions" tab
* Type "Haskell" in the search bar
* Select the "Haskell" extension. It should be the top option. This will automatically install the language server and provide intellisense.

Create a new project by executing the following command in a new folder called Test:

* `cabal init`

Open the Test folder in VS Code and check that your language server extension is working correctly by mousing over a type in `Main.hs`.

If some reasonable looking information is displayed, congratulations! You're all set.
