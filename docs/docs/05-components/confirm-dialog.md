﻿---
title: Blazor Confirm Dialog Component
description: Use Blazor Bootstrap confirm dialog component if you want the user to verify or accept something.
image: https://i.imgur.com/B5Hf85u.png

sidebar_label: Confirm Dialog
sidebar_position: 10
---

# Blazor Confirm Dialog

Use Blazor Bootstrap confirm dialog component if you want the user to verify or accept something.

<img src="https://i.imgur.com/B5Hf85u.png" alt="Blazor Bootstrap: Confirm Dialog component" />

## Methods

| Name | Return Type | Description | Added Version |
|:--|:--|:--|:--|
| ShowAsync(string title, string message1, ConfirmDialogOptions confirmDialogOptions = null) | Task<bool\> | Shows confirm dialog. | 1.1.0 |
| ShowAsync(string title, string message1, string message2, ConfirmDialogOptions confirmDialogOptions = null) | Task<bool\> | Shows confirm dialog. | 1.1.0 |
| ShowAsync<T\>(string title, Dictionary<string, object> parametres = null, ConfirmDialogOptions confirmDialogOptions = null) | Task<bool\> | Shows confirm dialog. T is component. | 1.1.0 |

## ConfirmDialogOptions Properties

| Name | Type | Default | Description | Added Version |
|:--|:--|:--|:--|:--|
| DialogCssClass | string | | Additional CSS class for the dialog (div.modal-dialog element). | 1.1.0 |
| Dismissable | bool | | Adds a dismissable close button to the confirm dialog. | 1.1.0 |
| HeaderCssClass | string | | Additional header CSS class (div.modal-header element). | 1.1.0 |
| IsScrollable | bool | | Allows confirm dialog body to be scrollable. | 1.1.0 |
| IsVerticallyCentered | bool | | Shows the confirm dialog vertically in the center of the page. | 1.1.0 |
| NoButtonColor | ButtonColor | | Gets or sets the 'No' button color. | 1.1.0 |
| NoButtonText | string | No | Gets or sets the 'No' button text. | 1.1.0 |
| Size | DialogSize | ModalSize.Regular | Size of the modal. | 1.1.0 | 
| YesButtonColor | ButtonColor | ButtonColor.Primary | Gets or sets the 'Yes' button color. | 1.1.0 |
| YesButtonText | string | Yes | Gets or sets the 'Yes' button text. | 1.1.0 |

## Examples

### Confirm Dialog

<img src="https://i.imgur.com/B5Hf85u.png" alt="Blazor Bootstrap: Confirm Dialog Component - Examples" />

```cshtml {1} showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Danger" @onclick="ShowConfirmationAsync"> Delete Employee </Button>
```

```cs {2,6-9,11} showLineNumbers
@code {
    private ConfirmDialog dialog;

    private async Task ShowConfirmationAsync()
    {
        var confirmation = await dialog.ShowAsync(
            title: "Are you sure you want to delete this?",
            message1: "This will delete the record. Once deleted can not be rolled back.",
            message2: "Do you want to proceed?");

        if (confirmation)
        {
            // do whatever
        }
        else
        {
            // do whatever
        }
    }
}
```

