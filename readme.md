# EasySync

Synchronize your phone with your WebDAV server, the easy way.

## Features

* Synchronize images, videos, audio and downloads
* Synchronize in both directions :
    * Files touched on your phone will be uploaded / deleted on your server
    * Files touched on your server will be uploaded / deleted on your phone
* Basic auth (login with password) or Digest auth
* Secure storage of your credentials
* Preserve timestamps if you use Nextcloud as DAV server

## Get it

### On Google Play

<a href='https://play.google.com/store/apps/details?id=com.phpbg.easysync&pcampaignid=pcampaignidMKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1'>
    <img align='center' width='240' alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png'/>
    <img align='center' width='128' alt='Get it on Google Play' src='./qr-playstore.png'/>
</a>

A free trial version (30 days) is
also [available here](https://play.google.com/store/apps/details?id=com.phpbg.easysync.trial&utm_source=github&pcampaignid=pcampaignidMKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1)

### On F-Droid

<a href='https://f-droid.org/packages/com.phpbg.easysync'>
    <img align='center' width='240' alt="Get it on F-Droid" src='https://fdroid.gitlab.io/artwork/badge/get-it-on.png'>
    <img align='center' width='128' alt='Get it on F-Droid' src='./qr-fdroid.png'/>
</a>

## FAQ

### What is synchronized

* **Images, video, screenshots**
    * If they are displayed in your gallery, they will be synchronized. This includes images and
      videos in `DCIM/`, `Pictures/`, `Movies/` and `Download/`
    * If they are only available in a specific app but not in gallery, they won't be synchronized
    * Please note that messaging apps (messages, whatsapp, signal, etc.) generally offer you the
      choice between saving files in your gallery (in such case they will be synchronized) or not
* **Audio, music**
    * All audio files that are visible in `Alarms/`, `Audiobooks/`, `Music/`, `Notifications/`,
      `Podcasts/`, `Ringtones/` and `Recordings/` will be synchronized
    * Beware that google's own voice recorder stores its files privately and offer its own cloud
      synchronization. They won't be synchronized by EasySync
* **Downloaded files**
    * All downloaded files in `Download/` will be synchronized, whether they are pdf, epubs,
      documents, images, etc.

### What is not synchronized

Everything not explicitly stated above is not synchronized. More specifically:

* Applications
* Applications data/state
* Messages
* Contacts
* Games progress
* Wifi or network parameters
* Android settings and phone customization

Files on **SD Card** are **NOT** synced (https://github.com/phpbg/easysync/issues/44)

### Can I choose what is synchronized

All files are synced unless you explicitly exclude folders.

### Will it eat all my cellular data plan?

No, you can choose if you allow sync on cellular or only on wifi.

### Will it eat all my storage?

No, you can select a subfolder on your NAS that will be synced.
For example if you own 2 devices in your family, you can have one folder per device so they are
synced independantly.

### I am a nextcloud user. Does this replace nextcloud app?

When you configure EasySync you select a specific folder on your DAV server. This folder will be
fully synced with your phone.

* If you want to access files on your DAV server that are **outside** that specific folder, then you
  still need nextcloud app.
* If you need **per folder synchronization**, then you still need nextcloud app.
* If you want to use all nextcloud features (such as sharing), then you still need nextcloud app.
* Otherwise it is probably not necessary.

### Changes on android device side are not immediately reflected

1. Please be sure to disable battery optimization permission (it will be shown on home screen if
   required). Disabling battery optimization will not drain your battery. It will just enable
   immediate sync of file changes.
2. You may also enable `Sync on cellular` and/or `Sync on battery` in `Synchronization settings` (
   available from home screen).

We suggest keeping `Sync on battery` enabled for immediate photo syncing.
Disabling it means syncs will only happen while charging on AC power, at Android's discretion (
usually at night), making the timing unreliable.
Even with `Sync on battery` enabled, EasySync should use very little battery.

### Changes on DAV server side are not immediately reflected

To preserve battery, updates from your DAV server are checked periodically.
If you require an immediate synchronization, please use the `Sync now` button located on the home
screen.

### Use a self-signed or a custom certificate

You can add your own trusted certificate in android `Settings` > `Encryption and Credentials`

## Supported Android phones

* From Android 8 to latest releases
* Huawei phones may kill the app in background, be warned. These tips will help you:
    * https://consumer.huawei.com/eg-en/support/article-list/article-detail/en-gb15792041/
    * https://dontkillmyapp.com/huawei

## Supported WebDAV servers

It should work with any DAV compliant server.

| WebDAV Server                                                              | Preserves file creation timestamps | Notes                                                                                             |
|----------------------------------------------------------------------------|------------------------------------|---------------------------------------------------------------------------------------------------|
| [Nextcloud](https://nextcloud.com/files/)                                  | ✅ Yes                              |                                                                                                   |
| [owncloud](https://owncloud.com/)                                          | ✅ Yes                              |                                                                                                   |
| [SFTPGo](https://github.com/drakkan/sftpgo)                                | ✅ Yes                              |                                                                                                   |
| [Apache](https://httpd.apache.org/docs/current/fr/mod/mod_dav.html)        | ❌ No                               |                                                                                                   | 
| [Hacdias Webdav](https://github.com/hacdias/webdav)                        | ❌ No                               |                                                                                                   |
| [Lighttpd](https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_webdav) | ❌ No                               | no etag support.                                                                                  |
| [nginx](http://nginx.org/en/docs/http/ngx_http_dav_module.html)            | ❌ No                               | no etag support.                                                                                  |
| [Photoprism](https://docs.photoprism.app/user-guide/sync/webdav/)          | ❓ Unknown                          | Photoprism reads photos creation timestamps from exif data, so it will display correct timestamps |

## Supported WebDAV providers

| WebDAV Provider                      | Preserves file creation timestamps | Notes                                                                                                                                           |
|--------------------------------------|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| [Mailbox](https://mailbox.org/)      | ❌ No                               | no etag support. Use https://office.mailbox.org/servlet/webdav.infostore as URL and /Userstore/<firstname lastname>/Documents as remote folder. |
| [kDrive](https://www.infomaniak.com) | ❓ Unknown                          |                                                                                                                                                 |

## Sync is slow on Nextcloud

There are several reports of nextcloud DAV to be slow.

You can get **drastic speedup** (almost 10x) when using a device password instead of your user's
password:

1. Create
   a [device password](https://docs.nextcloud.com/server/19/user_manual/session_management.html#managing-devices)
2. Go to DAV Settings in easysync, use your own login, but put the device password instead of your
   usual user password
3. Enjoy 10x speedup

## Donate

If you like this app consider making [a donation](https://github.com/sponsors/phpbg)

## License

MIT

By using this application, you agree to be bound
by [these terms and conditions and legal disclaimer.](./LICENSE)

## Roadmap

* Fix: handle permissions rejected that cannot be asked anymore (the permission activity doesn't
  start)
* Feature: check for low free space on dav or on device
* Optimization: when new remote files are locally added during FullSync, a FileSync is trigged which
  is useless. See if we can avoid this

## Update / add translations

* Create/update `app/src/main/res/values-xx/strings.xml`
* Create/update `fastlane/metadata/android/xx/full_description.txt`
* Create/update `fastlane/metadata/android/xx/short_description.txt`

Replace `xx` with
your [ISO 639-1 language code](https://www.loc.gov/standards/iso639-2/php/code_list.php). E.g. `en`
for english, `fr` for french, etc.

For new languages:

* Add a new locale entry to `app/src/main/res/xml/locales_config.xml`
* Add a new locale entry to `app/build.gradle` in `resourceConfigurations` key

## See also

* [NextCloud Android App](https://github.com/nextcloud/android)
* [Round-Sync Android App](https://github.com/newhinton/Round-Sync)
* [Awesome WebDAV: Android Apps](https://github.com/WebDAVDevs/awesome-webdav/tree/main?tab=readme-ov-file#android)
