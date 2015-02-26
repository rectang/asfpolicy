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

## Release content ### {#release-content}

### Official releases ### {#official-releases}

The content of official Apache releases and the process by which valid
releases are created is governed by Apache [Release
Policy](http://www.apache.org/dev/release).

### Binary packages ### {#binary-packages}

Release Policy [specifies](http://www.apache.org/dev/release#what) that binary
packages provided by third parties which meet certain criteria may be
distributed alongside official source packages.  Such packages are sometimes
referred to as "convenience binaries" to distinguish them from other binary
packages.

### Developer packages ### {#dev-packages}

Developer packages contain unreleased code, in either original or derived
form.

## Public distribution ## {#public-distribution}

All official releases MUST be uploaded to `www.apache.org/dist`.

Content suitable for the canonical distribution channel includes:

*   Official releases
*   "Convenience binaries"
*   Cryptographic signatures and checksums
*   A `KEYS` file containing the public key signatures of the release managers
    (and optionally other committers) for the project.
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

### Pre-upload notification ### {#heads-up}

Most projects can just distribute a release as described in the previous two
questions.  However, releases that are likely to strain the mirroring and
download resources **must** be coordinated with infrastructure.

Releases of more than 1GB of artifacts require a heads-up to Infrastructure in
advance.

Specific exemptions from other dist policies (such as what may or must or must
not be distributed via the mirrors) also need to be coordinated with Infrastructure.

## Release signing ### {#release-signing}

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

### PGP Signatures ### {#pgp}

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

### Checksums ### {#checksums}

Please note that further use of `SHA-1` should be [avoided](#sha1).

`SHA256` and `SHA512` use the same `SHA` algorithm family with longer hash
lengths (256 and 512 bits respectively). These longer variations are less
vulnerable to the weaknesses found in the algorithm family than `SHA1`.
SHA512 is [recommended](#sha1).

## Download links {#download-links}

Current releases must be served from the ASF mirroring system by placing them under
`http://www.apache.org/dist/`.  (How to upload releases to the `dist/`
tree is [explained](#upload-scp) [below](#upload-ci).) 

Project download
pages must link to the mirrors and not to the main Apache Web site; see
[instructions for creating download pages](release-download-pages) for
fuller details. 
The website documentation for the software must contain a link to the download page for the source.

Project websites (`http://{project}.apache.org`),
VMs (`http://{project}.zones.apache.org` and `http://{project}-vm.apache.org`),
and source control repositories (`svn.apache.org` and Git repositories)
may not be used to distribute releases --- that is, releases should not be
downloaded from them.

- All links to the mirrored distribution artifacts **must not** reference
the main Apache web site. They *should* use the standard mechanisms to
distribute the load between the mirrors.

- All links to checksums, detached signatures and public keys **must**
reference the main Apache web site and *should* use https:// (SSL).

- Old releases *should* be [archived](release.html#how-to-archive) and may
be linked from the download page.

- Artifacts which are not full official releases (for example, milestones,
betas and alphas) may be linked from the download page. Links to these
artifacts should be removed in a timely fashion.

Links to the checksum and signature for the artifact should be given next
to the download link. It is important that users check the sum and verify
the signature so these links should be close and clear. **Note:** these
documents *must not* be mirrored.

## Release archival ## {#archival}

All releases must be archived on <http://archive.apache.org/dist/>.

An automated process adds releases to the archive about a day after
they first appear on to <http://www.apache.org/dist/>.
Once a release
is placed under `http://www.apache.org/dist/` it will automatically be copied over
to `http://archive.apache.org/dist/` and held there permanently, even after it is deleted
from `http://www.apache.org/dist/`.

If you have (legacy?) releases that never got archived, 
ask infra to copy them to `http://archive.apache.org/dist/`.

`/www.apache.org/dist` should contain *the latest release in each branch 
that is currently under development*. When development ceases on a version 
branch, releases of that branch should be removed from `/dist`.

(If the project uses svnpubsub, 
this is done by deleting the artifacts from 
`https://dist.apache.org/repos/dist/release/<TLP name>/`.)

For example, if Apache Foo 1.2.x is a newer release in the same line as 
Foo 1.1.a, then 1.1.a should be removed when 1.2.x is released.
Note that all releases are automatically archived,
see [How Is An Old Release Moved To The Archives](#how-to-archive)

If Apache Foo 1.2 is a new branch, and development continues on 1.1 in 
parallel, then it is acceptable to serve both 1.1.a and 1.2.x from `/dist`.

`/www.apache.org/dist` is automatically archived. Therefore, a copy of an
official release will already exist in the archives. To move a release to
the archives, just delete the copy in `/www.apache.org/dist`. Remember to
update any links from the download page.

## Downstream distribution {#downstream}

### Maven {#maven}

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
