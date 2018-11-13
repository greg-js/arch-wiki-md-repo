From [CloudCross](http://cloudcross.mastersoft24.ru):

	The CloudCross is an open source project for a synchronization between your devices and various cloud storages. [...] CloudCross allows you synchronize all your local files or only a portion of the local/remote files and folders using the black or white lists (.include and .exclude files). At the same time, you have the opportunity to choose which files have the advantage - local or remote. Thus, you can keep relevance either local files or files on cloud storage.

It is written in pure [Qt](/index.php/Qt "Qt") without the use of other third-party library and it currently supports Microsoft OneDrive, [Google Drive](/index.php/Google_Drive "Google Drive"), [Dropbox](/index.php/Dropbox "Dropbox"), [Yandex Disk](/index.php/Yandex_Disk "Yandex Disk") and Cloud Mail.ru.

Main features:

*   Supports two-way conversion of docs when syncing from MS/Libre/Open Office format to Google Docs and back
*   Support for the so-called black and white lists of files that are involved in synchronization.
*   Setting preferences of local or remote files with the changes, the state of which it will be synchronized.
*   Manage the creation of new versions of files on Google Drive.
*   Possibility of forced download or upload files.
*   Ability to direct download the file to the cloud on the link to download.

CloudCross can be used in different situations when necessary to synchronize local files with the files in the cloud. It may be, for example, the duplication of files in a remote storage, working together with Google Docs or backup.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Delete files instead of downloading](#Delete_files_instead_of_downloading)
    *   [3.2 Constant upload / download office files](#Constant_upload_/_download_office_files)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [cloudcross](https://aur.archlinux.org/packages/cloudcross/) package.

## Usage

See the ccross(1) [man page](/index.php/Man_page "Man page") or the [online usage](https://cloudcross.mastersoft24.ru/usage).

To get started change into the directory you want to synchronize and run:

```
$ ccross --auth --provider *provider_name*

```

You will be prompted to copy the link and paste it into your browser. Following the proposed link, you log on to your Google account, and requested permission to take CloudCross applications. After that, you will be given a confirmation code to be inserted into the program. After passing authentication, the program is ready to work.

## Troubleshooting

When using CloudCross may have some problems.

### Delete files instead of downloading

When you start the sync to an empty folder, instead of downloading files from remote storage in the cloud files are deleted. This is because the program is prioritizing local files by default. To avoid this, use the startup option `--prefer remote`.

```
$ ccross --prefer remote

```

But, in any case, you have to remember that no local or remote files are not deleted permanently. You can always recover them from the Recycle Bin in the `cloud` (if supported by the service) or `.trash` synchronized folders.

### Constant upload / download office files

When you synchronize with Google Drive, if the option `--convert-doc` is used, you can see unchanged uploaded files being synchronized all over again. This is not an error. This happens because the file format conversion changes the checksum of the file without changing its content, so *ccross* tries to synchronize it assuming the file was changed. If the file has been modified since the last synchronization, *cross* with sincronize the newer version of the file.

## See also

*   [Project site](Http://cloudcross.mastersoft24.ru)
*   [Facebook Group](Https://www.facebook.com/groups/cloudcross)