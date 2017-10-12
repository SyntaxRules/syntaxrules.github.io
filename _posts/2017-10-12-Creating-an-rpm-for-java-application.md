# Creating an RPM for a Java Application

Herein lays an example of creating an RPM for Java Applications with Gradle.

## Overview

Creating a RPM that can run a Java application requires two steps. The first is to create a jar file that can be ran. The second is to create a RPM that installs this jar file and its dependecies on the target system. This certainly isn't the only way to do this, but it seems to be the easiest.

## Creating a runnable JAR file

There are many resources out there for creating a runnable JAR file. The Gradle application plugin will even create a jar for you out of the box. A regular JAR file isn't enough, you need a JAR file that also contains all of it dependecies. This kind of Jar file is often called a fat or uber JAR because of these extra dependecies. Luckly for us, a gradle plugin called **Shadow** takes care of this.

You can add shadow to your gradle file by adding the following lines to the beginning of your *.gradle file:

```
plugins {
    id 'com.github.johnrengelman.shadow' version '2.0.1'
}
```

Assuming you have the rest of your gradle set up to run your java application, you can immediately use Shadow after adding this line. Shadow adds a few gradle tasks, the one we are interested in is `gradle shadowJar`. See `gradle tasks` for all the exposed tasks shadow introduces.

Try it out. Run `gradle shadowJar` and look in your `build/libs` folder for the newly generated JAR file. you can run this jar file with `java -jar somefile.jar`.

## Creating an RPM package

To create an RPM package I used the `ospackage` gradle plugin. The plugin can be added to your gradle file by editing the plugins field we added in the last section. Modify it to look like:

```
plugins {
    id "nebula.ospackage" version "4.4.2"
    id 'com.github.johnrengelman.shadow' version '2.0.1'
}
```

Unlike the shadow plugin, ospackage requires the user to apply this plugin. I did so by adding the following line:

```
apply plugin: "nebula.ospackage"
```

ospackage doesn't know how to create an RPM specific to your project, it requires some extra configuration. See the [RPM packaging guide](http://rpm-guide.readthedocs.io/en/latest/rpm-guide.html) for information on how to configure it. Give it your best shot, here Is what I came up with:

```
ospackage {
    release '1.el7'
    user 'foo'
    permissionGroup "foo"
    summary 'Testing that RPMs can be created and ran using Java.'

    arch 'X86_64'
    os 'LINUX'
    type 'BINARY'

    from (shadowJar.outputs.files) {
        into "/opt/test"
    }

    from("scripts/rpmtest") {
        into "/opt/test"
        fileMode = 0755
    }

}

buildRpm {
    requires("some-dep", "0.2.7", GREATER | EQUAL)
    directory("/opt/test", 0755)
    link("/usr/bin/rpmtest", "/opt/test/rpmtest")
}
buildRpm.dependsOn(shadowJar)
```

There are a few things to point out in my configuration. First buildRpm.dependsOn(shadowJar). This is required so you can copy the JAR that shadow creates into your RPM. Second, I had to create a script to acutally run my fat JAR. This script is really simple, it just runs:

```
#!/usr/bin/env sh

java -jar /opt/test/rpmtest-*
```

After I finished this configuration I tested this approach by installing the rpm and attempting to run it. After a few permissions tweaks and trial and error, I got it running with the solution above.

## References

- [Creating Unix Services and RPM/DEB Packages with Spring Boot and Gradle](https://www.ccampo.me/java/spring/linux/2016/02/15/boot-service-package.html)
- [Ccampo Example Application](https://github.com/ccampo133/boot-daemon-demo)
- [Gradle ospackage RPM documentation](https://github.com/nebula-plugins/gradle-ospackage-plugin/wiki/RPM-Plugin)
- [Shadow (fat) jar documentation](http://imperceptiblethoughts.com/shadow/)
- [RPM packaging guide](http://rpm-guide.readthedocs.io/en/latest/rpm-guide.html)
