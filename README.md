# License

Developped at Orange Business Services under LGPL-2.1. See [LICENSE](LICENSE).

# How to use

## Pre-requisites

This plugin requires .NET Framework 4.6 minimum, you can download the latest version from [Microsoft website](https://dotnet.microsoft.com/download).

For Linux users, you need to install the latest `mono-complete` package.

## Usage

1. Download the [latest PLGX file](https://github.com/ttaeschn/keepass-vault-sync-plugin/releases) and copy it in the KeePass installation folder, in plugins directory
   * For Windows it's in `C:\Program Files (x86)\KeePass Password Safe 2\Plugins`
   * For Linux it's in `/usr/lib/keepass2/Plugins`
2. Open your database
3. Create an entry with name starting with `vault`. For example: `vault-personal-folder`
    * Username is the username used to authenticate on Vault
    * Password is the password used to authenticate on Vault
    * URL is the Vault Backend URL (port included). For example: `https://local-vault:8200`
    * In Advanced tab add the following String fields:
      * `auth` field contains the auth path. For basic Vault authentication, it should be `username`. For LDAP authentication, it should be the LDAP name.
      * `path` field contains the path to synchronize. Any secret in this path will be synchronized, recursively.
4. Click on *Tools -> Synchronize Vault entries*. Synchronization may take a while, since Vault API is really not designed for this kind of use case.
5. A folder named with your entry name followed by the date and time timestamp will be created. If the entry was previously synchronized, the previous folder won't be deleted.
6. You can save your database. The plugin won't do it for you.
7. For now, there is no error message in case of issue. Only the lack of synchronization will be a symptom of issue. It may be improved in future versions. If needed.

# Why these release names?

* Because release themes are cheap but are a small pleasure in release process
* Because it helps structuring releases
* Because why not?
* Because [Vault](https://en.wikipedia.org/wiki/Vault_\(comics\)), so [Release Theme](https://fr.wikipedia.org/wiki/Cat%C3%A9gorie:Super-vilain_Marvel)

# How to build

1. Get the dependencies listed [here](external/Readme.md)
1. Modify the version in both AssemblyInfo and KeepassPluginVersion.txt
1. Build the solution, targetting `Release PLGX`
1. The file is generated in VaultSyncPlugin/bin/ReleasePlgx/VaultSyncPlugin.plgx

For some reason, the execution of plgxtool can fail. The quick workaround consists in running the command directly in bash from the VaultSyncPlugin project folder.

# How to test

This part could be improved. For now, there are is one integration test, with minimal assertion.
On first run, a `secrets.json` file will be generated, containing the needed values to be modified for the test to run.
Since it contains sensitive data, this file is gitignored. But you should check regularly that it's not committed.

# Library used

* [KeePass](https://keepass.info) for plugin API (GPL-2.0)
* [Vault.NET](https://github.com/Chatham/Vault.NET) for Vault API C# wrapping (MIT)
* [PlgxTool](https://github.com/dlech/KeePassPluginDevTools) for PLGX generation (GPL-2.0)
* [Newtonsoft.Json](https://github.com/JamesNK/Newtonsoft.Json) as dependency of Vault.NET (MIT)
* A bunch of .NET extension libraries, as dependencies of dependencies, from .NET framework 4.6 or Microsoft libraries on nuget (Apache 2 and MIT, depends on the lib/framework)
