local ScreenGui = Instance.new("ScreenGui")
local BanFrame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local TitleLabel = Instance.new("TextLabel")
local ReasonLabel = Instance.new("TextLabel")
local AppealButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui

BanFrame.Parent = ScreenGui
BanFrame.Size = UDim2.new(0, 400, 0, 250)
BanFrame.Position = UDim2.new(0.5, -200, 0.5, -125)
BanFrame.BackgroundColor3 = Color3.fromRGB(170, 0, 0)
BanFrame.BackgroundTransparency = 0.1

UICorner.Parent = BanFrame
UICorner.CornerRadius = UDim.new(0, 15)

TitleLabel.Parent = BanFrame
TitleLabel.Size = UDim2.new(1, -20, 0, 50)
TitleLabel.Position = UDim2.new(0, 10, 0, 10)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "Você foi banido permanente,  mensagem da equipe: você é muito burro, temos anti-exploit"
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.TextSize = 22
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextXAlignment = Enum.TextXAlignment.Center

ReasonLabel.Parent = BanFrame
ReasonLabel.Size = UDim2.new(1, -20, 0, 80)
ReasonLabel.Position = UDim2.new(0, 10, 0, 60)
ReasonLabel.BackgroundTransparency = 1
ReasonLabel.Text = "Motivo: Exploitação de sistema\nDuração: Permanente\nID de Ban: #"..math.random(100000, 999999)
ReasonLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
ReasonLabel.TextSize = 18
ReasonLabel.Font = Enum.Font.Gotham
ReasonLabel.TextXAlignment = Enum.TextXAlignment.Center
ReasonLabel.TextYAlignment = Enum.TextYAlignment.Top

AppealButton.Parent = BanFrame
AppealButton.Size = UDim2.new(1, -40, 0, 40)
AppealButton.Position = UDim2.new(0, 20, 0, 160)
AppealButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
AppealButton.Text = "Apelar Banimento"
AppealButton.TextColor3 = Color3.fromRGB(255, 255, 255)
AppealButton.TextSize = 18
AppealButton.Font = Enum.Font.GothamBold

local UICornerButton = Instance.new("UICorner")
UICornerButton.Parent = AppealButton
UICornerButton.CornerRadius = UDim.new(0, 10)

AppealButton.MouseButton1Click:Connect(function()
    ReasonLabel.Text = "Seu apelo foi rejeitado."
    AppealButton.Text = "Indo para a tela inicial..."
    task.wait(3)
    BanFrame.Visible = false
end)

task.wait(10)
BanFrame.Visible = false
