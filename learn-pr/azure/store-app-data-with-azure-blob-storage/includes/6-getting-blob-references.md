.NET Core용 Azure Storage SDK에서 개별 Blob을 사용하여 작업하려면 ‘Blob 참조’, 즉 `ICloudBlob` 개체의 인스턴스가 필요합니다.

Blob의 이름을 사용하거나 컨테이너의 Blob 목록에서 선택하여 `ICloudBlob`을 가져올 수 있습니다. 두 방법 모두 `CloudBlobContainer`가 필요하며, 이에 대해서는 마지막 단원에서 가져오는 방법을 살펴보았습니다.

## <a name="getting-blobs-by-name"></a>이름으로 Blob 가져오기

`CloudBlobContainer`에서 `GetXXXReference` 메서드 중 하나를 호출하여 이름을 기준으로 `ICloudBlob`을 가져옵니다. 검색 중인 Blob의 유형을 알고 있는 경우에는 보다 구체적인 메서드(`GetBlockBlobReference`, `GetAppendBlobReference`, `GetPageBlobReference`) 중 하나를 사용하는 것이 더 좋습니다.

이러한 메서드는 네트워크 호출을 수행하지 않고 Blob이 실제로 존재하는지 여부를 확인하지도 않습니다. 별도의 `GetBlobReferenceFromServerAsync` 메서드가 Blob Storage API를 호출하고 Blob이 아직 없는 경우 예외를 throw합니다.

## <a name="listing-blobs-in-a-container"></a>컨테이너 Blob 나열

`CloudBlobContainer`의 `ListBlobsSegmentedAsync` 메서드를 사용하여 컨테이너의 Blob 목록을 가져올 수 있습니다. *Segmented*는 별개의 결과 페이지가 반환됨을 나타냅니다. `ListBlobsSegmentedAsync`에 대한 단일 호출은 단일 페이지에 모든 결과를 반환할 것을 보장하지 않습니다. 여러 페이지에 걸쳐 작업할 수 있으려면, 반환되는 `ContinuationToken`을 사용하여 반복적으로 호출해야 할 수 있습니다. 이렇게 하면 Blob을 나열하는 코드가 업로드 또는 다운로드하기 위한 코드보다 좀 더 복잡해지지만 컨테이너의 모든 Blob을 가져오는 데 사용할 수 있는 표준 패턴이 확보됩니다.

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

`continuationToken`이 결과의 끝을 나타내는 `null`일 때까지 `ListBlobsSegmentedAsync`을 반복적으로 호출합니다.

### <a name="processing-list-results"></a>목록 결과 처리

`ListBlobsSegmentedAsync`에서 가져올 개체에는 `IEnumerable<IListBlobItem>` 유형의 `Results` 속성이 포함되어 있습니다. `IListBlobItem`에는 Blob의 컨테이너 및 URL에 대한 몇 가지 속성이 포함되어 있지만 업로드 또는 다운로드 메서드는 포함되지 않습니다. 이는 일부 결과 개체가 개별 Blob 대신 가상 디렉터리를 나타내는 `CloudBlobDirectory` 개체일 수 있기 때문입니다.

개별 Blob에만 관심이 있는 경우에는 `OfType<>` 메서드를 사용하여 결과를 필터링할 수 있습니다. 다음은 몇 가지 예입니다.

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

`OfType<>`을 사용하려면 `System.Linq` 네임스페이스에 대한 참조(`using System.Linq;`)가 필요합니다.

## <a name="exercise"></a>연습

앱의 기능 중 하나가 작동하려면 API에서 Blob 목록을 가져와야 합니다. 위에 나온 패턴을 사용하여 컨테이너의 모든 Blob을 나열하겠습니다. 목록을 처리할 때 각 Blob의 이름을 가져옵니다.

편집기에서 `BlobStorage.cs`를 열고 `GetNames`에 다음 코드를 입력합니다.

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

이 메서드로 반환된 이름은 `FilesController`에 의해 처리되어 URL로 변환됩니다. 이 이름이 클라이언트에 반환되면 페이지에서 하이퍼링크로 렌더링됩니다.