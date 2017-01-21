[CloudCross](Http://cloudcross.mastersoft24.ru) - multi-client for cloud sync local files with various cloud storage, written in pure [Qt](/index.php/Qt "Qt") without the use of other third-party library.is currently supported to work with [Yandex Disk](/index.php/Yandex_Disk "Yandex Disk"), [Google Drive](/index.php/Google_Drive "Google Drive") and [Dropbox](/index.php/Dropbox "Dropbox"). CloudCross published under license GPL. Main features:

*   When working with Google Drive - Supports two-way conversion of documents from Microsoft Office file formats and Open / Libre Office in Google Doc format, unloading and the inverse transformation when loading.
*   Support for the so-called black and white lists of files that are involved in synchronization.
*   Setting preferences of local or remote files with the changes, the state of which it will be synchronized.
*   Manage the creation of new versions of files on Google Drive.
*   Possibility of forced download or upload files.
*   Ability to direct download the file to the cloud on the link to download.

## Contents

*   [1 Installation](#Installation)
*   [2 Choosing a provider](#Choosing_a_provider)
*   [3 Usage](#Usage)
*   [4 Use cases](#Use_cases)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Delete files instead of downloading](#Delete_files_instead_of_downloading)
    *   [5.2 Constant upload / download office files](#Constant_upload_.2F_download_office_files)
*   [6 See also](#See_also)

## Installation

Install the package [cloudcross](https://aur.archlinux.org/packages/cloudcross/).

## Choosing a provider

Starting with version 1.1.0 *'CloudCross'* supports multiple cloud services. To select the provider used --provider option *name* . As a *name* is used name of the provider. The default provider Google Drive.

## Usage

After installing, define a folder, the contents of which will be synchronized with the cloud. Go into it and pass authentication:

Google Drive for

```
$ ccross -a

```

for Dropbox

```
$ ccross --provider dropbox -a

```

You will be prompted to copy the link and paste it into your browser. Following the proposed link, you log on to your Google account, and requested permission to take CloudCross applications. After that, you will be given a confirmation code to be inserted into the program. After passing authentication, the program is ready to work.

## Use cases

CloudCross can be used in different situations when necessary to synchronize local files with the files in the cloud. It may be, for example, the duplication of files in a remote storage, working together with Google Docs or backup.

## Troubleshooting

When using CloudCross may have some problems.

### Delete files instead of downloading

When you start the sync to an empty folder, instead of downloading files from remote storage in the cloud files are deleted. This is because the program is prioritizing local files by default. To avoid this, use the startup option --prefer = remote

```
$ Ccross --prefer = remote

```

But, in any case, you have to remember that no local or remote files are not deleted permanently. You can always recover them from the Recycle Bin in the cloud (if supported by the service) or .trash folders synchronized folder.

### Constant upload / download office files

When you synchronize with Google Drive, if the option is used --convert-doc, which converts Office documents to Google Doc format and back, you can see the situation that office files uploaded to the server and unchanged since then, during the next synchronization begin loading back. And once again uploaded to the server during the next synchronization. This is not an error. This happens because the conversion changes the checksum of a file without changing the content and the program tries to synchronize the changes seeing them. If the file has been modified since the last synchronization, the synchronized newer version of the file.

## See also

*   [Project site](Http://cloudcross.mastersoft24.ru/ru)
*   [Group Facebook](Https://www.facebook.com/groups/cloudcross)