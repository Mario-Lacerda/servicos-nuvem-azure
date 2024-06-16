# Desafio Dio - Desvendando os Serviços de Nuvem do Azure



### **Projeto ainda mais completo e abrangente com mais códigos:  Desvendando os Serviços de Nuvem do Azure**

**Introdução**

Este projeto irá guiá-lo pelos fundamentos do Microsoft Azure, uma plataforma de computação em nuvem que oferece uma ampla gama de serviços para ajudá-lo a construir, implantar e gerenciar seus aplicativos.



### **Pré-requisitos**

- Uma conta do Microsoft Azure

- O Visual Studio 2019 ou superior

- O .NET Core SDK 3.1 ou superior

  

### **Instruções**

1. **Crie um novo projeto do Visual Studio.**

2. **Selecione o modelo "Aplicativo Web do ASP.NET Core".**

3. **Nomeie o projeto como "AzureCloudInAction".**

4. **Clique em "Criar".**

   

5. #### Adicione os seguintes pacotes NuGet ao projeto:

   

   - Microsoft.Azure.Storage.Blob

   - Microsoft.Azure.Storage.Queue

   - Microsoft.Azure.ServiceBus

     

6. #### Adicione as seguintes classes ao projeto:

   

   - **BlobStorageService.cs:** Esta classe fornece métodos para interagir com o serviço de armazenamento de blobs do Azure.
   - **QueueStorageService.cs:** Esta classe fornece métodos para interagir com o serviço de armazenamento de filas do Azure.
   - **ServiceBusService.cs:** Esta classe fornece métodos para interagir com o serviço de barramento de serviço do Azure.

   

7. #### **Adicione o seguinte código ao arquivo "Startup.cs":**

csharp



```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IBlobStorageService, BlobStorageService>();
    services.AddSingleton<IQueueStorageService, QueueStorageService>();
    services.AddSingleton<IServiceBusService, ServiceBusService>();
}
```



1. #### **Adicione o seguinte código ao arquivo "Controllers/HomeController.cs":**

csharp



```csharp
public class HomeController : Controller
{
    private readonly IBlobStorageService _blobStorageService;
    private readonly IQueueStorageService _queueStorageService;
    private readonly IServiceBusService _serviceBusService;

    public HomeController(IBlobStorageService blobStorageService, IQueueStorageService queueStorageService, IServiceBusService serviceBusService)
    {
        _blobStorageService = blobStorageService;
        _queueStorageService = queueStorageService;
        _serviceBusService = serviceBusService;
    }

    public IActionResult Index()
    {
        return View();
    }

    [HttpPost]
    public async Task<IActionResult> UploadFile(IFormFile file)
    {
        await _blobStorageService.UploadBlobAsync(file.FileName, file.OpenReadStream());

        return RedirectToAction("Index");
    }

    [HttpPost]
    public async Task<IActionResult> SendMessage(string message)
    {
        await _queueStorageService.SendMessageAsync(message);

        return RedirectToAction("Index");
    }

    [HttpPost]
    public async Task<IActionResult> PublishMessage(string message)
    {
        await _serviceBusService.PublishMessageAsync(message);

        return RedirectToAction("Index");
    }
}
```



1. #### **Execute o projeto.**



## **Conclusão**

Este projeto fornece uma base ainda mais sólida para você começar a usar o Microsoft Azure. Você pode usar os serviços de armazenamento de blobs, filas e barramento de serviço para armazenar e recuperar dados, enviar mensagens entre diferentes componentes do seu aplicativo e publicar mensagens para assinantes.


