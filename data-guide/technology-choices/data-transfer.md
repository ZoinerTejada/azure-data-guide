# WIP - Data Transfer

[About]()  
[What are your options when choosing a data transfer method?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a data transfer method?
There are several options for transferring data to/from Azure, depending on your needs:

- [Azure Import/Export Service](https://docs.microsoft.com/azure/storage/common/storage-import-export-service)
- [Azure Data Box](https://azure.microsoft.com/services/storage/databox/)
- [Command Line Tools](#cli)
    - AzCopy
    - PowerShell
    - AdlCopy
    - Distcp
    - Sqoop
- [Graphical User Interface Tools](#gui)
    - Azure Storage Explorer
    - Azure Portal
    - Azure Data Factory

### Azure Import/Export Service

The [Azure Import/Export service](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) allows you to securely transfer large amounts of data to Azure Blob Storage or Azure Files by shipping **internal** SATA HDDs or SDDs to an Azure data center. This can also be used to transfer data from Azure storage to hard disk drives and have them shipped to you for loading on-premises. Consider using Azure Import/Export service when uploading or downloading data over the network is too slow, or getting additional network bandwidth is cost-prohibitive.

You can use this service in scenarios such as:

- Migrating data to the cloud: Move large amounts of data to Azure quickly and cost effectively.
- Content distribution: Quickly send data to your customer sites.
- Backup: Take backups of your on-premises data to store in Azure Storage.
- Data recovery: Recover large amount of data stored in storage and have it delivered to your on-premises location.

Back up a series of folders or a list of files to send to the service. Consider using the [Azure Import/Export Tool](https://docs.microsoft.com/azure/storage/common/storage-import-export-tool-setup) to prepare your hard drive(s) that you'll send to the service.

### Azure Data Box

BLAH

### <a name="cli"></a> Command Line Tools

#### AzCopy

Use AzCopy from a [Windows](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) or [Linux](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) command-line to easily copy data to and from Azure Blob, File, and Table storage, with optimal performance. When using the Windows version, you can use AzCopy with Windows-style commands, such as `AzCopy /Source:<source> /Dest:<destination> [Options]`. The Linux version uses POSIX style command-line options, for example: `azcopy --source <source> --destination <destination> [Options]`.

Both platform versions offer the same filtering capabilities, as well as the ability to set the number of concurrent copy operations, using the `--parallel-level` option. The default number of concurrent operations is equal to eight times the number of processors you have, though you may want to specify a lower number when running across a low-bandwidth network.

#### PowerShell

Another command-line option is to use the [`Start-AzureStorageBlobCopy` PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azure.storage/start-azurestorageblobcopy?view=azurermps-5.0.0). This cmdlet can be used alongside other cmdlets by using the pipeline operator. For instance, the following command retrieves all of the blobs in a container named ContosoUploads, by using the `Get-AzureStorageBlob` cmdlet, and then passes the results to the `Start-AzureStorageBlobCopy` cmdlet to start copying the blobs to the ContosoArchives container: `Get-AzureStorageBlob -Container "ContosoUploads" | Start-AzureStorageBlobCopy -DestContainer "ContosoArchives"`.

#### AdlCopy

BLAH

#### Distcp

BLAH

#### Sqoop

BLAH

### <a name="gui"></a> Graphical User Interface Tools

#### Azure Storage Explorer

BLAH

#### Azure Portal

BLAH

#### Azure Data Factory

## <a name="howtochoose"></a> How do you choose?
Each data transfer solution brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements.

## <a name="criteria"></a> Key Selection Criteria

The following tables summarize the key differences in capabilities between each. For data transfer scenarios, choose the appropriate system for your needs by answering these questions:

- Do you need to transfer very large amounts of data, where doing so over an internet connection would take too long or be too expensive?
    - If yes, then narrow your options to those that deal with physical media.

## <a name="matrix"></a> Capability Matrix

### General Capabilities

| | Azure Import/Export Service | Azure Data Box | Command Line Tools | Graphical User Interface Tools |
| --- | --- | --- | --- | --- |
| Physical media | Yes | Yes | No | No |

### Physical Media Capabilities

| | Azure Import/Export Service | Azure Data Box |
| --- | --- | --- |

### Command Line Capabilities

| | AzCopy | PowerShell | AdlCopy | Distcp | Sqoop |
| --- | --- | --- | --- | --- | --- |

### Graphical User Interface Capabilities

| | Azure Storage Explorer | Azure Portal | Azure Data Factory |
| --- | --- | --- | --- |

## <a name="wheretogo"></a>Where to go from here
Read Next:

TODO: FIGURE OUT WHICH SOLUTION PATTERNS AND TECHNOLOGY CHOICES RELATE/SHOULD BE READ NEXT

See Also:

Related Solution Patterns
- Working with transactional data

Related Technology Choices
- Transactional data stores
