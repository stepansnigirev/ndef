# NDEF playground

Javacard applet for NDEF

Currently all the applets are tested on [NXP JCOP3 J3H145 card](https://www.smartcardfocus.com/shop/ilp/id~879/nxp-j3h145-dual-interface-java-card-144k/p/index.shtml).

## Applets

- [NDEF Static](./docs/static.md) - static data stored in the applet.

# Toolchain installation

JDK8 works. The most recent one doesn't.

Big thanks to https://adoptopenjdk.net/ for all old versions of jdk!

Install deps:

## MacOS

```sh
brew tap adoptopenjdk/openjdk
brew cask install adoptopenjdk/openjdk/adoptopenjdk8
brew install ant@1.9
```

Add to your path (maybe put into `.bash_profile`):

```sh
export PATH="/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home/bin/:$PATH"
export PATH="/usr/local/opt/ant@1.9/bin:$PATH"
export JAVA_HOME="/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home"
```

## Linux

```sh
sudo apt install openjdk-8-jdk
sudo apt install ant
```

Install the smartcard service:

```sh
sudo apt install pcscd
```

# Tools

- `gp.jar` - a working and easy to use tool for applets management, by [martinpaljak](https://github.com/martinpaljak/GlobalPlatformPro) (LGPL3)
- `ant-javacard.jar` - ant task to build javacard applet, by [martinpaljak](https://github.com/martinpaljak/ant-javacard) (MIT)
- `sdks` folder - submodule with JavaCard SDKs of different versions (Oracle-owns-you-and-your-grandma license)

It's convenient to make an alias for `gp.jar`:

```sh
alias gp="java -jar $PWD/gp.jar"
```

# How to build

Make sure to clone recursively or run `git submodule update --init --recursive` if you have an error "No usable JavaCard SDK referenced"

Run to compile all applets:

```sh
ant all
```

You should get `.cap` files for all the applets in the `build/cap` folder.

Run to compile a specific applet:

```sh
ant NDEFStatic
```

To see the build targets:

```sh
ant -projecthelp
```

Now upload applet to the card:

```sh
gp --install build/cap/NDEFStatic.cap
```

Check that it appeared in the list of applets (should appear with aid `???`):

```sh
gp -l
```

Now the applet is on the card and ready to use.

Check out [tests](./tests/tests) folder to get an idea how to communicate with the card.

# Useful links

- https://opencryptojc.org/ - making JavaCards open
- https://pyscard.sourceforge.io/ - python tool to talk to smartcards
- https://smartcard-atr.apdu.fr/ - ATR (Answer To Reset) parser
- https://www.youtube.com/watch?v=vd0-Uhx2OoQ - nice talk about JavaCards and open-source ecosystem

