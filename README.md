local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("CoreGui")

local function createESP(player, color)
    local highlight = Instance.new("Highlight")
    highlight.FillColor = color
    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
    highlight.Parent = CoreGui
    highlight.Adornee = player.Character
end

local function onPlayerAdded(player)
    player.CharacterAdded:Connect(function(character)
        local role = "Innocent" -- Default role
        -- Aqui você pode adicionar a lógica para determinar o papel do jogador
        if player.Name == "NomeDoAssassino" then
            role = "Murderer"
        elseif player.Name == "NomeDoXerife" then
            role = "Sheriff"
        end

        if role == "Murderer" then
            createESP(player, Color3.fromRGB(255, 0, 0)) -- Vermelho para assassino
        elseif role == "Sheriff" then
            createESP(player, Color3.fromRGB(0, 0, 255)) -- Azul para xerife
        else
            createESP(player, Color3.fromRGB(0, 255, 0)) -- Verde para inocentes
        end
    end)
end

Players.PlayerAdded:Connect(onPlayerAdded)
for _, player in pairs(Players:GetPlayers()) do
    onPlayerAdded(player)
end

