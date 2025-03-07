local function randomWait()
    task.wait(math.random(1, 3) * 0.1)
end

local function checkAdmins()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player:GetRankInGroup(123456) >= 200 then
            return true
        end
    end
    return false
end

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local AutoFarmButton = Instance.new("TextButton")
local FlyButton = Instance.new("TextButton")
local SpeedButton = Instance.new("TextButton")
local GodModeButton = Instance.new("TextButton")
local TitleLabel = Instance.new("TextLabel")
local ToggleButton = Instance.new("ImageButton")

ScreenGui.Parent = game.CoreGui
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 280, 0, 350)
Frame.Position = UDim2.new(0, 50, 0, 50)
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.BackgroundTransparency = 0.4
UICorner.Parent = Frame

local gradient = Instance.new("UIGradient")
gradient.Parent = Frame
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(50, 50, 50)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(70, 70, 70)),
})
gradient.Rotation = 45

TitleLabel.Parent = Frame
TitleLabel.Size = UDim2.new(0, 240, 0, 40)
TitleLabel.Position = UDim2.new(0, 20, 0, 10)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "Bazuka Hub - Natural Disaster"
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.TextSize = 20
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextAlignment = Enum.TextAlignment.Center

ToggleButton.Parent = Frame
ToggleButton.Size = UDim2.new(0, 50, 0, 50)
ToggleButton.Position = UDim2.new(0, 115, 0, 300)
ToggleButton.Image = "https://www.roblox.com/asset/?id=105882266197529"
ToggleButton.BackgroundTransparency = 1

local scriptActive = true
local panelVisible = true

local function createButton(name, text, position)
    local button = Instance.new("TextButton")
    button.Parent = Frame
    button.Size = UDim2.new(0, 240, 0, 40)
    button.Position = UDim2.new(0, 20, 0, position)
    button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 18
    button.Text = text
    button.Font = Enum.Font.GothamBold
    button.BackgroundTransparency = 0.2
    button.AutoButtonColor = false
    
    local UICornerButton = Instance.new("UICorner")
    UICornerButton.Parent = button
    UICornerButton.CornerRadius = UDim.new(0, 10)
    
    button.MouseEnter:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
    end)

    button.MouseLeave:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    end)
    
    return button
end

AutoFarmButton = createButton("AutoFarmButton", "Auto Farm", 70)
FlyButton = createButton("FlyButton", "Fly", 120)
SpeedButton = createButton("SpeedButton", "Speed Hack", 170)
GodModeButton = createButton("GodModeButton", "God Mode", 220)

AutoFarmButton.MouseButton1Click:Connect(function()
    if not scriptActive or checkAdmins() then return end
    randomWait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-300 + math.random(-5,5), 500, math.random(-5,5))
end)

local flying = false
FlyButton.MouseButton1Click:Connect(function()
    if not scriptActive or checkAdmins() then return end
    randomWait()
    flying = not flying
    local player = game.Players.LocalPlayer
    local char = player.Character or player.CharacterAdded:Wait()
    local humanoid = char:FindFirstChildOfClass("Humanoid")
    
    if flying then
        humanoid.PlatformStand = true
        local fly = Instance.new("BodyVelocity", char.HumanoidRootPart)
        fly.Velocity = Vector3.new(0, 40 + math.random(5, 10), 0)
        fly.Name = "FlyVelocity"
    else
        if char.HumanoidRootPart:FindFirstChild("FlyVelocity") then
            char.HumanoidRootPart.FlyVelocity:Destroy()
        end
        humanoid.PlatformStand = false
    end
end)

SpeedButton.MouseButton1Click:Connect(function()
    if not scriptActive or checkAdmins() then return end
    randomWait()
    local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if humanoid then
        humanoid.WalkSpeed = 90 + math.random(5, 15)
    end
end)

GodModeButton.MouseButton1Click:Connect(function()
    if not scriptActive or checkAdmins() then return end
    randomWait()
    local char = game.Players.LocalPlayer.Character
    if char then
        for _, v in pairs(char:GetChildren()) do
            if v:IsA("Humanoid") then
                local spoofed = v:Clone()
                spoofed.Parent = char
                spoofed.Name = "FakeHumanoid_"..math.random(1000,9999)
                v.Name = "GodMode_"..math.random(1000,9999)
            end
        end
    end
end)

ToggleButton.MouseButton1Click:Connect(function()
    panelVisible = not panelVisible
    Frame.Visible = panelVisible
end)

local dragToggle = nil
local dragSpeed = 0.25
local dragInput, dragStart, startPos

local function update(input)
    local delta = input.Position - dragStart
    Frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

Frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragToggle = true
        dragStart = input.Position
        startPos = Frame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragToggle = false
            end
        end)
    end
end)

Frame.InputChanged:Connect(function(input)
    if dragToggle and input.UserInputType == Enum.UserInputType.MouseMovement then
        update(input)
    end
end)

task.spawn(function()
    while true do
        if checkAdmins() then
            ScreenGui:Destroy()
            return
        end
        task.wait(5)
    end
end)