[See Confirm Dialog demo here.](https://demos.blazorbootstrap.com/confirm-dialog#examples)

### Dynamic component as confirm dialog

Render different components dynamically within the confirm dialog without iterating through possible types or using conditional logic.

If dynamically-rendered components have component parameters, pass them as an `IDictionary`. The `string` is the parameter's name, and the `object` is the parameter's value.

In the below example, we used `Toast Service` to show the user confirmation.

<img src="https://i.imgur.com/yNv7Wvw.png" alt="Blazor Bootstrap: Confirm Dialog Component - Dynamic component as confirm dialog" />

```cshtml {1} showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Danger" @onclick="DeleteEmployeeAsync"> Delete Employee </Button>
```

```cs {2,11,13} showLineNumbers
@code {
    private ConfirmDialog dialog;

    [Inject] ToastService ToastService { get; set; }

    private async Task DeleteEmployeeAsync()
    {
        var parameters = new Dictionary<string, object>();
        parameters.Add("EmployeeId", 321);

        var confirmation = await dialog.ShowAsync<EmployeeDemoComponent>("Are you sure you want to delete this employee?", parameters);

        if (confirmation)
        {
            // call API to delete the employee
            // show acknowledgment to the user
            ToastService.Notify(new ToastMessage(ToastType.Success, $"Employee deleted successfully."));
        }
        else
            ToastService.Notify(new ToastMessage(ToastType.Secondary, $"Delete action canceled."));
    }
}
```

**EmployeeDemoComponent.razor**

```cshtml showLineNumbers
<div class="row">
    <div class="col-5 col-md-3 text-end">Employee Id :</div>
    <div class="col-7 col-md-9">@EmployeeId</div>
</div>
<div class="row">
    <div class="col-5 col-md-3 text-end">First Name :</div>
    <div class="col-7 col-md-9">@employee.FirstName</div>
</div>
<div class="row">
    <div class="col-5 col-md-3 text-end">Last Name :</div>
    <div class="col-7 col-md-9">@employee.LastName</div>
</div>

@code {
    private Employee employee;

    [Parameter] public int EmployeeId { get; set; }

    protected override void OnInitialized()
    {
        // get employee with {EmployeeId} from DB

        employee = new Employee { FirstName = "Vikram", LastName = "Reddy" };

        base.OnInitialized();
    }
}
```

[See Confirm Dialog demo here.](https://demos.blazorbootstrap.com/confirm-dialog#dynamic-component-as-confirm-dialog)

### Change buttons text and color

Use `ConfirmDialogOptions` to change the text and color of the button.

<img src="https://i.imgur.com/uH19DpG.png" alt="Blazor Bootstrap: Confirm Dialog Component - Change buttons text and color" />

```cshtml showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Primary" @onclick="ShowSaveConfirmationAsync"> Save Employee </Button>
```

```cs showLineNumbers
@code {
    private ConfirmDialog dialog;

    private async Task ShowSaveConfirmationAsync()
    {
        var options = new ConfirmDialogOptions
            {
                YesButtonText = "OK",
                YesButtonColor = ButtonColor.Success,
                NoButtonText = "CANCEL",
                NoButtonColor = ButtonColor.Danger
            };

        var confirmation = await dialog.ShowAsync(
            title: "Simple Confirm Dialog",
            message1: "Do you want to proceed?",
            confirmDialogOptions: options);

        if (confirmation)
        {
            // do whatever
        }
        else
        {
            // do whatever
        }
    }
}
```

[See Confirm Dialog demo here.](https://demos.blazorbootstrap.com/confirm-dialog#change-buttons-text-and-color)

### Optional sizes

Confirm dialog have three optional sizes. These sizes kick in at certain breakpoints to avoid horizontal scrollbars on narrower viewports.

**Confirm Dialog Component - Small Size**
<img src="https://i.imgur.com/RHYTaee.png" alt="Blazor Bootstrap: Confirm Dialog Component - Optional sizes - Small" />

**Confirm Dialog Component - Large Size**
<img src="https://i.imgur.com/pojAFvk.png" alt="Blazor Bootstrap: Confirm Dialog Component - Optional sizes - Large" />

**Confirm Dialog Component - Extra Large Size**
<img src="https://i.imgur.com/PMz3lbn.png" alt="Blazor Bootstrap: Confirm Dialog Component - Optional sizes - Extra Large" />

```cshtml showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Primary" @onclick="() => ShowConfirmationAsync(DialogSize.Small)"> Small Confirm Dialog </Button>
<Button Color="ButtonColor.Primary" @onclick="() => ShowConfirmationAsync(DialogSize.Large)"> Large Confirm Dialog </Button>
<Button Color="ButtonColor.Primary" @onclick="() => ShowConfirmationAsync(DialogSize.ExtraLarge)"> Extra Large Confirm Dialog </Button>
```

```cs showLineNumbers
@code {
    private ConfirmDialog dialog;

    private async Task ShowConfirmationAsync(DialogSize size)
    {
        var options = new ConfirmDialogOptions { Size = size };

        var confirmation = await dialog.ShowAsync(
            title: "Simple Confirm Dialog",
            message1: "Do you want to proceed?",
            confirmDialogOptions: options);

        if (confirmation)
        {
            // do whatever
        }
        else
        {
            // do whatever
        }
    }
}
```

[See Confirm Dialog demo here.](https://demos.blazorbootstrap.com/confirm-dialog#optional-sizes)

### Scrolling long content

When dialogs become too long for the user's viewport or device, they scroll independent of the page itself. Try the demo below to see what we mean.

<img src="https://i.imgur.com/8P6UejF.png" alt="Blazor Bootstrap: Confirm Dialog Component - Scrolling long content" />

```cshtml showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Primary" @onclick="ShowDialogAsync"> Launch Confirm Dialog </Button>
```

```cs showLineNumbers
@code {
    private ConfirmDialog dialog;

    private async Task ShowDialogAsync()
    {
        var confirmation = await dialog.ShowAsync<LongContentDemoComponent>(title: "Confirm dialog title");

        if (confirmation)
        {
            // do whatever
        }
        else
        {
            // do whatever
        }
    }
}
```

You can also create a scrollable dialog that allows scroll the dialog body by updating `DialogOptions.IsScrollable="true"`.

<img src="https://i.imgur.com/kJdSffq.png" alt="Blazor Bootstrap: Confirm Dialog Component - Scrolling long content within the body" />

```cshtml showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Primary" @onclick="ShowDialogAsync"> Launch Confirm Dialog </Button>
```

```cs showLineNumbers
@code {
    private ConfirmDialog dialog;

    private async Task ShowDialogAsync()
    {
        var options = new ConfirmDialogOptions { IsScrollable = true };
        var confirmation = await dialog.ShowAsync<LongContentDemoComponent>(
            title: "Confirm dialog title",
            confirmDialogOptions: options);

        if (confirmation)
        {
            // do whatever
        }
        else
        {
            // do whatever
        }
    }
}
```

[See Confirm Dialog demo here.](https://demos.blazorbootstrap.com/confirm-dialog#scrolling-long-content)

### Vertically centered

Add `DialogOptions.IsVerticallyCentered="true"` to vertically center the confirm dialog.

<img src="https://i.imgur.com/MjueRsB.png" alt="Blazor Bootstrap: Confirm Dialog Component - Vertically centered" />

```cshtml showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Primary" @onclick="ShowDialogAsync"> Launch Vertically Centered Confirm Dialog </Button>
```

```cs showLineNumbers
@code {
    private ConfirmDialog dialog;

    private async Task ShowDialogAsync()
    {
        var options = new ConfirmDialogOptions { IsVerticallyCentered = true };
        var confirmation = await dialog.ShowAsync(
            title: "Simple Confirm Dialog",
            message1: "Do you want to proceed?",
            confirmDialogOptions: options);

        if (confirmation)
        {
            // do whatever
        }
        else
        {
            // do whatever
        }
    }
}
```

You can also create a scrollable dialog that allows scroll the dialog body by updating DialogOptions.IsScrollable="true".

```cshtml showLineNumbers
<ConfirmDialog @ref="dialog" />

<Button Color="ButtonColor.Primary" @onclick="ShowDialogAsync"> Launch Scrollable & Vertically Centered Confirm Dialog </Button>

```

```cs showLineNumbers
@code {
    private ConfirmDialog dialog;

    private async Task ShowDialogAsync()
    {
        var options = new ConfirmDialogOptions { IsScrollable = true, IsVerticallyCentered = true };
        var confirmation = await dialog.ShowAsync<LongContentDemoComponent>(title: "Confirm dialog title",
            confirmDialogOptions: options);

        if (confirmation)
        {
            // do whatever
        }
        else
        {
            // do whatever
        }
    }
}
```

[See Confirm Dialog demo here.](https://demos.blazorbootstrap.com/confirm-dialog#vertically-centered)