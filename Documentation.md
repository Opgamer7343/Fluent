# Fluent Library
This documentation is for Fluent Library (a roblox gui library helps you create gui's.)

## Booting the Library
```lua
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
```

## Creating a Window
```lua
local Window = Fluent:CreateWindow({
    Title = "Fluent "..Fluent.Version,
    SubTitle = "by dawid",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, 
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl
})

--[[
Title = <string> - The name of the window.
SubTitle = <string> - The subtitle displayed.
TabWidth = <number> - The width of the tab.
Size = <UDim2> - Size of the window.
Acrylic = <bool> - Enables or disables window blur.
Theme = <string> - The theme of the window ("Dark" or "Light").
MinimizeKey = <Enum.KeyCode> - Key to minimize the window.
]]
```

## Creating a Tab
```lua
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

--[[
Title = <string> - The title of the tab.
Icon = <string> - The icon for the tab (optional).
]]
```

## Notifying the User
```lua
Fluent:Notify({
    Title = "Notification",
    Content = "This is a notification",
    SubContent = "Optional subcontent", 
    Duration = 5
})

--[[
Title = <string> - The title of the notification.
Content = <string> - The main content of the notification.
SubContent = <string> - Optional subcontent of the notification.
Duration = <number> - Duration in seconds. Set to nil for no expiration.
]]
```

## Creating a Button
```lua
Tabs.Main:AddButton({
    Title = "Button",
    Description = "Very important button",
    Callback = function()
        Window:Dialog({
            Title = "Dialog Title",
            Content = "This is a dialog.",
            Buttons = {
                {
                    Title = "Confirm",
                    Callback = function()
                        print("Confirmed the dialog.")
                    end
                },
                {
                    Title = "Cancel",
                    Callback = function()
                        print("Cancelled the dialog.")
                    end
                }
            }
        })
    end
})

--[[
Title = <string> - The name of the button.
Description = <string> - Description for the button.
Callback = <function> - The function executed when the button is clicked.
]]
```

## Creating a Toggle
```lua
local Toggle = Tabs.Main:AddToggle("MyToggle", { Title = "Toggle", Default = false })
Toggle:OnChanged(function()
    print("Toggle changed:", Options.MyToggle.Value)
end)
Options.MyToggle:SetValue(false)

--[[
Title = <string> - The name of the toggle.
Default = <bool> - The default state of the toggle.
]]
```

## Creating a Slider
```lua
local Slider = Tabs.Main:AddSlider("Slider", {
    Title = "Slider",
    Description = "This is a slider",
    Default = 2,
    Min = 0,
    Max = 5,
    Rounding = 1,
    Callback = function(Value)
        print("Slider was changed:", Value)
    end
})
Slider:SetValue(3)

--[[
Title = <string> - The name of the slider.
Min = <number> - The minimum value of the slider.
Max = <number> - The maximum value of the slider.
Rounding = <number> - Rounding precision for the slider.
]]
```

## Creating a Dropdown
```lua
local Dropdown = Tabs.Main:AddDropdown("Dropdown", {
    Title = "Dropdown",
    Values = {"one", "two", "three"},
    Multi = false,
    Default = 1
})

Dropdown:SetValue("two")
Dropdown:OnChanged(function(Value)
    print("Dropdown changed:", Value)
end)

--[[
Title = <string> - The name of the dropdown.
Values = <table> - The list of values.
Multi = <bool> - Allows multiple selections if true.
Default = <string> - The default selected value.
]]
```

## Using the SaveManager and InterfaceManager
```lua
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)

SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({})

InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)

SaveManager:LoadAutoloadConfig()
```

## idk
```lua
Window:SelectTab(1)

Fluent:Notify({
    Title = "Fluent",
    Content = "The script has been loaded.",
    Duration = 8
})
```

--- 

This structured guide should help in understanding the Fluent library.
