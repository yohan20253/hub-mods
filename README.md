-- Cria a GUI principal
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local OpenCloseButton = Instance.new("TextButton")
local SpeedButton = Instance.new("TextButton")
local JumpButton = Instance.new("TextButton")
local NoclipButton = Instance.new("TextButton")

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.Name = "CheatGui"

MainFrame.Size = UDim2.new(0, 250, 0, 200)
MainFrame.Position = UDim2.new(0.5, -125, 0.5, -100)
MainFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)
MainFrame.Visible = true
MainFrame.Parent = ScreenGui

OpenCloseButton.Size = UDim2.new(0, 80, 0, 30)
OpenCloseButton.Position = UDim2.new(0, 10, 0, 10)
OpenCloseButton.Text = "Fechar"
OpenCloseButton.Parent = MainFrame

SpeedButton.Size = UDim2.new(0, 200, 0, 30)
SpeedButton.Position = UDim2.new(0, 25, 0, 50)
SpeedButton.Text = "Velocidade (Speed)"
SpeedButton.Parent = MainFrame

JumpButton.Size = UDim2.new(0, 200, 0, 30)
JumpButton.Position = UDim2.new(0, 25, 0, 90)
JumpButton.Text = "Pulo Alto (Jump)"
JumpButton.Parent = MainFrame

NoclipButton.Size = UDim2.new(0, 200, 0, 30)
NoclipButton.Position = UDim2.new(0, 25, 0, 130)
NoclipButton.Text = "Noclip"
NoclipButton.Parent = MainFrame

-- Função para abrir/fechar
OpenCloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    -- Botão para reabrir
    local reopen = Instance.new("TextButton")
    reopen.Size = UDim2.new(0, 80, 0, 30)
    reopen.Position = UDim2.new(0, 10, 0, 10)
    reopen.Text = "Abrir"
    reopen.Parent = ScreenGui
    reopen.MouseButton1Click:Connect(function()
        MainFrame.Visible = true
        reopen:Destroy()
    end)
end)

-- Cheat: Velocidade
SpeedButton.MouseButton1Click:Connect(function()
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100 -- padrão é 16
end)

-- Cheat: Pulo Alto
JumpButton.MouseButton1Click:Connect(function()
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = 150 -- padrão é 50
end)

-- Cheat: Noclip
local noclip = false
NoclipButton.MouseButton1Click:Connect(function()
    noclip = not noclip
    NoclipButton.Text = noclip and "Noclip (Ativo)" or "Noclip"
end)

game:GetService("RunService").Stepped:Connect(function()
    if noclip then
        for _,v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
            if v:IsA("BasePart") and v.CanCollide == true then
                v.CanCollide = false
            end
        end
    end
end)# hub-mods
