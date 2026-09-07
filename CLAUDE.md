# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a **Maven artifact repository** containing published Android library artifacts (AAR files), not a source code repository. It stores versioned releases of Bluetooth-related Android libraries for smart scales and body composition devices.

The repository is synced to GitHub at `git@github.com:LefuHengqi/PPBaseKit-Android.git` and serves as a local Maven repository that can be referenced by Android projects.

## Library Artifacts

The repository contains the following library families under `com.lefu`:

### Core Libraries
- **ppbluetoothkit** - Main Bluetooth communication library (latest: 4.6.23)
  - Depends on: `bluetoothkit:1.5.5`
  - Handles Bluetooth connectivity for smart scales
  
- **bluetoothkit** - Base Bluetooth library (v1.5.5, 1.5.6)
  - Foundation Bluetooth functionality

### Supporting Libraries
- **ppblebasekit** - BLE base functionality
- **ppdataanalysiskit** - Body composition data analysis
- **ppbasiccalculatekit** - Basic calculation utilities (two variants: main + cm)
- **ppcalculatekit** - Enhanced calculation kit
- **ppbasekit** - Base utility library
- **serialkit** - Serial communication (cm variant)

## Repository Structure

Standard Maven repository layout:
```
com/lefu/{artifactId}/{version}/
  ├── {artifactId}-{version}.aar        # Android library
  ├── {artifactId}-{version}.pom        # Maven metadata
  ├── *.md5, *.sha1, *.sha256, *.sha512 # Checksums
```

Each artifact directory also contains a `maven-metadata.xml` listing all available versions.

## Working with This Repository

### Publishing New Versions

When publishing a new library version, ensure:
1. Generate the AAR file with proper versioning
2. Create corresponding POM file with correct dependencies
3. Generate all checksum files (MD5, SHA1, SHA256, SHA512)
4. Update `maven-metadata.xml` with the new version and timestamp
5. Commit changes with descriptive message (preferably in Chinese based on git history pattern)

Example POM structure:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.lefu.ppbluetoothkit</groupId>
  <artifactId>ppbluetoothkit</artifactId>
  <version>X.Y.Z</version>
  <packaging>aar</packaging>
  <dependencies>
    <!-- Dependencies here -->
  </dependencies>
</project>
```

### Versioning Pattern

Libraries use semantic versioning with occasional patch levels:
- Major.Minor.Patch (e.g., 4.6.23)
- Sometimes Major.Minor.Patch.Fix (e.g., 4.6.0.1)

The ppbluetoothkit library has 70+ versions ranging from 4.0.1.7 to 4.6.23.

### Using These Artifacts in Android Projects

To consume these libraries in an Android project, add this repository to your build.gradle:

```gradle
repositories {
    maven { url 'file:///path/to/this/maven/repository' }
    // or for remote access:
    maven { url 'https://github.com/LefuHengqi/PPBaseKit-Android/raw/main/maven' }
}

dependencies {
    implementation 'com.lefu.ppbluetoothkit:ppbluetoothkit:4.6.23'
}
```

## Domain Context

Based on git history, these libraries support:
- Bluetooth communication with smart scales (体重秤)
- 8-electrode body composition devices
- User profile management (PPUserModel) with custom fonts
- Athlete mode functionality for 8-electrode devices
- Body composition data analysis and staging
- Serial port communication for specific scale models

Key models mentioned in commits:
- Torre/Borre/Dorre scales
- 577 8-electrode devices

## Git Workflow

Commit messages are primarily in Chinese. Recent changes focus on:
- Font styling fixes for user nicknames
- Adding `nameFont` field to PPUserModel
- Athlete mode activation logic for 8-electrode devices
- Bluetooth connection stability improvements
- Body composition data staging

When committing changes, follow the existing pattern of descriptive Chinese messages explaining what was added or fixed.
