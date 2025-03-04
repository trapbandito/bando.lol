-- Load UI Library
local library = loadstring(game:HttpGet("https://pastebin.com/raw/someUILibrary"))()

-- Create Main Window
local window = library:window({ 
    name = "Modern Dark GUI", 
    size = UDim2.fromOffset(550, 600), 
    theme = "Dark", 
})

-- Create Tabs
local homeTab = window:tab({name = "Home"})
local featuresTab = window:tab({name = "Features"})
local settingsTab = window:tab({name = "Settings"})

-- Home Tab Content
local homeSection = homeTab:section({name = "Welcome", side = "left"})
homeSection:label({name = "Welcome to the GUI!"})

-- Features Tab Content
local featuresSection = featuresTab:section({name = "Main Features", side = "left"})
featuresSection:button({
    name = "Feature 1",
    callback = function()
        print("Feature 1 activated!")
    end
})

-- Settings Tab Content
local settingsSection = settingsTab:section({name = "Customization"})
settingsSection:toggle({
    name = "Enable Dark Mode",
    default = true,
    callback = function(state)
        print("Dark Mode: ", state)
    end
})

-- UI Toggle Keybind
settingsSection:keybind({
    name = "Toggle UI",
    default = Enum.KeyCode.RightShift,
    callback = function()
        window:toggle()
    end
})
