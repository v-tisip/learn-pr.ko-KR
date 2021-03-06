<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


데이터는 Azure Cosmos DB의 JSON 문서에 저장됩니다. [문서](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents)는 이전 모듈에 나와 있는 대로 또는 이 모듈에서 설명한 대로 프로그래밍 방식으로 포털에서 만들어지거나, 검색되거나, 바뀌거나, 삭제될 수 있습니다. Azure Cosmos DB는 .NET, .NET Core, Java, Node.js 및 Python에 사용되는 클라이언트 쪽 SDK를 제공합니다. 이러한 도구는 각각 해당 작업을 지원합니다. 이 모듈에서는 .NET Core SDK를 사용하여 CRUD(만들기, 검색, 업데이트 및 삭제) 작업을 수행합니다. 

Azure Cosmos DB 문서에 대한 기본 작업은 [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 클래스의 일부입니다.
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet). Upsert는 문서가 이미 존재하는지 여부에 따라 만들기 또는 바꾸기 작업을 수행합니다.
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

이러한 작업을 수행하려면 데이터베이스에 저장된 개체를 나타내는 클래스를 만들어야 합니다. 사용자 데이터베이스로 작업하기 때문에 이름 및 사용자 ID(수평적 확장을 사용하도록 설정할 파티션 키이므로 필수임)와 배송 기본 설정 및 주문 기록에 대한 서브클래스 같은 기본 데이터를 저장할 **User** 클래스를 작성해야 합니다.

사용자를 나타내는 해당 클래스가 만들어져 있으면 각 인스턴스에 대한 새 사용자 문서를 만든 후에 문서에서 몇 가지 간단한 CRUD 작업을 수행합니다.

## <a name="create-documents"></a>문서 만들기

1. 먼저 Azure Cosmos DB에 저장할 개체를 나타내는 **User** 클래스를 만듭니다. **User** 내에서 사용되는 **OrderHistory** 및 **ShippingPreference** 서브클래스도 만듭니다. 문서에는 JSON에서 **ID**로 직렬화된 **ID** 속성이 있어야 합니다. 

    이러한 클래스를 만들려면 **BasicOperations** 메서드 아래에 있는 **User**, **OrderHistory**, **ShippingPreference** 클래스를 복사하여 붙여넣습니다.

    <!--TODO: specify JSON for all of these? -->
    ```csharp
    public class User
    {
            [JsonProperty("id")]
            public string Id { get; set; }
            [JsonProperty("userId")]
            public string UserId { get; set; }
            [JsonProperty("lastName")]
            public string LastName { get; set; }
            [JsonProperty("firstName")]
            public string FirstName { get; set; }
            [JsonProperty("email")]
            public string Email { get; set; }
            [JsonProperty("dividend")]
            public string Dividend { get; set; }
            public OrderHistory[] OrderHistory { get; set; }
            public ShippingPreference[] ShippingPreference { get; set; }
            public CouponsUsed[] Coupons { get; set; }
            public override string ToString()
            {
            return JsonConvert.SerializeObject(this);
            }
    }
    
    public class OrderHistory
    {
            public string OrderId { get; set; }
            public string DateShipped { get; set; }
            public string Total { get; set; }
    }
    
    public class ShippingPreference
    {
            public int Priority { get; set; }
            public string AddressLine1 { get; set; }
            public string AddressLine2 { get; set; }
            public string City { get; set; }
            public string State { get; set; }
            public string ZipCode { get; set; }
            public string Country { get; set; }
    }
    
    public class CouponsUsed
    {
            public string CouponCode { get; set; }
    
    }
    
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. 통합 터미널에서 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.

    ```csharp
    dotnet run
    ```

3. 이제 **ShippingPreference** 클래스 아래의 **CreateUserDocumentIfNotExists** 작업을 복사하여 붙여넣습니다.

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                    await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                    this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                    throw;
            }
            }
    }
    ```

4. 그런 다음, **BasicOperations** 메서드에 다음을 추가합니다.

    ```csharp
     User yanhe = new User
                {
                    Id = "1",
                    UserId = "yanhe",
                    LastName = "He",
                    FirstName = "Yan",
                    Email = "yanhe@todo.com",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);
    
                User nelapin = new User
                {
                    Id = "2",
                    UserId = "nelapin",
                    LastName = "Pindakova",
                    FirstName = "Nela",
                    Email = "nelapin@todo.com",
                    Dividend = "8.50",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1001",
                    DateShipped = "08/17/2018",
                    Total = "105.89"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    },
                    new ShippingPreference {
                            Priority = 2,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                    Coupons = new CouponsUsed[]
             {
                 new CouponsUsed{
                     CouponCode = "Fall2018"
                 }
             }
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

5. 통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.

    ```csharp
    dotnet run
    ```

    터미널은 사용자 레코드가 둘 다 성공적으로 만들어졌음을 나타내는 다음 출력을 표시합니다. 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>문서 읽기

1. 데이터베이스에서 문서를 읽으려면 다음 코드에서 복사하여 Program.cs 파일 끝에 놓습니다.

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found user {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  다음 코드를 복사하여 **BasicOperations** 메서드 끝의 `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` 줄 뒤에 붙여넣습니다.

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. Program.cs 파일을 저장한 후에 통합 터미널에서 다음 명령을 실행합니다.

    ```
    dotnet run
    ```
    터미널은 “사용자 1 찾음” 출력이 문서를 찾았음을 나타내는 다음 출력을 표시합니다.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a>문서 바꾸기
Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다. 이 경우 사용자 레코드를 업데이트하여 사용자의 성 변경을 처리합니다.

1. **ReplaceFamilyDocument** 메서드를 복사하여 **CreateUserDocumentIfNotExists** 메서드 아래에 붙여넣습니다.

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. 다음 코드를 복사하여 **BasicOperations** 메서드 끝의 `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` 줄 뒤에 붙여넣습니다.

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. Program.cs 파일을 저장한 후에 통합 터미널에서 다음 명령을 실행합니다.

    ```
    dotnet run
    ```
    터미널은 다음 출력을 표시합니다. 여기서, “Suh의 성을 바꿈” 출력은 문서가 바뀌었음을 나타냅니다.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh 
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a>문서 삭제

1. **DeleteUserDocument** 메서드를 복사하여 **ReplaceUserDocument** 메서드 아래에 붙여넣습니다.
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. 두 번째 쿼리 실행의 **BasicOperations** 메서드에 다음 코드를 복사하여 붙여넣습니다.

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. Program.cs 파일을 저장한 후에 통합 터미널에서 다음 명령을 실행합니다.

    ```
    dotnet run
    ```

    축하합니다! Azure Cosmos DB 문서를 성공적으로 삭제했습니다.

## <a name="summary"></a>요약

이 단원에서는 Azure Cosmos DB 데이터베이스에서 문서를 만들고, 바꾸고, 삭제했습니다.