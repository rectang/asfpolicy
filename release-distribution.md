Title: Release Distribution Policy
Notice:    Licensed to the Apache Software Foundation (ASF) under one
           or more contributor license agreements.  See the NOTICE file
           distributed with this work for additional information
           regarding copyright ownership.  The ASF licenses this file
           to you under the Apache License, Version 2.0 (the
           "License"); you may not use this file except in compliance
           with the License.  You may obtain a copy of the License at
           .
             http://www.apache.org/licenses/LICENSE-2.0
           .
           Unless required by applicable law or agreed to in writing,
           software distributed under the License is distributed on an
           "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
           KIND, either express or implied.  See the License for the
           specific language governing permissions and limitations
           under the License.

# Contents #

[TOC]

----------------

# Release Distribution Policy # {#policy}

This policy governs the distribution of Apache software releases
through channels maintained by Apache Infrastructure.  It complements Apache
[Release Policy](http://www.apache.org/dev/release), which governs how to
create releases.

## Release Distribution Channels ## {#channels}

The ASF's official channel for distribution of current Apache software
releases to the general public is `www.apache.org/dist`, augmented by the
Apache mirror network.

The public may also obtain Apache software from any number of "downstream"
channels which redistribute our releases in either original or derived form.
The vast majority of such downstream channels operate independently of Apache.

Apache Infrastructure maintains certain "developer" distribution channels
which facilitate distribution of unreleased software to consenting members of
a development community.

Finally, all historic Apache releases may be obtained from archive.apache.org.

## Release distribution directory ## {#dist-dir}

Every top-level project at Apache has its own public distribution directory,
which is a subdirectory of `www.apache.org/dist/`.  The PMC is responsible for
all artifacts within their distribution directory.

## Release content ## {#release-content}

The content of _official releases_ and the process by which valid
releases are created is governed by Apache [Release
Policy](http://www.apache.org/dev/release).

Release Policy [specifies](http://www.apache.org/dev/release#what) that binary
packages provided by third parties which meet certain criteria may be
distributed alongside official source packages.  Such packages are sometimes
referred to as _"convenience binaries"_ to distinguish them from other binary
packages.

_Developer packages_ contain unreleased code, in either original or derived
form.

## Public distribution ## {#public-distribution}

All official releases MUST be uploaded to `www.apache.org/dist`.

Content suitable for the canonical distribution channel includes:

*   Official releases
*   "Convenience binaries"
*   Cryptographic signatures and checksums
*   The [KEYS](#sigs-and-sums) file
*   `README`, `CHANGES` and similar documents describing distributed
    content

If an Apache PMC wishes to publish additional material through the canonical
distribution channel and there is any question about its suitability, the PMC
MUST consult with the Board.

## Distribution of developer packages ## {#dev-distribution}

Developer packages MUST NOT be distributed through `www.apache.org/dist`.

Developer packages MUST NOT be advertised to anyone outside of the project
development community.

Developer packages MAY be distributed to consenting members of a development
community through development channels such as
`dist.apache.org/repos/dist/dev`, `builds.apache.org` and so on.

## Pre-upload notification ## {#heads-up}

Releases of more than 1GB of artifacts MUST be coordinated with Infrastructure
in advance, in order to mitigate strain on mirroring and download resources.

## Cryptographic signatures and checksums ## {#sigs-and-sums}

Every artifact distributed to the public through Apache channels MUST be
accompanied by one file containing an [OpenPGP compatible ASCII armored
detached signature](release-signing#openpgp-ascii-detach-sig) and another file
containing an [MD5 checksum](release-signing#md5). The names of these files
MUST be formed by adding to the name of the artifact the following suffixes:

- the signature by suffixing `.asc` 
- the checksum by suffixing `.md5` 

An [SHA](release-signing#sha-checksum) checksum SHOULD also be created and
MUST be suffixed `.sha`.  The checksum SHOULD be generated using `SHA512`.

Projects MUST publish a "[KEYS](#release-signing#keys-policy)" file in their
distribution directory which contains all public keys used to sign artifacts.

Signing keys used at Apache MUST be published in the KEYS file and SHOULD be
available through the global [public keyserver](release-signing#keyserver)
network.  Signing keys SHOULD be linked into a strong [web of
trust](release-signing#web-of-trust).

Keys used to sign new artifacts MUST be RSA and at least 2048 bit.  Any new
keys SHOULD be 4096 bit RSA.

Private keys MUST NOT be stored on any ASF machine. So, signatures
MUST NOT be created on ASF machines.

Compromised signing keys MUST be revoked and replaced immediately.

## Download links ## {#download-links}

The website documentation for any Apache product MUST provide public download
links where current official source releases and accompanying cryptographic
files may be obtained.

All links to mirrored distribution artifacts MUST NOT reference the main
Apache web site. They SHOULD use the standard mechanisms to distribute the
load between the mirrors.

All links to checksums, detached signatures and public keys MUST
reference the main Apache web site and SHOULD use `https://` (SSL).

Old releases SHOULD be [archived](#archival) and MAY be linked from the
download page.

## Release archival ## {#archival}

All releases MUST be archived on `archive.apache.org`.  This generally happens
via an automated process which adds releases to the archive about a day after
they first appear on `www.apache.org/dist`.

Each project's [distribution directory](#dist-dir) SHOULD contain the latest
release in each branch that is currently under development.  When development
ceases on a version branch, releases of that branch SHOULD be removed.

## Maven ## {#maven}

Infrastructure operates an Apache Maven repository manager at
[repository.apache.org](https://repository.apache.org/).  Projects MAY
use the repository system as a downstream channel to redistribute released
materials, and MAY use it as a developer channel to make SNAPSHOTs available
to consenting members of the project development community.

## Policy Administration ## {#administration}

Changes to Release Distribution Policy MUST be approved by the V.P. of Apache
Infrastructure.

----------------

# Release Distribution FAQ # {#faq}

TODO
