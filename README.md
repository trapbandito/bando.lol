-- Juju.lol Remake
-- Dark-themed modern GUI with Aimlock & ESP

local GuiLibrary = loadstring(game:HttpGet("https://raw.githubusercontent.com/someone/gui-framework/main.lua", true))()

if not GuiLibrary then
    warn("Failed to load GUI Library")
    return
end

local Window = GuiLibrary:CreateWindow("Juju.lol Remake", "Dark Mode")
local AimlockTab = Window:CreateTab("Aimlock")
local ESPTab = Window:CreateTab("ESP")

-- Aimlock Functionality
local aimlockEnabled = false
local aimlockKey = Enum.KeyCode.E

game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == aimlockKey then
        aimlockEnabled = not aimlockEnabled
    end
end)

function Aimlock()
    while aimlockEnabled do
        local target = GetNearestTarget()
        if target then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = target.CFrame
        end
        wait(0.1)
    end
end

function GetNearestTarget()
    local closest, distance = nil, math.huge
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local mag = (player.Character.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude
            if mag < distance then
                closest = player.Character.HumanoidRootPart
                distance = mag
            end
        end
    end
    return closest
end

-- ESP Functionality
local espEnabled = false
local espColor = Color3.fromRGB(255, 0, 0)

function ToggleESP()
    espEnabled = not espEnabled
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local highlight = Instance.new("Highlight")
            highlight.Parent = player.Character
            highlight.FillColor = espColor
            highlight.OutlineTransparency = 0.5
        end
    end
end

AimlockTab:CreateToggle("Enable Aimlock", false, function(state)
    aimlockEnabled = state
    if state then
        Aimlock()
    end
end)

ESPTab:CreateToggle("Enable ESP", false, function(state)
    espEnabled = state
    ToggleESP()
end)
