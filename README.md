-- God Mode Function
local function godMode(player)
    local humanoid = player.Character:WaitForChild("Humanoid")
    humanoid.MaxHealth = math.huge
    humanoid.Health = math.huge
    print(player.Name .. " está em God Mode!")
end

-- ESP Function
local function createESP(player)
    local highlight = Instance.new("BoxHandleAdornment")
    highlight.Adornee = player.Character:WaitForChild("HumanoidRootPart")
    highlight.Size = player.Character.HumanoidRootPart.Size + Vector3.new(2, 2, 2)
    highlight.Color3 = Color3.new(1, 0, 0)
    highlight.Transparency = 0.5
    highlight.AlwaysOnTop = true
    highlight.ZIndex = 10
    highlight.Parent = player.Character.HumanoidRootPart
    print("ESP ativado para " .. player.Name)
end

-- Aimbot Function
local function aimbot(player)
    local mouse = player:GetMouse()
    local closestPlayer = nil
    local shortestDistance = math.huge

    for _, targetPlayer in pairs(game.Players:GetPlayers()) do
        if targetPlayer ~= player and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
            local targetPos = targetPlayer.Character.HumanoidRootPart.Position
            local distance = (mouse.Hit.p - targetPos).Magnitude
            if distance < shortestDistance then
                closestPlayer = targetPlayer
                shortestDistance = distance
            end
        end
    end

    if closestPlayer then
        local aimAt = closestPlayer.Character.HumanoidRootPart.Position
        player.Character:WaitForChild("Humanoid").CFrame = CFrame.lookAt(player.Character.HumanoidRootPart.Position, aimAt)
        print("Aimbot ativado, mirando em " .. closestPlayer.Name)
    end
end

-- Menu para chamar as funções
local player = game.Players.LocalPlayer

-- Ativar God Mode
godMode(player)

-- Ativar ESP para todos os jogadores
for _, otherPlayer in pairs(game.Players:GetPlayers()) do
    if otherPlayer ~= player then
        createESP(otherPlayer)
    end
end

-- Ativar Aimbot
aimbot(player)
