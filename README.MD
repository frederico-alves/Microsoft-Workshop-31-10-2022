# MICROSOFT WORKSHOP

🙋‍♂️ Ali Reza Farahnak
- Senior Cloud Solution Architect (Engineering)
🔗 https://github.com/MSFT-alfarahn
- University of Copenhagen

📍 Microsoft
Kanalvej 7 2800 Kgs. Lyngby

- helping with security
- security - learning path on Microsoft Learn
- Devops

- Data Centures Azure Globe
- AI for good - Orbitral
- Business and Competition
- Introduction to the cloud
- Setup Github
- Codespaces
- Chat Backend
- Chat Frontend
- Azure Deployment

Monalitic is hard to emigrate to Azure
- How can move
- Dependencies


=================================
HOW CAN WE SOLVE CLIMATE CHANGE?
=================================
- Microsoft AI for Earth
- https://infrastructuremap.microsoft.com/explore
- Azure Orbitral



==================
 CHAT APPLICATION
==================

========
BACKEND
========
`mkdir Frontend`
`mkdir Backend`

`cd Backend`
`dotnet new -h`
`dotnet new webapi -minimal`
> "The template "ASP.NET Core Web API" was created successfully."


> Backend > Program.cs
====================================================
var builder = WebApplication.CreateBuilder(args);
    builder.Services.AddEndpointsApiExplorer();
    builder.Services.AddSwaggerGen();

var app = builder.Build();
    app.UseSwagger();
    app.UseSwaggerUI();

app.UseHttpsRedirection();

app.Run();
====================================================

> write on line 11 
app.MapGet("/", ()=> "Hello from index");

> pass the localhost in app.Run();
app.Run("https://localhost:5001");


`dotnet build`
`dotnet run`
`dotnet watch run`

> update URL in the browser
`https://frederico-alves-curly-space-winner-wvwvv46j77jh5jg9-5001.preview.app.github.dev/messages/?name=frederico&body=lindissima`


========
FRONTEND
========
UI Components
- MudBlazor
The future of Microsoft will be only cloud provider

> open new terminal
`cd Frontend`
`dotnet new --install MudBlazor.Templates`
`dotnet new mudblazor --host wasm`
`dotnet run`

> in case of error go to > Frontend > Properties > launchSettings.json and update localhost  from 5001 to 5005
"applicationUrl": "https://localhost:5005;http://localhost:5000",

> run again
`dotnet watch run`

- https://mudblazor.com/components/snackbar#usage
- https://mudblazor.com/components/textfield#basic-text-field's

> Frontend > Pages > Counter.razor:
====================================================
@page "/counter"
@inject ISnackbar Snackbar

<PageTitle>Counter</PageTitle>

<MudText Typo="Typo.h3" GutterBottom="true">Counter</MudText>
<MudText Class="mb-4">Current count: @currentCount</MudText>
<MudButton Color="Color.Primary" Variant="Variant.Filled" @onclick="IncrementCount">Click me</MudButton>

<MudTextField @bind-Value="Name" Label="Name" Variant="Variant.Outlined"></MudTextField>
<MudTextField @bind-Value="Message" Label="Message" Variant="Variant.Outlined"></MudTextField>

@code {
    private int currentCount = 0;

    private string Name {get;set;}
    private string Message {get;set;}

    private void IncrementCount()
    {
        Snackbar.Add($"{Name} {Message}");
        Message = "";
        currentCount++;
        StateHasChanged();
    }
}
====================================================


===============
  BACKEND API
===============

> Backend > Program.cs
====================================================
var builder = WebApplication.CreateBuilder(args);
    builder.Services.AddEndpointsApiExplorer();
    builder.Services.AddSwaggerGen();

string chatsession = "";

var app = builder.Build();
    app.UseSwagger();
    app.UseSwaggerUI();

app.UseHttpsRedirection();

app.MapGet("/", ()=> "This app is live");

// app.MapGet("/Messages", (string name, string body)=> $"Hello {name} how are you? This is the message: {body}");
app.MapGet("/Messages", (string name, string body)=>{
    chatsession += $"{name}: {body}{System.Environment.NewLine}";
    return chatsession;
});

app.Run("https://localhost:5001");
====================================================

> Add name and body to the URL browser to exchange messages
https://frederico-alves-curly-space-winner-wvwvv46j77jh5jg9-5001.preview.app.github.dev/messages?name=fred&body=helloToMe


> Make Backend port PUBLIC so the frontend can access it