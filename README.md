local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local TitleLabel = Instance.new("TextLabel")
local PowerBox = Instance.new("TextBox")
local JumpPowerButton = Instance.new("TextButton")
local WalkSpeedButton = Instance.new("TextButton")
local PlayerNameBox = Instance.new("TextBox")
local TeleportButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui
MainFrame.Parent = ScreenGui
MainFrame.Size = UDim2.new(0, 350, 0, 400)
MainFrame.Position = UDim2.new(0.5, -175, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MainFrame.BackgroundTransparency = 0.2

UICorner.Parent = MainFrame
UICorner.CornerRadius = UDim.new(0, 15)

TitleLabel.Parent = MainFrame
TitleLabel.Size = UDim2.new(1, -20, 0, 40)
TitleLabel.Position = UDim2.new(0, 10, 0, 10)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "Bazuka Hub | Natural Disaster"
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.TextSize = 18
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextXAlignment = Enum.TextXAlignment.Left

PowerBox.Parent = MainFrame
PowerBox.Size = UDim2.new(1, -20, 0, 40)
PowerBox.Position = UDim2.new(0, 10, 0, 60)
PowerBox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
PowerBox.PlaceholderText = "Digite um valor (ex: 50)"
PowerBox.TextColor3 = Color3.fromRGB(255, 255, 255)
PowerBox.TextSize = 16

JumpPowerButton.Parent = MainFrame
JumpPowerButton.Size = UDim2.new(1, -20, 0, 40)
JumpPowerButton.Position = UDim2.new(0, 10, 0, 110)
JumpPowerButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
JumpPowerButton.Text = "Set Jump Power"
JumpPowerButton.TextColor3 = Color3.fromRGB(255, 255, 255)
JumpPowerButton.TextSize = 16

WalkSpeedButton.Parent = MainFrame
WalkSpeedButton.Size = UDim2.new(1, -20, 0, 40)
WalkSpeedButton.Position = UDim2.new(0, 10, 0, 160)
WalkSpeedButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
WalkSpeedButton.Text = "Set Walk Speed"
WalkSpeedButton.TextColor3 = Color3.fromRGB(255, 255, 255)
WalkSpeedButton.TextSize = 16

PlayerNameBox.Parent = MainFrame
PlayerNameBox.Size = UDim2.new(1, -20, 0, 40)
PlayerNameBox.Position = UDim2.new(0, 10, 0, 210)
PlayerNameBox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
PlayerNameBox.PlaceholderText = "Digite o nome do jogador"
PlayerNameBox.TextColor3 = Color3.fromRGB(255, 255, 255)
PlayerNameBox.TextSize = 16

TeleportButton.Parent = MainFrame
TeleportButton.Size = UDim2.new(1, -20, 0, 40)
TeleportButton.Position = UDim2.new(0, 10, 0, 260)
TeleportButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
TeleportButton.Text = "Teleport to Player"
TeleportButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TeleportButton.TextSize = 16

local function checkAdmins()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player:GetRankInGroup(123456) >= 200 then
            return true
        end
    end
    return false
end

JumpPowerButton.MouseButton1Click:Connect(function()
    if checkAdmins() then return end
    local value = tonumber(PowerBox.Text)
    if value and value > 0 then
        local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.UseJumpPower = true
            humanoid.JumpPower = value
        end
    end
end)

WalkSpeedButton.MouseButton1Click:Connect(function()
    if checkAdmins() then return end
    local value = tonumber(PowerBox.Text)
    if value and value > 0 then
        local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = value
        end
    end
end)

TeleportButton.MouseButton1Click:Connect(function()
    if checkAdmins() then return end
    local targetName = PlayerNameBox.Text
    local targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
    end
end)
