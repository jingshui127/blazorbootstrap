﻿---
title: Blazor Modal Service
description: Use Blazor Bootstrap modal service to show quick dialogs to your site for lightboxes, user notifications, or completely custom content.
image: https://i.imgur.com/Tze7msN.png

sidebar_label: Modal Service
sidebar_position: 1
---

# Blazor Modal Service

Use Blazor Bootstrap modal service to show quick dialogs to your site for lightboxes, user notifications, or completely custom content.

<img src="https://i.imgur.com/Tze7msN.png" alt="Blazor Modal Service" />
<br />
<a href="https://demos.blazorbootstrap.com/modal-service">See blazor modal service demo here.</a>

## Methods

| Name | Return Type | Description | Added Version |
|:--|:--|
| ShowAsync(**ModalOption** modalOption) | Task | Show the modal. | 1.9.0 |

## ModalOption Members

| Property Name | Type | Description | Required | Default | Added Version |
|:--|:--|:--|:--|:--|
| FooterButtonColor | `ButtonColor` | Gets or sets the footer button color. | | `ButtonColor.Secondary` | 1.9.0 |
| FooterButtonCSSClass | string | Gets or sets the footer button custom CSS class. | | null | 1.9.0 |
| FooterButtonText | string | Gets or sets the footer button text. | | OK | 1.9.0 |
| IsVerticallyCentered | bool | Gets or sets the IsVerticallyCentered. | | false | 1.9.0 |
| Message | string | Gets or sets the modal message. | ✔️ | null | 1.9.0 |
| ShowFooterButton | string | Shows or hides the footer button. | | true | 1.9.0 |
| Size | `ModalSize` | Gets or sets the modal size. | | `ModalSize.Regular` | 1.9.0 |
| Title | string | Gets or sets the modal title. | ✔️ | null | 1.9.0 |
| Type | `ModalType` | Gets or sets the modal type. | | `ModalType.Light` | 1.9.0 |

## Examples

### How it works

<img src="https://i.imgur.com/vIELA4s.png" alt="Blazor Modal Service: How it works" />

```cshtml {} showLineNumbers
<Button Color="ButtonColor.Primary" @onclick="() => ShowModal(ModalType.Primary)">Show Primary Modal</Button>
<Button Color="ButtonColor.Secondary" @onclick="() => ShowModal(ModalType.Secondary)">Show Secondary Modal</Button>
<Button Color="ButtonColor.Success" @onclick="() => ShowModal(ModalType.Success)">Show Success Modal</Button>
<Button Color="ButtonColor.Danger" @onclick="() => ShowModal(ModalType.Danger)">Show Danger Modal</Button>
<Button Color="ButtonColor.Warning" @onclick="() => ShowModal(ModalType.Warning)">Show Warning Modal</Button>
<Button Color="ButtonColor.Info" @onclick="() => ShowModal(ModalType.Info)">Show Info Modal</Button>
<Button Color="ButtonColor.Light" @onclick="() => ShowModal(ModalType.Light)">Show Light Modal</Button>
<Button Color="ButtonColor.Dark" @onclick="() => ShowModal(ModalType.Dark)">Show Dark Modal</Button>
```

```cs {} showLineNumbers
@code {
    [Inject] ModalService ModalService { get; set; } = default!;

    private async Task ShowModal(ModalType modalType)
    {
        var modalOption = new ModalOption
                          {
                              Title = "Modal title",
                              Message = "Modal body text goes here.",
                              Type = modalType,
                          };

        await ModalService.ShowAsync(modalOption);
    }
}
```

