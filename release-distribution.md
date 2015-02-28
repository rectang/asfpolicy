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

The Apache Software Foundation's official channel for distribution of current
Apache software releases to the general public is `www.apache.org/dist`.  It
is augmented by the ASF mirror network.

The public may also obtain Apache software from any number of downstream
channels which redistribute our releases in either original or derived form.
The vast majority of such downstream channels operate independently of Apache.

Infrastructure maintains a number of developer-only channels which facilitate
distribution of unreleased software to consenting members of a development
community.

Finally, all historic Apache releases may be obtained from
`archive.apache.org`.

## Release Distribution Directory ## {#dist-dir}

Every top-level project at Apache has its own public distribution directory,
which is a subdirectory of `www.apache.org/dist`.  The PMC is responsible for
all artifacts within their distribution directory.

## Release Content ## {#release-content}

The content of official Apache releases and the process by which valid
releases are created is governed by Apache [Release
Policy](http://www.apache.org/dev/release).

Release Policy [specifies](http://www.apache.org/dev/release#what) that binary
packages provided by third parties which meet certain criteria may be
distributed alongside official source packages.  Such packages are sometimes
referred to as "convenience binaries" to distinguish them from other binary
packages.

## Public Distribution ## {#public-distribution}

All official releases MUST be uploaded to the official distribution channel,
`www.apache.org/dist`.

Content suitable for the official distribution channel includes:

*   Official releases
*   "Convenience binaries"
*   Cryptographic signatures and checksums
*   The [KEYS](#sigs-and-sums) file
*   `README`, `CHANGES` and similar documents describing distributed
    content

If an Apache PMC wishes to publish additional materials through the official
distribution channel and there is any question about the suitability of said
materials, the PMC MUST consult with the Board.

## Distribution of Unreleased Materials ## {#unreleased}

Unreleased materials, in original or derived form...

*   MUST NOT be distributed through `www.apache.org/dist`.
*   MUST NOT be distributed through channels which encourage use by anyone
    outside the project development community.
*   MUST NOT be advertised to anyone outside of the project development
    community.
*   MAY be distributed to consenting members of a development community.

## Pre-upload Notification ## {#heads-up}

Releases of more than 1GB of artifacts MUST be coordinated with Infrastructure
in advance, in order to mitigate strain on mirroring and download resources.

## Cryptographic Signatures and Checksums ## {#sigs-and-sums}

Every artifact distributed by the Apache Software Foundation  *must* be
accompanied by one file containing an [OpenPGP
compatible ASCII armored detached signature](#openpgp-ascii-detach-sig) and
another file containing an [MD5 checksum](#md5). The names of these files
*must* be formed by adding to the name of the artifact the following
suffixes:

- the signature by suffixing `.asc` 

- the checksum by suffixing `.md5` 

An [SHA](#sha-checksum) checksum *should* also be created and *must* be
suffixed `.sha`.

Release managers *must not* store private keys used to sign Apache releases
on ASF hardware.

The private key *must not* be store on any ASF machine. So, signatures
*must not* be created on ASF machines.

Sensitive operations using a private key *must not* be executed on ASF
hardware.

The files that make up an Apache release are **always** accompanied by
cryptographic signatures.

It is vital that hash, signature and KEYS files are only downloaded from ASF hosts.
So the following files are excluded from synchronisation:

*.md5 *.MD5 *.sha1 *.sha *.sha256 *.sha512 *.asc *.sig KEYS KEYS.txt MD5SUM SHA*SUM

MD5SUM and SHA*SUM must look like the output of md5sum(1): lines containing
a checksum, followed by a filename ; use only plain filenames (no slashes).

Do not use any other file names for such files.

The source package must be
[cryptographically signed](/dev/release-signing.html) by the Release
Manager with a detached signature; and that package together with its
signature must be tested prior to voting +1 for release. Folks who vote +1
for release may offer their own cryptographic signature to be concatenated
with the detached signature file (at the Release Manager's discretion)
prior to release.

Now that there is doubt about the medium term security of [SHA-1](#sha1) ,
the DSA keys and 1024 bit RSA keys (which depend on this algorithm) should
be avoided for new keys. It is uncertain whether 2048 bit RSA keys will be
strong enough to remain secure until [SHA3](#sha3) (and the next generation
of standards) arrives. It is therefore recommended that new keys should be
at least 4096 bit RSA (the longest widely supported key length).

Keys used at Apache should be available through the global [public
keyserver](release-signing.html#keyserver) network. 

Projects maintain [KEYS](release-signing.html#keys-policy) files containing
the public keys used to sign Apache releases. These documents need not be
updated immediately, but they **MUST** be updated with an export before any
release is published using the new key.

It is vital that Apache code signing keys are linked into a strong [web of
trust](release-signing.html#web-of-trust). This allows independent
verification of the fidelity of Apache releases by anyone strongly linked
to this web. In particular, this enables to two important groups to
independently verify releases:

- The Apache Infrastructure Team
- Downstream packagers

The Apache web of trust is reasonably well connected to the wider open
source web of trust. So though every opportunity should be taken to link
into wider networks the most important action needs to be to plan to
exchange signatures with other Apache committers.

If your key has been compromised then you **MUST NOT** transition but
[revoke](#revoke-key) the old key and replace with a new one immediately.
**DO NOT** use a transition period.

If your key has been compromised, you **MUST NOT** use a transition period.
You should immediately [revoke](release-signing.html#revoke-key) the
compromised key and [create a new one](openpgp.html#generate-key). All [web
of trust](release-signing.html#web-of-trust) links signed by the old key
should be regarded as suspect. A completely new set of links **MUST** be
re-established by meeting [in
person](release-signing.html#key-signing-party).

All web of
trust links signed by the old key should be regarded as suspect. A completely
new set of links MUST be re-established by meeting in person.

- Committers with a DSA key or an RSA key of length less than 2048 bits
should generate a new key for signing releases. The original key does not
need to be revoked yet. Follow this [guide](key-transition.html).

- Committers with RSA keys of length 2048 or more do not need to generate a
new key yet. They should reconfigure their client to avoid the weakness by
following these [instructions](openpgp.html#sha1) and wait for the next
major OpenPGP revision.

Signatures should be [ASCII armored and
detached](#openpgp-ascii-detach-sig).

Your [public key](#public-private) should be [exported](#export) and the
result appended to the appropriate<code> [KEYS](#keys-policy)
</code>file(s).

Please note that further use of `SHA-1` should be [avoided](#sha1).

`SHA256` and `SHA512` use the same `SHA` algorithm family with longer hash
lengths (256 and 512 bits respectively). These longer variations are less
vulnerable to the weaknesses found in the algorithm family than `SHA1`.
SHA512 is [recommended](#sha1).

## Download Links ## {#download-links}

The website documentation for any Apache product MUST provide public download
links where current official source releases and accompanying cryptographic
files may be obtained.

All links to mirrored distribution artifacts MUST NOT reference the main
Apache web site. They SHOULD use the standard mechanisms to distribute the
load between the mirrors.

All links to checksums, detached signatures and public keys MUST
reference the main Apache web site and SHOULD use `https://` (SSL).

Old releases SHOULD be [archived](#archival) and MAY be linked from public
download pages.

## Release Archival ## {#archival}

All releases MUST be archived on `archive.apache.org`.  This generally happens
via an automated process which adds releases to the archive about a day after
they first appear on `www.apache.org/dist`.

Each project's [distribution directory](#dist-dir) SHOULD contain the latest
release in each branch that is currently under development.  When development
ceases on a version branch, releases of that branch SHOULD be removed.

## Maven ## {#maven}

In addition to the distribution directory, project that use Maven or
a related build tool sometimes place their
releases on `repository.apache.org` beside some convenience binaries. 
The distribution directory is required, 
while the repository system is an optional convenience.

Apache operates a repository manager at https://repository.apache.org/. It can
be used by Apache projects for deploying snapshots, releases, or both. See the
Publishing Maven Releases guide for more details.

The *snapshot* repositories are for interim *snapshot* releases and the
*ibiblio* repositories are for releasing via rsync to the 'central' Maven
repository.

## Policy Administration ## {#administration}

Changes to Release Distribution Policy MUST be approved by the V.P. of Apache
Infrastructure.

----------------

# Release Distribution FAQ # {#faq}

TODO
