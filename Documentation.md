## Booting the Library
```lua
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
```



## Creating the Main Window
```lua
local Window = Fluent:CreateWindow({
    Title = "Fluent " .. Fluent.Version,
    SubTitle = "by dawid",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl
})
```

## Add Tab
```lua
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}
```


## Notification
```lua
Fluent:Notify({
    Title = "Notification",
    Content = "This is a notification",
    SubContent = "SubContent",
    Duration = 5
})
```




## Add Paragraph
```lua
Tabs.Main:AddParagraph({
    Title = "Paragraph",
    Content = "This is a paragraph.\nSecond line!"
})
```



## Add Button
```lua
Tabs.Main:AddButton({
    Title = "Button",
    Description = "Very important button",
    Callback = function()
        Window:Dialog({
            Title = "Title",
            Content = "This is a dialog",
            Buttons = {
                { Title = "Confirm", Callback = function() print("Confirmed the dialog.") end },
                { Title = "Cancel", Callback = function() print("Cancelled the dialog.") end }
            }
        })
    end
})
```





## Add Toggle Button
```lua
local Toggle = Tabs.Main:AddToggle("MyToggle", {Title = "Toggle", Default = false })
Toggle:OnChanged(function() print("Toggle changed:", Options.MyToggle.Value) end)
Options.MyToggle:SetValue(false)
```


## Add a slider
```lua
local Slider = Tabs.Main:AddSlider("Slider", {
    Title = "Slider",
    Description = "This is a slider",
    Default = 2,
    Min = 0,
    Max = 5,
    Rounding = 1,
    Callback = function(Value) print("Slider was changed:", Value) end
})
Slider:OnChanged(function(Value) print("Slider changed:", Value) end)
Slider:SetValue(3)
```



## Add Dropdown
```lua
local Dropdown = Tabs.Main:AddDropdown("Dropdown", {
    Title = "Dropdown",
    Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},
    Multi = false,
    Default = 1,
})
Dropdown:SetValue("four")
Dropdown:OnChanged(function(Value) print("Dropdown changed:", Value) end)
```




# Add Multi-Select Dropdown 
```lua
local MultiDropdown = Tabs.Main:AddDropdown("MultiDropdown", {
    Title = "Dropdown",
    Description = "You can select multiple values.",
    Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},
    Multi = true,
    Default = {"seven", "twelve"},
})
MultiDropdown:SetValue({ three = true, five = true, seven = false })
MultiDropdown:OnChanged(function(Value)
    local Values = {}
    for Value, State in next, Value do
        table.insert(Values, Value)
    end
    print("Mutlidropdown changed:", table.concat(Values, ", "))
end)
```






## Add ColorPicker
```lua
local Colorpicker = Tabs.Main:AddColorpicker("Colorpicker", {
    Title = "Colorpicker",
    Default = Color3.fromRGB(96, 205, 255)
})
Colorpicker:OnChanged(function() print("Colorpicker changed:", Colorpicker.Value) end)
Colorpicker:SetValueRGB(Color3.fromRGB(0, 255, 140))
```




## Keybind idk
```lua
local Keybind = Tabs.Main:AddKeybind("Keybind", {
    Title = "KeyBind",
    Mode = "Toggle",
    Default = "LeftControl",
    Callback = function(Value) print("Keybind clicked!", Value) end,
    ChangedCallback = function(New) print("Keybind changed!", New) end
})
Keybind:OnClick(function() print("Keybind clicked:", Keybind:GetState()) end)
```






## Input Field idk
```lua
local Input = Tabs.Main:AddInput("Input", {
    Title = "Input",
    Default = "Default",
    Placeholder = "Placeholder",
    Numeric = false,
    Finished = false,
    Callback = function(Value) print("Input changed:", Value) end
})
Input:OnChanged(function() print("Input updated:", Input.Value) end)
```





## Addons
```lua
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({})
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")
InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)
```







## Tab Selection and Notification idk 
```lua
Window:SelectTab(1)
Fluent:Notify({
    Title = "Fluent",
    Content = "The script has been loaded.",
    Duration = 8
})
```





## Loading Configuration 
```lua

SaveManager:LoadAutoloadConfig()
```
