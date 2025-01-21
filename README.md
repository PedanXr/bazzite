<p align="center">
  <a href="https://bazzite.gg/"><img src="/repo_content/Bazzite_Tagline.svg?raw=true" alt="Bazzite"/></a>
</p>

[![build-bazzite](https://github.com/ublue-os/bazzite/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/bazzite/actions/workflows/build.yml) [![build-bazzite-isos](https://github.com/ublue-os/bazzite/actions/workflows/build_iso.yml/badge.svg)](https://github.com/ublue-os/bazzite/actions/workflows/build_iso.yml)

# [🇺🇸](https://github.com/ublue-os/bazzite/blob/main/README.md) [🇪🇸](https://github.com/ublue-os/bazzite/blob/main/README-SPA.md) [🇮🇩](https://github.com/ublue-os/bazzite/blob/main/README-ID.md) [🇨🇳](https://github.com/ublue-os/bazzite/blob/main/README-zh-cn.md) [🇫🇷](https://github.com/ublue-os/bazzite/blob/main/README-FR.md) [🇧🇷](https://github.com/ublue-os/bazzite/blob/main/README-BR.md) [🇳🇱](https://github.com/ublue-os/bazzite/blob/main/README-NL.md)

<p align="center">
  <a href="https://download.bazzite.gg/"><img src="/repo_content/download.png?raw=true" alt="Download Bazzite"/></a>
</p>

---

# Table of Contents
- [About \& Features](#about--features)
  - [Desktop](#desktop)
  - [Steam Deck/Home Theater PCs (HTPCs)](#steam-deckhome-theater-pcs-htpcs)
    - [Alternative Handhelds](#alternative-handhelds)
  - [GNOME](#gnome)
  - [Features from Upstream](#features-from-upstream)
    - [Universal Blue](#universal-blue)
    - [Features from Fedora Linux (Kinoite \& Silverblue)](#features-from-fedora-linux-kinoite--silverblue)
- [Why](#why)
- [Showcase](#showcase)
- [Documentation](#documentation)
- [Custom Packages](#custom-packages)
- [Verification](#verification)
- [Secure Boot](#secure-boot)
- [Contributor Metrics](#contributor-metrics)
- [Star History](#star-history)
- [Special Thanks](#special-thanks)
- [Build Your Own](#build-your-own)
- [Join The Community](#join-the-community)
---

## About & Features

[Please see our website](https://bazzite.gg/) for a newcomer-friendly explanation of Bazzite. This readme will cover everything in-depth.

Bazzite is built from [ublue-os/main](https://github.com/ublue-os/main) and [ublue-os/nvidia](https://github.com/ublue-os/nvidia) using [Fedora](https://fedoraproject.org/) technology, which means expanded hardware support and built in drivers are included. Additionally, Bazzite adds the following features:

### Desktop

Common variant available as `bazzite`, suitable for desktop computers.

- Automatic updates for the OS, Flatpaks, and all Distrobox containers - powered by [ublue-update](https://github.com/ublue-os/ublue-update) and [topgrade](https://github.com/topgrade-rs/topgrade).

> [!IMPORTANT]  
> **ISOs can be downloaded from our [website](https://download.ztsw.de), and a helpful install guide can be found [here](https://docs.bazzite.gg/General/Installation_Guide/).**

Rebase from an existing upstream Fedora Atomic to this image:

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/bazzite-deck:stable
```

> [!WARNING]  
> **Due to an upstream bug, Bazzite cannot be used on Steam Decks with 64GB eMMC storage at this time.**

**For users with Secure Boot enabled:** Follow our [secure boot documentation](#secure-boot) prior to rebasing.

## Documentation

- [Installing and Managing Applications](https://docs.bazzite.gg/Installing_and_Managing_Software/)
- [Updates, Rollbacks, and Rebasing](https://docs.bazzite.gg/Installing_and_Managing_Software/Updates_Rollbacks_and_Rebasing/)
- [Gaming Guide](https://docs.bazzite.gg/Gaming/)

View [additional documentation](http://docs.bazzite.gg/) surrounding the project.

## Verification

These images are signed with sigstore's [cosign](https://docs.sigstore.dev/cosign/overview/). You can verify the signature by downloading the `cosign.pub` key from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/ublue-os/bazzite
```

## Secure Boot

> [!WARNING]  
> **Steam Deck Users: The Steam Deck does not come with secure boot enabled and does not ship with any keys enrolled by default. Do not enable this unless you absolutely know what you're doing.**

Secure boot is supported with our custom key. The pub key can be found in the root of this repository [here](https://github.com/ublue-os/bazzite/blob/main/secure_boot.der).
If you'd like to enroll this key prior to installation or rebase, download the key and run the following:

```bash
sudo mokutil --timeout -1
sudo mokutil --import secure_boot.der
```

For users already on a Universal Blue image, you may instead run `ujust enroll-secure-boot-key`.

If asked for a password, use `universalblue`.

## Special Thanks

Bazzite is a community effort and wouldn't exist without everyone's support. Below are some of the people who've helped us along the way:

- [rei.svg](https://github.com/reisvg) - For creating our logo and overall branding.
- [SuperRiderTH](https://github.com/SuperRiderTH) - For creating our Steam game mode startup video.
- [evlaV](https://gitlab.com/evlaV) - For making Valve's code available and for being [this person](https://xkcd.com/2347/).
- [ChimeraOS](https://chimeraos.org/) - For gamescope-session and for valuable support along the way.
- [Jovian-NixOS](https://github.com/Jovian-Experiments) - For supporting us with technical issues and for creating a similar project. Seriously, go check it out. It's our Nix-based cousin.
- [sentry](https://copr.fedorainfracloud.org/coprs/sentry/) - For assistance with needed kernel patches and for creating the [kernel-fsync repo](https://copr.fedorainfracloud.org/coprs/sentry/kernel-fsync/) we now use.
- [nicknamenamenick](https://github.com/nicknamenamenick) - For being the MVP nearly single-handedly upkeeping our documentation and support literature, and countless cases of helping users.
- [Steam Deck Homebrew](https://deckbrew.xyz) - For choosing to support distributions other than SteamOS despite the extra work, and a special thanks to [PartyWumpus](https://github.com/PartyWumpus) for getting Decky Loader working with SELinux for us.
- [cyrv6737](https://github.com/cyrv6737) - For the initial inspiration and the base that became bazzite-arch.

## Build Your Own

Bazzite is built entirely in GitHub and creating your own custom version of it is as easy as forking this repository, adding a private signing key, and enabling GitHub actions.

[Familiarize yourself](https://docs.github.com/en/actions/security-guides/encrypted-secrets) on keeping secrets in github. You'll need to [generate a new keypair](https://docs.sigstore.dev/cosign/overview/) with cosign. The public key can be in your public repo <sub><sup>(Your users need it to check the signatures)</sup></sub>, and you can paste the private key in `Settings -> Secrets -> Actions` with the name `SIGNING_SECRET`.

We also ship a config for the popular [pull app](https://github.com/apps/pull) if you'd like to keep your fork in sync with upstream. Enable this app on your repo to keep track of Bazzite changes while also making your own modifications.

## Join The Community

- You can find us on the [Universal Blue Discord](https://discord.gg/f8MUghG5PB)
  - View the [archive](https://www.answeroverflow.com/c/1072614816579063828/1143023993041993769) of support threads without an account.

- Discuss and create user guides over at the [Universal Blue Discourse Forums](https://universal-blue.discourse.group/c/bazzite/5).

- Follow Universal Blue on [Mastodon](https://fosstodon.org/@UniversalBlue).

[**View the full list of Bazzite resources and social presence**](https://docs.bazzite.gg/Resources/).
