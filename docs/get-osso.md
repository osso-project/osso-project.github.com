---
title: Using Osso
layout: page
---

Osso may be used in your project in a few different ways.

* Contents
{:toc}

The latest version of Osso is **{{ site.osso-version }}**.

## Using Osso with Maven

To use Osso with a Maven-managed project, add the following to your project
`pom.xml` file.

```xml
<repositories>
  <repository>
    <id>osso-releases</id>
    <url>{{ site.osso-mvn-repo-releases }}</url>
  </repository>
  <repository>
    <id>osso-snapshots</id>
    <url>{{ site.osso-mvn-repo-snapshots }}</url>
  </repository>
</repositories>

<dependencies>
  <dependency>
    <groupId>{{ site.osso-mvn-groupid }}</groupId>
    <artifactId>{{ site.osso-mvn-artifactid }}</artifactId>
    <version>{{ site.osso-version }}</version>
  </dependency>
</dependencies>
```

## Using Osso with Gradle

To use Osso with a Gradle-managed project, add the following to your
`build.gradle` build file.

```gradle
repositories {
  maven {
    name 'osso-releases'
    url '{{ site.osso-mvn-repo-releases }}'
  }
  maven {
    name 'osso-snapshots'
    url '{{ site.osso-mvn-repo-snapshots }}'
  }
}

dependencies {
  compile group: '{{ site.osso-mvn-groupid }}', name: '{{ site.osso-mvn-artifactid }}', version: '{{ site.osso-version }}'
}
```

## Direct Downloads

In addition to the Maven artifacts, it is possible to directly download both
source and binary distributions of Osso releases from the Github Releases
section of the project page.

[All Releases]({{ site.github-osso }}/releases )