[See demo here.](https://demos.blazorbootstrap.com/modal-service#how-it-works)

### Vertically Centered

<img src="https://i.imgur.com/j1GeDQ3.png" alt="Blazor Modal Service: Vertically Centered" />

```cshtml {} showLineNumbers
<Button Color="ButtonColor.Primary" @onclick="() => ShowModal(ModalType.Primary)">Show Primary Modal</Button>
<Button Color="ButtonColor.Secondary" @onclick="() => ShowModal(ModalType.Secondary)">Show Secondary Modal</Button>
<Button Color="ButtonColor.Success" @onclick="() => ShowModal(ModalType.Success)">Show Success Modal</Button>
<Button Color="ButtonColor.Danger" @onclick="() => ShowModal(ModalType.Danger)">Show Danger Modal</Button>
<Button Color="ButtonColor.Warning" @onclick="() => ShowModal(ModalType.Warning)">Show Warning Modal</Button>
<Button Color="ButtonColor.Info" @onclick="() => ShowModal(ModalType.Info)">Show Info Modal</Button>
<Button Color="ButtonColor.Light" @onclick="() => ShowModal(ModalType.Light)">Show Light Modal</Button>
<Button Color="ButtonColor.Dark" @onclick="() => ShowModal(ModalType.Dark)">Show Dark Modal</Button>
```

```cs {} showLineNumbers
@code {
    [Inject] ModalService ModalService { get; set; } = default!;

    private async Task ShowModal(ModalType modalType)
    {
        var modalOption = new ModalOption
                          {
                              Title = "Modal title",
                              Message = "Modal body text goes here.",
                              Type = modalType,
                              IsVerticallyCentered = true
                          };

        await ModalService.ShowAsync(modalOption);
    }
}
```

[See demo here.](https://demos.blazorbootstrap.com/modal-service#vertically-centered)

### Size

<img src="https://i.imgur.com/HDBtQDf.png" alt="Blazor Modal Service: Size" />

```cshtml {} showLineNumbers
<Button Color="ButtonColor.Primary" @onclick="() => ShowModal(ModalSize.Regular)">Show Regular Modal</Button>
<Button Color="ButtonColor.Secondary" @onclick="() => ShowModal(ModalSize.Small)">Show Small Modal</Button>
<Button Color="ButtonColor.Success" @onclick="() => ShowModal(ModalSize.Large)">Show Large Modal</Button>
<Button Color="ButtonColor.Danger" @onclick="() => ShowModal(ModalSize.ExtraLarge)">Show ExtraLarge Modal</Button>
```

```cs {} showLineNumbers
@code {
    [Inject] ModalService ModalService { get; set; } = default!;

    private async Task ShowModal(ModalSize modalSize)
    {
        var modalOption = new ModalOption
                          {
                              Title = "Modal title",
                              Message = "Modal body text goes here.",
                              Size = modalSize
                          };

        await ModalService.ShowAsync(modalOption);
    }
}
```

[See demo here.](https://demos.blazorbootstrap.com/modal-service#size)

### Change footer button color and text

<img src="https://i.imgur.com/4Hwfj3P.png" alt="Blazor Modal Service: Change footer button color and text" />

```cshtml {} showLineNumbers
<Button Color="ButtonColor.Primary" @onclick="ShowModal">Show Modal</Button>
```

```cs {} showLineNumbers
@code {
    [Inject] ModalService ModalService { get; set; } = default!;

    private async Task ShowModal()
    {
        var modalOption = new ModalOption
                          {
                              Title = "Modal title",
                              Message = "Modal body text goes here.",
                              FooterButtonColor = ButtonColor.Primary,
                              FooterButtonText = "Got it!"
                          };

        await ModalService.ShowAsync(modalOption);
    }
}
```

[See demo here.](https://demos.blazorbootstrap.com/modal-service#change-footer-button-color-and-text)

### Hide footer button

<img src="https://i.imgur.com/NwMP5MT.png" alt="Blazor Modal Service: Hide footer button" />

```cshtml {} showLineNumbers
<Button Color="ButtonColor.Primary" @onclick="ShowModal">Show Modal</Button>
```

```cs {} showLineNumbers
@code {
    [Inject] ModalService ModalService { get; set; } = default!;

    private async Task ShowModal()
    {
        var modalOption = new ModalOption
                          {
                              Title = "Modal title",
                              Message = "Modal body text goes here.",
                              ShowFooterButton = false
                          };

        await ModalService.ShowAsync(modalOption);
    }
}
```

[See demo here.](https://demos.blazorbootstrap.com/modal-service#hide-footer-button)

### How to setup

1. Add the **Modal** component in **MainLayout.razor** page as shown below.

```cshtml {9} showLineNumbers
@inherits LayoutComponentBase

...

... MainLayour.razor code goes here ...

...

<Modal IsServiceModal="true" />
```

1. Inject **ModalService**, then call the `ShowAsync(...)` method as shown below. 
1. `ShowAsync` method accepts **ModalOption** object as a parameter.

```cs {2,10-15,17,23-28,30} showLineNumbers
@code {
    [Inject] ModalService ModalService { get; set; } = default!;

    private async Task SaveEmployeeAsync()
    {
        try
        {
            // call the service/api to save the employee details

            var modalOption = new ModalOption
                              {
                                  Title = "Save Employee",
                                  Message = "Employee details saved.",
                                  Type = ModalType.Success
                              };

            await ModalService.ShowAsync(modalOption);
        }
        catch(Exception ex)
        {
            // handle exception

            var modalOption = new ModalOption
                              {
                                  Title = "Save Employee",
                                  Message = $"Error: {ex.Message}.",
                                  Type = ModalType.Danger
                              };

            await ModalService.ShowAsync(modalOption);
        }
    }
}
```
