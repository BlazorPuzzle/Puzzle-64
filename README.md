# Blazor Puzzle #64

## A Phantom Menace?

YouTube Video: https://youtu.be/

Blazor Puzzle Home Page: https://blazorpuzzle.com

### The Challenge:

This is a .NET 9 Blazor Web App with Global Server Interactivity

We are initializing a global keypress handler in JavaScript, which calls our code whenever a key is pressed.

You can see the JavaScript code in *App.razor*:

```html
<script>
    window.InitializeKeyboardHandler = (dotNetRef) =>
    {
        document.addEventListener('keydown', (event) =>
        {
            dotNetRef.invokeMethodAsync('OnKeyDown', event.key);
        });
    }
</script>
```

*Home.razor*:

```c#
@page "/"
@inject IJSRuntime jsRuntime

<PageTitle>Home</PageTitle>

<p>This is a .NET 9 Blazor Web App with Global Server Interactivity</p>

<p>We are initializing a global keypress handler in JavaScript, which calls our code whenever a key is pressed.</p>

<p>You can see the JavaScript code in App.razor</p>

<p>It works, but there is a problem here.</p>

<p>What is it?</p>

<p>Test it by pressing keys.</p>

<h3>@Message</h3>

@code 
{
    string Message { get; set; } = "";

    protected override async Task OnAfterRenderAsync (bool firstRender)
    {
        if (firstRender)
        {
            await jsRuntime.InvokeVoidAsync("InitializeKeyboardHandler", DotNetObjectReference.Create(this));
        }
    }

    [JSInvokable]
    public async Task OnKeyDown(string key)
    {
        Message += key;
        await InvokeAsync(StateHasChanged);
    }
}
```

It works, but there is a problem here.

What is it?

