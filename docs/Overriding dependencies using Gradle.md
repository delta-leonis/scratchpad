# Overriding dependencies using Gradle

While developing on zosma and it's related libraries it is very common to have gradle dependencies on eachother. This document describes how to make gradle use your local version for a dependency instead of a published one.

### Directory structure

This document assumes the following structure:

```bash
xxx:robocup thumbnail95$ tree -L 2 -P *.gradle
.
├── algieba
│   ├── build.gradle
│   └── settings.gradle
├── subra
│   ├── build.gradle
│   └── settings.gradle
└── zosma
    ├── build.gradle
    └── settings.gradle
```

As an example we'll override the `zosma` dependency in `subra` to use our local directory.

### Include zosma as a dependency

We need to add `zosma` as an dependency to make gradle compile it with the project. First, include zosma and set the project directory by appending the following to `subra/settings.gradle`:

```groovy
include ':zosma'
project(':zosma').projectDir = new File(settingsDir, '../zosma')
```

Add `zosma`  to `subra/build.gradle` to make sure `zosma` is compiled as a dependency:

```groovy
dependencies {
  compile project(':zosma')
}
```

